{% include "links.txt" %}

# Foldout Expanded By Default

By using a combination of the [Property States] system and Odin's [OnInspectorInit] attribute we can set the state of the foldout everytime the inspector initializes.

```CSharp
[System.Serializable]
public class SomeClass
{
	public float SomeField;
	public float SomeOtherField;
	public float AnotherField;
}

[OnInspectorInit("@$property.State.Expanded = true")]
public SomeClass ClassInstance;
```

The *@* sign denotes this string as an [Attribute Expression] which makes everything behind it be basically treated as normal code. `$property` is a [NamedValue] and gives us the [InspectorProperty] of the `ClassInstance` field. It holds the foldout's state which we can then set directly.