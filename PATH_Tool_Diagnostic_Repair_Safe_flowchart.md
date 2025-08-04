## PATH_Tool_Diagnostic_Repair_Safe.ps1 - 操作流程圖

```mermaid
flowchart TD
    A[啟動腳本] --> B{是否有管理員權限？}
    B -- 是 --> C[初始化 GUI 與中斷監控器]
    B -- 否 --> D[請求提升權限]
    D --> D1{提權是否成功？}
    D1 -- 是 --> C
    D1 -- 否 --> E1[提示「需管理員權限」並退出]
    
    C --> Z[中斷監控器啟動 (全程監聽 Ctrl-C)]
    Z -->|檢測到中斷| M[觸發中斷處理]
    
    C --> E[掃瞄 PATH 環境變數]
    note over E: 這些階段均可被 Ctrl-C 中斷
    E --> F{是否發現問題？}
    F -- 否 --> G[顯示「無需修復」訊息]
    F -- 是 --> H[建立備份點]
    note over H: 這些階段均可被 Ctrl-C 中斷
    H --> I[執行修復操作]
    note over I: 這些階段均可被 Ctrl-C 中斷
    I --> J[記錄操作日誌]
    note over J: 這些階段均可被 Ctrl-C 中斷
    J --> L[完成修復並顯示結果]
    
    M --> N[自動回滾至備份狀態]
    N --> O[提示使用者恢復選項]
    
    style Z fill:#f9f,stroke:#333,stroke-width:2px
```
