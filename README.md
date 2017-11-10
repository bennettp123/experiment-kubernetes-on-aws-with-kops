# kubernetes on aws using kops

# Cluster info

* cluster deployed using
  [this guide](https://kubernetes.io/docs/getting-started-guides/kops/).

* cluster name is `apsoutheast2.kubernetes.sandbox.tas2.rocks`.

* route53 subdomain is `apsoutheast2.kubernetes.sandbox.tas2.rocks`.

* cluster state is kept in s3 bucket
  `s3://clusters.kubnernetes.sandbox.tas2.rocks`.

# Dashboard

* dashboard was deployed using
  [quickstart](https://github.com/kubernetes/dashboard#getting-started).

* obtain the kubectl config file (talk to Bennett).

* save it to `~/.kube/config`

* launch dashboard using `kubectl proxy`

* connect to dashboard at [http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/](http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/).

* if prompted for creds, click `skip`.

Alternatively, you can save the kubeconfig to a different file, and
call kubectl with `--kubeconfig=path/to/kubeconfig`.

