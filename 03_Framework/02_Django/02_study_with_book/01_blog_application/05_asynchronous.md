# Asynchronous (비동기)

## 1. 비동기란?
비동기(Asynchronous)는 작업이 완료될 때까지 기다리지 않고, 다른 작업을 동시에 수행할 수 있는 프로그래밍 모델이다. 다시 말해서, 특정 작업이 완료되기를 기다리지 않고, 그 작업이 진행되는 동안 다른 작업을 계속할 수 있게 해준다.

이를 통해 시스템의 효율성을 높이고, I/O 작업은 시간이 걸리는 작업을 효과적으로 처리할 수 있다. I/O Interrupt 가 들어오는 동안 Idle 상태에 있는 Thread 를 다른 작업을 수행하는 데에 사용할 수 있기 때문이다.

## 2. 멀티쓰레딩이란?
쓰레드에 대해서 설명할 때는 싱글 코어라고 가정하는 것이 좋다. 앞으로의 설명은 CPU 가 싱글 코어라고 가정한 상황에서 진행한다.

CPU 코어란, 중앙 처리 장치(Central Processing Unit, CPU) 내에서 독립적으로 명령을 실행할 수 있는 기본적인 처리 단위이다. 요즘 나오는 CPU 에는 보통 여러 개의 코어가 있다. 그리고 각 코어는 독립적으로 작업을 수행할 수 있는 능력을 가지고 있다.

하나의 코어는 여러 개의 쓰레드를 가지고 있다. 지금부터 싱글 코어를 기반으로 설명한다.

멀티 쓰레딩은 하나의 CPU 코어가 가지고 있는 여러 개의 쓰레드를 번갈아가며 사용하는 것이다. 한 시점을 정확하게 짚었을 때, 하나의 코어는 하나의 쓰레드밖에 동작시키지 못한다. 그러나, 이 과정에서 컨텍스트 스위칭(Thread 가 동작시키는 프로그램을 변경하는 일)을 통해 여러 쓰레드를 처리할 수 있다.

하나의 코어는 하나의 쓰레드만 동작할 수 있게 만들고, 하나의 쓰레드는 하나의 작업만 처리할 수 있다. 예를 들어, 하나의 코어에 할당 된 쓰레드가 다섯 개라면, 컴퓨터는 이론적으로 한 번에 다섯 개의 일만 처리할 수 있는 것이다. 크롬 브라우저가 다섯 개 띄워져 있다면, 한 시점에 크롬 웹 브라우저 서칭 외에 다른 일은 할 수 없다.

하지만 요즘 컴퓨터를 보면, 크롬 브라우저를 다섯 개 이상 띄우고, 카카오톡도 실행할 수 있다. 물론 멀티 코어의 도움도 있겠지만, 멀티 쓰레딩의 도움이 더 크다고 볼 수 있다.

멀티 쓰레드는 CPU가 빠르게 쓰레드 간에 전환하여 여러 작업을 수행하는 것처럼 보이게 만드는 방법이다. 예를 들어, 하나의 쓰레드만 사용하더라도 카카오톡에서 한 프로그램을 다운받는 것과 다른 사람에게 메시지를 보내는 것이 동시에 가능하다.

이는 하나의 쓰레드가 네트워크를 통해 파일을 다운받는 것과 사용자에게 I/O 처리를 받는 것을 매우 빠른 순간에 컨텍스트 스위칭을 할 수 있기에 가능한 것이다.

## 3. 비동기 처리란?
멀티 쓰레딩과 비동기 처리는 다르다. 비동기 처리는 주로 I/O 작업 또는 시간이 걸리는 작업을 효율적으로 처리하기 위한 프로그래밍 패턴이다. 비동기 방식에서는 한 작업이 완료될 때까지 기다리지 않고 다른 작업을 수행할 수 있도록 설계되어 있다.

