# RoboModels

獨立的 **3D 模型庫**（機械臂 CAD／網頁預覽資產），供 [RoboArm](https://github.com/BenYung-Git/RoboArm) 等應用程式以本機路徑讀取。

本 repository **不是** RoboArm 的子目錄，也不應併入 RoboArm 的 Git 歷史。

## 用途

- 集中存放各廠牌／機型的 CAD 來源與衍生的網頁靜態模型（例如 GLB）。
- 讓 RoboArm 透過「系統設定 → 附件路徑」指向本庫根目錄後，再依相對路徑載入已允許的檔案。
- 僅作為**靜態模型庫**：不包含應用程式資料庫、存貨資料，也不包含「存貨 ↔ 附件」關聯紀錄。

## 目錄結構（目前）

```text
RoboModels/
├── Jaka/
│   ├── zu5/          # 預留
│   └── zu7/
│       ├── 20260312142902A064.zip          # 原廠下載封裝（來源資產）
│       ├── cad/
│       │   └── JAKA Zu 7-V2.0_20231016.STEP
│       └── web/
│           ├── zu7_assembly.glb            # 由 STEP 轉出的靜態預覽
│           ├── manifest.json
│           ├── zu7_aabb_reconcile.json
│           └── zu7_check_report.json
└── Rokae/            # 預留（目前無檔案）
```

路徑與檔名應保持穩定；RoboArm 以「附件根目錄 + 相對 Path/File」定位，不應依賴本機絕對路徑。

## 在 RoboArm 中設定路徑

1. 將本庫 clone／同步到主機（Windows 建議 `C:\RoboModels`；Linux 依部署自訂絕對路徑）。
2. 開啟 RoboArm → **系統設定 → 附件路徑**。
3. 分別填寫／驗證 Windows 與 Linux 的模型庫根目錄，儲存後以後端實際 OS 選用生效路徑。
4. 存貨「各類附件」僅**登記**根目錄內既有檔案的相對位置；不會上傳、複製或搬移本庫檔案。
5. 虛擬測試頁的 Zu7 CAD 預覽亦從此根目錄下的允許相對路徑讀取 GLB（與存貨附件關聯無關）。

本庫**不包含**：

- RoboArm SQLite／設定 DB
- 存貨或 `attachment` 表的正式關聯資料
- Workflow、真機連線狀態

## 靜態模型限制

- GLB／STEP 用於**靜態顯示與量測參考**，不代表真機同步、關節動畫驗證或運動學已校準。
- 轉檔過程中的單位／座標系轉換已記錄於 `web/manifest.json` 等衍生檔；前端不應擅自再套用 mm→m 或 Z-up→Y-up。
- 空目錄（如 `Rokae/`、`Jaka/zu5/`）僅作預留，Git 不會追蹤空資料夾。

## 授權與再分發（請先確認）

遠端 repository 目前為 **Public**。

| 資產 | 已知來源（事實描述） | 授權／再分發 |
|------|----------------------|--------------|
| `Jaka/zu7/*.zip`、`.STEP` | 檔名與封裝顯示為 **JAKA Zu 7** 相關 CAD；由使用者取得之原廠／供應封裝解壓而來 | **原廠模型授權與公開再分發權限尚未確認**；本 README **不**宣稱其為 MIT、Apache 或其他開源授權 |
| `Jaka/zu7/web/zu7_assembly.glb` 及相關 JSON | 本機以 CadQuery／OCP 等工具自上述 STEP **衍生**的預覽與檢查產物 | 衍生檔是否可公開，仍取決於**來源 STEP／ZIP 的授權條款**；工具本身的授權≠模型資產授權 |
| 轉檔工具（CadQuery 等） | 僅出現在衍生 JSON 的工具／套件授權欄位 | 與 JAKA 模型權利分離，不得據此推論模型可開源再分發 |

公開 push 前請確認：是否允許將原廠 STEP／ZIP（及由其產生的 GLB）放在 Public GitHub。若未確認，請改為 Private，或自公開範圍移除受限檔案。

## Git 說明

- 一般 Git 追蹤；**目前未使用 Git LFS**。
- `.STEP`／`.glb`／`.zip` 以 binary 屬性處理（見 `.gitattributes`）。
- 勿將暫存、cache、log、備份提交進庫（見 `.gitignore`）。
