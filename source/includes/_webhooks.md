# Webhooks
RedSeed LMS allows you to configure webhooks to be notified when certain events occur in the system. This allows you to integrate RedSeed with other systems and automate processes.

## Setting up webhooks
To set up a webhook, you will need to provide:

- a URL to send the webhook to, 
- a list of events to be notified about, and
- any headers we should include in the request. 

You can do this by sending a request to support [at] redseed.com.

## User created

> The "UserCreated" webhook payload contains the newly-created user resource.

```json
{
  "event": "UserCreated",
  "payload": {
    "id": 190452,
    "firstName": "Webhook",
    "lastName": "TestUser",
    "email": "test@mail.com",
    "username": "webhook1",
    "code": null,
    "type": "Trainee",
    "status": "Active",
    "marker": 0,
    "locale": "en_NZ",
    "dateLastLogin": null,
    "dateCreatedAt": "2023-07-04T23:40:21.000000Z",
    "dateUpdatedAt": "2023-07-04T23:40:21.000000Z",
    "dateArchivedAt": null,
    "dateActivityAt": null,
    "location": {
      // Location resource
    },
    "userRole": {
      // UserRole resource
    },
    "userIdentities": [
      // UserIdentity resources
    ]
  }
}
```

This event is triggered when a user is created.

## User archived

> The "UserArchived" webhook payload contains the newly-created user resource.

```json
{
  "event": "UserArchived",
  "payload": {
    "id": 190452,
    "firstName": "Webhook",
    "lastName": "TestUser",
    "email": "test@mail.com",
    "username": "webhook1",
    "code": null,
    "type": "Trainee",
    "status": "Archived",
    "marker": 0,
    "locale": "en_NZ",
    "dateLastLogin": null,
    "dateCreatedAt": "2023-07-04T23:40:21.000000Z",
    "dateUpdatedAt": "2023-07-04T23:40:21.000000Z",
    "dateArchivedAt": "2023-07-05T23:40:21.000000Z",
    "dateActivityAt": null,
    "location": {
      // Location resource
    },
    "userRole": {
      // UserRole resource
    },
    "userIdentities": [
      // UserIdentity resources
    ]
  }
}
```

This event is triggered when a user is created.

## Training completed

> The "TrainingCompleted" webhook payload contains a training resource, including the user, coach, and course resources.

```json
{
  "event": "TrainingCompleted",
  "payload": {
    "id": 1754313,
    "status": "Completed",
    "percentComplete": 100,
    "seconds": 0,
    "dateCreatedAt": "2022-10-11T02:24:26.000000Z",
    "dateStartedAt": null,
    "dateUpdatedAt": "2023-06-30T03:11:39.000000Z",
    "dateCompletedAt": "2023-06-30T03:11:39.000000Z",
    "dateExpiresAt": null,
    "dateDeletedAt": null,
    "dateInactiveAt": null,
    "user": {
      // User resource
    },
    "coach": {
      // User resource
    },
    "course": {
      // Course resource
    },
  }
  
}

```

This event is triggered when a user completes a course. 
## Training expired

> The "TrainingExpired" webhook payload contains a training resource, including the user, coach, and course resources.

```json
{
  "event": "TrainingExpired",
  "payload": {
    "id": 1754313,
    "status": "Completed",
    "percentComplete": 100,
    "seconds": 312,
    "dateCreatedAt": "2022-10-11T02:24:26.000000Z",
    "dateStartedAt": null,
    "dateUpdatedAt": "2023-06-30T03:11:39.000000Z",
    "dateCompletedAt": "2023-06-30T03:11:39.000000Z",
    "dateExpiresAt": "2023-09-30T03:11:39.000000Z",
    "dateDeletedAt": null,
    "dateInactiveAt": null,
    "user": {
      // User resource
    },
    "coach": {
      // User resource
    },
    "course": {
      // Course resource
    },
  }
  
}

```

This event is triggered when a user's training expires. Training is checked for expiry every hour, on the hour.

## Pathway completed

> The "UserPathwayCompleted" webhook payload contains a UserPathway resource, including the user, coach, and course resources.

```json
{
  "event": "UserPathwayCompleted",
  "payload": {
    "id": 80548,
    "status": "Completed",
    "trainingCompleted": 3,
    "trainingTotal": 3,
    "dateCreatedAt": "2022-03-31T18:58:43.000000Z",
    "dateUpdatedAt": "2023-07-05T00:42:49.000000Z",
    "dateDeletedAt": null,
    "client": {
      // RedSeed Client resource
    },
    "pathway": {
      "id": "03d12776-7083-4958-ab03-0714cf2c2194",
      "name": "Test pathway",
      "description": "Pathway to test completion webhook",
      "status": "Active",
      "dateCreatedAt": "2020-03-30T19:17:20.000000Z",
      "dateUpdatedAt": "2021-11-23T18:06:35.000000Z",
      "dateDeletedAt": null,
      "courses": [
        // Course resources
      ]
    },
    "user": {
      // User resource
      "location": {
        // Location resource
      },
      }
    }
  }
}

```

This event is triggered when a user completes a course. 