**Kuberenets journey**

The **Cloud** is a Cluster for computation for the Fraunhofer IVI AWZ Ingolstadt physically located in the Donaukurier in the IT Media. It can also serve as a remote workstation. The Cloud consists of multiple worker and storage Nodes.

We are using [Kubernetes](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Kubernetes) as the software architecture to connect multiple Nodes.

[Kubernetes](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Kubernetes) handles resources by creating [pods](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/pod) which are containerized environments with their isolated resources, storage and access. One can think of them as small virtual machines in a big computer. These [Containerized Environments](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/pod) are created using [Cri-o](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Cri-o) which uses the same syntax as [Docker](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Docker), but is optimized for a server.

One Node is one physical computer with its own resources, all Nodes are connected through kubernetes to create one big Cluster

Kuberenetes It is mostly a container orchestrator, managing different containers, scheduling, restarting and distributing resources. Containers are run on the Kubernetes cluster, which are e.g. Docker container and bring their own capsuled system with their own distribution. Kubernetes is the Backbone and Kubeflow builds on Kubernetes. kubelet is a system service restarting and managing failed pods.

Resources → Different resources are maintained by kubernetes which all can be accesed via some commands, e.g. kubectl get < resource-name >

Nodes → Are the physical Servers which are connected, so awz-worker1, awz-storage1 are 2 different nodes

Pods → Pods are wrapper for container (like a docker container) but managed by kubernetes

Pods → Pods are wrapper for container (like a docker container) but managed by kubernetes

**Kuberenetes :** 

The Cloud is using kubernetes to manage resources. Kubernetes (often abbreviated as K8s) is an open-source container orchestrator platform that automates the deployment, scaling, and management of containerized applications.

- History
1. Early on applications were run on physical servers where resource allocation or define resource boundaries is not possible. If we run multiple applications, there might be instances where one application takes most of the resources leaving less resources for other applications so as a result they underperform. A solution for this is to run each application on a different physical server but it is very expensive for an organization to maintain many physical servers.
1. Then virtualization was started which allows you to run multiple VMs on a single physical server’s CPU. This provides better utilization of the resources and allows better scalability as it is very easy to add or update an application. Each VM is a fully machine running all its components including its own operating system, on the top of virtualized hardware.
1. After virtualization, containerization began. Containers are similar to VMs, but they share the operating system among the applications instead of installing separate OS for different application, this makes them light weight.

Containers are a good way to bundle and run your applications. In a production environment, it is very important to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down another container is created to ensure there is no downtime. It will be difficult to maintain it manually when the scale is too high and that is where Kubernetes is useful. Kubernetes provides with a framework to run distributed systems resiliently. It takes care of the scaling and failover for your application, provides deployment patterns, etc

- If traffic to a container is high, Kubernetes can load balance and distribute the      

`                   `network traffic so that deployment is stable.

- You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.

- You provide Kubernetes with a cluster of nodes that it can use to run containerized tasks. You tell Kubernetes how much CPU and memory (RAM) each container needs. Kubernetes can fit containers onto your nodes to make the best use of your resources.

- Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

- Here are the key components and concepts of Kubernetes:
- **Nodes:** A Kubernetes cluster consists of one or more nodes, which can be physical or virtual machines. Each node is responsible for running containers and has a container runtime (such as Docker) installed. Nodes are grouped into a cluster to form a unified computing resource.
- **Pods:** The basic scheduling unit in Kubernetes is a pod. A pod is a logical group of one or more containers that are co-located and share the same network and storage resources. Containers within a pod can communicate with each other over the localhost interface. Pods are designed to be ephemeral and can be created, destroyed, or scaled independently.
- **Namespaces:** Kubernetes supports logical isolation through namespaces. Namespaces provide a way to group and segregate resources within a cluster. They can be used to separate environments (e.g., development, staging, production) or different projects or teams. Namespaces provide resource-level access controls and resource quota management.

**Pod:**

is a Containerized-Environment inside [Kubernetes](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Kubernetes). Each pod has connected resources such as number of CPUs, RAM and GPUs. This (in theory) limits the amount of resources a single pod can use.

When creating every pod is connected to an [image](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/image), which defines the type of operating system and pre installed libraries.

