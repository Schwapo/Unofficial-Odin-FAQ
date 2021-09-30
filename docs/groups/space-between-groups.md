{% include "../links.txt" %}
[nest]: nesting-groups.md

# Space Between Groups

As of now the [VerticalGroup] is the only group that has parameters to add vertical spacing. In order to add vertical spacing to other groups you have to [nest] them inside a [VerticalGroup] like this.

```CSharp
[VerticalGroup("Space", PaddingTop = 20f, PaddingBottom = 20f)]
[BoxGroup("Space/Box")]
public float SomeField;
```

The [VerticalGroups] sole purpose in this case is to add vertical spacing using the `PaddingTop` & `PaddingBottom` parameters. The same principle applies to all other groups.