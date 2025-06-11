# 🛠️ Ansible Project Manual

Этот проект демонстрирует базовое управление удалённым сервером с помощью Ansible, эмулированным через Docker-контейнер с SSH-доступом.

## 📦 Состав проекта

- `Dockerfile` — Ubuntu 20.04 с установленным SSH-сервером, sudo, nano, htop
- `docker-compose.yml` — для запуска контейнера с пробросом порта 2222
- `ansible/inventory.ini` — настройка Ansible для подключения по SSH
- `ansible/manual_steps.txt` — список команд Ansible для выполнения вручную

---

## 🚀 Запуск проекта

1. Распакуй архив:

```bash
unzip ansible_project_manual.zip
cd ansible_project_manual
```

2. Построй образ и запусти контейнер:

```bash
docker compose build --no-cache
docker compose up -d
```

---

## 🔐 Подключение по SSH

```bash
ssh ansible@127.0.0.1 -p 2222
# Пароль: ansible
```

---

## ⚙️ Примеры Ansible-команд

Перейди в каталог с Ansible:

```bash
cd ansible
```

🔹 Пинг:

```bash
ansible remote -i inventory.ini -m ping
```

🔹 Создать файл:

```bash
ansible remote -i inventory.ini -m copy -a "content='Привет от Ansible\n' dest=/home/ansible/hello.txt" -b
```

🔹 Изменить файл:

```bash
ansible remote -i inventory.ini -m lineinfile -a "path=/home/ansible/hello.txt line='Файл изменён Ansible'" -b
```

🔹 Удалить файл:

```bash
ansible remote -i inventory.ini -m file -a "path=/home/ansible/delete_me.txt state=absent" -b
```

🔹 Установить пакет:

```bash
ansible remote -i inventory.ini -m apt -a "name=nano state=present update_cache=yes" -b
```

---

## 🔍 Проверка результатов

📌 Внутри контейнера по SSH:

```bash
ssh ansible@127.0.0.1 -p 2222
ls /home/ansible
cat /home/ansible/hello.txt
nano --version
```

📌 Или через Docker напрямую:

```bash
docker exec -it ansible_target bash
ls /home/ansible
```

---

## 💡 Полезно знать

- Контейнер использует имя `ansible_target`
- Порт 2222 проброшен на порт 22 контейнера
- Пользователь `ansible` имеет `sudo` без пароля
- Всё тестируется как будто на настоящем удалённом сервере

---

## 📤 Публикация в Git

```bash
git init
git remote add origin https://github.com/your_username/ansible_project_manual.git
git add .
git commit -m "Ansible + Docker + SSH test project"
git push -u origin master
```

---


