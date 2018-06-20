
A. G. Psaltis. Streaming Data: Understanding the real-time pipeline. Manning Publications Co. 2017

![The streaming data architectural blueprint](https://github.com/QuChunhe/study/blob/master/pics/TheStreamingDataArchitecturalBlueprint.JPG)


|Classification  | Example |Latency measured in |Tolerance for delay|
| :------------ | :------------ | :------------ | :------------| 
|Hard |Pacemaker, anti-lock brakes |Microseconds–milliseconds |None—total system failure, potential loss of life|
|Soft |	Airline reservation system,online stock quotes, VoIP (Skype) |	Milliseconds–seconds |Low—no system failure, no life at risk|  
|Near |Skype video, home automation |Seconds–minutes| High—no system failure,no life at risk |
