# Linked List Cycle 

## 풀이 과정
문제를 풀기는 나름 간단한 문제이다.    
배열에 node를 담고 다음 노드로 넘어갈때 노드들을 담아놓은 배열에 똑같은 노드가 존재하는지만 확인하면 되는 문제였다.    
문제라면 간단한 변수라면 모를까 클래스를 같은지는 알지 못한다는데에서 애를 먹었는데   
방법으로는   
1. 클래스에도 값을 비교할수 있게 ListNode에 "Equtable" 프로토콜을 채택하여 값을 비교할수 있게하는 방법과
2. 클래스 주소 자체를 비교하는 참조 연산자 "===" 를 사용하는 방법이 있었다.   

 
다만 여기선 클래스를 extension 할수 없기 때문에 간단한 참조 연산자를 사용했다.


```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public var val: Int
 *     public var next: ListNode?
 *     public init(_ val: Int) {
 *         self.val = val
 *         self.next = nil
 *     }
 * }
 */
class Solution {
    var visitedList: [ListNode] = []
    func hasCycle(_ head: ListNode?) -> Bool {
        guard let node = head else { return false }
        
        return isCycle(listNode: node)
    }
    
    func isCycle(listNode: ListNode?) -> Bool {
        
        guard let node = listNode else { return false }
        
        for index in 0..<visitedList.count {
            if visitedList[index] === node {
                return true
            }
        }
        
        visitedList.append(node)
        return isCycle(listNode: node.next)
    }
}
```

## 또 다른 방법
풀고 찾아보니 더욱 간편하고 빠른 방법이 있었다.   
두개의 포인터를 가지고 가는 방식인데   
한개의 포인터에는 한칸씩 천천히 가며 확인하는 포인터와   
한개는 빠르게 두개씩 검사하며 나아가는 포인터를 가지고   
천천히 가는 포인터와 빠르게 가는 포인터가 같아지는 경우에 true를 리턴하게 하는 방식이다.

```
func hasCycle(_ head: ListNode?) -> Bool {
    if head == nil { return false }
    var slow = head
    var fast = head?.next
    while true {
        if fast == nil { return false }
        if slow === fast { return true }
        slow = slow?.next
        fast = fast?.next?.next
    }
}
