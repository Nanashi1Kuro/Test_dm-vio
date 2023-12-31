# Метод DM-VIO

DM-VIO (Delayed Marginalization Visual-Inertial Odometry) - это метод визуальной инерциальной одометрии (VIO), основанный на VIO-DSO и DSO. Для более подробного понимания этого метода рекомендуется изучить статьи, связанные с DSO [DSO] [DM].

## Особенности DSO

В ходе исследования было обнаружено, что DSO обладает уникальной особенностью - максимальное использование фотометрических параметров камеры, что включает в себя оценки глубины, внутренние параметры камеры и коэффициенты аффинной коррекции яркости.

## Метод DM-VIO

DM-VIO представляет собой интегрированную систему, объединяющую данные с камеры и инерционных датчиков для более точного определения перемещения и ориентации устройства в пространстве.

![Скриншот работы метода DM-VIO](images/fg1.png)

### Ключевые аспекты DM-VIO включают в себя:

- Применение отложенной маргинализации для точного определения состояния системы.
- Прямую оптимизацию фотометрической функции ошибок для коррекции графов поз с учетом фотометрической неопределенности.
- Использование частичной маргинализации для эффективной обработки данных и оптимизации графов поз.
- Многоуровневую инициализацию IMU для улучшения точности оценок и производительности определения состояния.

## Создание Docker-образа и работа с ним

[Docker](https://www.docker.com/) - это платформа для разработки, доставки и запуска приложений с использованием контейнеров. 

### Установка Docker

Следуйте инструкции по [ссылке](https://docs.docker.com/get-docker/) для установки Docker.

### Клонирование репозитория

```bash
git clone https://github.com/Nanashi1Kuro/Test_dm-vio.git
cd Test_dm-vio
