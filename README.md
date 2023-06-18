DP-BETA2-HYUKLEE
------
* DRAGONPILOT의 BETA2브랜치를 일부 수정한 버전입니다.
* 넓은 한국어 지원
* 일부 값 수정

아래는 OPENPILOT의 README.md입니다.
-------

제한사항
------
* CAN-FD 차량은 작동하지 않습니다: EON/C2의 라이브러리가 오래되어 red panda 펌웨어를 빌드할 수 없기 때문입니다.
* Body는 작동하지 않습니다: 다시 말하지만, EON/C2의 라이브러리가 해당 펌웨어를 빌드할 수 없기 때문입니다.
* AI 모델은 0.8.16 버전을 유지합니다: tinygrad/pyopencl을 EON/C2에 이식하는 것은 너무 많은 노력이 들기 때문에 여전히 해결책을 조사 중입니다.
* NOO (Navigation On Openpilot)은 작동하지 않습니다: NOO는 새로운 주행 모델이 네비게이션 모델과 함께 작동하도록 요구하기 때문에 마지막 문제를 해결할 때까지 작동하지 않습니다.
* Logger는 작동하지 않습니다: 0.8.16 주행 모델을 거의 최대 성능으로 실행하고 있으며, Logger는 성능 및 열 문제를 일으킬 수 있습니다.

**요약하면, 이 버전은 openpilot 0.8.16 버전에 openpilot master 브랜치의 최신 차량 모델 지원이 추가된 것으로 생각하시면 됩니다.**

