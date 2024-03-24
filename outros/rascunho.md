


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




- Subir stack do projeto PES - OpenTelemetry.

- ERRO

~~~~bash
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl apply -f 01-backend.yaml
namespace/observability-backend created
secret/loki-config created
service/loki created
statefulset.apps/loki created
configmap/tempo created
error: error validating "01-backend.yaml": error validating data: ValidationError(Service): unknown field "data" in io.k8s.api.core.v1.Service; if you choose to ignore these errors, turn validation off with --validate=false
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry#
~~~~



- Ajustado

aplicando

~~~~bash

root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry# kubectl apply -f 01-backend.yaml
namespace/observability-backend unchanged
secret/loki-config unchanged
service/loki unchanged
statefulset.apps/loki configured
configmap/tempo configured
service/tempo created
deployment.apps/tempo created
configmap/mimir created
service/mimir created
statefulset.apps/mimir created
configmap/dashboards-demo-0 created
configmap/grafana-config created
configmap/grafana-dashboard-provisioning created
configmap/grafana-dashboards created
configmap/grafana-dashboards-demo created
configmap/grafana-datasources created
configmap/grafana-notification-channels created
service/grafana created
deployment.apps/grafana created
root@debian10x64:/home/fernando/cursos/opentelemetry/pes-2023-opentelemetry#

~~~~




- Abra uma conexão com o serviço do Grafana em uma outra sessão do terminal: 

````bash
kubectl port-forward -n observability-backend svc/grafana 3000:3000
````


root@debian10x64:/home/fernando# kubectl port-forward -n observability-backend svc/grafana 3000:3000
error: unable to forward port because pod is not running. Current status=Pending
root@debian10x64:/home/fernando# kubectl get pods -A
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   0          9m13s
kube-system             cilium-xqtsm                          1/1     Running   0          9m13s
kube-system             coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system             etcd-debian10x64                      1/1     Running   1137       27d
kube-system             kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system             kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system             kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system             kube-scheduler-debian10x64            1/1     Running   25         27d
observability-backend   grafana-65888b98d-w664v               0/1     Pending   0          2m48s
observability-backend   loki-0                                0/1     Pending   0          5m46s
observability-backend   mimir-0                               0/1     Pending   0          2m48s
observability-backend   tempo-694776547f-t5m5h                0/1     Pending   0          2m48s


Events:
  Type     Reason            Age    From               Message
  ----     ------            ----   ----               -------
  Warning  FailedScheduling  3m18s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando# kubectl get nodes
NAME          STATUS   ROLES           AGE   VERSION
debian10x64   Ready    control-plane   27d   v1.28.1
root@debian10x64:/home/fernando#











##  ChatGPT 3.5
 
User
como resolver o problema do pod com erro "Warning  FailedScheduling  3m18s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node-role.kubernetes.io/control-plane: }. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.."?
ChatGPT

Esse aviso indica que o Kubernetes não conseguiu agendar um pod porque não há nós disponíveis que possam tolerar as condições especificadas no pod. No seu caso, parece que o único nó disponível tem uma taint que não é tolerada pelo pod.

Você pode resolver esse problema de várias maneiras:

    Remova a taint do nó: Se o nó com a taint não é crítico para executar apenas componentes do plano de controle, você pode remover a taint para tornar o nó disponível para outros pods. Você pode fazer isso executando o seguinte comando:

    bash

kubectl taint nodes <nome_do_nó> node-role.kubernetes.io/control-plane:NoSchedule-

Substitua <nome_do_nó> pelo nome do nó que possui a taint que você deseja remover.

Adicione tolerâncias ao seu pod: Se não for possível ou desejável remover a taint do nó, você pode adicionar tolerâncias ao seu pod para permitir que ele seja agendado em nós com taints específicas. Você pode fazer isso adicionando a seguinte seção ao manifesto do seu pod:

yaml

tolerations:
- key: "node-role.kubernetes.io/control-plane"
  operator: "Exists"
  effect: "NoSchedule"

Isso permite que o pod seja agendado em nós com a taint node-role.kubernetes.io/control-plane.






- ANTES


root@debian10x64:/home/fernando# kubectl describe node debian10x64
Name:               debian10x64
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=debian10x64
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: unix:///var/run/crio/crio.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 25 Feb 2024 13:23:34 -0300
Taints:             node-role.kubernetes.io/control-plane:NoSchedule
Unschedulable:      false



- Ajuste


kubectl taint nodes <nome_do_nó> node-role.kubernetes.io/control-plane:NoSchedule-
kubectl taint nodes debian10x64 node-role.kubernetes.io/control-plane:NoSchedule-


root@debian10x64:/home/fernando# kubectl taint nodes debian10x64 node-role.kubernetes.io/control-plane:NoSchedule-
node/debian10x64 untainted
root@debian10x64:/home/fernando# DATE
bash: DATE: command not found
root@debian10x64:/home/fernando# date
Sat 23 Mar 2024 10:18:24 PM -03
root@debian10x64:/home/fernando#



- DEPOIS

root@debian10x64:/home/fernando# kubectl describe node debian10x64
Name:               debian10x64
Roles:              control-plane
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=debian10x64
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: unix:///var/run/crio/crio.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 25 Feb 2024 13:23:34 -0300
Taints:             <none>
Unschedulable:      false






- OK, Pod do Grafana subiu.

- Porém tem pods em pending:

~~~~bash

root@debian10x64:/home/fernando# kubectl get pods -A -w
NAMESPACE               NAME                                  READY   STATUS    RESTARTS   AGE
kube-system             cilium-operator-788c4f69bc-qndg8      1/1     Running   0          22m
kube-system             cilium-xqtsm                          1/1     Running   0          22m
kube-system             coredns-5dd5756b68-7vdkb              1/1     Running   0          27d
kube-system             coredns-5dd5756b68-84rbg              1/1     Running   0          27d
kube-system             etcd-debian10x64                      1/1     Running   1137       27d
kube-system             kube-apiserver-debian10x64            1/1     Running   23         27d
kube-system             kube-controller-manager-debian10x64   1/1     Running   24         27d
kube-system             kube-proxy-kx4h5                      1/1     Running   23         27d
kube-system             kube-scheduler-debian10x64            1/1     Running   25         27d
observability-backend   grafana-65888b98d-w664v               1/1     Running   0          15m
observability-backend   loki-0                                0/1     Pending   0          18m
observability-backend   mimir-0                               0/1     Pending   0          15m
observability-backend   tempo-694776547f-t5m5h                1/1     Running   0          15m


^Croot@debian10x64:/home/fernando# kubectl describe pod loki-0 -n observability-backend
Name:           loki-0
Namespace:      observability-backend

Events:
  Type     Reason            Age                From               Message
  ----     ------            ----               ----               -------
  Warning  FailedScheduling  18m                default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
  Warning  FailedScheduling  10m (x2 over 15m)  default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
root@debian10x64:/home/fernando#

~~~~




## PENDENTE
- TSHOOT, pods do Loki, Mimir.
            default-scheduler  0/1 nodes are available: pod has unbound immediate PersistentVolumeClaims. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling..
- Subir stack do projeto PES - OpenTelemetry.