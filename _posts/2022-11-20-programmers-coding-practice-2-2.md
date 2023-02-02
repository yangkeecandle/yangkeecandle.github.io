---   
layout: post  
author: Leo Yang  
title: [ 프로그래머스 ] 배열 덧셈기

---  

# 배열 덧셈기
## 문제

컴퓨터는 정수를 표현할 때, 자료형에 따라 표현 가능한 숫자의 범위가 정해져있다. 기산이는 이러한 한계를 해결하고자, 숫자를 배열로 표현하기로 하였다.

기산이가 선택한 방법은 아래와 같다.

-   양수의 경우, 숫자의 각 자리를 큰 자릿수부터 순서대로 배열에 저장한다.
-   음수는 사용하지 않는다.
-   0의 경우, 빈 배열로 표현한다.

위 방법을 이용하여 배열로 표현된 숫자의 예는 아래와 같다.

-   `1523`  ->  `{1, 5, 2, 3}`
-   `0`  ->  `{}`

기산이는 이 표현법을 이용하는 덧셈기를 구현하고자 한다.

첫 번째 인자인  `a`와 두 번째 인자인  `b`를 입력받아, 배열 표현법으로 결과를 출력하시오.

## 입력설명

-   `0 <= a.length <= 1000`
-   `0 <= b.length <= 1000`

## 출력설명

두 인자의 값을 더한 결과를 배열로 출력

## 매개변수 형식

`a = {5, 2, 1, 4, 6}`  
`b = {6, 1, 0, 4, 4}`

## 반환값 형식

`{1, 1, 3, 1, 9, 0}`

## 코드
```java
import java.util.Stack;  
  
public class Problem2 {  
    public static int[] solution(int[] a, int[] b) {  
        int[] answer = {};  
  Stack<Integer> stack = new Stack<>();  
 int maxLen = Math.max(a.length, b.length);  
 int offsetA = maxLen - a.length;  
 int offsetB = maxLen - b.length;  
  
 if(a.length == 0){  
            return b;  
  }  
        if(b.length == 0){  
            return a;  
  }  
  
        int overflow = 0;  
 for(int i = maxLen - 1; i >= 0; i--){  
            int aVal = (i - offsetA < 0) ? 0 : a[i - offsetA];  
 int bVal = (i - offsetB < 0) ? 0 : b[i - offsetB];  
 int cVal = aVal + bVal + overflow;  
  
 if(cVal >= 10) {  
                overflow = 1;  
  stack.push(cVal - 10);  
  } else {  
                overflow = 0;  
  stack.push(cVal);  
  }  
        }  
  
        int resLen = maxLen;  
 if(overflow == 1){  
            resLen++;  
  stack.push(1);  
  }  
  
        int[] result = new int[resLen];  
 for(int i = 0; i < resLen; i++){  
            result[i] = stack.pop();  
  }  
        return result;  
  
  
  }  
  
  
    public static void main(String[] args){  
        int[] a = {5,2,1,4,6};  
 int[] b = {6,1,0,4,4};  
  
  System.out.println(solution(a,b));  
  }  
  
}
```
> Written by Leo Yang
