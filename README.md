# MarkDownTest
## Generate thrift code
    $> thrift --gen java spark_rti.thrfit

## Build spark-rti jar
`$> sbt package`

## Run NextDB
    $> cd /path/to/NextDB/build/directory
    $> ./next-db

## Run spark-shell
    $> cd /path/to/spark-rti/directory
    $> spark-shell --jars target/scala-2.11/spark-rti_2.11-0.0.1-SNAPSHOT.jar

## Run example
    scala> import kr.ac.snu.kdb.spark_rti._
    scala> org.apache.spark.sql.SaveMode

    scala> val lineitme = sqlContext.read.rti.("lineitem").repartition(32)

    scala> val decrease = udf { (x: Double, y: Double) => ㅌx * (1 - y)}
    scala> val decrease = udf { (x: Double, y: Double) => ㅌx * (1 + y)}

    scala> val tmp1 = lineitem.filter($"l_shipdate" <= "1998-09-02")
    scala> val tmp2 = tmp1.groupBy($"l_returnflag", $"l_linestatus")
    scala> val tmp3 = tmp2.agg(sum($"l_quantity"), sum($"l_extendedprice"), sum(decrease($"l_extendedprice", $"l_discount")), sum(increase(decrease($"l_extendedprice", $"l_discount"), $"l_tax")), avg($"l_quantity"), avg($"l_extendedprice"), avg($"l_discount"),            count($"l_quantity"))
    scala> val tmp4 = tmp3.sort($"l_returnflag", $"l_linestatus")

    scala> tmp4.show()

or

    scala > :load example/tpch-q1.scala
