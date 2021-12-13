## Merge Two Sorted Singlely-Linked Lists
### Linked List class definition
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
     func mergeTwoLists(_ list1: ListNode?, _ list2: ListNode?) -> ListNode? {  
     //check if either node is nil. If so, return the other node
        if list1 == nil  {
            return list2
        } else if list2 == nil { 
            return list1
        }
        
        //Setup merge list, (not entirely needed. can be done recursively without allocating new space)
        var mergedList: ListNode?
        
        //find which node contains the lesser value
        //assigned the merge list to the node
        //recursively call the method for the next node
        if list1!.val < list2!.val {
            mergedList = list1
            mergedList?.next = mergeTwoLists(list1?.next, list2)
        } else {
            mergedList = list2
            mergedList?.next = mergeTwoLists(list1, list2?.next)
        }
        
        //return the newly merged list
        return mergedList
    }
 ```
 ## Notes
 There was an issue when trying to unwrap the optional nodes with a guard statement at the beginning of the method. The two lists would merge properly up until the last node. The very last node of the second list would not be added to the merge list. 
 ```swift 
 guard let head1 = list1 else { return nil }
 ```
I think defaulting to nil in the return case caused some sort of issue. 

Resolved by explicitely unwrapping with the original parameter with a bang.
 
 source: https://leetcode.com/problems/merge-two-sorted-lists/
 
