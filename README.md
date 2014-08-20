How to use F# with Unity
========================

Note: this has only been tested out with Xamarin Studio on Mac OS X

1. Create a Unity Project
2. Create a F# project (lib) and put it in the root of the Unity project
3. In the Unity 'Assets' folder, create a folder called 'Frameworks' and add the FSharp.Core.dll to it
4. Open the preferences for the F# project and change the 'Target Framework' to 'Mono / .NET 2.0'
5. Remove all References in the project, except FSharp.Core and System
6. Add the unity mscorlib.dll to somewhere in the F# project folder, and then to the project References
7. Make a custom build command (working dir: ${TargetDir}) that copies the resulting dll to the Unity 'Frameworks' folder

```bash
    cp GameTypes.dll ../../../../Assets/Frameworks/
```

How to write Unity components in F#
===================================

1. Copy UnityEngine.dll to the F# project and add it as a reference
2. The component will show up under the DLL in Unity's Project view, click the little arrow to fold it out (or just add it to a game object using the Add Component menu)
3. Import the Unity namespace

```fsharp
    open UnityEngine
```

4. Inherit from MonoBehaviour, as usual

```fsharp
    type SimpleComponent() =
    inherit MonoBehaviour()
        member this.stuff = 42
```

5. To show properties in the inspector, make them mutable and serializable

```fsharp
    [<SerializeField>]
    let mutable changeSpeed = 2.0f
```

6. Override member functions

```fsharp
    member this.Start () = 
        this.transform.Translate(1.0f, -1.0f, 2.0f)
```

7. Mutate members

```fsharp
    this.renderer.material.color <- Color.red
```

