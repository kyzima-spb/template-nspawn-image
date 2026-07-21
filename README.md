# Шаблон для создания образов systemd-nspawn

## Установка mkosi

Лучше выполнять установку в виртуальное окружение Python, можно указать версию или установить самую свежую:

```
cd my-project
python3 -m venv env
./env/bin/pip install git+https://github.com/systemd/mkosi.git@v26
```

## Команды

В старых хостовых системах могут быть ошибки с правами доступа.
Чтобы их избежать выполняйте команды от суперпользователя (`sudo`):

Сборка образа для распространения:

```
cd my-project
sudo -E ./env/bin/mkosi -C ./image build --incremental yes --force
```

Сборка образа для разработки и запуск контейнера с имененм `my-container`:

```
cd my-project
sudo -E ./env/bin/mkosi -C ./image --format directory build --incremental yes --force
sudo -E ./env/bin/mkosi -C ./image --format directory boot --machine my-container
```

Сборка образа для разработки с указанием профиля/профилей:

```
cd my-project
sudo -E ./env/bin/mkosi -C ./image --format directory --profile nginx build --incremental yes --force
sudo -E ./env/bin/mkosi -C ./image --format directory --profile nginx boot my-container
```

Затем в другом терминале входим в контейнер:

```
sudo machinectl shell my-container
```

Для остановки запущенного контейнера:

```
sudo machinectl stop my-container
```
