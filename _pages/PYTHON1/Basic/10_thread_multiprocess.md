---
title: "동시성과 병렬성"
tags:
    - python
    - basic
date: "2023-08-22"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# **thread & multiprocess**
---

## **thread**
---
하나의 프로세스가 하나의 스레드로 구성이 되는데 멀티 스레드를 구성 할 수있다. 멀티 스레딩은 **동시성 프로그래밍**으로 동시에 실행하는것처럼 보이게 한다.

{% highlight python %}
import threading

def subthread():
  <output>

worker = threading.Thread(target=subthread) # worker에 서브쓰레드 할당
worker.daemon = True # 메인쓰레드가 종료될때 sub도 종료됨(선택)
worker.start() # worker 실행
worker.join() # worker가 끝날때까지 대기(선택)

<main program>
{% endhighlight %}

## **multiprocess**
---
일반적으로 하나의 프로그램은 하나의 프로세스이지만 고도화된 프로그램과 같은 경우 멀티 프로세스를 사용할 수있다. 멀티 프로세싱은 **병렬성 프로그래밍**으로 작업이 동시에 실행된다.

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