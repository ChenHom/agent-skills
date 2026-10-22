# Examples

These examples illustrate structure and meaning preservation. They are not mandatory templates.

## General explanation

Original: 為了確保資訊在傳遞過程中的完整性，建議使用者於操作前先行確認相關資料是否已完成同步。

Clearer: 操作前，先確認資料已同步。這能降低使用不完整資料的風險。

Use “降低風險” rather than claiming that a sync check guarantees data integrity.

## Preserve conditions and certainty

Original: 如果備份已完成且校驗通過，可以刪除暫存檔；否則保留並通知管理員。

Clearer:
- 備份完成且校驗通過後，可以刪除暫存檔。
- 任一條件未滿足時，保留暫存檔並通知管理員。

Keep both conditions, the permission (“可以”), and the fallback. Do not change this into an unconditional deletion instruction.

## Work report

Vague: 本週持續優化處理流程，整體成效良好。

If records actually establish the following facts: 本週新增匯入前的欄位檢查。缺少必要欄位時，系統停止匯入並列出缺少的欄位。處理時間尚未量測。

Only use the concrete version when those facts are supplied or verified. Otherwise ask for needed facts or retain a clearly marked draft.

## Commit / PR

Vague: 改善 evidence 處理機制，提升可靠性。

If the actual diff establishes this behavior:

```text
fix: 將過期 evidence 判定為 unknown

原本的驗證器只檢查 evidence 是否存在。
新增有效期限檢查，讓過期 evidence 回傳 unknown。
必要 criterion 為 unknown 時，阻擋 DONE。
```

Add validation from actual execution records. The example does not establish that any test passed. A PR covering several commits should explain their combined behavior rather than concatenate their messages.

## Creative prose

Original: 雨停了，街道卻還醒著，招牌的光在水窪裡輕輕發抖。

Keep this sentence if it fits the intended voice. Do not mechanically rewrite it as “雨停了。街道有燈。水窪反射燈光。”
