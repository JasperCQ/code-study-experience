# 代码随想录算法训练营13期 栈与队列part03


 
 **学习时长：2h左右**
 
##  239. 滑动窗口最大值 难度：困难


### 第一想法：

第一想法觉得挺简单的，而且初步分析了一下时间复杂度，觉得也不高

### 题解:

就是采取构造单调队列。

我觉得重点的一句话是：既能维护队列元素先进先出的时间顺序，又能正确维护队列中元素最值————单调队列。

动态集合，维护最值的问题。

~~~
class Solution {
     class MonotonicQueue{
        Deque<Integer> maxque= new ArrayDeque<>();
        public void push(int n){
            //小于n都删除
            while(!maxque.isEmpty() && maxque.getLast()<n){
                maxque.pollLast();
            }
            maxque.addLast(n);
        }

        public int max(){
            return maxque.getFirst();
        }

        public void pop(int n){
            if(n==maxque.getFirst()){
                maxque.pollFirst();
            }

        }

    }



    public int[] maxSlidingWindow(int[] nums, int k) {
        MonotonicQueue window = new MonotonicQueue();
        List<Integer> res = new ArrayList<>();

        for(int i=0;i<nums.length;i++){
            if(i<k-1){
                //先填满窗口的前k-1
                window.push(nums[i]);
            }
            else{
                //窗口向前滑动，加入新数字
                window.push(nums[i]);
                //记录当前窗口最大值
                res.add(window.max());
                //移除旧数字
                window.pop(nums[i-k+1]);
            }

        }

        //转换答案
        int[] arr = new int[res.size()];
        for (int i = 0; i < res.size(); i++) {
            arr[i] = res.get(i);
        }
        return arr;
    }

}

~~~

### 困难：

实际上呢，虽然最笨的方法，时间复杂度也和单调队列在一个量级，但是实际上就是过不了，因为常数上的复杂度确实是不同的



##   347.前 K 个高频元素  难度：中等


### 第一想法:

用优先级队列，维护一个k大小的最小优先级队列

### 题解：

~~~
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // nums 中的元素 -> 该元素出现的频率
        HashMap<Integer,Integer> valtoFreq = new HashMap<>();
        for(int v: nums){
            valtoFreq.put(v,valtoFreq.getOrDefault(v,0)+1);
        }
// 队列按照键值对中的值（元素出现频率）从小到大排序
        PriorityQueue<Map.Entry<Integer,Integer>> pq = new PriorityQueue<>(Comparator.comparing(Map.Entry::getValue));
        for (Map.Entry<Integer, Integer> entry : valtoFreq.entrySet()) {
            pq.offer(entry);
            if (pq.size() > k) {
                // 弹出最小元素，维护队列内是 k 个频率最大的元素
                pq.poll();
            }
        }
        int[] res = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            // res 数组中存储前 k 个最大元素
            res[i] = pq.poll().getKey();
        }

        return res;
    }
}

~~~

### 困难:

最大的困难在于java的优先级队列这个数据结构的不熟悉。
