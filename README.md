

# frank-native-core



## Usage
Redesign the management about JavaScript prototype chain inheritance,Make every instance has independent prototype chain.
In other words:make inheritance like Java.
### Orignal oop code:
```js
function Parent(){
 
    var data;
 
    this.getData = functin(){
 
        return data;
 
    };
 
    this.setData(arg){
 
        data = arg;
 
    };
 
};

  
function Child(){};
 
Child.prototype = new Parent();
 
var b = new Child();
 
var c = new Child();
 
b.setData("b");
 
c.setData("c");
 
console.log("b:"+b.getData());//"b:c", incorrect
 
console.log("c:"+c.getData());//"c:c", correct
 ```
### Now oop code
 ```js
  const Frank = require("require");
 
  const Parent = Frank.buildType("Parent").classBody(function(){
 
    var data;
 
    this.getData = functin(){
 
        return data;
 
    };
 
    this.setData(arg){
 
        data = arg;
 
    };
 
}).toClass();
 
const Child = Frank.buildType("Child").extendsFrom(Parent).toClass();
 
 
var b = Frank.newInstance(Child);//or Child.newInstance() or new Child();
 
var c = Frank.newInstance(Child);//or Child.newInstance() or new Child();
 
b.setData("b");
 
c.setData("c");
 
console.log("b:"+b.getData());//"b:b" correct
 
console.log("c:"+c.getData());//"c:c" correct
 ```
## Developing
 ```js
const Frank = require("frank-native-core");
 
const SuperClass = function () {};
 
const Person = Frank.buildType("Person").extendsFrom(SuperClass).classBody(function () {
 
    this.name = Frank.FrankUtils.getter_setter();
 
    this.age = Frank.FrankUtils.getter_setter();
 
    this.job = Frank.FrankUtils.abstract4override;
 
    this.say = function () {
 
        return "I am a " + this.job() + ", " + this.name() + " , " + this.age() + " year-old.";
 
    };
 
}).toClass();
 
const Student = Frank.buildType("Student").extendsFrom(Person).classBody(function () {
 
    this.job = function () {
 
        return "student";
 
    }
 
}).toClass();
 
const Teacher = Frank.buildType("Teacher").extendsFrom(Person).classBody(function () {
 
    this.job = function () {
 
        return "teacher";
 
    }
 
}).toClass();
 
var student = Frank.newInstance(Student);
 
var teacher = Frank.newInstance(Teacher);
 
student.name("Tom").age(20);
 
teacher.name("Lili").age(30);
 
console.log("student.isInstance(   SuperClass)  :  " + student.isInstance(SuperClass);
 
console.log("student.isInstance(       Person)  :  " + student.isInstance(Person);
 
console.log("student.isInstance(      Student)  :  " + student.isInstance(Student);
 
console.log("Student.isAssignableFrom( Person)  :  " + Student.isAssignableFrom(Person);
 
console.log("Student.isAssignableFrom(Student)  :  " + Student.isAssignableFrom(Student);
 
console.log("teacher.isInstance(   SuperClass)  :  " + teacher.isInstance(SuperClass);
 
console.log("teacher.isInstance(       Person)  :  " + teacher.isInstance(Person);
 
console.log("teacher.isInstance(      Teacher)  :  " + teacher.isInstance(Teacher);
 
console.log("Teacher.isAssignableFrom( Person)  :  " + Teacher.isAssignableFrom(Person);
 
console.log("Teacher.isAssignableFrom(Teacher)  :  " + Teacher.isAssignableFrom(Teacher);
 
console.log("teacher.isInstance(      Student)  :  " + teacher.isInstance(Student);
 
console.log("teacher.isInstance(       Object)  :  " + teacher.isInstance(Object);
 
console.log(student.say());
 
console.log(teacher.say());
 ```
 ### output logs:
 ```
student.isInstance(   SuperClass)  :  true
student.isInstance(       Person)  :  true
student.isInstance(      Student)  :  true
Student.isAssignableFrom( Person)  :  true
Student.isAssignableFrom(Student)  :  false
teacher.isInstance(   SuperClass)  :  true
teacher.isInstance(       Person)  :  true
teacher.isInstance(      Teacher)  :  true
Teacher.isAssignableFrom( Person)  :  true
Teacher.isAssignableFrom(Teacher)  :  false
teacher.isInstance(      Student)  :  false
teacher.isInstance(       Object)  :  true
I am a student, Tom , 20 year-old.
I am a teacher, Lili , 30 year-old.
```
### API
 1. Type: Frank.buildType(className:string)
 2. Type: Frank.FrancFactory.buildType(className:string)
 3. Type: Type.extendsFrom(clazz:Function/Class/Constructor)
 4. Type: Type.classBody(func:Function/Class/Constructor)
 5. Class: Type.toClass()
 6. FrankBasic: Class.newInstance()
 7. FrankBasic: Frank.newInstance(Class)
 8. Boolean: Class.isAssignableFrom(clazz:Function/Class/Constructor)
 9. Boolean: FrankBasic.isInstance(clazz:Function/Class/Constructor)
 10. FrankBasic.superApply(methodName,arguments)
### Tools

Created with [Nodeclipse](https://github.com/Nodeclipse/nodeclipse-1)
 ([Eclipse Marketplace](http://marketplace.eclipse.org/content/nodeclipse), [site](http://www.nodeclipse.org))   

Nodeclipse is free open-source project that grows with your contributions.
