BSD License

For ig-json-parser

Copyright (c) 2014, Facebook, Inc. All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

 * Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

 * Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

 * Neither the name Facebook nor the names of its contributors may be used to
   endorse or promote products derived from this software without specific
   prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

ig-json-parser
==============

[![Build Status](https://travis-ci.org/Instagram/ig-json-parser.svg?branch=master)](https://travis-ci.org/Instagram/ig-json-parser) [![Release](https://jitpack.io/v/Instagram/ig-json-parser.svg)](https://jitpack.io/#Instagram/ig-json-parser)

Fast JSON parser for java projects. 


Getting started
===============

The easiest way to get started is to look at maven-example.  For more
comprehensive examples, check out the unit tests or the demo.


Gradle
-----

For Java projects, to use this library, add this to your build.gradle file:
```groovy
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}

...

dependencies {
  implementation 'com.github.instagram.ig-json-parser:runtime:master-SNAPSHOT' // the runtime
  implementation 'com.github.instagram.ig-json-parser:processor:master-SNAPSHOT' // the annotation processor 
}
```

For Android projects using Android Studio 3.0+ or Gradle 4.0+, you can enable the annotation processor as following:

```
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}

...

dependencies {
  annotationProcessor 'com.github.instagram.ig-json-parser:processor:master-SNAPSHOT'
  implementation 'com.github.instagram.ig-json-parser:runtime:master-SNAPSHOT'
}
```

If you are using older gradle versions, you can use old `apt` plugin to integrate the annotation processor:

```
allprojects {
  repositories {
    maven { url 'https://jitpack.io' }
  }
}

...

apply plugin: 'com.neenbedankt.android-apt'

dependencies {
  apt 'com.github.instagram.ig-json-parser:processor:master-SNAPSHOT'
  implementation 'com.github.instagram.ig-json-parser:runtime:master-SNAPSHOT'
}
```


If you are using other build sytems, please find instructions [here](https://jitpack.io/#Instagram/ig-json-parser)

Requirements for model classes
------------------------------

There should be a package-visible no-argument constructor for each of your
model classes.  The fields also need to be package-visible.

Each class that needs a serializer/deserializer generated should be
annotated with `@JsonType`.  Each field that needs to be mapped to/from
JSON should be annotated with `@JsonField`.  The `@JsonField` annotation
has one mandatory argument, which is the fieldname for the field in the
JSON.

The following is an example of a very simple model class:
```java
@JsonType
class Dessert {
  @JsonField(fieldName="type")
  String type;

  @JsonField(fieldName="rating")
  float rating;
}
```

Serializer/deserializer
-----------------------

Compiling your model classes with the annotations will automatically
generate the serializer and deserializer.  They will be in a generated
class with the same name as your class, except with the suffix
`__JsonHelper`.  For example, to deserialize the `Dessert` class above,
simply run the code:

```java
Dessert parsed = Dessert__JsonHelper.parseFromJson(inputJsonString);
```
To serialize a class, run:

```java
String serialized = Dessert__JsonHelper.serializeToJson(dessertObject);
```

Supported data types
--------------------

The following scalar types are supported:
* String
* boolean/Boolean
* int/Integer
* long/Long
* float/Float
* double/Double

If a json field is another dictionary, it can be represented by another
model class.  That model class must also have the `@JsonType` annotation.

Lists of objects are supported either as Java Lists or Queues.

Proguard
===============

Add the following lines to your proguard-rules file:
```
-dontwarn sun.misc.Unsafe
-dontwarn javax.annotation.**
```

Advanced features
=================

Postprocessing
--------------

TODO: Document this.  See the documentation in
common/src/main/java/com/instagram/common/json/annotation/JsonType.java in
the meanwhile.

Customized parsing code
-----------------------

TODO: Document this.  See the documentation in
common/src/main/java/com/instagram/common/json/annotation/JsonField.java
in the meanwhile.

Optional serializer generation
------------------------------
To save generating serializer code if you only need deserialization, serializer generation can be disabled or enabled
globally and per-class. The default is to generate serializers for all classes. To disable generation globally, pass

    -AgenerateSerializer=false

to the command-line arguments of javac. To override the default generation option for a single class, see
`JsonType.generateSerializer()`.
