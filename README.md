# What will you need

- At least K8S 1.10
- Enable local persistent volumes feature gates when launching K8S. Refer to this [gist](https://gist.github.com/gopinatht/0eafd7fc2b7929fb6700e147e1df4724#file-kubesprayvagrantwithonevm-L55) on how to do it in Vagrantfile with Kubespray.
- SSH into one of the nodes (lets call it **k8s-01**) you want to use for persistent volume and create the directory /var/local/vol1
- In the persistant-volume.yaml file, change the **values** section to point to the right node name on which the persistent volume should live. In the case of this example it is set to **k8s-01**.

# How to use
Run the following commands:

- kubectl create -f storage-class.yaml
- kubectl create -f persistant-volume.yaml
- kubectl create -f persistent_volume_claim.yaml
- kubectl create -f nginx-pod.yaml


You will notice a directory **/usr/share/nginx/html** when you exec into the **task-pv-pod** pod (kubectl exec -it task-pv-pod bash).

You can add/delete directories and files into this folder and it will persist between pod create/destroys and node reboots.

