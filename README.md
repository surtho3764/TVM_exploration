# TVM_exploration
TVM stack exploring the deep-learning frameworks 
這是我探索的note

# 介紹
將深度學習網路部署到平台例如mobile phones, IoT, and specialized accelarators(FPGAs, ASICs) 都需要進行優化。
TVM提供是一個端到端優化的深度學習編譯器，它具有
- graph級別的優化
- 算子級別的優化
- 為跨不同硬體後端的深度學習工作提供移植。


# 深度學習編譯器(簡單概述)
Source: TVM: An Automated End-to-End Optimizing Compiler for Deep Learning

TVM可以從TensorFLow,PyTorch或ONNX等框架導入模型，導入後會被TVM翻譯成高級模型語言Relay (high-level IR)。
針對Relay高階中間表達式TVM可以透過pass來優化計算圖。

針對高階中間表達式Relay，可以通過FuseOps pass，把計算圖模型劃分為許多小的子圖，並將子圖降級為 TE 表示。張量表達式（TE）是一種用於描述張量計算的領域特定語言。 TE 還提供了幾個 schedule 原語來指定底層循環優化，例如循環切分、向量化、張量化、循環展開和融合。為將 Relay 表示轉換為 TE 表示，TVM 包含了一個張量算子清單（TOPI），其中包含常用張量算子的預定義模板（例如，conv2d、transpose)。

TVM提供auto-tuning和AutoScheduler兩種方法，讓我們可以替TE中定義的算子或子圖搜索出最佳的算子或子圖底層循環優化稱為搜索最佳 schedule。

基於最佳schedule配置後，所有TE子圖可以降為TIR表達式(lower-)，並通過低層優化pass來進行優化，優化後的TIR可以透過關鍵的CodeGen，將TIR (low-level IR)生成可以部署到production環境的優化模型的最終程式碼。TVM低層支援多種不同的編譯器後端例如(LLVM)。

一般來說深度學習編譯器提供圖編譯器和算子編譯器兩種優化，讓我們可以針對計算圖和算子進行優化稱前端優化，之後轉換為low-level IR後，可以進行後端的優化，如依據各大廠平台自身的硬件設備、指令集、內核庫來進行後端優化。

# graph level and tensor operator level

## graph level
* OP Fusion
* Data Layout Transformation
* Memory Allocation
* Constant Fold
* Common Subexpression Elimination
* Dead Code Elimination



## tensor operator

* Loop Optimization
** Loop Unrolling
** Loop Tiling
** Loop Fusion
** Loop Reorder
** Loop Split
* Instructions Optimization
* Memory Optimization

# Test Benchmark scripts for TVM
## cpu (intel)
* AutoTVM


* AutoScheduler



## Nvidia GPU
* AutoTVM


* AutoScheduler