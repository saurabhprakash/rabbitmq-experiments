Some useful commands:
   - Running server(on local mac): sudo /usr/local/sbin/rabbitmq-server (On server run crash a probable error link: https://stackoverflow.com/questions/42895634/rabbitmq-server-boot-failed-on-mac-os-x-el-capitan/42898348#42898348)
   - List queues: sudo rabbitmqctl list_queues
   - Check queue contents: rabbitmqadmin get queue=<queue_name> requeue=true count=10
   - Check unacknowledged messages(not acknowledged by consumer): rabbitmqctl list_queues name messages_ready messages_unacknowledged
   
Experiments:
   - Tutorial 1 (https://www.rabbitmq.com/tutorials/tutorial-one-python.html): sender and reciver task, start a consumer(receive.py), which will run continuously waiting for deliveries.  Start the producer(send.py). The producer program will stop after every run.
   - Tutorial 2: working with workers, how to work with multiple workers, how rabbitmq handle situation when one worker dies(using help of acknowledgement), and how to handles cases when rabbitmq itself stops (https://www.rabbitmq.com/tutorials/tutorial-two-python.html): related files in current codebase - new_task.py, worker.py


Production checklist recommended by Rabbitmq: https://www.rabbitmq.com/production-checklist.html

Additional Important links:
 - How the memory limit works: https://www.rabbitmq.com/memory.html
 - How the disk limit works: https://www.rabbitmq.com/disk-alarms.html
 - How clients can determine if they are blocked: https://www.rabbitmq.com/connection-blocked.html
 - Networking guide: https://www.rabbitmq.com/networking.html
 
Create admin user on rabbitmq
  - rabbitmqctl add_user <username> <password>
  - rabbitmqctl set_user_tags <username> administrator
  - rabbitmqctl set_permissions -p / <username> ".*" ".*" ".*"

Setup:
 - installation :brew install rabbitmq
 - start server: brew services start rabbitmq
 - Server location: /usr/local/opt/rabbitmq/sbin/rabbitmq-server

For issue: "Error: Failure while executing; `git config --local --replace-all homebrew.private true` exited with 1."
Refer this link: https://saurabhbuddha.blogspot.com/2018/10/rabbit-mq-issues-and-fixes-setup-issue.html


