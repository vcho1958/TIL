# [TIL-220919] 코딩 인터뷰 완전 분석-VI big-O 예제

## 예제 3

```java
void foo(int[] arr){

	for(int j = 0; j < arr.length; i++)
		for(int i = j+1; i < arr.length; i++)
			System.out.println(arr[j]+ ", "+arr[i]);

}
```

-   답
    
    O(N^2)
    
-   이유
    
    총 반복횟수는 N-1 N-2 … +1 이므로 등차수열의 합공식을 대입하면
    
    N(N-1)/2 이다. 최고차항은 N^2이므로 O(N^2)이다.
    
-   이유 2
    
    기존 N^2의 경우와 차이점을 관찰한다.
    
    3번의 경우 j>i인 경우만 있다. 따라서 대략 절반인 N/2개라고 추론할 수 있고 N번 반복되므로 O(N^2)이다.
    
-   이유 3
    
    바깥루프 N
    
    만약 N = 10 이라면 안쪽 루프는 1,2,3,4,5,6,7,8,9,10번 반복할 것이다. 이 때 평균적으로는 대략 5번 이고
    
    N = N 이라면 안쪽루프는 평균 N/2번 반복할 것이므로 마찬가지로 O(N^2)이다.
    

## 예제 4

```java
void foo(int[] arr, int[] brr){

	for(int j = 0; j < arr.length; i++)
		for(int i = j+1; i < brr.length; i++)
			System.out.println(arr[j]+ ", "+brr[i]);

}
```

-   답
    
    O(ab)
    
-   이유
    
    arr의 원소 개수 a brr의 원소 개수 b의 곱만큼 반복되기 때문이다.
    

## 예제 8

```java
요소가 a개인 String[] 배열이 주어졌을 때
각 문자열의 글자를 사전순 정렬 후
각 문자열 역시 사전순으로 정렬할 때 걸리는 시간 복잡도는?
```

-   답
    
    a*s(loga+logs)
    
-   이유
    
    각 문자열을 정렬하는 시간복잡도는 가장 긴 문자열의 길이 s를 기준으로
    
    slogs이며 a번 반복되므로 aslogs다.
    
    문자열을 사전순으로 나열하는 시간 복잡도는 aloga다.
    
    이 때 문자열을 사전순으로 비교할 때 각 항마다 s만큼이 더 걸리므로 asloga다.
    
    따라서 as(loga+logs)가 답이다.
    

## 예제 9

```java
int sum(Node node){
	if(node == null)return 0;
	return sum(node.left) + node.value + sum(node.right);
}

```

-   답
    
    O(N)
    
-   풀이
    
    직관적으로 봤을 때 모든 노드를 순회해야하므로 O(N)이다.
    
    -   재귀분석
        -   분기 2 깊이(최대 호출스택) logN ⇒ 2^(logN) ⇒N

## 예제 11

```java
int fact(int n){
	if(n < 0)return -1;
	if(n == 0)return 1;
	return n * fact(n-1);
}
```

-   답
    
    O(N)
    
-   풀이
    
    분기 = 1, 깊이 = n 분기가 1일 때는 N이 된다.
    

## 예제 12

```java
void perm(String str){ perm(str, "");}
void perm(String str, String prefix){
	if(str.length()==0){
		System.out.println(prefix);
	}else{
		for(int i = 0; i < str.length(); i++){
			String rem = str.substring(0,i) + str.substring(i+1);
			perm(rem, prefix + str,charAt(i));
		}
	}
}
```

-   답
    
    s^2*s!
    
-   풀이
    
    for안에 만큼 걸리는 연산이 있으므로 s^2 최대 깊이는 s 분기 for 만큼이므로 s
    
    s^2*s^s 이므로 s^s인 줄 알았으나
    
    분기의 수는 깊이가 깊어질수록 -1된다. 따라서 s*(s-1)…_1이므로 s^2_s!이다
    

## 예제 14

```java
void pr(int n){
	for(int i = 0; i < n; i++)System.out.println(fib(i));
}

int fib(int n){
	if(n<=0)return 0;
	if(n == 1) return 1;
	return fib(n-1) + fib(n-2);
}
```

-   답
    
    2^n
    
-   풀이
    
    n루프안에서 2^n을 호출 하므로 n*2^n일것 같지만
    
    fib의 n은 처음 주는 n이 아니고 1씩 증가하는 n이다.
    
    따라서 2+2^2+2^3…+2^n이므로 총 시간복잡도는 2^n이다.
    

```java
int sqrt(int n){
	return sh(n, 1, n);
}

int sh(int n, int min, int max){
	if(max < min)return -1;
	int guess = (max+min)/2;
	if(guess*guess == n)return guess;
	if(guess*guess < n) return sh(n, guess+1, max);
	return sh(n, min, guess-1);
}
```

-   답