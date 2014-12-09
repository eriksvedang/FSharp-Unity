How to use F# libraries with Unity
==================================

Note: this has only been tested out with Xamarin Studio on Mac OS X

1. Create a Unity Project
2. Create a F# project (lib) and put it in the root of the Unity project
3. In the Unity 'Assets' folder, create a folder called 'Frameworks' and add the FSharp.Core.dll to it
4. Open the preferences for the F# project and change the 'Target Framework' to 'Mono / .NET 3.5'
5. Remove all References in the project, except FSharp.Core (2.3.0), System and System.Core
6. Add the unity mscorlib.dll to somewhere in the F# project folder, and then to the project References
7. Make a custom build command (working dir: ${TargetDir}) that copies the resulting dll to the Unity 'Frameworks' folder

```bash
    cp MyFsharpLib.dll ../../../../Assets/Frameworks/
```

* You can access namespaces/classes from C# components just like you'd expect

How to write Unity components in F#
===================================

* Copy UnityEngine.dll to the F# project and add it as a reference
* The component will show up under the DLL in Unity's Project view, click the little arrow to fold it out (or just add it to a game object using the Add Component menu)
* Import the Unity namespace

```fsharp
    open UnityEngine
```

* Inherit from MonoBehaviour, as usual

```fsharp
    type SimpleComponent() =
    inherit MonoBehaviour()
        member this.stuff = 42
```

* To show properties in the inspector, make them mutable and serializable

```fsharp
    [<SerializeField>]
    let mutable changeSpeed = 2.0f
```

* Override member functions

```fsharp
    member this.Start () = 
        this.transform.Translate(1.0f, -1.0f, 2.0f)
```

* Mutate members

```fsharp
    this.renderer.material.color <- Color.red
```

