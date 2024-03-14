# wca-4-oom-fix

This repository demonstrates how to simulate an Out of Memory issue (OOMKilled error) for a pod and fixing the same with the help of an Ansible Playbook which is generated using IBM Watsonx Code Assistant (WCA) for Ansible Lightspeed. 

## Prequisites

- Any flavor of Kubernetes Cluster 
- `kubectl` command line utility
- VS Code Editor configured with Ansible Lightspeed powered by WCA (Links provided in [References](https://github.com/dimallya/wca-4-oom-fix/tree/main?tab=readme-ov-file#references) section)

## Steps

1. Clone this repository in your machine and navigate into it.
```
git clone https://github.com/dimallya/wca-4-oom-fix
cd wca-4-oom-fix
```


2. In the CLI login to your K8s cluster. Create a namespace viz. `robot-shop`:
```
kubectl create ns robot-shop
```

3. Create `app-review` pod by executing following command:
```
kubectl create -f review-pod.yaml
```
Memory request and limit for the container in this pod are 50Mi and 100Mi respectively. However, due to the excess load (simulated stress) it needs 150Mi of memory which is exceeding its resource limit values. Hence this pod goes into **CrashLoopBackOff** and then **OOMKilled** state.

4. Open `scale-app-review.yml` file VS Code editor configured with Ansible Lightspeed to get Ansible code recommendations from WCA. Uncomment each tasks (prompt) one by one (Line #14 to #22) and press **Enter** at the end of each task description to get Ansible code from WCA. Press **Tab** to accept. If any further modification is required, edit the code accordingly. 

5. When the playbook generation is completed, execute the Ansible playbook. As the we are scaling up the container resources (by assigning higher memory resources i.e request as 150Mi and limit as 200Mi) and recreating the pod, it would come to **Running** state successfully without any "out of memory" issues.

## References
1. Installing the Ansible VS Code extension: https://docs.ai.ansible.redhat.com/vscode_guide/installing_vs/
2. Using the Ansible VS Code extension: https://docs.ai.ansible.redhat.com/vscode_guide/using_vs/
3. Configuring RH Ansible Lightspeed with WCA: [Link](https://access.redhat.com/documentation/en-us/red_hat_ansible_lightspeed_with_ibm_watsonx_code_assistant/2.x_latest/html/red_hat_ansible_lightspeed_with_ibm_watsonx_code_assistant_user_guide/configure-code-assistant_lightspeed-user-guide#doc-wrapper)
4. Ansible K8s module documentation: https://docs.ansible.com/ansible/latest/collections/kubernetes/core/k8s_module.html
