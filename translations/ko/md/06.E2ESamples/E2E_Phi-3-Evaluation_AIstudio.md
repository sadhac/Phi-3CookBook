# Azure AI Foundry에서 Microsoft의 책임 있는 AI 원칙을 중심으로 Fine-tuned Phi-3 / Phi-3.5 모델 평가하기

이 엔드 투 엔드(E2E) 샘플은 Microsoft Tech Community의 가이드 "[Azure AI Foundry에서 Microsoft의 책임 있는 AI를 중심으로 Fine-tuned Phi-3 / 3.5 모델 평가하기](https://techcommunity.microsoft.com/t5/educator-developer-blog/evaluate-fine-tuned-phi-3-3-5-models-in-azure-ai-studio-focusing/ba-p/4227850?WT.mc_id=aiml-137032-kinfeylo)"를 기반으로 합니다.

## 개요

### Azure AI Foundry에서 Fine-tuned Phi-3 / Phi-3.5 모델의 안전성과 성능을 어떻게 평가할 수 있을까요?

모델을 Fine-tuning하면 때때로 의도하지 않은 응답이 발생할 수 있습니다. 모델이 안전하고 효과적으로 유지되도록 하기 위해서는 모델이 유해한 콘텐츠를 생성할 가능성과 정확하고 관련성 있으며 일관된 응답을 생성할 수 있는 능력을 평가하는 것이 중요합니다. 이 튜토리얼에서는 Azure AI Foundry의 Prompt flow와 통합된 Fine-tuned Phi-3 / Phi-3.5 모델의 안전성과 성능을 평가하는 방법을 배우게 됩니다.

다음은 Azure AI Foundry의 평가 과정입니다.

![튜토리얼 아키텍처.](../../../../translated_images/architecture.1eb9d143d0771c6065f16c0f66a9eb233f466cdf9db0b0afe11adcbd57eb06ce.ko.png)

*이미지 출처: [생성형 AI 응용 프로그램 평가](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-approach-gen-ai?wt.mc_id%3Dstudentamb_279723)*

