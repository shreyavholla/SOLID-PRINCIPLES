# S - SINGLE RESPONSIBILITY PRINCIPLE

- Every Class must have a single responsibility.
- The principle states that a responsibility is basically a reason for change.
- If it is possible to think in more than one reason to change a specific, class it is because this class is assuming more than one responsibility.

Let us consider the following context : 
class Square
class GeometricGraphics
protocol Persistence

```
protocol Persistance {
  func save(_ square: Square)
}

class Square {
  let edge: Int
  let persistence: Persistence

  init(edge: Int, persistence: Persistence) {
    self.edge = edge
    self.peristence = persistence
  }

  //First Responsibility — calculates area of the square
  func area() -> Int {
    return edge * edge
  }

  //Second Responsibility - saves tge square with the persistence help
  func save() {
    persistence.save(self)
  }

  //Third - Coupled Responsibility - saves the square only if its area is greater than 20
  func saveAccordingToArea() {
    let area = self.area()
    if area > 20 {
      persistence.save(self)
    }
  }
}

//this class draws the square in a visual interface
  class GeometricGraphics {
    func draw(_ square: Square) {
      let squareArea = square.area()
      //draws the square in the application screen
    }

}

```

## What is wrong with this?
1) class Square has more than one responsibility
  - but why is it a problem ?
            => for example, and eventual change in the persistence structure will impact in a modification also in the Square Class. Since the GeometricGraphics structure depends on Square after the changes have been done, this structure is going to have to be rebuilt.
            => This is bad, since GeometricGraphics class is not dependent on the Persistence structure.

2) Coupling two responsibilities
3) One responsibility is going to hinder the testability of this structure.

# The solution...
create 2 protocols that would contain the area() and save() methods.
Let the Square class implement these two methods

```

protocol SquareGeometrics {
    func area() -> Int
}

protocol SquarePersistence {
    func save()
}

class Square: SquareGeometrics, SquarePersistence {
    let edge: Int
    let persistence: Persistence

    init(edge: Int, persistence: Persistence) {
        self.edge = edge
        self.persistence = persistence
    }

    // First Responsibility
    func area() -> Int {
        return edge * edge
    }

    // Second Responsibility
    func save() {
        persistence.save(self)
    }
}

class GeometricGraphics {
    // Note the dependency of this class in Square was changed for 
    // for just one of the responsibilities
    func draw(_ square: SquareGeometrics) {
        let squareArea = square.area()
        // Draw the square in the application screen
    }
}
```


