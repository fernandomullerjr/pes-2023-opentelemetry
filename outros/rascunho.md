


- Kubernetes com pods em pending

~~~~bash
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl get pod -A
NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   coredns-5dd5756b68-7vdkb              0/1     Pending   0          27d
kube-system   coredns-5dd5756b68-84rbg              0/1     Pending   0          27d
kube-system   etcd-debian10x64                      1/1     Running   1137       27d
kube-system   kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system   kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system   kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system   kube-scheduler-debian10x64            1/1     Running   25         27d

~~~~


- Tratar pods em pending, antes de subir o backend.






- Resolvida questão do disco.


- Novo erro:

~~~~bash
Events:
  Type     Reason                  Age                  From               Message
  ----     ------                  ----                 ----               -------
  Warning  FailedScheduling        6h59m (x18 over 8h)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling        149m (x2 over 154m)  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling        10m (x4 over 25m)    default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.kubernetes.io/disk-pressure: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Normal   Scheduled               6m                   default-scheduler  Successfully assigned kube-system/coredns-5dd5756b68-7vdkb to debian10x64
  Warning  FailedCreatePodSandBox  5m10s                kubelet            Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(0ebf8324d299f913dce4596373d288a48dba439eafb49b8bf1bb991d21e73700): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  4m7s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(5251c57c1c9443673c5bb73e6ea55acc934da7758e9eb6e6d5a229db69e9b4f7): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  3m6s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(6e3d9e9372b7ad119604abae8b1ae62a4e4514ed1edee04aa7f24d61c37ed4e9): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  2m4s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(cf96f56b30dc32b6b66fbd7ffac2eab9f98a0d9c6686642aeb4571ed6cd4e6a4): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
  Warning  FailedCreatePodSandBox  58s  kubelet  Failed to create pod sandbox: rpc error: code = Unknown desc = failed to create pod network sandbox k8s_coredns-5dd5756b68-7vdkb_kube-system_2ba615e6-b0c1-4b27-be36-f4271b935f2c_0(009dc0d8defea03d9f8b3f672f38c984ebd442296c56bad068515670e64b7f0d): error adding pod kube-system_coredns-5dd5756b68-7vdkb to CNI network "cilium": plugin type="cilium-cni" failed (add): unable to connect to Cilium daemon: failed to create cilium agent client after 30.000000 seconds timeout: Get "http://localhost/v1/config": dial unix /var/run/cilium/cilium.sock: connect: no such file or directory
Is the agent running?
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~






- Tratar erro do Cilium.

~~~~bash
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# helm install cilium cilium/cilium --namespace kube-system -f /home/fernando/cursos/cka-certified-kubernetes-administrator/Secao7-Security/148-x-cilium-values.yaml
NAME: cilium
LAST DEPLOYED: Sat Mar 23 21:57:54 2024
NAMESPACE: kube-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
You have successfully installed Cilium with Hubble.

Your release version is 1.14.1.

For any further help, visit https://docs.cilium.io/en/v1.14/gettinghelp
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# date
Sat 23 Mar 2024 09:57:57 PM -03
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# helm ls -A
NAME    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART           APP VERSION
cilium  kube-system     1               2024-03-23 21:57:54.364581094 -0300 -03 deployed        cilium-1.14.1   1.14.1
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~


## PENDENTE
- Tratar pods em pending, antes de subir o backend.
- Tratar erro do Cilium.


- OK, pods running

~~~~bash

root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# kubectl get pods -A
NAMESPACE     NAME                                  READY   STATUS    RESTARTS   AGE
kube-system   cilium-operator-788c4f69bc-qndg8      1/1     Running   0          58s
kube-system   cilium-xqtsm                          1/1     Running   0          58s
kube-system   coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system   coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system   etcd-debian10x64                      1/1     Running   1137       27d
kube-system   kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system   kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system   kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system   kube-scheduler-debian10x64            1/1     Running   25         27d
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage# date
Sat 23 Mar 2024 09:58:55 PM -03
root@debian10x64:/home/fernando/cursos/idp-devportal/backstage/deploy-ambiente/deploy-local/docker-multi-stage#

~~~~



## PENDENTE
- Subir stack do projeto PES - OpenTelemetry.