멀티 쓰레딩을 이용하여 비동기 처리를 할 수는 있다. 하지만, 비동기 처리를 함에 있어서 꼭 멀티 쓰레딩을 사용해야 하는 건 아니다. 하나의 쓰레드 만으로도 비동기 처리를 할 수 있고, 이게 비동기 처리와 멀티 쓰레딩의 가장 큰 차이점이다.

**비동기 처리는 작업을 어떻게 처리할 것인가에 대한 방법론이며, 멀티 쓰레딩은 실제로 작업을 수행하는 구체적인 방식이다.**

하나의 쓰레드 만으로 비동기 처리를 구현하는 것은 Java 에서도 가능하지만, Java 의 비동기 처리 모델은 주로 멀티 쓰레딩을 통해 구현된다.

반면, JS 는 기본적으로 싱글 쓰레드 환경에서 실행된다. 그런 의미에서, 싱글 쓰레드 만으로 비동기 처리를 가능하게 하는 JS 코드 예시를 보자.

## 4. 싱글 쓰레드로 비동기 처리하는 JS 코드 예시
```js
// 비동기 파일 쓰기 시뮬레이션
const fs = require('fs');

// 비동기 파일 쓰기
fs.writeFile('message.txt', 'Hello, World!', (err) => {
    if (err) {
        console.error('파일 쓰기 실패:', err);
        return;
    }
    console.log('메시지 저장 완료!');
});

// 비동기 네트워크 다운로드 시뮬레이션 (setTimeout 사용)
setTimeout(() => {
    console.log('네트워크 다운로드 완료!');
}, 2000);

// 메인 스레드 작업
console.log('메인 스레드 작업 중...');
```

위 코드에서 함수는 총 세 개다. 비동기 파일 쓰기 작업, 비동기 네트워크 다운로드 시뮬레이션, 메인 쓰레드 작업이다.

하나의 쓰레드라고 하더라도, 세 개의 메서드는 거의 동시에 실행된다. 물론 초기에 함수가 호출될 때는 위에서 아래로 코드를 실행한다. 이 과정은 동기적이며, 각 명령어는 순차적으로 실행된다.

그에 따라, 함수의 **호출 순서** 는 비동기 파일 쓰기 -> 비동기 네트워크 다운로드 -> 메인 스레드 작업 순으로 이루어진다.

그러나, 하나의 쓰레드가 작업이 마무리 될 때까지 기다리지 않고 다른 함수를 동작시킬 수 있으므로 함수가 마무리 되고 console.log 가 실행되는 시점은 세 메서드의 실행 시간에 따라 다르다.

만약 fs.writeFile 메서드가 매우 빠른 속도로 실행된다면, "메인 스레드 작업 중..." 이라는 메세지보다 더 빠르게 "메시지 저장 완료!" 라는 메시지가 출력될 수 있는 것이다.

주목해야 할 부분은 setTimeout() 쪽에 있는 코드이다. 하나의 쓰레드를 가진 싱글 쓰레드지만, 해당 메서드가 2초 동안 다른 작업을 수행하는 동안에 메인 스레드나 비동기 파일 쓰기 작업이 가능하다는 것이다.

나도 처음 안 사실인데, 실제로 다운로드를 하는 과정에서 비동기 작업을 수행하면, 메인 스레드는 대기하지 않으며 다운로드를 처리하는 주체는 메인 스레드가 아니라고 한다. 대신, 자바스크립트의 비동기 처리 모델과 이벤트 루프가 이를 관리한단다.

네트워크 요청(fetch API 등)을 사용하면, JS 는 HTTP 요청을 비동기적으로 처리한다. 이 과정에서 요청은 브라우저나 Node.js 의 네트워크 모듈에 의해 처리된다. 즉, 실제 네트워크 작업은 메인 스레드가 아니라, 운영체제의 네트워크 스택이나 브라우저의 내부에서 처리된다.

