---
title: "basic shell command"
tags:
    - shell
date: "2024-02-14"
thumbnail: "/assets/img/thumbnail/logo.jpg"
---

# setting
---
아래의 작업은 powershell에서 동작되며 관리자권한을 요구합니다.

{% highlight shell %}
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart # window용 linux 활성화

dism /Online /Enable-Feature /featurename:VirtualMachinePlatform /all /norestart # vertual machine 활성화
{% endhighlight %}

* default 다운 가능한 버전 목록
{% highlight shell %}
wsl --list --online # 다운로드 가능한 버전 목록
{% endhighlight %}

* 이전 버전 다운로드 목록
[download list](https://learn.microsoft.com/en-us/windows/wsl/install-manual#downloading-distributions)

{% highlight shell %}
Invoke-WebRequest -Uri https://aka.ms/wslubuntu2004 -OutFile Ubuntu.appx -UseBasicParsing # 이전 버전 다운받는 방법

Rename-Item .\Ubuntu.appx .\Ubuntu.zip
Expand-Archive .\Ubuntu.zip .\Ubuntu

Add-AppxPackage .\app_name.appx # 이전 버전 다운후 세팅
{% endhighlight %}

## setting(step.2)
---

{% highlight shell %}
wsl -l -v # 다운로드된 wsl의 리스트와 버전을 확인

wsl --set-default-version <Version> # wsl version 세팅{1 or 2}

wsl --install -d <os-name> # os 설치

wsl --set-default <os-name> # default os 설정
{% endhighlight %}

## additional
---
wsl상에서 python에서 pip 없을때 설치법

{% highlight shell %}
sudo apt install python3-pip

curl https://pyenv.run | bash # pyenv 설치
{% endhighlight %}

파이썬 실행중 _ctype error가 발생 될때 해결법

{% highlight shell %}
sudo apt-get update
sudo apt-get install -y libffi-dev
pyenv uninstall 3.8.0
pyenv install -v 3.8.0

source $HOME/.bashrc
{% endhighlight %}

## pyenv configs
{% highlight shell %}
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"

if command -v pyenv 1>/dev/null 2>&1; then
  eval "$(pyenv init -)"
fi
{% endhighlight %}
또는
{% highlight shell %}
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
{% endhighlight %}

# remove setting
---
삭제 방법은 다음과 같습니다.

{% highlight shell %}
dism.exe /online /disable-feature /featurename:Microsoft-Windows-Subsystem-Linux /remove /norestart # window용 linux 비활성화

dism /Online /Disable-Feature /FeatureName:VirtualMachinePlatform /Remove /norestart # vertual machine 비활성화

wsl -l -v # 다운로드된 wsl의 리스트와 버전을 확인

wsl --unregister <os-name> # 설치된 wsl os를 제거
{% endhighlight %}

이후 설치한 os를 microsoft 앱에서 삭제하면 됩니다.