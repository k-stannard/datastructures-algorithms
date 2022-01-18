## Remove an element from a linked list
Class definition
```swift
class ListNode {
    var val: Int
    var next: ListNode?
    init() { self.val = 0; self.next = nil; }
    init(_ val: Int) { self.val = val; self.next = nil; }
    init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
 }
 ```
 ### Recursive solution
 
 ```swift
 func removeElements(_ head: ListNode?, _ val: Int) -> ListNode? {
  //assign the next node to the recursive call
    head?.next = removeElements(head?.next, val)
    
    //if the current value is == to the target value
    //return the head?.next will execute the recursive call and skip over the current value
    //else return the current head 
    return head?.val == val ? head?.next : head
}
```
### Iterative solution
 ```swift
func removeElements(_ head: ListNode?, _ val: Int) -> ListNode? {
    // Check if list is empty
    if head == nil { return nil }
    
    // Create pointer
    var current = head
    
    // While the next node is not the end of the list
    // if the next node is the value to be removed
    // set the next node to the node after to remove the value
    // otherwise, move the pointer to the next node
    while current?.next != nil {
        if current?.next?.val == val {
            current?.next = current?.next?.next
        } else {
            current = current?.next
        }
    }
    
    // Check if the current value is the value to remove
    // If so, return the next node to remove the value
    // otherwise return the node as-is
    return head!.val == val ? head!.next : head!
}
```
### Notes

