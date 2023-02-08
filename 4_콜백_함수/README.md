## 4장 정리

>**세희**  
>중요한 점  
>- 콜백 함수의 제어권이 재미있고 중요하다고 생각
>- 코드 쓸 때 순서의 흐름을 한 번 읽어볼 수 있어서 좋았음
>몰랐던 점: 비동기(promise, generate, async, await)
  
>**찬균**  
>중요한 점  
>- 동기 비동기(async, await)가 빈도수가 높은 문법이라 중요하다고 생각
>- 비동기에 대한 공부가 제대로 되어 있어야겠다고 생각해 중요하게 봄
>- 인자 부분에 map 메소드가 나오는 것: map 메소드의 특성을 봐서 map에 대한 이해가 한층 더 깊어짐
  
>**효중**  
>중요한 점  
>- 비동기(async, await)
>- 콜백 함수 안에서 this값을 바인드하는 것
>어려운 점  
>P.101에 맵을 구현해보는 것: 맵의 기본적인 것은 알겠지만, 직접 구현해봤을 때 왜 이렇게 되는지 모르겠음
  
>**혜성**  
>중요한 점  
>- 비동기 제어 부분(특히 async, await)
>- 프로미스(알면 좋음) 제너레이터(빈도 낮음)
>- 실제로 회사채용에서도 나오는 개념
  
>**유진**  
>중요한 점  
>- 제어권을 다른 코드로 넘겨주는 것
>- this를 활용할 떄 기본적으로는 전역객체지만, 별도로 this가 할당될 때 그 대상을 참조하는 것
>- 콜백함수로 메소드를 전달하더라도 그 메소드는 메소드가 아닌 함수로서 호출되는 점
>어려운 점: 비동기 부분의 예제 코드가 어려웠음
>궁금한 점: 비동기 부분의 예제 코드
  
>**재훈**  
>중요한 점  
>- 콜백함수의 상황 예시(알람 예시): 뒤에 나오는 코드도 이 상황을 생각하니 잘 읽혔음
>- 콜백 지옥
>- 비동기(async, await)를 더 잘 이해할 수 있게 된 것 같음(코드를 어떻게 사용해야 할 지 감이 잡힘)
  
>**성은**  
>중요한 점  
>- 콜백함수의 뜻에 대해서 확실하게 알게 되었음
>- 비동기 제어 부분은 처음 봐서 이해하는 데 오래 걸림
>어려운 점: 비동기, 동기의 용어-비동기가 동시에 실행되는 건데 그 부분이 이해가 잘 안 감

>**은지**  
>중요한 점  
>- 콜백 함수도 함수라고, 어떤 객체의 메서드를 전달하더라도 메서드가 아닌 함수로서 호출되는 것
>- 비동기(promise, generate, async, await)
>어려운 점: P.106의 예쩨 4-11 바인딩 코드가 이해되지 않음  
  
## Q&A

### Q1. 동기와 비동기의 차이는?
- 동기: 동시가 아닌, 순차적으로 실행
- 비동기: 1번이 오래 걸리면 2번을 하다가 1번이 끝나면 나머지도 실행
  
### Q2. 왜 사람들이 동기적으로 쓰게 하기 위해서 노력했는가?
- 읽기 편하게 하기 위해서(위에서 아래로 읽는 게 편함)
- 여기서 나온 개념이 async, await
- 비동기적인 것을 동기적으로 만들기 위한 것이 개발자의 과제
    
### Q3. P.106 예제 4-11 코드
```js
var obj1 = {
    name: 'test',
    func: function() {
        console.log(this.name);
    },
};

var obj2 = {
    name: 'test2',
};

//콜백 함수에 전달받은 메서드(함수) => 함수
var bindFunc = obj1.func.bind(obj1);
setTimeout(bindFunc, 300); //0.3초가 지나고 한 번에(0.3초'마다'가 아님)
```
  
### Q4. async/await 코드1
```js
//시간을 기다리는 함수
var addCoffee = (name) => {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve(name);
        }, 1000);
    });
};

//Promise 3가지 상태
//1. pending(대기)
//2. rejected(실패)
//3. fulfilled(이행)

const main = async () => {
    const firstCoffee = await addCoffee("아메");
    console.log(firstCoffee)
}

main();

//async await을 빼면 프로미스 객체가 나옴(1번의 대기 상태)
```
  
### Q5. async/await 코드2
```js
const main = async () => {
    let coffeeList = "";

    coffeeList += await addCoffee("아메");
    coffeeList += await addCoffee("아샷추");
    coffeeList += await addCoffee("아바라");
    console.log(coffeeList)
}
main();
```
  
### Q6. async/await 코드3
```js
const _addCoffee = (커피리스트, 지금커피) => {
    return 커피리스트 + (커피리스트 ? ", " : "") + 지금커피;
}

const main = async () => {
    let 메인커피리스트 = "";

    메인커피리스트 = _addCoffee(메인커피리스트, await addCoffee("1"));
    메인커피리스트 = _addCoffee(메인커피리스트, await addCoffee("2"));
    메인커피리스트 = _addCoffee(메인커피리스트, await addCoffee("3"));
    
    console.log(메인커피리스트);
}

main();
```
  
## 링크

- https://discordapp.com/channels/1021027413020385351/1067376863422455838/1072439589849018418  
  
- https://discordapp.com/channels/1021027413020385351/1067376863422455838/1072439610984124436  
  
- https://discordapp.com/channels/1021027413020385351/1067376863422455838/1072453955562504202  
  
- https://discordapp.com/channels/1021027413020385351/1067376863422455838/1072454114463719424  
  