# Structs and Classes Lab - 2


## Question 1

Using the Room struct below, write code that demonstrates that it is a value type.

```swift
struct Room {
    var maxOccupancy: Int
    let length: Double
    let width: Double
}

let room1 = Room(maxOccupancy: 2, length: 5.5, width: 10.5)
var room2 = room1
room2.maxOccupancy = 3

print(room1)
//prints Room(maxOccupancy: 2, length: 5.5, width: 10.5)

print(room2)
//Room(maxOccupancy: 3, length: 5.5, width: 10.5)

//initial value of room2 is same as room1.  
//Changes made to properties of room2 do not overide properties of room1.
    
```
## Question 2

Using the Bike class below, write code that demonstrates that it is a reference type.

```swift
class Bike {
    var wheelNumber = 2
    var hasBell = false
}

let bicycle = Bike()
bicycle.hasBell
bicycle.wheelNumber = 3

print(bicycle.wheelNumber) // original value was 2 then changed to 3

let bike2 = bicycle
bike2.hasBell = true
bike2.wheelNumber = bicycle.wheelNumber

print(bike2.wheelNumber) //print 3
print(bike2.hasBell) //double checking, it changed the reference value to 'true'
```

## Question 3

a. Given the Animal class below, create a Bird subclass with a new `canFly` property.

```swift
class Animal {
    var name: String = ""

    init(name: String) {
        self.name = name
    }

    func printDescription() {

        print("I am an animal named \(name)")

    }
}

class Bird: Animal {
    var canFly = true

    init(name: String, canFly: Bool) {
        self.canFly = canFly
        super.init(name: name)
    }
}

var newBird = Bird(name:"kiki", canFly: true)
newBird.name
newBird.canFly
newBird.printDescription()
```

b. Override the printDescription method to have the instance of the Bird object print out its name and whether it can fly


```swift

class Animal {
    var name: String = ""

    init(name: String) {
        self.name = name
    }

    func printDescription() {
    print("I am an animal named \(name)")
    }
}

class Bird: Animal {
    var canFly = true

    init(name: String, canFly: Bool) {
    self.canFly = canFly
    super.init(name: name)
    }

    func flyPrint() -> String {
        if self.canFly == true {
            return "I can fly"
        } else {
            return "I cannot fly"
    }
}

    override func printDescription() {
        print("I'm \(name) and \(String(describing: flyPrint()))")
    }
}

var newBird = Bird(name: "kiki", canFly: true)
newBird.name
newBird.canFly
newBird.printDescription()
```

## Question 4

```swift
class Bike {
  let wheelNumber = 2
  let wheelWidth = 1.3
  var hasBell = true
  func ringBell() {
    if hasBell {
      print("Ring!")
    }
  }
}
```
a. Create a `LoudBike` subclass of Bike.  When you call `ringBell` it should ring the bell in all caps.

b. Give `LoudBike` a new method called `ringBell(times:)` that rings the bell a given number of times
```swift

class Bike {
    let wheelNumber = 2
    let wheelWidth = 1.3
    var hasBell = true

    func ringBell() {
        if hasBell {
        print("Ring!")
        }
    }
}

class LoudBike: Bike {
    var model: String = ""

    init(model: String, wheelNumber: Int, wheelWidth: Double, hasBell: Bool) {
        self.model = model
    }

    override func ringBell() {
        if hasBell {
            print("RING!")
        }
    }

    func bellsound(times: Int) {
        for _ in 0...times where hasBell == true {
            ringBell()
            }
    }
}


var bike = LoudBike(model: "Mountain Bike", wheelNumber: 2, wheelWidth: 1.3, hasBell: true)

bike.model
bike.ringBell()
bike.wheelNumber
bike.wheelWidth
bike.hasBell
bike.bellsound(times: 5)


```

## Question 5

```swift
class Shape {
    var name: String { return "This is a generic shape" }
    var area: Double { fatalError("Subclasses must override the area") }
    var perimeter: Double { fatalError("Subclasses must override the perimeter") }
}
```

a. Given the `Shape` object above, create a subclass `Square` with a property `sideLength` with a default value of 5.
```swift
class Square: Shape {
    var sideLength = 5.0
}

```
b. Override the `area` and `perimeter` computed values so the return the area/perimeter of the square as appropriate

c. Override the `name` property of `Square` so that it returns a String containing its name ("Square") and its area and perimeter
```swift
//answer for 5.b. and 5.c.

class Shape {
    var name: String { return "This is a generic shape" }
    var area: Double { fatalError("Subclasses must override the area") }
    var perimeter: Double { fatalError("Subclasses must override the perimeter") }
}
class Square : Shape {
    var sideLength = 5

    override var name: String {
        get {
            return "Square shape"
        }
    }
    override var area: Double {
        get {
            return Double(sideLength * sideLength)
        }
    }
    override var perimeter: Double {
        get {
            return Double(4 * sideLength)
        }
    }
}

var otherSquare = Square()

print(otherSquare.name, "with area of: \(otherSquare.area), and perimeter of: \(otherSquare.perimeter)")
    //print--> 'Square shape with area of: 25.0, and perimeter of: 20.0'

```

