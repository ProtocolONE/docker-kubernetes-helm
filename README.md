# kubernetes-helm

Image providing [kubernetes](http://kubernetes.io/) tools `kubectl` and `helm`.

## Overview

The main purpose of this image is to use it in CI pipelines, e.g. to deploy an
application using `helm`.

For example, for [Gitlab CI](https://about.gitlab.com/features/gitlab-ci-cd/):

```yaml
...

deploy-staging:
  image: p1hub/kubernetes-helm
  stage: deploy
  before_script:
    - kubectl config set-cluster ${KUBE_NAME} ...
    - kubectl config set-credentials ${KUBE_USER} ...
    - kubectl config set-context ${KUBE_NAME}
        --cluster="${KUBE_NAME}"
        --user="${KUBE_USER}"
        --namespace="${KUBE_NAMESPACE}"
    - kubectl config use-context ${KUBE_NAME}
  script:
    - helm init --client-only
    - helm install release-name chart/name --namespace ${KUBE_NAMESPACE}

...
```