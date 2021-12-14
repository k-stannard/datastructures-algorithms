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
### Notes

