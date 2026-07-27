# Ghostty 設定檔

我的 [Ghostty](https://ghostty.org) 終端機個人設定，位於 `~/.config/ghostty/config`。

- 測試環境：macOS（Darwin 25.5）
- Ghostty 版本：1.3.2（tip channel）

## 安裝

```bash
git clone git@github.com:stevecyj/ghostty.git ~/.config/ghostty
```

若 `~/.config/ghostty` 已存在，請先備份原本的 `config` 再覆蓋。

字型需要另外安裝：

```bash
brew install --cask font-jetbrains-mono-nerd-font
```

修改設定後按 <kbd>⌘</kbd>+<kbd>⇧</kbd>+<kbd>,</kbd> 即可重新載入，不必重開 Ghostty。

## 設定內容

完整設定如下：

```ini
font-family = JetBrainsMono Nerd Font
font-size = 15

theme = Dracula

copy-on-select = clipboard
clipboard-write = allow
clipboard-read = allow
window-save-state = always
macos-option-as-alt = true
```

### 字型

| 設定 | 值 | 說明 |
| --- | --- | --- |
| `font-family` | `JetBrainsMono Nerd Font` | 主要字型。Nerd Font 版本內建了 Powerlevel10k、eza、lazygit 等工具需要的圖示字元（glyph），少了它終端機會出現豆腐字。此選項可重複填寫以指定後備字型。 |
| `font-size` | `15` | 字級，單位為 point。 |

### 佈景主題

| 設定 | 值 | 說明 |
| --- | --- | --- |
| `theme` | `Dracula` | 使用 Ghostty 內建的 Dracula 配色。也可以填自訂主題名稱或主題檔的絕對路徑；若要依系統淺色／深色模式切換，語法為 `light:主題名,dark:主題名`。 |

執行 `ghostty +list-themes` 可預覽所有內建主題。

### 剪貼簿

| 設定 | 值 | 說明 |
| --- | --- | --- |
| `copy-on-select` | `clipboard` | 選取文字即自動複製。值為 `clipboard` 時會同時寫入系統剪貼簿與 selection clipboard（預設 `true` 只寫入 selection clipboard）。 |
| `clipboard-write` | `allow` | 允許終端機內的程式寫入系統剪貼簿，不跳出詢問視窗。 |
| `clipboard-read` | `allow` | 允許終端機內的程式讀取系統剪貼簿。Ghostty 預設是 `ask`（每次詢問），改成 `allow` 是為了讓 tmux、Neovim 等透過 OSC 52 存取剪貼簿的工具能順暢運作。 |

> [!NOTE]
> `clipboard-read = allow` 等於讓終端機裡跑的任何程式都能讀走剪貼簿內容（可能包含密碼）。若會在這台機器上執行來路不明的腳本，建議改回 `ask`。

### macOS 行為

| 設定 | 值 | 說明 |
| --- | --- | --- |
| `window-save-state` | `always` | 結束時永遠保存視窗狀態（位置、大小、分頁、分割），下次開啟自動還原。僅支援 macOS。 |
| `macos-option-as-alt` | `true` | 把 <kbd>⌥ Option</kbd> 當成 <kbd>Alt</kbd> 送給終端機程式，讓 <kbd>⌥</kbd>+<kbd>←</kbd>／<kbd>→</kbd> 之類的 Readline 與編輯器快捷鍵可用。代價是無法再用 Option 輸入 Unicode 特殊字元；若只想套用單邊，可改成 `left` 或 `right`。 |

## 參考

- [Ghostty 官方設定參考文件](https://ghostty.org/docs/config/reference)
- 本機查詢所有選項與預設值：`ghostty +show-config --default --docs`
