# wca-4-oom-fix

This playbook demonstrates how to simulate an Out of Memory issue (OOMKilled error) for a pod and fixing this issue with the help of an Ansible Playbook which is generated using IBM Watsonx Code Assistant (WCA) for Ansible Lightspeed. 

## Prequisites

Any flavor of Kubernetes Cluster 
kubectl command line utitliy
VS Code Editor configured with Ansible Lightspeed powered by WCA

# Steps

1. Clone this repository in your machine and navigate into it.
```
git clone https://github.com/dimallya/wca-4-oom-fix
cd wca-4-oom-fix
```


2. In the CLI login to K8s cluster using `kubectl login` command. Create a namespace viz. `robot-shop`
```
kubectl create ns robot-shop
```

3. Create `app-review` pod by executing following command
```
kubectl create -f review-pod.yaml
```
Memory request and limit for the container this pod are 50Mi and 100Mi respectively. However, due to the excess load (simulated stress) it needs 150Mi of memory which is exceeding its resource limit values. Hence this pod goes into **CrashLoopBackOff** and then **OOMKilled** state.

4. Open scale-app-review.yml file VS Code editor configured with Ansible Lightspeed to get Ansible code recommendations from WCA. Uncomment each tasks (prompt) one by one and Press Enter at the end of each task description to get Ansible code from WCA. Press Tab to accept. If any further modification is required, edit the code accordingly. 

5. When the playbook generation is completed, execute the playbook. As the we are scaling up the container resources (by assigning higher memory resources -request as 150Mi and limit as 200Mi) and recreating the pod, it would come to **Running** state without any "out of memory" issues. 