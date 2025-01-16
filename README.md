# Домашнее задание к занятию 3 «Резервное копирование»

### Задание 1
- Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию `/tmp/backup`
- Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
- Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
- На проверку направить скриншот с командой и результатом ее выполнения

# Решение
rsync -avh --delete --checksum --exclude='.*/' /home/igorek /tmp/backup
![image](https://github.com/user-attachments/assets/f714a9d6-e185-4bdf-aa91-9132b3ad7b3f)
![image](https://github.com/user-attachments/assets/108a0920-48e7-4892-a5ad-94de56e7d56c)

### Задание 2
- Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
- Резервная копия должна быть полностью зеркальной
- Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
- Резервная копия размещается локально, в директории `/tmp/backup`
- На проверку направить файл crontab и скриншот с результатом работы утилиты.

# Решение
#### Скрипт
```
#!/bin/bash
mkdir -p /tmp/backup1
rsync -avh --delete --checksum  /home/igorek /tmp/backup1 > /tmp/backup1/backup_sys_old.log
if [ $? -eq 0 ]; then
        echo "$(date) - Резервное копирование выполнено успешно" >> /var/log/backup_sys.log
else
        echo "$(date) - Резервное копирование не выполнено" >> /var/log/backup_sys.log
fi
```

#### Файл crontab
- резервное копирование каждый день в 2 часа ночи

![image](https://github.com/user-attachments/assets/d9d93da9-3ab4-48fd-a9a5-6d67f5fdc1b1)
![image](https://github.com/user-attachments/assets/0124a2b1-8c9f-40cc-a529-70628beaaf2e)
![image](https://github.com/user-attachments/assets/e38bf2f0-b67a-45aa-bfb9-9cf6c65975ee)
![image](https://github.com/user-attachments/assets/dee01404-f9b3-413a-b32a-85d7b42af706)



