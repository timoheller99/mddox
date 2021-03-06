[![NuGet version](https://badge.fury.io/nu/LoxSmoke.mddox.svg)](https://badge.fury.io/nu/LoxSmoke.mddox) [![NuGet](https://img.shields.io/nuget/dt/LoxSmoke.mddox.svg)](https://www.nuget.org/packages/LoxSmoke.mddox) 

# mddox

Global tool to create simple markdown documentation using reflection and XML comments that are extracted from the source code by the compiler.

[Sample documentation](https://github.com/loxsmoke/DocXml/blob/master/api-reference.md)

[XML documentation comments on MSDN](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)


## Installation

```bash
dotnet tool install -g loxsmoke.mddox
```

## Uninstallation

```bash
dotnet tool uninstall -g loxsmoke.mddox
```

## Usage

```bash
mddox
Usage: mddox <assembly> [optional-parameters]

<assembly>   - The name of the assembly to document.
```
Optional parameters:

Short format | Long format | Comment
|---|---|---|
| -**o** output_md |--**output** output_md  | The name of the markdown output file. |
| -**f** format | --**format** format   |  The markdown file format. Valid values: github,bitbucket. |
| -**r**  | --**recursive**           | Step into referenced assemblies recursively. This parameter can be used multiple times to specify multiple assemblies. |
| -**r** assembly  | --**recursive** assembly | Step recursivelly only into specified assembly or assemblies.<br> This parameter can be used multiple times to specify multiple assemblies. |
| -**m**  | --**ignore-methods**      | Do not generate documentation for methods and constructors. |
| -**a** name  | --**ignore-attribute** name | Do not generate documentation for properties with specified custom attribute. For example  JsonIgnoreAttribute<br> This parameter can be used multiple times to specify multiple sttributes. |
| -**t** name  | --**type** name         | Document only this type and all types referenced by this type. |
| -**d** [view]  | --**msdn** [view]       | Generate links to the MSDN documentation for System.* and Microsoft.* types.<br>The documentation pages are located at this site https://docs.microsoft.com<br>View is an optional parameter of URL specifying the version of the type. For example: netcore-3.1 |  
| -**n**  | --**no-title**            | Do not write the "created by mddox at date" in the markdown file. |
  
Documenting all types of one assembly

```bash
mddox MyAssembly.dll
```

Documenting only fields and properties of all types in assembly

```bash
mddox MyAssembly.dll --ignore-methods
```

Documenting types that do not have specified custom attributes

```bash
mddox MyAssembly.dll --ignore-attribute JsonIgnoreAttribute --ignore-attribute XmlIgnore
```

Document one type and all referenced types from different assemblies 

```bash
mddox MyAssembly.dll --type ClassToDocument --recursive ReferencedAssembly1.dll --recursive ReferencedAssembly2.dll
```

