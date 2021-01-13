## 교착 상태란?

**둘 이상의 프로세스가 자원을 점유하고 있는 상태에서 서로의 자원을 요구함으로써 무한정 기다리는 상태**를 말합니다.



## 교착 상태의 조건

> 교착 상태가 되기 위해서는 다음 4가지 조건을 모두 만족해야합니다.

##### 상호 배제 (Mutual exclusion)

- 자원은 한 번에 한 프로세스만이 사용해야합니다.

##### 점유 대기 (Hold and wait)

- 최소한 하나의 자원을 점유하고 있으면서 다른 프로세스의 자원을 추가로 점유하기 위해 기다립니다.

##### 순환 대기 (Circular wait)

- 각 프로세스는 순환적으로 다음 프로세스가 요구하는 자원을 가지고 있습니다.

##### 비선점 (No preemption)

- 프로세스가 어떤 자원의 사용을 끝낼 때까지 그 자원을 뺏을 수 없습니다.



## 교착상태 해결 방법

### 예방 기법 (Prevention)

> 교착 상태가 발생되지 않도록 사전에 시스템을 제어하는 방법
>
> 발생 4가지 조건 중에서 어느 하나를 제거(부정) 

##### 상호 배제 부정

- 한 번에 여러 프로세스가 공유 자원을 사용할 수 있도록 합니다. (실제로 구현하지는 않음)

##### 점유 대기 부정

- 프로세스 실행 전 모든 자원을 할당하여 프로세스 대기를 없게 합니다.
- 자원이 점유되지 않은 상태에서만 자원을 요구하도록 합니다.

##### 순환 대기 부정

- 자원을 선형 순서로 분류하여 고유번호를 할당하고, 각 프로세스는 현재 점유한 자원의 고유 번호보다 앞이나 뒤 어느 한쪽 방향으로만 자원을 요구하도록 합니다.

##### 비선점 부정

- 다른 프로세스가 자원을 요구하면 점유하고 있던 자원을 반납하고, 기다리게 하는 것입니다.



### 회피 기법 (Avoidance)

> 교착 상태가 발생하면 적절히 피해나가는 방법

##### 은행원 알고리즘

운영체제에서 안전 상태를 유지할 수 있는 요구만을 수락하고, 불안정 상태를 초래할 사용자의 요구는 나중에 만족할 때까지 거절하는 방법입니다.

##### 자원 할당 그래프 알고리즘



### 발견 기법 (Detection)

> 시스템을 점검하여 교착 상태에 있는 프로세스와 자원을 발견하는 것



### 회복 기법 (Recovery)

> 교착 상태에 있는 프로세스를 종료하거나 자원을 선점하여 프로세스나 자원을 회복하는 방법

##### 프로세스 종료

교착 상태를 일으킨 프로세스를 종료합니다. 교착 상태에 있는 모든 프로세스를 종료하거나 하나씩 종료해 나가는 방법이 있습니다.

##### 자원 선점

교착 상태의 프로세스가 점유하고 있는 자원을 선점하여 다른 프로세스에게 할당하고, 해당 프로세스를 일시 정지하는 방법입니다.
