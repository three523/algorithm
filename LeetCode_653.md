# LeetCode_653. Two Sum IV - Input is a BST
- Binary Search Tree의 root와 타겟 넘버 k가 주어질때, 두개 요소의 합이 타겟 넘버와 같은 경우 true를 넘겨준다

<img width="794" alt="스크린샷 2021-12-27 오후 8 15 46" src="https://user-images.githubusercontent.com/71269216/147466655-d0bf4596-c6a3-48ed-af80-e4c721bb4283.png">

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public var val: Int
 *     public var left: TreeNode?
 *     public var right: TreeNode?
 *     public init() { self.val = 0; self.left = nil; self.right = nil; }
 *     public init(_ val: Int) { self.val = val; self.left = nil; self.right = nil; }
 *     public init(_ val: Int, _ left: TreeNode?, _ right: TreeNode?) {
 *         self.val = val
 *         self.left = left
 *         self.right = right
 *     }
 * }
 */
class Solution {
    var list = Set<Int>()
    
    func dfs(_ node: TreeNode?, _ k: Int) -> Bool {
        guard let node = node else { return false }
        
        if list.contains(k - node.val) {
            return true
        }
        
        list.insert(node.val)
        
        return dfs(node.left,k) || dfs(node.right,k)
    }
    
    func findTarget(_ root: TreeNode?, _ k: Int) -> Bool {
        guard let node = root else { return false }
        
        return dfs(node,k)
    }
}
```
