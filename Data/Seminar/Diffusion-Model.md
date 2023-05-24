---
title: Diffusion Model
description: 
published: true
date: 2023-05-24T06:45:16.540Z
tags: ai, deep-learning
editor: markdown
dateCreated: 2023-05-24T05:45:39.841Z
---

# Diffusion 모델?
- 스케치 -> 딥러닝 생성 모델 (Diffusion Model) -> AI 그림
- ex) Lensa AI
   - 사진 -> 일러스트 생성

## Denoising Diffusion Probabilistic Models - Paper
## 딥러닝 모델
1. 모델 구조 : 입/출력
2. 실행 방법 : 어떻게 출력 결과
3. 학습 데이터 : Label?
4. 학습 방법 : Model?

## 생성 모델 (unconditional)
- 학습 데이터의 분포를 따르는 다양한 새로운 데이터 생성
- 다양한 이미지를 만들기 위해서 랜덤 노이즈를 입력으로 사용함
- 생성 모델 구조
  - Standard Gaussian 에서 샘플 데이터 생성 (n 차원의 Random Nosie / Latent space)
  - 생성모델 종류
     - VAE : Auto Encoder
     - GAN : USE Discriminator (Real or Fake)
     - Diffusion : VAE와 동일한 방식
        - 여러단계를 거쳐 학습이 수행됨
        - 랜덤 노이즈의 차원이 입력 이미지와 동일한 dimension을 사용
  - Output = Sample

## 생성 모델의 평가 요소
- 고품질의 이미지 : VAE의 단점
- 빠른 생성 : Diffusion의 단점
- 다양성 : GAN의 단점

# VAE (Variational AutoEncoder)
- 원본 이미지를 복원하도록 모델 학습
- [3 x 256 x 256] -> [1 x 256 (Latent Space)] -> [3 x 256 x 256 (original)]
- Auto Encoder vs Variational AE
   - Encoder에 Distribution +
   - Gaussian Distribution
- VAE 학습 Loss
   - 이미지 복원 + 분포 매칭(제약 조건)
   - 스탠다드 가우시안이 되도록 제한하면서 이미지 제한 (좀 더 포괄적인 입력값)
   - ~N(0,1)

# VAE vs Diffusion
- Latent Space가 더 고차원
- Coarse-to-Fine 생성되면서 좀 더 고품질

# Diffusion Model
## Diffusion-Denoising 과정
- Repeat Denosing -> Image!
	- for ( Noisy Image(+ Time Step) -> Diffusion Model )
- <- = Diffusion 과정

### Diffusion
- n -> Standard Gausian

### Deniosing
- Standard Gausian -> n

## 표기법
$$
I_t, I_(t-1), ..., I_0
$$

### Diffusion Step
$$
I_t-1 -> I_t
$$

### Denoising Step
$$
I_t -> I_t-1
$$

- 모델은 더해진 노이즈를 예측하고, 빼기를 함으로써 다음 스탭을 예측한다.
- 즉, 더해진 노이즈를 예측하도록 학습한다.
$$
I_0 + \epsilon_t = I_t
$$

# 수식 깊게 이해하기