# Debug

## Три главные команды
1. k describe ...
   - можно посмотреть статус
      - terminationreason 
        - omkilled - кончилась оперативная память
        - error - нужна следующая команда
2. k get events
   - события в подах (по умолчанию хранятся 1 час)
3. k logs <pod_name> --previous
   - логи предыдущего пода, если его перезапустил k8s

## Сделать очевиднее
kind: Deployment - container: terminationMessagePolicy: 
   - File (по умолчанию)
   - FallbackToLogsOnError - если приложение было перезапущено из-за самого приложения в логи будет добавлено 80 строк или 2Кб логов

## Профилировщики / дебагеры
- Могут работать по сети, без входа в контейнер
- Python:
  - Prometheus
  - Rookout