# ShowIf / HideIf Multiple Conditions

In order to be able to have multiple conditions inside a [ShowIf] / [HideIf] attribute we have to make use of Odin's [Attribute Expressions]. They allow us to basically write normal code inside the attributes [Resolver] string.

```CSharp
public bool ShowField;
public bool HideField;

[ShowIf("@ShowField && !HideField")]
public float SomeField;

[HideIf("@!ShowField && HideField")]
public float SomeField;
```

The *@* sign denotes this string as an [Attribute Expression] and everything behind it is just how you would write it in a normal if statement.









[ShowIf]: https://www.odininspector.com/attributes/show-if-attribute
[HideIf]: https://www.odininspector.com/attributes/hide-if-attribute
[Attribute Expression]: https://www.odininspector.com/tutorials/using-attributes/attribute-expressions
[Attribute Expressions]: https://www.odininspector.com/tutorials/using-attributes/attribute-expressions
[Resolver]: https://www.odininspector.com/tutorials/value-and-action-resolvers/resolving-strings-to-stuff
