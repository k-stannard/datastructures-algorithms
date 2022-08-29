# Sets

Similar to an array, a set is a collection of items with some slight differences.

Sets have the following additional characteristics:  
1. Unordered elements
2. Elements are unique - you cannot have two of the same elements in a set

## Advantages

Sets have the advantage of being a very performant data structure. Due to sets having no order and unique values, element insertion, removal, and lookup times are very quick. To find an element in an array, you have to check each index until a specific element is found, and depending on the size of the array - it could potentially take a very long time. Same idea for insertion and removal depending on the criteria. This is not the case for a set. 

Sets conform to *Hashable*, which gives the elements a constant time lookup through its hash value.
