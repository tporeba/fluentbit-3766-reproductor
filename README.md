# fluentbit-3766-reproductor
Reproductor for https://github.com/fluent/fluent-bit/issues/3766

## Usage:
 * cd fluentbit-3766-reproductor
 * to change the fluentbit version you want to test - edit the Dockerfile and run
 ```
 docker-compose build
 ```
 * run kafka and zookeeper in background
 ```
 docker-compose up -d kafka zookeeper
 ```
 * in first terminal, run consumer on kafka to watch for new messages
 ```
 docker exec -it fluentbit-3766-reproductor-reproductor_kafka_1 /opt/kafka/bin/kafka-console-consumer.sh --topic fluentbit-test --bootstrap-server kafka:9092
 ```
 * in second terminal run fluentbit interactively
 ```
 docker-compose up fluentbit
 ```
 * after the test :
 ```
 docker-compose down -v
 ```
## Expected output
 
### NOT reproduced (OK):
 * in kafka consumer terminal you will see messages coming. slowly, one by one but still coming. 
 * in fluentbit the thread [output:kafka:kafka.0] is active and this warn line keeps reappearing. Each reappearance coincides with message being force-pushed to kafka.
```
[ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
```

example output (kafka):

```
{"@timestamp":1626281632.650104,"cpu_p":2.0,"user_p":1.666666666666667,"system_p":0.3333333333333333,"cpu0.p_cpu":2.0,"cpu0.p_user":1.0,"cpu0.p_system":1.0,"cpu1.p_cpu":3.0,"cpu1.p_user":2.0,"cpu1.p_system":1.0,"cpu2.p_cpu":1.0,"cpu2.p_user":1.0,"cpu2.p_system":0.0}
{"@timestamp":1626281633.64889,"cpu_p":6.333333333333333,"user_p":4.0,"system_p":2.333333333333333,"cpu0.p_cpu":7.0,"cpu0.p_user":3.0,"cpu0.p_system":4.0,"cpu1.p_cpu":11.0,"cpu1.p_user":9.0,"cpu1.p_system":2.0,"cpu2.p_cpu":1.0,"cpu2.p_user":0.0,"cpu2.p_system":1.0}
{"@timestamp":1626281634.651985,"cpu_p":10.66666666666667,"user_p":10.33333333333333,"system_p":0.3333333333333333,"cpu0.p_cpu":9.0,"cpu0.p_user":9.0,"cpu0.p_system":0.0,"cpu1.p_cpu":21.0,"cpu1.p_user":20.0,"cpu1.p_system":1.0,"cpu2.p_cpu":2.0,"cpu2.p_user":2.0,"cpu2.p_system":0.0}
{"@timestamp":1626281640.648585,"cpu_p":4.0,"user_p":3.333333333333333,"system_p":0.6666666666666666,"cpu0.p_cpu":1.0,"cpu0.p_user":1.0,"cpu0.p_system":0.0,"cpu1.p_cpu":6.0,"cpu1.p_user":5.0,"cpu1.p_system":1.0,"cpu2.p_cpu":5.0,"cpu2.p_user":4.0,"cpu2.p_system":1.0}
{"@timestamp":1626281641.649316,"cpu_p":5.333333333333333,"user_p":4.0,"system_p":1.333333333333333,"cpu0.p_cpu":4.0,"cpu0.p_user":3.0,"cpu0.p_system":1.0,"cpu1.p_cpu":7.0,"cpu1.p_user":6.0,"cpu1.p_system":1.0,"cpu2.p_cpu":3.0,"cpu2.p_user":2.0,"cpu2.p_system":1.0}
{"@timestamp":1626281642.649651,"cpu_p":2.0,"user_p":1.666666666666667,"system_p":0.3333333333333333,"cpu0.p_cpu":3.0,"cpu0.p_user":2.0,"cpu0.p_system":1.0,"cpu1.p_cpu":3.0,"cpu1.p_user":2.0,"cpu1.p_system":1.0,"cpu2.p_cpu":1.0,"cpu2.p_user":1.0,"cpu2.p_system":0.0}
{"@timestamp":1626281643.65514,"cpu_p":1.333333333333333,"user_p":1.0,"system_p":0.3333333333333333,"cpu0.p_cpu":2.0,"cpu0.p_user":2.0,"cpu0.p_system":0.0,"cpu1.p_cpu":2.0,"cpu1.p_user":2.0,"cpu1.p_system":0.0,"cpu2.p_cpu":0.0,"cpu2.p_user":0.0,"cpu2.p_system":0.0}
{"@timestamp":1626281644.651122,"cpu_p":2.0,"user_p":2.0,"system_p":0.0,"cpu0.p_cpu":2.0,"cpu0.p_user":2.0,"cpu0.p_system":0.0,"cpu1.p_cpu":2.0,"cpu1.p_user":2.0,"cpu1.p_system":0.0,"cpu2.p_cpu":1.0,"cpu2.p_user":1.0,"cpu2.p_system":0.0}
{"@timestamp":1626281650.650997,"cpu_p":4.0,"user_p":3.666666666666667,"system_p":0.3333333333333333,"cpu0.p_cpu":7.0,"cpu0.p_user":6.0,"cpu0.p_system":1.0,"cpu1.p_cpu":7.0,"cpu1.p_user":6.0,"cpu1.p_system":1.0,"cpu2.p_cpu":0.0,"cpu2.p_user":0.0,"cpu2.p_system":0.0}
{"@timestamp":1626281651.648813,"cpu_p":3.666666666666667,"user_p":3.0,"system_p":0.6666666666666666,"cpu0.p_cpu":5.0,"cpu0.p_user":5.0,"cpu0.p_system":0.0,"cpu1.p_cpu":3.0,"cpu1.p_user":2.0,"cpu1.p_system":1.0,"cpu2.p_cpu":3.0,"cpu2.p_user":2.0,"cpu2.p_system":1.0}
{"@timestamp":1626281652.648213,"cpu_p":2.0,"user_p":1.333333333333333,"system_p":0.6666666666666666,"cpu0.p_cpu":3.0,"cpu0.p_user":1.0,"cpu0.p_system":2.0,"cpu1.p_cpu":1.0,"cpu1.p_user":1.0,"cpu1.p_system":0.0,"cpu2.p_cpu":3.0,"cpu2.p_user":2.0,"cpu2.p_system":1.0}
{"@timestamp":1626281653.648135,"cpu_p":3.666666666666667,"user_p":3.0,"system_p":0.6666666666666666,"cpu0.p_cpu":5.0,"cpu0.p_user":5.0,"cpu0.p_system":0.0,"cpu1.p_cpu":4.0,"cpu1.p_user":3.0,"cpu1.p_system":1.0,"cpu2.p_cpu":2.0,"cpu2.p_user":2.0,"cpu2.p_system":0.0}
{"@timestamp":1626281654.650763,"cpu_p":1.333333333333333,"user_p":1.333333333333333,"system_p":0.0,"cpu0.p_cpu":1.0,"cpu0.p_user":1.0,"cpu0.p_system":0.0,"cpu1.p_cpu":2.0,"cpu1.p_user":2.0,"cpu1.p_system":0.0,"cpu2.p_cpu":0.0,"cpu2.p_user":0.0,"cpu2.p_system":0.0}
{"@timestamp":1626281660.649883,"cpu_p":1.333333333333333,"user_p":1.333333333333333,"system_p":0.0,"cpu0.p_cpu":3.0,"cpu0.p_user":2.0,"cpu0.p_system":1.0,"cpu1.p_cpu":0.0,"cpu1.p_user":0.0,"cpu1.p_system":0.0,"cpu2.p_cpu":1.0,"cpu2.p_user":1.0,"cpu2.p_system":0.0}
{"@timestamp":1626281661.649047,"cpu_p":4.0,"user_p":3.333333333333333,"system_p":0.6666666666666666,"cpu0.p_cpu":5.0,"cpu0.p_user":4.0,"cpu0.p_system":1.0,"cpu1.p_cpu":6.0,"cpu1.p_user":5.0,"cpu1.p_system":1.0,"cpu2.p_cpu":2.0,"cpu2.p_user":1.0,"cpu2.p_system":1.0}
{"@timestamp":1626281662.656958,"cpu_p":5.666666666666667,"user_p":3.666666666666667,"system_p":2.0,"cpu0.p_cpu":9.0,"cpu0.p_user":6.0,"cpu0.p_system":3.0,"cpu1.p_cpu":5.0,"cpu1.p_user":4.0,"cpu1.p_system":1.0,"cpu2.p_cpu":2.0,"cpu2.p_user":2.0,"cpu2.p_system":0.0}
{"@timestamp":1626281663.650175,"cpu_p":3.666666666666667,"user_p":2.0,"system_p":1.666666666666667,"cpu0.p_cpu":4.0,"cpu0.p_user":2.0,"cpu0.p_system":2.0,"cpu1.p_cpu":4.0,"cpu1.p_user":2.0,"cpu1.p_system":2.0,"cpu2.p_cpu":3.0,"cpu2.p_user":1.0,"cpu2.p_system":2.0}
{"@timestamp":1626281664.648547,"cpu_p":1.0,"user_p":0.6666666666666666,"system_p":0.3333333333333333,"cpu0.p_cpu":0.0,"cpu0.p_user":0.0,"cpu0.p_system":0.0,"cpu1.p_cpu":1.0,"cpu1.p_user":1.0,"cpu1.p_system":0.0,"cpu2.p_cpu":1.0,"cpu2.p_user":1.0,"cpu2.p_system":0.0}
{"@timestamp":1626281670.649095,"cpu_p":11.66666666666667,"user_p":10.33333333333333,"system_p":1.333333333333333,"cpu0.p_cpu":11.0,"cpu0.p_user":11.0,"cpu0.p_system":0.0,"cpu1.p_cpu":18.0,"cpu1.p_user":16.0,"cpu1.p_system":2.0,"cpu2.p_cpu":5.0,"cpu2.p_user":3.0,"cpu2.p_system":2.0}
{"@timestamp":1626281671.648031,"cpu_p":4.333333333333333,"user_p":3.666666666666667,"system_p":0.6666666666666666,"cpu0.p_cpu":5.0,"cpu0.p_user":3.0,"cpu0.p_system":2.0,"cpu1.p_cpu":5.0,"cpu1.p_user":4.0,"cpu1.p_system":1.0,"cpu2.p_cpu":4.0,"cpu2.p_user":4.0,"cpu2.p_system":0.0}
{"@timestamp":1626281672.658907,"cpu_p":3.0,"user_p":2.333333333333333,"system_p":0.6666666666666666,"cpu0.p_cpu":2.0,"cpu0.p_user":1.0,"cpu0.p_system":1.0,"cpu1.p_cpu":1.0,"cpu1.p_user":1.0,"cpu1.p_system":0.0,"cpu2.p_cpu":5.0,"cpu2.p_user":5.0,"cpu2.p_system":0.0}
{"@timestamp":1626281665.648793,"cpu_p":2.666666666666667,"user_p":2.333333333333333,"system_p":0.3333333333333333,"cpu0.p_cpu":3.0,"cpu0.p_user":2.0,"cpu0.p_system":1.0,"cpu1.p_cpu":6.0,"cpu1.p_user":5.0,"cpu1.p_system":1.0,"cpu2.p_cpu":1.0,"cpu2.p_user":0.0,"cpu2.p_system":1.0}
```


