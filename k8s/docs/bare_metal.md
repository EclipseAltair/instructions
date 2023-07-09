# Начало
1. Отключить swap
2. Отключить SELinux
3. Отключить firewall т.к. iptables рулит kube-proxy

# Python
- можно поставить pyenv для python

# kubespray 2-22 - k8s 1.26.5
- invenories/my_cluster/iventory.ini
  - etcd должен быть нечетное кол-во
  - calico-rr - одна из внутренних сетей k8s
- invenories/my_cluster/group_vars/k8s-cluster/k8s-claster.yml

# Структура
- Все физ серверы в KVM вируализации. Безопасность, ресурс менеджмент
- 2 ingress-controller
  - Внешний load balancer (nginx, haproxy)
  - VRRP (Virtual Router Redundancy Protocol) - сетевой протокол объединяющий маршрутизаторы. Реализации: pacemaker, keepalived
- 3 master
- RBAC?

# Сеть и диски
- NFS (Network File System) - протокол сетевого доступа на основе RPC (Remote Procedure Call - удаленный вызов процедур) - межпроцессное взаимодействие IPC (Inter-process communication)
- Ceph - сеть (min 10 Гб/с) интерфейсов хранилищ
- CSI (Container Storage Interface) - унификация интерфейсов таких как Ceph, Portworx, NetApp и т.д. в k8s, docker swarm и т.д.
  - Общается с внешними компонентами через UNIX domain sockets с помощью gRPC
- CNI (Container Networking Interface) - сетевой интерфейс и стандарт для Linux-контейнеров (Calico, Flannel)
- NAT (Network Address Translation) - передача пакетов на границах разных сетей (преобразование IPs) (надстройка над NetFilter)
  - SNAT (Source NAT) - выход запроса наружу (меняется source IP)
  - DNAT (Destination NAT) - входящие запросы (меняется destination IP)

# Хосты
- k8s не работает с файлами /etc/hosts
- k8s работает с /etc/resolve.conf но там много хостов, не удобно
- нужен dns сервер