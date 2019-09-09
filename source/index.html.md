---
title: API Reference Test

language_tabs: # must be one of https://git.io/vQNgJ
  - json
  - shell
  - ruby
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

聲林之王，網站會員系統 API

# Facebook 登入

Facebook 登入用連結：

`https://www.facebook.com/v4.0/dialog/oauth?client_id=<APP-ID>&redirect_uri=<REDIRECT-URI>`

<aside class="notice">
使用 Facebook 登入了話，需要到 facebook app 設定 Facebook Login 白名單
</aside>

## 建立新使用者

建立會員，並回傳新的使用者的資料

### Facebook Login

### HTTP Request

`GET /auth/facebook/login?code=<CODE>&redirect_uri=<REDIRECT URI>`

### Query Parameters

Parameter | require | Description
--------- | ------- | -----------
code | true | Facebook 登入後取得的驗證碼
redirect_uri | true | If set to false, the result will include kittens that have already been adopted.

# Private me
Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).
Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`token: xxxxx`

<aside class="notice">
  Private 的相關 API 操作， 皆需帶入當前使用者的 token 才可進行操作
</aside>

## 取得個人資料

### HTTP Request

`GET /private/me.json&token=<TOKEN>`


```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 更新個人資料

### HTTP Request
`PUT /private/me.json&token=<TOKEN>`

### Body Parameters

Parameter | require | Description
--------- | ------- | -----------
avatar_data | false | 更新使用者個人大頭貼
group_name | false | 更新使用者加入的隊伍 blue、red、yellow (只允許更新一次)
nick_name | false | 使用者自訂玩家的名稱

```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 上傳 OG 分享圖

### HTTP Request
* method: GET
* URL: https://share.junglevoicewar.tw/users/7/share/avatar?entertain_code=xxx
備註： og 圖片上傳後，使用 user { id,  entertain_code} 組合出分享連結，當連結被請求時，追蹤碼的所有者會加入對應的分數

### HTTP Request
`PUT /private/me/ogimage&token=<TOKEN>`

### Query Parameters

Parameter | require | Description
--------- | ------- | -----------
base64 | true | base64
category | true | 對應不同的遊戲分類 (avatar, guess_song)

```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 新增 使用者分數 獲得點數的交易紀錄

`POST /private/me/point?token=<TOKEN>`

### Body Parameters

Parameter | require | Description
--------- | ------- | -----------
task_name | true | 獲得分數的任務名稱

```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 新增 使用者分數 花費點數的交易紀錄

`POST /private/me/buy?token=<TOKEN>`

### Body Parameters

Parameter | require | Description
--------- | ------- | -----------
product_name | true | 購買商品的名稱 `name`

```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 新增 使用者團隊分數 獲得點數交易紀錄

`POST /private/me/group_point?token=<TOKEN>`

### Query Parameters

Parameter | require | Description
--------- | ------- | -----------
task_name | true | 獲得分數的 團隊任務名稱
category | false | 團隊任務類型
lv | false | 如果 category 為 game 時，要給予對應遊戲成績的分數

```json
{
   "id": Number ,
   "name": String,
   "nick_name": String,
   "email": String,
   "point": Number,
   "entertain_code": String,
   "friend_entertain_code": String,
   "point_entertain_transactions": Array,
   "props": Array,
   "token": String,
   "group": {
       "id": Number,
       "name": String,
       "name_zh": String,
       "updated_at". timestamp,
       "created_at". timestamp
   }
}
```

## 更新好友招待碼

`PUT me/friend_entertain_code`

### Body Parameters

Parameter | require | Description
--------- | ------- | -----------
code | true | 朋友招待碼

# User

## 取得人使用者參與人數

`GET /users/count`

```json
{
   "data": Number
}
```

## 取得使用者列表

### HTTP Request

`GET /private/me.json&token=<TOKEN>`

### Query Parameters

Parameter | require | Description
--------- | ------- | -----------
preview | true | 每頁顯示資料數
page | true | 頁數
order_by | true | 排序參考欄位 `point`
sort: | true | 排序方式 `asc`、`desc`
group_id | false | 篩選對應的 group


```json
{
   "data": [
       {
           "id": Number,
           "name": String,
           "group_zh": String,
           "point": Number,
           "group_point": Number
       }
   ]
}
```

# Group

## 取得隊伍資訊

### HTTP Request

`GET /groups`

```json
{
   "data": [
       {
            "id": Number,
            "name": String,
            "name_Zh": String,
            "point": Number, // 團隊積分
            "updated_at": timestamp,
            "created_at": timestamp
       }
   ]
}
```

# PointTask

## 取得個人積分所有的任務：

### HTTP Request

`GET /groups`

```json
"tasks": [
       {
           "id": Number,
           "name": String,
           "name_zh": String,
           "point": Number,
           "description": String,
           "message": String,
           "web_hook": String,
           "limit_count": Number,
           "time_unit": String (null, everyday, everyNight)
           "start_at": timestamp,
           "end_at": timestamp,
           "update_at": timestamp,
           "create_at": timestamp
       }
   ]
```


# PointProduct

## 取得個人積分產品列表

### HTTP Request

`GET /point_products`

```json
{
    "products": [
        {
            "id": Number,
            "name": String,
            "name_zh": String,
            "description": String,
            "message": String,
            "limit_count": Number,
            "start_at": timestamp,
            "end_at": timestamp,
            "expiry_ay": timestamp,
            "update_at": timestamp,
            "create_at": timestamp
        }
    ]
}
```

# Other Detials

## 取得網頁造訪人數

### HTTP Request

`GET /detial/user_count`

```json
{
    "user_count": number
}
```
