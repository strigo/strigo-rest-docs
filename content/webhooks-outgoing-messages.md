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
`type`                  | String   | The type of entity for which the webhook was triggered (uppercase).
`action`                | String   | The action performed on that entity (uppercase).
`entity_ids`            | List     | The list of entity IDs for which the webhook was triggered. For example, multiple on-demand enrollments can expire at the same time, triggering a single webhook to notify the customer. This array can therefore contain things like class IDs, event IDs, enrollment IDs, etc..
`context`               | Object   | Any additional context a certain event may require.
`callback`              | List     | The callback URL to call to after the webhook was triggered.

### Response Structure:

Note that Strigo will convey the success or failure of webhook calls based on standard HTTP response codes (that the backend should provide).


## Example Message

All webhook messages should look like the following example.

The differences between them will be the `message_id`, `type`, `action` and `entity_ids` provided.

For a list of possible `type`s and `action`s, see below.


> Request Example

```shell
$ curl -X POST \
    -H "Authorization: Bearer ${ORG_BACKEND_USER}:${ORG_BACKEND_KEY}" \
    -H "Accept: application/json" \
    -H "Content-Type: appcourse
course
courselication/json" \
    "https://training.mycompany.com/webhooks/events" \
    -d @- <<EOF
    {
        "message_id": "4dd6be9e",
        "type": "EVENT",
        "action": "STARTED",
        "entity_ids": ["daf24556"],
        "context": {
            ...
        },
        "callback": "https://app.strigo.io/api/v1/webhooks/events/incoming"
    }
EOF
```

## Available types and actions

The following represents an exhaustive list of types of entities and actions corresponding with those types.

### TYPE: `EVENT`

Represents an ILT event.

* `STARTED` => The event started.
* `ENDED` => The event ended.
* `EXTENDED` => The event end time was extended.
* `WORKSPACE_JOINED` => An attendee has joined the event.
* `WORKSPACE_REMOVED` => An attendee was removed from the event.

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

### TYPE: `CLASS`

Represents a class template.

* `CREATED` => The class was created.
* `UPDATED` => The class configuration was updated.
* `DELETED` => The class was deleted.
