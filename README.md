# jaeger-all-in-one

Breaking news (7 April 2021): <br>
The latest jaegertracing/all-in-one docker image does not work properly with Istio 1.9.2. It ignores any built-in or user-defined micro services of the Istio service mesh, except jaeger-query. <br>
A quick fix is to fall back to an older jaegertracing image like jaegertracing/all-in-one:1.20.0 by using the patched template manifest: <br>
$ kubectl create -n istio-system -f https://raw.githubusercontent.com/snpsuen/jaeger-all-in-one/master/jaeger-all-in-one-template_1200.yaml <br>
<p>
--- <br>
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
