# 나머지 연산자
~~~
int x = 10;
int y = 8;
System.out.println("&d를 %d로 나누면", x, y);
System.out.println("몫: %d", x/y);
System.out.println("나머지: %d", x%y);
~~~
* 나누는 수로 0을 사용할 수 없다.
* 피연산자는 정수만 허용한다.

# 논리 / 비트 연산자
### 논리 연산자
~~~
|| (OR 걸합) - 피연산자 중 어느 한 쪽만 true여도 true를 결과로 얻는다.
&& (AND 결합) - 피연산자 양쪽 모두 true이어야 true를 결과로 얻는다.
~~~
### 비트 연산자
~~~
| (OR 연산자) - 피연산자 중 한 쪽의 값이 1이면, 1을 결과로 얻는다. 그 외에는 0을 얻는다.
& (AND 연산자) - 피연산자 양 쪽이 모두 1이어야만 1을 결과로 얻는다. 그 외에는 0을 얻는다.
^ (XOR dustkswk) 피연산자의 값이 서로 달르 때만 1을 결과로 얻는다. 같을 때는 0을 얻는다.
~~~
* 비트 연산자는 조건물을 모두 실행한다.
* 반면 논리 연산자는
    * ||(OR)의 경우 선조건이  
