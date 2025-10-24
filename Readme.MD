# This repo contains all the details about topics like 
    NodeSelectors, 
    Taints and Tolerations, 
    Affinity and Anti-Affinity

    First we should add labels to the node >>> kubectl label nodes <node-ip-address> hardware=gpu
        here key=hardware and value=gpu
    After adding these kind of kabels, we can do NodeAffinity or NodeSelectors

    