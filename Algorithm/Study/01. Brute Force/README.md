# 01. 나열된 수에서 최솟값과 최댓값 구하기

## 문제 정의

- 여러 개의 수가 배열에 있을 때 그 중 가장 큰 값과 가장 작은 값을 찾는다.
- 배열의 몇 번째에 있는지 순서를 찾는다.
- 반복문을 한번만 사용하여 문제를 해결한다.
- 수의 예 : [10, 55, 23, 2, 79, 101, 16, 82, 30, 45]

## 나의 풀이 #1
~~~java
public class Main {
    public static void main(String[] args){

        int[] randomNumList = {13, 25, 13, 22, 56, 3, 72, 34, 47, 45, 102};

        int minimumNum = randomNumList[0];
        int maximumNum = randomNumList[0];

        for (int i = 0; i < randomNumList.length; i++){
            if (minimumNum < randomNumList[i]){
                continue;
            }
            else{
                minimumNum = randomNumList[i];
            }
        }

        for (int i = 0; i < randomNumList.length; i++){
            if (maximumNum > randomNumList[i]){
                continue;
            }
            else{
                maximumNum = randomNumList[i];
            }
        }
        System.out.println(minimumNum);
        System.out.println(maximumNum);

    }
}
~~~

## 문제점
* for문 한 번만 돌아도 된다
* 불필요한 else문이 있다.

## 나의 풀이 #2
~~~java
public class Main {
    public static void main(String[] args){

        int[] randomNumList = {13, 25, 13, 22, 56, 3, 72, 34, 47, 45, 102};

        int minimumNum, maximumNum = randomNumList[0];
        
        for (int temp : randomNumList){
            if (minimumNum > temp){
                minimumNum = temp;
            }
            if (maximumNum < temp){
                maximumNum = temp;       
            }
        }
        
        System.out.println(minimumNum);
        System.out.println(maximumNum);

    }
}
~~~

## 문제점
- 문제를 제대로 읽지 않았다. 지금 요구하는 것은 값과 위치이기 때문에 향상된 for문을 쓰는 것은 옳지 않다.
- 애초에 position 값을 선언하지도 않았다는 게 아주 큰 문제이다
- 0번째 인덱스는 탐색할 필요가 없다. 0번쨰와 0번째를 비교하는 것은 말이 안 된다.

## 마지막 풀이
~~~java
public class Main {
    public static void main(String[] args){

        int[] randomNumList = {13, 25, 13, 22, 56, 3, 72, 34, 47, 45, 102};

        int minimumNum = randomNumList[0];
        int maximumNum = randomNumList[0];
        int minPos = 0;
        int maxPos = 0;

        for (int temp = 0; temp < randomNumList.length; temp++){
            if (minimumNum > randomNumList[temp]){
                minimumNum = randomNumList[temp];
                minPos = temp;
            }
            if (maximumNum < randomNumList[temp]){
                maximumNum = randomNumList[temp];
                maxPos = temp;
            }
        }

        System.out.println(minimumNum + " " + minPos);
        System.out.println((maximumNum) + " " + maxPos);

    }
}
~~~

## 정답

```java
public class MinMaxProblem {

	public static void main(String[] args) {

		int[] numbers = {10, 55, 23, 2, 79, 101, 16, 82, 30, 45};
		
		int min = numbers[0];
		int max = numbers[0];
		int minPos = 0;
		int maxPos = 0;
		
		for(int i=1; i<numbers.length; i++ ) {
			
			if(min > numbers[i]) {
				min = numbers[i];
				minPos = i+1;
			}
			
			if(max < numbers[i]) {
				max = numbers[i];
				maxPos = i+1;
			}
		}
		
		System.out.println("가장 큰 값은 " + max + "이고, 위치는 " + maxPos + "번째 입니다.");
		System.out.println("가장 작은 값은 " + min + "이고, 위치는 " + minPos + "번째 입니다.");
	}

}
```