example output (fluentbit):

```
fluentbit_1  | Fluent Bit v1.7.1
fluentbit_1  | * Copyright (C) 2019-2021 The Fluent Bit Authors
fluentbit_1  | * Copyright (C) 2015-2018 Treasure Data
fluentbit_1  | * Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
fluentbit_1  | * https://fluentbit.io
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:46] [ info] Configuration:
fluentbit_1  | [2021/07/14 16:53:46] [ info]  flush time     | 5.000000 seconds
fluentbit_1  | [2021/07/14 16:53:46] [ info]  grace          | 5 seconds
fluentbit_1  | [2021/07/14 16:53:46] [ info]  daemon         | 0
fluentbit_1  | [2021/07/14 16:53:46] [ info] ___________
fluentbit_1  | [2021/07/14 16:53:46] [ info]  inputs:
fluentbit_1  | [2021/07/14 16:53:46] [ info]      cpu
fluentbit_1  | [2021/07/14 16:53:46] [ info] ___________
fluentbit_1  | [2021/07/14 16:53:46] [ info]  filters:
fluentbit_1  | [2021/07/14 16:53:46] [ info] ___________
fluentbit_1  | [2021/07/14 16:53:46] [ info]  outputs:
fluentbit_1  | [2021/07/14 16:53:46] [ info]      kafka.0
fluentbit_1  | [2021/07/14 16:53:46] [ info] ___________
fluentbit_1  | [2021/07/14 16:53:46] [ info]  collectors:
fluentbit_1  | [2021/07/14 16:53:46] [ info] [engine] started (pid=1)
fluentbit_1  | [2021/07/14 16:53:46] [debug] [engine] coroutine stack size: 24576 bytes (24.0K)
fluentbit_1  | [2021/07/14 16:53:46] [debug] [storage] [cio stream] new stream registered: cpu.0
fluentbit_1  | [2021/07/14 16:53:46] [ info] [storage] version=1.1.0, initializing...
fluentbit_1  | [2021/07/14 16:53:46] [ info] [storage] in-memory
fluentbit_1  | [2021/07/14 16:53:46] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
fluentbit_1  | [2021/07/14 16:53:46] [debug] [kafka:kafka.0] created event channels: read=18 write=19
fluentbit_1  | [2021/07/14 16:53:46] [ info] [output:kafka:kafka.0] brokers='kafka:9092' topics='fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:46] [debug] [router] match rule cpu.0:kafka.0
fluentbit_1  | [2021/07/14 16:53:46] [ info] [sp] stream processor started
fluentbit_1  | [2021/07/14 16:53:50] [debug] [task] created task=0x7f06b8c37280 id=0 OK
fluentbit_1  | {"cpu_p"=>[2021/07/14 16:53:50] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | 25.666667, "user_p"=>23.000000, "system_p"=>2.666667, "cpu0.p_cpu"=>39.000000, "cpu0.p_user"=>34.000000, "cpu0.p_system"=>5.000000, "cpu1.p_cpu"=>13.000000, "cpu1.p_user"=>12.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>24.000000, "cpu2.p_user"=>23.000000, "cpu2.p_system"=>1.000000}{"cpu_p"=>[2021/07/14 16:53:50] [debug] [output:kafka:kafka.0] enqueued message (272 bytes) for topic 'fluentbit-test'
fluentbit_1  | 2.666667, "user_p[2021/07/14 16:53:50] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | "=>2.666667, "system_p"=>0.000000, "cpu0.p_cpu"=>7.000000, "cpu0.p_user"=>6.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>1.000000, "cpu1.p_user"=>1.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:53:50] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:50] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | {[2021/07/14 16:53:51] [debug] [output:kafka:kafka.0] message delivered (272 bytes, partition 0)
fluentbit_1  | "cpu_p"=>[2021/07/14 16:53:51] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | 1.000000[2021/07/14 16:53:51] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | , "user_p"=>0.333333, "system_p"=>0.666667, "cpu0.p_cpu"=>0.000000, "cpu0.p_user"=>0.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>2.000000, "cpu1.p_user"=>1.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:53:51] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:51] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | {[2021/07/14 16:53:52] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | "cpu_p"=>[2021/07/14 16:53:52] [debug] [output:kafka:kafka.0] enqueued message (267 bytes) for topic 'fluentbit-test'
fluentbit_1  | 3.666667[2021/07/14 16:53:52] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | , "user_p"=>1.666667, "system_p"=>2.000000, "cpu0.p_cpu"=>3.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>2.000000, "cpu1.p_cpu"=>5.000000, "cpu1.p_user"=>3.000000, "cpu1.p_system"=>2.000000, "cpu2.p_cpu"=>3.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>2.000000}[2021/07/14 16:53:52] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:52] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:53:53] [debug] [output:kafka:kafka.0] message delivered (267 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:53:53] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:53] [debug] [out coro] cb_destroy coro_id=0
fluentbit_1  | [2021/07/14 16:53:53] [debug] [task] destroy task=0x7f06b8c37280 (task_id=0)
fluentbit_1  | [2021/07/14 16:53:55] [debug] [task] created task=0x7f06b8c37280 id=0 OK
fluentbit_1  | [2021/07/14 16:53:55] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>0.333333, "user_p"=>0.333333, "system_p"=>0.000000, "cpu0.p_cpu"=>0.000000, "cpu0.p_user"=>0.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>0.000000, "cpu1.p_user"=>0.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>0.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:53:55] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:55] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:53:56] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:53:56] [debug] [output:kafka:kafka.0] enqueued message (267 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:56] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>5.333333, "user_p"=>4.666667, "system_p"=>0.666667, "cpu0.p_cpu"=>8.000000, "cpu0.p_user"=>7.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>4.000000, "cpu1.p_user"=>4.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>5.000000, "cpu2.p_user"=>5.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:53:56] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:56] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:53:57] [debug] [output:kafka:kafka.0] message delivered (267 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:53:57] [debug] [output:kafka:kafka.0] enqueued message (280 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:57] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>2.000000, "user_p"=>1.666667, "system_p"=>0.333333, "cpu0.p_cpu"=>2.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>3.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:53:57] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:57] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:53:58] [debug] [output:kafka:kafka.0] message delivered (280 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:53:58] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:58] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>6.333333, "user_p"=>4.000000, "system_p"=>2.333333, "cpu0.p_cpu"=>7.000000, "cpu0.p_user"=>3.000000, "cpu0.p_system"=>4.000000, "cpu1.p_cpu"=>11.000000, "cpu1.p_user"=>9.000000, "cpu1.p_system"=>2.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:53:58] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:58] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:53:59] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:53:59] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:53:59] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>10.666667, "user_p"=>10.333333, "system_p"=>0.333333, "cpu0.p_cpu"=>9.000000, "cpu0.p_user"=>9.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>21.000000, "cpu1.p_user"=>20.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:53:59] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:53:59] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:00] [debug] [task] created task=0x7f06b8c37320 id=1 OK
fluentbit_1  | [2021/07/14 16:54:00] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:00] [debug] [output:kafka:kafka.0] enqueued message (282 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:00] [debug] [out coro] cb_destroy coro_id=2
fluentbit_1  | [2021/07/14 16:54:00] [debug] [out coro] cb_destroy coro_id=1
fluentbit_1  | [2021/07/14 16:54:00] [debug] [retry] new retry created for task_id=1 attempts=1
fluentbit_1  | [2021/07/14 16:54:00] [ warn] [engine] failed to flush chunk '1-1626281635.648642630.flb', retry in 10 seconds: task_id=1, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:00] [debug] [task] destroy task=0x7f06b8c37280 (task_id=0)
fluentbit_1  | [2021/07/14 16:54:05] [debug] [task] created task=0x7f06b8c37280 id=0 OK
fluentbit_1  | [2021/07/14 16:54:05] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>4.000000, "user_p"=>3.333333, "system_p"=>0.666667, "cpu0.p_cpu"=>1.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>6.000000, "cpu1.p_user"=>5.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>5.000000, "cpu2.p_user"=>4.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:54:05] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:05] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:06] [debug] [output:kafka:kafka.0] message delivered (282 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:06] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:06] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>5.333333, "user_p"=>4.000000, "system_p"=>1.333333, "cpu0.p_cpu"=>4.000000, "cpu0.p_user"=>3.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>7.000000, "cpu1.p_user"=>6.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>3.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:54:06] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:06] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:07] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:07] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:07] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>2.000000, "user_p"=>1.666667, "system_p"=>0.333333, "cpu0.p_cpu"=>3.000000, "cpu0.p_user"=>2.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>3.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:07] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:07] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:08] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:08] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:08] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>1.333333, "user_p"=>1.000000, "system_p"=>0.333333, "cpu0.p_cpu"=>2.000000, "cpu0.p_user"=>2.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>2.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>0.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:08] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:08] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:09] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:09] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:09] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>2.000000, "user_p"=>2.000000, "system_p"=>0.000000, "cpu0.p_cpu"=>2.000000, "cpu0.p_user"=>2.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>2.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:09] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:09] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:10] [debug] [task] created task=0x7f06b8c373c0 id=2 OK
fluentbit_1  | [2021/07/14 16:54:10] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:10] [debug] [output:kafka:kafka.0] enqueued message (237 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:10] [debug] [out coro] cb_destroy coro_id=4
fluentbit_1  | [2021/07/14 16:54:10] [debug] [out coro] cb_destroy coro_id=5
fluentbit_1  | [2021/07/14 16:54:10] [debug] [out coro] cb_destroy coro_id=3
fluentbit_1  | [2021/07/14 16:54:10] [debug] [retry] re-using retry for task_id=1 attempts=2
fluentbit_1  | [2021/07/14 16:54:10] [ warn] [engine] failed to flush chunk '1-1626281635.648642630.flb', retry in 88 seconds: task_id=1, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:10] [debug] [retry] new retry created for task_id=2 attempts=1
fluentbit_1  | [2021/07/14 16:54:10] [ warn] [engine] failed to flush chunk '1-1626281645.649084006.flb', retry in 6 seconds: task_id=2, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:10] [debug] [task] destroy task=0x7f06b8c37280 (task_id=0)
fluentbit_1  | {"cpu_p"=>4.000000, "user_p"=>3.666667, "system_p"=>0.333333, "cpu0.p_cpu"=>7.000000, "cpu0.p_user"=>6.000000[2021/07/14 16:54:15] [debug] [task] created task=0x7f06b8c37280 id=0 OK
fluentbit_1  | , "cpu0.p_system"[2021/07/14 16:54:15] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | =>1.000000, "cpu1.p_cpu"=>7.000000, "cpu1.p_user"=>6.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>0.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:15] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:15] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:16] [debug] [output:kafka:kafka.0] message delivered (237 bytes, partition 0)
fluentbit_1  | {"cpu_p"=>3.666667, "user_p[2021/07/14 16:54:16] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | "=>3.000000, "[2021/07/14 16:54:16] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | system_p"=>0.666667, "cpu0.p_cpu"=>5.000000, "cpu0.p_user"=>5.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>3.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>3.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:54:16] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:16] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:16] [debug] [out coro] cb_destroy coro_id=7
fluentbit_1  | [2021/07/14 16:54:16] [debug] [retry] re-using retry for task_id=2 attempts=2
fluentbit_1  | [2021/07/14 16:54:16] [ warn] [engine] failed to flush chunk '1-1626281645.649084006.flb', retry in 22 seconds: task_id=2, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:17] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | {"cpu_p"=>2.000000, "user_p"=>1.333333, "system_p"=>0.666667, "cpu0.p_cpu"=>3.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>2.000000, "cpu1.p_cpu"=>1.000000, "cpu1.p_user"=>1.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>3.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:54:17] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:17] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:17] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:17] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:18] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | {"cpu_p[2021/07/14 16:54:18] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:18] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | "=>3.666667, "user_p"=>3.000000, "system_p"=>0.666667, "cpu0.p_cpu"=>5.000000, "cpu0.p_user"=>5.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>4.000000, "cpu1.p_user"=>3.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:18] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:18] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:19] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | {"cpu_p"=>[2021/07/14 16:54:19] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | 1.333333, "user_p"=>[2021/07/14 16:54:19] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | 1.333333, "system_p"=>0.000000, "cpu0.p_cpu"=>1.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>2.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>0.000000, "cpu2.p_user"=>0.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:19] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:19] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:20] [debug] [task] created task=0x7f06b8c37460 id=3 OK
fluentbit_1  | [2021/07/14 16:54:20] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:20] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:20] [debug] [out coro] cb_destroy coro_id=8
fluentbit_1  | [2021/07/14 16:54:20] [debug] [out coro] cb_destroy coro_id=6
fluentbit_1  | [2021/07/14 16:54:20] [debug] [retry] new retry created for task_id=3 attempts=1
fluentbit_1  | [2021/07/14 16:54:20] [ warn] [engine] failed to flush chunk '1-1626281655.651616087.flb', retry in 6 seconds: task_id=3, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:20] [debug] [task] destroy task=0x7f06b8c37280 (task_id=0)
fluentbit_1  | {"cpu_p"=>1.333333, "user_p"=>1.333333, "system_p"=>0.000000, "cpu0.p_cpu"=>3.000000, "cpu0.p_user"=>2.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>0.000000, "cpu1.p_user"=>0.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:25] [debug] [task] created task=0x7f06b8c37280 id=0 OK
fluentbit_1  | [2021/07/14 16:54:25] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:25] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:25] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:26] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:26] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:26] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>4.000000, "user_p"=>3.333333, "system_p"=>0.666667, "cpu0.p_cpu"=>5.000000, "cpu0.p_user"=>4.000000, "cpu0.p_system"=>1.000000, "cpu1.p_cpu"=>6.000000, "cpu1.p_user"=>5.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:54:26] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:26] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:26] [debug] [out coro] cb_destroy coro_id=10
fluentbit_1  | [2021/07/14 16:54:26] [debug] [retry] re-using retry for task_id=3 attempts=2
fluentbit_1  | [2021/07/14 16:54:26] [ warn] [engine] failed to flush chunk '1-1626281655.651616087.flb', retry in 97 seconds: task_id=3, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:27] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:27] [debug] [output:kafka:kafka.0] enqueued message (266 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:27] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>5.666667, "user_p"=>3.666667, "system_p"=>2.000000, "cpu0.p_cpu"=>9.000000, "cpu0.p_user"=>6.000000, "cpu0.p_system"=>3.000000, "cpu1.p_cpu"=>5.000000, "cpu1.p_user"=>4.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:27] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:27] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:28] [debug] [output:kafka:kafka.0] message delivered (266 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:28] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:28] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>3.666667, "user_p"=>2.000000, "system_p"=>1.666667, "cpu0.p_cpu"=>4.000000, "cpu0.p_user"=>2.000000, "cpu0.p_system"=>2.000000, "cpu1.p_cpu"=>4.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>2.000000, "cpu2.p_cpu"=>3.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>2.000000}[2021/07/14 16:54:28] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:28] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:29] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:29] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:29] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | {"cpu_p"=>1.000000, "user_p"=>0.666667, "system_p"=>0.333333, "cpu0.p_cpu"=>0.000000, "cpu0.p_user"=>0.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>1.000000, "cpu1.p_user"=>1.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>1.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>0.000000}[2021/07/14 16:54:29] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:54:29] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:54:30] [debug] [task] created task=0x7f06b8c37500 id=4 OK
fluentbit_1  | [2021/07/14 16:54:30] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | [2021/07/14 16:54:30] [debug] [output:kafka:kafka.0] enqueued message (267 bytes) for topic 'fluentbit-test'
fluentbit_1  | [2021/07/14 16:54:30] [debug] [out coro] cb_destroy coro_id=11
fluentbit_1  | [2021/07/14 16:54:30] [debug] [out coro] cb_destroy coro_id=9
fluentbit_1  | [2021/07/14 16:54:30] [debug] [retry] new retry created for task_id=4 attempts=1
fluentbit_1  | [2021/07/14 16:54:30] [ warn] [engine] failed to flush chunk '1-1626281665.648805863.flb', retry in 6 seconds: task_id=4, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:54:30] [debug] [task] destroy task=0x7f06b8c37280 (task_id=0)

```

