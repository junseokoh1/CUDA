# CUDA API 아키텍쳐



![1565920959270](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565920959270.png)

- CUDA Driver API

  : 가장 low level

- CUDA Runtiem API

  : CUDA Driver API의 상위 레벨에 존재, 가장 많이 사용

- CUDA Libraries

  : 특정 계산을 위한 기능들을 제공

  

# CUDNN

- cuDNN : CUDA 기반 Deep Neural Network 라이브러리
- CDUA가 GPU 이용 고속연산처리 수단이므로 cuDNN도 GPU를 이용한 고속화 처리 가능
- DNN 응용에서 자주 요구되는 루틴들을 제공
  - convolution, Pooling, Softmax forward and backward 등



- ```
  cudnnTensorDescriptor_t
  ```

  : a pointer to an opaque(struct나 class를 완전히 정의하지 않은 상태로 갖고있는 타입) structure holding the description of a generic n-D dataset.

    cudnnCreateTensorDescriptor() is used to create one instance.

  
  
- ```
  cudnnHandle_t
  ```

  ![1565759415401](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565759415401.png)

- cudnnSoftmaxForward 222pg



# CUDA

- Compute Unified Device Architecture

  :GPU에서 수행하는 병렬처리 알고리즘을 산업 표준 언어를 사용하여 작성할 수 있도록 하는 GPGPU 기술. CUDA 플랫폼은 컴퓨터 커널의 실행을 위해 GPU의 가상 명령 집합과 병렬 연산 요소들을 직접 접근할 수 있는 소프트웨어 계층이다.

  - GPGPU(General-Purpose computing on Graphics Processing Units)

    : 일반적으로 컴퓨터 그래픽스를 위한 계산만 맡았던 그래픽 처리 장치(GPU)를, 전통적으로 중앙 처리 장치(CPU)가 맡았던 응용 프로그램들의 계산에 사용하는 기술
  
- NVCC(Nvidia CUDA Compiler)

  : CUDA와 함께 사용하기위한 Nvidia의 독점 컴파일러입니다.

  - 코드를 host부분과 decive에 들어갈 부분을 분리

    Device function - NVIDIA compiler가 처리

    Host funtions - 일반 compiler가 처리

![1565684681840](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565684681840.png)

- Host : CPU와 CPU 메모리를 의미합니다. (Host Memoery)
- Device : GPU와 GPU메모리를 의미합니다. (Device Memeory)
- C프로젝트에 소스파일(~.c)과 헤더파일(~.h)이 존재하듯이 CUDA에는 소스파일(~.cu)과 헤더파일(~.cuh)이 존재



-   threadIdx, blockIdx, blockDIM,gridDIM



- ```
  _global_
  ```

  : CUDA C/C++ keyword로 이 키워드를 앞에 붙인 함수는 다음과 같은 의미를 가집니다.

  - Device에서 실행됩니다.
  - Host에서 호출합니다.

- Execution configuration syntax

  global function must specify the execution configuration for that call.

  : host code가 device code를 호출한다는 마킹

  ```c++
  <<< Dg, Db, Ns, s >>>
  ```

  - ​	example

    ```
    _global_ void Func(float* parameter);
    ```

    이 함수를 호출하는 방법

    ```
    Func<<< Dg, Db, Ns >>>(parameter);
    ```

    - Dg : type dim3 and specifies the dimenstion and size of the grid
    - Ns : type size_t and specifies the number of bytes in shared memory 

  - kernel <<< noBlock, threadsPerBlock >>>

    위큐에서 이렇게 사용

    총 thread수 = noBlock * threadsPerBlock

- **threadIdx**

  ```
  threadIdx
  ```

  Each thread that executes the kernel is given a unique thread ID that is accessible within the kernel through the built-in threadIdx variable.

  3-component vector 
  $$
  D~x~, D~y~, D~z~
  $$
  ​			

  ```c++
  int i = threadIdx.x;
  int j = threadIdx.y;
  ```



### Device memory

- ```c++
  cudaMalloc()
  ```

  ddd

- ```c++
  cudaFree()
  ```

  dd

- ```c++
  cudaMemcpy()
  ```

  ddd



- dd

- ```c++
  cudaFree()
  ```

  dd

  

- ```c++
  cudaMemcpy()
  ```




# WICWIU

- ```
  cudaDeviceProp
  ```

  : 이 구조체 형식을 이용하여 device들의 정보를 저장합니다. 이를 이용하여 device의 다양한 정보를 불러올 수 있습니다.

- cudaGetDevice

  ![1565856912193](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565856912193.png)

- cudaGetDeviceProperties

  ![1565857204529](C:\Users\오준석\AppData\Roaming\Typora\typora-user-images\1565857204529.png)



ss