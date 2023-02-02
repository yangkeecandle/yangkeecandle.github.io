```
---   
layout: post  
author: Leo Yang  
title: [ 프로그래머스 ] 배열에서 네명의 당첨자를 뽑는 경우의 수
description: 민서는 회사에서 종일 일정으로 진행된 체육 행사를 주관하게 되었다. 즐겁게 행사를 마치고 경품 추첨 시간이 되었다.
---  
```
# 배열에서 네명의 당첨자를 뽑는 경우의 수
## 문제

민서는 회사에서 종일 일정으로 진행된 체육 행사를 주관하게 되었다. 즐겁게 행사를 마치고 경품 추첨 시간이 되었다.

경품 추첨은 추첨함에 이름을 적어 넣은 사람들만이 추첨 대상이 된다. 그런데, 민서는 추첨함에 동일 이름을 여러번 넣은 사람들이 있다는 첩보를 전달받았다.

추첨함에 담긴 이름이  `names`  배열에 담겨있다고 할 때, 이 중 총  `4`명의 순위 구분이 없는 당첨자를 뽑는 경우의 수를 구하시오.

단, 동일 이름을 여러번 넣은 경우에는 한 번만 넣은 것으로 하며, 동명이인은 없다고 가정한다.

## 입력설명

-   `4 < names.length <= 100`
-   `0 < names[i] <= 10`

## 출력설명

4명의 당첨자를 뽑는 경우의 수를 정수로 반환

## 매개변수 형식

`names = {"제로", "베이스", "자바", "스쿨", "자바", "베이스", "베이스", "백엔드", "화이팅"}`

## 반환값 형식

`15`

## 예시 입출력 설명

중복이 있는 "베이스"와 "자바"를 골라내면, 총 6명이 참가하였다. 따라서 6명 중 4명을 뽑는 가짓수를 구하면 된다.


## 코드
```java
import java.util.Arrays;  
import java.util.HashSet;  
import java.util.Set;  

public class problem2 {  

    public static int solution(String[] names) {  
        // Use of Set removes all duplicated elements  
		Set<String> set = new HashSet<>(Arrays.asList(names));  
		int n = set.size();  
		int m = 4;  
 ```
 Set을 통해 중복된 element를 제거해준뒤 업데이트된 사이즈를 n에 저장한다
 ```java
  //nC4  
 long numerator = 1;  
 long denominator = 1;  
 for(int i = 0; i < m; i++){  
            numerator *= n - i;  
			   denominator *= (i + 1);  
  }  

        return (int) (numerator / denominator);  

  }  
    public static void main(String[] args){  
        String[] names = {"제로", "베이스", "자바", "스쿨", "자바", "베이스", "백엔드", "화이팅"};  
  System.out.println(solution(names));  
  }  
}
```
nC4 공식을 통해 확률을 계산한다

> Written by Leo Yang
