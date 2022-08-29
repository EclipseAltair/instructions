# RBAC
- Нет пользователей, только роли

## Role
- Список прав на объект

## RoleBinding
- Связывает Role и ServiceAccount
- Ограничен namespace`ом. Нужно выдавать для каждого namespace

## ClusterRole
Базовые роли
- view -  позволяет посмотреть все в namespace
- edit - позволяет отредактировать
- admin - позволяет посмотреть объект secret
- cluster-admin - можно делать все что угодно

## ClusterRoleBinding
- Тоже самое на уровне кластера

## ServiceAccount
- Общается с API server через JWT token и авторизуется через Bearer Authorization
- Автоматически создается в namespace serviceaccount с именем default и токеном. По умолчанию может посмотреть только на свой под

# PodSecurityPolicy (deprecated)
- Запретить запускать подам с небезопасными механизмым (например: hostPath)
- Контролирует аспекты безопасности в описании подов
- Включается как admission controller plugin
  - При включении запрещает запуск подов без PSP