Some useful commands:
   - Running server(on local mac): sudo /usr/local/sbin/rabbitmq-server (On server run crash a probable error link: https://stackoverflow.com/questions/42895634/rabbitmq-server-boot-failed-on-mac-os-x-el-capitan/42898348#42898348)
   - List queues: sudo rabbitmqctl list_queues
   - Check queue contents: rabbitmqadmin get queue=<queue_name> requeue=true count=10
   
Experiments:
    - Basic: sender and reciver task, start a consumer(receive.py), which will run continuously waiting for deliveries.  Start the producer(send.py). The producer program will stop after every run.
