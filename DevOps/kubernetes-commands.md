Here’s an expanded cheat sheet with some added details for `kubectl` and `kubeadm` commands. This should help you quickly navigate and execute tasks related to Kubernetes clusters.

---

# **Kubernetes Kubectl & Kubeadm Cheat Sheet**

## **Viewing and Managing Resources**

### **Nodes**
- **List all nodes in the cluster:**
  ```bash
  kubectl get nodes
  ```
- **View detailed information about each node:**
  ```bash
  kubectl get nodes -o wide
  ```
  - *Description:* Shows node IP addresses, status, roles, and additional metadata.

### **Namespaces**
- **List all namespaces in the cluster:**
  ```bash
  kubectl get ns
  ```
  - *Description:* Namespaces allow you to separate resources within a single cluster, useful for managing environments like dev, test, and prod.

### **Pods**
- **View pods in a specific namespace as another user:**
  ```bash
  kubectl get pods -n crawl-pods --as <user>
  ```
    ```bash
  kubectl --kubeconfig <path>/config get pods -n <namespace>
  ```
  - *Description:* Useful for verifying the configuration file and checking user access permissions within specific namespaces, with user impersonation.

### **Services**
- **List services across all namespaces:**
  ```bash
  kubectl get svc -A
  ```
- **List services within a specific namespace with additional details:**
  ```bash
  kubectl get svc -n <namespace> -o wide
  ```
  - *Description:* This provides a more detailed view, including cluster IPs, external IPs, ports, and node ports.

## **Configuration and Certificates Management**

### **Configurations**
- **View the current Kubernetes configuration:**
  ```bash
  kubectl config view
  ```
  - *Description:* Displays details like clusters, users, and contexts. Ideal for verifying or troubleshooting your current setup.

- **View a condensed version of the config file (minimal details):**
  ```bash
  kubectl config view --raw --minify --flatten --output 'jsonpath={.clusters[].cluster.certificate-authority-data}'
  ```
  - *Description:* Useful when you need to extract specific details, such as certificate authority data, for secure connections.

### **Certificates**
- **Check certificate expiration dates:**
  ```bash
  kubeadm certs check-expiration
  ```
  - *Description:* Ensures you stay informed about certificate lifecycles and avoid service disruptions.

- **Renew all Kubernetes certificates:**
  ```bash
  kubeadm certs renew
  ```
  - *Description:* Run this when certificates are near expiry or when implementing security updates.

## **Events Management**

### **Listing Events with Filters**

- **Monitor certain namespace events in live:**
  ```bash
  kubectl get events -n <namespace> --watch
  ```
- **Monitor all events in live, sorted by timestamp:**
  ```bash
  kubectl get events -A --sort-by='.lastTimestamp' --watch
  ```
- **Show only warning events across all namespaces:**
  ```bash
  kubectl get events -A --field-selector type=Warning
  ```
- **Show events that are not related to pods:**
  ```bash
  kubectl get events --field-selector involvedObject.kind!=Pod
  ```
  - *Description:* This can help pinpoint issues related to nodes, services, or other resources.

## **Managing Pods and Logs**

### **Executing Commands in Pods**
- **Run a shell command interactively in a pod:**
  ```bash
  kubectl exec -it <pod-name> -n <namespace> bash
  ```
  - *Description:* Useful for debugging within containers, accessing logs, or checking configurations inside a specific pod.

### **Fetching Logs**
- **Stream logs from a deployment’s pod with a specific timeframe:**
  ```bash
  kubectl logs deploy/<deployment-name> -n <namespace> --since=10m -f
  ```
  - *Description:* Great for troubleshooting recent issues or monitoring ongoing processes in live. The --since flag is particularly useful when you need to focus on logs from the past few minutes or hours, helping you avoid wading through older, unrelated log entries.

- **Stream logs from a pod with a specific timeframe:**
  ```bash
  kubectl logs pod/<pod-name> -n <namespace> --since=10m -f
  ```
  - *Description:* Great for troubleshooting recent issues or monitoring ongoing processes in real-time. The --since flag is particularly useful when you need to focus on logs from the past few minutes or hours, helping you avoid wading through older, unrelated log entries.

## **ConfigMap Management**

### **Editing ConfigMap**
- **Edit a ConfigMap in the specified namespace:**
  ```bash
  kubectl edit cm -n kube-system kubeadm-config
  ```
  - *Description:* ConfigMaps store configuration data for applications, which can be edited to change the behavior of Kubernetes components.

## **Labels & Taints for Nodes**

### **Adding Labels**
- **Add a custom label to a node, e.g., for storage roles:**
  ```bash
  sudo kubectl label nodes <node-name> role=storage-node
  ```
  - *Description:* Node labels help in organizing and selecting nodes for specific purposes.

### **Applying Taints**
- **Add a taint to prevent pods from being scheduled on a node unless they tolerate the taint:**
  ```bash
  sudo kubectl taint nodes <node-name> node-role.kubernetes.io/storage-node:NoSchedule
  ```
  - *Description:* Taints help ensure that only specific pods, which tolerate the taints, are scheduled on the node.

## **Additional Administrative Commands**

### **Token Management**
- **Generate a token for adding nodes to the cluster:**
  ```bash
  sudo kubeadm token create --print-join-command
  ```
  - *Description:* This will output a command that can be run on new nodes to join them to the cluster.

### **Converting to Base64**
- **Convert file contents to Base64 encoding:**
  ```bash
  sudo cat <filename>.crt | base64 | tr -d "\n"
  ```
  - *Description:* This is helpful when you need to include certificates in configurations or secrets securely.

- **Convert string contents to Base64 encoding:**
  ```bash
  sudo echo "<string>" | tr -d "\n" | base64 
  ```
  - *Description:* This is helpful when you need to include secrets values in secrets securely.
---
