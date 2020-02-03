# GPU

- Kernel

  : GPU에서 처리하는 동작 내지는 함수를 의미하며, GPU가 처리하는 function 코드라고 볼 수 있다.
  
- Thread ㅡ> (Warp ㅡ>) Block ㅡ> Grid

  : Thread가 모여서 Block이 되고, Block이 모여서 Grid가 된다.



![1565922528467](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565922528467.png)

- HardWare

  - Scalar Processor(SP)

    - 정수 계산을 위한 ALU, 실수 계산을 위한 FPU, 데이터를 load/store하기 위한 LSU를 갖고 있다.

    - 4개의 스레드로 구성.

  - Streaming Multiprocessor(SM)

    - 8개의 SP로 이루어져 있고 GPU는 SM의 집합니다.
  - 32개의 스레드가 있으며 이 32개의 스레드를 워프(Warp)라고 부른다.
    
    - CUDA 프로그램에서 warp와 block 단위의 실행을 담당한다.
    
  - Shared Memory

    : SM내에 있는 8개 SP가 서로 데이터를 공유하고 빠르게 사용할 수 있는 메모리

- Software

- Thread ㅡ> (Warp ㅡ>) Block ㅡ> Grid

  : Thread가 모여서 Block이 되고, Block이 모여서 Grid가 된다.

  - Thread - register - SP(내 추정)

    : 커널 함수 등이 호출되었을 때 실제로 엄무를 수행하는 최소의 단위

  - Warp - SM(이렇게 쓰일수도 있지만 Block에 대응시키는게 보통인 듯)

    : 보통 32개의 스레드를 묶어 1개의 워프를 구성, 몇 개의 스레드를 묶어서 하나의 워프로 할지는 구현마다 다르다.

  - Block - 공유 메모리(Shared Memory) - SM

    : 스레드가 모이면 블록이 된다.

  - Grid - 전역 메모리(상수 메모리, 텍스쳐 메모리, global 메모리)



![1565920808811](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565920808811.png)



| 구분 |   CUDA    |   학교    |
| ---- | :-------: | :-------: |
|      |   Grid    |   학년    |
|      |   Block   |    반     |
|      | Block ID  |  반 번호  |
|      |  Thread   |   학생    |
|      | Thread ID | 학생 번호 |



- blockIdx : 블록의 인덱스

- threadIdx : 스레드의 인데스

- blockDim : 블록당 스레드의 수, 블록이 몇 차원으로 구성되어 있는지

- gridDim : 그리드당 블록의 수

  ![1565864614459](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565864614459.png)

