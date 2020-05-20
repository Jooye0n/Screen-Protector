# Screen-Protector
1. 목표
Win32에서 OpenVG를 이용하여 이미지를 움직인다.

2. 요구 사항
다음 사항을 모두 만족하는 응용 프로그램을 작성한다. Window에 우주 배경과 잔상이 있는 혜성 이미지가 그려진다. 이 혜성은 Window에서 1초에 30번씩 대각선으로 움직인다. Window 경계에 부딪치 면 적절한 방향으로 튕기고 잔상의 방향도 바뀌어야 한다. 초기 Window의 크기는 800 x 300이고 ‘혜성의 위치’는 (400, 200)이며 ‘움직이는 방향’은 오른쪽 아래이다. 프레임당 x 방향으로 5만큼, y 방향으로 5만큼 이동해야 한다.

3. 과정
OpenVG를 사용하기 위해 필요한 코드를 추가한다. 필요한 헤더 파일을 include하고 전역 변수를 선언한다. WndProc 함수에서 WM_CREATE case를 추가하고 EGL 초기화를 수행한다. EGL은 디바이스와 OpenVG를 연결해주는 역할을 한다. 우주 이미지와 혜성 이미지를 OpenVG를 이용하여 그린다. WndProc 함수의 WM_PAINT case에서 그리는 것이 아니라 timerProc 함수에서 직접 그린다. 전역 변수로 ‘우주 배경 이미지’와 ‘방향별 혜성 이미지’들을 저장할 변수들을 선 언한다. WndProc 함수의 WM_CREATE case에서 EGL 초기화 후에, ‘우주 배경 이미지’와 ‘방향별 혜성 이미지’들을 읽어 위의 변수들에 저장한다. VG_MATRIX_MODE를 VG_MATRIX_IMAGE_USER_TO_SURFACE로 지정한다. OpenVG에서 Transformation은 행렬로 계산된다. 그리기 전에, 현재 변환 행렬을 항등 행렬로 설정한다. 즉, 이전 프레임에서 설정 되어 있던 변환 행렬을 초기화 한다. ‘혜성의 위치’만큼 변환 행렬을 평행 이동시키고, 해당 위치에서 방향에 따른 혜 성 이미지를 출력한다. 혜성의 중심과 Window의 경계가 충돌 했을 때, 혜성의 ‘움직이는 방향’을 적절히 변 경한다.

4. 결과
![image](https://user-images.githubusercontent.com/38244836/82404121-6a2a8000-9a9b-11ea-8605-169e0c390d83.png)
(Right Down 방향으로 움직이고 있는 상태.)
