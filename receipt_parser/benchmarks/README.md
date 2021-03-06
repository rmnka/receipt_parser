## Датасет
Для оценки работы разных моделей нормализаторов [собран](https://github.com/slgero/check_parser/blob/master/receipt_parser/benchmarks/prepare_benchmark.ipynb) следующий датасет [standard.csv](https://github.com/slgero/check_parser/blob/master/receipt_parser/benchmarks/standard.csv "standard.csv"):

```python
pd.read_csv('standard.csv').sample(5)
```
|    | shop_name   | Название                                         | product          | brand   | category                        |
|---:|:------------|:-------------------------------------------------|:-----------------|:--------|:--------------------------------|
| 27 | МАГНИТ      | ПЕРЕЦ красный 1кг                                | перец            | -       | Овощи, фрукты, ягоды            |
|  4 | АТАК        | СР-ВО АНТИЖИР 500МЛ                              | средство антижир | -       | Красота, гигиена, бытовая химия |
| 10 | БИЛЛА       | БАНАНЫ                                           | бананы           | -       | Овощи, фрукты, ягоды            |
| 37 | ПЕРЕКРЕСТОК | БЗМЖ Йогурт EPICA SIMPLE 130г                    | йогурт           | epica   | Молоко, сыр, яйца               |
| 28 | МАГНИТ      | РУБАТКИ Котлеты куриные с чесноком 450г п/п(Котл | котлеты          | рубатки | Птица, мясо, деликатесы         |

Он включает в себя 5 рандомно выбранных товарных позиций для каждого магазина из списка: Атак, Ашан, Билла, Дикси, Лента, Магнит, О'кей, Перекрёсток, Пятёрочка.

## Система оценки
Оценка производится по 3 категориям:
1. Название товара
2. Бренд товара
3. Категория товара

Для оценки использовалась самописная accuracy:
-   за каждый верное угадывание +1 балл
-   за частично верное +0.5
-   за неверное +0

Затем общая оценка переводится в проценты.

## Результаты
Качество распознавания для [Тинькофф](https://receiptnlp.tinkoff.ru/#/):
* Название товара: 86%
* Бренд товара: 67%
* Категория товара: 76%

Качество распознавания для [RuleBased model](https://github.com/slgero/check_parser/blob/master/receipt_parser/reciept_parser.py#L12):
* Название товара: 92%
* Бренд товара: 84%
* Категория товара: 76%

Более подробно можно ознакомится [здесь](https://github.com/slgero/check_parser/blob/master/receipt_parser/benchmarks/evaluate.ipynb).

***
P.S. Не хочется занижать работу ребят из Тинькофф, возможно, на сайте представлена урезанная версия для распознавания. Насколько я понял, занимаясь этой задачей, они используют несколько разных нейронных сетей для распознавания, что должно быть куда круче, чем моя модель, основанная на простых правилах :)