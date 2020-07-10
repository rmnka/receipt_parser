Для создания размеченного датасета я использовал этот [ресурс](https://xmldatafeed.com/catalog/) *(не реклама)*. Там можно скачать уже готовые спаршенные данные с разных магазинов. Однако была проблема, что информация уже немного устаревшая, поэтому пришлось писать свои парсеры, чтобы обогатить данные.

## Описание парсеров:
* [Перекрёсток](https://www.perekrestok.ru) - собраны все актуальные товары.
* [Магнит](https://edadeal.ru/) - к сожалению, у них не представлен список товаров на сайте, поэтому пришлось парсить едадил, но данных там мало.
* [Пятёрочка](http://pyaterochkaakcii.ru/) - аналогично магниту, для неё нет списка товаров, единственное, что мне удалось найти, так это сайт с акциями, вот его и парсил.
* [Тинькофф](https://receiptnlp.tinkoff.ru/) - это сервис для нормализации чеков, он достаточно не плох и в нём используются нейронки. Я порой использовал его для разметки данных. Для скрапинга используется selenium, а чтобы запустить его, нужно из команжной строки передать 3 аргумента:
	* Путь до датасета в формате .csv, который нужно разметить. Колонка с описанием товара должна называться `Название`.
	* Путь, куда будет сохраняться размеченный датасет.
	* Количество ядер CPU, для мультипроцессинга

	Пример использования:
	```bash
	$ python3 tinkoff.py magnit.csv magnit_clean.csv 4
	```