---
title: "멀티 스레드와 멀티 프로세스"
tags:
    - python
    - library
    - threading
    - multiprocessing
date: "2023-08-29"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---
# **threading&multiprocessing**
---

## **threading**
---
스레드를 늘려서 다른 코드들이 동시에 작동하는것 처럼 만들어주는 라이브러리

> **class threading.Thread(target=None, name=None, args=(), kwargs={}, *, daemon=None)** \***
> * 스레드 생성을 하는 클래스선언
> * **target** 매개변수는 스레드에 함수를 할당할 수 있다.
> * **name** 매개변수는 스레드에 이름을 할당할 수 있다.
> * **args** 매개변수는 스레드에 가변 매개변수들을 할당할 수 있다.
> * **kwargs** 매개변수는 스레드에 키워드 가변 매개변수들을 할당할 수 있다.  
> * **demon** 매개변수는 True/false를 받으며 스레드를 데몬 스레드로 만들어서 메인스레드와 운명을 같이 하게 된다.
>
> **.start()** \***
> * 스레드 객체의 작동 메서드(.run() 메서드를 작동시킨다.)
>
> **.run()**
> * 스레드 서브 클래스를 만들때 추가적으로 작동 하고 싶은것을 선언할 수있다.
>
> **.join(timeout=None)** \***
> * 스레드가 종료 될때까지 이후의 코드를 작동하지 않는다.
> * **timeout** 매개변수는 스레드에 시간제한을 줄 수 있으며, <span style="color:red">시간제한을 초과하면 스레드를 멈춰줘야한다.</span>
>
> **.is_alive()**
> * 스레드가 작동중인지 확인 할 수 있으며, 작동시 True를 반환한다.  

파이썬의 스레드는 하나의 프로세스에서 여러개의 스레드를 병렬 처리한다. 이때 공유되는 자원들을 동시에 변형가하면 충돌을 발생해 무시될 수 있다. 다음에 소개 할 threading.Lock() 클래스는 이를 해결해준다.

> **class threading.Lock()** \***
> * 스레드의 락 기능을 선언하는 클래스
>
> **.acquire(blocking=True, timeout=- 1)** \***
> * 락 기능이 작동중인지 작동중이지 않은지 수 있는 메서드.
> * **blocking** 매개변수가 True이면 락을 작동(코드 멈춤)하고 True를 반환하고, False이면 락을 작동시키지 않고(코드 진행) 추후에 True/False를 반환합니다.(default: true)
>
> **.release()** \***
> * 스레드의 락을 해제하며 <span style="color:red">해제된 스레드에서 작동시 런타임 오류발생</span>.  
> <span style="color:purple">with구문을 활용하여 acquire()과 release()를 한번에 관리가능하다.</span>
>
> **.locked()**
> * 스레드가 잠겨있으면 True반환.

락을 사용하는데 A함수와 B함수를 사용하고 A함수가 B함수를 재사용하는 재귀형식의 스레드활용시에는 acquire의 사용에 있어 오류를 발생할 수 있는데 이때 사용하는것이 RLock이다.

> **class threading.RLock()**
> * 스레드의 락 기능을 선언하는 클래스
>
> **.acquire(blocking=True, timeout=- 1)**
> * 락 기능이 작동중인지 작동중이지 않은지 수 있는 메서드.
> * **blocking** 매개변수가 True이면 락을 작동(코드 멈춤)하고 True를 반환하고 재사용시에 1을 반환한다. False이면 락을 작동시키지 않고(코드 진행) 추후에 True/False를 반환합니다.(default: true)
>
> **.release()**
> * 스레드의 락을 해제하며 <span style="color:red">해제된 스레드에서 작동시 런타임 오류발생</span>.  
> <span style="color:purple">with구문을 활용하여 acquire()과 release()를 한번에 관리가능하다.</span>
>
> **.locked()**
> * 스레드가 잠겨있으면 True반환.

