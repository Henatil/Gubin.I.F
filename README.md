# Gubin
Устанавливаем Linux Oracle на VirtualBox

Ообраз Linux При установки операционной системы, желательно выбераем английский язык (В будущем будет легче решать ошибки).
Далее переходим к установке docker с использованием terminal, вводим следующий набор команд:

1. `sudo yum install wget`

• Выдает ошибку `is not in the sudoers file`

![image](https://github.com/user-attachments/assets/2ac1c34b-c488-4348-b4e3-3c2d0e7510fa)

Данную ошибку решаем через коректировку конфигурационного файла /etc/sudoers

vi /etc/sudoers

![image](https://github.com/user-attachments/assets/726e7317-ec25-48bf-9a6a-f825ec01c1b2)

![image](https://github.com/user-attachments/assets/12d35f06-f51f-4df3-baa1-1f1722c94790)

После решения проблемы прописываем `sudo yum install wget`

• Для установки улиты wget (wget=это утилита командной строки для загрузки файлов из интернета.)

![image](https://github.com/user-attachments/assets/00342289-0516-4526-badd-079013edec20)

2. Устанавливаем `sudo yum install curl` 

![image](https://github.com/user-attachments/assets/29fba53b-e0fa-4496-b027-f99d85829be6)

2.1 `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

• Скачиваем файл репозитория

![image](https://github.com/user-attachments/assets/3d9a7925-aeed-4050-890e-3abfd1fef2fb)

3. `sudo yum install docker-ce docker-ce-cli containerd.io`

• Устанавливаем docker

![image](https://github.com/user-attachments/assets/1876c9f2-89fa-4f65-9707-1b4aee9464de)

4. `sudo systemctl enable docker --now`

• Запускаем его и разрешаем автозапуск

![image](https://github.com/user-attachments/assets/40257b44-f7b1-49be-bb45-50ee3ca24671)

5. `sudo yum install curl`

• Для этого сначала убедимся в наличие пакета curl

6. `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней
версии Docker Compose
![image](https://github.com/user-attachments/assets/1a319c45-0467-4354-80ae-8adb82d8ad57)

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`                        

• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

![image](https://github.com/user-attachments/assets/6f4a7ffc-ff0c-4155-a082-07d7d0efc5e5)

8. `sudo chmod +x /usr/bin/docker-compose`

• Предоставление прав на выполнение файла docker-compose.

9. `docker-compose --version`

• Проверка установленной версии Docker Compose.

![image](https://github.com/user-attachments/assets/5a7024a8-b070-489c-a21b-1799118f110a)

• Можно скачать git прямо из командной строки прописав Y

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

• выдаст ошибку и предложит скачать git, согласиться и продолжить
![image](https://github.com/user-attachments/assets/b469b556-d8b7-467c-a1d9-125487dcafd8)

11. `cd grafana_stack_for_docker`
    
• переход в папку

12.`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

13. `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

14. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

15.` touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

16. `cp config/* /mnt/common_volume/swarm/grafana/config/`

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

17. `mv grafana.yaml docker-compose.yaml `

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

18.` sudo docker compose up -d`

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.
![image](https://github.com/user-attachments/assets/a58b0533-185d-49d2-b5ae-f48ce5ec261f)

![image](https://github.com/user-attachments/assets/929f2f13-f8e2-4a24-8bef-a423f785b144)

5. `sudo docker compose stop`
![image](https://github.com/user-attachments/assets/e228f373-5aed-4965-8233-f95ba450c509)

6. `sudo docker compose down`
![image](https://github.com/user-attachments/assets/e92cd705-87a7-465e-90a3-18a4277e8ecd)

7. `sudo docker compose ps`
![image](https://github.com/user-attachments/assets/542f9f2a-59b7-446f-8ca8-16137f59e9ac)

8. `git clone [https://github.com/Henatil/Gubin.I.F.git]`

Командой выполняем клонирование удаленного Git-репозитория с GitHub на компьютер
![image](https://github.com/user-attachments/assets/abb749e9-103d-4139-9520-f79806e39b9a)





