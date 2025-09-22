<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "9a6b22a2eff0f499b66236be973b24ad",
  "translation_date": "2025-08-23T23:53:24+00:00",
  "source_file": "5-browser-extension/solution/translation/README.it.md",
  "language_code": "ko"
}
-->
# Carbon Trigger 브라우저 확장 프로그램: 시작하기 위한 코드

tmrow의 Signal CO2 API를 사용하여 전기 사용량을 모니터링하고, 자신의 지역에서 전기 사용량이 얼마나 많은지 브라우저에서 직접 알림을 받을 수 있는 브라우저 확장 프로그램을 만들어 보겠습니다. 이 맞춤형 확장 프로그램을 사용하면 이러한 정보를 바탕으로 자신의 활동을 평가하는 데 도움이 됩니다.

![확장 프로그램 화면](../../../../../5-browser-extension/extension-screenshot.png)

## 시작하기

[npm](https://npmjs.com)이 설치되어 있어야 합니다. 이 코드를 컴퓨터의 폴더에 다운로드하세요.

필요한 모든 패키지를 설치합니다:

```
npm install
```

webpack을 사용하여 확장 프로그램을 생성합니다:

```
npm run build
```

Edge에 설치하려면, 브라우저 오른쪽 상단의 "세 점" 메뉴를 사용하여 확장 프로그램 패널을 찾으세요. 아직 활성화되지 않았다면, 개발자 모드(왼쪽 하단)를 활성화하세요. "압축 해제된 로드"를 선택하여 새 확장 프로그램을 로드합니다. 프롬프트에서 "dist" 폴더를 열면 확장 프로그램이 로드됩니다. 사용하려면 CO2 Signal API의 API 키가 필요합니다([여기에서 이메일을 통해 얻을 수 있습니다](https://www.co2signal.com/) - 이 페이지의 상자에 이메일을 입력하세요) 그리고 [전기 지도](https://www.electricitymap.org/map)에 해당하는 [자신의 지역 코드](http://api.electricitymap.org/v3/zones)가 필요합니다 (예: 보스턴의 경우 "US-NEISO").

![설치](../../../../../5-browser-extension/install-on-edge.png)

API 키와 지역을 확장 프로그램 인터페이스에 입력하면, 브라우저 확장 프로그램 바의 색 점이 지역의 에너지 사용량을 반영하도록 변경됩니다. 또한 에너지 소비가 높은 활동 중 어떤 것이 적합한지에 대한 지침을 제공합니다. 이 "점" 시스템의 개념은 캘리포니아의 배출량을 위한 [Energy Lollipop 확장 프로그램](https://energylollipop.com/)에서 제공되었습니다.

**면책 조항**:  
이 문서는 AI 번역 서비스 [Co-op Translator](https://github.com/Azure/co-op-translator)를 사용하여 번역되었습니다. 정확성을 위해 최선을 다하고 있으나, 자동 번역에는 오류나 부정확성이 포함될 수 있습니다. 원본 문서의 원어 버전을 권위 있는 출처로 간주해야 합니다. 중요한 정보의 경우, 전문적인 인간 번역을 권장합니다. 이 번역 사용으로 인해 발생하는 오해나 잘못된 해석에 대해 당사는 책임을 지지 않습니다.