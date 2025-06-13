# 文件目录
```text
Image_Captioning_FLICKR8K/
├── dataset/
│   ├── images/            # Flickr8k 图像文件
│   ├── captions.txt       # 原始描述（image_id, caption）
│   ├── descriptions.json  # 清洗后的描述（由 caption_loader 生成）
│   ├── train.txt / test.txt  # 训练/测试集图像文件名
├── saved/
│   ├── glove.6B.50d.txt   # GloVe 词向量
│   ├── encoded_train_features.pkl  # 训练集图像编码（2048维）
│   ├── encoded_test_features.pkl   # 测试集图像编码
├── model_weights/
│   ├── model_epoch_*.pt   # 每轮保存的模型
│   ├── final_model.pt     # 最终训练好的模型
│   ├── metadata.pkl       # 保存 word_to_idx, idx_to_word, max_len
├── loss_history.json      # 训练过程中的损失记录
├── models/
│   └── caption_model.py   # 图像字幕生成模型定义（CNN+LSTM）
├── caption_loader.py      # 清洗原始 caption 文件并保存为 JSON
├── caption_preprocessor.py # 添加 <start>/<end> token，构建词表
├── vocab_builder.py       # 词频统计与词表生成工具
├── image_encoder.py       # 提取图像特征（ResNet-50）
├── train_improved.py      # 模型训练主脚本（推荐）
├── show_predictions.py    # 随机预测图像字幕并可视化展示
├── predict_caption.py     # 图像字幕生成函数
├── evaluate.py           # 使用 BLEU 分数评估模型表现
```

# 执行流程
## 1. caption_loader 
### 清洗文本
```text
输入文件：dataset/captions.txt
输出文件：dataset/descriptions.json
```
```text
python caption_loader.py
```

## 2. caption_preprocessor
### 构建词表、添加 <start> <end> token
```text
输入：descriptions.json, train.txt
输出：控制台显示词表大小（自动集成进训练）
```

```text
python caption_preprocessor.py
```

## 3. image_encoder
### 图像编码提取（ResNet-50）
```text
输入：images/, train.txt, test.txt
输出：encoded_train_features.pkl, encoded_test_features.pkl
```
```text
python image_encoder.py
```

## 4. train_improved
### 模型训练
```text
输出：
model_epoch_*.pt 每轮模型
final_model.pt 最终模型
metadata.pkl（用于预测）
loss_history.json
```

## 5. show_predictions
### 随机预测图像字幕并可视化展示
```text
python show_predictions.py
```

## 6. evaluate
```text
输出：BLEU-1 ~ BLEU-4 分数
```

```text
python evaluate.py
```
