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
`action`                | String   | The action performed on that entity.
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
    -H "Content-Type: application/json" \
    "https://training.mycompany.com/webhooks/events" \
    -d @- <<EOF
    {
        "message_id": "4dd6be9e",
        "type": "event",
        "action": "started",
        "entity_ids": ["daf24556"],
        "context": {
            ...
        },
        "callback": "https://app.strigo.io/api/v1/webhooks/events/incoming"
    }
EOF
```

## Available types and actions

The following represents an exhaustive list of types of entities and actions for those types.

* `event` (An ILT, Live event)
    * `start` (The event started).
    * `end` (The event ended).
    * `extend` (The event end time was extended).
    * `workspace_join` (An attendee has joined the event).
    * `workspace_remove` (An attendee was removed from the event).
* `ondemand_enrollment` (An On-demand self-paced enrollment)
    * `create` (A user was enrolled to an on-demand course).
    * `start` (A user has started their lab).
    * `finish` (A user has used up their allotted time).
    * `expire` (An enrollment has passed its designated time before the student started it).
    * `stop` (An enrollment was stopped (either manually or automatically)).
    * `resume` (An enrollment was resumed).
* `lab`
    * `restarted`
    * `replaced`
* `class` (A class template)
    * `create`
    * `update`
    * `delete`
