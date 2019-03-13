

## Streaming Process

A. G. Psaltis. Streaming Data: Understanding the real-time pipeline. Manning Publications Co. 2017

![The streaming data architectural blueprint](https://github.com/QuChunhe/study/blob/master/pics/TheStreamingDataArchitecturalBlueprint.JPG)


|Classification  | Example |Latency measured in |Tolerance for delay|
| :------------ | :------------ | :------------ | :------------| 
|Hard |Pacemaker, anti-lock brakes |Microseconds–milliseconds |None—total system failure, potential loss of life|
|Soft |	Airline reservation system,online stock quotes, VoIP (Skype) |	Milliseconds–seconds |Low—no system failure, no life at risk|  
|Near |Skype video, home automation |Seconds–minutes| High—no system failure,no life at risk |




## Python

```
import os
del os.environ['PYSPARK_SUBMIT_ARGS']

from pyspark import SparkContext
import random

sc =  SparkContext("local", "Pi")

num_samples = 100000000
def inside(p):     
  x, y = random.random(), random.random()
  return x*x + y*y < 1
count = sc.parallelize(range(0, num_samples)).filter(inside).count()
pi = 4 * count / num_samples
print(pi)
sc.stop()
```
