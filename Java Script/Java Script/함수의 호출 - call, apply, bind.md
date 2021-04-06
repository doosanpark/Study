# 함수의 호출 - call, apply, bind

```jsx
function func(){}
func();
```

func()와 같은 객체는 속성을 가지고 있다. 속성에 함수가 들어있다면 method라고 부른다.

func()는 객체이기 때문에 메소드를 가지고 있다. 이것은 JS가 만들어준다.

이 덕분에 func.apply와 func.call과 같은 메소드에 접근 가능하다.

```jsx
function sum(arg1, arg2){
    return arg1+arg2;
}
alert(sum.apply(null, [1,2]))
```

sum.apply(null, [인자의 첫번째 값, 인자의 두번째 값]);

```jsx
o1 = {val1:1, val2:2, val3:3, sum:sum}
o2 = {v1:10, v2:50, v3:100, v4:25}
function sum(){
    var _sum = 0;
    for(name in this){
        _sum += this[name];
    }
    return _sum;
}
alert(sum.apply(o1)) // 6
alert(sum.apply(o2)) // 185
```

this는 함수가 **호출 시**에 선언된다. 그렇기에 함수 sum() 그 자체에서 this에는 아무런 데이터가 담기지 않는다.

apply는 함수를 호출할 때 사용한다. sum.apply(o1) 이걸 실행시키면 this가 o1이 된다.