> [!NOTE]
>
> Phi-3 / Phi-3.5에 대한 더 자세한 정보와 추가 리소스를 탐색하려면 [Phi-3CookBook](https://github.com/microsoft/Phi-3CookBook?wt.mc_id=studentamb_279723)을 방문하세요.

### 사전 준비 사항

- [Python](https://www.python.org/downloads)
- [Azure 구독](https://azure.microsoft.com/free?wt.mc_id=studentamb_279723)
- [Visual Studio Code](https://code.visualstudio.com)
- Fine-tuned Phi-3 / Phi-3.5 모델

### 목차

1. [**시나리오 1: Azure AI Foundry의 Prompt flow 평가 소개**](../../../../md/06.E2ESamples)

    - [안전성 평가 소개](../../../../md/06.E2ESamples)
    - [성능 평가 소개](../../../../md/06.E2ESamples)

1. [**시나리오 2: Azure AI Foundry에서 Phi-3 / Phi-3.5 모델 평가하기**](../../../../md/06.E2ESamples)

    - [시작하기 전에](../../../../md/06.E2ESamples)
    - [Phi-3 / Phi-3.5 모델을 평가하기 위해 Azure OpenAI 배포](../../../../md/06.E2ESamples)
    - [Azure AI Foundry의 Prompt flow 평가를 사용하여 Fine-tuned Phi-3 / Phi-3.5 모델 평가](../../../../md/06.E2ESamples)

1. [축하합니다!](../../../../md/06.E2ESamples)

## **시나리오 1: Azure AI Foundry의 Prompt flow 평가 소개**

### 안전성 평가 소개

AI 모델이 윤리적이고 안전한지 확인하기 위해 Microsoft의 책임 있는 AI 원칙에 따라 모델을 평가하는 것이 중요합니다. Azure AI Foundry에서는 안전성 평가를 통해 모델의 탈옥 공격에 대한 취약성과 유해한 콘텐츠 생성 가능성을 평가할 수 있습니다.

![안전성 평가.](../../../../translated_images/safety-evaluation.5ad906c4618e4c8736fdeeff54a52dac8ae6d0756b15824e430177fba7b6a8b4.ko.png)

*이미지 출처: [생성형 AI 응용 프로그램 평가](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-approach-gen-ai?wt.mc_id%3Dstudentamb_279723)*

#### Microsoft의 책임 있는 AI 원칙

기술적 단계를 시작하기 전에, AI 시스템의 책임 있는 개발, 배포 및 운영을 안내하는 윤리적 프레임워크인 Microsoft의 책임 있는 AI 원칙을 이해하는 것이 중요합니다. 이러한 원칙은 AI 기술이 공정하고 투명하며 포괄적인 방식으로 구축되도록 보장합니다. 이러한 원칙은 AI 모델의 안전성을 평가하는 데 기반이 됩니다.

Microsoft의 책임 있는 AI 원칙에는 다음이 포함됩니다:

- **공정성 및 포괄성**: AI 시스템은 모든 사람을 공정하게 대하고 유사한 상황에 있는 그룹을 다르게 대하지 않아야 합니다. 예를 들어, AI 시스템이 의료 치료, 대출 신청 또는 고용에 대한 지침을 제공할 때, 유사한 증상, 재정 상황 또는 직업 자격을 가진 모든 사람에게 동일한 권장 사항을 제공해야 합니다.

- **신뢰성 및 안전성**: 신뢰를 구축하기 위해 AI 시스템이 신뢰할 수 있고 안전하며 일관되게 작동하는 것이 중요합니다. 이러한 시스템은 원래 설계된 대로 작동하고 예상치 못한 조건에 안전하게 대응하며 유해한 조작에 저항할 수 있어야 합니다. 그들의 행동과 처리할 수 있는 다양한 조건은 개발자가 설계 및 테스트 중에 예상한 상황과 환경의 범위를 반영합니다.

- **투명성**: AI 시스템이 사람들의 삶에 큰 영향을 미치는 결정을 내리는 데 도움을 줄 때, 사람들이 그 결정이 어떻게 내려졌는지 이해하는 것이 중요합니다. 예를 들어, 은행이 AI 시스템을 사용하여 사람의 신용 가치 여부를 결정할 수 있습니다. 회사는 AI 시스템을 사용하여 가장 적합한 후보를 결정할 수 있습니다.

- **개인정보 보호 및 보안**: AI가 더 널리 사용됨에 따라 개인 및 비즈니스 정보를 보호하고 보안을 유지하는 것이 더욱 중요하고 복잡해지고 있습니다. AI에서는 개인정보 보호 및 데이터 보안이 중요한 관심사가 되며, 데이터에 대한 접근은 AI 시스템이 사람에 대한 정확하고 정보에 입각한 예측과 결정을 내리는 데 필수적입니다.

- **책임성**: AI 시스템을 설계하고 배포하는 사람들은 시스템이 어떻게 작동하는지에 대한 책임을 져야 합니다. 조직은 업계 표준을 기반으로 책임성 규범을 개발해야 합니다. 이러한 규범은 AI 시스템이 사람들의 삶에 영향을 미치는 결정에 대한 최종 권한이 되지 않도록 보장할 수 있습니다. 또한 인간이 고도로 자율적인 AI 시스템에 대해 의미 있는 통제력을 유지할 수 있도록 보장할 수 있습니다.

![Fill hub.](../../../../translated_images/responsibleai2.ae6f996d95dcc46b3b3087c0e4f4f4b74c64e961083009ecca7a0a3998b3f716.ko.png)

*이미지 출처: [책임 있는 AI란 무엇인가?](https://learn.microsoft.com/azure/machine-learning/concept-responsible-ai?view=azureml-api-2&viewFallbackFrom=azureml-api-2%253fwt.mc_id%3Dstudentamb_279723)*

> [!NOTE]
> Microsoft의 책임 있는 AI 원칙에 대해 더 자세히 알아보려면 [책임 있는 AI란 무엇인가?](https://learn.microsoft.com/azure/machine-learning/concept-responsible-ai?view=azureml-api-2?wt.mc_id=studentamb_279723)을 방문하세요.

#### 안전성 지표

이 튜토리얼에서는 Azure AI Foundry의 안전성 지표를 사용하여 Fine-tuned Phi-3 모델의 안전성을 평가합니다. 이러한 지표는 모델의 유해한 콘텐츠 생성 가능성과 탈옥 공격에 대한 취약성을 평가하는 데 도움을 줍니다. 안전성 지표에는 다음이 포함됩니다:

- **자해 관련 콘텐츠**: 모델이 자해 관련 콘텐츠를 생성할 가능성을 평가합니다.
- **혐오 및 불공정 콘텐츠**: 모델이 혐오 또는 불공정한 콘텐츠를 생성할 가능성을 평가합니다.
- **폭력적 콘텐츠**: 모델이 폭력적 콘텐츠를 생성할 가능성을 평가합니다.
- **성적 콘텐츠**: 모델이 부적절한 성적 콘텐츠를 생성할 가능성을 평가합니다.

이러한 측면을 평가함으로써 AI 모델이 유해하거나 불쾌한 콘텐츠를 생성하지 않도록 보장하여 사회적 가치와 규제 표준에 부합하게 합니다.

![안전성 기반 평가.](../../../../translated_images/evaluate-based-on-safety.63d79ac01570713002d5d858bfbb8f4d7295557ae8829d0c379485d67a3fcd1c.ko.png)

### 성능 평가 소개

AI 모델이 예상대로 작동하는지 확인하기 위해 성능 지표를 기준으로 모델의 성능을 평가하는 것이 중요합니다. Azure AI Foundry에서는 성능 평가를 통해 모델이 정확하고 관련성 있으며 일관된 응답을 생성하는지 평가할 수 있습니다.

![성능 평가.](../../../../translated_images/performance-evaluation.259c44647c74a80761cdcbaab2202142f99a5a0d28326c8a1eb6dc2765f5ef77.ko.png)

*이미지 출처: [생성형 AI 응용 프로그램 평가](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-approach-gen-ai?wt.mc_id%3Dstudentamb_279723)*

#### 성능 지표

이 튜토리얼에서는 Azure AI Foundry의 성능 지표를 사용하여 Fine-tuned Phi-3 / Phi-3.5 모델의 성능을 평가합니다. 이러한 지표는 모델이 정확하고 관련성 있으며 일관된 응답을 생성하는지 평가하는 데 도움을 줍니다. 성능 지표에는 다음이 포함됩니다:

- **Groundedness**: 생성된 답변이 입력 소스의 정보와 얼마나 잘 일치하는지 평가합니다.
- **Relevance**: 주어진 질문에 대한 생성된 응답의 관련성을 평가합니다.
- **Coherence**: 생성된 텍스트가 얼마나 자연스럽게 읽히고 인간과 같은 언어를 닮았는지 평가합니다.
- **Fluency**: 생성된 텍스트의 언어 능력을 평가합니다.
- **GPT 유사성**: 생성된 응답을 기준 답변과 비교하여 유사성을 평가합니다.
- **F1 점수**: 생성된 응답과 소스 데이터 간의 공유된 단어 비율을 계산합니다.

이러한 지표는 모델이 정확하고 관련성 있으며 일관된 응답을 생성하는지 평가하는 데 도움을 줍니다.

![성능 기반 평가.](../../../../translated_images/evaluate-based-on-performance.33ccf1c52f210af8e76d9cab863716d3f67db3d765254371a30136cc8f852b37.ko.png)

## **시나리오 2: Azure AI Foundry에서 Phi-3 / Phi-3.5 모델 평가하기**

### 시작하기 전에

이 튜토리얼은 이전 블로그 게시물 "[Fine-Tune and Integrate Custom Phi-3 Models with Prompt Flow: Step-by-Step Guide](https://techcommunity.microsoft.com/t5/educator-developer-blog/fine-tune-and-integrate-custom-phi-3-models-with-prompt-flow/ba-p/4178612?wt.mc_id=studentamb_279723)" 및 "[Fine-Tune and Integrate Custom Phi-3 Models with Prompt Flow in Azure AI Foundry](https://techcommunity.microsoft.com/t5/educator-developer-blog/fine-tune-and-integrate-custom-phi-3-models-with-prompt-flow-in/ba-p/4191726?wt.mc_id=studentamb_279723)"의 후속입니다. 이 게시물에서는 Azure AI Foundry에서 Phi-3 / Phi-3.5 모델을 Fine-tuning하고 Prompt flow와 통합하는 과정을 다뤘습니다.

이 튜토리얼에서는 Azure AI Foundry에서 평가자로 Azure OpenAI 모델을 배포하고 이를 사용하여 Fine-tuned Phi-3 / Phi-3.5 모델을 평가합니다.

이 튜토리얼을 시작하기 전에 이전 튜토리얼에서 설명한 다음 사전 준비 사항을 확인하세요:

1. Fine-tuned Phi-3 / Phi-3.5 모델을 평가할 준비된 데이터셋.
1. Azure Machine Learning에 배포된 Fine-tuned Phi-3 / Phi-3.5 모델.
1. Azure AI Foundry에서 Fine-tuned Phi-3 / Phi-3.5 모델과 통합된 Prompt flow.

> [!NOTE]
> 이전 블로그 게시물에서 다운로드한 **ULTRACHAT_200k** 데이터셋의 데이터 폴더에 있는 *test_data.jsonl* 파일을 Fine-tuned Phi-3 / Phi-3.5 모델을 평가할 데이터셋으로 사용합니다.

#### Azure AI Foundry에서 Prompt flow와 통합된 사용자 정의 Phi-3 / Phi-3.5 모델(코드 우선 접근 방식)

> [!NOTE]
> "[Fine-Tune and Integrate Custom Phi-3 Models with Prompt Flow in Azure AI Foundry](https://techcommunity.microsoft.com/t5/educator-developer-blog/fine-tune-and-integrate-custom-phi-3-models-with-prompt-flow-in/ba-p/4191726?wt.mc_id=studentamb_279723)"에서 설명한 저코드 접근 방식을 따랐다면 이 연습을 건너뛰고 다음으로 진행할 수 있습니다.
> 그러나 "[Fine-Tune and Integrate Custom Phi-3 Models with Prompt Flow: Step-by-Step Guide](https://techcommunity.microsoft.com/t5/educator-developer-blog/fine-tune-and-integrate-custom-phi-3-models-with-prompt-flow/ba-p/4178612?wt.mc_id=studentamb_279723)"에서 설명한 코드 우선 접근 방식을 따라 Phi-3 / Phi-3.5 모델을 Fine-tuning하고 배포한 경우, 모델을 Prompt flow에 연결하는 과정이 약간 다릅니다. 이 연습에서는 이 과정을 배우게 됩니다.

Fine-tuned Phi-3 / Phi-3.5 모델을 Azure AI Foundry의 Prompt flow에 통합해야 합니다.

#### Azure AI Foundry Hub 만들기

프로젝트를 만들기 전에 Hub를 만들어야 합니다. Hub는 리소스 그룹과 유사하게 여러 프로젝트를 Azure AI Foundry 내에서 조직하고 관리할 수 있도록 합니다.

1. [Azure AI Foundry](https://ai.azure.com/?wt.mc_id=studentamb_279723)에 로그인합니다.

1. 왼쪽 탭에서 **All hubs**를 선택합니다.

1. 탐색 메뉴에서 **+ New hub**를 선택합니다.

    ![Hub 만들기.](../../../../translated_images/create-hub.8d452311ef5b4b9188df89f7cff7797c67ec8f391282235b19b988e167f3e920.ko.png)

1. 다음 작업을 수행합니다:

    - **Hub 이름**을 입력합니다. 고유한 값이어야 합니다.
    - Azure **Subscription**을 선택합니다.
    - 사용할 **Resource group**을 선택합니다(필요한 경우 새로 만듭니다).
    - 사용할 **Location**을 선택합니다.
    - 사용할 **Connect Azure AI Services**를 선택합니다(필요한 경우 새로 만듭니다).
    - **Connect Azure AI Search**를 **Skip connecting**으로 선택합니다.
![Fill hub.](../../../../translated_images/fill-hub.8b19834866ef631a2fd031584c77b78c0438a385bdee8f981361b14bbc46f5e1.ko.png)

1. **Next**를 선택합니다.

#### Azure AI Foundry 프로젝트 생성

1. 생성한 Hub에서 왼쪽 탭에서 **All projects**를 선택합니다.

1. 네비게이션 메뉴에서 **+ New project**를 선택합니다.

    ![Select new project.](../../../../translated_images/select-new-project.1a925c25ca3bc47b2b16feefc5a76f5c29e211ac464ea5c3cdfe389868d87da7.ko.png)

1. **Project name**을 입력합니다. 고유한 값을 입력해야 합니다.

    ![Create project.](../../../../translated_images/create-project.ff239752937343b4cb38156740ebda92bc1d8b16299183c245f3e3661432db31.ko.png)

1. **Create a project**를 선택합니다.

#### 미세 조정된 Phi-3 / Phi-3.5 모델을 위한 사용자 정의 연결 추가

사용자 정의 Phi-3 / Phi-3.5 모델을 Prompt flow와 통합하려면 모델의 엔드포인트와 키를 사용자 정의 연결에 저장해야 합니다. 이 설정을 통해 Prompt flow에서 사용자 정의 Phi-3 / Phi-3.5 모델에 액세스할 수 있습니다.

#### 미세 조정된 Phi-3 / Phi-3.5 모델의 API 키와 엔드포인트 URI 설정

1. [Azure ML Studio](https://ml.azure.com/home?wt.mc_id=studentamb_279723)에 방문합니다.

1. 생성한 Azure Machine learning 작업 영역으로 이동합니다.

1. 왼쪽 탭에서 **Endpoints**를 선택합니다.

    ![Select endpoints.](../../../../translated_images/select-endpoints.3027748aed379990fd8ee9bf27f70ff11918955bb1a10269e2f34f6931b26955.ko.png)

1. 생성한 엔드포인트를 선택합니다.

    ![Select endpoints.](../../../../translated_images/select-endpoint-created.560a5cadfbbb58b66abb2fb61b4450b22060371910af1b45c358bde548234ebc.ko.png)

1. 네비게이션 메뉴에서 **Consume**을 선택합니다.

1. **REST endpoint**와 **Primary key**를 복사합니다.

    ![Copy api key and endpoint uri.](../../../../translated_images/copy-endpoint-key.56de01742992f2402d57139849304b5b049fb468fb38abc7982b7dfc311daf9e.ko.png)

#### 사용자 정의 연결 추가

1. [Azure AI Foundry](https://ai.azure.com/?wt.mc_id=studentamb_279723)에 방문합니다.

1. 생성한 Azure AI Foundry 프로젝트로 이동합니다.

1. 생성한 프로젝트에서 왼쪽 탭에서 **Settings**를 선택합니다.

1. **+ New connection**을 선택합니다.

    ![Select new connection.](../../../../translated_images/select-new-connection.a1ff72172d07054308a3fc7b7b86e25e9ca1c879f0a382b9a2be2c80bb2ebcc5.ko.png)

1. 네비게이션 메뉴에서 **Custom keys**를 선택합니다.

    ![Select custom keys.](../../../../translated_images/select-custom-keys.b17eb3b15eae28126a4eeda8f53396b9a6f773745f2dd68c464252575a77b5d3.ko.png)

1. 다음 작업을 수행합니다:

    - **+ Add key value pairs**를 선택합니다.
    - 키 이름에 **endpoint**를 입력하고 Azure ML Studio에서 복사한 엔드포인트를 값 필드에 붙여넣습니다.
    - 다시 **+ Add key value pairs**를 선택합니다.
    - 키 이름에 **key**를 입력하고 Azure ML Studio에서 복사한 키를 값 필드에 붙여넣습니다.
    - 키를 추가한 후 **is secret**을 선택하여 키가 노출되지 않도록 합니다.

    ![Add connection.](../../../../translated_images/add-connection.c01c94851c9eece708711456a4853355b9532b0cb1f970e24f165e7e1d6c0a03.ko.png)

1. **Add connection**을 선택합니다.

#### Prompt flow 생성

Azure AI Foundry에 사용자 정의 연결을 추가했습니다. 이제 다음 단계에 따라 Prompt flow를 생성합니다. 그런 다음, 이 Prompt flow를 사용자 정의 연결에 연결하여 미세 조정된 모델을 Prompt flow 내에서 사용할 수 있게 합니다.

1. 생성한 Azure AI Foundry 프로젝트로 이동합니다.

1. 왼쪽 탭에서 **Prompt flow**를 선택합니다.

1. 네비게이션 메뉴에서 **+ Create**를 선택합니다.

    ![Select Promptflow.](../../../../translated_images/select-promptflow.766ad0f2403e2bd6f374bee40a607321e3e2b416629063acf3204a983fb4bcaa.ko.png)

1. 네비게이션 메뉴에서 **Chat flow**를 선택합니다.

    ![Select chat flow.](../../../../translated_images/select-flow-type.0e18b84032da1200e48a702e5140c1775b1eb6de9cf222c6a8007840fa278e97.ko.png)

1. 사용할 **Folder name**을 입력합니다.

    ![Select chat flow.](../../../../translated_images/enter-name.43919b211b1e8e0184536dc09184190e7e8c56bf960d4b5601443efddc757db4.ko.png)

1. **Create**를 선택합니다.

#### 사용자 정의 Phi-3 / Phi-3.5 모델과 대화하는 Prompt flow 설정

미세 조정된 Phi-3 / Phi-3.5 모델을 Prompt flow에 통합해야 합니다. 그러나 제공된 기존 Prompt flow는 이 목적에 맞지 않으므로, 사용자 정의 모델 통합을 위해 Prompt flow를 다시 설계해야 합니다.

1. Prompt flow에서 기존 흐름을 재구성하기 위해 다음 작업을 수행합니다:

    - **Raw file mode**를 선택합니다.
    - *flow.dag.yml* 파일의 기존 코드를 모두 삭제합니다.
    - 다음 코드를 *flow.dag.yml*에 추가합니다.

        ```yml
        inputs:
          input_data:
            type: string
            default: "Who founded Microsoft?"

        outputs:
          answer:
            type: string
            reference: ${integrate_with_promptflow.output}

        nodes:
        - name: integrate_with_promptflow
          type: python
          source:
            type: code
            path: integrate_with_promptflow.py
          inputs:
            input_data: ${inputs.input_data}
        ```

    - **Save**를 선택합니다.

    ![Select raw file mode.](../../../../translated_images/select-raw-file-mode.2084d7f905df40f69cc5ebe48efa2318e92fd069358625a92993ef614f189d84.ko.png)

1. 사용자 정의 Phi-3 / Phi-3.5 모델을 Prompt flow에서 사용하려면 *integrate_with_promptflow.py*에 다음 코드를 추가합니다.

    ```python
    import logging
    import requests
    from promptflow import tool
    from promptflow.connections import CustomConnection

    # Logging setup
    logging.basicConfig(
        format="%(asctime)s - %(levelname)s - %(name)s - %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S",
        level=logging.DEBUG
    )
    logger = logging.getLogger(__name__)

    def query_phi3_model(input_data: str, connection: CustomConnection) -> str:
        """
        Send a request to the Phi-3 / Phi-3.5 model endpoint with the given input data using Custom Connection.
        """

        # "connection" is the name of the Custom Connection, "endpoint", "key" are the keys in the Custom Connection
        endpoint_url = connection.endpoint
        api_key = connection.key

        headers = {
            "Content-Type": "application/json",
            "Authorization": f"Bearer {api_key}"
        }
    data = {
        "input_data": [input_data],
        "params": {
            "temperature": 0.7,
            "max_new_tokens": 128,
            "do_sample": True,
            "return_full_text": True
            }
        }
        try:
            response = requests.post(endpoint_url, json=data, headers=headers)
            response.raise_for_status()
            
            # Log the full JSON response
            logger.debug(f"Full JSON response: {response.json()}")

            result = response.json()["output"]
            logger.info("Successfully received response from Azure ML Endpoint.")
            return result
        except requests.exceptions.RequestException as e:
            logger.error(f"Error querying Azure ML Endpoint: {e}")
            raise

    @tool
    def my_python_tool(input_data: str, connection: CustomConnection) -> str:
        """
        Tool function to process input data and query the Phi-3 / Phi-3.5 model.
        """
        return query_phi3_model(input_data, connection)

    ```

    ![Paste prompt flow code.](../../../../translated_images/paste-promptflow-code.667abbdf848fd03153828c0aa70dde58a851e09b1ba4c69bc6f686d2005656aa.ko.png)

> [!NOTE]
> Azure AI Foundry에서 Prompt flow를 사용하는 자세한 정보는 [Prompt flow in Azure AI Foundry](https://learn.microsoft.com/azure/ai-studio/how-to/prompt-flow)를 참조하십시오.

1. **Chat input**, **Chat output**을 선택하여 모델과 대화할 수 있도록 합니다.

    ![Select Input Output.](../../../../translated_images/select-input-output.d4803eae144b03579db4a23def15c68bb50527017cdc4aa9f72c8679588a0f4c.ko.png)

1. 이제 사용자 정의 Phi-3 / Phi-3.5 모델과 대화할 준비가 되었습니다. 다음 연습에서는 Prompt flow를 시작하고 이를 사용하여 미세 조정된 Phi-3 / Phi-3.5 모델과 대화하는 방법을 배웁니다.

> [!NOTE]
>
> 재구성된 흐름은 아래 이미지와 같아야 합니다:
>
> ![Flow example](../../../../translated_images/graph-example.5b309021deca5b503270e50888da4784256730c210ed757f799f9bff0a12bb19.ko.png)
>

#### Prompt flow 시작

1. Prompt flow를 시작하려면 **Start compute sessions**를 선택합니다.

    ![Start compute session.](../../../../translated_images/start-compute-session.75300f481218ca70eae80304255956c71a9b6be31a18b43264118c19c0b1a016.ko.png)

1. 매개변수를 갱신하려면 **Validate and parse input**을 선택합니다.

    ![Validate input.](../../../../translated_images/validate-input.a6c90e55ce6117ea44e2acd88b8a20bc31136bf6c574b0a6c9217867201025c9.ko.png)

1. 사용자 정의 연결에 대한 **connection**의 **Value**를 선택합니다. 예를 들어, *connection*.

    ![Connection.](../../../../translated_images/select-connection.6573a1269969a14c83c397334051f71057ec9a243e95ea1b849483bd7481ff6a.ko.png)

#### 사용자 정의 Phi-3 / Phi-3.5 모델과 대화하기

1. **Chat**을 선택합니다.

    ![Select chat.](../../../../translated_images/select-chat.25eab3d62b0a6c4960f0ae1b5d6efd6b5847cc20d468fd28cb1f0d656936cc22.ko.png)

1. 결과 예시: 이제 사용자 정의 Phi-3 / Phi-3.5 모델과 대화할 수 있습니다. 미세 조정에 사용된 데이터를 기반으로 질문하는 것이 좋습니다.

    ![Chat with prompt flow.](../../../../translated_images/chat-with-promptflow.105b5a3b70ff64725c1d4cd2e9c6b55301219c7d68c9bec59106a49fb8bf40f2.ko.png)

### Phi-3 / Phi-3.5 모델 평가를 위해 Azure OpenAI 배포

Azure AI Foundry에서 Phi-3 / Phi-3.5 모델을 평가하려면 Azure OpenAI 모델을 배포해야 합니다. 이 모델은 Phi-3 / Phi-3.5 모델의 성능을 평가하는 데 사용됩니다.

#### Azure OpenAI 배포

1. [Azure AI Foundry](https://ai.azure.com/?wt.mc_id=studentamb_279723)에 로그인합니다.

1. 생성한 Azure AI Foundry 프로젝트로 이동합니다.

    ![Select Project.](../../../../translated_images/select-project-created.7b3c97c3883c3a95d547173b41e579cd748df940749c3d9616fe03ef46a3eda2.ko.png)

1. 생성한 프로젝트에서 왼쪽 탭에서 **Deployments**를 선택합니다.

1. 네비게이션 메뉴에서 **+ Deploy model**을 선택합니다.

1. **Deploy base model**을 선택합니다.

    ![Select Deployments.](../../../../translated_images/deploy-openai-model.f09a74e1f976b52f85fdef711372452b9faed270e9d015887e09f44b41bbc163.ko.png)

1. 사용할 Azure OpenAI 모델을 선택합니다. 예를 들어, **gpt-4o**.

    ![Select Azure OpenAI model you'd like to use.](../../../../translated_images/select-openai-model.29fbbd802d6a9aa941097ae80a0ffe256239e636190b7c1e49f28d3d66143a0d.ko.png)

1. **Confirm**을 선택합니다.

### Azure AI Foundry의 Prompt flow 평가를 사용하여 미세 조정된 Phi-3 / Phi-3.5 모델 평가

### 새 평가 시작

1. [Azure AI Foundry](https://ai.azure.com/?wt.mc_id=studentamb_279723)에 방문합니다.

1. 생성한 Azure AI Foundry 프로젝트로 이동합니다.

    ![Select Project.](../../../../translated_images/select-project-created.7b3c97c3883c3a95d547173b41e579cd748df940749c3d9616fe03ef46a3eda2.ko.png)

1. 생성한 프로젝트에서 왼쪽 탭에서 **Evaluation**을 선택합니다.

1. 네비게이션 메뉴에서 **+ New evaluation**을 선택합니다.
![Select evaluation.](../../../../translated_images/select-evaluation.7d8a8228ebdf3f3b46bf5cf6ab5bdcb4565132ba6b28126d9757aaf3abade725.ko.png)

1. **Prompt flow** 평가를 선택합니다.

    ![Select Prompt flow evaluation.](../../../../translated_images/promptflow-evaluation.ff4265fafd69c7f5ded1b5275cacecbd5f3272a6358c1f784f62e64bcb9e949f.ko.png)

1. 다음 작업을 수행합니다:

    - 평가 이름을 입력합니다. 고유한 값이어야 합니다.
    - 작업 유형으로 **문맥 없는 질문과 답변**을 선택합니다. 이 튜토리얼에서 사용하는 **UlTRACHAT_200k** 데이터셋은 문맥을 포함하지 않기 때문입니다.
    - 평가하고자 하는 프롬프트 플로우를 선택합니다.

    ![Prompt flow evaluation.](../../../../translated_images/evaluation-setting1.d3b22a8343f8265807e2b507fa7eec9d86a9cefd4a67bc39ba2022d572f13e1d.ko.png)

1. **다음**을 선택합니다.

1. 다음 작업을 수행합니다:

    - **데이터셋 추가**를 선택하여 데이터셋을 업로드합니다. 예를 들어, **ULTRACHAT_200k** 데이터셋을 다운로드할 때 포함된 *test_data.json1*과 같은 테스트 데이터셋 파일을 업로드할 수 있습니다.
    - 데이터셋에 맞는 **데이터셋 열**을 선택합니다. 예를 들어, **ULTRACHAT_200k** 데이터셋을 사용하는 경우 **${data.prompt}**을 데이터셋 열로 선택합니다.

    ![Prompt flow evaluation.](../../../../translated_images/evaluation-setting2.32749fa51bc4fdb32f75dfd09b96bee74454c51ce3084bcc6f95b7286177a657.ko.png)

1. **다음**을 선택합니다.

1. 성능 및 품질 지표를 설정하기 위해 다음 작업을 수행합니다:

    - 사용할 성능 및 품질 지표를 선택합니다.
    - 평가를 위해 생성한 Azure OpenAI 모델을 선택합니다. 예를 들어, **gpt-4o**를 선택합니다.

    ![Prompt flow evaluation.](../../../../translated_images/evaluation-setting3-1.db76b89d94911c84ece6ce793593a4289278e1b24520e38ecd8372f4b9dc1167.ko.png)

1. 위험 및 안전 지표를 설정하기 위해 다음 작업을 수행합니다:

    - 사용할 위험 및 안전 지표를 선택합니다.
    - 사용할 결함률을 계산하기 위한 임계값을 선택합니다. 예를 들어, **중간**을 선택합니다.
    - **질문**의 경우, **데이터 소스**를 **{$data.prompt}**로 선택합니다.
    - **답변**의 경우, **데이터 소스**를 **{$run.outputs.answer}**로 선택합니다.
    - **정답**의 경우, **데이터 소스**를 **{$data.message}**로 선택합니다.

    ![Prompt flow evaluation.](../../../../translated_images/evaluation-setting3-2.eb9892654970af140ebb74fcc99e06dad7eca3d38365e3f2cbe90101392f41ee.ko.png)

1. **다음**을 선택합니다.

1. 평가를 시작하려면 **제출**을 선택합니다.

1. 평가가 완료되는 데 시간이 걸릴 수 있습니다. **평가** 탭에서 진행 상황을 모니터링할 수 있습니다.

### 평가 결과 검토

> [!NOTE]
> 아래에 제시된 결과는 평가 과정을 설명하기 위한 예시입니다. 이 튜토리얼에서는 비교적 작은 데이터셋에서 미세 조정된 모델을 사용했기 때문에 최적의 결과를 얻지 못할 수 있습니다. 실제 결과는 사용된 데이터셋의 크기, 품질 및 다양성, 모델의 특정 구성에 따라 크게 달라질 수 있습니다.

평가가 완료되면 성능 및 안전 지표에 대한 결과를 검토할 수 있습니다.

1. 성능 및 품질 지표:

    - 모델이 일관되고 유창하며 관련성 있는 응답을 생성하는지 평가합니다.

    ![Evaluation result.](../../../../translated_images/evaluation-result-gpu.5b6e301e6d1af6044819f4d3c8443cbc44fb7db54ebce208b4288744ca25e6e8.ko.png)

1. 위험 및 안전 지표:

    - 모델의 출력이 안전하고 책임감 있는 AI 원칙에 부합하며, 유해하거나 불쾌한 콘텐츠를 피하는지 확인합니다.

    ![Evaluation result.](../../../../translated_images/evaluation-result-gpu-2.d867d40ee9dfebc40c878288b8dc8727721a2fec995904b1475c513f0960e8e0.ko.png)

1. **상세 지표 결과**를 보기 위해 아래로 스크롤할 수 있습니다.

    ![Evaluation result.](../../../../translated_images/detailed-metrics-result.6cf00c2b6026bb500ff758ee3047c20f600aab3878c892897e99e2e3a88fb002.ko.png)

1. 맞춤형 Phi-3 / Phi-3.5 모델을 성능 및 안전 지표에 대해 평가함으로써 모델이 효과적일 뿐만 아니라 책임감 있는 AI 실천을 준수하여 실제 배포에 준비가 되었는지 확인할 수 있습니다.

## 축하합니다!

### 튜토리얼을 완료했습니다

프롬프트 플로우와 통합된 Azure AI Foundry에서 미세 조정된 Phi-3 모델을 성공적으로 평가했습니다. 이는 AI 모델이 잘 작동할 뿐만 아니라 Microsoft의 책임감 있는 AI 원칙을 준수하여 신뢰할 수 있고 안정적인 AI 애플리케이션을 구축하는 데 중요한 단계입니다.

![Architecture.](../../../../translated_images/architecture.1eb9d143d0771c6065f16c0f66a9eb233f466cdf9db0b0afe11adcbd57eb06ce.ko.png)

## Azure 리소스 정리

계정에 추가 요금이 발생하지 않도록 Azure 리소스를 정리합니다. Azure 포털로 이동하여 다음 리소스를 삭제합니다:

- Azure Machine Learning 리소스.
- Azure Machine Learning 모델 엔드포인트.
- Azure AI Foundry 프로젝트 리소스.
- Azure AI Foundry 프롬프트 플로우 리소스.

### 다음 단계

#### 문서

- [microsoft/Phi-3CookBook](https://github.com/microsoft/Phi-3CookBook?wt.mc_id=studentamb_279723)
- [책임 있는 AI 대시보드를 사용하여 AI 시스템 평가](https://learn.microsoft.com/azure/machine-learning/concept-responsible-ai-dashboard?view=azureml-api-2&source=recommendations?wt.mc_id=studentamb_279723)
- [생성형 AI 평가 및 모니터링 지표](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-metrics-built-in?tabs=definition?wt.mc_id=studentamb_279723)
- [Azure AI Foundry 문서](https://learn.microsoft.com/azure/ai-studio/?wt.mc_id=studentamb_279723)
- [프롬프트 플로우 문서](https://microsoft.github.io/promptflow/?wt.mc_id=studentamb_279723)

#### 교육 콘텐츠

- [Microsoft의 책임 있는 AI 접근 방식 소개](https://learn.microsoft.com/training/modules/introduction-to-microsofts-responsible-ai-approach/?source=recommendations?wt.mc_id=studentamb_279723)
- [Azure AI Foundry 소개](https://learn.microsoft.com/training/modules/introduction-to-azure-ai-studio/?wt.mc_id=studentamb_279723)

### 참고 자료

- [microsoft/Phi-3CookBook](https://github.com/microsoft/Phi-3CookBook?wt.mc_id=studentamb_279723)
- [책임 있는 AI란 무엇인가?](https://learn.microsoft.com/azure/machine-learning/concept-responsible-ai?view=azureml-api-2?wt.mc_id=studentamb_279723)
- [더 안전하고 신뢰할 수 있는 생성형 AI 애플리케이션 구축을 위한 Azure AI의 새로운 도구 발표](https://azure.microsoft.com/blog/announcing-new-tools-in-azure-ai-to-help-you-build-more-secure-and-trustworthy-generative-ai-applications/?wt.mc_id=studentamb_279723)
- [생성형 AI 애플리케이션 평가](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-approach-gen-ai?wt.mc_id%3Dstudentamb_279723)

**면책 조항**:
이 문서는 기계 기반 AI 번역 서비스를 사용하여 번역되었습니다. 우리는 정확성을 위해 노력하지만, 자동 번역에는 오류나 부정확성이 포함될 수 있습니다. 원본 문서를 권위 있는 출처로 간주해야 합니다. 중요한 정보에 대해서는 전문적인 인간 번역을 권장합니다. 이 번역을 사용하여 발생하는 오해나 오역에 대해 우리는 책임지지 않습니다.