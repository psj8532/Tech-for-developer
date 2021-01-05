### Bloking / NonBlocking 과 Synchronous / Asynchronous



### Bloking / NonBlocking

> 호출된 함수가 바로 리턴을 하는지 아닌지가 중점

##### Blocking

- 호출된 함수가 자신의 작업을 <u>모두 마치고</u> 리턴하면서 제어권을 넘겨준다. 따라서 호출한 함수는 호출된 함수가 <u>작업이 끝날 때까지 계속 기다려야한다</u>.

##### NonBolocking

- 호출된 함수가 바로 리턴해서 **제어권**을 <u>호출한 함수에게 넘겨주고</u>, 호출한 함수는 그 동안 다른 일을 할 수 있다.



### Synchronous / Asynchronous

> 호출된 함수의 작업 완료 여부를 누가 확인하는지가 중점

##### Synchronous

- 호출된 함수의 작업 완료 여부를 호출한 함수가 계속 확인

##### Asynchronous

- 호출된 함수에 콜백 함수를 같이 전달하여, 작업 완료가 되면 콜백함수를 실행한다. 따라서 호출한 함수는 작업 완료 여부를 전혀 신경쓰지 않는다.



![](C:\Users\eladh\Desktop\project\Tech-for-developer\Programming\images\block-sync-nonblock-async.PNG)



### 다른 조합

> 일반적으로 Sync와 Block은 비슷한 동작을하고, `Async`와 `Nonblock`이 비슷한 동작을합니다. 하지만 이 둘을 섞어서 조합을 만든 경우 더 깊이 생각해봐야합니다

##### NonBlock + Sync

- 호출된 함수는 바로 리턴해서 제어권을 넘겨주어, 호출한 함수는 다른 작업을 수행할 수 있습니다. 하지만, 호출된 함수의 작업 완료 여부를 계속 문의하여 확인해줍니다. 정리하면, 다른 작업을 수행하면서도 호출한 함수의 작업 완료 여부를 계속 확인하는 것입니다.

![](C:\Users\eladh\Desktop\project\Tech-for-developer\Programming\images\nonblock-sync.PNG)

##### Block  + Async

- 호출된 함수는 작업을 모두 마친후에 리턴하지만, 호출한 함수는 작업 완료 여부를 신경쓰지 않는 것입니다. 그래서 호출한 함수는 작업 완료 여부를 문의만 하지 않을뿐, 호출된 함수가 끝날때까지 다른 일을 하지 못하고 대기하다가 작업이 끝나면 콜백이 실행되는 것입니다. 이 경우 어차피 다른 일을 할 수 없으므로 Block + Sync 방식과 유사하며 이점이 없으므로 잘 사용하지 않습니다.

![](C:\Users\eladh\Desktop\project\Tech-for-developer\Programming\images\block-async.PNG)



#### 참고

> - http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/