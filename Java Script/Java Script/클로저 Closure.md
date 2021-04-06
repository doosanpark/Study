# 클로저 Closure

클로저(closure)는 내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것을 가르킨다. 클로저는 자바스크립트를 이용한 고난이도의 테크닉을 구사하는데 필수적인 개념으로 활용된다.

# 내부함수

```jsx
function outter(){ //외부함수
    var title = 'coding everybody'; //외부함수의 지역변수
    function inner(){  //내부함수
        alert(title);  //inner에 변수가 없기 때문에 외부함수에서 찾음
    }
    inner();
}
outter();
```

# 클로저

내부함수는 외부함수의 지역변수에 접근 가능한데 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근할 수 있다.

```jsx
function outter(){
    var title = 'coding everybody';  
    return function(){        
        alert(title);
    }
}
inner = outter(); //이 시점에서 outter 함수는 끝남
inner();  //끝난 outter 함수가 실행됨
```

### private variable

get_title과 set_title에는 언제든지 가능하다.

지역 변수 title은 factory_movie가 소멸한 이후기 때문에 set_title, get_title로만 접근할 수 있기에 **private**하다.

```jsx
function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function(_title){
            title = _title
        }
    }
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
 
alert(ghost.get_title());  //출력: Ghost in the shell
alert(matrix.get_title()); //출력: Matrix
 
ghost.set_title('공각기동대');  //gost의 지역변수 title의 값을 바꿈
 
alert(ghost.get_title());  //출력: 공각기동대
alert(matrix.get_title()); //출력: Matrix
```

위의 예제를 통해서 알 수 있는 것들을 정리해보면 아래와 같다.

1. 클로저는 **객체의 메소드에서도 사용**할 수 있다. 위의 예제는 함수의 리턴값으로 객체를 반환하고 있다. 이 객체는 메소드 get_title과 set_title을 가지고 있다. 이 메소드들은 외부함수인 factory_movie의 인자값으로 전달된 지역변수 title을 사용하고 있다.

2. 동일한 외부함수 안에서 만들어진 내부함수나 메소드는 외부함수의 **지역변수를 공유**한다. 17행에서 실행된 set_title은 외부함수 factory_movie의 지역변수 title의 값을 '공각기동대'로 변경했다. 19행에서 ghost.get_title();의 값이 '공각기동대'인 것은 set_title와 get_title 함수가 title의 값을 공유하고 있다는 의미다.

3. 그런데 똑같은 외부함수 factory_movie를 공유하고 있는 ghost와 matrix의 get_title의 결과는 서로 각각 다르다. 그것은 **외부함수가 실행될 때마다 새로운 지역변수를 포함하는 클로저가 생성**되기 때문에 ghost와 matrix는 **서로 완전히 독립된 객체**가 된다.

4. factory_movie의 지역변수 **title은 2행에서 정의된 객체의 메소드에서만 접근 할 수 있는 값**이다. 이 말은 title의 값을 읽고 수정 할 수 있는 것은 factory_movie 메소드를 통해서 만들어진 객체 뿐이라는 의미다. JavaScript는 기본적으로 Private한 속성을 지원하지 않는데, 클로저의 이러한 특성을 이용해서 **Private한 속성을 사용**할 수 있게된다.

위 코드를 응용화면 다음과 같다.

```jsx
function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function(_title){
						if(typeof _title === 'string'){
							title = _title;
						} else {
							alert('에러: 제목은 문자열이어야 합니다. 현재: '+(typeof _title));
						}
        }
    }
}
var matrix = factory_movie(); 
matrix.set_title("matrix");  //문자열이 아니기 때문에 에러 출력
alert(matrix.get_title());
```

### 클로저의 응용

```jsx
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i;  //i가 함수의 외부 함수의 값이 아님
    }
}
for(var index in arr) {
    console.log(arr[index]()); //5가 다섯 번 출력
}
```

위 코드는 return i;의 i가 외부함수의 지역변수가 아니다. arr[i]에는 function 자체가 입력되기에 arr[i]의 모든 요소는 같은 주소를 공유하게 된다. 그렇기에 서로 다른 주소와 i의 값에 접근하기 위해서는 다음과 같이 바뀌어야 한다.

```jsx
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id){
			return function(){
        return id;  //i가 함수의 외부 함수의 값이 아님
			}
    }(i);
}

for(var index in arr) {
    console.log(arr[index]()); //0, 1, 2, 3, 4 출력
}
```