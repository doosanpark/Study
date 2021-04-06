# 유효범위 Scope

scope는 변수의 수명을 의미함

```jsx
var vscope = 'global';  //전역변수
function fscope(){
	alert(vscope);  //global 출력
}
fscope();
```

함수 내에서 함수 바깥의 변수에 접근 가능

```jsx
var vscope = 'global';  //지역변수
function fscope(){
	vscope = 'local';
	alert(vscope);  //local 출력
}
fscope();
```

자기 자신에서 가까운 변수(함수 내부)를 먼저 접근함

```jsx
var vscope = 'global';  //지역변수
function fscope(){
	var vscope = 'local';
  var lv = 'local variables';
	alert(vscope);  //local 출력
}
alert(lv)// 호출 불가
fscope();
```

함수 외부에서 함수 내부의 새로 생성된 변수에 접근하지 못한다.

# 전역변수를 사용하는 Style

타인과 사용하는 전역변수와 구분하기 위해 나만의 전역변수명을 만들어서 사용 가능

```jsx
var MYAPP = {}   // 내가 사용하는 전역변수명을 지정
MYAPP.calculator = {
	'left': null,
	'right': null
}
MYAPP.coordinate = {
	'left': null,
	'right': null
}

MYAPP.calculator.left = 10;
MYAPP.calculator.right = 20;

function sum(){
	return MYAPP.calculator.left + MYAPP.calculator.right;
}
document.write(sum());

```

# 유효범위의 대상(함수)

자바스크립트는 함수에 대한 유효범위만을 제공한다. 그렇기에 for문 안에서 변수를 선언하더라도 for문 밖에서 이를 인식할 수 있다.

```jsx
for(var i = 0; i < 1; i++){
	var name = "coding everybody";
}
alert(name); //coding everybody 출력
```

# 정적 유효범위(Static Scope), 
렉시컬 유효범위(Lexical Scope)

자바스크립트는 함수가 선언된 지점에서의 유효범위를 갖는다. 이런 유효범위의 방식을 정적 또는 렉시컬 유효범위라고 한다.

```jsx
var i = 5;  //전역변수

function a(){
	var i = 10; //지역변수
	b();
}

function b(){
	document.write(i); //i는 누구?
}

a();  //5
```

함수가 사용될 때가 아닌 선언될 때를 기점으로 판단하기 때문에 접근할 수 있는 변수는 전역변수 var i = 5;가 된다.

b()의 경우 어디에든 사용될 수 있는데 그때마다 사용 시점의 변수를 사용하게 되면 동적이게 되지만 사용처가 달라도 전역변수만을 사용하기 때문에 정적 유효범위라고 부른다.