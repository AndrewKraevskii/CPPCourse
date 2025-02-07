#	Основные понятия теории графов. DFS и его применения

[TOC]

##	Графы

###	Что такое граф?

Граф - это совокупность множества вершин и множества ребер, их соединяющих.

![Картинки по запросу "графы примеры"](https://graphonline.ru/tmp/saved/Pl/Planar.png)

**Множество вершин** графа обозначают буквой $V$.

**Множество ребер** графа обозначают буквой $E$.

Чаще всего, когда говорят о конкретных вершинах графа, их называют буквами $u, v$.

**Смежные вершины** - вершины u и v, для которых существует ребро (u, v).

###	Основные понятия теории графов

####	Ориентированность

Ориентированный граф - граф, где множество ребер представляет собой набор **упорядоченных** пар, то есть ребро (u, v) означает, что из вершины u можно напрямую попасть в вершину v, но при этом ничего не говорит о возможности попасть из вершины v в вершину u.

![Directed.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a2/Directed.svg/125px-Directed.svg.png)

Неориентированный граф - граф, где множество вершин  представляет собой неупорядоченный набор пар, то есть наличие ребра (u, v) означает, что из вершины u можно попасть в вершину v и наоборот.

![Undirected.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/b/bf/Undirected.svg/125px-Undirected.svg.png)

####	Связность графа

**Связный граф** — граф, содержащий ровно одну компоненту связности. Это означает, что между любой парой вершин этого графа существует как минимум один путь.

На картинке три компоненты связности: $1: (A, B, C, D, G); 2: (F, E); 3: (H)$

![Картинки по запросу "несвязный граф"](https://sites.google.com/site/pythontutorarticles/_/rsrc/1478606469815/grafy-opredelenia-i-sposoby-hranenia/first_graph.png)

####	Циклы. Деревья 

**Цикл **- любой путь в графе, содержащий хотя бы одно ребро, а также начинающийся и заканчивающийся в одной вершине.

![Картинки по запросу "wbrk d uhfat"](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/Undirected_6_cycle.svg/274px-Undirected_6_cycle.svg.png)

**Дерево** - связный граф, не содержащий циклов.

![Картинки по запросу "lthtdj uhfa"](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Binary_tree.svg/192px-Binary_tree.svg.png)

####	Петли и кратные ребра. Простой граф

![Картинки по запросу "петли и кратные ребра"](https://sites.google.com/site/pythontutorarticles/_/rsrc/1478606497888/grafy-opredelenia-i-sposoby-hranenia/third_graph.png)

**Петля** - ребро в графе, начинающееся и заканчивающееся в одной вершине. 
Пример: $(u, u)$. 
Замечание: является тривиальным случаем цикла.

**Кратные ребра** - ребра, начинающиеся и заканчивающиеся в одних и тех же вершинах. 

**Простой граф** - граф без петель и кратных ребер. Чаще всего в теории графов рассматриваются именно простые графы.

###	Способы представления графов

####	Матрица смежности

Матрица смежности - двумерный массив, где на месте $[i][j]$ стоит 0 или 1. 1 в случае, если существует ребро из вершины i в вершину j, 0 - если не существует.

![Картинки по запросу "матрица смежности графа"](https://prog-cpp.ru/wp-content/uploads/graf2.png)

####	Список смежности

Список смежности - массив, в каждой ячейке которого хранится список/множество вершин, для которых существует ребро в них из исходной.

![Картинки по запросу "список смежности графа"](https://prog-cpp.ru/wp-content/uploads/graf4.png)

##	DFS (Deep First Search)

Очень часто при работе с графами нам становится необходимо обойти все вершины графа в каком-то порядке. Всего таких часто применяемых порядков два - обход в глубину (DFS) и обход в ширину (BFS). Давайте рассмотрим первый.

Этот алгоритм, применяемый для проверки связности, поиска цикла и компонент сильной связности в графе, для топологической сортировки. Кроме того, он применяется во многих задачах, где использование графов и, в частности, DFS сначала кажется странным.

### Описание алгоритма

Общая идея алгоритма состоит в следующем: для каждой *не пройденной* вершины необходимо найти все *не пройденные* смежные вершины и повторить поиск для них.

1. Выбираем любую вершину из еще *не пройденных*, обозначим ее как u.

2. Запускаем процедуру dfs(u)

   - Помечаем вершину u как *пройденную*
   - Для каждой *не пройденной* смежной с u вершиной (назовем ее v) запускаем dfs(v)

3. Повторяем шаги 1 и 2, пока все вершины не окажутся *пройденными*.

### Псевдокод

```pseudocode
function dfs(u: int):
  color[u] = gray           
  for v: (u, v) in G                   
    if color[v] == white
      dfs(v)
  color[u] = black   
  
function doDfs(G[n]: Graph): // принимает граф G с кол-вом вершин n и выполняет DFS в нем
   color = array[n, white]
   
   for i = 1 to n             
      if color[i] == white                
         dfs(i)
```

### Пример

Пример смотрим [тут]([http://neerc.ifmo.ru/wiki/index.php?title=%D0%9E%D0%B1%D1%85%D0%BE%D0%B4_%D0%B2_%D0%B3%D0%BB%D1%83%D0%B1%D0%B8%D0%BD%D1%83,_%D1%86%D0%B2%D0%B5%D1%82%D0%B0_%D0%B2%D0%B5%D1%80%D1%88%D0%B8%D0%BD](http://neerc.ifmo.ru/wiki/index.php?title=Обход_в_глубину,_цвета_вершин)).

Рассмотрим, как будут изменяться цвета вершин при обходе в глубину данного графа.

| Описание шага                                                | Состояние графа                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| В функции doDfs присваиваем всем вершинам в массиве color[] белый цвет. Затем проверяем, что первая вершина окрашена в белый цвет. Заходим в нее и раскрашиваем ее в серый цвет. | [![Dfs1.png](http://neerc.ifmo.ru/wiki/images/f/f7/Dfs1.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs1.png) |
| Пробуем пойти в вершину с номером 2. Проверяем, что она белая, и переходим в нее. Окрашиваем ее в серый цвет. | [![Dfs2.png](http://neerc.ifmo.ru/wiki/images/1/1f/Dfs2.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs2.png) |
| Пробуем пойти в вершину с номером 3. Проверяем, что она белая, и переходим в нее. Окрашиваем ее в серый цвет. | [![Dfs3.png](http://neerc.ifmo.ru/wiki/images/9/94/Dfs3.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs3.png) |
| Проверяем, что из вершины с номером 3 не исходит ни одного ребра. Помечаем ее в черный цвет и возвращаемся в вершину с номером 2. | [![Dfs4.png](http://neerc.ifmo.ru/wiki/images/a/a4/Dfs4.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs4.png) |
| Пробуем пойти в вершину с номером 4. Проверяем, что она белая, и переходим в нее. Окрашиваем ее в серый цвет. | [![Dfs5 6 7.png](http://neerc.ifmo.ru/wiki/images/7/73/Dfs5_6_7.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs5_6_7.png) |
| Пробуем пойти в вершину с номером 3. Видим, что она черного цвета, и остаемся на месте. | [![Dfs5 6 7.png](http://neerc.ifmo.ru/wiki/images/7/73/Dfs5_6_7.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs5_6_7.png) |
| Пробуем пойти в вершину с номером 1. Видим, что она серого цвета, и остаемся на месте. | [![Dfs5 6 7.png](http://neerc.ifmo.ru/wiki/images/7/73/Dfs5_6_7.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs5_6_7.png) |
| Из вершины с номером 4 больше нет исходящих ребер. Помечаем ее в черный цвет и возвращаемся в вершину с номером 2. | [![Dfs8.png](http://neerc.ifmo.ru/wiki/images/6/64/Dfs8.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs8.png) |
| Из вершины с номером 2 больше нет исходящих ребер. Помечаем ее в черный цвет и возвращаемся в вершину с номером 1. | [![Dfs9.png](http://neerc.ifmo.ru/wiki/images/f/f5/Dfs9.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs9.png) |
| Из вершины с номером 1 больше нет исходящих ребер. Помечаем ее в черный цвет и выходим в программу doDfs. В ней проверяем, что все вершины окрашены в черный цвет. Выходим из функции doDfs. Алгоритм завершен. | [![Dfs10.png](http://neerc.ifmo.ru/wiki/images/b/bb/Dfs10.png)](http://neerc.ifmo.ru/wiki/index.php?title=Файл:Dfs10.png) |

###	Асимптотика работы алгоритма

Оценим время работы обхода в глубину. 

Процедура dfs вызывается от каждой вершины не более одного раза, а внутри процедуры рассматриваются все ребра, начинающиеся в текущей вершине. Всего таких ребер для всех вершин в графе $O(E)$, следовательно, время работы алгоритма оценивается как $O(V+E)$.

###	Примеры задач, решающихся при помощи DFS.

####	Проверка наличия пути из одной вершины в другую

| **Задача:**                                                  |
| ------------------------------------------------------------ |
| *Дан граф $G=(V,E)$ и две вершины s и t. Необходимо проверить, существует ли путь из вершины s в вершину t по рёбрам графа G.* |

Небольшая модификация алгоритма обхода в глубину. Смысл алгоритма заключается в том, чтобы запустить обход в глубину из вершины s и проверять при каждом посещении вершины, не является ли она искомой вершиной t. Так как в первый момент времени все пути в графе "белые", то если вершина t и была достижима из s, то по [лемме о белых путях](https://neerc.ifmo.ru/wiki/index.php?title=Лемма_о_белых_путях) в какой-то момент времени мы зайдём в вершину t, чтобы её покрасить. Время работы алгоритма $O(|V|+|E|)$.

#### Проверка графа на связность

| **Задача:**                                                  |
| ------------------------------------------------------------ |
| *Дан неориентированный граф $G=(V,E)$. Необходимо проверить, является ли он связным.* |

Снова небольшая модификация алгоритма обхода в глубину, в которой будем возвращать количество посещенных вершин. Запустим такой dfs() от некоторой вершины графа G, если его результат равен |V|, то мы побывали во всех вершинах графа, а следовательно он связен, иначе какие-то вершины остались непосещенными. Работает алгоритм за O(|V|+|E|).

#####	Псевдокод

```pseudocode
int dfs(u: int, visited: bool[]):              
    int visitedVertices = 1
    visited[u] = true           // помечаем вершину как пройденную
    for v: uv ∈∈ E             // проходим по смежным с u вершинам
        if not visited[v]     // проверяем, не находились ли мы ранее в выбранной вершине
            visitedVertices += dfs(v, visited)
    return visitedVertices
```

####	Алгоритм пути для прохода по лабиринту

[Ссылка на хабр](https://habr.com/ru/post/200074/)

![img](https://habrastorage.org/getpro/habr/post_images/7fa/964/81d/7fa96481dab0e4d868bb82f77adb4f1f.jpg)

| **Задача:**                                                  |
| ------------------------------------------------------------ |
| *Дан лабиринт. Он разделен на множество комнат, между некоторыми из них можно перемещаться. Требуется найти путь из комнаты A в комнату B.* |

Пример комнаты:

![img](https://habrastorage.org/getpro/habr/post_images/2e7/466/b05/2e7466b05ca84f21eb216732a2a98117.gif)

Заметим, что в теории графов «комнаты» называются вершинами, «переходы» между ними — ребрами. Комната А — начальная вершина, комната В — конечная.

Тогда наш лабиринт можно представить в виде графа:

![img](https://habrastorage.org/getpro/habr/post_images/4a5/f7a/73f/4a5f7a73fc544d64a9cc4fa00111a001.png)

Теперь мы свели задачу к поиску наличия пути из вершины u в вершину v,  который мы уже поняли, как решать выше.

Осталось научиться выводить путь. Для этого будем хранить отдельно для каждой вершины, откуда мы в нее пришли. Тогда по окончании работы DFS мы для каждой вершины будем знать, как мы в нее попали. Теперь начиная из последней вершины (v) и идя по полученному пути, мы в какой-то момент найдем вершину u. 

Такая задача кажется простой, но только вот мы в таком случае можем найти очень длинный путь из одной вершины в другую, а если нам было бы важно прибежать к финишу быстрее всех, то нам пришлось бы сильно изменить наш алгоритм. Как именно это сделать? Можете подумать на досуге.



##	ДЗ

Реализуйте поиск пути из одной точки в другую в лабиринте. Лабиринт является картинкой в формате .png, Цвет стен - черный, цвет пола - белый. Необходимо загружать картинку из файла, обрабатывать два нажатия мыши на две точки (начало и конец). Рисовать сам путь внутри лабиринта цветом sf::Color(255, 0, 0, 100).	