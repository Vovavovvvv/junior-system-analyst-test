# Задание 2. Проектирование REST API

## Предположение

На экране мобильного приложения отображается список магазинов-партнеров.

При нажатии на карточку магазина пользователь переходит на внешний сайт партнера.

---

# REST API

## Получение списка магазинов-партнеров

### HTTP Request

```http
GET /api/v1/partner-shops
Host: api.petrushka-green.ru
Authorization: Bearer <access_token>
Accept: application/json
```

### Описание

Метод возвращает список магазинов-партнеров для отображения на экране мобильного приложения.

---

## Успешный ответ

### HTTP Status

```http
200 OK
```

### Response Body

```json
{
  "shops": [
    {
      "id": 1,
      "name": "Зоомир",
      "description": "Товары для домашних животных",
      "imageUrl": "https://cdn.petrushka-green.ru/shops/zoomir.png",
      "externalUrl": "https://zoomir.ru"
    },
    {
      "id": 2,
      "name": "Сад и Огород",
      "description": "Товары для дачи",
      "imageUrl": "https://cdn.petrushka-green.ru/shops/garden.png",
      "externalUrl": "https://garden.ru"
    },
    {
      "id": 3,
      "name": "Фермерские продукты",
      "description": "Натуральные продукты",
      "imageUrl": "https://cdn.petrushka-green.ru/shops/farm.png",
      "externalUrl": "https://farm-market.ru"
    }
  ]
}
```

---

## Описание полей

| Поле | Тип | Описание |
|--------|--------|--------|
| id | integer | Идентификатор магазина |
| name | string | Название магазина |
| description | string | Краткое описание |
| imageUrl | string | Ссылка на изображение |
| externalUrl | string | Ссылка для перехода на сайт партнера |

---

## Возможные ошибки

### Пользователь не авторизован

```http
401 Unauthorized
```

```json
{
  "message": "Unauthorized"
}
```

---

### Внутренняя ошибка сервера

```http
500 Internal Server Error
```

```json
{
  "message": "Internal server error"
}
```

---

## Логика работы экрана

1. Пользователь открывает экран магазинов-партнеров.
2. Мобильное приложение выполняет запрос GET /api/v1/partner-shops.
3. Backend возвращает список магазинов.
4. Пользователь нажимает на карточку магазина.
5. Приложение открывает ссылку из поля externalUrl.
