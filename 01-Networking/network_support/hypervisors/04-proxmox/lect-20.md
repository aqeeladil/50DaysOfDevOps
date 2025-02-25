# Kubernetes Cluster Setup on Proxmox

This guide provides step-by-step instructions to set up a **Kubernetes cluster** on **Proxmox**. The cluster will consist of a **control plane (master node)** and **worker nodes**, all running **Ubuntu Server 22.04**. By the end of this guide, you will have a fully functional Kubernetes cluster and a sample application deployed.

---

## **Prerequisites**
Before starting, ensure you have the following:
1. **Proxmox VE** installed and running.
2. At least **2 virtual machines (VMs)** running **Ubuntu Server 22.04**.
   - One VM will act as the **control plane (master node)**.
   - The other(s) will act as **worker nodes**.
3. Sufficient resources (CPU, RAM, and storage) for the VMs.
4. Basic familiarity with Linux commands and Proxmox.

---

## **Step 1: Set Up Virtual Machines in Proxmox**
1. **Create a Template**:
   - Use an **Ubuntu 22.04 cloud image** to create a VM template in Proxmox.
   - Follow the steps in the **LearnLinuxTV** video to create and configure the template.

2. **Clone the Template**:
   - Clone the template to create at least **2 VMs**:
     - One for the **control plane** (e.g., `k8s-ctrl`).
     - One or more for **worker nodes** (e.g., `k8s-node1`, `k8s-node2`).

3. **Configure VM Resources**:
   - Assign at least **2 CPU cores** and **2GB RAM** to the control plane.
   - Assign at least **1 CPU core** and **1GB RAM** to each worker node.

4. **Start the VMs**:
   - Boot the VMs and ensure they are accessible via SSH.

---

## **Step 2: Configure Networking**
1. **Assign Static IPs**:
   - Edit the Netplan configuration on each VM to assign static IPs.
   - Example for the control plane (`k8s-ctrl`):
     ```bash
     sudo nano /etc/netplan/50-cloud-init.yaml
     ```
     Add the following configuration:
     ```yaml
     network:
       ethernets:
         eth0:
           addresses:
             - 10.10.10.213/24
           nameservers:
             addresses:
               - 10.10.10.1
           routes:
             - to: 0.0.0.0/0
               via: 10.10.10.1
     ```
   - Apply the changes:
     ```bash
     sudo netplan apply
     ```

2. **Disable Swap**:
   - Kubernetes does not work well with swap enabled. Disable it on all nodes:
     ```bash
     sudo swapoff -a
     sudo sed -i '/swap/d' /etc/fstab
     ```

---

## **Step 3: Install Kubernetes Components**
1. **Install `containerd` (Container Runtime)**:
   - Install `containerd` on all nodes:
     ```bash
     sudo apt update
     sudo apt install -y containerd
     ```
   - Configure `containerd`:
     ```bash
     sudo mkdir -p /etc/containerd
     containerd config default | sudo tee /etc/containerd/config.toml
     sudo systemctl restart containerd
     ```

2. **Install Kubernetes Tools**:
   - Add the Kubernetes repository and install `kubeadm`, `kubectl`, and `kubelet`:
     ```bash
     sudo apt update
     sudo apt install -y apt-transport-https ca-certificates curl
     curl -fsSL https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-archive-keyring.gpg
     echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
     sudo apt update
     sudo apt install -y kubelet kubeadm kubectl
     sudo apt-mark hold kubelet kubeadm kubectl
     ```

---

## **Step 4: Initialize the Kubernetes Cluster**
1. **Initialize the Control Plane**:
   - On the control plane node (`k8s-ctrl`), run:
     ```bash
     sudo kubeadm init --control-plane-endpoint=10.10.10.213 --pod-network-cidr=10.244.0.0/16
     ```
   - Save the `kubeadm join` command output for adding worker nodes.

2. **Configure `kubectl`**:
   - Set up `kubectl` for the current user:
     ```bash
     mkdir -p $HOME/.kube
     sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
     sudo chown $(id -u):$(id -g) $HOME/.kube/config
     ```

3. **Install a Pod Network (Flannel)**:
   - Deploy the Flannel network plugin:
     ```bash
     kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
     ```

---

## **Step 5: Join Worker Nodes**
1. **Run the `kubeadm join` Command**:
   - On each worker node, run the `kubeadm join` command saved earlier:
     ```bash
     sudo kubeadm join 10.10.10.213:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>
     ```

2. **Verify Node Status**:
   - On the control plane, check the status of the nodes:
     ```bash
     kubectl get nodes
     ```
   - All nodes should show as `Ready`.

---

## **Step 6: Deploy an Application**
1. **Create an NGINX Pod**:
   - Create a YAML file (`nginx-pod.yaml`):
     ```yaml
     apiVersion: v1
     kind: Pod
     metadata:
       name: nginx-example
       labels:
         app: nginx
     spec:
       containers:
         - name: nginx
           image: nginx
           ports:
             - containerPort: 80
     ```
   - Deploy the pod:
     ```bash
     kubectl apply -f nginx-pod.yaml
     ```

2. **Expose the Pod via NodePort**:
   - Create a `NodePort` service (`nginx-service.yaml`):
     ```yaml
     apiVersion: v1
     kind: Service
     metadata:
       name: nginx-service
     spec:
       type: NodePort
       ports:
         - port: 80
           targetPort: 80
           nodePort: 30080
       selector:
         app: nginx
     ```
   - Deploy the service:
     ```bash
     kubectl apply -f nginx-service.yaml
     ```

3. **Access the Application**:
   - Open a web browser and navigate to `http://<node-ip>:30080`.
   - You should see the NGINX welcome page.

---

## **Conclusion**
By following this guide, you have successfully set up a **Kubernetes cluster** on **Proxmox** and deployed a sample application. This setup is ideal for learning, testing, and small-scale deployments. For production environments, consider using a more robust setup with high availability and additional security measures.

---

## **Additional Resources**
- [Kubernetes Documentation](https://kubernetes.io/docs/home/)
- [Proxmox VE Documentation](https://pve.proxmox.com/wiki/Main_Page)
- [LearnLinuxTV YouTube Channel](https://www.youtube.com/c/LearnLinuxTV)

---

