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
## 12.矩阵中的路径

:black_nib:解题思路：

1. 大佬：深度优先搜索+剪枝

```java
class Solution {
	public boolean exist(char[][] board, String word) {
		char[] words = word.toCharArray();
		int m = board.length;
		int n = board[0].length;
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < n; j++) {
				if (dfs(board, words, i, j, 0)) {
					return true;
				}
			}
		}
		return false;
	}

	private boolean dfs(char[][] board, char[] words, int i, int j, int k) {
		if (i < 0 || j < 0 || i >= board.length || j >= board[i].length || words[k] != board[i][j]) {
			return false;
		}
		if (k == words.length - 1) {
			return true;
		}
		char temp = board[i][j];
		board[i][j] = '/';
		boolean result = dfs(board, words, i + 1, j, k + 1) || dfs(board, words, i - 1, j, k + 1)
				|| dfs(board, words, i, j + 1, k + 1) || dfs(board, words, i, j - 1, k + 1);
		board[i][j] = temp;
		return result;
	}
}
```
## 63.股票的最大利润

:black_nib:解题思路：

```java
class Solution {
	public int maxProfit(int[] prices) {
		int len = prices.length;
		if (len < 1) {
			return 0;
		}
		int min = prices[0];
		int max = 0;
		for (int i = 1; i < len; i++) {
			min = min > prices[i] ? prices[i] : min;
			max = max < prices[i] - min ? prices[i] - min : max;
		}
		return max;
	}
}
```

