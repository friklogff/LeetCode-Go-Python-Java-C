# [62. Unique Paths](https://leetcode.com/problems/unique-paths/)


## 题目

A robot is located at the top-left corner of a *m* x *n* grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

Above is a 7 x 3 grid. How many possible unique paths are there?

**Note:** *m* and *n* will be at most 100.

**Example 1:**

    Input: m = 3, n = 2
    Output: 3
    Explanation:
    From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
    1. Right -> Right -> Down
    2. Right -> Down -> Right
    3. Down -> Right -> Right

**Example 2:**

    Input: m = 7, n = 3
    Output: 28


## 题目大意

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。问总共有多少条不同的路径？


## 解题思路

- 这是一道简单的 DP 题。输出地图上从左上角走到右下角的走法数。
- 由于机器人只能向右走和向下走，所以地图的第一行和第一列的走法数都是 1，地图中任意一点的走法数是 `dp[i][j] = dp[i-1][j] + dp[i][j-1]`
当然，让我为每个版本详细介绍解题思路：

**Go 版本解题思路**

1. **创建二维切片：** 首先，我们创建一个大小为 `n` 的二维切片 `dp`，用于存储每个位置的唯一路径数。Go 中的切片是动态数组，可以方便地动态扩展。

2. **初始化第一行和第一列：** 遍历二维切片，初始化第一行和第一列的路径数为 1，因为在这些位置上，机器人只有一种路径可以到达，即向右或向下移动。

3. **填充二维切片：** 从第二行和第二列开始，遍历每个位置 `(i, j)`，用动态规划的思想计算出到达这个位置的唯一路径数。路径数等于上方格子的路径数加上左边格子的路径数，即 `dp[i][j] = dp[i-1][j] + dp[i][j-1]`。

4. **返回结果：** 最终，右下角格子的路径数就是从左上角到右下角的唯一路径数，即 `dp[n-1][m-1]`。

**Python 版本解题思路**

1. **创建二维列表：** 首先，我们创建一个大小为 `n` x `m` 的二维列表 `dp`，用于存储每个位置的唯一路径数。Python 中的列表是动态数组，可以方便地动态扩展。

2. **初始化第一行和第一列：** 遍历二维列表，初始化第一行和第一列的路径数为 1，因为在这些位置上，机器人只有一种路径可以到达，即向右或向下移动。

3. **填充二维列表：** 从第二行和第二列开始，遍历每个位置 `(i, j)`，用动态规划的思想计算出到达这个位置的唯一路径数。路径数等于上方格子的路径数加上左边格子的路径数，即 `dp[i][j] = dp[i-1][j] + dp[i][j-1]`。

4. **返回结果：** 最终，右下角格子的路径数就是从左上角到右下角的唯一路径数，即 `dp[n-1][m-1]`。

**Java 版本解题思路**

1. **创建二维数组：** 首先，我们创建一个大小为 `n` x `m` 的二维数组 `dp`，用于存储每个位置的唯一路径数。Java 中的二维数组可以表示矩阵。

2. **初始化第一行和第一列：** 遍历二维数组，初始化第一行和第一列的路径数为 1，因为在这些位置上，机器人只有一种路径可以到达，即向右或向下移动。

3. **填充二维数组：** 从第二行和第二列开始，遍历每个位置 `(i, j)`，用动态规划的思想计算出到达这个位置的唯一路径数。路径数等于上方格子的路径数加上左边格子的路径数，即 `dp[i][j] = dp[i-1][j] + dp[i][j-1]`。

4. **返回结果：** 最终，右下角格子的路径数就是从左上角到右下角的唯一路径数，即 `dp[n-1][m-1]`。

**C++ 版本解题思路**

1. **创建二维向量：** 首先，我们创建一个大小为 `n` x `m` 的二维向量 `dp`，用于存储每个位置的唯一路径数。C++ 中的向量可以动态地增加或减少元素。

2. **初始化第一行和第一列：** 遍历二维向量，初始化第一行和第一列的路径数为 1，因为在这些位置上，机器人只有一种路径可以到达，即向右或向下移动。

3. **填充二维向量：** 从第二行和第二列开始，遍历每个位置 `(i, j)`，用动态规划的思想计算出到达这个位置的唯一路径数。路径数等于上方格子的路径数加上左边格子的路径数，即 `dp[i][j] = dp[i-1][j] + dp[i][j-1]`。

4. **返回结果：** 最终，右下角格子的路径数就是从左上角到右下角的唯一路径数，即 `dp[n-1][m-1]`。

希望这些解题思路能够帮助你更好地理解每个版本的代码！如果有任何进一步的问题，请随时向我提问。
## 代码

## Go

