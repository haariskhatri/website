+++
title = "Restart Policy in Docker Containers"
date = "2024-12-11T19:37:12.040Z"
type = "post"
description = "How to use restart policies for docker containers"
in_search_index = true
[taxonomies]
tags = ["Containerizaton","Docker"]
+++

# Restart Policy in Docker Containers

When working with Docker containers for POCs (Proof of Concepts) or testing applications, you often need those containers running continuously, even over extended periods like a week.

Restarting containers manually after the host machine restarts can be inconvenient and error-prone. This is where **restart policies** come into play. Restart policies define rules that govern the lifecycle of Docker containers, ensuring they behave as expected under various scenarios.

Below are the available restart policy options in Docker:


### 1. **`no`**
This is the default option. Containers will not restart automatically if they stop or fail. This is suitable for services that do not need to run continuously or restart after failures.

**Usage**:
```bash
docker run --restart no nginx
```

### 2.**`always`**
This policy ensures that the container restarts automatically regardless of its exit status (success or failure). Containers using this policy will restart even if the Docker daemon itself is restarted. However, if you stop the container manually, it will still restart when the daemon restarts.

**Best for**: Critical services that must always run.

**Usage**
```bash
docker run --restart always nginx
```

### 3. **`on-failure`**
This policy restarts the container only if it exits with a non-zero exit code, indicating a failure. It is especially useful for handling **transient issues**—temporary problems like network glitches or resource constraints that can be resolved with a restart. You can also specify the maximum number of restart attempts. However, if you do not specify the maximum number of restarts, the container will keep restarting indefinitely until the failure condition is solved.

**Best For**: Services prone to temporary failures.

N : Maximum Number of restarts

**Usage**
```bash
docker run --restart on-failure[:N] nginx
```

### 4. **`unless-stopped`**
This policy ensures that the container restarts automatically, like  `always`, but with one key difference: If you manually stop the container, it will not restart after the Docker daemon is restarted. The container remains stopped until explicitly restarted.

**Best For**: Long-running services where manual intervention should persist across daemon restarts.

**Usage**
```bash
docker run --restart unless-stopped nginx
```
### **Conclusion**

Choosing the right restart policy depends on your use case. For example:

-   Use  `always`  for critical, always-on services.
-   Use  `on-failure`  for services prone to transient errors.
-   Use  `unless-stopped`  for services that should remain stopped after manual intervention.

With the right restart policy, you can ensure better reliability and minimize manual intervention in managing Docker containers.