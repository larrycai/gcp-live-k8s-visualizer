## Kubernetes/Container Engine Visualizer

// cloned from https://github.com/saturnism/gcp-live-k8s-visualizer with different labelSelector
// https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#set-based-requirement

This is a simple visualizer for use with the Kubernetes API using labelSelector "tie in (frontend, backend)"

It will fit for the demo of https://github.com/kubernetes/kubernetes/blob/master/examples/guestbook/all-in-one/guestbook-all-in-one.yaml

## Usage:
   * First install a Kubernetes
   * ```git clone https://github.com/larrycai/gcp-live-k8s-visualizer.git```
   * ```kubectl proxy --www=gcp-live-k8s-visualizer --address 0.0.0.0 --accept-hosts '.*' --port 8178```

That's it.  The visualizer uses labels to organize the visualization.  In particular it expects that

   * pods, replicationcontrollers, and services have a ```name``` label, and pods and their associated replication controller share the same ```name```, and
   * the pods in your cluster will have a ```uses``` label which contains a comma separated list of services that the pod uses.

   ```
   * Access visualizer via Public IP of EC2 instance on which you created it:
    ```
   http://<public ip>:8178/static/
   ```

### Playground ###
 
   the playground url is like http://ip10-0-15-4-8178.host2.labs.play-with-k8s.com/ , the `ip10-0-15-4` is the real virtual ip (`10.0.15.4`) for the master node

## Demo ##

the basic demo is 

    kubectl run whoami --image=larrycai/whoami -l tier=frontend --port=5000
    kubectl expose deploy whoami --type=NodePort -l tier=frontend # may not needed
    kubectl scale --replicas=8 deployment/whoami # scale out
    kubectl scale --replicas=1 deployment/whoami # scale ine
    
### Guestbook demo ###

    kubectl create -f https://git.io/v7ytR # shorturl to guestbook-all-in-one.yaml

## Reference

* guestbook: https://github.com/kubernetes/kubernetes/blob/master/examples/guestbook/all-in-one/guestbook-all-in-one.yaml
* codingwithme k8s: https://github.com/larrycai/codingwithme-k8s
* blog: http://kubecloud.io/guide-setting-up-visualizer-for-kubernetes/
* playground: http://labs.play-with-k8s.com/ 
