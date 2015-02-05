# YamlDotNet

YamlDotNet is a .NET library for YAML. YamlDotNet provides low level parsing and emitting of YAML as well as a high level object model similar to XmlDocument. A serialization library is also included that allows to read and write objects from and to YAML streams.

## What is YAML?

YAML, which stands for "YAML Ain't Markup Language", is described as "a human friendly data serialization standard for all programming languages". Like XML, it allows to represent about any kind of data in a portable, platform-independent format. Unlike XML, it is "human friendly", which means that it is easy for a human to read or produce a valid YAML document.

## The YamlDotNet library

The library has now been successfully used in multiple projects and is considered fairly stable.

## More information

More information can be found in the [official page of the project](http://aaubry.net/pages/yamldotnet.html).

## Installing

Just install the [YamlDotNet NuGet package](http://www.nuget.org/packages/YamlDotNet/):

```
PM> Install-Package YamlDotNet 
```

If you do not want to use NuGet, you can [download binaries here](https://ci.appveyor.com/project/aaubry/yamldotnet).


# Changelog

## Version 3.5.1

Fix bug:

* Scalars returned by the scanner do not have their Start and End properties set.

## Version 3.5.0

* Add native support of System.Guid serialization.
* Add properties to YamlMemberAttribute:
    * Order: specifies the order of the members when they are serialized.
    * Alias: instructs the deserializer to use a different field name for serialization.
* The YamlAliasAttribute is now obsolete. New code should use YamlMemberAttribute instead.
* Throw proper exceptions, with correct marks, when deserialization of a node fails.

## Version 3.4.0

Changes and fixes on the Scanner to make it more usable:

* Report the location of comments correctly, when the scanner is created with "skipComments = false"
* In case of syntax error, do not report an empty range and skip to the next token.
* Make the scanner and related types serializable, so that the state of the scanner can be captured and then restored later (assuming that the TextReader is also serializable).

## Version 3.3.1

This release adds a signed package and portable versions of the library.

## Version 3.3.0

* Make types in YamlDotNet.RepresentationModel serializable.

## Version 3.2.1

* Fix AnchorNotFoundException when another exception occurs during deserialization.

## Version 3.2.0

This release adds merge key support: http://yaml.org/type/merge.html

Example from BackreferencesAreMergedWithMappings unit test:

```C#
var reader = new EventReader(new MergingParser(new Parser(stream)));
var result = Deserializer.Deserialize<Dictionary<string, Dictionary<string, string>>>(parser);
```

## Version 3.1.1

This is a bugfix release that fixes issue #90.

## Version 3.1.0

* Add a parameter to the deserializer to ignore unmapped properties in YAML.

## Version 3.0.0

* Fix issue #26: Use the actual type of the objects instead of the statically detected one.
* Merged the Core, Converters and RepresentationModel assemblies. **The NuGet packages YamlDotNet.Core and YamlDotNet.RepresentationModel are now a single package, named YamlDotNet**.
* Removed YamlDotNet.Configuration and YamlDotNet.Converters.
* Line numbers in error messages now start at one.
* TypeConverter is now used to cast list items.
* Various code improvements.
* More and better unit tests.

## Version 2.2.0

TODO

## Version 2.1.0

TODO

## Version 2.0.0

* YamlSerializer has been replaced by the Deserializer class. It offer the same functionality of YamlSerializer but is easier to maintain and extend.
  * **Breaking change:** DeserializationOverrides is no longer supported. If you need this, please file a bug and we will analyze it.
  * **Breaking change:** IDeserializationContext is no longer supported. If you need this, please file a bug and we will analyze it.
  * Tag mappings are registered directly on the Deserializer using RegisterTagMapping()
  * ObjectFactory is specified in the constructor, if required.

* Bug fixes to the Serializer:
  * Fix bug when serializing lists with nulls inside. e9019d5f224f266e88d9882502f83f0c6865ec24

* Adds a YAML editor add-in for Visual Studio 2012. Available on the [Visual Studio Gallery](http://visualstudiogallery.msdn.microsoft.com/34423c06-f756-4721-8394-bc3d23b91ca7).
