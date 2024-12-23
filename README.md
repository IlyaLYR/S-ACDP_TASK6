# Лабиринт Минотавра

Дано поле размером N×M, некоторые клетки поля закрашены. В одной из незакрашенных клеток поля стоит Минотавр, он умеет
ходить только по незакрашенным клеткам (из текущей клетки он может пойти только в ту клетку, с которой имеет общую
сторону). Какое минимальное количество клеток нужно закрасить, чтобы Минотавр не смог выбраться за пределы поля?

## Доказательство:

Очевидно, что ответ не больше, чем количество всех путей от Минотавра до крайних клеток. Сделаем ещё более строгое
неравенство: ответ не больше, чем максимальное количество клеточно-непересекающихся путей, т.к. если взять какие-нибудь
2 пересекающихся пути и закрасить клетку в позиции, где они пересекаются, то блокируется выход за пределы поля сразу по
2 этим путям. С другой стороны, если закрасить клетку на каком-то из путей, то блокируется только этот путь, т.к. были
взяты клеточно-непересекающиеся пути. Значит, ответ не меньше, чем количество таких путей.

## Переход к сети

Рассмотрим сеть, в которой вершинам будут соответствовать незакрашенные клетки поля, соседние незакрашенные клетки
соединим ориентированными рёбрами с пропускной способностью 1. В качестве истока возьмём вершину, которой соответствует
клетка Минотавр. Добавим в граф ещё одну вершину — сток, добавим рёбра из вершин, соответствующим крайним клеткам поля,
в сток с пропускной способностью 1. Чтобы пути не пересекались по клеткам, раздвоим каждую вершину графа на 2 вершины: в
одну будут только входить рёбра, из другой — только выходить рёбра, и сами эти вершины соединим ребром с пропускной
способностью 1. Используя алгоритм Форда-Фалкерсона, найдём максимальный поток в сети. Согласно теореме о декомпозиции,
нахождение максимального потока эквивалентно тому, что мы нашли максимальное количество путей из истока в сток. Т.е.
требуемый ответ на задачу равен максимальному потоку.
