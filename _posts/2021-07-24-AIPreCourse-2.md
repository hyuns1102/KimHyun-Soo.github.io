---
title: "[네이버 부스트 캠프] AI-Tech - week5"
categories: AI
tags: python
published: true
---

## week5

---

### Docker

모든 컴퓨터에서의 세팅을 동일하게 하기 위해서 도커를 쓴다 !

- 도커는 컨테이너 기반의 가상화 시스템  
  현실의 존재하지 않는 것을 있는 것처럼 만들어주는 시스템  
  물리적인 서버를 쪼개서 여러 사람들에게 줄 수 있다. (클라우드 서비스)

- 운영체제에 도커를 설치해서 어느 컴퓨터에서 돌아갈 수 있도록 한다.  
  새로운 컨테이너를 만들어서 그 위에 파이토치 실습을 이용할 수 있다.

- Docker Toolbox 가 더이상 업데이트가 없으니 Desktop for Docker를 이용하자. Desktop for Docker는 다 똑같은 데 UX 디자인을 제공해줘서 더 편하게 만들어주려고 하는 것 같다.

- 가이드 라인이랑 많이 다르게 나와서 cmd 터미널을 통해 docker image를 다운 받아 컨테이너를 사용할 준비부터 다시 시작한다.  
  [도커가이드](https://github.com/deeplearningzerotoall/PyTorch/blob/master/docker_user_guide.md)를 참고해서 '도커 이미지 다운로드 받기' 부터 다시 시작하자.  
  Docker의 default machine with IP는 cmd-ipconfig를 통해 나의 로컬 호스트 ip를 이용하면 된다. (이것 때문에 조금 헤맸지만 어쨌든 완성!)

- 명령어
  container Id : pt
  container 접속 : dockers start pt  
  container 터미널 실행 : dockers attach pt
  container 종료 : exit
  jupyter 실행 (쉘로 만들어 놓음) : sh run_jupyter_docker.sh

### Pytorch

- Tensor Manipulation
  - 1차원 : 벡터, 2차원 : 행렬(Matrix), 3차원 : 텐서(Tensor)
    Tensor의 크기를 항상 생각하면서 구현하자.  
    2D Tensor _(Typical Simple Setting)_
    |t| = (batch size, dim)  
    주로, batch size : 64 X dim : 256 으로 이용된다.
    <br>
    3D Tensor _(Typical Computer Vision)_
    |t| = (batch size, width, height)  
    위의 순서대로 가로, 세로, 깊이를 뜻한다. (pdf 강의자료 필기를 같이 보자)
    <br>
    3D Tensor _(Typical Natural Language Processing)_
    |t| = (batch size, length, dim)  
    위의 순서대로 가로, 세로, 깊이를 뜻한다. (pdf 강의자료 필기를 같이 보자)
  - Numpy 와 유사하거나 더 나은 기능들이 있다.  
    numpy와 같이, 1d array, 2d array 기능이 동일,  
    Broadcasting 이용 시, 행렬의 차원이 맞지 않아도 자동으로 맞춰 계산한다는 점에서 조심해야 한다. 이외에도 다양한 기능 제공  
    numpy review -> jupyter notebook 실행해서 확인한다. (강의자료 확인)
