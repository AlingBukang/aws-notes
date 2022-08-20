
# ECS Task Deployment

Amazon ECS supports the following task placement strategies:

- binpack – Place tasks based on the least available amount of CPU or memory. This minimizes the number of instances in use.
- random – Place tasks randomly.
- spread – Place tasks evenly based on the specified value. Accepted values are attribute key-value pairs, instanceId, or host.


Port mappings allow containers to access ports on the host container instance to send or receive traffic. Port mappings are specified as part of the container definition which can be configured in the task definition.

For task definitions that use the awsvpc network mode, you should only specify the containerPort. The hostPort can be left blank or it must be the same value as the containerPort.

Port mappings on Windows use the NetNAT gateway address rather than localhost. There is no loopback for port mappings on Windows, so you cannot access a container’s mapped port from the host itself.




Service scheduler provides you the ability to run tasks manually (for batch jobs or single run tasks), with Amazon ECS placing tasks on your cluster for you. The service scheduler is ideally suited for long running stateless services and applications.

Container instance is an Amazon EC2 instance that is running the Amazon ECS container agent and has been registered into a cluster. When you run tasks with Amazon ECS, your tasks using the EC2 launch type are placed on your active container instances.

Container Agent allows container instances to connect to your cluster. The Amazon ECS container agent is included in the Amazon ECS-optimized AMIs, but you can also install it on any Amazon EC2 instance that supports the Amazon ECS specification. 