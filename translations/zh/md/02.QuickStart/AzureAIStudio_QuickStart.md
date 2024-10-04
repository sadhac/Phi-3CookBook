# **在 Azure AI Studio 中使用 Phi-3**

随着生成式 AI 的发展，我们希望使用一个统一的平台来管理不同的 LLM 和 SLM，进行企业数据集成、微调/RAG 操作，以及在集成 LLM 和 SLM 后评估不同企业业务等，从而更好地实现生成式 AI 智能应用。[Azure AI Studio](https://ai.azure.com) 是一个企业级的生成式 AI 应用平台。

![aistudo](../../../../translated_images/ai-studio-home.e25e21a22af0a57c0cb02815f4c7554c8816afe8bc3c3008ac74e2eedd9fbaa9.zh.png)

通过 Azure AI Studio，您可以评估大型语言模型 (LLM) 的响应，并通过提示流协调提示应用组件以获得更好的性能。该平台便于将概念验证转变为全面生产，并支持持续监控和改进以实现长期成功。

我们可以通过简单的步骤在 Azure AI Studio 上快速部署 Phi-3 模型，然后使用 Azure AI Studio 完成与 Phi-3 相关的 Playground/Chat、微调、评估等相关工作。

## **1. 准备工作**

## [AZD AI Studio Starter Template](https://azure.github.io/awesome-azd/?name=AI+Studio)

### Azure AI Studio Starter

这是一个 Bicep 模板，可以部署开始使用 Azure AI Studio 所需的一切。包括带有依赖资源的 AI Hub、AI 项目、AI 服务和一个在线端点。

### 快速使用

如果您的机器上已经安装了 [Azure Developer CLI](https://learn.microsoft.com/azure/developer/azure-developer-cli/overview?WT.mc_id=aiml-138114-kinfeylo)，那么使用这个模板就像在新目录中运行这个命令一样简单。

### 终端命令

```bash
azd init -t azd-aistudio-starter
```

或者
如果使用 azd VS Code 扩展，您可以在 VS Code 命令终端中粘贴此 URL。

### 终端 URL

```bash
azd-aistudio-starter
```

## 手动创建

在 [Azure Portal](https://portal.azure.com?WT.mc_id=aiml-138114-kinfeylo) 上创建 Azure AI Studio

![portal](../../../../translated_images/ai-studio-portal.8ae13fc10a0fe53104d7fe8d1c8c59b53f5ff7f4d74e52d81bcd63b5de6baf13.zh.png)

完成工作室命名和区域设置后，您可以创建它

![settings](../../../../translated_images/ai-studio-settings.ac28832948da45fd844232ae8e743f3e657a4b88e8a02ce80ae6bfad8ba4733a.zh.png)

创建成功后，您可以通过 [ai.azure.com](https://ai.azure.com/) 访问您创建的工作室

![page](../../../../translated_images/ai-studio-page.9bfba68b0b3662a5323008dab8d9b24d4fc580be93777203bb64ad78283df469.zh.png)

一个 AI Studio 上可以有多个项目。在 AI Studio 中创建一个项目以进行准备。

![proj](../../../../translated_images/ai-studio-proj.62b5b49ee77bd4e382a82c1c28c247c1204c11ea212a4d95b39e467c6a24998f.zh.png)

## **2. 在 Azure AI Studio 中部署 Phi-3 模型**

点击项目的 Explore 选项进入模型目录并选择 Phi-3

![model](../../../../translated_images/ai-studio-model.d90f85e0b4ce4bbdde6e460304f2e6676502e86ec0aae8f39dd56b7f0538afb9.zh.png)

选择 Phi-3-mini-4k-instruct

![phi3](../../../../translated_images/ai-studio-phi3.9320ffe396abdbf9d1026637016462406090df88e0883e411b1984be34ed5710.zh.png)

点击 'Deploy' 部署 Phi-3-mini-4k-instruct 模型

> [!NOTE]
>
> 部署时可以选择计算能力

## **3. 在 Azure AI Studio 中的 Playground Chat Phi-3**

进入部署页面，选择 Playground，与 Azure AI Studio 的 Phi-3 聊天

![chat](../../../../translated_images/ai-studio-chat.ba2c631ac2279f2deb4e87998895b0688e33d2f79475da6a3851e3fb3a0495c5.zh.png)

## **4. 从 Azure AI Studio 部署模型**

要从 Azure 模型目录部署模型，您可以按照以下步骤操作：

- 登录 Azure AI Studio。
- 从 Azure AI Studio 模型目录中选择您要部署的模型。
- 在模型的详细信息页面上，选择 Deploy，然后选择带有 Azure AI Content Safety 的无服务器 API。
- 选择您要部署模型的项目。要使用无服务器 API 服务，您的工作区必须属于 East US 2 或 Sweden Central 区域。您可以自定义部署名称。
- 在部署向导中，选择 Pricing and terms 以了解定价和使用条款。
- 选择 Deploy。等待部署准备就绪，您将被重定向到 Deployments 页面。
- 选择 Open in playground 开始与模型互动。
- 您可以返回 Deployments 页面，选择部署，并记下端点的 Target URL 和 Secret Key，您可以使用它们来调用部署并生成完成。
- 您可以随时通过导航到 Build 选项卡并从 Components 部分选择 Deployments 来找到端点的详细信息、URL 和访问密钥。

> [!NOTE]
> 请注意，您的帐户必须在资源组上具有 Azure AI Developer 角色权限才能执行这些步骤。

## **5. 在 Azure AI Studio 中使用 Phi-3 API**

您可以通过 Postman GET 访问 https://{Your project name}.region.inference.ml.azure.com/swagger.json 并结合 Key 了解提供的接口

![swagger](../../../../translated_images/ai-studio-swagger.ae9e8fff8aba78ec18dc94b0ef251f0efe4ba90e77618ff0df13e1636e196abf.zh.png)

例如访问 score api 

![score](../../../../translated_images/ai-studio-score.0d5c8ce86241111633e946acf3413d3073957beb81cd37382cfd084ae310678f.zh.png)

您可以非常方便地获取请求参数以及响应参数。这是 Postman 结果

![result](../../../../translated_images/ai-studio-result.8563455b3a437110aa1d99bfc21cd8c624510b100f20b8907653cba5eef36226.zh.png)
