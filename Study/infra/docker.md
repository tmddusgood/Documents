---
layout: reference
title: 14회차 Docker로 배포해보기
date: '2018-01-11T00:00:00.000Z'
categories: nodejs
summary: Node.js 강의 후기
description: 도커 컨테이너에 대해 알아보자
---

# DOCKER

![https://lsjsj92.tistory.com/395](../../.gitbook/assets/img1.daumcdn%20%281%29.png)

## 컨테이너란 무엇인가

모듈화 되고 격리된 컴퓨팅 공간, 컴퓨팅 환경을 의미하며, 낮은 시스템 환경 의존성을 가진다.

### 컨테이너 특징

#### 격리\(isolation\)

* 프로세스 자체를 격리하여 실행 안전성이 보장된다.
* 상호 간섭을 없앨 수 있다.

#### 독립\(independent\)

* 게스트OS\(Guest OS\)가 Container에 포함되지 않기 때문에, 구동 방법이 간단하다.
* 게스트OS로 발생하는 성능 문제도 줄일 수 있다.

#### 스케일링\(scaling\)

* 수요에 맞춰 스케일링을 간단히 할수 있다.
* 비즈니스가 요구하는 새로운 기능을 간단히 적용할 수 있다.
* 반대로 이슈 발생 시 이전 버전으로 롤백도 신속히 가능하다

## 컨테이너 vs Virtual Machine

![](../../.gitbook/assets/1%20%289%29.png)

### Virtual Machine

기존 가상화에서는 각각의 가상화에 게스트 OS 가 들어가고 이를 중간 관리하는 하이퍼바이저\(Hypervisor\)가 존재한다. 이는 각 가상머신에 완벽한 격리를 보장하지만, 가상머신의 용량 증가, 게스트OS의 자원필요하다. 이를 ‘하드웨어 수준의 가상화’ 라고 한다. 실행중인 가상머신들이 모두 하이퍼바이저를 통해 디스크 읽기/쓰기 작업을 하기 때문에 병목현상이 발생

### Container 방식

하이퍼바이저, 게스트OS를 없애고 애플리케이션의 실행하는데 필요한 것들만 가상화 하기 때문에 용량이 적다. 이를 ‘운영체제 수준의 가상화’ 라고 한다.

### 경량화된 컨테이너가 얻는 이점

![](../../.gitbook/assets/2%20%285%29.png)

#### 더 많은 응용프로그램 실행이 가능하다.

기존의 VM 방식은 게스트 OS까지 가상머신에 포함시켰기 때문에, 동시에 여러개의 가상머신을 실행하는데 한계가 존재하였다. 하지만 Container방식은 게스트 OS와 하이퍼바이저를 제외하므로써 실행시 오버헤드를 줄이고, 이는 동시에 여러개의 서비스를 동작이 가능하게 하였다.

#### 구동방식이 간단하다.

Container는 실행시 필요한 모든 라이브러리, 바이너리 파일들이 패키지화 되어 있어서, 실행하는 것으로 구동할 수 있지만 VM 방식은 새로운 VM을 실행하고 해당 VM에서 실행자원을 할당한 다음 게스트OS를 부팅한 후 어플리케이션을 실행해야 한다.

## 도커란 무엇인가

### Container 기반의 가상화 소프트웨어 중 하나이다.

리눅스의 응용 프로그램들을 소프트웨어 컨테이너 안에 배치시키는 일을 자동화 하는 오픈 소스 프로젝트‌이다.

기존 LXC\(LinuX Container\) 기술에 이식성을 향상시키고 데이터와 코드의 분산된 관리가 가능해졌다.

### Image 기반의 Container

이미지 : Container 실행에 필요한 파일, 설정 값들을 미리 정의

#### 같은 이미지에서 다수의 Container 생성 가능하다

* 같은 이미지에서 다수의 컨테이너가 실행 가능하며, 컨테이너의 상태가 바뀌거나 삭제 되더라도 이미지는 그대로 남아있게 된다.
* 추가되거나 변경된 값은 컨테이너에 저장되고, 이미지의 원본은 보존된다.
* 컨테이너 이미지 도구를 통해서 이미지를 만들 수 있고, 이 이미지를 배포하여 실행한다.

## 컨테이너 오케스트레이션은?

![](../../.gitbook/assets/1%20%2815%29%20%281%29%20%281%29.png)

### Container의 관리 도구의 필요성

* Container 경량화로 관리, 운영의 어려움 증가되었다.
* 생성, 소멸, 시작과 중단 시점 제어, 스케줄링, 로드 밸런싱, 클러스터링 과 같은 기능이 필요하였다.

### Container Orchestration 제공기능

#### Service discovery

서비스 탐색 기능으로 기본적으로는 클라우드 환경에서 컨테이너의 생성과 배치 이동 여부를 알 수 없기에 IP, Port 정보 업데이트 및 관리를 통해 서비스를 지원한다.

#### Scaling

* Load Balancing : 생성된 컨테이너의 컴퓨팅 자원 사용량의 설정 및 자동 배분이 가능하다
* Scheduling : 늘어난 컨테이너를 적합한 서버에 나누어 배포하고, 서버가 다운될 경우 실행 중이던 컨테이너를 다른 서버에서 구동 시킬 수 있다.

#### Clustering

여러 개의 서버를 묶어 하나의 서버처럼 사용할 수 있도록 지원하거나, 가상 네트워크를 이용하여 산재된 서버를 연결 시켜준다.

#### Logging/Monitoring

여러 개의 서버를 동시에 관리할 경우 한 곳에서 서버 상태를 모니터링 하고 로그 관리를 할 수 있도록 기능을 제공한다.

## 도커 오케스트레이션 비교

### Docker Swam

* Docker에서 출시하였다.
* Docker 컨테이너 용 Docker 고유 오케스트레이션이다.
* Docker native api 를 사용할 수 있다.
* 설치 또는 설정이 매우 간단하다.
* 약간 불안정 하고, 아직도 활발하게 릴리즈 중이다.

### K8S

* 구글에서 만든 오케스트레이션이다.
* 설정이 조금 복잡하나, yaml 파일을 활용하여 클러스터의 모든 서비스를 정의할 수 있다.
* 매우 안정적이고 스케줄링을 통한 배포 관리에 적합하다.

### Memos

* 소규모일 경우 설치와 설정이 간편하지만 규모가 커질 수록 산술 연산이 복잡하다.
* JSON 기반으로 하여 다양한 설정 파일을 정의할 수 있다.
* 매우 안정적이어서 큰 규모의 클러스터에도 적합하다.

## 참고

* [https://lsjsj92.tistory.com/395](https://lsjsj92.tistory.com/395)
* [https://dev.to/adnanrahic/containers-vs-serverless-from-a-devops-standpoint-e4n](https://dev.to/adnanrahic/containers-vs-serverless-from-a-devops-standpoint-e4n)
* [https://www.edureka.co/blog/what-is-docker-container](https://www.edureka.co/blog/what-is-docker-container)
* [https://medium.com/@chrisjune\_13837/infra-kubernetes-vs-swarm-vs-mesos-비교-b04b2cd032ab](https://medium.com/@chrisjune_13837/infra-kubernetes-vs-swarm-vs-mesos-%EB%B9%84%EA%B5%90-b04b2cd032ab)

