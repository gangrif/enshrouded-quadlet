#A basic deployment of enshrouded-server in qadlet/podman

##Setup
In enshrouded-configmap.yaml you will find two variables you must define
SERVER_NAME - This should be set to your desired server name
SERVER_PASSWORD - This should be set to the password that players will need in order to connect to your server

In enshrouded-pod.yaml You will find a volumes section at the bottom, I have used hostpaths, if you choose to use volumes you will need to modify this configuration.  

At the very least, you will likely need to change the path to your data.

I may switch my deployment to use a voume def, so that config can be dropped in more easily, but for now, it is what it is.

##Quadlet
I set this up to easily drop into quadlet. 
In quadlet/enshourded-pod.kube you will find paths to the configmap and the pod yaml, update those to where you store those two files. 

Then drop enshrouded-pod.kube into /etc/containers/systemd and run
```systemctl daemon-reload```

Once this reloads, you should be able to simply 
```systemctl start enshrouded-pod```

Dont forget to open ports 15636-15637/udp

##Podman
If instead you'd rather just have podman run the pod. 

podman play kube --configmap /path/to/enshrouded-configmap.yaml /path/to/enshrouded-pod.yaml 

Again, be sure to open ports 15636-15637/udp