### Reproduced (Bug):
 * kafka consumer terminal receives a few messages initially and then no new messages arrive
 * in fluentbit the thread [output:kafka:kafka.0] is active only briefly and after one of "internal queue is full" warnings stops logging anything
 
 
example output (kafka):
```
[2021-07-14 16:49:27,686] WARN [Consumer clientId=consumer-console-consumer-52891-1, groupId=console-consumer-52891] Error while fetching metadata with correlation id 2 : {fluentbit-test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-07-14 16:49:27,793] WARN [Consumer clientId=consumer-console-consumer-52891-1, groupId=console-consumer-52891] Error while fetching metadata with correlation id 4 : {fluentbit-test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-07-14 16:49:27,916] WARN [Consumer clientId=consumer-console-consumer-52891-1, groupId=console-consumer-52891] Error while fetching metadata with correlation id 6 : {fluentbit-test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
[2021-07-14 16:49:28,027] WARN [Consumer clientId=consumer-console-consumer-52891-1, groupId=console-consumer-52891] Error while fetching metadata with correlation id 8 : {fluentbit-test=LEADER_NOT_AVAILABLE} (org.apache.kafka.clients.NetworkClient)
{"@timestamp":1626281382.653004,"cpu_p":1.666666666666667,"user_p":1.666666666666667,"system_p":0.0,"cpu0.p_cpu":1.0,"cpu0.p_user":1.0,"cpu0.p_system":0.0,"cpu1.p_cpu":2.0,"cpu1.p_user":2.0,"cpu1.p_system":0.0,"cpu2.p_cpu":2.0,"cpu2.p_user":2.0,"cpu2.p_system":0.0}
{"@timestamp":1626281383.648235,"cpu_p":4.0,"user_p":2.0,"system_p":2.0,"cpu0.p_cpu":3.0,"cpu0.p_user":1.0,"cpu0.p_system":2.0,"cpu1.p_cpu":5.0,"cpu1.p_user":3.0,"cpu1.p_system":2.0,"cpu2.p_cpu":2.0,"cpu2.p_user":1.0,"cpu2.p_system":1.0}
Processed a total of 2 messages
```

