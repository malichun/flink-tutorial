### 为数据类型创建类型信息

Flink类型系统的核心类是`TypeInformation`。它为系统在产生序列化器和比较操作符时，提供了必要的类型信息。例如，如果我们想使用某个key来做联结查询或者分组操作，`TypeInformation`可以让Flink做更严格的类型检查。

Flink针对Java和Scala分别提供了类来产生类型信息。在Java中，类是

```java
org.apache.flink.api.common.typeinfo.Types
```

举个例子：

```java
TypeInformation<Integer> intType = Types.INT;

TypeInformation<Tuple2<Long, String>> tupleType = Types
  .TUPLE(Types.LONG, Types.STRING);

TypeInformation<Person> personType = Types
  .POJO(Person.class);
```

在Scala中，类是 `org.apache.flink.api.scala.typeutils.Types` ，举个例子：

```scala
// TypeInformation for primitive types
val stringType: TypeInformation[String] = Types.STRING
// TypeInformation for Scala Tuples
val tupleType: TypeInformation[(Int, Long)] = Types.TUPLE[(Int, Long)]
// TypeInformation for case classes
val caseClassType: TypeInformation[Person] = Types.CASE_CLASS[Person]
```

>别忘了导入`import org.apache.flink.streaming.api.scala._`

