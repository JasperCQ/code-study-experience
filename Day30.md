
# 代码随想录算法训练营13期 第七章 回溯算法part06

今天的题确实都很难，我就也不写了，写下思路先。

 
 **学习时长**
 
## 332. 重新安排行程 难度：困难


### 第一想法:
当时就觉得这个不是个图的题吗？，然后路径也是求最小的，但是因为是字典序最小的，所以其实用不着图里面那些复杂的最小路径方法，用回溯算法就可以。
要保证字典序最小的话，就先排个序就可以。然后从左往右遍历节点就行。


### 题解:
首先需要构建图的一些基础，比如邻接表形式的边。

~~~
class Solution {
    // 邻接表形式的图，key 是机场名字，value 是从该机场出发能够到达的机场列表
    Map<String, List<String>> graph = new HashMap<>();
    // 和 graph 对应，记录每张机票是否被使用过
    // 比如 graph["JFK"][2] = true 说明从机场 JFK 出发的第 3 张机票已经用过了
    Map<String, boolean[]> used = new HashMap<>();
    List<List<String>> tickets;

    // 回溯算法使用的数据结构
    LinkedList<String> track = new LinkedList<>();
    // 回溯算法记录结果
    List<String> res = null;

    public List<String> findItinerary(List<List<String>> tickets) {
        this.tickets = tickets;
        // 1. 用机场的名字构建邻接表
        for (List<String> ticket : tickets) {
            String from = ticket.get(0);
            String to = ticket.get(1);
            if (!graph.containsKey(from)) {
                graph.put(from, new ArrayList<>());
            }
            graph.get(from).add(to);
        }
        // 2. 对邻接表的每一行进行排序，保证字典序最小
        for (List<String> list : graph.values()) {
            Collections.sort(list);
        }
        // 3. 初始化 used 结构，初始值都为 false
        for (String key : graph.keySet()) {
            int size = graph.get(key).size();
            used.put(key, new boolean[size]);
        }
        // 4. 从起点 "JFK" 开始启动 DFS 算法递归遍历
        track.add("JFK");
        backtrack("JFK");
        return res;
    }

    void backtrack(String airport) {
        if (res != null) {
            // 已经找到答案了，不用再计算了
            return;
        }
        if (track.size() == tickets.size() + 1) {
            // track 里面包含了所有的机票，即得到了一个合法的结果
            // 注意 tickets.size() 要加一，因为 track 里面额外包含了起点 "JFK"
            res = new LinkedList<>(track);
            return;
        }
        if (!graph.containsKey(airport)) {
            // 没有从 s 出发的边
            return;
        }

        // 遍历当前机场所有能够到达的机场
        List<String> nextAirports = graph.get(airport);
        for (int nextIndex = 0; nextIndex < nextAirports.size(); nextIndex++) {
            String nextAirport = nextAirports.get(nextIndex);
            if (used.get(airport)[nextIndex]) {
                // 如果这张机票被使用过，跳过
                continue;
            }
            // 做选择
            used.get(airport)[nextIndex] = true;
            track.add(nextAirport);
            // 递归
            backtrack(nextAirport);
            // 撤销选择
            used.get(airport)[nextIndex] = false;
            track.removeLast();
        }
    }
}

~~~


## 51. N 皇后  难度：困难




### 第一想法:

第一想法其实还真没有太多思路，就只是感觉就是每一行，每一行的选呗，但其实这个就可以带进回溯算法的模板，就是每一行当作依次选择，然后保证每次选择都做合法的选择就行。



### 题解:

~~~
class Solution {
    List<List<String>> res = new ArrayList<>();

    /**
     * 输入棋盘边长 n，返回所有合法的放置
     */
    public List<List<String>> solveNQueens(int n) {
        // '.' 表示空，'Q' 表示皇后，初始化空棋盘。
        List<String> board = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < n; i++) {
            sb.append('.');
        }
        for (int i = 0; i < n; i++) {
            board.add(sb.toString());
        }
        backtrack(board, 0);
        return res;
    }

    /**
     * *路径：board 中小于 row 的那些行都已经成功放置了皇后
     * *选择列表：第 row 行的所有列都是放置皇后的选择
     * *结束条件：row 超过 board 的最后一行
     */
    private void backtrack(List<String> board, int row) {
        if (row == board.size()) {
            res.add(new ArrayList<>(board));
            return;
        }

        int n = board.get(row).length();
        for (int col = 0; col < n; col++) {
            // 排除不合法选择
            if (!isValid(board, row, col)) {



                continue;
            }
            // 做选择
            char[] arr = board.get(row).toCharArray();
            arr[col] = 'Q';
            board.set(row, String.valueOf(arr));
            // 进入下一行决策
            backtrack(board, row + 1);
            // 撤销选择
            arr[col] = '.';
            board.set(row, String.valueOf(arr));
        }
    }

    /* 是否可以在 board[row][col] 放置皇后？*/
    private boolean isValid(List<String> board, int row, int col) {
        int n = board.size();

        // 检查列是否有皇后互相冲突
        for (int i = 0; i <= row; i++) {
            if (board.get(i).charAt(col) == 'Q') {
                return false;
            }
        }

        // 检查右上方是否有皇后互相冲突
        for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
            if (board.get(i).charAt(j) == 'Q') {
                return false;
            }
        }

        // 检查左上方是否有皇后互相冲突
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board.get(i).charAt(j) == 'Q') {
                return false;
            }
        }

        return true;
    }
}


~~~


## 37. 解数独 难度：困难


### 第一想法:

这个题其实和N皇后是一样的，可以对每一行，从左往右填空格，然后填合法的就行。



### 题解:
~~~

class Solution {
    public void solveSudoku(char[][] board) {
        backtrack(board, 0, 0);
    }

    boolean backtrack(char[][] board, int i, int j) {
        int m = 9, n = 9;
        if (j == n) {
            // 穷举到最后一列的话就换到下一行重新开始。
            return backtrack(board, i + 1, 0);
        }
        if (i == m) {
            // 找到一个可行解，触发 base case
            return true;
        }

        if (board[i][j] != '.') {
            // 如果有预设数字，不用我们穷举
            return backtrack(board, i, j + 1);
        }

        for (char ch = '1'; ch <= '9'; ch++) {
            // 如果遇到不合法的数字，就跳过
            if (!isValid(board, i, j, ch))
                continue;

            board[i][j] = ch;
            // 如果找到一个可行解，立即结束
            if (backtrack(board, i, j + 1)) {
                return true;
            }
            board[i][j] = '.';
        }
        // 穷举完 1~9，依然没有找到可行解，此路不通
        return false;
    }

    // 判断 board[i][j] 是否可以填入 n
    boolean isValid(char[][] board, int r, int c, char n) {
        for (int i = 0; i < 9; i++) {
            // 判断行是否存在重复
            if (board[r][i] == n) return false;
            // 判断列是否存在重复
            if (board[i][c] == n) return false;
            // 判断 3 x 3 方框是否存在重复
            if (board[(r/3)*3 + i/3][(c/3)*3 + i%3] == n)
                return false;
        }
        return true;
    }
}

~~~