example output (fluentbit):
```
fluentbit_1  | Fluent Bit v1.7.2
fluentbit_1  | * Copyright (C) 2019-2021 The Fluent Bit Authors
fluentbit_1  | * Copyright (C) 2015-2018 Treasure Data
fluentbit_1  | * Fluent Bit is a CNCF sub-project under the umbrella of Fluentd
fluentbit_1  | * https://fluentbit.io
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:49:42] [ info] Configuration:
fluentbit_1  | [2021/07/14 16:49:42] [ info]  flush time     | 5.000000 seconds
fluentbit_1  | [2021/07/14 16:49:42] [ info]  grace          | 5 seconds
fluentbit_1  | [2021/07/14 16:49:42] [ info]  daemon         | 0
fluentbit_1  | [2021/07/14 16:49:42] [ info] ___________
fluentbit_1  | [2021/07/14 16:49:42] [ info]  inputs:
fluentbit_1  | [2021/07/14 16:49:42] [ info]      cpu
fluentbit_1  | [2021/07/14 16:49:42] [ info] ___________
fluentbit_1  | [2021/07/14 16:49:42] [ info]  filters:
fluentbit_1  | [2021/07/14 16:49:42] [ info] ___________
fluentbit_1  | [2021/07/14 16:49:42] [ info]  outputs:
fluentbit_1  | [2021/07/14 16:49:42] [ info]      kafka.0
fluentbit_1  | [2021/07/14 16:49:42] [ info] ___________
fluentbit_1  | [2021/07/14 16:49:42] [ info]  collectors:
fluentbit_1  | [2021/07/14 16:49:42] [ info] [engine] started (pid=1)
fluentbit_1  | [2021/07/14 16:49:42] [debug] [engine] coroutine stack size: 24576 bytes (24.0K)
fluentbit_1  | [2021/07/14 16:49:42] [debug] [storage] [cio stream] new stream registered: cpu.0
fluentbit_1  | [2021/07/14 16:49:42] [ info] [storage] version=1.1.1, initializing...
fluentbit_1  | [2021/07/14 16:49:42] [ info] [storage] in-memory
fluentbit_1  | [2021/07/14 16:49:42] [ info] [storage] normal synchronization mode, checksum disabled, max_chunks_up=128
fluentbit_1  | [2021/07/14 16:49:42] [debug] [kafka:kafka.0] created event channels: read=18 write=19
fluentbit_1  | [2021/07/14 16:49:42] [ info] [output:kafka:kafka.0] brokers='kafka:9092' topics='fluentbit-test'
fluentbit_1  | [2021/07/14 16:49:42] [debug] [router] match rule cpu.0:kafka.0
fluentbit_1  | [2021/07/14 16:49:42] [ info] [sp] stream processor started
fluentbit_1  | [2021/07/14 16:49:46] [debug] [task] created task=0x7f8bd3c37280 id=0 OK
fluentbit_1  | {"cpu_p"=>1.666667, "user_p"=>[2021/07/14 16:49:46] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | 1.666667, "system_p"=>0.000000, "cpu0.p_cpu"=>1.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>0.000000, "cpu1.p_cpu"=>2.000000, "cpu1.p_user"=>2.000000, "cpu1.p_system"=>0.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>2.000000, "cpu2.p_system"=>0.000000}{"cpu_p"=>[2021/07/14 16:49:46] [debug] [output:kafka:kafka.0] enqueued message (265 bytes) for topic 'fluentbit-test'
fluentbit_1  | 4.000000, [2021/07/14 16:49:46] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | "user_p"=>2.000000, "system_p"=>2.000000, "cpu0.p_cpu"=>3.000000, "cpu0.p_user"=>1.000000, "cpu0.p_system"=>2.000000, "cpu1.p_cpu"=>5.000000, "cpu1.p_user"=>3.000000, "cpu1.p_system"=>2.000000, "cpu2.p_cpu"=>2.000000, "cpu2.p_user"=>1.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:49:46] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:49:46] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | {"cpu_p"=>[2021/07/14 16:49:47] [debug] [output:kafka:kafka.0] message delivered (265 bytes, partition 0)
fluentbit_1  | 7.333333, "user_p"=>[2021/07/14 16:49:47] [debug] [output:kafka:kafka.0] enqueued message (237 bytes) for topic 'fluentbit-test'
fluentbit_1  | 6.000000, "system_p[2021/07/14 16:49:47] [debug] in produce_message
fluentbit_1  | 
fluentbit_1  | "=>1.333333, "cpu0.p_cpu"=>9.000000, "cpu0.p_user"=>7.000000, "cpu0.p_system"=>2.000000, "cpu1.p_cpu"=>9.000000, "cpu1.p_user"=>8.000000, "cpu1.p_system"=>1.000000, "cpu2.p_cpu"=>4.000000, "cpu2.p_user"=>3.000000, "cpu2.p_system"=>1.000000}[2021/07/14 16:49:47] [error] % Failed to produce to topic fluentbit-test: Local: Queue full
fluentbit_1  | 
fluentbit_1  | [2021/07/14 16:49:47] [ warn] [output:kafka:kafka.0] internal queue is full, retrying in one second
fluentbit_1  | [2021/07/14 16:49:51] [debug] [task] created task=0x7f8bd3c37320 id=1 OK
fluentbit_1  | [2021/07/14 16:49:51] [debug] [out coro] cb_destroy coro_id=1
fluentbit_1  | [2021/07/14 16:49:51] [debug] [retry] new retry created for task_id=1 attempts=1
fluentbit_1  | [2021/07/14 16:49:51] [ warn] [engine] failed to flush chunk '1-1626281386.648523162.flb', retry in 7 seconds: task_id=1, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:49:56] [debug] [task] created task=0x7f8bd3c373c0 id=2 OK
fluentbit_1  | [2021/07/14 16:49:56] [debug] [out coro] cb_destroy coro_id=2
fluentbit_1  | [2021/07/14 16:49:56] [debug] [retry] new retry created for task_id=2 attempts=1
fluentbit_1  | [2021/07/14 16:49:56] [ warn] [engine] failed to flush chunk '1-1626281391.649216890.flb', retry in 11 seconds: task_id=2, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:49:58] [debug] [out coro] cb_destroy coro_id=3
fluentbit_1  | [2021/07/14 16:49:58] [debug] [retry] re-using retry for task_id=1 attempts=2
fluentbit_1  | [2021/07/14 16:49:58] [ warn] [engine] failed to flush chunk '1-1626281386.648523162.flb', retry in 98 seconds: task_id=1, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:01] [debug] [task] created task=0x7f8bd3c37460 id=3 OK
fluentbit_1  | [2021/07/14 16:50:01] [debug] [out coro] cb_destroy coro_id=4
fluentbit_1  | [2021/07/14 16:50:01] [debug] [retry] new retry created for task_id=3 attempts=1
fluentbit_1  | [2021/07/14 16:50:01] [ warn] [engine] failed to flush chunk '1-1626281396.649538326.flb', retry in 7 seconds: task_id=3, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:06] [debug] [task] created task=0x7f8bd3c37500 id=4 OK
fluentbit_1  | [2021/07/14 16:50:06] [debug] [out coro] cb_destroy coro_id=5
fluentbit_1  | [2021/07/14 16:50:06] [debug] [retry] new retry created for task_id=4 attempts=1
fluentbit_1  | [2021/07/14 16:50:06] [ warn] [engine] failed to flush chunk '1-1626281401.648276426.flb', retry in 6 seconds: task_id=4, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:07] [debug] [out coro] cb_destroy coro_id=6
fluentbit_1  | [2021/07/14 16:50:07] [debug] [retry] re-using retry for task_id=2 attempts=2
fluentbit_1  | [2021/07/14 16:50:07] [ warn] [engine] failed to flush chunk '1-1626281391.649216890.flb', retry in 71 seconds: task_id=2, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:08] [debug] [out coro] cb_destroy coro_id=7
fluentbit_1  | [2021/07/14 16:50:08] [debug] [retry] re-using retry for task_id=3 attempts=2
fluentbit_1  | [2021/07/14 16:50:08] [ warn] [engine] failed to flush chunk '1-1626281396.649538326.flb', retry in 31 seconds: task_id=3, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:11] [debug] [task] created task=0x7f8bd3c375a0 id=5 OK
fluentbit_1  | [2021/07/14 16:50:11] [debug] [out coro] cb_destroy coro_id=8
fluentbit_1  | [2021/07/14 16:50:11] [debug] [retry] new retry created for task_id=5 attempts=1
fluentbit_1  | [2021/07/14 16:50:11] [ warn] [engine] failed to flush chunk '1-1626281406.648322871.flb', retry in 7 seconds: task_id=5, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:12] [debug] [out coro] cb_destroy coro_id=9
fluentbit_1  | [2021/07/14 16:50:12] [debug] [retry] re-using retry for task_id=4 attempts=2
fluentbit_1  | [2021/07/14 16:50:12] [ warn] [engine] failed to flush chunk '1-1626281401.648276426.flb', retry in 101 seconds: task_id=4, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:16] [debug] [task] created task=0x7f8bd3c37640 id=6 OK
fluentbit_1  | [2021/07/14 16:50:16] [debug] [out coro] cb_destroy coro_id=10
fluentbit_1  | [2021/07/14 16:50:16] [debug] [retry] new retry created for task_id=6 attempts=1
fluentbit_1  | [2021/07/14 16:50:16] [ warn] [engine] failed to flush chunk '1-1626281411.649218484.flb', retry in 8 seconds: task_id=6, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:18] [debug] [out coro] cb_destroy coro_id=11
fluentbit_1  | [2021/07/14 16:50:18] [debug] [retry] re-using retry for task_id=5 attempts=2
fluentbit_1  | [2021/07/14 16:50:18] [ warn] [engine] failed to flush chunk '1-1626281406.648322871.flb', retry in 27 seconds: task_id=5, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:21] [debug] [task] created task=0x7f8bd3c376e0 id=7 OK
fluentbit_1  | [2021/07/14 16:50:21] [debug] [out coro] cb_destroy coro_id=12
fluentbit_1  | [2021/07/14 16:50:21] [debug] [retry] new retry created for task_id=7 attempts=1
fluentbit_1  | [2021/07/14 16:50:21] [ warn] [engine] failed to flush chunk '1-1626281416.655350329.flb', retry in 11 seconds: task_id=7, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:24] [debug] [out coro] cb_destroy coro_id=13
fluentbit_1  | [2021/07/14 16:50:24] [debug] [retry] re-using retry for task_id=6 attempts=2
fluentbit_1  | [2021/07/14 16:50:24] [ warn] [engine] failed to flush chunk '1-1626281411.649218484.flb', retry in 31 seconds: task_id=6, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:26] [debug] [task] created task=0x7f8bd3c37780 id=8 OK
fluentbit_1  | [2021/07/14 16:50:26] [debug] [out coro] cb_destroy coro_id=14
fluentbit_1  | [2021/07/14 16:50:26] [debug] [retry] new retry created for task_id=8 attempts=1
fluentbit_1  | [2021/07/14 16:50:26] [ warn] [engine] failed to flush chunk '1-1626281421.648340537.flb', retry in 11 seconds: task_id=8, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:31] [debug] [task] created task=0x7f8bd3c37820 id=9 OK
fluentbit_1  | [2021/07/14 16:50:31] [debug] [out coro] cb_destroy coro_id=15
fluentbit_1  | [2021/07/14 16:50:31] [debug] [retry] new retry created for task_id=9 attempts=1
fluentbit_1  | [2021/07/14 16:50:31] [ warn] [engine] failed to flush chunk '1-1626281426.648397858.flb', retry in 6 seconds: task_id=9, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:32] [debug] [out coro] cb_destroy coro_id=16
fluentbit_1  | [2021/07/14 16:50:32] [debug] [retry] re-using retry for task_id=7 attempts=2
fluentbit_1  | [2021/07/14 16:50:32] [ warn] [engine] failed to flush chunk '1-1626281416.655350329.flb', retry in 62 seconds: task_id=7, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:36] [debug] [task] created task=0x7f8bd3c378c0 id=10 OK
fluentbit_1  | [2021/07/14 16:50:36] [debug] [out coro] cb_destroy coro_id=17
fluentbit_1  | [2021/07/14 16:50:36] [debug] [retry] new retry created for task_id=10 attempts=1
fluentbit_1  | [2021/07/14 16:50:36] [ warn] [engine] failed to flush chunk '1-1626281431.653045212.flb', retry in 9 seconds: task_id=10, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:37] [debug] [out coro] cb_destroy coro_id=18
fluentbit_1  | [2021/07/14 16:50:37] [debug] [out coro] cb_destroy coro_id=19
fluentbit_1  | [2021/07/14 16:50:37] [debug] [retry] re-using retry for task_id=8 attempts=2
fluentbit_1  | [2021/07/14 16:50:37] [ warn] [engine] failed to flush chunk '1-1626281421.648340537.flb', retry in 84 seconds: task_id=8, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:37] [debug] [retry] re-using retry for task_id=9 attempts=2
fluentbit_1  | [2021/07/14 16:50:37] [ warn] [engine] failed to flush chunk '1-1626281426.648397858.flb', retry in 44 seconds: task_id=9, input=cpu.0 > output=kafka.0 (out_id=0)
fluentbit_1  | [2021/07/14 16:50:39] [debug] [out coro] cb_destroy coro_id=20
fluentbit_1  | [2021/07/14 16:50:39] [debug] [retry] re-using retry for task_id=3 attempts=3
fluentbit_1  | [2021/07/14 16:50:39] [ warn] [engine] failed to flush chunk '1-1626281396.649538326.flb', retry in 141 seconds: task_id=3, input=cpu.0 > output=kafka.0 (out_id=0)
```