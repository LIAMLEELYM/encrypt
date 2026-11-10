# CRYPT//LOCAL

單文件、純瀏覽器的文字加解密工具。所有運算都在本機完成,不上傳任何資料。
A single-file, browser-only text encryption tool. Everything runs locally; nothing is uploaded.


---

## 中文

### 功能
- 使用密碼短語加密與解密文字
- AES-256-GCM 認證加密,密碼錯誤或密文被改動時會直接解密失敗
- 密碼強度提示、複製結果、中英文切換、兩種配色主題
- 單一 `index.html`,無後端、無依賴、無第三方腳本

### 安全設計
| 項目 | 實作 |
|---|---|
| 加密算法 | AES-256-GCM(Web Crypto API) |
| 密鑰導出 | PBKDF2-SHA256,600,000 次迭代 |
| Salt / IV | 每次加密隨機生成(16 / 12 位元組) |
| 密文格式 | Base64( 版本(1) ‖ salt(16) ‖ IV(12) ‖ 密文+認證標籤 ) |
| 網路隔離 | CSP 設為 `default-src 'none'`,頁面無法對外連線 |

### 使用方法
1. 輸入密碼短語(建議 5 個以上隨機單詞)
2. 貼上明文,按「加密」,把輸出的字串傳給對方
3. 對方輸入相同密碼短語,貼上密文,按「解密」
4. **密碼請透過另一個渠道傳送**(例如電話口述),不要和密文走同一個平台

### 限制與威脅模型(請務必閱讀)
- **未經第三方安全審計**,僅供學習與輕量用途。高風險場景請使用 Signal、age 或 GPG。
- 只保護內容,**不隱藏元數據**(誰、何時、與誰聯絡)。
- **沒有前向保密**:密碼一旦洩漏,所有用該密碼加密的密文都可被解開。
- 安全性取決於密碼強度,弱密碼可被離線暴力破解。
- 無法防禦已被入侵的裝置(木馬、鍵盤記錄器、惡意瀏覽器擴充功能)。
- 使用線上版時,你需要信任託管方每次載入的代碼。需要更高保障請下載離線版使用。
- 不支援文件加密,過大的文字可能影響效能。

### 離線使用(建議)
下載 `index.html`,斷網後用瀏覽器直接開啟即可。

### 部署
Settings → Pages → Deploy from a branch → `main` / root。GitHub Pages 預設使用 HTTPS,可滿足 Web Crypto 的要求。

### 授權
MIT License

---

## English

### Features
- Encrypt and decrypt text with a passphrase
- AES-256-GCM authenticated encryption: wrong passphrase or tampered ciphertext fails to decrypt
- Passphrase strength meter, copy button, ZH/EN toggle, two themes
- One `index.html`, no backend, no dependencies, no third-party scripts

### Security design
| Item | Implementation |
|---|---|
| Cipher | AES-256-GCM (Web Crypto API) |
| Key derivation | PBKDF2-SHA256, 600,000 iterations |
| Salt / IV | Random per encryption (16 / 12 bytes) |
| Format | Base64( version(1) ‖ salt(16) ‖ IV(12) ‖ ciphertext+tag ) |
| Network isolation | CSP `default-src 'none'` blocks all outbound requests |

### Usage
1. Enter a passphrase (5+ random words recommended)
2. Paste plaintext, click Encrypt, send the output string
3. The recipient enters the same passphrase, pastes the ciphertext, clicks Decrypt
4. **Share the passphrase through a different channel** than the ciphertext

### Limitations and threat model
- **Not independently audited.** For learning and light use only. For high-risk use, prefer Signal, age, or GPG.
- Protects content only; **metadata is not hidden**.
- **No forward secrecy**: if a passphrase leaks, everything encrypted with it can be decrypted.
- Security depends on passphrase strength; weak passphrases can be brute-forced offline.
- Cannot defend against a compromised device or malicious browser extensions.
- With the hosted version you must trust the code served on each load. Use the offline copy for higher assurance.
- No file encryption; very large text may be slow.

### Offline use (recommended)
Download `index.html` and open it in a browser with the network disconnected.

### License
MIT License
