# API для классификации страйкбольного снаряжения

API для определения категорий и подкатегорий страйкбольного снаряжения по тексту и изображениям объявлений.

## Установка

1. Установите зависимости:
bash
```pip install -r requirements.txt

Настройте базу данных PostgreSQL и измените app.config['DATABASE_URI'] в api.py.

Поместите модели в корневую папку:

pytorch_model.bin - модель классификации текста

yolov8n.pt - модель YOLOv8 для обнаружения объектов

# Использование
Получите токен:

curl -X GET http://localhost:5000/get_token
Отправьте запрос на классификацию:

bash
curl -X POST \
  http://localhost:5000/predict \
  -H 'Authorization: Bearer YOUR_TOKEN' \
  -H 'Content-Type: application/json' \
  -d '{
    "post_id": "12345",
    "text": "Продаю новую страйкбольную винтовку ASG и тактический жилет.",
    "photos": [
      {"photo_id": "1", "url": "https://example.com/photo1.jpg"},
      {"photo_id": "2", "url": "https://example.com/photo2.jpg"}
    ]
  }'
Ответ
API возвращает JSON с предсказанными категориями и подкатегориями для каждого обнаруженного объекта.

Пример ответа:

json
{
  "post_id": "12345",
  "text_category": "Страйкбольное оружие",
  "text_confidence": 0.95,
  "objects": [
    {
      "object_id": "a1b2c3d4",
      "category": "Страйкбольное оружие",
      "subcategory": "rifle",
      "confidence": 0.92,
      "photo_ids": ["1"]
    },
    {
      "object_id": "e5f6g7h8",
      "category": "Снаряжение и защита",
      "subcategory": "vest",
      "confidence": 0.89,
      "photo_ids": ["2"]
    }
  ]
}
