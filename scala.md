Scala
=====

Scala Language
--------------

* [https://www.scala-lang.org](https://www.scala-lang.org)

Scala IDE
---------

* [http://scala-ide.org](http://scala-ide.org)

REPL(Read Eval Pring Loop)
--------------------------

```
C:\dev\scala\hello>scala
Welcome to Scala 2.12.3 (Java HotSpot(TM) 64-Bit Server VM, Java 1.8.0_141).
Type in expressions for evaluation. Or try :help.

scala> 1 + 2
res0: Int = 3

scala> 1 + 2
res1: Int = 3

scala> res0 + res1
res2: Int = 6

scala> :quit

C:\dev\scala\hello>
```

Compile & Execute
-----------------

```
C:\dev\scala\hello>scalac hello.scala
Hello$.class   Hello.class    hello.scala

C:\dev\scala\hello>scala -classpath . Hello
Hello World!

C:\dev\scala\hello>
```