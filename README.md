# Easy buttons for the Unity default inspector

Original Autor:
https://github.com/madsbangh/EasyButtons

These tiny scripts add the ability to quickly show a button in the inspector for any method.

## Installation

### Git URL

Project supports Unity Package Manager. To install the project as a Git package do the following:

1. In Unity, open **Window** -> **Package Manager**.
2. Press the **+** button, choose "**Add package from git URL...**"
3. Enter "https://github.com/Romenics/EasyButtons.git" and press **Add**.

## How To Use

Add the Button attribute to a method.

   ```csharp
   using EasyButtons; // 1. Import the namespace
   using UnityEngine;
   
   public class ButtonsExample : MonoBehaviour
   {
       // 2. Add the Button attribute to any method.
   	[Button]
   	public void SayHello()
       {
           Debug.Log("Hello");
       }
   }
   ```

## Attribute Options

The `Button` attribute has different options that allow customizing the button look.

***Mode*** - indicates when the button is enabled. You can choose between the following options:

- AlwaysEnabled - the button is enabled in edit mode and play mode.

- EnabledInPlayMode - the button is only enabled in play mode.

- DisabledInPlayMode - the button is only enabled in edit mode.

***Spacing*** - allows to have some space before or after the button. The following options can be used:

- None - no spacing at all.

- Before - adds space above the button.

- After - adds space below the button.

***Expanded*** - whether to expand the parameters foldout by default. It only works with buttons that have parameters.

## Custom Editors

If you want to show buttons in a custom editor, you can use the **ButtonsDrawer** class defined in EasyButtons.Editor.

Instantiate ButtonsDrawer in OnEnable if possible, then draw the buttons with help of the DrawButtons method, as in the example:

```csharp
[CustomEditor(typeof(Example))]
public class CustomEditor : ObjectEditor
{   
    private ButtonsDrawer _buttonsDrawer;

    private void OnEnable()
    {
        _buttonsDrawer = new ButtonsDrawer(target);
    }

    public override void OnInspectorGUI()
    {
        DrawDefaultInspector();
        _buttonsDrawer.DrawButtons(targets);
    }
}
```

You can also draw only specific buttons:

```csharp
// Draw only the button called "Custom Editor Example"
_buttonsDrawers.Buttons.First(button => button.DisplayName == "Custom Editor Example").Draw(targets);
```

You can search for a specific button using its ***DisplayName*** or ***Method*** (MethodInfo object the button is attached to.)

## Notes
- Older versions of Unity might not understand the reference to EasyButtons runtime in the EasyButtons editor assembly definition. If you experience issues, you can re-add the reference, or remove the asmdefs completely.
