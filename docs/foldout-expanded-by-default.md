# Foldout Expanded By Default

By using a combination of the [Property States] system and Odin's [OnInspectorInit] attribute we can set the state of the foldout everytime the inspector initializes.

```CSharp
// Example class
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

The *@* sign denotes this string as an [Attribute Expression] which makes everything behind it be basically treated as normal code. `$property` is a [Named Value] and gives us the [InspectorProperty] of the `ClassInstance` field. It holds the foldout's state which we can then set directly.







[OnInspectorInit]: https://www.odininspector.com/attributes/on-inspector-init-attribute
[Property States]: https://www.odininspector.com/tutorials/using-attributes/property-states
[Attribute Expression]: https://www.odininspector.com/tutorials/using-attributes/attribute-expressions
[Named Value]: https://www.odininspector.com/tutorials/value-and-action-resolvers/named-values
[InspectorProperty]: https://www.odininspector.com/documentation/sirenix.odininspector.editor.inspectorproperty