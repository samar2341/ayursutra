# API

Base URL: `http://localhost:5000/api`

Responses use:

```json
{ "success": true, "message": "OK", "data": {}, "timestamp": "2026-05-26T00:00:00.000Z" }
```

## Auth

- `POST /auth/register` `{ "name": "Anaya", "email": "a@example.com", "password": "password123" }`
- `POST /auth/login` `{ "email": "a@example.com", "password": "password123" }`
- `GET /auth/me` Bearer token required
- `POST /auth/logout` Bearer token required

## Dosha

- `GET /dosha/questions`
- `POST /dosha/assessment` `{ "answers": [{ "questionId": "id", "answer": 1 }] }`
- `GET /dosha/latest`
- `GET /dosha/history`

## Journal

- `POST /journal` `{ "mood": "calm", "sleepQuality": "deep", "digestion": "steady", "energyLevel": "steady", "stressLevel": "balanced", "notes": "..." }`
- `GET /journal?limit=30`
- `DELETE /journal/:id`

## Routine

- `GET /routine/today`
- `POST /routine` `{ "date": "2026-05-26", "meditation": true, "yoga": true }`
- `PATCH /routine/:id` `{ "warmWater": true }`

## Remedies

- `GET /remedies`
- `GET /remedies/:id`
- `GET /remedies/saved/list`
- `POST /remedies/:id/save`
- `DELETE /remedies/:id/save`

## Recommendations

- `GET /recommendations`

## Seasonal

- `GET /seasonal-tips`