메인 스레드는 이러한 비동기 요청을 시작한 후, 다른 작업이나 코드 실행을 계속한다. 이때 메인 스레드는 요청의 완료를 기다리지 않는다.

위 작업에서 비동기 코드의 흐름은 다음과 같다.

1. 비동기 작업(예: 파일 다운로드)을 시작한다.
2. 메인 스레드는 대기하지 않고 다음 코드를 실행한다.
3. 비동기 작업이 완료되면, 해당 작업의 콜백이 이벤트 큐에 추가된다.
4. 메인 스레드는 현재 실행 중인 작업이 끝난 후 이벤트 큐를 확인하고, 콜백을 실행한다.

## 5. JS 가 비동기 처리를 하는 방법
비동기 처리는 이벤트 루프를 통해 작업을 스케줄링하며, 특정 작업이 완료되면 콜백이나 프라미스를 통해 결과를 처리한다. 이는 주로 네트워크 요청이나 파일 시스템 작업 등에서 사용된다.

### 5-1. 이벤트 루프(Event Loop)란?
이벤트 루프는 비동기 프로그래밍에서 중요한 역할을 하는 구조로, 비동기 작업을 관리하고 실행하는 메커니즘이다. 이벤트 루프는 다음과 같은 방식으로 작동한다.

1. 콜스택 : JS 는 싱글 스레드로 동작하므로, 하나의 호출 스택을 사용하여 현재 실행 중인 함수들을 관리한다. 함수가 호출되면 스택에 추가되고, 실행이 끝나면 스택에서 제거된다.

2. 이벤트 큐 : 비동기 작업이 완료되면, 해당 작업의 콜백 함수가 이벤트 큐에 추가된다. 이 큐는 메인 스레드가 처리해야 할 작업을 기록한다.

3. 루프 과정
- 메인 스레드는 콜 스택이 비어 있을 때 이벤트 큐를 확인한다. (비동기 작업은 빠르게 처리될 수 있는 작업으로 구성)
- 이벤트 큐에 대기 중인 콜백이 있으면, 이를 콜 스택으로 가져와 실행한다. (밀린 비동기 작업 처리)
- 이러한 과정을 반복하여 비동기 작업을 효율적으로 처리한다.

### 5-2. 콜백(CallBack)이란?
콜백은 특정 작업이 완료된 후 호출되는 함수이다. 주로 비동기 작업에서 결과를 처리하기 위해 사용된다. 예를 들어, 파일 읽기 작업이 완료된 후에 결과를 처리하는 함수를 콜백으로 전달할 수 있다.

그러나, 콜백을 중첩해서 사용하는 경우 "콜백 헬" 이라고 불리는 가독성 문제를 초래할 수 있다. 이는 코드의 유지보수를 어렵게 만들고, 오류 발생 시 디버깅이 복잡해질 수 있다.

### 5-3. 프라미스(Promise)란?
프라미스는 비동기 작업의 완료 여부와 결과 값을 나타내는 객체이다. 프라미스를 사용하면 비동기 작업을 더 직관적으로 처리할 수 있다.

프라미스는 세 가지 상태를 가진다.
- 대기(Pending) : 초기 상태, 완료되지 않은 상태.
- 이행(Fulfilled) : 작업이 성공적으로 완료된 상태.
- 거부(Rejected) : 작업이 실패한 상태.

추가적으로, .then() 메서드를 사용하여 프라미스의 결과를 처리하고, .catch() 를 통해 오류를 처리할 수 있다. 이를 체이닝 방식이라고 하는데, 가독성을 높이고 콜백 헬 문제를 해결하는 데 기여한다.

```js
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { name: "John Doe" };
            resolve(data); // 작업 완료 후 resolve 호출
        }, 1000);
    });
}

fetchData()
    .then(data => {
        console.log('데이터:', data);
    })
    .catch(error => {
        console.error('오류:', error);
    });
```

