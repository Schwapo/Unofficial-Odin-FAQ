# Hide The Reference Picker

![](assets/some-interface-implementation.png "Interface implementation with visible reference object picker")

You can add the [HideReferenceObjectPicker] attribute to the class to hide the reference picker.

```CSharp
[HideReferenceObjectPicker]
public interface ISomeInterface
{
    float SomeField { get; set; }
    float SomeOtherField { get; set; }
}

public ISomeInterface SomeInterfaceField;

```

![](assets/some-interface-implementation-hidden-reference-object-picker.png "Hidden reference object picker")

You can also add the attribute to the `SomeInterfaceField` instead if you only want to hide the reference picker for that specific instance.






[HideReferenceObjectPicker]: https://www.odininspector.com/attributes/hide-reference-object-picker-attribute