d. Create a class `Rectangle` that subclasses from `Shape`.  Give it a `width` property with a default value of 6 and a `height` property with a default value of 4

e. Override the `name` property of `Rectangle` so that it returns a String containing its name ("Rectangle") and its area and perimeter.
```swift
//answer for 5.d. and 5.e.

class Rectangle: Shape {
    var width = 6
    var height = 4

    override var name: String {
        get {
            return "Rectangle shape"
        }
    }
    override var area: Double {
        get {
            return Double(width * height)
        }
    }
    override var perimeter: Double {
        get {
            return Double((width * 2) + (height * 2))
        }
    }
}

var otherRectangle = Rectangle()

print(otherRectangle.name, "with area of: \(otherRectangle.area), and perimeter of: \(otherRectangle.perimeter)")
    //print -->'Rectangle shape with area of: 24.0, and perimeter of: 20.0'

```

f. (BONUS) What happens when you run the code below?  Explain why.

```swift
var myShapes = [Shape]()

myShapes.append(Square())
myShapes.append(Rectangle())

for shape in myShapes {
    print("This is a \(shape.name) with an area of \(shape.area) and a perimeter of \(shape.perimeter)")
}

//print --> 'This is a Square shape with an area of 25.0 and a perimeter of 20.0'
//print --> 'This is a Rectangle shape with an area of 24.0 and a perimeter of 20.0'

//because the value in "myShapes" variable were 'appended' with most recent values, when they were called by "print"

```
class Square: Shape {
var sideLength = 5.0
}
    init(name: String, area: Double, perimeter: Double, sideLength: Double) {
        self.sideLength = sideLength
    }

    override var area: Double {
        get {
        return sideLength * sideLength
        }
    }
}

var square1 = Square(name: "square", area: 25.0, perimeter: 20.0, sideLength: 5.0)

print(square1.area)
```


## Question 6

a. Given the Point object below, complete the `distance` method so that it returns the distance between a given point.

The equation for the distance formula can be found [here](https://www.mathsisfun.com/algebra/distance-2-points.html) and is give by:

```swift
let horizontalDistance = pointOneXValue - pointTwoXValue
let verticalDistance = pointOneYValue - pointTwoYValue
let distanceBetweenTwoPoints = sqrt(horizontalDistance * horizontalDistance + verticalDistance * verticalDistance)
```

`sqrt` is a method in Swift that gives the square root.  Make sure to have `import Foundation` or `import UIKit` to use this method.

```swift
struct Point {
    let x: Double
    let y: Double
    func distance(to point: Point) -> Double {
      //Code in your answer here
    }
}

let pointOne = Point(x: 0, y: 0)
let pointTwo = Point(x: 10, y: 10)

print(pointOne.distance(to: pointTwo)) //Prints 14.142135623730951
```


b. Given the above Point object, and Circle object below, add a `contains` method that returns whether or not a given point is on the circle

```swift
struct Circle {
    let radius: Double
    let center: Point
}

let pointOne = Point(x: 0, y: 0)
let circleOne = Circle(radius: 5, center: pointOne)
let pointTwo = Point(x: 5, y: 0)
let pointThree = Point(x: 4, y: 0)
let pointFour = Point(x: sqrt(12.5), y: sqrt(12.5))
circleOne.contains(pointTwo) //true
circleOne.contains(pointThree) // false
circleOne.contains(pointFour) //true
```

c. Add another method to `Circle` that returns a random point on the circle

Hint: Given the radius of a circle and the x value of a point on the circle, the y value of the point is defined by:

```
√(r^2) - (x^2)
```

```swift
circleOne.contains(circleOne.getRandomPoint()) //Should always be true
```


## Question 7

a. Create a struct called HangmanModel with 3 properties `targetWord: String`, `numberOfIncorrectGuesses: Int` and `guessedLetters: [Character]`.

b. Add a method called `playerWon` that returns whether all of the characters in `targetWord` are in `guessedLetters`

```swift
var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","e","o","l"]
model.playerWon //true
```

c. Add a method called `printDisplayVersionOfWord` that prints the `targetWord` replacing characters that are not in `guessedLetters` with "\_"

```
var model = HangmanModel()
model.targetWord = "hello"
model.guessedLetters = ["h","l"]
model.printDisplayVersionOfWord
//prints h_ll_
```

d. Add a method called `guess(_:)` that takes in a character as input, and updates `guessedLetters` and `numberOfIncorrectGuesses` as appropriate.

```swift
var model = HangmanModel()
model.targetWord = "hello"
model.guess("h")
model.guess("a")
model.guessedLetters // ["h", "a"]
model.numberOfIncorrectGuesses // 1
```

e. Have `guess(_:)` also print out the current display version of the word, the number of incorrect guesses and if the player has won.
