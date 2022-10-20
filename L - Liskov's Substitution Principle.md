# L - Liskov Substitution Principle

The mathematical defintion from Barabara Liskov is : 
“If for each object o1 of type S there is an object o2 of type T, such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T.”

So, this translates to ….

Programs that references an object from a base class must be able to use an object of a derived class without behavior differences and without knowing about its existence.

So, in this article we're going to focus on inheritances for presenting the benefits of respecting the LSP.

```

class Rectangle {

  var width: Double = 0
  var length: Double = 0

  var area : Double {

    return width * height
  }

}

class Square: Rectangle {

  override var width: Double {
      didSet{
        length = width
      }
  }

let objRectangle = Rectangle()
objRectangle.length = 5
objRectangle.width = 3

debugPrint(“Area of Rectangle = \(objRectangle.area)”)

let objSquare = Square()
objSquare.width = 3

debugPrint(“Area of Square = \(objSquare.area)”)


```

## The problem ...

LSP is Broken here...

1)  if we get a single item and change some of their properties, or call one of its methods, we don’t know what item type we would be handling with.

2) imagine that the rectangle is our single item, which we don’t know what type it can be, a square, a rectangle, or even another types, if we have it. The only thing we know about it is that it’s a rectangle. So, it’s fair enough that this object would behavior as a rectangle, right? And that’s where the problem in this example is. The object is not behaving as a rectangle.

3) Another really good example where breaking this principle can be really awful to us developers. For example, when we’re consuming a framework. We don’t want and we don’t need to know all the private structures this framework has, specially when using a public one. So, it would be really nice if we have expected behaviors for those public structures, which wouldn’t depend on our knowledge about the private ones


## The Solution...
Create a protocol Shape, and let the ShapeClasses(Square and Rectangle) inherit from the protocol.

What this does is that creating a protocol to centralize the same behavior both structures should have is going to guarantee that. When consuming them, we don’t use from properties or methods that we shouldn’t. And because of that, we won’t have unexpected behaviors.

```
protocol Shape{
  var area: Double {get}
}
class Rectangle: Shape{

  var width: Double = 0
  var length: Double = 0

  var area : Double {

    return width * height
  }

}

class Square: Shape {

  var width: Double = 0
  
  var area : Double {

    return width * width
  }

  
  }

let objRectangle = Rectangle()
objRectangle.length = 5
objRectangle.width = 3

debugPrint(“Area of Rectangle = \(objRectangle.area)”)

let objSquare = Square()
objSquare.width = 3

debugPrint(“Area of Square = \(objSquare.area)”)



```

Overview: 
1) This will avoid other developers having to know private structures and their behaviors when consuming a framework, an API or any software entity.

2) This for sure will help to reduce bugs, since unexpected behaviors are definitely synonymous of bugs.

3) This will make other developers that will have to maintain or change some of your code lives easier.

4) This principle can be really co-related to the OCP, since when we break LSP, we often beak the OCP simultaneously. So, all the disadvantages read in the previous article of this series would be applied, what’s not really nice.

5) Finally, to avoid breaking this principle, the better recommendation is to prefer composition over inheritance for the abstractions. For sure it’s not a silver bullet, but we really believe it solves the most of cases.
