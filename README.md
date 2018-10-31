# MachineLearning

- [Метрические алгоритмы классификации](#Метрические-алгоритмы-классификации)
  - [1NN](#1NN)
  - [KNN](#KNN)
  - [KWNN](#KWNN)
  - [Сравнение качества алгоритмов kNN и kwNN](#Сравнение-качества-алгоритмо-kNN-и-kwNN)
  - [Парзеновское окно](#Парзеновское окно)


## Метрические алгоритмы классификации
__Гипотеза компактности:__
Схожим объектам соответствуют схожие ответы.
Для формализации понятия сходства вводится __функция расстояния__ в
пространстве объектов X. 

__Метрические методы обучения__ — методы, основанные на анализе сходства
объектов. (similarity-based learning, distance-based learning).

## 1NN 
Алгоритм ближайшего соседа – 1NN относит классифицируемый объект
u ∈ X к тому классу, которому принадлежит его ближайший сосед:
<a href="http://www.picshare.ru/view/9312477/" target="_blank"><img src="http://www.picshare.ru/uploads/181017/84uQkCZ7F7.jpg" border="0" width="811" height="524" title="Хостинг картинок PicShare.ru"></a>


__Преимуществ:__
<ul>
  <li>Простота реализации.</li>
</ul>

__Недостатки:__
<ul>
  <li>Неустойчивость к погрешностям — выбросам.</li>
  <li>Отсутствие параметров, которые можно было бы настраивать по выборке.</li>
  <li>Алгоритм полностью зависит от того, насколько удачно выбрана метрика ρ.</li>
  <li>Низкое качество классификации.</li>
</ul>

## KNN 

__Алгоритм k ближайших соседей – kNN__ относит объект u к тому классу,
элементов которого больше среди k ближайших соседей x.
__функция оценки близости__  <br><a href="https://imgbb.com/"><img src="https://image.ibb.co/g8GRPU/2.png" alt="2" border="0"></a>

При k = 1 получаем метод ближайшего соседа
и, соответственно, неустойчивость к шуму, при k = l, наоборот, алгоритм
чрезмерно устойчив и вырождается в константу. Таким образом, крайние значения
k нежелательны. На практике оптимальное k подбирается по критерию
скользящего контроля LOO.

![LOO для KNN...](KNN/KnnPng.png) 
## KWNN
Существует и альтернативный вариант метода kNN: в каждом классе выбирается
__k__ ближайших к __U__ объектов, и объект u относится к тому классу, для
которого среднее расстояние до __k__ ближайших соседей минимально.
![](http://latex.codecogs.com/gif.latex?w%28i%2Cu%29%3D%5Bi%5Cleq%20k%5Dw%28i%29)
где,
![](http://latex.codecogs.com/gif.latex?w%28i%29) — строго убывающая последовательность вещественных весов, задающая
вклад i-го соседа при классификации объекта u.

![LOO для KWNN...](KWNN/KWNNPNG.png) 
я решил использовать весы такого вида
```
weightsKWNN = function(i, k)
{
  (k + 1 - i) / k
}
```

## Сравнение качества алгоритмо kNN и kwNN. 

kNN — один из простейших алгоритмов классификации, поэтому на реальных задачах он зачастую оказывается неэффективным. Помимо точности классификации, проблемой этого классификатора является скорость классификации.

kwNN отличается от kNN, тем что учитывает порядок соседей классифицируемого объекта, улчшая качество классификации.
Пример, показывающий преимущество метода kwNN над kNN:
<a href="http://www.picshare.ru/view/9312480/" target="_blank"><img src="http://www.picshare.ru/uploads/181018/l7iAu3dDsZ.jpg" border="0" width="1462" height="524" title="Хостинг картинок PicShare.ru"></a>

В примере передается параметр k=5. Так как Kwnn в отличии от Knn оценивает не только индекс соседа, но и его расстояние, то результат получается более точный, в этом примере это наглядно видно.

## Парзеновское окно

