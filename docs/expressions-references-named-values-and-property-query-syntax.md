{% include "links.txt" %}

# Expressions, References, Named Values and Property Query Syntax

This tutorial is meant to clear up any confusion about the usage of Odin's resolved strings, named values, references, expressions and the property query syntax.
It is not meant to replace the existing documentation around these topics.
We're going to look at the different symbols used <key>@</key> <key>$</key> <key>#</key> and learn what they mean and when to use which.

??? info "Resolved Strings"
	Resolved strings are the central part of all the different concepts mentioned above. 
	They allow us to take a string and resolved them to different values like booleans, integers, vectors, ..., into another string or even actions that can be executed. 
	To learn how to create your own attributes that make use of them click [here](https://odininspector.com/tutorials/value-and-action-resolvers/resolving-strings-to-stuff).

	??? example "Example"
		The "GetColor" string will be resolved to the color that's returned by the referenced function.
		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[GUIColor("GetColor")]
			public string SomeField;

			public Color GetColor() => Color.red;
		}
		```

??? info "Named Values - $"
	Named values are used within resolved strings. In short, they're contextual values that can be accessed by the string that is being resolved. Think of them as simple variables.
	Named values are always prefixed with a **$** symbol so that Odin can differentiate them from normal strings/words. 
	The only other time that a **$** symbol is used inside of resolved strings is to reference members by name and we're going to look at that shortly, but in general whenever you see a **$** symbol inside of a resolved string, you're probably working with a named value.
	Almost all resolvers have at least two named values, **$property** and **$value**

	- **InspectorProperty property:** The property instance that the string is being resolved on.
	- **TValue value:** The value of the property that the string is being resolved on - note that this named value only exists on properties that have values, and the type of the named value changes based on the value type of the property!
	
	??? example "Example"
		**Finding an isolated example of named values without using attribute expressions is pretty hard since they often go hand in hand so in this example focus on the named value and ignore the @ symbol which we'll talk about later.**  
		
		The named value **$value** refers to the value of the InfoMessage field in this case. This snippet will show an info box whose message is equal to the InfoMessage string.

		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[InfoBox("@$value")]
			public string InfoMessage;
		}
		```

	Some resolvers have additional named values which can currently only be found by looking at the source code or by purposefully making a mistake in the resolved string and reading the error message which will show the available named values.
	I have also created an interactive documentation window that can be opened in Unity which lists all attributes with resolved parameters and shows basic interactive code examples for them, you can find it [here](https://github.com/Schwapo/Odin-Resolved-Parameters-Overview)

	Named values are automatically passed as arguments to the function you reference inside of the resolved string if that function defines a corresponding parameter.
	??? example "Example"
		Even though we're not passing any argument to the LogHealth function inside of the string, Odin knows what the LogHealth function expects and tries to find a named value that fits the parameter.
		In this case the corresponding named value is **$value**. Note that the names of the named value and the parameter don't have to be the same.
		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[InlineButton("LogHealth")]
			public int Health = 100;

			public void LogHealth(int value) => Debug.Log(value);
		}
		```

	If you want to know more about them or want to see how you can use them for your own attributes, look [here](https://odininspector.com/tutorials/value-and-action-resolvers/named-values).

??? info "References - $"
	References are the only other place inside of a resolved string where you'll see a **$** symbol outside of named values.
	They are only needed in the special case that your resolved string will be resolved into another string `(string -> string)` and you want to reference a member such as a field or method name.
	The **$** symbol tells Odin that the following word is meant to be treated as a reference to a member in the current scope, similarly to how it works for named values.
	In all other cases for example if you resolve a string to an integer `(string -> integer)`, it is not necessary to use the **$** symbol to reference a member.
	
	**You don't need to prefix the member name with a $ symbol if you're using expressions which we will talk about next.**

	??? example "String to String Example"
		Referencing a member inside of a resolved string that resolves into another string **(string -> string)**
		As you can see we have to prepend the member name with a **$** symbol since the string will be resolved to a string (message).

		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[InfoBox("$Message")]
			public string SomeField;

			public string Message;
		}
		```
	??? example "String to Non String Example"
		Referencing a member inside of a resolved string that resolves into a color **(string -> color)**
		As you can see we **do not** have to prepend the member name with a **$** symbol since the string will **not be** resolved into another string.

		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[GUIColor("FieldColor")]
			public string SomeField;

			public Color FieldColor;
		}
		```
	??? example "Expression Example"
		**We didn't learn about expressions yet, but here's an example referencing a member inside of them for completeness sake.**  
		
		As you can see we **do not** have to prepend the member name with a **$** symbol since this is an attribute expression.

		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[InfoBox("@Message")]
			public string SomeField;

			public string Message;
		}
		```

??? info "Expressions - @"
	Expressions are denoted by a string that begins with an **@** symbol. They allow you to basically write normal C# code inside of the string which will then be resolved and executed.
	You can still access named values inside of expressions using the normal **$** symbol syntax from before.
	Named values will not be automatically passed into the function referenced inside of the expression, that only works if it's not an expression.

	**Some C# features might not be supported as of now, but Odin will give you an error message in that case. Try to use less fancy C# features if it comes up :)**

	??? example "Expression Example"
		We create an inline button that when pressed will execute the expression we passed into it.
		In this case that would be logging the current value of the SomeField member. 
		As you can see we make use of named values as well to get the current value of the SomeField member and pass it into the `Debug.Log` function.
		This also demonstrates the need to pass in arguments manually unlike the log health example we've seen inside the named values section.

		```CSharp
		using Sirenix.OdinInspector;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[InlineButton("@UnityEngine.Debug.Log($value)")]
			public string SomeField;

			public string Message;
		}
		```
	
	You can learn more about expressions [here](https://odininspector.com/tutorials/using-attributes/attribute-expressions)
	
??? info "Property Query Syntax - #"
	Usually, if you want to access the InspectorProperty of a field, you do so by using the **$property** named value that we've seen in the named value section.
	However, if you want to access the InspectorProperty of another field in the current scope you can do so by using the property query syntax.
	To use it you write the name of the member whose InspectorProperty you want in parentheses and prefix it with a **#** symbol **#(SomeMemberName)**. 

	??? example "Example"
		We're accessing the InspectorProperty representing the SomeList member to be able to set its expanded state.
		```CSharp
		using Sirenix.OdinInspector;
		using System.Collections.Generic;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			public List<string> SomeList = new List<string>();

			[OnValueChanged("@#(SomeList).State.Expanded = $value")]
			public bool ExpandList;
		}
		```
	
	**There is one special case for groups since all groups silently have "#" prepended to their path identifier to avoid naming conflictions with members, you have to add it to their name when using the property query syntax #(#SomeGroupName).**

	??? example "Example"
		We're accessing the InspectorProperty representing the foldout group to be able to set its expanded state.
		
		**Note how we had to prepend the identifier of the group with an # symbol**
		```CSharp
		using Sirenix.OdinInspector;
		using System.Collections.Generic;
		using UnityEngine;

		public class SomeMonoBehaviour : MonoBehaviour
		{
			[FoldoutGroup("Foldout")]
			public string SomeString;

			[OnValueChanged("@#(#Foldout).State.Expanded = $value")]
			public bool ExpandFoldout;
		}
		```