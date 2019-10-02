# programming_kubernetes

## Events, the DNA of Kubernetes 

* kubernetes component
![k8s-arch](https://user-images.githubusercontent.com/33475309/65926748-bef88800-e431-11e9-93ff-b84ec7bfdce6.png)

* 모든것은 control loop 를 통하여 처리되고 api server를 통해 통신한다.

## 쿠버네티스 이벤트흐름

<img width="550" alt="k8s-api-server-queues" src="https://user-images.githubusercontent.com/33475309/65926992-eac83d80-e432-11e9-95fb-e9be27a00775.png">


## using custom resource
~~~go
import (
      metav1 "k8s.io/apimachinery/pkg/apis/meta/v1"
             "k8s.io/client-go/tools/clientcmd"
             "k8s.io/client-go/kubernetes"
  )
  
kubeconfig = flag.String("kubeconfig", "~/.kube/config", "kubeconfig file")
flag.Parse()
config, err := clientcmd.BuildConfigFromFlags("", *kubeconfig)
clientset, err := kubernetes.NewForConfig(config)

pod, err := clientset.CoreV1().Pods("book").Get("example", metav1.GetOptions{})
~~~

* import meta/v1 패키지는 metav1.Getoptions 를 사용하기위해
* import clientcmd 는 kubeconfig를 읽고 parsing 하기 위해 사용되었음
* import kubernets 는 kubernetes resource 를 위해 

* pod, err := clientset.CoreV1().Pods("book").Get("example", metav1.GetOptions{})
* The Get call sends an HTTP GET request to /api/v1/namespaces/book/pods/example on the server
