# Project 01 - Favorites

實作一個將使用者最愛的數字、顏色和興趣儲存在區塊鏈上的 Solana 程式。

## 🎯 專案目標

學習 Solana 程式開發的基礎概念：
- 使用 Anchor 框架開發 Solana 程式
- 建立和管理 PDA (Program Derived Address)
- 處理帳戶初始化和資料儲存
- 撰寫和執行測試

## 🔧 技術堆疊

- **Solana**: 區塊鏈平台
- **Anchor**: Solana 開發框架  
- **Rust**: 程式語言
- **TypeScript**: 測試和客戶端
- **Node.js**: 開發環境

## 📋 功能特色

### 主要功能
- ✅ 儲存使用者最愛的數字 (u64)
- ✅ 儲存使用者最愛的顏色 (String, 最多 50 字元)
- ✅ 儲存使用者的興趣列表 (Vec<String>, 最多 5 項，每項最多 50 字元)
- ✅ 使用 PDA 為每個使用者建立獨特的帳戶

### 程式指令
- `set_favorites`: 設定或更新使用者的最愛資料

## 🏗️ 專案結構

```
project-01-favorites/
├── programs/
│   └── favorites/
│       └── src/
│           └── lib.rs          # 主要程式邏輯
├── tests/
│   └── anchor.ts               # 測試檔案
├── client/
│   └── client.ts               # 客戶端範例
├── app/                        # 前端應用程式
├── Anchor.toml                 # Anchor 配置
├── Cargo.toml                  # Rust 專案配置
└── package.json                # Node.js 依賴

```

## 🚀 快速開始

### 環境需求
- Solana CLI (1.14.16+)
- Anchor CLI (0.29.0+)
- Node.js (16+)
- Rust (1.70+)

### 安裝與執行

1. **安裝依賴**
   ```bash
   yarn install
   ```

2. **建構程式**
   ```bash
   anchor build
   ```

3. **執行測試**
   ```bash
   anchor test
   ```

4. **部署到本地測試網**
   ```bash
   # 啟動本地驗證器
   solana-test-validator
   
   # 部署程式
   anchor deploy
   ```

## 📝 程式架構

### Favorites 結構體
```rust
pub struct Favorites {
    pub number: u64,           // 最愛的數字
    pub color: String,         // 最愛的顏色 (最多 50 字元)
    pub hobbies: Vec<String>   // 興趣列表 (最多 5 項)
}
```

### PDA 種子
- 種子: `["favorites", user.key()]`
- 每個使用者都有唯一的 Favorites 帳戶

## 🧪 使用範例

### 呼叫 set_favorites 指令
```typescript
await program.methods
  .setFavorites(
    new BN(42),                    // 最愛的數字
    "藍色",                        // 最愛的顏色
    ["程式設計", "音樂", "旅行"]      // 興趣列表
  )
  .accounts({
    user: userPublicKey,
    favorites: favoritesPda,
    systemProgram: SystemProgram.programId,
  })
  .rpc();
```

## 📚 學習重點

1. **PDA (Program Derived Address)**
   - 理解如何使用種子生成確定性地址
   - 學習 `init_if_needed` 的使用時機

2. **Anchor 框架**
   - 帳戶驗證和約束
   - 自動序列化和反序列化
   - 空間計算和租金處理

3. **Solana 程式結構**
   - 指令處理器的實作
   - 帳戶結構定義
   - 錯誤處理

## 🎓 延伸學習

- [ ] 添加 `get_favorites` 查詢指令
- [ ] 實作興趣的增刪功能
- [ ] 添加權限控制
- [ ] 建立前端界面
- [ ] 部署到 Devnet

## 🐛 除錯說明

常見問題及解決方法：

1. **程式 ID 不匹配**
   ```bash
   anchor keys sync
   ```

2. **帳戶不存在**
   - 確認 PDA 計算正確
   - 檢查種子是否一致

3. **空間不足**
   - 檢查 `INIT_SPACE` 計算
   - 確認字串長度限制

--------------------------------
# github 插曲
```bash
本地 commit ──→ [衝突] ←── GitHub 上的 commit
                    ↓
                解決衝突後
                    ↓
            git rebase --continue
```