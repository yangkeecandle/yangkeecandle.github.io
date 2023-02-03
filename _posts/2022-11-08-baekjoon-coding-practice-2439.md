# 2439번: 별 찍기 - 2

첫째 줄에는 별 1개, 둘째 줄에는 별 2개, N번째 줄에는 별 N개를 찍는 문제 하지만, 오른쪽을 기준으로 정렬한 별(예제 참고)을 출력하시오.
[  
https://www.acmicpc.net/problem/2439](https://www.acmicpc.net/problem/2439)

[](https://www.acmicpc.net/problem/2439)


----------




-   **문제  


    **

![](https://blog.kakaocdn.net/dn/0HfFc/btqB5FfAzgq/OWdQ8RvO43kPVKwkTMmbm1/img.png)




이전 포스팅과 문제가 유사하다.

아마 반복문 연습 때 대표적인 별찍기 중 하나로 한 번씩은 해봤으리라 본다.

(그래도 포스팅은 계속될 것이니..)

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

그리고 출력을 보면 전 문제(별 찍기 - 1)와는 다르게 공백이 1 행에 4개 출력, 2행에 3개 출력, ...

즉, n 번째 행에는 N-n개의 공백이 출력되고, 별은 n 번째 행에 n 개가 출력되어야 한다.

그러면 i 가 행을 의미하니 N-i 의 값 만큼 공백을 출력해주어야 겠다.

고로, 위의 for문 안에 for문 ( 이중for문 ) 을 작성해본다면 아래와 같을 것이다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= N-i ; j++ ) {
		print(" ");
	}
}
```

즉, 공백 출력의 경우 내부 for문의 j 는 N-i 의 값만큼 반복해주면 된다.

그리고는 각 행에 별도 출력해주어야한다. 별의 개수는 i 의 값만큼 출력하니 for문을 외부 for문 아래에 하나 더 써주어야겠다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= N-i ; j++ ) {
		print(" ");
	}
	for( int k = 1 ; k <= i ; k++ ){
		print("*");
	}
}
```

또한, 한 행의 출력이 모두 끝나면 개행(줄바꿈)을 해주어야되지 않겠는가?

그러므로 내부 for문이 종료 될 때마다 개행을 해주면 되겠다.  


```java
for ( int i = 1 ; i <= N ; i++ ){
	for( int j = 1 ; j <= N-i ; j++ ) {
		print(" ");
	}
	for( int k = 1 ; k <= i ; k++ ){
		print("*");
	}
	print('\n');
}
```

이런식으로 구조를 짜면 된다.




----------




-   **풀이**



**- 방법 1**

```java
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {
		Scanner in = new Scanner(System.in);

		int N = in.nextInt();
		in.close();

		for (int i = 1; i <= N; i++) {
			for (int j = 1; j <= N - i; j++) {
				System.out.print(" ");
			}
			for (int k = 0; k < i; k++) {
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
			for (int j = 1; j <= N - i; j++) {
				System.out.print(" ");
			}
			for (int k = 1; k <= i; k++) {
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
			for (int j = 1; j <= N - i; j++) {
				sb.append(' ');
			}
			for (int k = 1; k <= i; k++) {
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
			for (int j = 1; j <= N - i; j++) {
				bw.write(' ');
			}
			for (int k = 1; k <= i; k++) {
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

![](https://blog.kakaocdn.net/dn/bl0rUR/btqB5gG9p63/yLcglFRaHl40hxTALQ2gNk/img.png)




위에서 부터 순서대로

**채점 번호 : 17801720 - BufferedReader + BufferedWriter**

**채점 번호 : 17801709 - BufferedReader + StringBuiler**

**채점 번호 : 17801704 - BufferedReader + System.out.print**

**채점 번호 : 17801695 - Scanner + System.out.print**

시간을 보면 BufferedReader 와 Scanner 의 성능차이 및 출력 방법에 따른 성능 차이 또한 볼 수 있다.

>Written by st-lab
