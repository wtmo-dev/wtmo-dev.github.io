---
title: "JAVA io"
tags:
    - JAVA
    - basic
date: "2024-04-08"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# input, output of JAVA
---
자바는 다양한 입출력 방식이 있습니다.

# console io
---
다음은 console을 활용한 기본적인 io입니다.

{% highlight java %}
System.out.println("text"); // text\n 출력
System.out.print("text"); // text 출력

import java.io.InputStream;

InputStream inputData = System.in; // console 입력 선언
byte[] a = new byte[10]; // 입력 size 설정
a = in.read(); // console 입력 받기(askii code)

import java.io.InputStreamReader;

InputStream in = System.in; // console 입력 선언
InputStreamReader reader = new InputStreamReader(in); // streaming 설정
char[] a = new char[3]; // 입력 size 설정
reader.read(a); // console 입력 받기

import java.io.BufferedReader;

InputStream in = System.in; // console 입력 선언
InputStreamReader reader = new InputStreamReader(in); // streaming 설정
BufferedReader br = new BufferedReader(reader); // 입력 size free 설정
String a = br.readLine(); // console 입력 받기

import java.util.Scanner;

Scanner sc = new Scanner(System.in);
System.out.println(sc.next());
{% endhighlight %}

# file io
---
다음은 file을 활용한 io의 예시입니다. 다양한 방법이 있으며 필요한 방법을 활용하면 됩니다.

{% highlight java %}
import java.io.FileOutputStream;

FileOutputStream output = new FileOutputStream("c:/out.txt");
output.close();

import java.io.FileOutputStream;

String data = "Hello world.\r\n";
output.write(data.getBytes());
output.close();

import java.io.FileWriter;

FileWriter fw = new FileWriter("c:/out.txt");
String data = "Hello world.\r\n";
fw.write(data);
fw.close();

FileWriter fw = new FileWriter("c:/out.txt", true); // 파일을 추가 모드로 연다.
String data = "Hello world.\r\n";
fw.write(data);
fw.close();

import java.io.PrintWriter;

PrintWriter pw = new PrintWriter("c:/out.txt");
String data = "Hello world.\r\n";
pw.println(data);
pw.close();

PrintWriter pw = new PrintWriter(new FileWriter("c:/out.txt", true));
String data = "Hello world.\r\n";
pw.println(data);
pw.close();
{% endhighlight %}















{% highlight java %}
{% endhighlight %}

