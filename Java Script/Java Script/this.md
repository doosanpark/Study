# this

# 함수와 this

this는 함수 내에서 함수 호출 맥락(context)를 의미한다. 맥락이라는 것은 **상황에 따라서 달라진다**는 의미인데 즉 함수를 **어떻게 호출하느냐**에 따라서 this가 가리키는 대상이 달라진다는 뜻이다. 함수와 객체의 관계가 느슨한 자바스크립트에서 this는 이 둘을 연결시켜주는 실질적인 연결점의 역할을 한다.

```jsx
function func(){
    if(window === this){
        document.write("window === this");
    }
}
func();  //결과: window === this
```

# 메소드와 this

**객체의 소속인 메소드의 this**는 그 객체를 가르킨다. 위 코드와 아래 코드를 봤을 때 func()와 o.func()에서 this의 동작 과정은 같다. 위 코드의 func()는 window의 메소드이고, 아래 코드에서 o.func()의 func()는 객체 o의 메소드이기 때문이다.

```jsx
var o = {
    func : function(){
        if(o === this){
            document.write("o === this");
        }
    }
}
o.func();  //결과: o === this
```

 

# 생성자와 this

아래 코드는 함수를 호출했을 때와 new를 이용해서 생성자를 호출했을 때의 차이를 보여준다.

```jsx
var funcThis = null; 
 
function Func(){
    funcThis = this;
}
var o1 = Func();
if(funcThis === window){
    document.write('window <br />');
}
 
var o2 = new Func();
if(funcThis === o2){
    document.write('o2 <br />');
}//내부적으로 비어있는 객체를 만들기에 생성자는 객체 내부의 생성자가 된다.
```

생성자는 빈 객체를 만든다. 그리고 이 객체내에서 **this는 만들어진 객체**를 가르킨다. 이것은 매우 중요한 사실이다. 생성자가 실행되기 전까지는 객체는 변수에도 할당될 수 없기 때문에 this가 아니면 객체에 대한 어떠한 작업을 할 수 없기 때문이다.

 

```jsx
function Func(){
    document.write(o);
}
var o = new Func();
```

# apply, call

함수의 메소드인 apply, call을 이용하면 this의 값을 제어할 수 있다.

```jsx
function sum1(x,y) {return x+y;}
sum1(1,2); //결과: 3
```

```jsx
var sum2 = new Function('x', 'y', 'return x+y;');
sum2(1,2); //결과: 3
```

sum1과 sum2는 같은 방식으로 선언된 함수이다. 원래 같은 경우 sum2 방식으로 함수를 선언해야 하지만 JS는 코딩을 쉽게 할 수 있도록 sum1과 같이 작성한 것을 자바스크립트 해석기를 통해 sum2처럼 변환하도록 한다. sum1과 같은 것을 함수 리터럴이라고 한다.

```jsx
var o = {}
var p = {}
function func(){
    switch(this){
        case o:
            document.write('o<br />');
            break;
        case p:
            document.write('p<br />');
            break;
        case window:
            document.write('window<br />');
            break;          
    }
}
func();
func.apply(o);
func.apply(p);
```

func.apply를 통해 o와 p객체를 호출하는 시점에서 this는 o와 p객체가 된다.