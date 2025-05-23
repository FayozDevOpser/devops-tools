# Настройка статического IP-адреса 
1) nmcli connection modify ens160 ipv4.addresses 10.0.10.10/24 
2) nmcli connection modify ens160 ipv4.gateway 10.0.10.2 
3) nmcli connection modify ens160 ipv4.dns 10.0.10.2
4) nmcli connection modify ens160 ipv4.method manual
5) nmcli general hostname postgresql
6) systemctl restart NetworkManager

# Настройте репозиторий Postgresql 15 (OS ning uzidagi versiyani enable qilish)
1) yum module list
2) yum module enable postgresql -y
3) yum install postgresql-server

# Ннициализируете кластер базы данных
1) postgresql-setup --initdb
2) systemctl enable --now postgresql

# Переключаетесь на пользователя postgres
1) su - postgres
2) pwd
3) /var/lib/pgsql
4) cat /etc/passwd | grep postgres
5) postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash

# Команда \? используется в оболочке psql для вывода справочной информации о доступных командах и их использовании. 
postgres=# \?
# Команда \l используется в оболочке psql для вывода списка баз данных на сервере.
postgres=# \l"

# Команда create database zabbixdb; выполняется в оболочке psql и создает новую базу данных с именем zabbixdb.
postgres=# create database zabbixdb;
postgres=# \l
# Команда \connect или \c используется в оболочке psql для подключения к другой базе данных. 
postgres=# \connect zabbixdb"

# в оболочке psql для создания новой таблицы с именем table01 в базе данных zabbixdb. Таблица будет содержать два столбца: ""col01"" с типом данных ""int"" (целое число) и ""col02"" с типом данных varchar(20) (строка переменной длины до 20 символов).
zabbixdb=# create table table01 (col01 int, col02 varchar(20));
# Команда \dt используется в оболочке psql для вывода списка всех таблиц в текущей базе данных. Если вы выполните эту команду после создания таблицы table01, то она должна показать эту таблицу в списке.
zabbixdb=# \dt
# insert into table01 values (1, 'RedHat'), (2, 'Debian'); в оболочке psql, чтобы вставить данные в таблицу ""table01"" в базе данных ""zabbixdb"".
1) Эта команда вставляет две строки данных в таблицу ""table01"":
2) Значение 1 для столбца ""col01"" и строка ""RedHat"" для столбца ""col02"".
3) Значение 2 для столбца ""col01"" и строка ""Debian"" для столбца ""col02"".
4) zabbixdb=# insert into table01 values (1, 'RedHat'), (2, 'Debian');
# select * from table01 в оболочке psql будет выведено содержимое таблицы ""table01"" из базы данных ""zabbixdb"". 
zabbixdb=# select * from table01;

ss -tnlup

# изменяем параметр listen_addresses на 10.0.10.10. Это означает, что сервер PostgreSQL будет слушать только соединения на указанном IP-адресе 10.0.10.10.
nano /var/lib/pgsql/data/postgresql.conf
listen_addresses = '10.0.10.10'

systemctl restart postgresql.service

ss -tnlup

# в файле ""pg_hba.conf"" задает правило доступа для подключений к серверу PostgreSQL.
nano /var/lib/pgsql/data/pg_hba.conf
host    all             all             10.0.10.0/24            md5

host: Это тип соединения. В данном случае, это подключение по сети TCP/IP.
all: Это имя базы данных, для которой применяется это правило. Здесь указано ""all"", что означает применение правила ко всем базам данных.
all: Это имя пользователя, для которого применяется это правило. Здесь также указано ""all"", что означает применение правила ко всем пользователям.
10.0.10.0/24: Это сеть или IP-адрес, для которых разрешено подключение.
md5: Это метод аутентификации. Здесь используется метод MD5, который требует от пользователя вводить пароль при подключении."

psql 
postgres=# alter user postgres with password 'Huawei@1234' ;

systemctl restart postgresql.service

![image](https://github.com/user-attachments/assets/9d6b2f46-28d9-4ce3-8b43-a92aa25e2588)

