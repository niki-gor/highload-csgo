# CS:GO System Design

## Содержание

* [Тема и целевая аудитория](#1)
* [Расчет нагрузки](#2)
* [Логическая схема](#3)
* [Физическая схема](#4)
* [Технологии](#5)
* [Схема проекта](#6)
* [Список серверов](#7)


## 1. Тема и целевая аудитория <a name="1"></a>

**Counter Strike: Global Offensive** — многопользовательский шутер от первого лица, разработанный компаниями Valve и Hidden Path Entertainment.

### MVP
- Подбор матча на основе ELO и геолокации
- Двусторонняя отправка запросов игрок-сервер в реальном времени
- Просмотр игровой статистики
- Интеграция с Торговой площадкой Steam
  - Во время игры может случайным образом выпасть предмет, который затем можно продать

### Целевая аудитория

[CS:GO имеет 43,3 млн активных пользователей в месяц](https://activeplayer.io/counter-strike-global-offensive/) (август 2023).

[Распределение игроков по странам](https://cybersport.metaratings.ru/news/rossiya-vozglavila-spisok-stran-po-kolicestvu-igrokov-v-matcmeikinge-csgo-44609/) (июль 2022).
![Alt text](image-1.png)

## 2. Расчет нагрузки <a name="2"></a>

### Продуктовые метрики

- Месячная аудитория - 43,3 млн человек
- Играют одновременно в среднем [900 тысяч человек](https://steamcharts.com/app/730)
  - Число людей, непосредственно находящихся в матче, меньше
- Среднее количество действий пользователя по типам в день
  1. Подбор матча.
     TBD
  2. Двусторонняя отправка запросов игрок-сервер в реальном времени.
      - Есть разные типы матчей
        - MM (MatchMaking, основной) длится около 40 минут.   
        - Deathmatch, гонка вооружений и др. длятся около 15 минут.
      - В среднем возьмем 20 минут.
      - Скриншот из Wireshark, зафиксирована 1 секунда во время матча ![Alt text](image-4.png)
        - От сервера (162.254.198.101, Стокгольм) пришло чуть более 60 пакетов, каждый из которых в среднем весит 600 байт
          - Тикрейт официальных серверов - 60
        - От клиента к серверу было отправлено 22 пакета, каждый из которых в среднем весит 160 байт
          - Так мало пакетов могло быть отправлено из-за недостаточных технических характеристик оборудования для игры
            - Я играл с 20-30 FPS
  3. Получение после матча игровых предметов, связанных с Торговой площадкой
      - TBD определить, сколько предметов выпадает ежедневно  


### Технические метрики
TBD
## 3. Логическая схема <a name="3"></a>

## 4. Физическая схема <a name="4"></a>

## 5. Технологии <a name="5"></a>

## 6. Схема проекта <a name="6"></a>

## 7. Список серверов <a name="7"></a>

### Глобальная балансировка

Низкий пинг является неотъемлемой частью игры в шутер, поэтому нагрузка будет распределяться с помощью Latency-based DNS.

### Физическое расположение датацентров

Физическое расположение датацентров, [карта](https://netduma.com/blog/csgo-server-locations/)
![Alt text](image-2.png)

Несмотря на то, что в России больше всего игроков (11,51% ото всех игроков, в США - 10,71%), датацентры на Урале и в Сибири полностью отсутствуют.

Физическое расположение датацентров, [список]()
![Alt text](image-3.png)