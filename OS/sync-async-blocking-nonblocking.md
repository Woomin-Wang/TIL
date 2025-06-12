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
> - 동기/비동기 - 작업완료
> - 블로킹/논블로킹 - 제어권

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
- 

<br>

### 논블로킹(Non-Blocking)
- 

<br>
