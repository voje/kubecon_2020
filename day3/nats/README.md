# Adding my own notes (kristjan)
First, let's set up a k8s with NATS.   

```bash
$ minikube start

$ kubectl apply -f https://raw.githubusercontent.com/nats-io/k8s/master/nats-server/single-server-nats.yml
configmap/nats-config created
service/nats created
statefulset.apps/nats created

$ kubectl apply -f https://raw.githubusercontent.com/nats-io/k8s/master/nats-streaming-server/single-server-stan.yml
configmap/stan-config created
service/stan created
statefulset.apps/stan created

$ k get pods
NAME     READY   STATUS              RESTARTS   AGE
nats-0   0/1     Running             0          15s
stan-0   0/1     ContainerCreating   0          5s

$ kubectl run -i --rm --tty nats-box --image=synadia/nats-box --restart=Never
If you don't see a command prompt, try pressing enter.
nats-box:~# nats
/bin/sh: nats: not found
nats-box:~# nats-sub 
Usage: nats-sub [-s server] [-creds file] [-t] <subject>
  -creds string
    	User Credentials File
  -h	Show help message
  -q string
    	Queue Group Name (default "NATS-RPLY-22")
  -s string
    	The NATS System (default "connect.ngs.global")
  -t	Display timestamps
  -v	Show version
nats-box:~# nats-sub -s nats
Usage: nats-sub [-s server] [-creds file] [-t] <subject>
  -creds string
    	User Credentials File
  -h	Show help message
  -q string
    	Queue Group Name (default "NATS-RPLY-22")
  -s string
    	The NATS System (default "connect.ngs.global")
  -t	Display timestamps
  -v	Show version
nats-box:~# nats-sub -s nats hello-chan &
nats-box:~# Listening on [hello-chan]

nats-box:~# nats-pub -s nats hello-chan hey
[#1] Received on [hello-chan]: 'hey'
nats-box:~# 
```

Demo seems to be working.   
