# Начало
2. Отключить swap
2. Отключить SELinux?
3. Отключить firewall

# Python
- можно поставить pyenv для python

# kubespray 2-22 - k8s 1.26.5
- invenories/my_cluster/iventory.ini
  - etcd должен быть нечетное кол-во
  - calico-rr - одна из внутренних сетей k8s
- invenories/my_cluster/group_vars/k8s-cluster/k8s-claster.yml


# Сеть и диски
- NFS (Network File System) - протокол сетевого доступа на основе RPC (Remote Procedure Call - удаленный вызов процедур) - межпроцессное взаимодействие IPC (Inter-process communication)
- Ceph - сеть (min 10 Гб/с) интерфейсов хранилищ
- CSI (Container Storage Interface) - унификация интерфейсов таких как Ceph, Portworx, NetApp и т.д. в k8s, docker swarm и т.д.
  - Общается с внешними компонентами через UNIX domain sockets с помощью gRPC

# Хосты
- k8s не работает с файлами /etc/hosts
- k8s работает с /etc/resolve.conf но там много хостов, не удобно
- нужен dns сервер