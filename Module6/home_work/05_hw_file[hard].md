## "Обработка списка фруктов"

### Задание

Дана ведомость расчета заработной платы [data/workers.txt](data/workers.txt).

Рассчитайте зарплату всех работников, зная что они получат полный оклад, если отработают норму часов. \
Если же они отработали меньше нормы, то их ЗП уменьшается пропорционально, \
а за каждый час переработки они получают удвоенную ЗП, пропорциональную норме. \
Кол-во часов, которые были отработаны, указаны в файле ["data/hours_of.txt](data/hours_of.txt)

### Формат входных данных

Дано два текстовых файла. Один с информацией о сотрудниках, второй с количеством отработанных часов.

Гарантируется, что каждый сотрудник имеет уникальную фамилию(однофамильцев нет).

### Формат выходных данных

Выведите зарплату сотрудников с учетом переработки и недоработки.

### Решение задачи

```python
path_w = "workers.txt" 
path_h = "hours_of.txt" 

worker = {}
hour = {}
i=0

with open(path_w, "r", encoding="UTF-8") as w:
    for line in w:
      worker[i]=line.split()
      i+=1
i=0
with open(path_h, "r", encoding="UTF-8") as h:
    for line in h:
      hour[i]=line.split()
      for key, value in worker.items():
        if value[1]==hour[i][1]:
          value.append(hour[i][2])
          if i!=0:
            value[2]=int(value[2])
            value[4]=int(value[4])
            value[5]=int(value[5])
      i+=1

for key, value in worker.items():
  if key==0:
    value.append('Начисленная зарплата')
  if key!=0:
    zp_ch=value[2]/value[4]
    if value[5]<=value[4]:
      zar=zp_ch*value[5]
    else:
      zar=zp_ch*(value[4]+2*(value[5]-value[4]))
    value.append(int(zar))

for key, value in worker.items():
  l1=10-len(value[0])
  l2=10-len(value[1])
  print (value[0]," "*l1, value[1]," "*l2, value[6] )
```

---
