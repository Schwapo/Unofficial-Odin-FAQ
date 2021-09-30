{% include "links.txt" %}

# Remove Unity's Default Foldout

![](assets/someclass-expanded.png "SomeClass Expanded")

By adding the [InlineProperty] Attribute to the class we can tell Odin to draw the contents of the class inline
meaning no drop-down will be drawn. 

```CSharp
[InlineProperty]
[System.Serializable]
public class SomeClass
{
	public float SomeField;
	public float SomeOtherField;
	public float AnotherField;
}

public SomeClass ClassInstance;
```

![](assets/someclass-expanded-inline-property.png "SomeClass with InlineProperty applied to it.")


By itself, this will leave the label of the field which will indent all fields
contained in the class. Adding the [HideLabel] Attribute removes that label, leaving us with the desired result.

```CSharp
[HideLabel]
[InlineProperty]
[System.Serializable]
public class SomeClass
{
	public float SomeField;
	public float SomeOtherField;
	public float AnotherField;
}

public SomeClass ClassInstance;
```

![](assets/someclass-expanded-inline-property-hide-label.png "SomeClass with InlineProperty and HideLabel applied to it. ")

You can also add these attributes to the `ClassInstance` instead if you only want that specific instance to not have the drop-down.