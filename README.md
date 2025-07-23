# Проект: Kubernetes-манифесты для приложений и сервисов

## Описание

В этом репозитории собраны манифесты для развертывания различных приложений и инфраструктурных сервисов в Kubernetes-кластере. Основное внимание уделено демонстрационным приложениям, мониторингу, очередям сообщений и базам данных.

## Структура

- `kube-config/` — директория с Kubernetes-манифестами:
  - `*-dep.yml` — Deployment для приложений и сервисов
  - `*-svc.yml` — Service (ClusterIP, NodePort и др.)
  - `*-pvc.yml` — PersistentVolumeClaim для хранения данных
  - `*-ingress.yml` — Ingress для маршрутизации HTTP-трафика

## Основные компоненты

- **conv-app** — пример приложения с балансировкой и ingress
- **postgres** — база данных с PVC для хранения данных
- **rmq (RabbitMQ)** — очередь сообщений с management-плагином и персистентным хранилищем


## Быстрый старт

1. Примените необходимые PVC:
   ```sh
   kubectl apply -f kube-config/postgres-pvc.yml
   kubectl apply -f kube-config/rmq-pvc.yml
   # ... другие PVC при необходимости
   ```

2. Разверните сервисы и приложения:
   ```sh
   kubectl apply -f kube-config/postgres-dep.yml
   kubectl apply -f kube-config/postgres-svc.yml
   kubectl apply -f kube-config/rmq-dep.yml
   kubectl apply -f kube-config/rmq-svc.yml
   kubectl apply -f kube-config/conv-app.yml
   kubectl apply -f kube-config/cluster-ip.yml
   kubectl apply -f kube-config/ingress.yml
   # ... другие манифесты по необходимости
   ```

3. Проверьте статус:
   ```sh
   kubectl get pods
   kubectl get svc
   kubectl get ingress
   ```

## Важно
- Для работы ingress необходим установленный ingress-контроллер (например, nginx-ingress).
- Все пароли и логины заданы для демонстрационных целей, не используйте их в продакшене.
- Для RabbitMQ используется образ с management-плагином (`rabbitmq:3.12.7-management`).

## Документация
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [RabbitMQ Docker Hub](https://hub.docker.com/_/rabbitmq)
- [PostgreSQL Docker Hub](https://hub.docker.com/_/postgres)


