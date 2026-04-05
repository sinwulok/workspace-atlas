# amc-amr-gff-nn

AMC AMR Gated Fusion Former neural network for automatic modulation recognition.

---

## Overview

Production version of the AMR_GateFusionFormer neural network. The gating mechanism functions as a signal-to-noise ratio-aware routing system, prioritizing frequency features (STFT) under high SNR conditions and structural preservation features (S-TD/IQ) under heavy noise conditions.

---

## Category / Lifecycle / Tags

- **Category**: Development
- **Type**: Deep Learning | Neural Network
- **Lifecycle**: stable
- **Tags**: deep-learning, neural-network, gated-fusion-former, automatic-modulation-recognition

---

## Dataset

This project uses [RadioML 2016.10a (RML2016.10a)](https://www.deepsig.ai/datasets).
After downloading and extracting, use `RML2016.10a_dict.pkl` as the `--data` parameter.

---

## Model Architecture

GatedFusionFormer NeuralNetwork fuses three modality features:

```
IQ Signal  (2, T)   → Conv1d Embedding
STFT Map   (1,32,T) → 2D Conv + Freq-Adaptive Pool
S-TD Stats (2, T)   → Conv1d Embedding
                           ↓
              GatingNetwork (dynamic fusion weights)
                           ↓
              FusionTransformerBlock × depth
              (Conv Encoder + Multi-Head Attention)
                           ↓
                    Linear Classifier
```

See [`model.py`](model.py) for details.

---

## Structure

```
amc-amr-gff-nn/
├── assets/
├── src/
│   ├── __init__.py
│   ├── run.py                 # CLI / subcommands entrypoint
│   ├── export.py              # Model export / ONNX / TorchScript (optional)
│   ├── utils.py               # Shared utilities (IO, plotting, metrics)
│   ├── configs/
│   │   └── config.py          # Default settings / hyperparams
│   ├── core/                  # Analysis/experiment modules
│   │   ├── dataset.py
│   │   ├── evaluate.py
│   │   ├── deep_analysis.py
│   │   ├── ablation.py
│   │   ├── gating_weights.py
│   │   └── cnn_vs_transformer.py
│   └── models/
│       ├── factory.py         # build_model(...)
│       ├── model.py
│       ├── gff_nn.py
│       └── cnn2.py / mod_rec_net.py
├── README.md
```

---

## Dependencies

```bash
pip install torch torchvision timm scipy scikit-learn matplotlib seaborn tqdm pandas
```

---

## How to Run

All scripts share the same two required parameters:

| Parameter | Description |
|---|---|
| `--weights` | Trained model weights file (.pth) — required |
| `--data` | Full path to RML2016.10a_dict.pkl — required |

Optional parameters:

| Parameter | Default | Description |
|---|---|---|
| `--batch-size` | 256 | Inference batch size |
| `--output-dir` | `outputs` | Chart output directory |
| `--device` | auto | `cpu` or `cuda` (auto-detected) |

---

## Experiments

### `evaluate.py` — Basic Model Evaluation

```bash
python src/run.py evaluate --weights path/to/model.pth --data path/to/RML2016.10a_dict.pkl --batch-size 256
```

**輸出：**
- `confusion_matrix_counts.png` — 原始計數混淆矩陣
- `confusion_matrix_normalized.png` — 歸一化混淆矩陣
- `accuracy_vs_snr.png` — 整體 Accuracy vs SNR

---

### `deep_analysis.py` — 深度性能分析

```bash
python src/run.py deep_analysis --weights model.pth --data RML2016.10a_dict.pkl
```

**輸出：**
- `per_class_accuracy_vs_snr.png` — 各類別 Accuracy vs SNR
- `confused_categories_high_snr.png` — 高 SNR 易混淆類別柱狀圖
- `tsne_visualization.png` — t-SNE 特徵空間可視化（低 / 高 SNR）

![per_class_acc_vs_snr](assets/per_class_acc_vs_snr.png)
![tsne_visualization](assets/tsne_visualization.png)
---

### `ablation.py` — 模態消融實驗

```bash
python src/run.py ablation --weights model.pth --data RML2016.10a_dict.pkl
```

**輸出：**
- `ablation_single_modality.png` — 單模態消融 Accuracy vs SNR
- `ablation_pairwise_modality.png` — 成對模態消融 Accuracy vs SNR
- `ablation_confused_categories.png` — 高 SNR 易混淆類別對比

![ablation_single_modality](assets/ablation_single_modality.png)
![ablation_pairwise_modality](assets/ablation_pairwise_modality.png)


---

### `gating_weights.py` — 門控網絡權重分析

```bash
python src/run.py gating --weights model.pth --data RML2016.10a_dict.pkl
```

**輸出：**
- `gating_weights_vs_snr.png` — IQ / STFT / S-TD 模態重要性 vs SNR

![gating_weights_vs_snr](assets/gating_weights_vs_snr.png)

---

### TODO:
### `cnn_vs_transformer.py` — CNN vs Transformer 對比

```bash
python src/run.py compare --weights model.pth --data RML2016.10a_dict.pkl
```

**輸出：**
- `gffnn_compare_acc.png` — 整體 Accuracy vs SNR 對比折線圖
- `gffnn_compare_overall.png` — 整體準確率柱狀圖



---

（若 prefer module run）
```bash
python -m src.run evaluate --weights ... --data ...
```

---

## 輸出說明

- 所有圖表、可視化結果、CSV、與 logs 會儲存在 `--output-dir` 指定的目錄（預設 `outputs/`）。
- 常見輸出檔例：
  - `confusion_matrix_counts.png`
  - `confusion_matrix_normalized.png`
  - `accuracy_vs_snr.png`
  - `per_class_accuracy_vs_snr.png`
  - `tsne_visualization.png`
  - `gating_weights_vs_snr.png`
  - `ablation_*.png`
  - `cnn_vs_transformer_accuracy.png`

### 程式化呼叫（當作 library 使用）

如果你想在其他程式中直接使用模型或 pipeline，可以匯入 factory 與工具函式：
```python
from src.models.factory import build_model
from src.core.dataset import RMLDataset
from src.utils import load_weights, predict_batch

# 建構模型
model = build_model(name="gff_nn", num_classes=11)
# 載入權重
load_weights(model, "path/to/model.pth")
# 資料/推理
dataset = RMLDataset("path/to/RML2016.10a_dict.pkl", split="test")
preds = predict_batch(model, dataset, device="cuda")
```
（上述 API 名稱為範例；請以實際 code 中的 function/class 名稱為準）

---

### Maintenance & Development Recommendations

- Apply unittest / pytest to CLI subcommands to ensure behavior consistency after refactoring
- Move config (hyperparameters) to YAML/JSON with version tracking for reproducible experiments
- Annotate compatibility between model factory and config to reduce configuration errors

### Version History

- README.v4.md — This file (modular / production-friendly)

---

## Related Links

- [Project Catalog](../../catalog/index.md)
- [Repository Root](../../README.md)
