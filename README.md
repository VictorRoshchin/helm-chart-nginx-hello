# Helm chart nginxdemos/hello

_Данный репозитерий является тестовым заданием от **[Byndyusoft](https://byndyusoft.com/ "Сайт Byndyusoft")**_

В репозитерии представлен helm сhart для запуска в кластере k8s образа **[nginxdemos/hello](https://hub.docker.com/r/nginxdemos/hello)**.

## Инструкция запуска

0. Проверить и при необходимости переопределить переменные в файлах chart.yaml и values.yaml:
    * charts.yaml:

            name: nginxdemos-hello                  # Наименование chart-а
            version: 0.1.0                          # Версия chart-a (редактируется вручную при изменении chart-а)
            appVersion: "0.3"                       # Версия разворачиваемого приложения

    * values.yaml:

            replicaCount: 2                         # Количество pod-ов, которые будет поддерживать deployment при отключении автомасштабирования (autoscaling.enable: false)
            image.tag: ""                           # Переопределяет версию приложения
            resources:                              # Определяет запросы и лимиты по ресурсам на один pod
            autoscaling:                            # Определеят параметры автомасштабирования, по умолчанию влючено. Минимальное количество pod-ов 1, максимальное - 5, измеряемый показатель - нагрузка на ресурс цпу pod-a равная 80
            ingress:                                # Определяет параметры точки входа в кластер. По умолчанию включено
            ingress.hosts.host: hello-world.info    # Хост точки входа в кластер, по умолчанию hello-world.info для кластера minikube*.

        \* - [Подключение ingress в minikube](https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/) 


1. Создание релиза helm chart:

        helm install nginxdemos-hello nginxdemos-hello

2. Для обновление релиза

        helm upgrade nginxdemos-hello nginxdemos-hello

3. Для отката релиза

        helm rollback nginxdemos-hello [REVISION]   # REVISION - номер релиза до которого необходимо откатиться

4. Для проверки соединения

        helm test nginxdemos-hello

* Просмотр списка chart-ов

        helm ls

* Проверка статуса chart-а nginxdemos-hello

        helm status nginxdemos-hello

* Удаление chart-а

        helm uninstall nginxdemos-hello