### 5-4. aysnc, await
async 와 await 는 프라미스를 기반으로 한 비동기 코드를 더 간결하고 읽기 쉽게 만들어주는 문장이다. 주요 특징은 다음과 같다.

- async 함수 : async 키워드를 사용하여 정의된 함수는 항상 프라미스(비동기 작업의 완료 여부와 같은 결과 값을 나타내는 객체)를 반환한다. 함수 내에서 비동기 작업을 수행할 수 있다.

- await 함수 : await 키워드를 사용하여 프라미스가 이행될 때까지 기다린다. await 는 async 함수 내에서만 사용할 수 있다.

비동기 작업을 처리하는 동안에, 특정 데이터나 결과를 순차적으로 처리해야 할 경우 async 와 await 를 함께 사용할 수 있다. 예를 들어, 여러 비동기 작업이 있지만, 각 작업이 완료된 후 다음 작업을 수행해야 할 때 유용하다.

## 6. 비동기 처리의 파이썬 코드 예시
다음은 Python의 asyncio를 사용한 비동기 코드 예시이다.
```python
import asyncio

async def fetch_data():
    print("Fetching data...")
    await asyncio.sleep(2)  # Simulates a network delay
    print("Data fetched!")
    return "Data"

async def main():
    result = await fetch_data()
    print(result)

# 실행
asyncio.run(main())
```

js 와 상당히 비슷한 형태를 띤다.

## 7. 비동기 처리의 장단점

### 7-1. 비동기 처리의 장점
- 효율적인 I/O 처리 : 대기 시간 동안 다른 작업을 수행할 수 있다. (네트워크 요청 동시 가능, Idle Time 줄임)
- 높은 동시성 : 많은 요청을 동시에 처리할 수 있습니다. (여러 클라이언트의 요청을 동시에 처리할 수 있음)

### 7-2. 비동기 처리의 단점
- 복잡성 증가 : 비동기 코드의 흐름을 이해하고 관리하기 어려울 수 있습니다.
- 디버깅 어려움 : 비동기 작업의 상태를 추적하기 어려울 수 있습니다.

## 8. 동기 처리의 장단점

### 8-1. 동기 처리의 장점
- 코드의 흐름이 명확하고 이해하기 쉽다.
- 디버깅이 상대적으로 쉽다.

### 8-2. 동기 처리의 단점
- I/O 작업 시 대기 시간이 길어질 수 있으며, 다른 작업을 수행하지 못한다.
- 동시성 처리에 한계가 있다.

## 9. 비동기의 경우 트랜잭션 처리는 어떻게 되는가?
데이터베이스 트랜잭션 처리에서는 데이터의 무결성과 일관성을 보장하는 것이 매우 중요하다. 동기 방식은 이러한 안정성을 제공하는 데 유리하다.

트랜잭션의 ACID(Atomicity, Consistency, Isolation, Durability)을 보장하기 위해서는 동기적으로 작업을 처리하는 것이 필요하다. 예를 들어, 한 트랜잭션 내에서 여러 작업이 성공되어야만 전체 트랜잭션이 커밋되어야 하며, 중간에 오류가 발생하면 롤백해야 한다.

이런 관점에서 동기 방식이 순차적 처리를 자연스럽게 지원하기 때문에, 데이터의 일관성을 유지하는 데에 도움이 된다.

그러나, 내가 배울 Django 의 ORM 은 비동기 ORM 을 지원한다. 어떻게 데이터의 일관성을 유지할까?

---

비동기 ORM 을 사용한다고 하더라도 트랜잭션을 시작하고, 여러 작업을 수행한 후, 모든 작업이 성공적으로 완료되면 한 번에 커밋한다. 이러한 과정은 동기 처리를 지원하는 것이다.

또한, atomic() 컨텍스트 매니저를 사용하여 원자성(Atomicity)을 구현할 수 있다. atomic() 을 사용하면 여러 데이터베이스 작업을 하나의 트랜잭션으로 묶을 수 있다. 이 트랜잭션 내에서 모든 작업이 성공해야만 커밋되며, 중간에 오류가 발생하면 모든 작업이 롤백된다.

