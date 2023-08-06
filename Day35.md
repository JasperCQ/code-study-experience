
# 代码随想录算法训练营13期 第八章 贪心算法 part04

 
 **学习时长**
 
## 860. 柠檬水找零 难度：简单




### 第一想法:

这个 确实比较简单。

### 题解:
~~~
class Solution {
    public boolean lemonadeChange(int[] bills) {
        HashMap<Integer,Integer> counts = new HashMap<>();
        counts.put(5,0);
        counts.put(10,0);

        for(int i=0;i<bills.length;i++){
            if(bills[i]==5)
                counts.replace(5,counts.get(5)+1);
            else if (bills[i]==10){
                if(counts.get(5)>=1){
                    counts.replace(5,counts.get(5)-1);
                    counts.replace(10,counts.get(10)+1);
                }
                else
                    return false;
            }
            else{
                if(counts.get(10)>=1 && counts.get(5)>=1){
                    counts.replace(5,counts.get(5)-1);
                    counts.replace(10,counts.get(10)-1);
                }
                else if(counts.get(5)>=3){
                    counts.replace(5,counts.get(5)-3);
                }
                else
                    return false;
            }
        }
        return true;

    }
}

~~~


##  难度：


### 第一想法:



### 题解:



##  难度：


### 第一想法:



### 题解:


