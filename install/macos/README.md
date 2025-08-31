Install on MacOS

🧰 Шаг 1: Установи Docker Desktop

Скачай и установи Docker Desktop для Apple Silicon (M1/M2):

👉 https://www.docker.com/products/docker-desktop/

После установки — запусти Docker Desktop, дождись, пока значок станет зелёным ✅.

📦 Шаг 2: Установи Minikube и kubectl
brew install minikube
brew install kubectl


Проверь версии:

minikube version
kubectl version --client

🚀 Шаг 3: Запусти Minikube с драйвером Docker
minikube start --driver=docker


⚙️ Minikube создаст виртуальный кластер в контейнере.

🔍 Шаг 4: Проверка работы
kubectl get nodes


Должен быть виден один node в статусе Ready.

🧼 (Опционально) Остановить кластер
minikube stop


Удалить:

minikube delete

💡 Советы

Для экономии ресурсов можно указать CPU/память:

minikube start --driver=docker --cpus=2 --memory=4096


Для удобства можно экспортировать Docker env:

eval $(minikube docker-env)


Это позволяет собирать образы локально и использовать в кластере, не пуша в Docker Hub или GHCR.