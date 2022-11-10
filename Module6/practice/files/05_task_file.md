## "Улучшенный кассовый аппарат"

### Задание
Кассовый аппарат был доработан, теперь он пишет не только цены, но и тип проданных товаров. \
Файл [data/items_sold.txt](data/items_sold.txt) - продажи всех товаров за день. \
Каждая строка файла - покупка одного покупателя.

Узнайте:
1. Какова общая выручка магазина
2. Какова выручка магазина по каждому типу товаров
3. Какой тип товара был продан на самую большую сумму
4. Сколько различных типов товаров было продано за день

### Формат входных данных

Дан текстовый файл. На каждой строке записана информация о проданных товарах в формате:

**тип_товара:цена**, например **fruits:45.10**

Все проданные товары разделены одним или более пробелами.

### Формат выходных данных

Вывести:
1. Какова общая выручка магазина
2. Какова выручка магазина по каждому типу товаров
3. Какой тип товара был продан на самую большую сумму. Если таких несколько, вывести любой.
4. Сколько различных типов товаров было продано за день

### Решение задачи

```python
path = "items_sold.txt" 

chek = {}
i=0
with open(path, "r", encoding="UTF-8") as sold:
    for line1 in sold:
      fruits = []
      price = []
      line1=line1.split()
      for line2 in line1:
        line3=line2.split(":")
        fruits.append(line3[0])
        price.append(float(line3[1]))
      chek[i] = dict(zip(fruits, price))
      i+=1
elm = i

goods = {}

for i in range(elm):
  for key, value in chek[i].items():
    goods [key] = 0  

summ = 0
product = ''
max_value = 0 
for i in range(elm):
  for key, value in chek[i].items():
    goods [key] += value
    summ+=value
    if max_value < value:
      max_value = value
      product = key
    

print (goods)
 
print ('1. Общая выручка магазина =', summ)
print ('2. Выручка магазина по каждому типу товаров:')
for key, value in goods.items():
  print (key, '-', round (value,2))
print ('3.', product, '- товар был продан на самую большую сумму.')

print ('4. Различных типов товаров было продано за день:')
for i in range(elm):
  print (i+1, 'день', len(chek[i]), 'продукт(ов)')
  
```

---
