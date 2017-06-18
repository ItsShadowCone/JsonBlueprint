# JsonBlueprint

## Short Description (255 chars)

Exports all C++ Json Functions to Blueprints and provides convenient C++ functions for using Json parameters as input or output parameters for blueprint functions.

## Description (1500 chars)

Provides high-level functions for working with Json in C++ as well as in Blueprints.

Note: If you only want to use Json in C++, use the integrated Json module; use this plugin only if you also want to use Json Objects in Blueprint

Features:
 - Parse and create both Json object ({"some": "example"}) and array strings (["some", "example"])
 - Convert C++ FJsonObjects to a Blueprintable class and vice versa
 - Provides rigid type checking, no casting is done unless explicitly wanted for Json Values
 - Solely Blueprint Pure functions (without execution pins). If you care about performance and often need to create the same object, however, you can just store it in a variable instead of re-creating it
 - 100% free and easy to integrate in your own plugin

## Technical Details (2043 chars)

This plugin is thought to be a dependency for other plugins that accept Json input or return Json output. It is entirely free and placed under a permissive open source license. You can find the source code here: https://github.com/Cl1608Ho/JsonBlueprint

You can add it to your own plugin simply by including "JsonBlueprint" in your PrivateDependencyModuleNames (inside the Build.cs file) and including "JsonBlueprint.h" in the files. Your plugin's LoadingPhase should be set to Default or later.

Then you can use UBlueprintJsonObject::Parse(FString JsonString, UBlueprintJsonObject*& JsonObject) (which returns true on success; false if parsing didn't work) to parse a Json Object string to a Blueprintable Json Object or JsonObject->Stringify(bool PrettyPrint = false) (returns the FString) to convert a Blueprintable Json Object to a string.

Additionally, you can use UBlueprintJsonObject::FromSharedPointer(TSharedPtr<FJsonObject> JsonObject) to convert a FJsonObject to a Blueprintable one and JsonObject->ToSharedPointer() for the other direction. The same applies to Blueprintable Json Values (and FJsonValue).

You can also use UBlueprintJsonValue::ParseArray(FString JsonString, TArray<UBlueprintJsonValue*>& Values) and UBlueprintJsonValue::StringifyArray(TArray<UBlueprintJsonValue*> Values, bool PrettyPrint = false) like the UBlueprintJsonObject function to parse and stringify a Json array (["some", "example"])

The Get methods on a Blueprintable Json Object return the requested object only if the type matches (exception: every integer is also a float, but floats aren't integers), otherwise returns an error (indicated by the Return Value being false). If you want go around that, use the generic Get (which returns a Blueprintable Json Value) and then use one of the To functions on that to cast it to the wanted type.

Using one of the Has methods before a Get method is not needed, the Get methods already do this and return an error if the key does not exist (or isn't of that type).

## Platforms tested

Windows, Mac 

Should work with all platforms