# API 開發規範

本文件定義API開發時的命名與回應格式，為了確保整體API的一致性、可讀性與維護性。

## 目錄

- [路徑 & 標頭](#路徑--標頭)
  - [路徑](#路徑)
  - [標頭](#標頭)
- [Request格式](#request格式)
  - [Route Param & Query String](#route-param--query-string)
  - [Request Body (JSON)](#request-body-json)
- [Response格式](#response格式)
  - [Status Code：200 (成功)](#status-code200-成功)
  - [Status Code：400 (錯誤請求)](#status-code400-錯誤請求)
  - [Status Code：500 (伺服器錯誤)](#status-code500-伺服器錯誤)
- [總結](#總結)

---

## 路徑 & 標頭

### 路徑
- **API路徑** 使用 **kebab-case** 命名。

**範例：**
```
GET - /api/v1/points-plan
```
### 標頭
| Key              | Value                  |
|------------------|------------------------|
| Content-Type     | `application/json`     |
| Accept           | `application/json`     |
| Authorization    | `Bearer {token}`       |

---

## Request格式

### Route Param & Query String
- **路由參數(Route Param)** 與 **查詢參數(Query String)** 使用 **camelCase** 命名。

**範例：**
```
GET /api/v1/activities/search?city=新北市&level=初階&participants=20
```

### Request Body (JSON)
- 所有欄位 key 使用 **camelCase**。

**範例：**
```json
{
  "id": "0793cf35-b550-498d-9ab1-9a54517a1241",
  "currentCount": 5,
  ...
}
```

---

## Response格式

### Status Code：200 (成功)
- 所有欄位 key 一律使用 **camelCase**。
- 最外層欄位為 `message`, `data`
- `message` 欄位表示回應狀態。
- `data` 欄位可包含巢狀物件、陣列與分頁資訊。
- `data` 欄位可包含單筆資料或多筆資料。
- `item` 欄位包含單筆資料。
- `items` 陣列包含多筆資料。
- `pagination` 物件包含分頁資訊，如 `totalPage`, `currentPage` 等。

**範例：**
- 單筆
```json
{
  "message": "成功",
  "data": {
    "item": { ... }
  }
}
```
- 多筆
```json
{
  "message": "成功",
  "data": {
    "items": [ ... ],
    "pagination": { 
      "totalPage": 10,
      "currentPage": 1 
    }
  }
}
```
- 無需回傳結果時，`data` 欄位設為 `null`。
```json
{
  "message": "成功",
  "data": null
}
```

---

### Status Code：400 (錯誤請求)
- 表示輸入條件錯誤或驗證未通過。
- 僅回傳 `message` 欄位。

**範例：**
```json
{
  "message": "請輸入正確的條件"
}
```

---

### Status Code：500 (伺服器錯誤)
- 表示伺服器發生未預期錯誤。
- 僅回傳 `message` 欄位。

**範例：**
```json
{
  "message": "伺服器錯誤"
}
```

---

## 總結

| 項目              | 命名方式            |
|------------------|--------------------|
| Content-Type     | `application/json` |
| Accept           | `application/json` |
| Authorization    | `Bearer {token}`   |
| API路徑           | kebab-case        |
| 路由參數          | camelCase          |
| 查詢參數          | camelCase          |
| Request Body     | camelCase          |
| Response         | camelCase          |
| 成功回應 (200)    | `message`, `data`  |
| 錯誤回應（400）    | `message`          |
| 錯誤回應（500）    | `message`          |

---
