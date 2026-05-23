# TSV File Viewer (s1131501_林昱綸_TSV)

## 專案簡介

這是一個以 **Windows Forms (.NET)** 開發的 TSV（Tab-Separated Values）單字檔案檢視器，
可讀取 `.tsv` 或 `.txt` 格式的單字資料，並以清單方式顯示單字、音標、音檔路徑與解釋。

---

## 功能特色

- 開啟 `.tsv` / `.txt` 單字檔案
- 以 ListView 顯示單字清單（單字、音標、音檔路徑、解釋）
- 顯示已載入單字數量
- 關於視窗（About）
- 關閉視窗前確認提示

---

## 專案結構
s1131501_林昱綸_TSV/
├── frmTSVFile.cs         # 主視窗邏輯（開啟檔案、更新 ListView、結束程式）
├── frmTSVFile.Designer.cs
├── frmAbout.cs           # 關於視窗
├── WordItem.cs           # 單字資料類別（Word / Phonogram / SoundPath / Explain）
├── WordCollection.cs     # 單字集合類別，繼承 Collection<WordItem>
└── Program.cs            # 程式進入點
---

## 類別說明

### `WordItem`
代表一筆單字資料，由 TSV 單行字串建構。

| 屬性 | 型別 | 說明 |
|------|------|------|
| `Word` | string | 單字 |
| `Phonogram` | string | 音標 |
| `SoundPath` | string | 音檔路徑 |
| `Explain` | string | 解釋（支援多欄位合併） |

建構子接受一行 TSV 字串，以 `\t` 分隔後依序指派各屬性。  
第 4 欄（index 3）之後的內容會以換行合併為解釋欄位。

---

### `WordCollection`
繼承 `Collection<WordItem>`，提供從字串陣列批次載入資料的方法。

| 方法 | 說明 |
|------|------|
| `LoadFromStringArray(string[] lines)` | 清空現有資料，逐行建立 `WordItem` 並加入集合 |

---

### `frmTSVFile`（主視窗）
| 方法 | 說明 |
|------|------|
| `UpdateListView()` | 將 `_WordList` 的資料更新至 ListView |
| `tsmiOpen_Click` | 開啟檔案對話框，讀取 TSV/TXT 並載入 |
| `tsmiExit_Click` | 關閉程式 |
| `tsmiAbout_Click` | 顯示關於視窗 |
| `frmTSVFile_FormClosing` | 關閉前顯示確認對話框 |

---

## TSV 檔案格式

每行一筆資料，欄位以 **Tab (`\t`)** 分隔，檔案編碼為 **UTF-8**：
單字[TAB]音標[TAB]音檔路徑[TAB]解釋
apple[TAB][ˈæpl][TAB]audio/apple.mp3[TAB]蘋果
| 欄位順序 | 欄位名稱 | 說明 |
|----------|----------|------|
| 0 | Word | 英文單字 |
| 1 | Phonogram | 音標 |
| 2 | SoundPath | 音檔相對路徑 |
| 3+ | Explain | 中文解釋（多欄合併） |

---

## 使用方式

1. 啟動程式
2. 點選選單 **檔案 → 開啟**
3. 選擇 `.tsv` 或 `.txt` 格式的單字檔案
4. 單字清單顯示於 ListView，狀態列顯示載入數量
5. 點選 **檔案 → 離開** 或關閉視窗結束程式（會出現確認提示）

---

## 開發環境

- **語言：** C#
- **框架：** .NET Windows Forms
- **編碼：** UTF-8

---

## 作者

**林昱綸**　學號：s1131501
