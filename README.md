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
