---
layout: post
title: "Image recognition"
tags: [Machine Learning, Object Dection]
comments: true
---
## 이미지 인식 문제의 개요

**이미지 인식(image recognition)** 문제에서는, 기계로 하여금 주어진 이미지 상에 포함되어 있는 대상이 무엇인지, 또한 어느 위치에 있는지 등을 파악하도록 하는 것을 주된 목표.

**Classification** 문제에서는, 주어진 이미지 안에 어느 특정한 클래스에 해당하는 사물이 포함되어 있는지 여부를 분류하는 모델을 만드는 것을 주요 목표로 한다.

분류 모델은 주어진 이미지에 대하여 신뢰도 점수 결과물을 제출하며, 이에 기반하여 단일 사물 분류 문제에서는 정확도를, 복수 사물 분류 문제에서는 정밀도 및 재현율을 주요한 평가 척도로 사용한다. 정밀도 및 재현율에 대한 문턱값을 미리 정하여 최종 성능을 산출하는 대신, PASCAL VOC Challenge에서는 평균 정밀도를 채택하여 모든 가능한 재현율 값에 대한 평균적인 정밀도를 계산한다.



![Classification 문제](http://research.sualab.com/assets/images/image-recognition-overview-1/classification-model.svg)

<center>Classification 문제</center>

**Detection** 문제에서는, 다른 이미지 인식 대회에서는 'Image Localization'이라고 표현함. 주어진 이미지 안에 어느 특정한 클래스에 해당하는 사물이 어느 위치에 포함되어 있는지 바운딩 박스 형태로 검출하는 모델을 만드는 것을 목표로 한다.



![Detection](http://research.sualab.com/assets/images/image-recognition-overview-2/pascal-voc-detection-bbox-example.svg)

<center>Detection 문제에서의 바운딩 박스 예시</center>

검출 모델의 성능 측정을 위해, 모델이 예측한 바운딩 박스와 GT 바운딩 박스를 매칭하는 과정을 선행하는데, 이 때 IOU를 사용하여 둘 간에 얼마나 겹쳐지는지를 평가한다. 

**Segmentation** 문제에서는 주어진 이미지 안에 어느 특정한 클래스에 해당하는 사물이 (만약 있다면) 어느 위치에 포함되어 있는지 '픽셀 단위로' 분할하는 모델을 만드는 것을 목표로 한다. 

주어진 이미지 내 각 위치 상의 픽셀들을 하나씩 조사하면서, 현재 조사 대상인 픽셀이 특정한 클래스에 해당하는 사물의 일부인 경우, 해당 픽셀의 위치에 그 클래스를 나타내는 ‘값’을 표기하는 방식으로 예측 결과물을 생성한다. 만약 조사 대상 픽셀이 어느 클래스에도 해당하지 않는 경우, 이를 ‘*배경(background)*’ 클래스로 규정하여 예측 결과물의 해당 위치에 0을 표기합니다. 이렇게 생성된 결과물을 **마스크(mask)**라고도 부릅니다.



![Segmentation 예시](http://research.sualab.com/assets/images/image-recognition-overview-2/segmentation-result-to-values.svg)

<center>Segmentation 분할 결과 = 픽셀 단위 분류 결과</center>

##### 세부 문제 구분

- Semantic Segmentation

  분할 기본 단위를 클래스로 하여, 동일한 클래스에 해당하는 사물을 예측 마스크 상에 동일한 색상으로 표시.

- Instance Segmentation

  분할 기본 단위를 사물로 하여, 동일한 클래스에 해당해도 서로 다른 사물에 해당하면 다른 생각으로 표시.



![Segmentation 종류](http://research.sualab.com/assets/images/image-recognition-overview-2/segmentation-types.svg)

<center>Segmentation 종류: Semantic Segmentation, Instance Segmentation</center>

분할 모델은 클래스를 나타내는 값들로 구성되는 마스크를 제출하도록 디자인되며, IOU를 사용하여 예측 성능에 대한 측정이 이루어진다.
