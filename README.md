# AS5600 실습

## 📌 프로젝트 개요

이 프로젝트는 AS5600 자기 각도 센서의 **아날로그 출력 모드(OUTMODE_ANALOG_100)** 를 이용하여 회전각을 아날로그 전압으로 읽어들이는 실습입니다.  
AS5600 라이브러리에서 기본 제공되는 코드를 응용하여 작성하였고, 센서에서 출력되는 아날로그 값을 아두이노 UNO 보드로 받아 시리얼 모니터에 출력하며, I2C로 읽은 디지털 각도값과 비교할 수 있도록 구성했습니다.

최종적으로 5010 BLCD 모터와 simpleFOC 아두이노 쉴드를 활용해서 폐루프 PID제어를 하기 위한 가장 기초적인 실습입니다.


https://github.com/user-attachments/assets/e2465318-d916-4683-8962-e5015a295904


---

## 🔧 사용한 부품 및 장비

| 항목 | 설명 |
|------|------|
| Arduino UNO | 메인 마이크로컨트롤러 보드 |
| AS5600 | 자기 회전각 센서 (아날로그 출력 지원 모델) |
| 3D 프린터 출력 노브 | 센서 축에 장착하여 회전 테스트용 |

---

## 🖨️ 3D 프린팅
- 간단히 설계한 knob와 frame을 AS5600보드 위에 올려 사용하였습니다.
- 특히 frame의 경우, 상단 4개의 막대구조가 온전히 출력되기 위해 **Creality ender3 pro 모델 기준 10mm/s 속도로 설정**하여 출력 해야 했습니다.
- AS5600 모듈의 구조상, 아래 이미지의 방향대로 frame을 조립해야 온전히 사용할 수 있습니다.
- 해당 파일들은 /STL files 폴더에 포함되어 있습니다.

<img width="400" alt="knob and frame2" src="https://github.com/user-attachments/assets/84f04b14-d0b2-4f64-9444-f1211907799b" /> 
<img width="400" alt="knob and frame" src="https://github.com/user-attachments/assets/77b0af62-828c-450d-bcbc-55836e7a4b0a" />

- [Josselin Hefti / AS5600 f3d file](https://www.printables.com/model/1295862-as5600)
---

## 📁 코드 개요

- 사용한 코드는 [`Rob Tillaart/AS5600`](https://github.com/RobTillaart/AS5600) 라이브러리의 예제 중  
  `AS5600_outmode_analog_100.ino` 를 기반으로 작성되었으며, 일부 핀 설정과 출력 포맷을 변경하였습니다.

- 주요 기능:
  - I2C 통신을 통한 디지털 각도 읽기
  - OUT 핀에서 아날로그 출력 전압 읽기 (`analogRead`)
  - 방향 설정 핀(DIR) 설정
  - 아날로그 출력 모드 설정
 
- 해당 코드는 /src 폴더에 AS5600_Example.cpp 라는 이름으로 포함되어 있습니다.

---

## 🔌 회로 연결 (Arduino UNO 기준)

| AS5600 핀 | Arduino 핀 | 설명 |
|-----------|-------------|------|
| VCC       | 5V          | 전원 |
| GND       | GND         | 그라운드 |
| SDA       | A4          | I2C 데이터 |
| SCL       | A5          | I2C 클럭 |
| DIR       | D4          | 회전 방향 설정 |
| OUT       | A0          | 아날로그 출력 (전압) |

---

## 📝 참고 사항

- 아날로그 출력 기능은 **AS5600L** 모델에는 **지원되지 않으므로**, 반드시 **AS5600 (표준 버전)** 을 사용해야 합니다.


---

## 📚 관련 라이브러리

- [Rob Tillaart / AS5600 라이브러리](https://github.com/RobTillaart/AS5600)

---

## ✍️ 작성자

- Jaebin Ahn / 2025  
- 프로젝트용 3D 노브 모델링 및 출력, 회로 구성 및 실험
