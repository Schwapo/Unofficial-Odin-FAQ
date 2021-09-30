{% include "links.txt" %}

# Named Value List

### All Resolvers
| Name     | Type                |
| -------- | ------------------- |
| property | [InspectorProperty] |
| value    | TValue              |

---

### [AssetList]
| Name  | Type     |
| ----- | -------- |
| asset | TElement |

---

### [CustomValueDrawer]
| Name           | Type                         |
| -------------- | ---------------------------- |
| label          | [GUIContent]                 |
| callNextDrawer | [Func]<[GUIContent], [bool]> |

---

### [TableMatrix]
| Name    | Type     |
| ------- | -------- |
| rect    | [Rect]   |
| element | TElement |
| value   | TElement |
| array   | TArray   |
| x       | [int]    |
| y       | [int]    |

---

### [OnCollectionChanged]
| Name | Type                   |
| ---- | ---------------------- |
| info | [CollectionChangeInfo] |