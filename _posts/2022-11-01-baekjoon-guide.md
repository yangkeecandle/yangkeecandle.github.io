```
---   
layout: post  
author: Leo Yang  
title: [ 백준 ] JAVA 문제풀이 주의점
description: main문 자체가 static 함수이므로 거기서 사용하는 전역변수 및 모든 함수또한 static이어야 한다. 뭐 문제 푸는데 지장이 있는건 아니지만 그냥 static 안쓰면 동작이 안되니까 써둔걸로밖에 안보인다.
---  
```
# JAVA 백준 문제풀이 주의점
### 1. 클래스명은 'Main', 패키지는 없어야 한다.

![](https://blog.kakaocdn.net/dn/beaQAq/btrp0aqpC48/dCTdQR1V3thKJ9UftgiT7k/img.png)

이런식으로 package없이 클래스명을 Main으로 두고 작성해야 한다. IDE에서 작성할때 Version Control을 위해 따로 둘 수는 있겠으나, 어쨌든 제출할 때는 저렇게 해야 한다. 또한 제출 시 당연히 import 부분도 같이 넣어줘야 한다.

### 2. Main 이외의 클래스를 추가로 쓰고싶다면 public이 아닌 클래스 혹은 Inner 클래스를 쓰면 된다.

![](https://blog.kakaocdn.net/dn/wTMf8/btrp1achiNI/Q890WHDX9kmp9xQlz3m8CK/img.png)

아무튼 public class는 무조건 Main 이어야하고, public class는 하나여야 한다.

### 3. main 함수에서 바로 작성 시, 당연하게도 모든걸 static으로 작성해야 한다.

main문 자체가 static 함수이므로 거기서 사용하는 전역변수 및 모든 함수또한 static이어야 한다. 뭐 문제 푸는데 지장이 있는건 아니지만 그냥 static 안쓰면 동작이 안되니까 써둔걸로밖에 안보인다.

![](https://blog.kakaocdn.net/dn/3Gei2/btrp0ImUACc/VFH0Nu0Ku3M7cdX5K2XWx0/img.png)

다음과 같이 함수로 한번 래핑하면 된다. 또한 프로그래머스, AtCoder도 비슷하게 코드를 돌려쓸 수 있어서 더 이득이다!

![](https://blog.kakaocdn.net/dn/94bfE/btrpYmxT55i/IThK9UQLyFCmP92GJMUC01/img.png)

### 4. 빠르게 입력 받기! Scanner는 느리다.

일반적으로 Scanner sc = new Scanner(System.in); 을 통해 입력을 받곤한다. 그런데 Scanner는 내부적으로 nextFloat() 이런걸 호출 시 다음 입력을 찾기 위해 정규식을 사용하므로 느리다. 이걸 쓰면 로직은 맞았는데도 시간초과나서 맞왜틀을 외치게될 수 있다. 다음과 같이 BufferedReader를 사용하자.  [여기](https://www.acmicpc.net/blog/view/56)에 백준님이 측정해둔 입력 시간 차이가 있다. 매우 큰 차이를 보임을 알 수 있다.

![](https://blog.kakaocdn.net/dn/cujgLK/btrpZ9yiWHe/YkKXcufAWOzK2QSLmMALV1/img.png)

마찬가지로 String에 대한 split() 보다는 StringTokenizer로 짜르는게 더 빠르다. 따라서 입력받을 때 BufferedReader와 StringTokenizer로 입력받는다면 빠르게 입력받을 수 있다.

예시로 백준에서 자주 볼만한 다음과 같은 형식의 입력값이 있다.

```
3
1 5
3 10 11 12
5 1 2 3 4 5
```

첫 줄은 n으로 이하 몇 줄이 있는지 나타낸다. 매 줄의 첫번째 값은 해당 줄에 몇 개의 값이 있는지를 나타낸다.

이걸 Scanner와 split으로 입력받는다면 다음과 같다.

![](https://blog.kakaocdn.net/dn/bh7Leg/btrp0LcI3Ug/OmNFkAbE3Vq9ZKAM3kanFK/img.png)

다음으로 BufferedReader와 StringTokenizer로 짠 코드는 다음과 같다.

![](https://blog.kakaocdn.net/dn/bh4cJ7/btrp1HVnhrt/DkiLVtx9I9pdbh695oNYQ0/img.png)

추가로 더 빠른 입력방식이 존재하긴 한다. 직접 1byte씩 읽어오는 방식인데, 이건 사실 백준에서는 딱히 쓸 일이 없다. CP(경쟁 프로그래밍) 대회용으로 조금이라도 극한으로 입력시간을 줄이기 위해 사용한다고 보면 될 것 같다. 다만 백준에서도 문제 난이도가 높아질수록 자바론 정말 극한으로 시간, 메모리 관리를 해야할 경우가 있긴 하다. 하지만 그정도 풀 정도면 애초에 이 글을 안 볼 수준일테니 상관이 없다(?). 어쨌든 알아두면 좋긴 하다(단 로직이 느린건데 입력때문에 그렇다는 핑계거리 하나가 사라지므로 주의가 필요하다(?)) [이 링크](https://www.geeksforgeeks.org/fast-io-in-java-in-competitive-programming/)를 참고하면 된다.

### 5. 입력을 위한 클래스는 하나만 쓸 것!

가끔씩 함수마다 Scanner를 새로 생성해서 문제를 풀고 왜 안되냐고 물어보는 경우가 있다. 결론부터 말하자면 아무튼 System.in 이 들어간 클래스는 단 하나만 생성하자. 각자의 IDE에서는 여러개를 선언해도 크게 문제가 없을 것이다. 직접 입력할 것이므로 버퍼가 딱히 의미가 없다. 하지만 백준의 경우 실제로 입력되는건 파일로, Scanner나 BufferedReader나 둘 다 미리 일정량을 읽어들인 후 사용자의 요청(readLine() 등)에 따라 해당 버퍼에서 꺼내온다. 따라서 이걸 여러개 선언해버리면 이미 다른 클래스에서 버퍼에 쌓인 부분때문에 제대로 읽을 수 없게된다.

Scanner와 BufferedReader 짜둔걸 보면 저렇게 BufferSize가 존재한다.

![](https://blog.kakaocdn.net/dn/bgO1jC/btrp1I7OIdF/3NbDQganRMkrF7cwBQca31/img.png)

### 6. 출력도 System.out.println()은 느리다!

[여기](https://www.acmicpc.net/blog/view/57)를 보면 역시 백준님이 측정해둔 속도 비교표가 있다. 말도안되는 속도 차이를 볼 수 있다. (약 30배)

마찬가지로 이것도 모르면 로직은 맞았는데 쓸데없이 출력이 느려서 시간초과가 날 수 있다. 결론적으로 다음과 같이 사용하면 된다. '4'에 있던 코드에서 System.out.println() 부분을 BufferedWriter로 출력한 경우이다. (참고로 BufferedReader나 BufferedWriter 둘 다 깔끔하게 맨 끝에 close를 해주는게 좋긴하다.)

![](https://blog.kakaocdn.net/dn/cHRFtk/btrpVwA3tQb/SBPJiM47j50guoMZUK09D1/img.png)

다만 int를 바로 출력할 수 없고, 그렇다고 ""+data 이런식으로 하기엔 String에 대한 '+' 연산 자체가 느리므로 빠른 출력을 쓰는 의미가 퇴색된다. 그래서 저렇게 String.valueOf로 처리하자니 상당히 지저분하다. 그래서 내 경우엔 속도 차이가 크지 않으면서도 사용하기 쉬운 방식을 쓴다. StringBuilder로 출력할 것들을 전부 모아준 다음 그냥 System.out.println()으로 출력해주는 방식으로 다음과 같다.

![](https://blog.kakaocdn.net/dn/FdzQf/btrpU12qM6Y/7IFT9xYMn68YM0AV4rn5p1/img.png)

### 7. 자바로 풀 수 없는 문제가 간혹 있다.

이건 그냥 인정하고 다른 언어로 푸는 수밖에 없다. 제일 대표적인 예시는  [이 문제(0.1)](https://www.acmicpc.net/problem/11921)  이다. 근데 엄청 간혹있는거라 크게 신경 안써도 된다.

![](https://blog.kakaocdn.net/dn/2RbHt/btrp1Hnzh2F/Hl6EF2ZWFCKTt9ZINqwIkK/img.png)

꾸준히 시도해보긴 했었다 ㅠㅠ. 다른분들도 자바로 100점 맞은 사람은 없다.

>Written by nahwasa
