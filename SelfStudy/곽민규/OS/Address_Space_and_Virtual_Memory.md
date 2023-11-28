- [ ] # 📬 주소 공간과 가상 메모리


  ## 🌝 초기 컴퓨터의 메모리 구성

  > 옛날 옛적 윤선희 담배 피던 시절 컴퓨터는...

  - 프로그램을 실행할때 한 번에 하나의 Process만 사용
  - 프로세스 하나 + OS가 전체 메모리를 사용
  - 활용성, 효율성이 부족함

  ## 🤹🏻 여러 프로그램을 동시에 실행할 때

  > Time Sharing 기법을 사용하여 여러 개의 프로그램 실행

  - 기존 방법 사용

    [<img src ="./images/Address1.png" width="400"/>](./images/Address1.png)

    - 프로세스 중단 → 디스크에 저장 → 다음 프로세스 불러오기 → 짧은 시간 실행 → 프로세스 중단 → ...
    - 디스크에 저장하는 과정이 느림
    - 새로운 방법 필요

  - 프로세스를 메모리에 유지하는 방법 사용

    [<img src ="./images/Address2.png" width="400"/>](./images/Address2.png)

    - 프로세스(공간A) 실행 → 중단 → 프로세스(공간B) 실행 → 중단 → 프로세스(공간C) 실행 ... 
    - 메모리 안에서 프로세스가 사용할 수 있는 공간을 나눔
    - 여러 개의 프로세스들이 서로의 메모리에 접근하지 않도록 적절한 할당 필요


  ## 💡 주소 공간(Address Space)과 가상 메모리(Virtual Memory)

  > OS가 프로세스에 메모리를 할당하는 과정에서 필요한 개념들

- 여러 프로세스들이 서로 데이터를 침범하지 않도록 OS에서 실제 메모리를 할당
- 프로세스 입장에서는 실제 메모리 주소를 알아야 할까?
    - OS가 관리해주지 않고 프로세스가 직접 메모리에 접근하는 것은 위험하고 번거로움
    - 프로세스 입장에서 사용하기 쉽고 안전한 메모리 개념이 필요 → **주소 공간**
- 프로세스가 요구하는 메모리가 너무 많거나 이미 많은 프로세스에 메모리를 할당해 부족하다면 프로세스에 메모리 할당을 못 할까?
    - 프로그램이 실행될 때 프로그램 전체가 실제 메모리에 있을 필요는 없음
    - 현재 실행되어야 하는 부분만 실제 메모리에 옮겨져 있으면 됨
    - 실제로 큰 메모리를 할당하지 않더라도 프로세스 입장에서 가상의 매우 큰 메모리가 있다고 보이게 함 → **가상 메모리**
- 주소공간과 가상메모리를 사용하는 이유와 목표?
  - 투명성 (transparency) : 프로세스 입장에서 마치 하나의 독립적인 실제 메모리가 있는 것 처럼 작동함
  - 효율성 (efficiency) : 시간&공간 자원을 효율적으로 사용하고 이를 위해 [TLB](./Paging.md#TLB)와 같은 하드웨어 지원을 받음
  - 보호 (protection) : 프로세스와 운영체제 자신을 다른 프로세스로부터 보호 (프로세스를 격리시킴)



  ### 💡 주소 공간(Address Space)

  > OS가 실제 메모리를 추상화해서 프로세스에 할당하는 것

- 프로그램 코드, 힙, 스택 등 프로그램 실행에 필요한 메모리 공간 존재

  [<img src ="./images/Address3.png" width="400"/>](./images/Address3.png)

  - 위 그림에서는 0~16KB 사이에 데이터가 있지만, 실제로 접근할 때는 OS가 할당한 임의의 물리 주소를 이용
  - Program Code : 기계어 형태의 코드, static / global 변수 (컴파일 시 저장, 프로그램 종료 시 반환)
  - Heap : 사용자의 동적 할당 영역 (런타임 시 저장, 원할 때 반환)
  - Stack : 지역변수, 함수의 매개변수 (함수 실행 시 저장, 종료 시 반환)
  - Program Code 영역의 크기는 고정되어 있는 반면, Heap&Stack 영역의 크기는 가변적이기 때문에 서로 마주보고 확장하는 형태


  ### 💡 가상 메모리(Virtual Memory)

> 실제 메모리 크기와 상관없이 메모리를 이용할 수 있도록 가상의 메모리 주소를 사용하는 방법

- 프로세스 입장에서 실제 물리주소의 매우 큰 공간을 가지고 있다고 생각하게끔 함
- 가상 주소가 아닌 실제 물리 주소를 보장하는 것은 OS의 역할
- MMU(Memory Management Unit) : 가상 주소 메모리 접근이 필요할 때, 해당 주소를 물리 주소값으로 변환해주는 하드웨어 장치
- 실제 메모리에 프로세스를 연속적으로 할당한다면 단편화 문제가 발생

  - 고정된 사이즈로 프로그램을 할당, 해제하는 과정(**고정 분할 기법**)을 반복한다면 → **내부 단편화** 발생

  [<img src ="./images/InternalFragmentation.png" width="400"/>](./images/InternalFragmentation.png)

  - 프로세스가 요청하는 메모리 크기만큼 할당, 해제하는 과정(**동적 분할 기법**)을 반복한다면 → **외부 단편화** 발생

  [<img src ="./images/ExternalFragmentation.png" width="400"/>](./images/ExternalFragmentation.png)
- [페이징](./Paging.md) 또는 [세그먼테이션](./Segmentation)을 통해 불연속적으로 할당하는 방법이 필요함

  <br>

  # ❓ 예상 질문

  <details>
    <summary><b>주소 공간에 대해 설명해주세요</b></summary>
    <div markdown="1">
    OS가 실제 메모리를 추상화해서 만든 공간으로, 코드, 스택, 힙과 같이 프로그램을 실행시키기 위한 모든 메모리 상태가 들어있습니다.
    </div>
  </details>

  <details>
    <summary><b>메모리를 가상화하는 이유에 대해 설명해주세요</b></summary>
    <div markdown="1">
    프로세스와 운영체제 자신을 격리시켜 메모리 침범으로부터 보호하고, 효율적이고 투명한 메모리 활용을 하기 위해서입니다.
    </div>
  </details>


  <br>

  # 👁‍🗨 Reference

  - [주소 공간과 가상 메모리(Address Space, Virtual Memory)](https://github.com/Fancy96/2023-CS-Study/blob/main/OS/os_address_space.md)
  - [[OSTEP] 주소 공간의 개념](https://velog.io/@kshired/OSTEP-%EC%A3%BC%EC%86%8C-%EA%B3%B5%EA%B0%84%EC%9D%98-%EA%B0%9C%EB%85%90)
  - [[컴퓨터시스템] 가상메모리 (Virtual Memory)](https://beeehappy.tistory.com/53)
  - [[OS] 메모리 단편화,페이징,세그멘테이션](https://velog.io/@nnnyeong/OS-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%8B%A8%ED%8E%B8%ED%99%94-%ED%8E%98%EC%9D%B4%EC%A7%95-%EC%84%B8%EA%B7%B8%EB%A9%98%ED%85%8C%EC%9D%B4%EC%85%98)

  
