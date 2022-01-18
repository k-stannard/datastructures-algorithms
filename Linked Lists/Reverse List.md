## Reverse a Linked List

Class definition
```swift
 public class ListNode {
     public var val: Int
     public var next: ListNode?
     public init() { self.val = 0; self.next = nil; }
     public init(_ val: Int) { self.val = val; self.next = nil; }
     public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
 }

 ```
Reverse list method
```swift
func reverseList(_ head: ListNode?) -> ListNode? {
    // Init current pointer and previous pointer
    var current = head
    var previous = head
    
    // while current is not at the end of the list
    // Init the next pointer
    while current != nil {
        var next = current?.next
        current?.next = previous
        previous = current
        current = next
    }
    
    // Return the previous node for the reversed list
    return previous
}
```
