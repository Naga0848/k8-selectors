# This repo contains all the details about topics like 
    NodeSelectors, 
    Taints and Tolerations, 
    Affinity and Anti-Affinity

# In order to use  NodeSelectors, Taints and Tolerations, Affinity and Anti-Affinity we need to first apply labels on the desired node
        First we should add labels to the node >>> kubectl label nodes <node-ip-address> hardware=gpu
        here key=hardware and value=gpu
        After adding these kind of kabels, we can proceed with the NodeSelectors, Taints and Tolerations, Affinity and Anti-Affinity rules

    # Understanding NodeSelectors:-
        If we want, we can schedule a particular pod on to a specific node by using NodeSelector
        In the Pod defenition file we should use a NodeSelector and this NodeSelector is a label on that respective node(kubectl get nodes --show-labels)
        Here for this kind of pods, we use ImagePullPolicy 
            ImagePullPolicy: Always is used in a Pod
            This we have other than Always value, node cannot pull the images from the DockerHub if we did any changes to the code and built a new image
            Other ImagePullPolicies are IfNeverPresent and Never

    # Understanding Node Affinity and Anti-Affinity
        Before a pod gets scheduled on a node and gets executed, there is a chance that the labels of that pod can be changed by our colleague.
        These can be implemented by using the Node Affinity and Anti-Affinity Rules
        Affinity:-  Affinity  ==== Like === Ishtam === The node should attract the pod (this happens when they have same labesl on them)
            Affinity = NodeSelector + more matching rules with operators like In, Exists, NotExist, Greaterthan, Lessthan etc
            Rule - 1 is requiredDuringSchedulingIgnoredDuringExecution(Hardrule)
                pod status goes to pending if node labels are not matched with the pod NodeSelectors i.e., Scheduler will not schedule that pod.
            Rule - 2 is preferredDuringSchedulingIgnoredDuringExecution(Softrule)
                If labels of a node are not matched with the pod NodeSelector, the selector will try to schedule on the different nodes.
            kubectl label nodes <ip-address-of-node> hardware=gpu   >>>> adding a label to a node
                In the above command key is hardware and value is gpu which has to beused in a pod at NodeSelector

        


            



