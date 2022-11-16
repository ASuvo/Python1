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
Другое решение
info = []
with open(f'data/workers.txt', 'r', encoding='UTF-8') as file:
    for line in file:
        info.append(line.split())

workers = {}
for i in range(1, len(info)):
    workers[i] = {}
for i in range(1, len(info)):
    workers[i]['Имя'] = info[i][0]
    workers[i]['Фамилия'] = info[i][1]
    workers[i]['Зарплата'] = info[i][2]
    workers[i]['Должность'] = info[i][3]
    workers[i]['Норма часов'] = info[i][4]

workers = list(workers.values())

info = []
with open(f'data/hours_of.txt', 'r', encoding='UTF-8') as file:
    for line in file:
        info.append(line.split())

for i in range(1, len(info)):
    for j in range(len(workers)):
        if info[i][1] == workers[j]['Фамилия']:
            workers[j]['Отработано_часов'] = info[i][2]


for el in workers:
    print(el)
    if int(el['Отработано_часов']) <= int(el['Норма часов']):
        koef = int(el['Отработано_часов'])/int(el['Норма часов'])
        print(f"Зарплата работника составила:{int(koef*int(el['Зарплата']))} рублей")
    else:
        salary_per_hour = int(el['Зарплата'])/int(el['Норма часов'])
        pererabotka = int(el['Отработано_часов']) - int(el['Норма часов'])
        additional_salary = pererabotka*salary_per_hour*2
        print(f"Зарплата работника составила:{int(el['Зарплата']) + additional_salary} рублей")



