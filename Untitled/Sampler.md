https://youtu.be/VnfD2ZB1Y8k?si=LdZFu229Rg7DqvWZ

PM(Probabilisic Models)
	확률 분포를 기바능로 샘플링 진행
	(DDPM, DPM, DDIM, PLMS)
Numerical Approach Methods
	수치적으로 계산한 값(미분방정식)을 기반으로 샘플링을 진행
	(Euler, Heun, LMS)
+ 숫자 2
	예측 및 보정 2단계(second order) 계산을 진행하여 정확도를 더 높인 모델
+ s
	정확도를 높이는 계산을 한 번에(single step) 계산하는 모델
+ m
	정확도를 높이는 계산을 여러차례(multi step)에 걸쳐 계산하는 모델
- a(ancestral)
	이전 스텝의 변수를 기준으로 매 스텝 랜덤노이즈를 새로 추가
- SDE(Stochastic Differential Equation)
	매 스텝 랜덤노이즈 추가, 적은 스텝에 고품질 정교한 이미지 생성 가능, 대신 느림
![[Pasted image 20240828045110.png]]