# deployment-monitoring-tutorial

## Reflection on Hello Minikube

1. Compare the application logs before and after you exposed it as a Service. Try to open the app several times while the proxy into the Service is running. What do you see in the logs? Does the number of logs increase each time you open the app?

Before:
![alt text](image.png)

After:
![alt text](image-1.png)

*Yes, the number of logs increases each time I access the app because each HTTP request to the service is logged by the application. This demonstrates that the Service is successfully routing external traffic to the Pod.*

2. Notice that there are two versions of `kubectl get` invocation during this tutorial section. The first does not have any option, while the latter has `-n` option with value set to `kube-system`. What is the purpose of the `-n` option and why did the output not list the pods/services that you
explicitly created?

Without -n:
![alt text](image-2.png)

With -n:
![alt text](image-3.png)

The -n option in kubectl stands for "namespace" and is used to specify which Kubernetes namespace to query or operate on.
When we ran kubectl get pods and kubectl get services without the -n option, it showed resources in the default namespace, which included our hello-node deployment and service.
When we ran kubectl get pods,services -n kube-system, it showed resources in the kube-system namespace, which contains system-level components like:

coredns (DNS server)
etcd (key-value store)
kube-apiserver (API server)
metrics-server (resource monitoring)

*The `-n` option in kubectl stands for "namespace" and is used to specify which Kubernetes namespace to query or operate on.*

*When we ran `kubectl get pods` and `kubectl get services` without the `-n` option, it showed resources in the `default` namespace, which included our hello-node deployment and service.*

*When we ran `kubectl get pods,services -n kube-system`, it showed resources in the `kube-system` namespace, which contains system-level components like:*
- *coredns (DNS server)*
- *etcd (key-value store)*
- *kube-apiserver (API server)*
- *metrics-server (resource monitoring)*

*The output didn't list the pods/services we explicitly created because those were created in the `default` namespace, while the `-n kube-system` command only shows resources in the `kube-system` namespace. Kubernetes uses namespaces to logically separate and organize resources, providing isolation between different applications or environments.*
