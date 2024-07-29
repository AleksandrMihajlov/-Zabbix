Система мониторинга Zabbix - Aleksandr Mihajlov SYS34  
**Задание1**    

*Обновляем репозитории и устанавливаем postgresql*  
sudo apt update  
sudo apt install postgresql  
*Скачиваем, распаковываем и обновляем репозиторий.*  
sudo wget https://repo.zabbix.com/zabbix/7.0/debian-arm64/pool/main/z/zabbix-release/zabbix-release_7.0-2+debian12_all.deb  
sudo dpkg -i zabbix-release_7.0-2+debian12_all.deb  
sudo apt update  
*Устанавливаем сервер*  
sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent  
*Создаем пользователя, пароль, базу*    
sudo -u postgres createuser --pwprompt zabbix  
sudo -u postgres createdb -O zabbix zabbix  
*Импортируем данные* 
sudo zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix  
*Вводим созданный пароль в файле*  
/etc/zabbix/zabbix_server.conf  
в графе DBPassword=password  
*Перезагружаем сервис и устанавливаем автозапуск*  
systemctl restart zabbix-server zabbix-agent apache2  
systemctl enable zabbix-server zabbix-agent apache2  
*Устанавливаем веб сервер*   
sudo apt install zabbix-web-service  
*Перезагружаем сервис и устанавливаем автозапуск*  
sudo systemctl restart zabbix-web-service  
sudo systemctl enable zabbix-web-service  
![alt text](https://github.com/AleksandrMihajlov/Zabbix-hw-02/blob/main/1.png)  
![alt text](https://github.com/AleksandrMihajlov/Zabbix-hw-02/blob/main/1.1.png)  
  
**Задание2**