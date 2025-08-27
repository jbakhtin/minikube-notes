# Настраиваем GitHub Container Registry

Миникуб работает только с Docker образами. Образы могут располагаться локально или в Container Registry, например
GitHub CR или Docker Hub.

## Что бы сделать образ в GitHub CR, нужно:
1. Аккаунт на GitHub
2. Репозиторий на GitHub для вашего проекта, который вы хотите хранить в GitHub CR
3. Dockerfile в вашем проекте для сборки образа

Далее идем по шагам:

**Шаг 1. Создаем Personal Access Token (PAT)**
1. Перейди на GitHub: https://github.com/settings/tokens
2. Нажми "Generate new token (classic)"
3. Выбери scope:
    - write:packages
    - read:packages
    - delete:packages (по желанию)
    - repo (если приватный репозиторий)
4. Сохрани токен!

**Шаг 2. Настраиваем секреты**
1. Перейди в свой репозиторий → Settings → Secrets and variables → Actions → New repository secret
2. Создай:
    - GH_USERNAME	Твой GitHub логин (например, jbakhtin)
    - CR_PAT	Тот самый токен из Шага 4

**Шаг 3. Добавить GitHub Actions для автоматического обновления GitHub CR**
1. Создай файл `.github/workflows/docker-publish.yml`:

```YML
name: Build and Push to GHCR

on:
push:
branches:
- main

jobs:
push-to-ghcr:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Login to GitHub Container Registry
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ secrets.GH_USERNAME }}
          password: ${{ secrets.CR_PAT }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ghcr.io/${{ github.repository }}:latest
```