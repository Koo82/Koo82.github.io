---
title: "Jupyter notebook virtual environment kernel add"
---
Conda 가상환경 생성 및 쥬퍼티 노트북에 추가
(Conda Virtual Env. generation and add it to jupyter notebook)


* Conda 가상환경 생성 및 제거하기

1. 가상환경 생성  
```
conda create -n <가상환경이름> <설치하고 싶은 라이브러리> # conda create -n torch python==3.8
```
2. 가상환경 제거  
```
conda remove -n <가상환경이름> --all # conda remove -n torch --all
```


* 쥬피터 노트북에 가상 환경 추가하는 방법

1. 가상환경 활성화
```
source activate [Virtual Env name]
```
2. ipykernel 설치
```
pip install ipykernel
```
3. jupyter notebook에 등록
```
python -m ipykernel install --user --name [Virtual Env name] --display-name "[displayKernelName]"
```