Additionally each pod is connected to [Persistent-Volume-Claims](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Persistent-Volume-Claims) and uses those as their storage device. Basically the [image](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/image) is a pre configered operating system and the [Persistent-Volume-Claim](https://euc-word-edit.officeapps.live.com/cloud/cloud/-/wikis/Persistent-Volume-Claims) is the external hard drive you connect to your computer. The resource limits define how much your computer can do.

Your notebooks on Kubeflow on the cloud are pods

**Why containers :** 

You can run your software on ist own environment (container), that includes all required code, database and other dependencies. You can isolate your container from the host einvironment. And this will increase portaility and reusability.

But the questions are : on which host (node) should be our container being runned.

Kuberenetes is a container orchestrator--> check the container state if it is healthy or not, restart it , decide on which host the container to run , ….

Pod : a wrapper for containers ---> we call containers pod in kubernetes , but pod actually wraps around your container to manage it.

Namespace: devide resources into isolated areas. --> e.g put all database pods on a same namespace

Node: the underlying host machine that kuberenets is running on

We have nodes (host machines) and the pods (containers) and kuberenetes is between these two managing them.

If a node fails you have other nodes that will take care of your pods.

**Pod lifecycle :** 

- When kuberenets create a pod with the image you provided , it selects a node with free resources and starts the pod.
- Kuberenets will check if a pod is in a healthy state and restarts it if necessary(with bash scripts within your pod --> if the script runned succesfully (returns something) then everything is fine)
- If a node fails , kuberenets will start a new pod or restart the pod.

In kuberenetes we have master nodes (manager) and worker nodes.

**Kubeflow :** 

Machine learning platform on Kuberenetes. containerize your Ml workflow.

In the workflow you load data, preprocess data and train the model and each of thiese steps could be started on ist own pod.

By creating notebooks on kubeflow you can access your pods where your python code (your application --> Gitlab code) will run and you can do development

But you also can do remote development via VSCode, 

for this purpose you need a config file in your local machine (C:/Username/.kube/config) , this config file is a yaml file containing configuartion for the kuberenetes cluster.

This is an example : 

![](Aspose.Words.9dafb7df-2536-44dc-94cb-3f73526b12ad.001.png)

You also need to install the command line for kuberenets -- > install kubectl

Plus “kuberenetes” and “remote development plugins” in vscode

**Kuberenetes cluster :** 

On a kubernetes cluster, we have multiole singular nodes which are compute workers (a normal pc) and you have resources on this nodes and you use this kube architecture to connect these nodes together

We have one master nodes and multiple worker nodes.

Some user come and ask master nodes that I will run this app and then master node will decide to start this instance of application on worker node1 , and then you can scale it easily by running multiple of this app instances on multiple worker nodes to ensure reachibality

Kuberenetes runs on pods, each of containers (app instances) is a pod and is a virtual environment inside the worker node

You can have multiple pods, doing completely different things on the same worker node

But these pods do not speak with each other and live on their own container

Now on the other hand, we have a main script in out jupyter notebook, that it is also a pod (main pod) then when running this main pod it will start multiple worker pods, this worker pods will run sumo simulation and with this we generate traffic data

Between the main pod and worker pods there is a rabbitmq that do the communication between these two types of pods

And we have also a shared volume (shared storage) for communication that the workers pods and main pods will write on this shared volume

The issue : if the main crashes and disappears all the worker pods will still running and send massages to rabitmq and fill up the memory, so we want to close worker pods and prevent worker pods to unnecessarily running

We want to stop the training pods if the main is not running, if something happens to the main like crash, keyboard interrupt then I want to stop all the worker pods after training but first save all the logs to file


**Further :** 

**Pod :**

A container as we all know, is a **self-contained environment** where we package applications and their dependencies. Typically a container runs a single process (Although there are ways to run multiple processes). Each container gets an IP address and can attach volumes and control CPU and memory resources, among other things. All these happen via the concepts of namespaces and control groups.

Kubernetes is a container orchestration system for deploying, scaling, and managing containerized applications and it has its own way of running containers. **We call it a pod**. A pod is the **smallest deployable unit in Kubernetes** that represents a single instance of an application.

A container is a single unit. However, a pod can contain more than one container. You can think of **pods as a box that can hold one or more containers** together.

Pod provides a higher level of abstraction that allows you to manage multiple containers as a single unit. Here instead of each container getting an IP address, the **pod gets a single unique IP address** and containers running inside the pod use localhost to connect to each other on **different ports**.

![](Aspose.Words.9dafb7df-2536-44dc-94cb-3f73526b12ad.002.png)

- Pods communicate with each other using the IP address.
- Containers inside a pod connect using localhost on different ports.
- Containers running inside a pod should have different port numbers to avoid port clashes.
- You can set CPU and memory resources for each container running inside the pod.

**How to define a pod:**

Now that we have a basic understanding of a Pod, let’s have a look at how we define a Pod. Pod is a native [Kubernetes Object](https://devopscube.com/kubernetes-objects-resources/) and if you want to create a pod, you need to declare the pod requirements in YAML format. You can also create a pod using the kubectl imperative command.

apiVersion: v1

kind: Pod

**metadata:**

`  `**name**: web-server-pod

`  `labels:

`    `app: web-server

`    `environment: production

`  `annotations:

`    `description: This pod runs the web server

**spec:**

`  `**containers:**

`  `- **name**: web-server

`    `image: nginx:latest

`    `ports:

`    `- containerPort: 80

![](Aspose.Words.9dafb7df-2536-44dc-94cb-3f73526b12ad.003.png)


**pod lifecycle phases:**

When you deploy a pod, it could typically fall under any one of the following phases.

- **Pending**: It means the pod creation request is successful, however, the scheduling is in process. For example, it is in the process of downloading the container image.
- **Running:** The pod is successfully running and operating as expected. For example, the pod is service client requests.
- **Succeeded:** All containers inside the pod have been successfully terminated. For example, the successful completion of a CronJob object.
- **Failed:** All pods are terminated but at least one container has terminated in failure. For example, the application running inside the pod is unable to start due to a config issue and the container exits with a non-zero exit code.
- **Unknown:** Unknown status of the pod. For example, the cluster is unable to monitor the status of the pod.

















































**You can not use ping for a kuberenets service , why :**

A Kubernetes Service is a stable networking endpoint that sits in front of a set of application *Pods*. Instead of accessing *Pods* directly you access them through the *Service*. The Service exposes a DNS name, virtual IP, and network port that you can use to connect to the Pods behind it.

Combinations that work include:

- name:port
- IP:port

you can reach the application Pods via either of the following sockets:

- web-svc:8080
- 10.20.30.40:8080

The reason why you an’t use **ping** is due to the ***port*** requirement!

The short reason is that a Kubernetes Service only activates when connections arrive on the correct **port**. Unfortunately **ping** doesn’t use **ports** 








**What is RabbitMQ :** 

there are the different protocols defining the means of transportation and the properties of the communication. Some examples of such protocols include SMTP, FTP, HTTP or WebSockets (to name a few), which are all based on TCP/UDP. They deal with the formatting, reliability and finding the correct recipient of a message.

it is a middleware layer that enables different services in your application to communicate with each other without worrying about message loss while providing different quality of service (QoS) requirements.

RabbitMQ is a message-queueing software also known as a message broker or queue manager. Simply said; it is software where queues are defined, to which applications connect in order to transfer a message or messages.

The queue-manager software stores the messages until a receiving application connects and takes a message off the queue. The receiving application then processes the message.

A message broker acts as a middleman for various services (e.g. a web application, as in this example). They can be used to reduce loads and delivery times of web application servers by delegating tasks that would normally take up a lot of time or resources to a third party that has no other job.

Messages are not published directly to a queue; instead, the producer sends messages to an exchange. An exchange is responsible for routing the messages to different queues with the help of bindings and routing keys. A binding is a link between a queue and an exchange.

**One Use Case Example** : In this guide, we follow a scenario where a web application allows users to upload information to a website. The site will handle this information, generate a PDF, and email it back to the user. Handling the information, generating the PDF, and sending the email will, in this example case, take several seconds. That is one of the reasons why a message queue will be used to perform the task. When the user has entered user information into the web interface, the web application will create a "PDF processing" message that includes all of the important information the user needs into a message and place it onto a queue defined in RabbitMQ.

In Kuberenetes it is used to balance loads between workers.

**Connecting to RabbitM and send messages** : 

In order to connect to RabbitMQ in python, we need to install the libraray Pika by 

pip install Pika 

To connect to RabbitMQ from Python, we need to create a connection and a channel. The connection represents a TCP connection to the RabbitMQ broker, while the channel is a virtual connection within the TCP connection that allows us to send and receive messages.

- connection = pika.BlockingConnection(pika.ConnectionParameters('localhost')) channel = connection.channel()

**Or**

- params = pika.URLParameters(

"amqp://rabbitmq-service.rf-rl.svc.cluster.local:5672/%2F?heartbeat=36000&blocked\_connection\_timeout=3600000" )

`            `connection = pika.BlockingConnection(params)      

`            `channel = connection.channel()  

- channel.queue\_declare(queue='hello') ----> name of the queue

`              `message = 'Hello, RabbitMQ!' 

`             `channel.basic\_publish(exchange='', routing\_key='hello', body=message)

we first declare a queue named “hello” and then publish a message to this queue

**Further:**

In a conversation, parties greet each other, exchange verbal banter, and eventually continue on their way. A similar form of communication occurs over low-level TCP connections exposing lightweight channels in RabbitMQ

A **connection (TCP)** is a link between the client and the broker, that performs underlying networking tasks including initial authentication, IP resolution, and networking.

Connections can multiplex over a single TCP connection, meaning that an application can open "lightweight connections" on a single connection. T**his "lightweight connection" is called a channel**. Each connection can maintain a set of underlying channels.

Many applications needs to have multiple connections to the broker, and instead of having many connections an application can reuse the connection, by instead, create and delete channels. Keeping many TCP connections open at the same time is not desired, as they consume system resources

A connection is created by opening a physical TCP connection to the target server. The client resolves the hostname to one or more IP addresses before sending a handshake. The receiving server then authenticates the client.

To send a message or manage queues, a connection is created with the broker before establishing a channel through a client. The channel packages the messages and handles protocol operations. Clients send messages through the channel’s basic\_publish method.

## **Publish a message to the RabbitMQ broker**
We will look at a simple example from the Python library [Pika.](https://github.com/pika/pika)

1. As with all clients, you establish a TCP connection.
1. After that, a logical channel is created for sending data or performing other operations (like the creation of a queue). You provide authorization information when instantiating a BlockingConnection since the broker verifies this information on a per-connection basis.
1. A message is routed to the queue, over the channel.
1. The connection is closed (and so the are all channels in the connection).

connection = pika.BlockingConnection(connection\_parameters)
channel = connection.channel()
channel.basic\_publish(exchange="my\_exchange",
`  `routing\_key="my\_route",
`  `body= bytes("test\_message")
)
connection.close()

you should establish one connection per process with a dedicated channel given to each new thread.

We recommend that each process only creates one TCP connection and uses multiple channels in that connection for different threads.

Use at least one connection for publishing and one for consuming for each app/service/process.

RabbitMQ can apply back pressure on the TCP connection when the publisher is sending too many messages for the server to handle. If you consume on the same TCP connection, the server might not receive the message acknowledgments from the client, thus affecting the consumer performance. With a lower consume speed, the server will be overwhelmed.

Use one channel per thread in your application, and make sure that you don’t share channels between threads as most clients don’t make channels thread-safe.

















**An Error we encountered and why :** 

Pika, the RabbitMQ library for Python, and its underlying library, amqp, are not thread-safe when it comes to sharing a connection object across multiple threads without proper synchronization.

Non-Thread-Safe Connection Objects:

Pika Connection Object: When you create a connection using Pika, it typically uses an underlying connection object from the amqp library. These connection objects are not designed to be accessed concurrently by multiple threads without proper synchronization.

Single-Threaded I/O Loop: Pika and amqp rely on a single-threaded I/O loop to manage communication with the RabbitMQ server. This loop processes events, sends and receives data, and handles network operations. If multiple threads access the same connection without synchronization, they may interfere with the operation of this loop.

Concurrency Issues:

Race Conditions: When multiple threads try to perform operations on the same connection simultaneously, race conditions can occur. For example, one thread may attempt to send a message while another is closing the connection, leading to unpredictable behavior.

Buffering and Data Corruption: Pika uses internal buffers to store outgoing and incoming data. If multiple threads write to these buffers concurrently, it can lead to data corruption and buffer overflows.

Resource Conflicts: Concurrent access can also lead to conflicts over resources like channels and queues, which may not be managed properly when accessed from multiple threads.

Thread Safety with add\_callback\_threadsafe:

To address these issues, Pika provides the add\_callback\_threadsafe function. It allows you to schedule operations on the connection's I/O loop in a thread-safe manner. Here's how it works:

Instead of directly interacting with the connection from multiple threads, you define the operation you want to perform in a callback function.

You then use add\_callback\_threadsafe to schedule this callback function to be executed within the context of the connection's I/O loop. This ensures that operations are serialized and executed one at a time, avoiding concurrency issues.

This approach allows you to safely use a single connection object from multiple threads, as long as you use add\_callback\_threadsafe to coordinate access to the connection.

In summary, the error occurs because sharing a Pika connection object directly across multiple threads can lead to concurrency issues, data corruption, and resource conflicts. To avoid these problems, you should use add\_callback\_threadsafe to schedule operations on the connection's I/O loop in a thread-safe manner, ensuring that interactions with the connection are properly synchronized. This approach helps maintain the integrity and reliability of your RabbitMQ communication in a multithreaded environment.

The problem is that your work takes too long and blocks Pika's I/O loop. This causes heartbeats to be missed, and RabbitMQ thinks your connection is dead.

Till the time the job gets processed and your process comes back to send an ACK, there are many heartbeats missed, and thus the connection gone.

**Ideal Solution (Recommended)**

Use threading and run your code in thread. But pay attention that pika is not therad-safe


**Brokenpipe Error**

This article deals about RabbitMQ error: Broken pipe or closed connection. Why the time-out is occurring even after configuring keep-alive under RabbitMQ, and what the work-around solution was to prevent further connection time-outs.

This error indicates that your connection is dead, either due to the TCP connection being dropped or that RabbitMQ has closed your connection.








