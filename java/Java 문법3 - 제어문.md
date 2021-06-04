## 제어문

### If 문

기본문법은 다음과 같다. 

```java
if(조건식) {
    수행문;
}

if(조건식1) {
    수행문1;
} else if(조건식2) {
    수행문2;
} else {
    수행문3;
}
```

- statement가 하나일 때 중괄호(`{}`)를 쓰지 않아도 되지만, 이후 추가될 경우를 대비해 항상 쓰는 것을 추천한다.



### switch-case 문

조건이 정수, 문자열 값으로 그 값에 따라 수행 결과가 달라지는 경우 사용할 수 있다.

예를 들어,

```java
switch(rank) {
    case 1: medalColor = 'G';
        break;
    case 2: medalColor = 'S';
        break;
    case 3: medalColor = 'B';
        break;
    default : medalColor = 'A'; // 어떤 케이스에도 해당하지 않는 경우
}
```

이렇게 사용할 수 있다.



### While, do-while 문

```java
while(조건식) {
    수행문;
}

// 예시 - 1부터 10까지의 합 구하기
int num = 1;
int sum = 0;

while( num <= 10 ) {
    sum += num;
    num++;
}

System.out.println(sum); // 55
System.out.println(num); // 11

// 무한루프
while(true) {
    
}
```

먼저 수행해야하는 수행문이 있는 경우 do-while문을 쓸 수 있다. do-while 문은 별로 사용할 경우가 없기는 하지만 알아만두자.

```java
int num = 1;
int sum = 0;

do {
    sum += num;
    num++;
} while(num <= 10);

// 입력 받는 정수를 모두 더해주는데, 입력 정수가 0이면 반복문 빠져 나온다.
Scanner scanner = new Scanner(System.in);
int input;
do {
    input = scanner.nextInt(); 
    sum += input;
}while(input != 0);
```



### for문

일반적인 for 문

```java
for (int num=1; num <= 5; num++) {
    System.out.println(num);
}

// 무한루프
for(;;) {
    
}
```

- `;` 로 구분된 세 부분(초기치, 조건문, 증가치) 생략해도 되는 경우 생략할 수 있다.

다음과 같이 `향상된 for문`을 사용하면 배열의 원소를 인덱스 없이 탐색할 수 있으며 가독성을 높일 수 있다. 

```java
int[] arr = {1, 2, 3, 4, 5};

for(int num:arr) {
    System.out.println(num);
}

// 결과
1
2
3
4
```

- 단, 오직 배열의 값을 가져다 사용할 수만 있고 수정할 수는 없다.



### break, continue

break

- **감싸고 있는 블록의 제어를 빠져나오는 기능**이다.
- 반복문, 조건문, switch-case 등과 같이 쓰이며 현재 수행하고 있던 블록에서 수행을 중지하고 외부로 제어가 이동한다.

continue

- 반복의 수행 중 조건문과 조건이 맞는 경우 **이후 블록 내부의 다른 수행문을 수행하지 않는다**. 

```java
//continue를 사용해서 100이하의 자연수 중 3의 배수만 출력해보자.

int num;
for(num=1; num <= 100; num++) {
    if(num % 3 != 0) continue;
    System.out.println(num);
}
```

```java
// 구구단을 출력할 때 짝수 단만 출력하면서 단보다 곱하는 수가 작거나 같을 때까지만 출력해보자(break, continue 둘 다 사용).

for(int dan=1; dan<=9; dan++) {
    if(dan % 2 != 0) continue;
    for(int count=1; count<=9; count++) {
        if(dan < count) break;
        System.out.println(dan + '*' + count + '=' + dan*count );
    }
}
```

