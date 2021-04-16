# Object

Object 객체는 객체의 가장 기본적인 형태를 가지고 있는 객체이다. 다시 말해서 아무것도 상속받지 않는 순수한 객체다. 자바스크립트에서는 값을 저장하는 기본적인 단위로 Object를 사용한다.

```jsx
**var** grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
```

동시에 자바스크립트의 모든 객체는 Object 객체를 상속 받는데, 그런 이유로 **모든 객체는 Object 객체의 프로퍼티를 가지고 있다**.

# Object 객체 사용법

![Object%20ef312c3e8c71486ea12f8c321ef182ac/Untitled.png](.\Object/Untitled.png)

![Object%20ef312c3e8c71486ea12f8c321ef182ac/Untitled%201.png](.\Object/Untitled%201.png)



# Object 확장

다음과 같은 방식으로 기존에 없던 기능을 새롭게 추가하여 사용할 수 있게 만들 수 있다.

```jsx
Object.prototype.contain = function(neddle) {
    for(var name in this){
        if(this[name] === neddle){
            return true;
        }
    }
    return false;
}
var o = {'name':'egoing', 'city':'seoul'}
console.log(o.contain('egoing'));
var a = ['egoing','leezche','grapittie'];
console.log(a.contain('leezche'));
```

# Object 확장 시 주의점

Object에 속성을 추가하게 되면 다음처럼 Object를 상속 받는 모든 객체에 contain이 항상 추가되어 출력되는 문제가 생김

```jsx
Object.prototype.contain = function(neddle) {
    for(var name in this){
        if(this[name] === neddle){
            return true;
        }
    }
    return false;
}
var o = {'name':'egoing', 'city':'seoul'}
console.log(o.contain('egoing'));
var a = ['egoing','leezche','grapittie'];
console.log(a.contain('leezche'));

for(var name in o){
	console.log(name);  //name, city, contain 출력
}
for(var name in a){
	console.log(name);  //0, 1, 2, contain 출력
}

//해결책 중 하나
for(var name in o){
  if(o.hasOwnProperty(name)){
		console.log(name);  //name, city 출력
	}
}
for(var name in a){
  if(a.hasOwnProperty(name)){
		console.log(name);  //0, 1, 2 출력
	}
}
```