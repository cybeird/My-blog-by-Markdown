---
title: 计算字符串的相似度(TOWQs)
date: 2016-10-27 17:01:35
tags:
  - TOWQs
  - Trip Of WaterQuestions
  - 递归
  - 动态规划
categories: cpp
description: 给定任意两个字符串，你能否写出一个算法来计算出它们的相似度呢？
---
>　　许多程序会大量的使用字符串。对于不同的字符串，我们希望能有办法判断其相似程度。我们定义了一套操作方法来把两个不相同的字符串变得相同，具体的操作方法为:
>　　　　1 修改一个字符(如把“a”替换为“b”);
>　　　　2 增加一个字符(如把“abdd”变为“aebdd”)；
>　　　　3 删除一个字符(如把“travelling”变为“traveling”)。
>　　比如，对于“abcdefg”和“abcdef”两个字符来说，我们认为可以通过增加/减少一个“g”的方式来达到目的。上面的两种方案，都仅仅需要一次操作。把这个操作所需要的次数定义为两个字符串的距离，而相似度等于“距离+1”的倒数。也就是说，“abcdefg”和“abcdef”的距离为1，相似度为1/2 = 0.5。
>　　给定任意两个字符串，你能否写出一个算法来计算出它们的相似度呢？
### 问题分析：
　　当我们看到这一道题的第一个思路是通过写大量的函数，暴力枚举各种各样的情况，然后从中寻找出其中使其相似度最小的那一种情况。
　　但当我们仔细读一读题目就会发现一些规律:两个字符串的距离肯定不超过它们的长度之和。
　　实际上我们应该是可以通过递归使其转化成更小的问题来进行求解：
　　　　首先，读入了两个字符串A[1,...,lenA]、B[1,...,lenB].然后无非就是一下六种操作：
　　　　　1 修改A[1]为B[1]，接着再比较A[2,...,lenA]和B[2,...,lenB]的距离
　　　　　2 修改B[1]为A[1]，接着再比较A[2,...,lenA]和B[2,...,lenB]的距离
　　　　　3 删除A[1]，接着再比较A[2,...,lenA]和B[1,...,lenB]的距离
　　　　　4 删除B[1]，接着再比较A[1,...,lenA]和B[2,...,lenB]的距离
　　　　　5 将A[1]插入到字符串B的第一个字符之前，接着再比较A[2,...,lenA]和B[1,...,lenB]的距离
　　　　　6 将B[1]插入到字符串A的第一个字符之前，接着再比较A[1,...,lenA]和B[2,...,lenB]的距离
　　　　然后思路就比较好搞了，但是在这之前我们可以先进行归类就发现可以合并成三种操作：
　　　　　1 修改后比较A[2,...,lenA]和B[1,...,lenB]的距离
　　　　　2 修改后比较A[1,...,lenA]和B[2,...,lenB]的距离
　　　　　3 修改后比较A[2,...,lenA]和B[2,...,lenB]的距离
　　这样就可以很方便的写出递归的程序了。

