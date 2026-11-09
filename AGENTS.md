# User Notifications

Use `notify-user [message]` to send progress updates to the operator.

- Send brief updates at key milestones or before long-running tasks.
- Notify when tasks complete or when operator intervention is needed.
- Keep notification messages concise and informative.
- Never include sensitive information (secrets, passwords, API tokens).

Example usage:
```bash
notify-user "Starting test suite execution"
notify-user "Finished refactoring auth module; all tests pass"
```
