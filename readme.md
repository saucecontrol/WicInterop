This repo exists primarily to support the [PhotoSauce](https://github.com/saucecontrol/PhotoSauce) project.  Because the code here is based on interop code included in the WIC Tools demo, which was licensed under the Ms-PL, it must remain under that license.

The repo is designed to be included as a Git submodule.  Any project using this code must use the following C# compiler settings:

```XML
<PropertyGroup>
    <LangVersion>8</LangVersion><!-- minimum -->
    <AllowUnsafeBlocks>true</AllowUnsafeBlocks>
    <Nullable>enable</Nullable>
    <Features>strict</Features>
</PropertyGroup>
```

If building for a target that does not include the Nullable annotation attributes, they can be obtained by adding a reference to the [ReferenceAssemblyAnnotator](https://www.nuget.org/packages/TunnelVisionLabs.ReferenceAssemblyAnnotator) NuGet package.

Additionally, the [System.Memory](https://www.nuget.org/packages/System.Memory/)NuGet package or equivalent (included in `netcoreapp2.1`+ and `netstandard2.1`+) as well as [System.Runtime.CompilerServices.Unsafe](https://www.nuget.org/packages/System.Runtime.CompilerServices.Unsafe) (included in `netcoreapp3.0`+) are required.

Finally, the `VarEnum` type required for metadata support is marked obsolete in `netcoreapp2.1` and `netstandard2.1`.  This was [undone](https://github.com/dotnet/corefx/pull/35161) for `netcoreapp3.0`, so the warnings can safely be ignored.

```XML
<PropertyGroup>
    <NoWarn Condition="'$(TargetFramework)'=='netcoreapp2.1' or '$(TargetFramework)'=='netstandard2.1'">$(NoWarn);CS0618</NoWarn>
</PropertyGroup>
```

I make no promises of compatibility or API stability.  Changes will be made as needed by the PhotoSauce project.
