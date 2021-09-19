# Nesting Groups

Groups are nested like folder paths. For example If you want to nest a [HorizontalGroup] inside a [BoxGroup] you do:

```CSharp
[BoxGroup("Box")]
public float SomeField;

[HorizontalGroup("Box/Horizontal")]
public float SomeOtherField;
```

```
📁 Box
└─ 📁 Horizontal

```

Visualizing it like this also shows that you always have to create the previous "folder" since you cannot create a folder inside another folder that doesn't exist. That doesn't mean that the group attribute needs to be before other groups that are nested inside of it as order doesn't matter when defining groups. It just means that it needs to exist somewhere inside this file.

```CSharp
// Error since the SomeGroupName "folder" doesn't exist
[HorizontalGroup("SomeGroupName/Horizontal")]
public float AnotherField;
```

---

If you create a nested group path and the previous "folder" doesn't exist you get an exception like this:
> Group attribute 'HorizontalGroupAttribute' on member 'AnotherField' expected a group with the name 'SomeGroupName' to exist in declaring type 'SomeMonoBehaviour'. Its ID was 'SomeGroupName/Horizontal'.

---

<br/>

[Nesting TabGroups] has a slightly different behaviour you can learn about it [here]









[Nesting TabGroups]: nesting-tab-groups.md
[BoxGroup]: https://www.odininspector.com/attributes/box-group-attribute
[HorizontalGroup]: https://www.odininspector.com/attributes/horizontal-group-attribute
[here]: nesting-tab-groups.md 