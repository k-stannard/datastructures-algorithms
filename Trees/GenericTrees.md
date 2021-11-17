## A basic tree struct of Generic type

```swift
struct Node<Value> {
    var value: Value
    private(set) var children: [Node]

    init(_ value: Value) {
        self.value = value
        children = []
    }

    init(_ value: Value, children: [Node]) {
        self.value = value
        self.children = children
    }
    
    mutating func add(child: Node) {
        children.append(child)
    }
}

```

## Things you may want to know about value-type trees

	Is the tree equatable?
	How big the tree is
	Find a specific node
	
## Tree traversal using recursion
You can use a computed property in the Node struct to count each child node:
```swift
var count: Int {
    1 + children.reduce(0) { $0 + $1.count }
}

```
This computed property can tell you how large the tree is at any point in the tree.

## Finding a specific node
You may use a recursive method to find a specific node in the tree.
```swift
extension Node where Value: Equatable {
    func find(_ value: Value) -> Node? {
        //If the current node is the node you're seeking, return it's value
        if self.value == value {
            return self
        }
		
        //Otherwise, for each child in the array of children,
        //look for the value recursively and return the value when found
        for child in children {
            if let match = child.find(value) {
                return match
            }
        }		
        return nil
    }
}
```

### Conforming to Equatable
Conforming to `Equatable` will allow you to compare two nodes to see if they are the same.
	
```swift
extension Node: Equatable where Value: Equatable { }
let x = Node("1")
let y = Node("2")
print(x == x) //returns true
print(x != y) //returns true
print(x == y) //returns false
```

You may also conform to `Hashable` and `Codable`, allowing nodes to be used as dictionaries and encode trees of items.

## Family Tree Example
```swift
var andrew = Node("Andrew")
let john = Node("John")
andrew.add(child: john)

var paul = Node("Paul")
let sophie = Node("Sophie")
let charlotte = Node("Charlotte")
paul.add(child: sophie)
paul.add(child: charlotte)

var root = Node("Terry")
root.add(child: andrew)
root.add(child: paul)
```

Printing the output of the tree will give the following results:
```swift
print(root)
// Node<String>(value: "Terry", children: [main.Node<Swift.String>(value: "Andrew", children: [main.Node<Swift.String>(value: "John", children: [])]), main.Node<Swift.String>(value: "Paul", children: [main.Node<Swift.String>(value: "Sophie", children: []), main.Node<Swift.String>(value: "Charlotte", children: [])])])
print(paul)
// Node<String>(value: "Paul", children: [main.Node<Swift.String>(value: "Sophie", children: []), main.Node<Swift.String>(value: "Charlotte", children: [])])
```

## Issues with using Structs

If you wanted to add a child to a node, then print out the number of children, you would get an incorrect return amount due to the behavior of Structs.
Example:
```swift
var paul = Node("Paul")
let sophie = Node("Sophie")
let charlotte = Node("Charlotte")
paul.add(child: sophie)
paul.add(child: charlotte)

let taylor = Node("Taylor")
sophie.add(child: taylor)

print(paul.count) // Returns 3
```

Since Structs use value types instead of a reference type, Paul would be receiving a copy of sophie at that point in the code. Later on when Taylor is added to Sophie, Sophie would be receiving her child on a different copy.

To fix this, you would either have to move the creation of taylor to be earlier in the code:
```swift
var paul = Node("Paul")
let sophie = Node("Sophie")
let taylor = Node("Taylor")
sophie.add(child: taylor)
let charlotte = Node("Charlotte")
paul.add(child: sophie)
paul.add(child: charlotte)
```
or change the Struct into a Class to use a reference type instead.

## Class Example

```swift

final class Node<Value> {
    var value: Value
    private(set) var children: [Node]

    init(_ value: Value) {
        self.value = value
        children = []
    }

    init(_ value: Value, children: [Node]) {
        self.value = value
        self.children = children
    }
    
    func add(child: Node) {
        children.append(child)
    }
}

extension Node: Equatable where Value: Equatable { 
    static func ==(lhs: Node, rhs: Node) -> Bool {
        lhs.value == rhs.value && lhs.children == rhs.children
    }
}

extension Node: Hashable where Value: Hashable { 
    func hash(into hasher: inout Hasher) {
        hasher.combine(value)
        hasher.combine(children)
    }
}

```
The struct is now a `final class` and the `mutating` keyword has been removed from the add child method. Side note: using a class now means that `Equatable` and `Hashable` must be written by hand as well.

The family tree will now return the correct value of the tree.
```swift
var paul = Node("Paul")
let sophie = Node("Sophie")
let charlotte = Node("Charlotte")
paul.add(child: sophie)
paul.add(child: charlotte)

let taylor = Node("Taylor")
sophie.add(child: taylor)

print(paul.count) // Returns 4
```

There are issues using classes instead of structs. Playing with sub trees can potentially cause problems due to using a reference type.

## Function Builders - Swift 5.1 Addition

Function builders are designed to convert several values, in this case tree nodes, into a single value, in this case an array of tree nodes.
You only have to implement functionality for the parts you need.

```swift
@FunctionBuilder //If not using Swift v5.3 or later, you may need to declair as @_functionBuilder
struct NodeBuilder {
    static func buildBlock<Value>(_ children: Node<Value>...) -> [Node<Value>] {
        return children
    }
}
```

Now the initializer on the Node struct may be modified to use the function builder and return whatever the children get from the function.
```swift
init(_ value: Value, @NodeBuilder builder: () -> [Node]) {
    self.value = value
    self.children = builder()
}
```

Now, when building a tree you can do the following:
```swift
let terry = Node("Terry") {
    Node("Paul") {
        Node("Sophie")
        Node("Charlotte")
    }
    
    Node("Andrew") {
        Node("John")
    }
}

print(terry.count) //Returns 6
```
