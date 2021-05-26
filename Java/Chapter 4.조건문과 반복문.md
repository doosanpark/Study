# 조건문과 반복문

### switch문의 제약조건

1. switch문의 조건식 결과는 정수 또는 문자열이어야 한다.
2. case문의 값은 정수 상수만 가능하며, 중복되지 않아야 한다.

```java
int num, result;
final int ONE = 1;

switch(result){
	case '1';  //OK. 문자 리터럴(정수 상수 49와 동일)
	case ONE;  //OK. 정수 상수
	case "YES; //OK. 문자열 리터럴. JDK 1.7부터 허용
	case num;  //에러. 변수는 불가.
	case 1.0;  //에러. 실수도 불가.
}
```

### for문은 조건식을 생략해도 되지만 while문은 생략할 수 없다.

```java
for(;;){} //항상 참
while(){} //에러
```

### 이름 붙은 반복문

```java
Loop1:  for(var i = 0; i < 5; i++){

    for(var j = 0; j < 100; j++){
        if(j===10){
            break Loop1;
        }
        System.out.println("j: "+j);
    }
    System.out.println("i: "+i);
}
```