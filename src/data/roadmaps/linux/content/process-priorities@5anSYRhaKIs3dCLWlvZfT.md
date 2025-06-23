# Process Priorities

Linux assigns priority levels to processes, affecting execution timing and resource allocation. Process priorities use "nice" values ranging from -20 (highest priority) to +19 (lowest priority) and only root can set negative nive value. The `/proc` filesystem contains process information including priorities. You can view priorities with `ps -eo pid,pri,user,comm` and modify them using `renice` command.

Visit the following resource to learn more:

- [@article@niceness](https://linuxjourney.com/lesson/process-niceness)
