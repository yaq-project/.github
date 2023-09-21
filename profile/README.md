<p align="center">
<img 
    style="display: block; 
           margin-left: auto;
           margin-right: auto;
           width: 30%;
           align: center;"
    src="https://raw.githubusercontent.com/yaq-project/yaq-fyi/main/logos/yaq-logo-411x256.png" 
    alt="Our logo">
</img>
</p>
  
👋 Hello, and welcome to the GitHub home of the yaq project.

yaq---Yet Another acQuisition

We are building a modular and extensible instrument control framework on top of [Apache Avro RPC](https://avro.apache.org/docs/1.11.1/specification/). 
In human terms, this means we have designed a simple user-friendly interface to control scientific hardware (motors, sensors, etc) from Python.
We already support [lots of hardware](https://yaq.fyi/hardware/), and more is being added all the time.

The yaq project has no official orchestration support.
We don't have "smart" tools to define experimental scans and record data.
Our _only_ goal is to build an excelent interface for addressing hardware.
Let yaq solve the annoying part (hardware interface support) while you focus on the fun part (your unique experiment).
Write a simple script to try an interesting experiment.
Use Jupyter to interact with your hardware.
Use an existing project focused on orchestration _e.g._ [Bluesky](https://blueskyproject.io/).
Develop your own one-off application, _e.g._ [Pressure Monitoring Reactor](https://github.com/uw-madison-chem-shops/pressure-monitoring-reactor).

```python
# minimal 2D scan---from scratch
import time
import yaqc
motor1 = yaqc.Client(port=38000)
motor2 = yaqc.Client(port=38001)
sensor = yaqc.Client(port=38002)
data = []
for m1 in range(-10, 10, 1):
    for m2 in range(0, 300, 5):
        motor1.set_position(m1)
        motor2.set_position(m2)
        for c in [motor1, motor2]:
            while c.busy():
                time.sleep(0.001)
        sensor.measure()
        while sensor.busy():
            time.sleep(0.001)
        reading = dict()
        reading["timestamp"] = time.time()
        reading["motor1"] = motor1.get_position()
        reading["motor2"] = motor2.get_position()
        reading.update(sensor.get_measured())
        data.append(reading)
```

Come join us!

Our website: https://yaq.fyi/

Chat room: https://matrix.to/#/#yaq:matrix.org

Community call: https://hackmd.io/team/yaq

Email listserve: https://groups.google.com/a/g-groups.wisc.edu/g/yaq

Publication: https://doi.org/10.1063/5.0135255

