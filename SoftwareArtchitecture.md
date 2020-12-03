

<<Patterns of Enterprise Application Architecture>>

* Usually, there are two common elements:
  * One is the highest-level breakdown of a system into its parts;
  * The other, decisions that are hard to change.
* There are multiple architectures in a system, and the view of what is architecturally significant is one that can change over a system's lifetime.


Thinking About Performanc
* Response time
* Responsiveness
* Latency
* Throughput
* Load
* Load sensitivity
* efficiency
* The capacity of a system
* Scalability


Layering（分层）
* Use to break apart a complicated software system
  * The principal subsystems in software arranged similar to some form of layer cake
  * The higher layer uses various services defined by the lower layer, but the lower layer in unware of the higher layer
* The hardest part of a layered architecture is deciding what layers to have and what the responsibility of each layer should be



