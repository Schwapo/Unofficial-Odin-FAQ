# Nesting  TabGroups

Nesting [TabGroups] correctly requires you to know how [Nesting Groups] works in general and how [TabGroups] differ from normal groups. The first thing you need to know is that there are two different overloads of the [TabGroup] constructor. 

---

The first one looks like this:

```CSharp
public TabGroupAttribute(
	string tab, bool useFixedHeight = false, float order = 0f)
   	: this("_DefaultTabGroup", tab, useFixedHeight, order)
```

Usually you only provide the *tab* parameter which decides how the tab is named and referenced when nesting. As you can see we call the base constructor and pass *_DefaultTabGroup* as the group name. This results in the final group path `#!CSharp "_DefaultTabGroup/TabInsideTheFirstGroup"`

```CSharp
[TabGroup("TabInsideTheFirstGroup")]
public float SomeField;
```

If you now want to nest another [TabGroup] inside this group you will have to provide the full path of the previous group and add the new group name to it.

```CSharp
[TabGroup("_DefaultTabGroup/TabInsideTheFirstGroup/SecondTabGroup", "TabInsideTheSecondGroup")]
public float SomeOtherField;
```

---

The second constructor looks like this:

```CSharp
public TabGroupAttribute(
	string group, string tab, bool useFixedHeight = false, float order = 0f)
	: base(group, order)
```

This constructor allows you to pass in a group name to use instead of *_DefaultTabGroup*. I would recommend to always use this way to define a tab group as it makes it easier to understand. Now, instead of using *_DefaultTabGroup* when nesting your group use your provided group name.

```CSharp
[TabGroup("FirstGroup", "TabInsideFirstGroup")]
public float SomeField;

[TabGroup("FirstGroup/TabInsideFirstGroup/SecondGroup", "TabInsideSecondGroup")]
public float SomeOtherField;
```

---

> If you have missing or duplicate elements, make sure to check your group path this is a sign that you did not nest your group correctly.










[Nesting Groups]: nesting-groups.md
[TabGroup]: https://www.odininspector.com/attributes/tab-group-attribute
[TabGroups]: https://www.odininspector.com/attributes/tab-group-attribute
