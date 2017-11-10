# kubernetes on aws using kops

# Cluster info

* cluster deployed using
  [this guide](https://kubernetes.io/docs/getting-started-guides/kops/).

* cluster name is `apsoutheast2.kubernetes.sandbox.tas2.rocks`.

* route53 subdomain is `apsoutheast2.kubernetes.sandbox.tas2.rocks`.

* cluster state is kept in s3 bucket
  `s3://clusters.kubnernetes.sandbox.tas2.rocks`.

# Quick deploy instructions for `apsoutheast2.kubernetes.sandbox.tas2.rocks`

**read [this guide](https://kubernetes.io/docs/getting-started-guides/kops/)
before you continue!!!!**

* if redeploying `apsoutheast2.kubernetes.sandbox.tas2.rocks`, then the buckets
  and zones should already exist.

* set `KOPS_STATE_STORE`:
    ```bash
    export KOPS_STATE_STORE=s3://clusters.kubnernetes.sandbox.tas2.rocks
    ```

* create the cluster:
    ```bash
    kops create cluster --zones=ap-southeast-2c apsoutheast2.kubernetes.sandbox.tas2.rocks
    ```

* modify the instance groups using the following commands:
    ```bash
    kops edit ig --name=apsoutheast2.kubernetes.sandbox.tas2.rocks master-ap-southeast-2c
    kops edit ig --name=apsoutheast2.kubernetes.sandbox.tas2.rocks nodes
    ```

* add `Operating Schedule` tags by adding the following yaml to the `spec`
  section of each instance group:
    ```yaml
    spec:
      cloudLabels:
        Operating Schedule: 24x7
    ```

* create the cluster in AWS (no-op unless `--yes` is specified):
    ```bash
    kops update cluster apsoutheast2.kubernetes.sandbox.tas2.rocks
    kops update cluster apsoutheast2.kubernetes.sandbox.tas2.rocks --yes
    ```

* delete cluster:
    ```bash
    kops delete cluster --name apsoutheast2.kubernetes.sandbox.tas2.rocks
    ```

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

