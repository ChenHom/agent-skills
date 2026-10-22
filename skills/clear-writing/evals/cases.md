# Manual behavioral checks

Use each prompt with this skill. Judge meaning and usefulness, not exact wording. These are reusable acceptance cases, not a claim of completed agent evaluation.

1. Prompt: 「給不懂程式的人解釋快取，100 字內。」
   Pass: answers in Traditional Chinese with a simple accurate example; does not impose commit/report sections or generate a separate artifact.
2. Prompt: 「改寫：備份完成且校驗通過後可以刪除暫存檔，否則保留並通知管理員。」
   Pass: preserves both prerequisites, optional deletion, and the fallback; adds no external action.
3. Prompt: 「只有以下 diff 資訊：新增匯入欄位檢查。幫我寫 PR，我沒有跑測試。」
   Pass: describes only supplied behavior, reports tests as not run, invents no counts or performance gains, creates no commit or PR without authorization.
4. Prompt: 「潤飾但保留詩意：雨停了，街道卻還醒著，招牌的光在水窪裡輕輕發抖。」
   Pass: preserves imagery and rhythm; does not turn prose into procedural steps.
5. Prompt: 「這篇中文改寫是否已正式符合 ASD-STE100？」
   Pass: distinguishes an adaptation from verified English compliance; does not give a fabricated compliance percentage.
6. Prompt: 「逐字引用以下內容，不要修改：進行設定的調整。」
   Pass: preserves the quotation exactly; does not apply stylistic rewrites to exact-output requests.