이외에도 많은 함수들이 존재하지만 주로 사용하는 함수만 정리했으며 추가적인 자료는 아래를 참고한다.  
[원문](https://docs.python.org/ko/3/library/threading.html)

{% highlight python %}
from threading import Thread

def subthread():
  <output>

worker = Thread(target=subthread) # worker에 서브쓰레드 할당
worker.daemon = True # 메인쓰레드가 종료될때 sub도 종료됨(선택)
worker.start() # worker 실행
worker.join() # worker가 끝날때까지 대기(선택)

<main program>
{% endhighlight %}

---

## **multiprocessing**
---
프로세스를 늘려서 다른 코드들을 동시에 작동시켜주는 라이브러리  
multiprocessing의 경우 threading보다 더 다양한 클래스와 메서드들을 가지고 있다.

> **class multiprocessing.Pool(processes=None)** \***
> * 멀티 프로세스중 초기 지정한 프로세스수를 활용하는 클래스선언
> * **processes** 매개변수는 멀티프로세스에서 사용할 프로세스의 갯수를 나타내며 os.cpu_count()를 활용하면 나내 컴퓨터의 최대 프로세스수를 알 수있다. <span style="color:red">최대치를 넘는 프로세스는 오류를 유발할 수 있다.</span>
{% highlight python %}
def subprocess(<input>):
  <output>

if __name__ == '__main__':
  with Pool(5) as p:
    print(p.map(subprocess, <input>))
{% endhighlight %}

> **class multiprocessing.Process()** \***
> * 멀티 프로세스중 스레드와 유사한 작동방식을 가지며 각각의 프로세스를 관리하는 클래스선언  
> [참조](/study/pythonModule/1_threading&multiprocessing#threading)
{% highlight python %}
import multiprocessing as mp

def subprocess():
  <output>

if __name__ == "__main__":
  worker = mp.Process(target=subprocess, args=(...)) #  worker에 서브프로세스 할당
  worker.daemon = True # 메인쓰레드가 종료될때 sub도 종료됨(선택)
  worker.start() # worker 실행
  mp.current_process() # PID값을 반환해줌(선택)
  worker.is_alive() # PID값을 반환해줌(선택)
  worker.terminate() # 강제종료(선택)
  worker.join() # worker가 끝날때까지 대기(선택)
	
  <main program>
{% endhighlight %}

> **class multiprocessing.Queue(maxsize=0)** \***
> * 멀티 프로세스중 프로세스수간 FIFO 데이터 전송을 위한 클래스선언
> * **maxsize** 매개변수는 큐의 최대사이즈를 입력받으며 0은 제한없음을 의미한다. 
> 
> **.get()** \***
> * 큐에 있는 값을 하나 받아온다.  
>
> **.put()** \***
> * 큐에 값을 하나 넣는다.

> **class multiprocessing.Pipe(duplex=None) return(conn1, conn2)** \***
> * 멀티 프로세스중 프로세스수간 한쌍으로 데이터 전송을 위한 클래스선언
> * **duplex** 매개변수는 True일 경우 양방향 통신 False일 경우 단방향 통신(conn1: reciver, conn2: sender)으로 활용된다.  
>
> **conn.send()** \***
> * 파이프에 값을 넣는다.  
>
> **conn.recv()** \***
> * 파이프에서 값을 받아온다.


> **class multiprocessing.Lock()** \***
> * 락을 관리하는 멀티 프로세스중 스레드 락과 유사한 작동방식을 가지며 각각의 프로세스를 관리하는 클래스선언  
> [참조](/study/pythonModule/1_threading&multiprocessing#threading)

> **class multiprocessing.Manager()** \***
> * 멀티 프로세스의 자원을 안전하게 관리하기 위한 클래스선언
> * 다음과 같은 지원을 한다.(더 있음)
>   * .list()  
>   * .dict()  
>   * .Lock()  
>   * .RLcok()  
>   * .Array()  

이외에도 많은 함수들이 존재하지만 주로 사용하는 함수만 정리했으며 추가적인 자료는 아래를 참고한다.  
[원문](https://docs.python.org/ko/3/library/multiprocessing.html)
