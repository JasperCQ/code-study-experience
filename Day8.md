
# 代码随想录算法训练营13期 字符串part01 、344.反转字符串 、 541. 反转字符串II、剑指Offer 05.替换空格 、151.翻转字符串里的单词、 剑指Offer58-II.左旋转字符串 


 
 **学习时长：3h多一点**
 
## 344. 反转字符串 难度：简单


### 第一想法：

python里面我记得用reverse方法就行，java里面应该也有对应的，不过我不确定，所以如果不用的话，感觉用双指针就可以

~~~
class Solution {
   public void reverseString(char[] s) {
        int left = 0;
        int right= s.length-1;

        while(left<right){
            char temp= s[left];
            s[left]=s[right];
            s[right]=temp;
            left++;
            right--;
        }
    }
}
~~~
### 题解:

就是使用双指针做，我也去搜了下reverse 函数， java 的reverse 是 StringBuffer才有所以要使用的话，用下面这个格式
String reverse = new StringBuffer(string).reverse().toString();

### 困难


 

 
## 541. 反转字符串 II 难度：简单


### 第一想法：

由于需要遍历s 字符串，然后慢慢构造出来新的字符串，并且里面存在很多小的字符串需要处理，我想用一个Stringbuffer来存储


~~~

class Solution {
    public String reverseStr(String s, int k) {
        int n = s.length();
        char[] arr = s.toCharArray();
        for (int i = 0; i < n; i += 2 * k) {
            reverse(arr, i, Math.min(i + k, n) - 1);
        }
        return new String(arr);
    }

    public void reverse(char[] arr, int left, int right) {
        while (left < right) {
            char temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
}


~~~


### 题解:

这道题自己做的不好，想的很复杂，思路很明显不够清晰，而且java直接处理字符串是真的麻烦，也容易弄错，虽然有substring方法可以使用，所以之后还是直接都转成charArray，最后返回的时候再转回来比较好。

### 困难




 
## 剑指 Offer 05. 替换空格 难度：简单

~~~

class Solution {
    public String replaceSpace(String s) {
        String[] str_ls=s.split("");
        for(int i =0 ;i<str_ls.length;i++){
            if (str_ls[i].equals(" "))
                str_ls[i]="%20";
        }
        StringBuffer res_buffer= new StringBuffer();
        for (String stri:str_ls){
            res_buffer.append(stri);
        }
        return res_buffer.toString();
    }
}

~~~


### 第一想法：

这个在python中我没记错应该也是有函数可以直接替换的，不用函数的话，转换成charArray应该就行

### 题解:

在做的时候发现首先是，不能用char 数组，因为要转成的是两个字符，

### 困难


## 151. 反转字符串中的单词 难度：中等


### 第一想法：

隐约见过这样的题，所以知道应该是反转两次就能达到效果



~~~

class Solution {
    public String reverseWords(String s) {
        String[] word_ls= split(s.strip());
        StringBuffer res_buffer = new StringBuffer();
        for(String word: word_ls){
            System.out.println(word);
            //判断是否为空格
            if (word.equals(" "))
                continue;
            res_buffer.append(reverse(word.strip()));
            //记得加空格
            res_buffer.append(" ");
        }
        res_buffer.reverse();
        return res_buffer.toString().strip();

    }
    public String reverse(String s){
        char[] ls_char=s.toCharArray();
        int left = 0;
        int right= ls_char.length-1;

        while(left<right){
            char temp= ls_char[left];
            ls_char[left]=ls_char[right];
            ls_char[right]=temp;
            left++;
            right--;
        }
        return new String(ls_char);
    }

    public String[] split(String s){
        List<String> res_ls= new ArrayList<>();
        StringBuffer cur_buffer = new StringBuffer();
        for(int i =0 ; i<s.length();i++){
            if (s.charAt(i)!=' ')
                cur_buffer.append(s.substring(i,i+1));
            else{
                if(cur_buffer.length()>0) {
                    res_ls.add(cur_buffer.toString());
                    cur_buffer.delete(0, cur_buffer.length());
                }
            }
        }
        res_ls.add(cur_buffer.toString());
        return res_ls.toArray(new String[0]);
    }
}

~~~

### 题解：

我自己是写了一个能够正确split 的函数，因为我发现直接用java的split函数会出现问题，对于字符串间多个空格的问题，
官方题解还给出了双端队列这种解法，但其实本质都一样，都是要实现翻转和去除空格这两个大部分。

### 困难：
java里面有很多数据类型的转换，比如list转array，

 
## 剑指 Offer 58 - II. 左旋转字符串 难度：简单


### 第一想法：

结合Stringbuffer 和取模的操作我觉得就能完成

~~~
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuffer res_buffer= new StringBuffer();
        res_buffer.append(s.substring(n,s.length()));
        res_buffer.append(s.substring(0,n));
        return res_buffer.toString();
    }
}
~~~

### 题解：

发现不需要取模，利用Stringbuffer就行


### 困难
