# jsclass-serializer
Yet another serialize module for Node.js, with unique feature that deserialize to its original class based Object.

## What Makes class-serializer Unique
Amoung many serializers, jsclass-serializer module is unique for its class
restore ability.  That is, deserializing does not result in creating
Object object, but original class-based object are restored.

## How to Use
Just extend your class based on "Serializable" class.  And everything works.

## Save and/or Load from File (new @0.2.0)
You can save your serialized json text to file, and load it back easily.
```
const Serializable = require('jsclass-serializer');

// Save and load to/from file

class SampleClass extends Serializable{};

let source = new SampleClass();

Serializable.setStoragePath('./data/');
source.saveToFile();

let target = new SampleClass();
target.loadFromFile(source.uuid);
```

## Date Ready
"jsclass-serializer" can de/serialize built-in Date type object collect.

## Works with "jsclass-mixin"
When developer decide to extend his/her class from Serializable, developer
should give up to extend from other classes.  That is a huge limitation, while
Java Script allows only single inheritance.
Now its not a limitation any more!  "jsclass-serializable" can be used with
["jsclass-mixin"](https://www.npmjs.com/package/jsclass-mixin)!  
Check out the code below!
```
// Serializable with jsclass-mixin
const Serializable = require('jsclass-serializer');
const mix = require('jsclass-mixin');

class B {};

class A extends mix(B, Serializable) {
  constructor() {
    super();

    //call Serializable constructor with "this" makes class A serializable
    Serializable.new(this);
  }
};


let source = new A();
let json = source.serialize();
let target = Serializable.deserialize(json);

//below code return true!
console.log(target instanceof A);
```

## Some Notes
### Use of Global Namespace
Class serializer consumes global with namespace "__serializable_classes__".
Within this name space, every constructor of Serializable subclasses are
stored.  This is because of its module-scoped nature of node, by default
class-serializer can not recognize target class definition.  Please note that
this results in extra node instance memory space
consuming.

### Property "classname" and "uuid" Are Attached Automatically
Serializable attaches property "classname" and "uuid" to its subclasses.  
"classname" is to retrieve original class info, and "uuid" is use as filename
when you save/load to/from files.

## Code Usage
Please take a look at  test/test.js for more sample codes.

### usage1:
```
const Serializable = require('jsclass-serializer');

// Serialize and Deserialize Using Static Methods

class SampleClass extends Serializable{};
let c = new SampleClass();

let json = Serializable.serialize(c);
let o = Serializable.deserialize(json);

//o is not a [Object object], but an instance of SampleClass
//below code returns, true.
console.log(o instanceof SampleClass);
```

### usage2:
```
const Serializable = require('jsclass-serializer');

// Serialize and Deserialize Using Normal Methods
//
class SampleClass extends Serializable{};
let c1 = new SampleClass();
c1.a = "A";

let json = c1.serialize();

let c2 = new SampleClass();
c2.deserialize(json);

//You can deserialize back to its original class.
//below code returns "A"
console.log(c2.a);
```

## API
<!-- Generated by documentation.js. Update this documentation by updating the source code. -->
<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [constructor][1]
    -   [Parameters][2]
-   [setStoragePath][3]
    -   [Parameters][4]
-   [serialize][5]
-   [saveToFile][6]
    -   [Parameters][7]
-   [saveToFile][8]
-   [loadFromFile][9]
    -   [Parameters][10]
-   [loadFromFile][11]
    -   [Parameters][12]
-   [serialize][13]
    -   [Parameters][14]
-   [deserialize][15]
    -   [Parameters][16]
-   [deserialize][17]
    -   [Parameters][18]

## constructor

"jsclass-serializer" provides features to serialize and deserialize to memory
and to file in json format.  Deserializing returns instance of original class.

### Parameters

-   `baseclass` **any** Set "this", when use with jsclass-mixin.

## (static) serialize

Serialize object to json format.
This method can serialize any type of object.

### Parameters

-   `o` **any** Object to serialize.

Returns **[json][20]** Json text.

## (static) deserialize

Deserialize json text to object
This method can deserialize any file with json text.

### Parameters

-   `json` **[json][20]** [description]

## (static) setStoragePath

Set directory path to save/load serialized information to/from file.

### Parameters

-   `p` **[string][19]** Absolute or relative directory path

## (static) saveToFile

Save serialized json object to file.  Where directory path would be the
path previously set by setStoragePath().
This method can serialize any type of object.

### Parameters

-   `o` **any** Object to serialize.
-   `filename` **[string][19]** Filename to save object.

Returns **[json][20]** Json text.

## (static) loadFromFile

Load json text from file and convert to object. Where directory path would
be the path previously set by setStoragePath().
This method can deserialize any file with json text.

### Parameters

-   `filename` **[string][19]** Filename to load json from.

Returns **any** Deserialized object.

## serialize

Serialize object to json format.

Returns **[json][20]** Json text.

## deserialize

Deserialize json text to object

### Parameters

-   `json` **[json][20]** [description]

## saveToFile

Save serialized json object to file.  Where directory path would be the
path previously set by setStoragePath(), and file name would be set equally
to given objects uuid.

Returns **[json][20]** Json text.


## loadFromFile

Load json text from file and convert to object. Where directory path would
be the path previously set by setStoragePath().

### Parameters

-   `uuid` **[string][19]** Unique identifier to specify the file to load from.


[1]: #constructor

[2]: #parameters

[3]: #setstoragepath

[4]: #parameters-1

[5]: #serialize

[6]: #savetofile

[7]: #parameters-2

[8]: #savetofile-1

[9]: #loadfromfile

[10]: #parameters-3

[11]: #loadfromfile-1

[12]: #parameters-4

[13]: #serialize-1

[14]: #parameters-5

[15]: #deserialize

[16]: #parameters-6

[17]: #deserialize-1

[18]: #parameters-7

[19]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[20]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/JSON
