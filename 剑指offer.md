# 2020.3.14

## 34.二叉树中和为某一值的路径

:black_nib:解题思路：

1. 二叉树的先序遍历

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
	public List<List<Integer>> pathSum(TreeNode root, int sum) {
		List<List<Integer>> lists = new ArrayList<>();
		List<Integer> path = new ArrayList<>();
		getLists(root, path, lists, sum);
		return lists;
	}

	private void getLists(TreeNode root, List<Integer> path, List<List<Integer>> lists, int sum) {
		if (root == null) {
			return;
		}
		path.add(root.val);
		sum -= root.val;
		if (root.left == null && root.right == null && sum == 0) {
			lists.add(new ArrayList<>(path));
		}
		if (root.left != null) {
			getLists(root.left, path, lists, sum);
		}
		if (root.right != null) {
			getLists(root.right, path, lists, sum);
		}
		path.remove(path.size() - 1);
	}
}
```

## 55-I.二叉树的深度

:black_nib:解题思路：

1. 遍历根节点，若`root == null`，返回0；否则返回左右子树的最大深度。

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
	public int maxDepth(TreeNode root) {
		if (root == null) {
			return 0;
		}
		int leftHight = maxDepth(root.left);
		int rightHight = maxDepth(root.right);
		return 1 + Math.max(leftHight, rightHight);
	}
}
```

## 55-II.平衡二叉树

:black_nib:解题思路：

1. 遍历根节点的左右节点，判断其深度之差是否小于2

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
	public boolean isBalanced(TreeNode root) {
		if (root == null) {
			return true;
		}
		return Math.abs(getHight(root.left) - getHight(root.right)) < 2 && isBalanced(root.left) && isBalanced(root.right);
	}

	/**
	 * 获取树的高度
	 */
	private int getHight(TreeNode root) {
		if (root == null) {
			return -1;
		}
		return 1 + Math.max(getHight(root.left), getHight(root.right));
	}
}
```