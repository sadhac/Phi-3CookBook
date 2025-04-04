<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "418c693c63cc0e817dc560558f730a7a",
  "translation_date": "2025-04-04T17:55:51+00:00",
  "source_file": "md\\01.Introduction\\04\\QuantifyingPhi.md",
  "language_code": "hk"
}
-->
# **量化 Phi 家族**

模型量化是指将神经网络模型中的参数（例如权重和激活值）从较大的数值范围（通常是连续的数值范围）映射到较小的有限数值范围的过程。这项技术可以减小模型的大小和计算复杂度，并提升模型在资源有限的环境中（如移动设备或嵌入式系统）的运行效率。通过降低参数的精度，模型量化实现了压缩，但同时也引入了一定的精度损失。因此，在量化过程中，需要平衡模型大小、计算复杂度和精度。常见的量化方法包括定点量化、浮点量化等，可以根据具体场景和需求选择合适的量化策略。

我們希望將 GenAI 模型部署到邊緣設備，使更多設備能夠進入 GenAI 場景，例如移動設備、AI PC/Copilot+PC，以及傳統物聯網設備。通過量化模型，我們可以根據不同設備將其部署到不同的邊緣設備。結合硬件製造商提供的模型加速框架和量化模型，我們可以構建更好的 SLM 應用場景。

在量化場景中，我們有不同的精度選擇（INT4、INT8、FP16、FP32）。以下是常用量化精度的解釋。

### **INT4**

INT4 量化是一種激進的量化方法，將模型的權重和激活值量化為 4 位整數。由於表示範圍較小且精度較低，INT4 量化通常會導致更大的精度損失。然而，與 INT8 量化相比，INT4 量化可以進一步減少模型的存儲需求和計算複雜度。需要注意的是，INT4 量化在實際應用中相對較少，因為過低的精度可能導致模型性能顯著下降。此外，並非所有硬件都支持 INT4 操作，因此選擇量化方法時需要考慮硬件兼容性。

### **INT8**

INT8 量化是將模型的權重和激活值從浮點數轉換為 8 位整數的過程。雖然 INT8 整數表示的數值範圍較小且精度較低，但它能顯著減少存儲和計算需求。在 INT8 量化過程中，模型的權重和激活值會經過量化處理，包括縮放和偏移，以儘可能保留原始浮點信息。在推理過程中，這些量化值會被解量化回浮點數進行計算，然後再量化回 INT8 進行下一步操作。這種方法在大多數應用中可以提供足夠的精度，同時保持高計算效率。

### **FP16**

FP16 格式，即 16 位浮點數（float16），與 32 位浮點數（float32）相比，將內存占用減少了一半，在大規模深度學習應用中具有顯著優勢。FP16 格式允許在相同的 GPU 內存限制下加載更大的模型或處理更多數據。隨著現代 GPU 硬件不斷支持 FP16 操作，使用 FP16 格式還可能帶來計算速度的提升。然而，FP16 格式也有其固有的缺點，即精度較低，可能在某些情況下導致數值不穩定或精度損失。

### **FP32**

FP32 格式提供更高的精度，能準確表示廣泛的數值範圍。在需要進行複雜數學運算或需要高精度結果的場景中，FP32 格式是首選。然而，高精度也意味著更多的內存使用和更長的計算時間。對於大規模深度學習模型，尤其是模型參數眾多且數據量龐大的情況下，FP32 格式可能導致 GPU 內存不足或推理速度下降。

在移動設備或物聯網設備上，我們可以將 Phi-3.x 模型轉換為 INT4，而 AI PC / Copilot PC 則可以使用更高的精度，例如 INT8、FP16、FP32。

目前，不同的硬件製造商有不同的框架來支持生成模型，例如 Intel 的 OpenVINO、Qualcomm 的 QNN、Apple 的 MLX 和 Nvidia 的 CUDA 等，結合模型量化完成本地部署。

在技術方面，量化後我們有不同的格式支持，例如 PyTorch / Tensorflow 格式、GGUF 和 ONNX。我對 GGUF 和 ONNX 的格式比較及應用場景進行了分析。在這裡，我推薦 ONNX 量化格式，因為它從模型框架到硬件都有良好的支持。在本章中，我們將重點使用 ONNX Runtime for GenAI、OpenVINO 和 Apple MLX 進行模型量化（如果您有更好的方法，也可以通過提交 PR 告訴我們）。

**本章包括**

1. [使用 llama.cpp 對 Phi-3.5 / 4 進行量化](./UsingLlamacppQuantifyingPhi.md)

2. [使用 onnxruntime 的生成式 AI 擴展對 Phi-3.5 / 4 進行量化](./UsingORTGenAIQuantifyingPhi.md)

3. [使用 Intel OpenVINO 對 Phi-3.5 / 4 進行量化](./UsingIntelOpenVINOQuantifyingPhi.md)

4. [使用 Apple MLX 框架對 Phi-3.5 / 4 進行量化](./UsingAppleMLXQuantifyingPhi.md)

**免責聲明**:  
本文件使用AI翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 進行翻譯。我們努力確保翻譯準確，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原文作為權威來源。如涉及關鍵資訊，建議尋求專業人工翻譯。我們對因使用本翻譯而引起的任何誤解或誤讀概不負責。