# 2438번: 별 찍기 - 1

첫째 줄에는 별 1개, 둘째 줄에는 별 2개, N번째 줄에는 별 N개를 찍는 문제

www.acmicpc.net




----------




-   **문제**





![](https://blog.kakaocdn.net/dn/ds9l4T/btqB8bc0BMx/1lt5HMkx2c25EDmaZaX8XK/img.png)




아마 대부분 언어를 처음 배울 때 반복문에서 가장 많이 하는 실습이 별찍기 일 것이다.

그정도로 반복문을 어떻게 짜느냐가 중요하다고 할 수 있을 것이다.




----------




-   **2가지 입력방법을 이용하여 풀이한다.**

Scanner 로 입력받아 연산하는 방법과 BufferedReader 로 입력받아 연산하는 방법, 두 가지 방법을 통해 풀이해보고자 한다.

또한 BufferedReader 에서 출력방법을 바꿔보며 어느 방법이 시간을 더 단축 시킬 수 있는지 한 번 보고자 한다.

----------




-   **알고리즘**


먼저 N 이라는 숫자가 주어진다.

1 행부터 N 행까지 출력을 하기 위한 가장 큰 틀의 반복문을 먼저 구상한다.  


```java
for ( int i = 1 ; i <= N ; i++ )
```

그리고 출력을 보면 1 행에 1개 출력, 2행에 2개 출력, ... 즉, n 번째 행에는 n개가 출력되어야 한다.

그러면 i 가 행을 의미하니 i 의 값만큼 반복해서 출력해주면 될 것 같다.

고로, 위의 for문 안에 for문 ( 이중for문 ) 을 작성해본다면 아래와 같을 것이다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= i ; j++ ) {}
}
```

즉, 내부 for문의 j 는 i 의 값만큼 반복해주면 된다.

그럼 좀 더 구체화 해보자.

일단 한 행(i)당 j 의 반복 횟수만큼 출력을 해주어야 할 것이다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= i ; j++ ) {
		print("*");
	}
}
```

또한, 한 행의 출력이 모두 끝나면 개행(줄바꿈)을 해주어야되지 않겠는가?

그러므로 내부 for문이 종료 될 때마다 개행을 해주면 되겠다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= i ; j++ ) {
		print("*");
	}
	print('\n'); // 줄바꿈
}
```

이런식으로 구조를 짜면 된다.

----------




-   **풀이**



**- 방법 1  

**

```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);

		int N = in.nextInt();
		in.close();

		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

가장 기본적인 방법이다.

그리고 무의식 중에 내부 for문 안에 System.out.println("*") 을 하다간 큰일난다...

----------

**- 방법 2**




BufferedReader 을 쓰는 방식이다.

**그리고 반드시 자료형 타입을 잘 보아야 한다.**

br.readLine() 은 문자열로 데이터를 읽으니 반드시 꺼내서 쓸 때 int 형으로 쓰고자 한다면 Integer.parseInt()로 String 을 int 형으로 변환시켜준다.  


```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		br.close();

		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

위 코드를 실행하면 물론 Scanner 보다 BufferedReader 가 속도가 빠르니 시간이 단축되지만 출력 부분에서 System.out.print() 를 너무 자주 호출해주기 때문에 이 부분에서 좀 더 시간을 절약해볼 방법을 알아보자.

----------

다음 방법은 StringBuilder 을 사용하는 방법이다.

모든 문자열을 하나의 객체에 연결해준다음 출력은 마지막에 한 번만 해주니 시간을 아낄 수 있는 방법 중 하나다.  


```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		br.close();

		StringBuilder sb = new StringBuilder();

		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= i; j++) {
				sb.append('*');
			}
			sb.append('\n');
		}
		System.out.print(sb);
	}
}
```

----------

또 다른 방법은 BufferedWriter 을 사용하는 방법이다. 이 방법 또한 출력 할 문자들이 많아지면 많아질수록 다른 출력 방법들에 비해 매우 우수한 성능을 보여준다.  


```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.BufferedWriter;
import java.io.OutputStreamWriter;
import java.io.IOException;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
		int N = Integer.parseInt(br.readLine());
		br.close();

		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= i; j++) {
				bw.write('*');
			}
			bw.newLine();
		}
		bw.flush();
		bw.close();
	}
}
```

----------




-   **성능 차이**

![](https://blog.kakaocdn.net/dn/Upqzp/btqB4ZS8eqn/ANtlzLvAK4OKPIHx7yinGK/img.png)




위에서 부터 순서대로

**채점 번호 : 17800240 - BufferedReader + BufferedWriter**

**채점 번호 : 17800213 - BufferedReader + StringBuiler**

**채점 번호 : 17800175 - BufferedReader + System.out.print**

**채점 번호 : 17800154 - Scanner + System.out.print**

시간을 보면 BufferedReader 와 Scanner 의 성능차이 및 출력 방법에 따른 성능 차이 또한 볼 수 있다.

>Written by st-lab
