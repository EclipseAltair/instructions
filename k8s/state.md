# State
Good state - dead state (stateless)

Если приложение хранит state, то pod становится уникальным и не переподнимется при падении.
Лучше хранить в БД, S3, Redis, Memcached и т.д.

## Если нужно хранить state:
### HostPath
`pod: hostPath(/etc/kubernetes)`

Не безопасно. Если есть доступ к hostPath, то есть доступ к админским правам

### EmptyDir
`pod: временный диск`

При удалении пода, данные удалятся. Нужен для тестов (данные, которые не нужно хранить)

### PV / PVC (PersistentVolume / PersistentVolumeClaim)

- Storage class: хранит параметры подключения (где хранятся данные: hdd, облако и т.д.)
- PersistentVolume: хранит параметры и статус тома (какой диск выдан: адрес диска)
- PersistentVolumeClaim: описываает требования к тому (заявка какой диск нужен)

SC -> PVC 50 gb -> PV 50gb+ (займет полностью даже если больше) 

PV Provisioners: создает PVC нужного размера под PVC 
cli -> api -> provisioner -> storage provider