```Go
func uniquePaths(m int, n int) int {
    // 创建一个大小为 n 的二维切片 dp，用于存储每个位置的唯一路径数
    dp := make([][]int, n)
    for i := 0; i < n; i++ {
        // 对每一行都创建一个大小为 m 的切片
        dp[i] = make([]int, m)
    }

    // 遍历矩形网格的每个位置
    for i := 0; i < n; i++ {
        for j := 0; j < m; j++ {
            // 如果当前位置是第一行或第一列，那么路径数为1，因为只能向右或向下移动一步
            if i == 0 || j == 0 {
                dp[i][j] = 1
                continue
            }
            // 对于其他位置，路径数等于上方格子的路径数加上左边格子的路径数
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
        }
    }

    // 返回右下角格子的路径数，这就是从左上角到右下角的唯一路径数
    return dp[n-1][m-1]
}

```

## Python

```Python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        # 创建一个大小为 n 的二维数组 dp，用于存储每个位置的唯一路径数
        dp = [[0] * m for _ in range(n)]
        
        # 初始化第一行和第一列的路径数为1，因为只有一种方式可以到达这些位置
        for i in range(n):
            dp[i][0] = 1
        for j in range(m):
            dp[0][j] = 1
        
        # 从第二行第二列开始填充数组，每个位置的路径数等于上方格子和左边格子的路径数之和
        for i in range(1, n):
            for j in range(1, m):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        
        # 返回右下角格子的路径数，即从左上角到右下角的唯一路径数
        return dp[n-1][m-1]

```

## Java

```Java
class Solution {
    public int uniquePaths(int m, int n) {
        // 创建一个大小为 n 的二维数组 dp，用于存储每个位置的唯一路径数
        int[][] dp = new int[n][m];
        
        // 初始化第一行和第一列的路径数为1，因为只有一种方式可以到达这些位置
        for (int i = 0; i < n; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < m; j++) {
            dp[0][j] = 1;
        }
        
        // 从第二行第二列开始填充数组，每个位置的路径数等于上方格子和左边格子的路径数之和
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        
        // 返回右下角格子的路径数，即从左上角到右下角的唯一路径数
        return dp[n-1][m-1];
    }
}

```

## Cpp

```Cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        // 创建一个大小为 n 的二维数组 dp，用于存储每个位置的唯一路径数
        vector<vector<int>> dp(n, vector<int>(m, 0));
        
        // 初始化第一行和第一列的路径数为1，因为只有一种方式可以到达这些位置
        for (int i = 0; i < n; i++) {
            dp[i][0] = 1;
        }
        for (int j = 0; j < m; j++) {
            dp[0][j] = 1;
        }
        
        // 从第二行第二列开始填充数组，每个位置的路径数等于上方格子和左边格子的路径数之和
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                dp[i][j] = dp[i-1][j] + dp[i][j-1];
            }
        }
        
        // 返回右下角格子的路径数，即从左上角到右下角的唯一路径数
        return dp[n-1][m-1];
    }
};

```
当然，让我们分开介绍每个版本的代码所需的基础知识。

**Go 版本**

1. **基础语法：** 了解 Go 语言的基本语法，包括变量、循环、条件语句等。了解切片（slices）的使用，它是 Go 中动态数组的数据结构。

2. **二维切片（Two-dimensional slices）：** 学习如何创建和操作二维切片，即切片的切片，用于表示二维数据结构。

3. **动态规划（Dynamic Programming）：** 理解动态规划的基本概念，了解如何通过填充二维数组来解决动态规划问题。在这个问题中，二维数组表示了网格中各个位置的唯一路径数。

**Python 版本**

1. **基础语法：** 了解 Python 的基本语法，包括变量、循环、条件语句等。

2. **列表（Lists）：** 了解列表的使用，列表是 Python 中的动态数组，可以存储多个元素。

3. **二维列表（Two-dimensional lists）：** 学习如何创建和操作二维列表，它是嵌套列表的概念，用于表示二维数据结构。

4. **动态规划（Dynamic Programming）：** 理解动态规划的基本概念，了解如何通过填充二维数组来解决动态规划问题。在这个问题中，二维数组表示了网格中各个位置的唯一路径数。

**Java 版本**

1. **基础语法：** 了解 Java 的基本语法，包括变量、循环、条件语句等。

2. **二维数组（Two-dimensional arrays）：** 学习如何创建和操作二维数组，它是 Java 中表示矩阵的数据结构。

3. **动态规划（Dynamic Programming）：** 理解动态规划的基本概念，了解如何通过填充二维数组来解决动态规划问题。在这个问题中，二维数组表示了网格中各个位置的唯一路径数。

**C++ 版本**

1. **基础语法：** 了解 C++ 的基本语法，包括变量、循环、条件语句等。

2. **向量（Vectors）：** 了解向量的使用，它是 C++ 中的动态数组，可以存储多个元素。

3. **二维向量（Two-dimensional vectors）：** 学习如何创建和操作二维向量，它是嵌套向量的概念，用于表示二维数据结构。

4. **动态规划（Dynamic Programming）：** 理解动态规划的基本概念，了解如何通过填充二维数组来解决动态规划问题。在这个问题中，二维数组表示了网格中各个位置的唯一路径数。

以上是每个版本代码所需的基础知识。如果你在其中的任何一个方面有疑问，都可以随时问我！