Objective:

● Deploy a sample application (e.g., nginx) on a Kubernetes cluster.

● Configure the application for high availability.

● Implement rolling updates for the application.


step1: I've configured a Deployment manifest with podAntiAffinity of type RequiredDuringSchedulingIgnoredDuringExecution to distribute nginx pods across nodes in the cluster. This setup aims to enhance high availability by ensuring that no two nginx pods are scheduled on the same node. In case of a node failure, the remaining nodes can seamlessly handle incoming requests.

![nginx-deployment_HA](https://github.com/Akash-29-1995/Kubenetes/assets/45091399/0ad1eddb-2f5f-4ab0-a05b-8c08eb4b1d50)

Note: Here I want to mention one more thing that is I have initially run the two nodes in eks cluster but face a problem because here I was running 2 replicas, as per podAntiAffinity only one pod can be scheduled on the node at a time but in rolling updated strategy it says old pod will terminate when new comes up, so, in this case, try to set replica count to 1 and apply it, once new pod comes up then old will terminate after that you can scale it to 2 or 3 or as per your requirement but in the real-world scenario in the live project generally we are using cluster autoscaler to handle this situation.

step2: To achieve rolling update, I have added a strategy to mention the deployment type in the manifest.

![Screenshot from 2024-04-14 23-22-33](https://github.com/Akash-29-1995/Kubenetes/assets/45091399/3357aadf-6981-4b0c-89b4-ddc8ca639e31)
