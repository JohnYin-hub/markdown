#### 正则表达式

```scala
object test_regress {
  def main(args:Array[String]): Unit ={
    val pattern = "Scala".r
    val str ="Scala is Scalable and cool"

    println(pattern findFirstIn str )
  }
}

output:some(Scala)
```



```scala
import scala.util.matching.Regex

object test_regress{
  def main(args:Array[String]): Unit ={
    val pattern = new Regex("(S|s)calal")
    val str = "Scala is scalable and cool"

    println((pattern findAllIn str).mkString(","))
  }
}

output:Scala,scala
```



### Mongo-java多条件查询

![image-20210918204235975](/Users/johnma/Library/Application Support/typora-user-images/image-20210918204235975.png)



```scala
import com.mongodb.MongoClient

object test_Mongo {
  def main(args:Array[String]):Unit={
    val mClient = new MongoClient("192.168.101.84",27001)
    val db = mClient.getDatabase("one_edr")
    val coll = db.getCollection("detection_ext_ip")
    val doc = coll.find().iterator()
```

