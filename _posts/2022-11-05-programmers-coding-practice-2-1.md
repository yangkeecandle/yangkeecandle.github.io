# 비어있는 숫자

촘촘이는 무엇이든 연속으로 가득찬 것을 좋아한다. 이번에 촘촘이가 빠진 취미는 빠짐없이 연속된 숫자를 모으는 것이다.

촘촘이는 연속된 숫자가 무작위 순서로 배치된 배열  `numbers`를 입력받았다.

이 배열에는 최소한 하나 이상 비어있는 숫자가 있으며, 배열에서 가장 작은 숫자는 알려져 있지 않다.

배열에서 비어있는 숫자 중, 가장 작은 숫자를 출력하는 프로그램을 작성하시오.

## 입력설명

-   `0 <= numbers[i] <= 100000`
-   `2 <= numbers.length <= 100000`

## 출력설명

`6`

## 매개변수 형식

`numbers = {9, 4, 2, 3, 7, 5}`

## 반환값 형식

`6`

## 예시 입출력 설명

배열에서 가장 작은 숫자는  `2`이고,  `3`,  `4`,  `5`가 배열에 있고  `6`은 없으므로, 가장 작은 비어있는 숫자는  `6`이다.

## 코드

```java
public static int solution2(int[] numbers) {  
    Arrays.sort(numbers);  
	for(int i = 0; i < numbers.length - 1; i++){  
        if (numbers[i] + 1 != numbers[i + 1]){  
            return numbers[i] + 1;  
  }  
    }  
    return -1;  
}  

public static void main(String[] args){  
    int[] n = {9,4,2,3,7,5};  
  System.out.println(solution(n));  
}
```
> Written by Leo Yang
