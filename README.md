# 🔔 Webhook: Отправка данных о заказе

## 📍 URL

```
POST https://smallprice.date/api/webhook/orders
```

## 🧾 Пример тела запроса (application/json)

```json
{
  "orderId": "9999999999test",
  "orderAmount": "100.2",
  "site": "lp-mobi.test",
  "utmCampaign": "123",
  "utmMedium": "",
  "utmSource": "",
  "createdAt": "2025-04-15 00:25:00"
}
```

## 📌 Обязательные поля

| Поле         | Тип     | Описание                                                                               |
|--------------|---------|----------------------------------------------------------------------------------------|
| `orderId`     | string  | Уникальный идентификатор заказа                                                        |
| `orderAmount` | string  | Сумма заказа (например: `"100.50" или "100,50"`)                                       |
| `site`        | string  | Домен, uri, с которого пришёл заказ (например: "lp-mobi.biz", "https://lp-mobi.biz", "http://lp-mobi.biz") |

## 🧩 Необязательные поля

| Поле          | Тип      | Описание                                                     |
|---------------|----------|--------------------------------------------------------------|
| `utmSource`   | string\|null | UTM Source (`google`, `facebook`, и т.д.)              |
| `utmMedium`   | string\|null | UTM Medium (`cpc`, `email`, и т.д.)                    |
| `utmCampaign` | string\|null | UTM Кампания                                             |
| `createdAt`   | string\|null | Дата/время заказа в формате `Y-m-d H:i:s` или `d-m-Y H:i:s`. По умолчанию — текущее время. |
| `timezone`    | string\|null | Временная зона. По умолчанию — UTC. |

## ✅ Пример cURL

```bash
curl -X POST https://smallprice.date/api/webhook/orders \
     -H "Content-Type: application/json" \
     -d '{
           "orderId": "9999999999test",
           "orderAmount": "100.2",
           "site": "lp-mobi.test",
           "utmCampaign": "123",
           "utmMedium": "",
           "utmSource": "",
           "createdAt": "2025-04-15 00:25:00"
         }'
```

## 📤 Ответ при успешной отправке

```json
{
  "message": "Order saved",
  "status": "success",
  "orderId": "9999999999test"
}
```

## ⚠️ Возможные ошибки

| Статус | Причина             | Ответ                                           |
|--------|---------------------|-------------------------------------------------|
| 400    | Неверный orderId    | `{"message":"Invalid order ID","status":"error"}` |
| 200    | Дубликат заказа     | `{"message":"Duplicate order","status":"error"}` |
| 500    | Ошибка на сервере   | `{"message":"Server error","status":"error"}`    |
