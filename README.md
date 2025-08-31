# Заметки о работе с Minikube

[Настройка Container Registry](container-registry/README.md)
[Установка Minikube](install/README.md)


Полезные Юзкейсы:
- Билд кастомного образа под свои задачи
  minikube image build -t <новый тег образа> <путь к Dockerfile>

- Проверить статус работы миникуба:
  minikube status

- Вывести информацию о всех подах:
  kubectl get pods -A

- Вывести информацию о подах конкретного namespace:
  kubectl get pods -n <название namespace>

- Вывести логи пода
  kubectl logs -n <название области> pod/<имя пода>

- Удалить под. После удаления пода он будет автоматически создан в актуальном состоянии
  kubectl delete pod <имя пода> -n logging