**빌드가 매우 난잡합니다. 포팅/로깅 목적으로는 [openpilot mastertwo 브랜치](https://github.com/commaai/openpilot/tree/commatwo_master)를 사용하는 것을 권장합니다.**

![](https://i.imgur.com/b0ZyIx5.jpg)

목차
=======================

* [openpilot이란 무엇인가요?](#openpilot이란-무엇인가요)
* [차량에서 실행하기](#차량에서-실행하기)
* [PC에서 실행하기](#pc에서-실행하기)
* [커뮤니티 및 기여](#커뮤니티-및-기여)
* [사용자 데이터 및 comma 계정](#사용자-데이터-및-comma-계정)
* [안전성과 테스트](#안전성과-테스트)
* [디렉토리 구조](#디렉토리-구조)
* [라이선스](#라이선스)

---

openpilot이란 무엇인가요?
------

[openpilot](http://github.com/commaai/openpilot)은 오픈 소스 운전자 지원 시스템입니다.

 현재 openpilot은 적응형 크루즈 컨트롤(ACC), 자동 차선 중앙 맞춤(ALC), 전방 충돌 경고(FCW), 차선 이탈 경고(LDW) 기능을 수행하며, 점점 더 많은 [지원되는 차량 제조사, 모델 및 모델 년도](docs/CARS.md)를 대상으로 합니다. 또한 openpilot이 작동 중일 때, 카메라 기반의 운전자 모니터링(DM) 기능을 통해 졸음 운전 및 주의력이 흐트러진 운전자에게 경고합니다. [차량 통합](docs/INTEGRATION.md) 및 [제한사항](docs/LIMITATIONS.md)에 대해 자세히 알아보세요.

<table>
  <tr>
    <td><a href="https://youtu.be/NmBfgOanCyk" title="Greer Viau의 비디오"><img src="https://i.imgur.com/1w8c6d2.jpg"></a></td>
    <td><a href="https://youtu.be/VHKyqZ7t8Gw" title="Logan LeGrand의 비디오"><img src="https://i.imgur.com/LnBucik.jpg"></a></td>
    <td><a href="https://youtu.be/VxiR4iyBruo" title="Charlie Kim의 비디오"><img src="https://i.imgur.com/4Qoy48c.jpg"></a></td>
    <td><a href="https://youtu.be/-IkImTe1NYE" title="Aragon의 비디오"><img src="https://i.imgur.com/04VNzPf.jpg"></a></td>
  </tr>
  <tr>
    <td><a href="https://youtu.be/iIUICQkdwFQ" title="Logan LeGrand의 비디오"><img src="https://i.imgur.com/b1LHQTy.jpg"></a></td>
    <td><a href="https://youtu.be/XOsa0FsVIsg" title="PinoyDrives의 비디오"><img src="https://i.imgur.com/6FG0Bd8.jpg"></a></td>
    <td><a href="https://youtu.be/bCwcJ98R_Xw" title="JS의 비디오"><img src="https://i.imgur.com/zO18CbW.jpg"></a></td>
    <td><a href="https://youtu.be/BQ0tF3MTyyc" title="Tsai-Fi의 비디오"><img src="https://i.imgur.com/eZzelq3.jpg"></a></td>
  </tr>
</table>


차량에서 실행하기
------

openpilot을 차량에서 사용하려면 네 가지가 필요합니다.
* 이 소프트웨어를 실행할 수 있는 지원되는 장치: [comma three](https://comma.ai/shop/products/three).
* 이 소프트웨어. comma three의 설치 절차에서 사용자는 사용자 정의 소프트웨어의 URL을 입력

할 수 있습니다. openpilot.comma.ai라는 URL을 입력하면 openpilot의 출시 버전이 설치됩니다. openpilot master를 설치하려면 installer.comma.ai/commaai/master를 사용할 수 있으며, commaai를 다른 GitHub 사용자 이름으로 바꾸면 포크를 설치할 수 있습니다.
* [200개 이상의 지원되는 차량](docs/CARS.md) 중 하나. Honda, Toyota, Hyundai, Nissan, Kia, Chrysler, Lexus, Acura, Audi, VW 등을 지원합니다. 차량이 지원되지 않지만 적응형 크루즈 컨트롤과 차선 유지 보조 시스템이 있는 경우 openpilot을 실행할 수 있습니다.
* [차량 연결용 차량 하네스](https://comma.ai/shop/products/car-harness).

[comma의 설치 가이드](https://comma.ai/setup)에서 장치를 차량에 설치하는 방법에 대한 자세한 지침을 찾을 수 있습니다.

PC에서 실행하기
------

모든 openpilot 서비스는 특별한 하드웨어나 차량 없이 PC에서 일반적으로 실행할 수 있습니다. 또한 openpilot을 기록된 또는 시뮬레이션 데이터로 실행하여 openpilot을 개발하거나 실험할 수 있습니다.

openpilot의 도구를 사용하여 로그를 그래프로 그리고 주행을 다시 재생하고 고해상도 카메라 스트림을 시청할 수 있습니다. 자세한 내용은 [도구 README](tools/README.md)를 참조하세요.

또한 openpilot을 시뮬레이션 [CARLA 시뮬레이터](tools/sim/README.md)에서 실행할 수 있습니다. 이를 통해 openpilot이 Ubuntu 기기에서 가상 차량을 주행할 수 있습니다. 전체 설정은 몇 분 정도 걸리지만 좋은 GPU가 필요합니다.

PC에서 openpilot을 실행하려면 [웹캠](https://github.com/commaai/openpilot/tree/master/tools/webcam), [블랙 판다](https://comma.ai/shop/products/panda) 및 [하네스](https://comma.ai/shop/products/car-harness)를 연결해야 차량을 제어할 수 있습니다.

커뮤니티 및 기여
------

openpilot은 [comma](https://comma.ai/) 및 사용자들에 의해 개발되었습니다. 우리는 [GitHub](http://github.com/commaai/openpilot)에서의 풀 리퀘스트와 이슈를 환영합니다. 버그 수정과 새로운 차량 포트는 권장됩니다. [기여 문서](docs/CONTRIBUTING.md)를 확인하세요.

openpilot 개발 관련 문서는 [docs.comma.ai](https://docs.comma

.ai)에서 찾을 수 있습니다. openpilot 실행에 관련된 정보(FAQ, 지문, 문제 해결, 사용자 정의 포크, 커뮤니티 하드웨어)는 [위키](https://github.com/commaai/openpilot/wiki)에 작성되어야 합니다.

자동차를 지원하려면 [브랜드](https://blog.comma.ai/how-to-write-a-car-port-for-openpilot/) 및 [모델](https://blog.comma.ai/openpilot-port-guide-for-toyota-models/) 포트를 따르는 가이드를 따를 수 있습니다. 일반적으로 적응형 크루즈 컨트롤과 차선 유지 보조 시스템이 있는 차량이 적합합니다. [Discord에 참여](https://discord.comma.ai)하여 차량 포트에 대해 논의할 수 있습니다. 대부분의 차량 제조사에는 전용 채널이 있습니다.

openpilot 작업에 대해 지급받으려면 [comma에서 채용 공고](https://comma.ai/jobs/)를 확인하세요.

그리고 [Twitter에서 팔로우](https://twitter.com/comma_ai)하세요.

사용자 데이터 및 comma 계정
------

기본적으로 openpilot은 주행 데이터를 우리 서버에 업로드합니다. 또한 [comma connect](https://connect.comma.ai/)를 통해 데이터에 액세스할 수 있습니다. 우리는 데이터를 사용하여 더 나은 모델을 훈련시키고 openpilot을 개선합니다.

openpilot은 오픈 소스 소프트웨어이며, 사용자는 데이터 수집을 원하지 않으면 비활성화할 수 있습니다.

openpilot은 도로 정면 카메라, CAN, GPS, IMU, 자력계, 열 센서, 충돌 및 운영 체제 로그를 기록합니다.
운전자 정면 카메라는 설정에서 명시적으로 동의하지 않는 한 기록되지 않습니다. 마이크는 기록되지 않습니다.

openpilot 사용으로 인해 사용자는 comma의 개인 정보 보호 정책에 동의합니다(https://comma.ai/privacy). 사용자 데이터의 사용에 대한 동의로 인해 데이터의 comma에 대한 무기한, 영구, 전 세계적인 사용권이 부여됩니다.

안전성과 테스트
----

* openpilot은 ISO26262 가이드라인을 준수합니다. 자세한 내용은 [SAFETY.md](docs/SAFETY.md)를 참조하세요.
* openpilot은 모든 커밋에서 실행되는 소프트웨어 인 더 루프 [테스트](.github/workflows/selfdrive_tests.yaml)를 수행합니다.
* 안전 모델을 적용하는

 코드는 panda에 있으며 C로 작성되었습니다. 자세한 내용은 [code rigor](https://github.com/commaai/panda#code-rigor)를 참조하세요.
* panda에는 소프트웨어 인 더 루프 [안전 테스트](https://github.com/commaai/panda/tree/master/tests/safety)가 있습니다.
* 내부적으로는 하드웨어 인 더 루프 Jenkins 테스트 스위트가 구축되어 다양한 프로세스를 빌드하고 단위 테스트를 수행합니다.
* panda에는 추가적인 하드웨어 인 더 루프 [테스트](https://github.com/commaai/panda/blob/master/Jenkinsfile)가 있습니다.
* 우리는 테스트 플레이트에 10대의 comma 장치가 연속적으로 경로를 재생하는 테스트 클로젯을 운영합니다.

디렉토리 구조
------
    .
    ├── cereal              # 모든 로그를 위한 메시징 사양 및 라이브러리
    ├── common              # 개발된 라이브러리 기능
    ├── docs                # 문서
    ├── opendbc             # 차량에서 데이터 해석을 위한 파일
    ├── panda               # CAN 통신에 사용되는 코드
    ├── third_party         # 외부 라이브러리
    ├── pyextra             # 추가 Python 패키지
    └── system              # 일반적인 서비스
        ├── camerad         # 카메라 센서에서 이미지 캡처를 위한 드라이버
        ├── clocksd         # 현재 시간을 방송
        ├── hardware        # 하드웨어 추상화 클래스
        ├── logcatd         # 시스템디 저널 서비스
        ├── loggerd         # 차량 데이터의 로거 및 업로더
        ├── proclogd        # /proc에서 정보를 기록하는 로거
        ├── sensord         # IMU 인터페이스 코드
        └── ubloxd          # u-blox GNSS 모듈 인터페이스 코드
    └── selfdrive           # 자동차 운전에 필요한 코드
        ├── assets          # UI에 대한 폰트, 이미지 및 사운드
        ├── athena          # 앱과의 통신을 허용
        ├── boardd          # 보드와 통신하기 위한 데몬
        ├── car             # 상태를 읽고 액추에이터를 제어하는 차량 특정 코드
        ├── controls        # 계획 및 제어
        ├── debug           # 디버그 및 차량 포트 도구
        ├── locationd       # 정밀한 로컬라이제이션 및 차량 매개변수 추정
        ├── manager         # 필요에 따라 모든 다른 데몬을 시작

/정지하는 데몬
        ├── modeld          # 주행 및 모니터링 모델 실행기
        ├── monitoring      # 운전자 주의 확인을 위한 데몬
        ├── navd            # 길 안내
        ├── test            # 유닛 테스트, 시스템 테스트 및 차량 시뮬레이터
        └── ui              # 사용자 인터페이스

라이선스
------

openpilot은 MIT 라이선스로 배포됩니다. 일부 소프트웨어는 특정한 라이선스에 따라 배포됩니다.

이 소프트웨어 사용자는 이 소프트웨어의 사용으로 인해 발생하는 모든 주장, 요구, 조치, 소송, 손해, 책임, 부담, 손실, 합의, 판결, 비용 및 비용(변호사 수임료 및 비용 포함)으로부터 Comma.ai, Inc. 및 그 이사, 임원, 직원, 대리인, 주주, 계약자 및 고객을 면책시킬 것입니다.

**이것은 연구 목적으로만 사용되는 알파 품질 소프트웨어입니다. 제품이 아닙니다.
사용자는 관련 법률과 규정을 준수해야 합니다.
어떠한 명시적이거나 묵시적인 보증도 없습니다.**


본 README는 ChatGPT를 통해 번역되었습니다.
