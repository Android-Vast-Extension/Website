# 类型转换拓展

!!! 类型转换

    === "Kotlin"

        ```kotlin
        open class Person(val name:String)

        class Student(val grade:Int, val stuName: String):Person(stuName){
            fun hungry(){
                LogUtils.i(stuName,"I'm hungry.")
            }
        }

        val a = cast<Person>(Student(6,"小明"))
        ```

    === "Java"

        ```java
        class Person{
            protected String name;

            public Person(String name) {
                this.name = name;
            }
        }
        
        class Student extends Person{
            protected int grade;

            public Student(int grade,String name) {
                super(name);
                this.grade = grade;
            }
        }

        try {
            Person person = CastExtension.cast(new Student(1,"李明"));
        } catch (Exception e) {
            e.printStackTrace();
        }
        ```
