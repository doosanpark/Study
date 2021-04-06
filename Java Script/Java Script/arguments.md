# arguments

여러가지 인자를 담고 있는 객체로서 배열과 특징이 비슷하다.

```jsx
function sum(){
    var i, _sum = 0;    
    for(var i = 0; i < arguments.length; i++){
        document.write(i+' : '+arguments[i]+'<br />');
        _sum += arguments[i];
    }   
    return _sum;
}
document.write('result : ' + sum(1,2,3,4));
```

위 코드에서 sum 호출 과정을 보면 인자는 있으나 매개변수(파라미터)가 없음.

JS의 경우 인자와 매개변수의 갯수 차이가 나도 큰 문제가 없음

매개변수와 인자의 수를 비교하는 방식의 코딩도 가능함

```jsx
function two(arg1, arg2){
    console.log(
        'two.length', two.length,
        'arguments', arguments.length
    );
}
two('val1');  // two.length 2 arguments 1
```