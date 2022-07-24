# Устройство кластера. Компоненты k8s

## kubectl
- Команды для пользователя
- Общается с API server 

## Etcd
Хранит в ключ-значение. База данных kubernetes. Все хранится в ней

### RAFT
Протокол с которым работает etcd
- Обычно 3 или 5 нод и на каждой свой etcd

## API server
- Центральный компонент k8s
- Единственный кто общается с etcd
- Все общаются с ним для получения информации
- Работает по REST API
- Другие компоненты watch`ат его с помощью HTTP/2 long polling

## Controller-manager
- Не создает поды, только передает информацию в etcd
- Общается с API server 
- Может быть 1 и более. Одновременно работает только 1.

Набор контроллеров:
- Node controller
  - контролирует, что нода пишет о себе информацию, что она жива. Запускает перенос на другие ноды в случае проблемы
- Replicaset controller
  - Смотрит в API server и на основании информации создает replicaset 
- Endpoints controller
  - Для каждого сервиса автоматически создает эндпоинты

GarbageCollector:
  - Удаляет старые поды/репликасеты/... 

## Scheduler
- Не создает поды
- Общается с API server 
- Назначет поды на ноды
- Может быть 1 и более. Одновременно работает только 1.

Механизмы фильтрации и скоринга:
- QoS (Quality of Service) политика
  - В зависимости от ресурсов и лимитов он определит куда назначить поды.
- Affinity / anti-affinity
  - Определяет назначение
- Requested resources
  - Выбирает приоритет по ресурсам
- Priority Class
  - Выбирает приоритет

## kubelet
- Общается с API server и передает информацию о ноде
- Работает на каждой ноде
- Единственный компонент работяющий не в докере, а как процесс на хосте
- Отдает команды docker daemon 
- Создает поды
- Делает проверки probe. Делает проверку по localhost внутри одной ноды.

## kube-proxy
- Общается с API server 
- Стоит на все нодах
- Управляет сетевыми правилами на нодах
- Фактически реализует Service (ipvs и iptables)

## Баги
- Есть deploy, но нет pods - сломался controller manager
- Вечный pending - сломался Scheduler