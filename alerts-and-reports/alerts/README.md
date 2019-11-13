# Alerts

Alerting module was introduced in version 2.2.

Alerts are triggered by checks and can trigger various actions, such as notifications or reports. 

### Concept

Checks are executed by an agent job every minute and can call multiple actions. Normally an action is called when the check returns WARNING or CRITICAL status, or, when it recovers from WARNING or CRITICAL back to OK.

Actions are added to the queue to be processed by the queue processor \(another Agent Job\)

Reports can be either scheduled \(i.e. daily or weekly reports\) or can be triggered by an action on the back of the check. 

![](../../.gitbook/assets/image%20%2836%29.png)

