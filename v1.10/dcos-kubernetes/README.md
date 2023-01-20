## To reproduce:

This Kubernetes conformance report is generated by Kubernetes on DC/OS.

### Provision the Kubernetes cluster

To recreate these results, first you need to provision a DC/OS cluster and
install the Kubernetes package. To do so, please follow [these instructions](https://github.com/mesosphere/dcos-kubernetes-quickstart/blob/master/docs/cncf_conformance.md).

When the Kubernetes cluster is up and running, proceed to run the conformance tests.

### Run conformance tests

Start the conformance tests:

```bash
$ curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl apply -f -
```

Then follow Sonobuoy's logs:

```bash
$ kubectl logs -f -n sonobuoy sonobuoy
```

and wait for the follow line to show up:

>no-exit was specified, sonobuoy is now blocking


At this point, copy the results to your working directory:

```bash
$ kubectl cp sonobuoy/sonobuoy:/tmp/sonobuoy .
```

Finally, unarchive the test results. You will find them in `plugins/e2e/results/{e2e.log,junit.xml}`.

### Clean-up

Let's start by deleting the conformance test resources:

 ```bash
 $ curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl delete -f -
 ```

 Next, if you'd like, you can follow [these instructions](https://github.com/mesosphere/dcos-kubernetes-quickstart/blob/master/docs/cncf_conformance.md)
 to delete the entire infrastructure.