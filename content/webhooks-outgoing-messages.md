---
weight: 1000
---


# Webhooks - Outgoing Messages

## Outgoing Message

The following messages are sent from Strigo to the customer's backend, where they can then perform any required actions.

For example, when an on-demand enrollment starts, a message will be sent, allowing the customer to create the lab for the student.

See [Incoming Messages](#webhooks-incoming-messages) for examples on the API calls to make from the customer's side.

### Attributes:

Attribute               | Type     | Description
---------               | -------  | -------
`message_id`            | String   | The message's unique identifier. This will be used to correlate webhook calls with their corresponding actions.
`type`                  | String   | The type of entity for which the webhook was triggered.
`status`                | String   | The current status of the entity.
`entity_ids`            | List     | The list of entity IDs for which the webhook was triggered. For example, multiple on-demand enrollments can expire at the same time, triggering a single webhook to notify the customer. This array can therefore contain things like class IDs, event IDs, enrollment IDs, etc..
`timestamp`             | Datetime | An ISO8601 compatible timestamp.
`context`               | Object   | Any additional context a certain event may require.
`callback`              | String   | The callback URL to call to after the webhook was triggered.

See [list of possible types and statuses](#available-types-and-statuses) below.

### Response Structure:

Note that Strigo will convey the success or failure of webhook calls based on standard HTTP response codes (that the backend should provide).


## Example Message

All webhook messages should look somehwat like the following example.

> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_BACKEND_USER}:${ORG_BACKEND_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://training.mycompany.com/webhooks/events" \
    -d @- <<EOF
    {
        "message_id": "4dd6be9e",
        "type": "EVENT",
        "status": "STARTED",
        "entity_ids": ["daf24556"],
        "timestamp": "2020-10-05T08:36:09+00:00",
        "context": {
            ...
        },
        "callback": "https://app.strigo.io/api/v1/webhooks/events/incoming"
    }
EOF
```

## Available types and statuses

The following represents an exhaustive list of types of entities and statuses corresponding with those types.

### TYPE: `CLASS`

Represents a class template.

* `CREATED` => The class was created.
* `UPDATED` => The class configuration was updated.
* `DELETED` => The class was deleted.

### TYPE: `EVENT`

Represents an ILT event.

* `STARTED` => The event started.
* `ENDED` => The event ended.
* `EXTENDED` => The event end time was extended.

### TYPE: `EVENT_WORKSPACE`

Represents a single attendee in an event.

* `CREATED` => An attendee has joined the event.
* `REMOVED` => An attendee was removed from the event.
* `REINSTATED` => An attendee was reinstated, and can now rejoin the event.
* `DELETED` => The event ended, and so the workspace was deleted.

### TYPE: `ONDEMAND_COURSE`

Represnts an On-demand self-paced course.

* `CREATED` => The course was created.
* `UPDATED` => The course configuration was updated.
* `DELETED` => The course was deleted.
* `STATUS_CHANGE` => The course status was set to ONLINE/OFFLINE

### TYPE: `ONDEMAND_ENROLLMENT`

Represents an On-demand self-paced enrollment.

* `CREATED` => A user was enrolled to an on-demand course.
* `STARTED` => A user has started their lab.
* `FINISHED` => A user has used up their allotted time.
* `EXPIRED` => An enrollment has passed its designated time before the student started it.
* `STOPPED` => An enrollment was stopped (either manually or automatically).
* `RESUMED` => An enrollment was resumed.

### TYPE: `RESOURCE`

Represents a single resource that can be either restarted or replaced (like a VM).

* `RESTARTED` => The resource was restarted.
* `REPLACED` => The resource was replaced.
