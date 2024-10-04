# **LM Studio에서 Phi-3 사용하기**

[LM Studio](https://lmstudio.ai)는 로컬 데스크톱 애플리케이션에서 SLM과 LLM을 호출할 수 있는 애플리케이션입니다. 사용자는 다양한 모델을 쉽게 사용할 수 있으며 NVIDIA/AMD GPU/Apple Silicon을 이용한 가속 컴퓨팅을 지원합니다. LM Studio를 통해 사용자는 Hugging Face 기반의 다양한 오픈 소스 LLM 및 SLM을 다운로드, 설치 및 실행하여 코딩 없이 로컬에서 모델 성능을 테스트할 수 있습니다.

## **1. 설치**

![LMStudio](../../../../translated_images/LMStudio.87422bdb03d330dc05137ba237dd0cb43f7964245b848a466ab1730de93bc4db.ko.png)

LM Studio의 웹사이트 [https://lmstudio.ai/](https://lmstudio.ai/)를 통해 Windows, Linux, macOS 중에서 설치를 선택할 수 있습니다.

## **2. LM Studio에서 Phi-3 다운로드**

LM Studio는 양자화된 gguf 형식의 오픈 소스 모델을 호출합니다. LM Studio 검색 UI에서 제공하는 플랫폼을 통해 직접 다운로드하거나, 직접 다운로드하여 관련 디렉토리에 지정할 수 있습니다.

***LM Studio 검색에서 Phi3를 검색하고 Phi-3 gguf 모델을 다운로드합니다***

![LMStudioSearch](../../../../translated_images/LMStudio_Search.1e577e0f69f336fc26e56653eeec2a20b90c3895cc4aa2ff05b6ec51059f12fd.ko.png)

***LM Studio를 통해 다운로드한 모델을 관리합니다***

![LMStudioLocal](../../../../translated_images/LMStudio_Local.55f9d6f61eb27f0f37fc4833599aa43fa45a66dfc20444ba1419a922b60b5005.ko.png)

## **3. LM Studio에서 Phi-3와 채팅하기**

LM Studio Chat에서 Phi-3를 선택하고 채팅 템플릿(Preset - Phi3)을 설정하여 Phi-3와 로컬 채팅을 시작합니다.

![LMStudioChat](../../../../translated_images/LMStudio_Chat.1bdc3a8f804f12d9548b386448c1642b741c10816576973155a90ef55f8a9c8d.ko.png)

***참고***:

a. LM Studio 제어판의 고급 설정을 통해 매개변수를 설정할 수 있습니다.

b. Phi-3는 특정 채팅 템플릿 요구사항이 있으므로, Preset에서 반드시 Phi-3를 선택해야 합니다.

c. GPU 사용량 등 다양한 매개변수를 설정할 수도 있습니다.

## **4. LM Studio에서 Phi-3 API 호출하기**

LM Studio는 로컬 서비스의 빠른 배포를 지원하며, 코딩 없이 모델 서비스를 구축할 수 있습니다.

![LMStudioServer](../../../../translated_images/LMStudio_Server.917c115e12599e7698ce323085ce4f8bdb020665656bbe90edca2d45a7de932d.ko.png)

Postman에서의 결과는 다음과 같습니다.

![LMStudioPostman](../../../../translated_images/LMStudio_Postman.4481aa4873ecaae0e05032f539090897002fc9aca9da5d1336fb28776f4c45a7.ko.png)

면책 조항: 이 번역은 원본을 AI 모델에 의해 번역된 것으로 완벽하지 않을 수 있습니다. 
출력을 검토하시고 필요한 수정 사항을 반영해 주세요.