## 기준

### 동기/비동기

**작업 완료를 누가 신경 쓰는가?**

> 1. 동기: **호출한 함수**가 스스로 신경 쓴다.
> 2. 비동기: **호출된 함수**(callback 함수)가 신경쓰고, **호출한 함수**는 신경 쓰지 않는다.

<br>

### 블로킹/논블로킹

**호출되는 함수가 바로 return 되는가? 호출한 함수가 제어권을 넘겨주는가?**

> 1. 블로킹: **호출된 함수**가 자신의 작업을 모두 마칠 때까지 **호출한 함수**에게 제어권을 넘겨주지 않고 대기한다.
> 2. 논블로킹: **호출된 함수**에게 제어권이 넘어가지 않고, **호출한 함수**가 제어권을 가지고 계속해서 다른 일을 한다.

<br>

**판단 기준**
- 동기/비동기 → **작업 완료** 시점 기준
  - 동기(Synchronous): 작업이 완료될 때까지 기다림 (대기)
  - 비동기(Asynchronous): 작업 완료를 기다리지 않고 다른 작업 수행 

- 블로킹/논블로킹 → **제어권** 반환 여부 기준
  - 블로킹(Blocking): 호출한 함수가 작업이 끝날 때까지 제어권을 넘기지 않음 → 코드 흐름이 멈춤
  - 논블로킹(Non-blocking): 호출한 함수가 즉시 제어권을 반환 → 코드 흐름이 계속 진행됨

<br>
<br>

## 동기(synchronous),비동기(asynchronous)

### 동기(synchronous)
- 요청과 결과가 동시에 일어난다.
- 어떤 작업에 대한 요청이 발생했을 때, 그 요청에 대한 응답을 받을 때까지 대기해야한다.
- 작업에 대한 완료를 '호출한 함수'가 신경 쓰고 있다.

<br>

![image](https://github.com/user-attachments/assets/bcfa070b-4733-4e1b-8509-bbd9132a4091)

> Thread1 → 작업 위임 → Thread2
> 
> Thread2 작업 완료 전까지 → Thread1은 대기 상태

<br>
<br>

![image](https://github.com/user-attachments/assets/ff384ef0-42a3-40f1-bc36-f0a7983b7549)

Thread1이 작업1, 작업2, 작업3, 작업4를 가지고있다.

<br>
<br>

![image](https://github.com/user-attachments/assets/3cc191bc-d075-4351-9502-8a62f5f1993f)

Thread1이 작업1을 Thread2에게 보냈다. Thread1은 Thread2의 작업이 끝난 후부터 2라는 작업을 처리할 수 있다.

<br>
<br>

### 비동기(asynchronous)
- 요청과 결과가 동시에 일어나지 않는다.
- 작업에 대한 완료를 '호출 함수'가 아닌 'callback'이 신경 쓴다.

![image](https://github.com/user-attachments/assets/9a37db42-4867-4e89-bda8-7a7987e54129)

> Thread1 → 작업1(Task1) 위임 → Thread2
> 
> Thread1 → Task2 → Task3 계속 진행
> 
> Thread2 → Task1 수행 완료 (별개로)

<br>
<br>

![image](https://github.com/user-attachments/assets/09bb096d-93bc-4345-a3c4-16845ae6ca69)

Thread1이 작업1, 작업2, 작업3, 작업4를 가지고있다.

<br>
<br>


![image](https://github.com/user-attachments/assets/d1992437-250f-42f4-81cd-beee04163336)

Thread1이 작업1을 Thread2에게 보냈다. Thread1은 Thread2의 작업의 완료 여부에 상관 없이 계속 실행한다.

<br>
<br>

## 블로킹(Blocking), 논블로킹(Non-Blocking)

###  블로킹(Blocking)

![image](https://github.com/user-attachments/assets/07ce826c-558d-418a-b188-ac81593abb38)

A 함수가 실행 중 B 함수로 재어권이 넘어가면, A 함수는 더 이상 제어권을 갖지 않게 되며 B함수가 종료될 때까지 대기해야한다.

작업은 A 함수와 B 함수, 두 개로 구성되어 있으며, 제어권을 잃은 A 함수는 자신의 작업을 즉시 이어가지 못하고, B 함수가 끝날 때까지 기다린 뒤 중단했던 부분부터 다시 실행을 이어간다.

<br>
<br>

### 논블로킹(Non-Blocking)

![image](https://github.com/user-attachments/assets/267b3505-21b4-4bf3-b2bc-198b84427c88)

A 함수가 실행되는 도중에 B 함수가 호출되더라도, A 함수는 제어권을 B 함수에 넘기지 않고 계속 자신이 유지한다.

따라서, B 함수의 실행 완료 여부와 관계없이 A 함수는 자신의 작업을 중단하지 않고 그대로 이어서 수행한다.

<br>
<br>
<br>

## 조합

### 1. 동기(Synchronous) / 블로킹(Blocking)
- 동기(Synchronous) : 호출한 함수가 작업 완료 여부를 확인한다.
- 블로킹(Blocking) : 호출된 함수(task1)이 제어권을 가진다.
  
![image](https://github.com/user-attachments/assets/3a479959-4d42-441a-b059-977fe0cd9ee3)

Thread1은 task1이 완료될 때까지 대기해야 하며, 그동안 다른 작업을 수행하지 못한다.

실행 흐름이 순차적으로 진행되기 때문에 프로그램으 제어와 흐름을 예측하고 관리하기 쉽다.

<br>
<br>

### 2. 동기(Synchronous) / 논블로킹(Non-Blocking)
- 동기(Synchronous) : 호출한 함수가 작업 완료 여부를 확인한다.
- 논블로킹(Non-Blocking) : 호출된 함수가 제어권을 가진다.

![image](https://github.com/user-attachments/assets/bcc82399-6b70-4491-bba2-cc246ab5f5c5)

Thread1은 task1의 완료 여부와 관계없이 다른 작업을 동시에 진행할 수 있다.

단, task1의 완료 여부를 주기적으로 확인해야 하므로, 추가적인 관리가 필요하다.

<br>
<br>

### 3. 비동기(Asynchronous) / 블로킹(Blocking)
- 비동기(Asynchronous) : Callback 함수가 작업 완료 여부를 확인
- 블로킹(Blocking) : 호출된 함수(task1)이 제어권을 가진다.

![image](https://github.com/user-attachments/assets/fd6cb212-2537-4ed6-b520-4b3c3a395cce)

Thread1은 task1의 작업 완료 여부를 신경 쓰지 않지만, 작업이 완료될 때까지 아무것도 하지 못하고 대기 상태에 빠진다.

이 경우 비동기 방식임에도 불구하고 블로킹이 발생한 예로, 보통 비동기 + 논블로킹 조합에서 구현되었을 때와 같다.

<br>
<br>

### 4. 비동기(Asynchronous) / 논블로킹(Non-Blocking)
- 비동기(Asynchronous) : Callback 함수가 작업 완료 여부를 확인
- 논블로킹(Non-Blocking) : 호출한 함수가 제어권을 가짐

![image](https://github.com/user-attachments/assets/a60e7258-402f-45c2-b0e7-6dde289e0c3d)


Thread1은 task1의 완료 여부를 신경 쓰지 않고, 다른 작업을 동시에 진행한다.

이 방식은 성능과 자원 효율 면에서 가장 우수하다.

<br>
<br>








