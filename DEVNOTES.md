Random developer notes:

Logging:
I think we're following this guy's advice:
https://fangpenlin.com/posts/2012/08/26/good-logging-practice-in-python/


# Standalone Workers

Our goal is to be able to spin up N workers of an instance type, have
them be able to pull tasks off the queue, run them with our
environment, etc.

Use SQS for jobs. SQS queue is set in the config file, used at setup. 
Each machine runs a daemon that pulls from SQS queue, runs things, returns
results. 
Each worker checks its uptime and the queue status and self-terminates
after a certain amount of time. 

Todo: 
[ ] Refactor wrenhandler to be more platform-agnostic. 
[ ] refactor Wren to let us invoke via non-Lambda mechanisms




Supervisord notes:
# get this init script

https://gist.github.com/hilios/b4974ad4b7771571705e6d0830c67119


[program:testprogram]
command=/usr/bin/python /home/ec2-user/testprogram.py
autorestart=true


stand-alone server
1. grabs from queue, processes job out-of-band
2. if there are no jobs for 5 min and you've been idle for 5 min, terminate


order of cloud-init directives:
http://stackoverflow.com/questions/34095839/cloud-init-what-is-the-execution-order-of-cloud-config-directives


