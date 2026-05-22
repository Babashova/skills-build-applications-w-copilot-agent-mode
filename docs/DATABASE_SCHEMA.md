# Database Schema

## MongoDB Collections

### Users Collection

Stores user account information.

**Collection Name:** `users`

#### Schema

```typescript
interface IUser {
  _id: ObjectId;
  name: string;
  email: string;
  createdAt: Date;
  updatedAt: Date;
}
```

#### Fields

| Field | Type | Required | Unique | Description |
|-------|------|----------|--------|-------------|
| `_id` | ObjectId | ✓ | ✓ | MongoDB generated ID |
| `name` | String | ✓ | ✗ | User's full name |
| `email` | String | ✓ | ✓ | User's email address |
| `createdAt` | Date | ✓ | ✗ | Timestamp of user creation |
| `updatedAt` | Date | ✓ | ✗ | Timestamp of last update |

#### Indexes

- `email` - Unique index for user lookup

#### Example Document

```json
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "John Doe",
  "email": "john@example.com",
  "createdAt": "2026-05-22T10:30:00Z",
  "updatedAt": "2026-05-22T10:30:00Z"
}
```

---

### Future Collections

#### Activities Collection
Will store fitness activity logs with:
- User reference
- Activity type (running, cycling, swimming, etc.)
- Duration, distance, calories
- Timestamp

#### Goals Collection
Will store user fitness goals:
- User reference
- Goal type
- Target value
- Start and end dates
- Progress tracking

#### Achievements Collection
Will store unlocked achievements:
- User reference
- Achievement type
- Unlock date
- Points/rewards

---

## Relationships

```
Users (1) ──→ (Many) Activities
Users (1) ──→ (Many) Goals
Users (1) ──→ (Many) Achievements
```

---

## Connection Details

**Connection String:** `mongodb://localhost:27017/octofit-tracker`

**Database Name:** `octofit-tracker`

---

## Backup & Recovery

### Backup
```bash
mongodump --uri="mongodb://localhost:27017/octofit-tracker" --out=./backup
```

### Restore
```bash
mongorestore --uri="mongodb://localhost:27017/octofit-tracker" ./backup/octofit-tracker
```
