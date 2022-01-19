## Intersection of Two Linked Lists

Class definition
```swift
 public class ListNode {
     public var val: Int
     public var next: ListNode?
     public init(_ val: Int) {
         self.val = val
         self.next = nil
     }
}
```

### Iterative solution
```swift
func getIntersectionNode(_ headA: ListNode?, _ headB: ListNode?) -> ListNode? {
    if headA == nil || headB == nil { return nil }
        
    var a = headA
    var b = headB
        
    while a !== b {
        if a == nil {
            a = headB
        } else {
            a = a?.next
        }
            
        if b == nil {
            b = headA
        } else {
            b = b?.next
        }
    }
        
    return a
}
```

## Notes

[Leetcode problem](https://leetcode.com/problems/intersection-of-two-linked-lists/)
[Walkthrough by Nick White](https://www.youtube.com/watch?v=IpBfg9d4dmQ)
