# Interface Segregation Principle

Fat Protocol Scenario...
Fat Interface

 this principle says we should segregate interfaces, that is, separate them into several ones

 "Clients should not be forced to depend upon interfaces that they do not use."

What is Fat Protocol ?
- Implementing a protocol in a class that has an extra functionality that the class does not need.

```
protocl Human{
  func goToWork()
  func buyAHouse()
  func eat()
  func sleep()
}

protocol Humans: Human{

  func goToWork(){

    print(“Humans go to Work”)
  }

  func buyAHouse(){

    print(“Humans can buy a house”)
  }

  func eat(){


    print(“Humans eat”)
  }

  func sleep(){

    print(“Humans sleep”)
  }
}

protocol Lion:Human{

  func goToWork(){

    //lions cant go to work
  }

  func buyAHouse(){

    //lions cant buy a house
  }

  func eat(){

    print(“Lions eat”)
  }

  func sleep(){

    print(“Lions sleep”)
  }
}

```


To slove this...
implement those protocols only in your class that will need all the functionalities of that protocol, else make another protocol

```

protocol Mammal{
  func eat()
  func sleep()
}
protocol Human: Mammal{
  func goToWork()
  func buyAHouse()
  func eat()
  func sleep()

}

protocol Animal: Mammal{

  func hunt()
}

protocol Humans: Human{

  func goToWork(){

    print(“Humans go to Work”)
  }

  func buyAHouse(){

    print(“Humans can buy a house”)
  }

  func eat(){

    print(“Humans eat”)
  }

  func sleep(){

    print(“Humans sleep”)
  }
}

protocol Lion:Animal{

  
  func eat(){

    print(“Lions eat”)
  }

  func sleep(){

    print(“Lions sleep”)
  }

  func hunt(){
    print(“Lions hunt”)
}

```

Overview ISP
1) This principle says Clients should not be forced to depend upon interfaces that they do not use.

2) Not following this principle and implementing fat interfaces are synonyms. Fat interfaces are not cohesive interfaces. We could say that those interfaces have more than one responsibility and co-relate this to Single Responsibility Principle (SRP) too.

- Respect this principle is positive because:

1) It avoids fat interfaces and, consequently, unnecessary coupling.

2) It avoids unnecessary rebuilding and retesting when some changes are required in the fat interface.

3) It makes the developed software easier to understand and test.
It can inspire less experienced developers in a code base, since they could assume naturally this is a better approach, what could avoid having fat interfaces as a pattern inside that software.

4) Finally, to avoid breaking this principle, the better recommendation is preferring to segregate fat interfaces into smaller ones. Just pay attention on how deep you should go, measuring the present and future benefits of that segregation.
