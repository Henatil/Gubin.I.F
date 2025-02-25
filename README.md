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
![image](https://github.com/user-attachments/assets/2e951858-540c-4848-a278-a1990a2fa29e)

7. `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`                        

• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin

![image](https://github.com/user-attachments/assets/79588f34-614e-47ea-ad35-3031981127ba)

8. `sudo chmod +x /usr/bin/docker-compose`

• Предоставление прав на выполнение файла docker-compose.

9. `docker-compose --version`

• Проверка установленной версии Docker Compose.

![image](https://github.com/user-attachments/assets/5b020289-6738-4b35-a781-198bfa8bfa6c)

• Можно скачать git прямо из командной строки прописав Y

10. `git clone https://github.com/skl256/grafana_stack_for_docker.git`

• выдаст ошибку и предложит скачать git, согласиться и продолжить
![image](https://github.com/user-attachments/assets/3c397f5e-483d-428f-8b14-e0c6e2e0b91b)

11. `cd grafana_stack_for_docker`
    
• переход в папку

12.`sudo mkdir -p /mnt/common_volume/swarm/grafana/config`

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

13. `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}`

• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

14. `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}`

• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе
![image](https://github.com/user-attachments/assets/197172d2-bdd5-43aa-ab62-601a03941f88)

15.` touch /mnt/common_volume/grafana/grafana-config/grafana.ini`

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

16. `cp config/* /mnt/common_volume/swarm/grafana/config/`

• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

17. `mv grafana.yaml docker-compose.yaml `

• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls
![image](https://github.com/user-attachments/assets/2412d6dd-7516-4989-94fa-1b42f53a5db8)

18.` sudo docker compose up -d`

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.

![image](https://github.com/user-attachments/assets/946f1974-f27e-40e0-a4ca-9c430c4b7040)

19.` sudo vi docker-compose.yaml`

•команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.

• Нас перекинет в текстовый редактор

• Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре

• Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services

![image](https://github.com/user-attachments/assets/269213a9-6e34-4687-8d85-2d4b0c4aa453)

20. `sudo docker compose stop`

•Останавливает все запущенные контейнеры, но не удаляет их.
•Контейнеры остаются в состоянии "остановленных".

![image](https://github.com/user-attachments/assets/e228f373-5aed-4965-8233-f95ba450c509)

21. `sudo docker compose down`

•Полностью останавливает и удаляет все контейнеры, сети.
•Эта команда является более радикальной по сравнению с командой stop. После её выполнения все данные, находящиеся в хранилищах, будут уничтожены, если не будет указано иное для их сохранения.

![image](https://github.com/user-attachments/assets/e92cd705-87a7-465e-90a3-18a4277e8ecd)

22. `sudo docker compose ps`

•Отображает статус всех контейнеров, указанных в файле. Данная команда предоставляет список контейнеров с информацией об их состоянии (активен/неактивен), портах, сетях и другими характеристиками.

![image](https://github.com/user-attachments/assets/542f9f2a-59b7-446f-8ca8-16137f59e9ac)

23. `git clone [https://github.com/Henatil/Gubin.I.F.git]`

•Команда осуществляет клонирование удаленного Git-репозитория с GitHub в указанную директорию.

![image](https://github.com/user-attachments/assets/abb749e9-103d-4139-9520-f79806e39b9a)

24. `pwd`

•Показывает путь

![image](https://github.com/user-attachments/assets/ad9bc814-0a2a-43b8-9205-8b5e6cc8422e)






