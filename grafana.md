# Домашнее задание «Средство визуализации Grafana»

1. Развертывание системы с помощью docker compose  

![image](https://github.com/user-attachments/assets/0ef6daca-fde5-4ff2-a22c-098404d6aa34)  


2–3. Dashboard c panels и alerts  
![image](https://github.com/user-attachments/assets/6b7eac9c-4d35-4e5f-8d88-374310e3949e)  
![image](https://github.com/user-attachments/assets/85887b77-d020-44d5-9cc8-92d3ec01e526)


### Утилизация CPU для nodeexporter (в процентах, 100-idle):
**Решение:**
- формула получения метрики:  
  `100 - avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100`
- alert:  
  `WHEN avg() of query(A,5m, now) is above 90`
![image](https://github.com/user-attachments/assets/60b38193-82d7-4aa8-9e51-a3718524a90b)
![image](https://github.com/user-attachments/assets/2722a022-90f2-4d3e-9beb-e185487807df)


---

### CPULA 1/5/15:
**Решение:**
- формула получения метрики:  
  `node_load1`, `node_load5`, `node_load15`   (указываются раздельно, в каждом query)
- alert:  
  `WHEN avg() of query(A,5m, now) is above 4`
![image](https://github.com/user-attachments/assets/1564e309-6380-4e24-b7ad-cf3742072e83)

![image](https://github.com/user-attachments/assets/fbd722ac-8b8d-4ec4-9141-d6b43b4007ac)

---

### Количество свободной оперативной памяти:
**Решение:**
- формула получения метрики:  
  `node_memory_MemFree_bytes / node_memory_MemTotal_bytes * 100`
- alert:  
  `WHEN last() of query(A,5m, now) is below 10`
![image](https://github.com/user-attachments/assets/98b8441b-ba43-482e-ae95-3b3596ab286a)  
![image](https://github.com/user-attachments/assets/66fe3305-6ac5-4885-9551-784e1b0b27ac)  

---

### Количество места на файловой системе:
**Решение:**
- формула получения метрики:  
  `node_filesystem_avail_bytes{fstype="ext4", mountpoint="/"} / node_filesystem_size_bytes{fstype="ext4", mountpoint="/"} * 1000`
- alert:  
  `WHEN avg() of query(A,5m, now) is below 10`

![image](https://github.com/user-attachments/assets/f72bcc04-8ea0-48cb-8796-b9a10c5f9696)  
![image](https://github.com/user-attachments/assets/9a41d5a4-27d6-499d-a2be-10e6b748bc9b)  


  
