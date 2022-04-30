{% include "links.txt" %}

# Collapse And Expand With Code

[Odin 3.0.1.0] introduced a new [Property States] system to properties, accessible through `InspectorProperty.State`, which manages certain states of properties such as Visible, Expanded and Enabled.
We can use it to programatically control the Collapsed/Expanded state of a foldout.

I'm going to show two examples, one is a bool that toggles the expanded state of a foldout group and the other is a an example showing how you would use it on a list that has folded elements inside of it.
We're going to add two buttons to the list's title bar that collapse and expand all entries.
I'm also going to add the possibility to hold <key>ctrl</key> while doing so to collapse and expand them recursively.
	Throughout this tutorial you might come accross some concept that you haven't heard of or didn't use yet. You can find links to the relevant pages in the **Odin concepts / API's used throughout the example** section.

---

??? example "Examples"

	??? example "Bool"
		=== "SomeMonoBehaviour.cs"
			```CSharp
			using Sirenix.OdinInspector;
			using UnityEngine;

			public class SomeMonoBehaviour : MonoBehaviour
			{
				[FoldoutGroup("Foldout")]
				public string SomeField;

				// All groups silently have "#" prepended to their path identifier to avoid naming conflicts with members.
				// Thus, the "Foldout" group is accessed via the "#(#Foldout)" syntax.
				[OnValueChanged("@#(#Foldout).State.Expanded = $value")]
				public bool ExpandFoldout;
			}
			```
	
	??? example "List Buttons"
		=== "SomeMonoBehaviour.cs"
			```CSharp
			using Sirenix.OdinInspector;
			using Sirenix.OdinInspector.Editor;
			using Sirenix.Utilities.Editor;
			using System.Collections.Generic;
			using UnityEngine;

			public class SomeMonoBehaviour : SerializedMonoBehaviour
			{
				[ListDrawerSettings(OnTitleBarGUI = "DrawExpandStateControls")]
				public List<SomeData> ListOfSomeData = new List<SomeData>();

				private void DrawExpandStateControls(InspectorProperty property)
				{
					// If one of the buttons is pressed, set the childrens expanded state.
					// If Event.current.control is true, meaning the user is holding ctrl, expand/collapse them recursively.

					if (SirenixEditorGUI.ToolbarButton(EditorIcons.ArrowDown))
					{
						this.SetChildExpandedState(property, true, Event.current.control);
					}
					
					if (SirenixEditorGUI.ToolbarButton(EditorIcons.ArrowUp))
					{
						this.SetChildExpandedState(property, false, Event.current.control);
					}
				}

				private void SetChildExpandedState(InspectorProperty property, bool state, bool recursive = false)
				{
					var childProperties = recursive 
						? property.Children.Recurse() 
						: property.Children;

					foreach (var child in childProperties)
					{
						child.State.Expanded = state;
					}
				}
			}
			```
		
		=== "Test Data"
			```CSharp
			public class SomeData
			{
				public string SomeString;
				public float SomeFloat;
				public bool SomeBool;
				public SomeOtherData SomeOtherData = new SomeOtherData();
			}

			public class SomeOtherData
			{
				public string SomeOtherString;
				public float SomeOtherFloat;
				public bool SomeOtherBool;
			}
			```

		<p align="center">
		![](../assets/collapse-and-expand.png)
		</p>

??? info "Odin concepts / API's used throughout the example"

	[ActionResolvers]  
	Used to resolve the `"DrawExpandStateControls"` string that's passed to the `OnTitleBarGUI` parameter into an executable action.

	[Attribute Expressions - @]  
	Used inside the OnValueChanged attribute to set the expanded state of the bool example without writing a separate function.

	[EditorIcons]  
	Used to have nice icons for our buttons.

	[FoldoutGroup]  
	Used to draw a foldable group around our properties.

	[InspectorProperty]  
	Used to access the property's state.

	[ListDrawerSettings]  
	Used to add the buttons to the list's title bar.

	[NamedValues - $]  
	Used to automagically pass the InspectorProperty argument into the DrawExpandStateControls function.

	[OnValueChanged]  
	Used to get a callback whenever our bool changes its values so that we can change the property's state accordingly.

	[Property States]  
	Used to access the property's state and set if it should be expanded or not.
	
	[Property Query Syntax - #]  
	Used to retrieve the InspectorProperty representing the FoldoutGroup.

	[Recurse]  
	Used to return an IEnumerable that recursively yields all children of the property, depth first.

	[SerializedMonoBehaviour]  
	Used so that our test data will automatically have a foldout.
	The serialization is not the important part here.

	[SirenixEditorGUI]  
	Used to draw the title bar's buttons in the same style as the default add button.
