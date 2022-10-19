# O - Open Close Principle
The open close principle states that software entities ( modules, classes, functions, etc) should be open for **Extension** and closed for **Modification**.


Consider The following code :

a shape calculator 

```
```
```
class Rectangle {

 let width: Double
 let height: Double

 init(width: Double, height: Double){

     self.width = width
     self.height = height
   
 }

 func calculateArea() -> Double {

      return width*height
  }
}

class Circle {

 let radius: Double

 init(radius: Double){

     self.radius = radius
 }

 func calculateArea() -> Double {

      return  Double.pi ` * radius * radius`
  }
}

class AreaCalculator{

    func area(shape: Rectangle) -> Double{

            return shape.calculateArea()
      }

    func area(shape: Triangle) -> Double{

            return shape.calculateArea()
      }
}

let objCalculator = AreaCalculator()

let objRectangle = Rectangle(width:2, height:2)
let objTraingle = Triangle(radius:5)
print(“Area: \(objCalculator.area(shape: objRectangle))”)

```

The problem with this is:
- it disobeys open - close principle
- its not closed to modification
- the areaCalculator class needs to be modified whenever a new shape is added


The solution

```

protocol Shape{

  function calculateArea() -> Double 
}

class Rectangle : Shape {

 let width: Double
 let height: Double

 init(width: Double, height: Double){

     self.width = width
     self.height = height
   
 }

 func calculateArea() -> Double {

      return width*height
  }
}

class Circle : Shape{

 let radius: Double

 init(radius: Double){

     self.radius = radius
 }

 func calculateArea() -> Double {

      return  Double.pi ` * radius * radius`
  }
}

class AreaCalculator{

    func area(shape: Shape) -> Double{

            return shape.calculateArea()
      }
}

et objCalculator = AreaCalculator()

let objRectangle = Rectangle(width:2, height:2)
let objTraingle = Triangle(radius:5)


```

Now you see, that with the introduction of a protocol Shape, the class AreaCalculator follows the open-close principle, where it is open to extension to other shape classes as well as closed to modificiation.

- Ensure this condition is positive for the following factors:

1) This will avoid that changes or extensions in a module imply in changes in other modules, what can generate overwork for developer and also an unnecessary rebuilt and retest of some modules because of that.

2) This will also avoid that some new bugs and problems arise, besides facilitating a lot the business rules changes of an application, since the extension will not lead the alteration of other modules.

3) Abstractions (Use of protocols in Swift) in general are going to solve the problem of OCP violation.

4) Enums in general are going to disrespect the OCP, so care must be taken with its use. When concluding that is really necessary to use this structure, it is recommended to centralize the switch-case implementation that uses all of those cases. This is going to avoid modifications in lots of pieces of code throughout the application, when an extension is necessary.

5) It is impossible to turn a code 100% closed for modifications, so the best to do is to try to measure the main changing axes and make the code closed for these axes.

6) The use of private variables inside classes is an heuristic derived from this principle and can also be useful to respect it. The same occur to the heuristic that says to not use global variables.

 