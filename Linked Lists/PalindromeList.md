## Linked List Palindrome Algorithm

To solve this algorithm:
- you will need two pointers at the head of the linked list
- one pointer will iterate over each node faster than the other
- by the time the fast pointer reaches the end of the list, the slow pointer will be at the middle of the list
- reverse one half of the list
- iterate over the list and check if both pointers are the same

### Class Definition
```swift
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init() { self.val = 0; self.next = nil; }
 *     public init(_ val: Int) { self.val = val; self.next = nil; }
 *     public init(_ val: Int, _ next: ListNode?) { self.val = val; self.next = next; }
 * }
 */
```

### isPalindrome method

```swift
func isPalindrome(_ head: ListNode?) -> Bool {
  // Check if list is nil
    if head == nil { return true }
  
  // Init slow and fast pointers
    var slow = head
    var fast = head
  
  // While the fast pointer's next & next.next nodes have not reached end of the list, iterate through list
  // Point fast to the next.next node and slow to its next node
    while fast?.next != nil && fast?.next?.next != nil {
        fast = fast?.next?.next
        slow = slow?.next
    }
  
  // Set one pointer to the head of the first half of the list
  // And the other to the head of the second half of the list in reversed order
  // Since slow is already in the middle of the list, 
  // you send the next node which will return the previous node when reversed.
    var firstHalf = head
    var secondHalf = reverseList(slow?.next)
  
  // While not at the end of the list
  // Check each value of both pointers
  // If one differs, the list is not a palindrome
  // Otherwise continue to the next node
    while firstHalf?.next != nil && secondHalf?.next != nil {
        if firstHalf?.val != secondHalf?.val {
            return false
        }
          
        firstHalf = firstHalf?.next
        secondHalf = secondHalf?.next
    }
  
    // If method makes it through all the checkpoints
    // The list is a palindrome
    return true
}

// Reverse List Method
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

## Notes

[isPalindrome problem @ Leetcode](https://leetcode.com/problems/palindrome-linked-list/)
