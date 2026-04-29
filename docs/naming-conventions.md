# 命名規範 | Naming Conventions

## 專案命名 | Project Naming

### 原則 | Principles

- 使用小寫字母與連字符（kebab-case）
- 名稱應具描述性，能反映專案內容
- 避免過長的名稱（建議不超過 50 個字元）
- 使用英文命名

### 範例 | Examples

- ✅ `cnogb-abnormal-intervention`
- ✅ `cnpbb-abnormal-drift`
- ✅ `machine-learning-applications-in-fmri`
- ✅ `r3f-portfolio`
- ❌ `MyProject`（應使用 kebab-case）
- ❌ `proj1`（缺乏描述性）

## 目錄命名 | Directory Naming

### 頂層目錄 | Top-Level Directories

- `research/` - 全小寫，單數形式
- `development/` - 全小寫，單數形式
- `other/` - 全小寫，單數形式
- `catalog/` - 全小寫
- `docs/` - 全小寫

### 專案內部目錄 | Project Internal Directories

遵循各專案使用的技術棧慣例，不強制統一規範。

## 檔案命名 | File Naming

### 文件檔案 | Documentation Files

- 使用 kebab-case: `migration-plan.md`
- 使用描述性名稱: `architecture.md`, `governance.md`
- 不以全大寫（ALL CAPS）提升 AI/LLM 可讀性；語意清楚的標題、段落與清楚檔名更重要

### 設定檔 | Configuration Files

- 遵循工具慣例: `projects.yml`, `tags.yml`
- 使用小寫與連字符或底線

## 標籤命名 | Tag Naming

- 使用小寫字母與連字符
- 簡潔明瞭，避免縮寫
- 範例: `data-science`, `machine-learning`, `frontend`
