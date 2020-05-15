# Performance overhead on the remote instance

The performance impact on the remote instance will be mainly driven by the amount of data we are pulling with each connection. The collection from the remote instance into the central repository is primarily delta with few exceptions of full load. The more often we are pulling data into the central repository the less impact it will have. Below is an example of the CPU utilisation of the remote instance whilst pulling a 5 minutes delta into the central repository. Note that pull does not last longer than few seconds:

![](../../.gitbook/assets/image%20%286%29.png)

