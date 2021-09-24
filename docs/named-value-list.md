# Named Value List

### [AssetList]
| Name  | Type     |
| ----- | -------- |
| asset | TElement |

### [CustomValueDrawer]
| Name           | Type                         |
| -------------- | ---------------------------- |
| label          | [GUIContent]                 |
| callNextDrawer | [Func]<[GUIContent], [bool]> |

### [TableMatrix]
| Name    | Type     |
| ------- | -------- |
| rect    | [Rect]   |
| element | TElement |
| value   | TElement |
| array   | TArray   |
| x       | [int]    |
| y       | [int]    |

### [OnCollectionChanged]
| Name | Type                   |
| ---- | ---------------------- |
| info | [CollectionChangeInfo] |





[AssetList]: https://www.odininspector.com/documentation/sirenix.odininspector.assetlistattribute
[TableMatrix]: https://www.odininspector.com/documentation/sirenix.odininspector.tablematrixattribute
[CustomValueDrawer]: https://www.odininspector.com/documentation/sirenix.odininspector.customvaluedrawerattribute
[OnCollectionChanged]: https://www.odininspector.com/documentation/sirenix.odininspector.oncollectionchangedattribute

[CollectionChangeInfo]: https://www.odininspector.com/documentation/sirenix.odininspector.editor.collectionchangeinfo 

[GUIContent]: https://docs.unity3d.com/ScriptReference/GUIContent.html
[Func]: https://docs.microsoft.com/en-us/dotnet/api/system.func-2?view=net-5.0
[bool]: https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/bool
[Rect]: https://docs.unity3d.com/ScriptReference/Rect.html
[int]: https://docs.microsoft.com/en-us/dotnet/api/system.int32?view=net-5.0