```cpp
	int check(string A, int beginA, string B, int beginB){
		if(beginA > lenA){
			if(beginB > lenB)
				return 0;
			else return lenB - beginB + 1;
		}
		if(beginB > lenB){
			if(beginA > lenA)
				return 0;
			else return lenA - beginA + 1;
		}
		//如果字符串A已经读完了而且B已经读完了，直接返回0就可以了
		//如果一个读完而另一个没有读完，那么距离增加没有读完的字符串的剩余长度
		if(A[beginA] == B[beginB])
			return check(A, beginA + 1, B, beginB + 1);
		else {
			int c1,c2,c3;
			c1 = check(A, beginA + 1, B, beginB);
			c2 = check(A, beginA,     B, beginB + 1);
			c3 = check(A, beginA + 1, B, beginB + 1);
			return minplus(c1, c2, c3) + 1;				//嗯，minplus是自己写的函数，用了比较三个数的最小值
		}
	}
```
　　然后就写完了我们的递归程序，思路也很明朗，不过有一点需要改进的地方。
<hr/>
　　相信细心的你已经找到了问题所在：没错，这其中有着大量的重复计算！！！
　　Just Like This！
　　![](http://img.my.csdn.net/uploads/201212/09/1355029218_9181.jpg)
### 问题优化
　　但是如何解决呢？记忆化搜索？没错！
　　我们所需要的仅仅只是新创建一个二维数组，然后对于每一次check，将其结果保存在数组中，然后在下次check的时候，先检查一下是否已经计算过，然后再返回值，这就完成了记忆化搜索，节省了大量的重复计算。

```cpp
int check(string A, int beginA, string B, int beginB, int **temp) {  
    int a, b, c;  
    if(beginA > pAEnd) {  
        if(beginB > pBEnd) {  
            return 0;  
        } else {  
            return pBEnd - beginB + 1;  
        }  
    }  
    if(beginB > pBEnd) {  
        if(beginA > pAEnd) {  
            return 0;  
        } else {  
            return pAEnd - beginA + 1;  
        }  
    }  
    //和刚才思路一样，到了这种地步并不需要去记忆化了
    if(strA[beginA] == strB[beginB]) {  
        if(temp[beginA + 1][beginB + 1] != 0) {  
            a = temp[beginA + 1][beginB + 1];  
        } else {  
            a = check(strA, beginA + 1, strB, beginB + 1, temp);  
        }  
        return a;  
    } else {  
        if(temp[beginA + 1][beginB + 1] != 0) {  
            a = temp[beginA + 1][beginB + 1];  
        } else {  
            a = check(strA, beginA + 1, strB, beginB + 1, temp);  
            temp[beginA + 1][beginB + 1] = a;  
        }  
  
        if(temp[beginA + 1][beginB] != 0) {  
            b = temp[beginA + 1][beginB];  
        } else {  
            b = check(strA, beginA + 1, strB, beginB, temp);  
            temp[beginA + 1][beginB] = b;  
        }  
  
        if(temp[beginA][beginB + 1] != 0) {  
            c = temp[beginA][beginB + 1];  
        } else {  
            c = check(strA, beginA, strB, beginB + 1, temp);  
            temp[beginA][beginB + 1] = c;  
        }  
        //若数组中有值，则直接调用，若没有，则check一次，然后将数组赋值(记忆化)
        return minplus(a, b, c) + 1;  
    }  
}  
```

　　当然，更加有趣(方便)的做法便是用动态规划了。
　　设Ai为字符串A的前i个字符（即为a[1],a[2],a[3]...a[i]）
　　设Bj为字符串B的前j个字符（即为b[1],b[2],b[3]...b[j]）
　　设 L(i,j)为使两个字符串和Ai和Bj相等的最小操作次数。
　　1. 当ai==bj时 显然 L(i,j) = L(i-1,j-1)
　　2. 当ai!=bj时 
　　　　2.1. 若将它们修改为相等，则对两个字符串至少还要操作L(i-1,j-1)次
　　　　2.2. 若删除ai或在bj后添加ai，则对两个字符串至少还要操作L(i-1,j)次
　　　　2.3. 若删除bj或在ai后添加bj，则对两个字符串至少还要操作L(i,j-1)次
　　此时L(i,j) = min( L(i-1,j-1), L(i-1,j), L(i,j-1) ) + 1 
　　显然，L(i,0)=i，L(0,j)=j, 再利用上述的递推公式，可以直接计算出L(i,j)值。L(i,0)代表Ai和B0，如果想把一个字符串和一个空字符串变的相同，那么之后删除非空串中的字符或者把空串变成和非空串相同的字符串，那么所需要操作的次数为i次。

```cpp
int check(string A, int lenA, string B, int lenB) {
    for(int i = 1; i <= lenA; i++) {
        temp[i][0] = i;
    }
    for(int i = 1; i <= lenB; i++) {  
        temp[0][i] = i;  
    }
    temp[0][0] = 0;
    for(i = 1; i <= len_a; i++) {
        for(j = 1; j <= len_b; j++) {
            if(strA[i - 1] == strB[j - 1]) {
                temp[i][j] = temp[i - 1][j - 1];
            } else {
                temp[i][j] = min(temp[i - 1][j], temp[i][j - 1], temp[i - 1][j - 1]) + 1;
            }
        }
    }
    return temp[len_a][len_b];  
}  
```
　　嗯，好了，然后我就[无法自拔](http://cybeird.tk/2048/)了(自从加入了“鬼畜”的音乐之后。。。)