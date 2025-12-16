# Credit Card Poller Process API

API Process qui synchronise périodiquement les données cartes depuis Credit Card System vers Global Data.

## Description

Cette API utilise un scheduler pour déclencher périodiquement la synchronisation des cartes de crédit depuis Credit Card System vers Global Data. Elle supporte également des synchronisations à la demande.

## Endpoints

### POST /api/poller/credit-card/sync/cards
Déclenche une synchronisation manuelle des cartes depuis Credit Card System vers Global Data.

**Response:** 202 Accepted avec syncId

## Configuration

### Scheduler

Voir README.md de Core Banking Poller Process API pour la configuration du scheduler.

### Connexions HTTP Requises

- **Credit Card System API** (port 8081)
- **Global Financial Account System API** (port 8081) - pour upsert des cartes

Configurer dans `global.xml`:
- `Credit_Card_System_API_Config`
- `Global_Financial_Account_System_API_Config`

### Port

- **Port HTTP**: 8082

## Architecture Technique

### Flows Schedulés

- `scheduled-sync-cards-flow`: Synchronisation périodique des cartes (déclenché par scheduler)

### Flows Business-Logic (On-Demand)

- `sync-cards-business-logic`: Synchronisation manuelle des cartes (appelé via POST /sync/cards)

### Subflows

- `sync-cards-subflow`: Logique de synchronisation des cartes

## Exemples de Requêtes

### POST /api/poller/credit-card/sync/cards

```bash
curl -X POST http://localhost:8082/api/poller/credit-card/sync/cards
```

**Response:**
```json
{
  "message": "Card sync completed",
  "syncId": "550e8400-e29b-41d4-a716-446655440000",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

