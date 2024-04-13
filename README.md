# MindSet_test
Тестовое задание для стажировки в компании [MindSet](https://m-s-e-t.com/ru)

## Постановка задачи
Найти и изучить изучить 10 алгоритмов Visual Slam/Odometry применить найденные алгоритмы для построения траектории человека, по заданному видео.

## Visual Slam / Odometry
Визуальная Одометрия - это процесс оценки собственного движения наблюдателя (транспортного средства/человека/робота) в реальном времени на основании изображений одной или нескольких камер, установленных на нём.

Сравнение VO (Visual Odometry) и VSlam (Visual Slam):
VO | VSlam 
--- | --- 
Получение локального пути | Получение глобального пути
Последовательное восстановление пути кадр за кадром | Хранение карты для определения замыкания (loop closure)
Оптимизация последних n поз (window bundle adjustment) | Оптимизация на основе информации о замыканиях

## Подходы изученные в процессе выполнения задачи
Direct Slam - В рамках этого подхода мы напрямую отслеживаем пиксели. В каком-то смысле мы вычисляем ID точки, для этого используется одно число — яркость этих пикселей.

Feature Based Slam - Находим четкие границы, за которыми удобно следить между кадрами. Оставляем только точки с самым сильным градиентом (изменением цвета) в небольших окошках. Для каждой точки считаем ORB-дескриптор — некий ID. Затем по битам сравниваем ID точек на сходство.

Double Window Optimization - Оптимизация, которая выполняется путем минимизации суммы квадратов ошибок χ2 по всем позициям Ti ∈ W1 ∪ W2 в double window и по всем соответствующим точкам xk.

Stereo DSO  - Ответвление direct slam направленное на обработку видо со стерео камер.

Sparser Relative Bundle Adjustment -  Это метод, который используется для восстановления 3D-структуры и положения камеры на основе серии монокулярных или стереоизображений.

## Файлы решения
папка Videos - папка в которой содержатся видео с демонстрацией работы программы.

папка Images - папка в которой содержатся фото финальной карты.

файл config.yaml - файл с конфигурацией видеокамеры.

файл map.msg - файл с получившейся картой.

## Необходимые библиотеки
Eigen : version 3.3.0 or later.

g2o : 20230223_git or later. 20230223_git is recommended.

SuiteSparse : Required by g2o.

FBoW : Please use the custom version of FBoW released in [source](https://github.com/stella-cv/FBoW).

yaml-cpp : version 0.6.0 or later.

OpenCV : version 3.3.1 or later.

[Stella_Vslam](https://github.com/stella-cv/stella_vslam)


## Запуск программы

 ./run_video_slam -v ./orb_vocab.fbow -m ./2.mp4 -c ./config.yaml --frame-skip 3 --no-sleep --map-db-out map.msg

## Полученная карта

![final_map](https://github.com/gsgol/MindSet_test/assets/77744037/973d14fd-b53e-4c21-bac7-148070008afe)

## References
@inproceedings{openvslam2019,

  author = {Sumikura, Shinya and Shibuya, Mikiya and Sakurada, Ken},
  
  title = {{OpenVSLAM: A Versatile Visual SLAM Framework}},
  
  booktitle = {Proceedings of the 27th ACM International Conference on Multimedia},
  
  series = {MM '19},
  
  year = {2019},
  
  isbn = {978-1-4503-6889-6},
  
  location = {Nice, France},
  
  pages = {2292--2295},
  
  numpages = {4},
  
  url = {http://doi.acm.org/10.1145/3343031.3350539},
  
  doi = {10.1145/3343031.3350539},
  
  acmid = {3350539},
  
  publisher = {ACM},
  
  address = {New York, NY, USA}
}


