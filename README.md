# jaeger-all-in-one
The Jaeger all-in-one yaml template is adapted from https://raw.githubusercontent.com/jaegertracing/jaeger-kubernetes/master/all-in-one/jaeger-all-in-one-template.yml, by modifying the deployment manifest:
1.  apiVersion: apps/v1
2.  spec: <br>
      selector: <br>
        matchLabels: <br>
          app: jaeger <br>
        
It has been tested to work with istio in a Katacoda Kubernetes playground.

Run these commands on the master node to install Jaeger and change the jaeger-query service type to NodePort. <br>
$ kubectl create -n istio-system -f https://raw.githubusercontent.com/snpsuen/jaeger-all-in-one/master/jaeger-all-in-one-template.yaml <br>
$ kubectl patch service jaeger-query -p '{"spec":{"type": "NodePort"}}' -n istio-system <br>
$ kubectl get service jaeger-query -n istio-system
