#### This repo contains all the details about topics like 
    NodeSelectors, 
    Taints and Tolerations, 
    Affinity and Anti-Affinity

#### In order to use  NodeSelectors, Taints and Tolerations, Node Affinity & Anti-Affinity  and Pod Affinity &  Anti-Affinity we need to first apply labels on the desired node
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
        Node Affinity will be more flixible when compare to the NodeSelectors as it has more values

        Anti-Affinity:-
            If we use NotIn operator in the pod definition file, the pod will be scheduled on other than this particular node
    
    # Understanding Pod Affinity and Anti-Affinity
        If pod-1 is on a node 192.23.36.25
        And pod-2 like to be with the pod-1 only then Pod Affinity rules comes into picture
        Pod Affinity:-
        Here also we have two rules
            Rule - 1 is requiredDuringSchedulingIgnoredDuringExecution(Hardrule)
                If pod-2 labels and node labels are matched then pod-2 goes onto the same node where pod-1 is scheduled, otherwise the pod+2 goes to pending status.
            Rule - 2 is preferredDuringSchedulingIgnoredDuringExecution(Softrule)
                If pod-2 labels are matched with the node labels then pod-2 goes onto the node where pod-1 is scheduled, otherwise the schedules the pod-2 onto a different node.
        Why Pod affinity is required ?
            In general application hits DB, if a user is requesting something and displays data to the user
            If the data requested by the user is already present in a Cache, then application need to go to DB and this saves the time and increases the performance. This is happens when application pod and cache are in the same node i.e., by using the  Pod Affinity rules.
        Pod Anti-Affinity:-
            This is completely opposite to the Pod Affinity
            The pod goes to the pending status or gets scheduled on a different node if we are using the Pod Anti-Affinity rules.       
        


            



