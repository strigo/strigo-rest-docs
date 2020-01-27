---
weight: 115
---


# Workspace Exercises

Workspace exercises represent the manifestation of an exercise for a specific workspace in a live event or and on-demand course.

This representation has information about the status and progress of the exercises within the workspace.

## The Workspace Exercise Resource

### Attributes:

Attribute                   | Type     | Description
---------                   | -------  | -------
`id`                        | String   | A unique identifier of the workspace exercise.
`title`                     | String   | The title of the exercise.
`status`                    | String   | The completion status of the exercise, i.e. OPEN or DONE.
`finished_at`               | Datetime | The date and time the exercise has been completed on. Will be omitted if the exercise had not been complete at all.
