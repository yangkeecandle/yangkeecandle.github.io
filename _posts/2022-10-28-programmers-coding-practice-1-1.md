# N보다 작은 소수의 개수

소수란 자기 자신과 1만을 약수로 가지는 자연수를 말한다. 예를 들어, 2, 3, 5는 소수이지만, 1, 4, 6은 소수가 아니다.

수학 영재 민준이는  `n`보다 작은 소수의 개수를 세 주는 프로그램을 개발하고자 한다.

`n`보다 작은 소수의 개수를 출력하는 프로그램을 작성하시오.

## 입력설명

-   `0 < n <= 100`

## 출력설명

`n`보다 작은 모든 소수의 개수를 정수로 반환

## 매개변수 형식

`n = 15`

## 반환값 형식

`6`

## 예시 입출력 설명

`15`보다 작은 소수는 다음과 같다.

-   `2, 3, 5, 7, 11, 13`  => 총  `6`개

## 문제해결

```java
import java.util.Arrays;  

public class problem1 {  

    public static int solution(int n) {  
        int[] intArray = new int[n];  

	 // initialize array elements to 1  
	 // 1 is true // 0 is false  
		 for(int i = 2; i < n; i++){  
            intArray[i] = 1;  
		 }  
  ```
  intArray 배열을 1로 Initialize 해준다.
  n보다 작은 소수일경우 intArray[i]는 1, 소수가 아닐 경우 0
  ```java

        for(int i = 2; i <= (int)Math.sqrt(n); i++){  
            if(intArray[i] == 0)  
                continue;  
			int num = i * 2;  
			while(num < n){  
                intArray[num] = 0;  
				num += i;  
			}  
        }  
  ```
0과 1은 소수가 아니기 때문에 Starting Index는 2에서 시작하고,
sqrt(n)보다 큰 수의 배수는 찾을 필요가 없기 때문에 반복문은 sqrt(n) 까지만 실행한다.

전체 배열을 1로 Initialize 해뒀기 때문에 intArray[i] 가 0일 경우 업데이트된 인덱스이니 건너뛰어준다.



```java
        return Arrays.stream(intArray).sum();  
  }  

    public static void main(String[] args){  
        System.out.println(solution(15));  
  }  
}
```
Arrays.stream().sum() Method를 통해 배열에 있는 소수의 개수를 더한다.
## 전체코드
```java
import java.util.Arrays;  

public class problem1 {  

    public static int solution(int n) {  
        int[] intArray = new int[n];  

		 // initialize array elements to 1  
		 // 1 is true // 0 is false  
		 for(int i = 2; i < n; i++){  
            intArray[i] = 1;  
		 }  


        for(int i = 2; i <= (int)Math.sqrt(n); i++){  
            if(intArray[i] == 0)  
                continue;  
			int num = i * 2;  
			while(num < n){  
                intArray[num] = 0;  
				num += i;  
			}  
        }  

        return Arrays.stream(intArray).sum();  
  }  

    public static void main(String[] args){  
        System.out.println(solution(15));  
  }  
}
```

> Written by Leo Yang
