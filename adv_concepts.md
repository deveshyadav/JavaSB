## K8s Questions

### What is master nodes architecture
It has master- worker node structure. 
**Master node manages cluster**
**worker nodes run the applications**
Here is master node structure:- 
1. ApiServer(kube api server)
2. Distributed Database(etcd)
  -Desired state of an app is stored here
  -distributed in nature
  -maintains replicas so that data is not lost
  -
4. Scheduler(Kube scheduler)
  - schedules pods onto nodes
5. Controller manager(kube controller manager
  - it manages the changes required in desired states of pods.


### Can you run only docker containers in K8s
No ,any container that is of type OCI- open container interface, we can run on k8s.


### Does server go down if master node goes down?
No, when any api is hit, master doesnt get involved at all. So in this case no effect on the app.
Just that we cannot make changes to the nodes.
