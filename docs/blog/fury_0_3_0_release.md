# Fury v0.3.0 released

Author: [chaokunyang](https://github.com/chaokunyang)

I'm pleased to announce the 0.3.0 release of the Fury. With this release, fury supports all scala 2/3 objects serializaiton now, including: **case/pojo/object/option/tuple/collecton/enum and other types**. case/pojo/object are tightly integrated with fury JIT. Fury will generate highly-optimized serializer by generate serialize code at runtime to speed up serializaiton. The serialization for those objects will be extremely fast.

For a long time, scala serialization is always tricky, only reliable way is JDK serialization. But it’s too slow, and the serialized size is too large. Although we have frameworks such as chill, but the support for scala types are limited, and the performance is limited too.Now with fury scala, you can serialize any scala objects you want and get extremly fast performance. Please try it out and let us know if you have any issues.

## Scala Serialization Guide
Install dependecy:
```sbt
libraryDependencies += "org.furyio" % "fury-core" % "0.3.0"
```

Creating fury:

```scala
val fury = Fury.builder()
 .withScalaOptimizationEnabled(true) 
 .requireClassRegistration(false)
 .withRefTracking(true)
 .build()
```

Serialize case objects:

```scala
case class Person(github: String, age: Int, id: Long)
val p = Person("https://github.com/chaokunyang", 18, 1)
println(fury.deserialize(fury.serialize(p)))
println(fury.deserializeJavaObject(fury.serializeJavaObject(p)))
```

Serialize singleton objects:

```scala
object singleton {
}
val o1 = fury.deserialize(fury.serialize(singleton)) 
val o2 = fury.deserialize(fury.serialize(singleton)) 
println(o1 == o2)
```

Serialize collection objects:

```scala
val seq = Seq(1,2)
val list = List("a", "b") val map = Map("a" -> 1, "b" -> 2)
println(fury.deserialize(fury.serialize(seq)))
println(fury.deserialize(fury.serialize(list)))
println(fury.deserialize(fury.serialize(map)))
```

Serialize enum:

```scala
enum Color { case Red, Green, Blue }
println(fury.deserialize(fury.serialize(Color.Green)))
```

## Highlight
-  [Scala] Support scala serialization: `case/object/tuple/string/collection/enum/basic` all supported
-  [Scala] Add [scala user documentation](https://github.com/alipay/fury/blob/main/docs/guide/scala_guide.md)
- [Scala] add optimized scala singleton object serializer
-  [Java] Make `java.io.Externalizable` compatible with Java `writeReplace/readResolve` API
-  [Java] Integrate fury with dubbo https://github.com/apache/dubbo-spi-extensions/pull/226
- [Java] support bytes string serialization for jdk8 with JDK17 runtime

## BugFix
- [Java] Allow for `InputStream` not reading entire length 
- [Java] Use `ReflectionUtils.getCtrHandle()` for non-public constructor in `ExternalizableSerializer`
- [Java] fix jdk compatible serialization for inheritance 

## What's Changed
* [Impove][Doc] Improve README by @caicancai in https://github.com/alipay/fury/pull/1011
* [Java] rename wrong ascii naming to latin by @chaokunyang in https://github.com/alipay/fury/pull/1013
* [Doc] Update go install doc by @chaokunyang in https://github.com/alipay/fury/pull/1015
* fix(grammatical): correct typos and improve grammar by @iamahens in https://github.com/alipay/fury/pull/1018
* [Improve][Doc] Improve README by @caicancai in https://github.com/alipay/fury/pull/1020
* [Improve][Doc] add environment requirement by @caicancai in https://github.com/alipay/fury/pull/1022
* chore(docs): fixed typos by @Smoothieewastaken in https://github.com/alipay/fury/pull/1023
* bugfix: read buffer error when object contain binary field by @wangweipeng2 in https://github.com/alipay/fury/pull/1026
* [Doc] Optimize class registration doc by @chaokunyang in https://github.com/alipay/fury/pull/1027
* [Java] fix jdk compatible serialization for inheritance by @chaokunyang in https://github.com/alipay/fury/pull/1030
* [Doc] add scala user doc by @chaokunyang in https://github.com/alipay/fury/pull/1028
* [Doc] refine scala doc by @chaokunyang in https://github.com/alipay/fury/pull/1031
* Update README.md - fix grammatrical errors in README. by @ayushrakesh in https://github.com/alipay/fury/pull/1037
* [Java] Support local static class jit by @chaokunyang in https://github.com/alipay/fury/pull/1036
* [Java] support bytes string serialization for jdk8 by @chaokunyang in https://github.com/alipay/fury/pull/1039
* [Java] set timeout to JITContextTest by @chaokunyang in https://github.com/alipay/fury/pull/1040
* [Java] fix string builder serialization for jdk8 with jdk17 runtime by @chaokunyang in https://github.com/alipay/fury/pull/1042
* [Doc] add auto code reviewers by @chaokunyang in https://github.com/alipay/fury/pull/1043
* [Java] Allow for `InputStream` not reading entire length by @knutwannheden in https://github.com/alipay/fury/pull/1034
* [Java] Use `ReflectionUtils.getCtrHandle()` in `ExternalizableSerializer` by @knutwannheden in https://github.com/alipay/fury/pull/1044
* [Improve] make maven-spotless-plugin version as a parameter by @caicancai in https://github.com/alipay/fury/pull/1046
* Update README.md by @Shivam250702 in https://github.com/alipay/fury/pull/1047
* [Java] support writeReplace/readResolve for Externalizable by @chaokunyang in https://github.com/alipay/fury/pull/1048
* Update README.md by @Spyrosigma in https://github.com/alipay/fury/pull/1051
* Grammatical error in CODE_OF_CONDUCT.md by @HimanshuMahto in https://github.com/alipay/fury/pull/1050
* Update scala link title README.md by @chaokunyang in https://github.com/alipay/fury/pull/1052
* [Doc] add scala readme and refine document by @chaokunyang in https://github.com/alipay/fury/pull/1041
* [Java] populate StackOverflowError with enable ref tracking message by @chaokunyang in https://github.com/alipay/fury/pull/1049
* [Scala] Setup scala project by @chaokunyang in https://github.com/alipay/fury/pull/1054
* [Scala] add scala singleton object serializer by @chaokunyang in https://github.com/alipay/fury/pull/1053
* Updated README.md by @vidhijain27 in https://github.com/alipay/fury/pull/1056
* [Scala] add scala tuple serialization tests  by @chaokunyang in https://github.com/alipay/fury/pull/1059
* Empty ListExpression#genCode will throw npe by @farmerworking in https://github.com/alipay/fury/pull/1063

## New Contributors
* @iamahens made their first contribution in https://github.com/alipay/fury/pull/1018
* @Smoothieewastaken made their first contribution in https://github.com/alipay/fury/pull/1023
* @ayushrakesh made their first contribution in https://github.com/alipay/fury/pull/1037
* @knutwannheden made their first contribution in https://github.com/alipay/fury/pull/1034
* @Shivam250702 made their first contribution in https://github.com/alipay/fury/pull/1047
* @Spyrosigma made their first contribution in https://github.com/alipay/fury/pull/1051
* @HimanshuMahto made their first contribution in https://github.com/alipay/fury/pull/1050
* @vidhijain27 made their first contribution in https://github.com/alipay/fury/pull/1056
* @farmerworking made their first contribution in https://github.com/alipay/fury/pull/1063

**Full Changelog**: https://github.com/alipay/fury/compare/v0.2.1...v0.3.0