Django 의 ORM 이 비동기 ORM 이라고 불리울 수 있는 이유는, 비동기적으로 쿼리를 실행하고 결과를 기다릴 수 있기 때문이다. 그럼에도 불구하고, 비동기 ORM 은 내부적으로 동기 처리의 트랜잭션을 관리하여 ACID 속성을 유지한다.

## 10. 비동기 ORM 과 동기 ORM 의 차이점
주로 쿼리 실행 방식과 처리 흐름에 있다.

### 10-1. 쿼리 실행 방식
동기 ORM 에서는 데이터베이스 쿼리 실행이 블로킹 방식으로 이루어진다. 다시 말해서, 쿼리를 실행하면 해당 작업이 완료될 때까지 코드의 실행이 멈춘다.

예를 들어, 데이터베이스 쿼리를 실행하고 기다리는 동안 다른 작업을 수행할 수 없다. 이로 인해 전체 애플리케이션의 응답성이 저하될 수 있다.

반면에 비동기 ORM 에서는 데이터베이스 쿼리 실행이 비블로킹 방식으로 이루어진다. 즉, 쿼리를 실행할 때 await 키워드를 사용하여 결과를 기다릴 수 있으며, 이 동안 다른 작업을 수행할 수 있다.

또한, 비동기 ORM 은 이벤트 루프를 기반으로 하여 여러 비동기 작업을 동시에 처리할 수 있어, 높은 동시성을 제공한다.

### 10-2. 코드 흐름
동기 ORM 에서는 코드가 위에서 아래로 순차적으로 실행되며, 각 쿼리의 결과를 기다리는 동안 다음 코드는 실행되지 않는다. 이로 인해 코드 흐름이 명확하지만, I/O 작업이 많을 경우 대기 시간이 길어져 성능이 저하될 수 있다.

비동기 ORM 에서는 코드가 비동기적으로 실행되며, 여러 작업을 동시에 진행할 수 있다. **비동기 쿼리를 실행할 때, 결과를 기다리는 동안 다른 비동기 작업을 수행할 수 있다.** 다만, 코드가 복잡해질 수 있으며, 가독성을 유지하기 위해 적절한 구조와 패턴을 사용하는 것이 중요하다.

예를 들면, 한 데이터베이스에 저장하는 쿼리를 던지고 다른 데이터베이스에 복제하는 코드 대신, 두 데이터베이스에 동시에 저장하는 쿼리를 기다리고 이를 트랜잭션으로 묶어 안정성을 확보함과 동시에 복제를 용이하게 관리할 수 있겠다.

### 10-3. 사용 사례
동기 ORM 은 단순한 애플리케이션이나 I/O 작업이 적은 환경에서 유용하다. 예를 들어, 간단한 데이터베이스 CRUD 작업을 수행하는 작업을 수행하는 애플리케이션에서 적합하다. 또한 데이터의 일관성과 안정성이 중요한 경우에도 동기 ORM 이 선호될 수 있다.

반면, 높은 동시성이 요구되는 웹 애플리케이션이나 실시간 데이터 처리 시스템에서 유용하다. 예를 들어, 사용자가 매우 많은 웹 서비스나 API 서버에서 비동기 ORM 을 사용하면 성능을 극대화할 수 있다.

### 10-4. 개인적인 의견
대규모 서버에서는 Java 가 Django, Node.js 보다 더 나을 것이라고 생각한다. 그리고 비동기는 RabbitMQ 혹은 Kafka 를 통해서도 구현할 수 있을 것이다. 이렇게 별도의 비동기 처리 서버를 이용하면 해결할 수 있는 문제이기 때문에, 높은 동시성이 요구된다고 해서 비동기 ORM 을 꼭 써야하는 건 아니지 않을까 싶다.