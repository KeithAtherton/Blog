---
title: "Power App Gallery Control / ForAll Gotcha"
subtitle: A Power App Gallery Control / ForAll gotcha and how to handle it
date: 2023-05-05
tags: ["PowerApps"]
---

Recently, I came across a Power App gallery control / ForAll gotcha which I managed to handle so I'm sharing this here in case anyone else experiences the same issue.

OK, let's set the scene: It's a sunny Thursday afternoon in May in central Scotland. The *hero* is working on a Power App, and binds the following collection (colItems) to a gallery control:

```
ClearCollect(colItems,
    {
        ID:1,
        Name:"Dog"
    },
    {
        ID:2,
        Name:"Cat"
    },
    {
        ID:3,
        Name:"Rabbit"
    }
);
```

|![Power App gallery control showing a collection of data.](/img/2023-05-05-power-app-gallery-forall-gotcha/power-app-gallery.png "Power App gallery control showing a collection of data.")|
|-|

Great, the gallery is showing the data collection as expected!

Next up, I click a button which performs the following:

```
Clear(colTest1);

ForAll(galItems.AllItems,
    Collect(colTest1,
        {
            ID: txtID.Text,
            Name: txtName.Text
        }
    );
);
```

|![colTest1 data.](/img/2023-05-05-power-app-gallery-forall-gotcha/colTest1.png "colTest1 data.")|
|-|

Cool, the colTest1 collection data looks good.

You know what, I want to use the [As operator](https://learn.microsoft.com/en-us/power-platform/power-fx/reference/operators#as-operator) to alias each record as "locItem" to make future code easier to read when it becomes more complex later on. Let's do that:

```
Clear(colTest2);

ForAll(galItems.AllItems As locItem,
    Collect(colTest2,
        {
            ID: txtID.Text,
            Name: txtName.Text
        }
    );
);
```

|![colTest2 data.](/img/2023-05-05-power-app-gallery-forall-gotcha/colTest2.png "colTest2 data.")|
|-|

Woah, hang on! That's not what I was expecting - the first record has been repeated!?

OK, let's try a different approach: we'll use the [With function](https://learn.microsoft.com/en-us/power-platform/power-fx/reference/function-with) to alias the record as "locItem" instead:

```
Clear(colTest3);

ForAll(galItems.AllItems,
    With(
        {
            locItem:ThisRecord
        },
        Collect(colTest3,
            {
                ID: txtID.Text,
                Name: txtName.Text
            }
        );
    );
);
```

|![colTest3 data.](/img/2023-05-05-power-app-gallery-forall-gotcha/colTest3.png "colTest3 data.")|
|-|

Yup, that's now working as expected!

## Notes

This issue was experienced in a real-world app and manifested itself further downstream, and was traced back to the gallery control / ForAll code similar to this example.

However, please note that this walkthrough of the issue and solution has been intentionally stripped-back to remove any "noise" and keep it easy to follow along with.

The real-world app had a requirement to access all gallery control items as well as text input control values, and involved extra code.

Hope this helps if you experience something similar!