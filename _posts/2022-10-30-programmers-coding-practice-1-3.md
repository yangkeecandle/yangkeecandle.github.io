---   
layout: post  
author: Leo Yang  
title: [ 프로그래머스 ] 맥주잔 쌓기 문제

---  

# 맥주잔 쌓기
## 문제

아리는 치킨과 맥주를 무척이나 좋아한다. 맥주를 즐기다 보니, 맥주잔을 예쁘게 쌓아 올리는 것에 관심이 생겼다.

맥주잔은  `2x1`의 크기로, 세로의 길이가 가로의 길이보다 두 배 더 길다. 하지만 맥주잔은 옆으로 놓을 경우  `1x2`로 가로로 배치할 수도 있다.

맥주잔의 위아래는 구분을 하지 않는다고 한다. 즉, 맥주잔을 거꾸로 놓은 것과 맥주잔을 똑바로 놓은 것은 동일하게 취급한다고 한다.

이 때, 맥주잔을 높이  `N`까지  `Nx2`의 직사각형 형태로 쌓아 올리는 방법의 수를 구하시오.

## 입력설명

-   `0 < N <= 10`

## 출력설명

방법의 수를 정수로 반환

## 매개변수 형식

`N = 4`

## 반환값 형식

`5`

## 예시 입출력 설명

`N=4`인 경우, 아래와 같이 총 5가지 방법이 있다. 맥주잔의 위아래 구분이 없는 점에 유의.

![img.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/973193d6-9df4-4271-b2a9-13b38ab15c09/img.png)
## 코드
```java
public class problem3 {  
    public static int solution(int N) {  
        // f(n) = f(n - 1) + f(n - 2)  
 // f(1) = 1, f(2) = 2  
		 if(N <= 2){  
	         return N;  
  }  
  
        return solution(N-1) + solution(N-2);  
  
  }  
  
    public static void main(String[] args){  
        System.out.println(solution(10));  
  }  
}
```
피보나치 배열을 통해 재귀적으로 구현
> Written by Leo Yang
