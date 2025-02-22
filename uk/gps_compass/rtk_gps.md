# RTK GNSS (GPS)

[Системи GNSS/GPS з реальним кінематичним положенням (RTK)](https://en.wikipedia.org/wiki/Real_Time_Kinematic) забезпечують точність на рівні сантиметрів, що дозволяє використовувати PX4 у таких застосунках, як точне обстеження (де важлива точність до кожного сантиметра).

Ця функція потребує _QGroundControl_, який працює на ноутбуці/ПК та транспортного засобу з бездротовим або телеметричним радіозв'язком з наземним лаптопом.

:::info Деякі налаштування RTK GNSS можуть надавати інформацію про курс/головний напрямок як альтернативу компасу:

- [Напрямок за допомогою RTK GPS з подвійним u-blox F9P](../gps_compass/u-blox_f9p_heading.md).
- GPS безпосередньо виводить курс (див. таблицю нижче).

:::

## Пристрої, що підтримуються

PX4 підтримує GPS [u-blox M8P](https://www.u-blox.com/en/product/neo-m8p), [u-blox F9P](https://www.u-blox.com/en/product/zed-f9p-module) та [Trimble MB-Two](https://www.trimble.com/Precision-GNSS/MB-Two-Board.aspx), а також продукцію, що включає їх.

Список сумісних пристроїв RTK нижче, які очікуються для роботи з PX4 (він виключає припинені пристрої). Таблиця вказує пристрої, які також виводять курсову відмітку, а також можуть надавати курсову відмітку, коли використовуються дві одиниці на транспортному засобі. Він також відзначає пристрої, які підключаються через CAN шину, та ті, які підтримують PPK (пост-процесуальну кінематику).

| Пристрій                                                                                                  |         GPS          |  Компас  | [DroneCAN](../dronecan/index.md) | [GPS Yaw](#configuring-gps-as-yaw-heading-source) |   PPK   |
|:--------------------------------------------------------------------------------------------------------- |:--------------------:|:--------:|:--------------------------------:|:-------------------------------------------------:|:-------:|
| [ARK RTK GPS](../dronecan/ark_rtk_gps.md)                                                                 |         F9P          |  BMM150  |             &check;              |                [Dual F9P][DualF9P]                |         |
| [ARK MOSAIC-X5 RTK GPS](../dronecan/ark_mosaic__rtk_gps.md)                                               |      Mosaic-X5       | IIS2MDC  |             &check;              |      [Septentrio Dual Antenna][SeptDualAnt]       |         |
| [CUAV C-RTK GPS](../gps_compass/rtk_gps_cuav_c-rtk.md)                                                    |       M8P/M8N        | &check;  |                                  |                                                   |         |
| [CUAV C-RTK2](../gps_compass/rtk_gps_cuav_c-rtk2.md)                                                      |         F9P          | &check;  |                                  |                [Dual F9P][DualF9P]                |         |
| [CUAV C-RTK 9Ps GPS](../gps_compass/rtk_gps_cuav_c-rtk-9ps.md)                                            |         F9P          |  RM3100  |                                  |                [Dual F9P][DualF9P]                |         |
| [CUAV C-RTK2 PPK/RTK GNSS](../gps_compass/rtk_gps_cuav_c-rtk.md)                                          |         F9P          |  RM3100  |                                  |                                                   | &check; |
| [CubePilot Here+ RTK GPS](../gps_compass/rtk_gps_hex_hereplus.md)                                         |         M8P          | HMC5983  |                                  |                                                   |         |
| [CubePilot Here3 CAN GNSS GPS (M8N)](https://www.cubepilot.org/#/here/here3)                              |         M8P          | ICM20948 |             &check;              |                                                   |         |
| [Drotek SIRIUS RTK GNSS ROVER (F9P)](https://store-drotek.com/911-sirius-rtk-gnss-rover-f9p.html)         |         F9P          |  RM3100  |                                  |                [Dual F9P][DualF9P]                |         |
| [DATAGNSS GEM1305 RTK Receiver][DATAGNSS GEM1305 RTK]                                                     |       TAU951M        | &cross;  |                                  |                      &cross;                      |         |
| [Femtones MINI2 Receiver](../gps_compass/rtk_gps_fem_mini2.md)                                            |     FB672, FB6A0     | &check;  |                                  |                                                   |         |
| [Freefly RTK GPS](../gps_compass/rtk_gps_freefly.md)                                                      |         F9P          | IST8310  |                                  |                                                   |         |
| [Holybro H-RTK ZED-F9P RTK Rover (DroneCAN variant)](../dronecan/holybro_h_rtk_zed_f9p_gps.md)            |         F9P          |  RM3100  |             &check;              |                [Dual F9P][DualF9P]                |         |
| [Holybro H-RTK ZED-F9P RTK Rover](https://holybro.com/collections/h-rtk-gps/products/h-rtk-zed-f9p-rover) |         F9P          |  RM3100  |                                  |                [Dual F9P][DualF9P]                |         |
| [Holybro H-RTK F9P Ultralight](https://holybro.com/products/h-rtk-f9p-ultralight)                         |         F9P          | IST8310  |                                  |                [Dual F9P][DualF9P]                |         |
| [Holybro H-RTK F9P Helical or Base](../gps_compass/rtk_gps_holybro_h-rtk-f9p.md)                          |         F9P          | IST8310  |                                  |                [Dual F9P][DualF9P]                |         |
| [Holybro DroneCAN H-RTK F9P Helical](https://holybro.com/products/dronecan-h-rtk-f9p-helical)             |         F9P          |  BMM150  |             &check;              |                [Dual F9P][DualF9P]                |         |
| [Holybro H-RTK F9P Rover Lite](../gps_compass/rtk_gps_holybro_h-rtk-f9p.md)                               |         F9P          | IST8310  |                                  |                                                   |         |
| [Holybro DroneCAN H-RTK F9P Rover](https://holybro.com/products/dronecan-h-rtk-f9p-rover)                 |         F9P          |  BMM150  |                                  |                [Dual F9P][DualF9P]                |         |
| [Holybro H-RTK M8P GNSS](../gps_compass/rtk_gps_holybro_h-rtk-m8p.md)                                     |         M8P          | IST8310  |                                  |                                                   |         |
| [Holybro H-RTK Unicore UM982 GPS](../gps_compass/rtk_gps_holybro_unicore_um982.md)                        |        UM982         | IST8310  |                                  |      [Unicore Dual Antenna][UnicoreDualAnt]       |         |
| [LOCOSYS Hawk R1](../gps_compass/rtk_gps_locosys_r1.md)                                                   |     MC-1612-V2b      |          |                                  |                                                   |         |
| [LOCOSYS Hawk R2](../gps_compass/rtk_gps_locosys_r2.md)                                                   |     MC-1612-V2b      | IST8310  |                                  |                                                   |         |
| [mRo u-blox ZED-F9 RTK L1/L2 GPS](https://store.mrobotics.io/product-p/m10020d.htm)                       |         F9P          | &check;  |                                  |                [Dual F9P][DualF9P]                |         |
| [RaccoonLab L1/L2 ZED-F9P][RaccoonLab L1/L2 ZED-F9P]                                                      |         F9P          |  RM3100  |             &check;              |                                                   |         |
| [RaccoonLab L1/L2 ZED-F9P with external antenna][RaccnLabL1L2ZED-F9P ext_ant]                             |         F9P          |  RM3100  |             &check;              |                                                   |         |
| [Septentrio AsteRx-m3 Pro](../gps_compass/septentrio_asterx-rib.md)                                       |        AsteRx        | &check;  |                                  |      [Septentrio Dual Antenna][SeptDualAnt]       | &check; |
| [Septentrio mosaic-go](../gps_compass/septentrio_mosaic-go.md)                                            | mosaic X5 / mosaic H | &check;  |                                  |      [Septentrio Dual Antenna][SeptDualAnt]       | &check; |
| [SIRIUS RTK GNSS ROVER (F9P)](https://store-drotek.com/911-sirius-rtk-gnss-rover-f9p.html)                |         F9P          | &check;  |                                  |                [Dual F9P][DualF9P]                |         |
| [SparkFun GPS-RTK2 Board - ZED-F9P](https://www.sparkfun.com/products/15136)                              |         F9P          | &check;  |                                  |                [Dual F9P][DualF9P]                |         |
| [Trimble MB-Two](../gps_compass/rtk_gps_trimble_mb_two.md)                                                |         F9P          | &check;  |                                  |                      &check;                      |         |

<!-- links used in above table -->

Примітки:

- &check; або конкретний номер артикулу вказує на те, що функція підтримується, тоді як &cross; або пусте поле вказує на те, що функція не підтримується. "?" означає "невідомо".
- Там, де це можливо і доречно, використовується назва деталі (наприклад, &check; у колонці GPS вказує на наявність GPS-модуля, але деталь невідома).
- Деякі RTK-модулі можна використовувати лише в певній ролі (база або ровер), тоді як інші можна використовувати як взаємозамінні.
- У списку може бути відсутнє деяке зняте з виробництва обладнання, яке все ще підтримується. Наприклад, [CubePilot Here+ RTK GPS](../gps_compass/rtk_gps_hex_hereplus.md) більше не випускається і може бути вилучений зі списку у наступному релізі. Перевірте попередні версії, якщо тут не згадано модуль, який перестали випускати.

## Налаштування/Конфігурація розташування

Позиціонування RTK вимагає _пару_ [пристроїв RTK GNSS](#supported-devices): "базового" для земельної станції та "роувера" для транспортного засобу.

Крім того, вам знадобиться:

- _Ноутбук/ПК_ з QGroundControl (QGroundControl для Android/iOS не підтримує RTK)
- Транспортний засіб із WiFi або телеметричним радіозв'язком з ноутбуком.

:::info _QGroundControl_ with a base module can theoretically enable RTK GPS for multiple vehicles/rover modules. На момент написання цього випадку використання цей випадок не був протестований.
:::

### Налаштування обладнання

#### Модуль Rover RTK (Транспортний)

Спосіб підключення та необхідні кабелі/роз'єми залежать від вибраного модуля RTK (і від [контролера польоту](../flight_controller/index.md)).

Більшість з'єднані через порт GPS контролера польоту, так само, як будь-який інший модуль GPS. Деякі з них підключені до шини [CAN](../can/index.md) (тобто використовують [DroneCAN](../dronecan/index.md)).

See [documentation for the selected device](#supported-devices), general [GNSS Hardware/Configuration Setup](../gps_compass/index.md#hardware-setup), and [DroneCAN](../dronecan/index.md) for more information on wiring and configuration.

#### Базовий модуль RTK (наземний)

Підключіть базовий модуль до _QGroundControl_ за допомогою USB. Модуль бази не повинен зміщуватися, коли його використовують.

:::tip
Виберіть позицію, де базовий модуль не потрібно буде переміщувати, має чіткий вид на небо і добре відокремлений від будь-яких будівель.
Часто корисно підняти базовий GPS, використовуючи штатив або монтувавши його на дах.
:::

#### Телеметрійне радіо/WiFi

Автомобіль і ноутбук керування на землі повинні бути підключені через [Wi-Fi або радіозв'язок телеметрії](../telemetry/index.md).

Посилання _має_ використовувати протокол MAVLink 2, оскільки він більш ефективно використовує канал. Це повинно бути встановлено за замовчуванням, але якщо ні, слід дотримуватися [конфігураційні інструкції MAVLink2](#mavlink2) нижче.

### Процес підключення RTK

Підключення RTK GPS насправді просте:

1. Розпочніть виконання _QGroundControl_ та підключіть базовий RTK GPS через USB до наземної станції. Пристрій визнається автоматично.
1. Запустіть автомобіль і переконайтеся, що він підключений до _QGroundControl_.

:::tip
_QGroundControl_ показує значок статусу RTK GPS у верхній панелі значків, коли підключено пристрій RTK GPS (на додачу до звичайного значка статусу GPS). Іконка червона, поки налаштовується RTK, а потім змінюється на білу, коли RTK GPS активний. Ви можете натиснути на піктограму, щоб побачити поточний стан та точність RTK.
:::

1. _QGroundControl_ потім починає процес налаштування RTK (відомий як "Survey-In").

   Survey-In - це процедура запуску для отримання точної оцінки положення базової станції. Процес зазвичай триває кілька хвилин (він закінчується після досягнення мінімального часу та точності, вказаних у налаштуваннях [RTK](#rtk-gps-settings)).

   Ви можете відстежити прогрес, натиснувши на піктограму стану RTK GPS.

   ![survey-in](../../assets/qgc/setup/rtk/qgc_rtk_survey-in.png)

1. Після завершення опитування:

   - Іконка RTK GPS змінюється на білу, а _QGroundControl_ починає транслювати дані про позицію на транспортний засіб:

     ![RTK streaming](../../assets/qgc/setup/rtk/qgc_rtk_streaming.png)

   - Транспортний GPS переходить у режим RTK. Новий режим відображається у _звичайному_ піктограмі стану GPS (<0>звичайний</0> блокування GPS RTK 3D):

     ![RTK GPS Status](../../assets/qgc/setup/rtk/qgc_rtk_gps_status.png)

### Налаштування GPS як Джерело розділення/Курсування

GPS can be used as a source for yaw fusion when using a single device with two antenna where _yaw output is supported by the device_, or when using some [RTK GPS Setups with Dual u-blox F9P](../gps_compass/u-blox_f9p_heading.md). Using GPS as a heading source has the benefit that yaw calculations are not impacted by magnetic interference.

Both approaches work comparing the time taken for a GNSS signal to reach two separated antennas. The minimum distance between antenna depends on the device but is of the order of 50 cm (check manufacturer documentation).

The devices that can be used are listed in this way are listed in the **GPS Yaw** column of the table above, such as [Septentrio AsteRx-m3 Pro](../gps_compass/septentrio_asterx-rib.md), [Holybro H-RTK Unicore UM982 GPS](../gps_compass/rtk_gps_holybro_unicore_um982.md), and [Trimble MB-Two](../gps_compass/rtk_gps_trimble_mb_two.md). The links in the table take you to the device-specific PX4 configuration.

Generally when using a GNSS as a source of yaw information you will need to configure the following parameters:

| Параметр                           | Налаштування                                                                                                                                                |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [GPS_YAW_OFFSET][GPS_YAW_OFFSET] | The angle made by the _baseline_ (the line between the two GPS antennas) relative to the vehicle x-axis (front/back axis, as shown [here][fc_orientation]). |
| [EKF2_GPS_CTRL][EKF2_GPS_CTRL]   | Встановіть бітову позицію 3 "Напрямок подвійної антени" на `1` (тобто додайте 8 до значення параметра).                                                     |

<!-- links used in table above -->

:::tip
Якщо ви використовуєте цю функцію, всі інші конфігурації мають бути налаштовані стандартно (наприклад, [RTK Positioning](../gps_compass/rtk_gps.md#positioning-setup-configuration)).
:::

### Додаткова конфігурація PX4

Можливо, знадобиться змінити наступні налаштування (використовуючи _QGroundControl_).

#### Налаштування RTK GPS

Налаштування RTK GPS вказано у _QGroundControl_ [Загальних налаштуваннях](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/settings_view/general.html#rtk_gps) (**SettingsView > Загальні налаштування > Налаштування RTK GPS**).

![RTK GPS Setup](../../assets/qgc/setup/rtk/settings_view_general_rtk_gps.jpg)

Ці параметри визначають мінімальну тривалість та мінімальну точність для завершення процесу налаштування RTK GPS (відомий як "Survey-In).

:::tip
Можна зберегти й повторно використовувати базове положення, щоб заощадити час: виконайте Вимірювання-In один раз, виберіть _Використовувати Вказану Базову Позицію_ та натисніть **Зберегти Поточне Базове Положення**, щоб скопіювати значення для останнього вимірювання. Значення будуть збережені після перезавантажень QGC до тих пір, поки їх не змінять.
:::

#### MAVLink2

Протокол MAVLink2 повинен бути використаний, оскільки він ефективніше використовує канали з низькою пропускною здатністю. Це має бути увімкнено за замовчуванням на останніх збірках.

Для забезпечення використання MAVLink2:

- Оновіть прошивку модуля телеметрії до останньої версії (див. [QGroundControl > Налаштування > Прошивка](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/firmware.html)).
- Встановіть [MAV_PROTO_VER](../advanced_config/parameter_reference.md#MAV_PROTO_VER) на 2 (див. [QGroundControl Налаштування > Параметри](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/setup_view/parameters.html))

#### Налаштування

Вам може додатково знадобитися налаштувати деякі параметри, оскільки параметри за замовчуванням налаштовані з припущенням точності GPS в порядку метрів, а не сантиметрів. Наприклад, ви можете зменшити [EKF2_GPS_V_NOISE](../advanced_config/parameter_reference.md#EKF2_GPS_V_NOISE) та [EKF2_GPS_P_NOISE](../advanced_config/parameter_reference.md#EKF2_GPS_P_NOISE) на 0.2.

#### Подвійні приймачі

Другий приймач GPS може бути використаний як резервний (RTK або не RTK). Дивіться розділ [Конфігурація GPS EKF2](../advanced_config/tuning_the_ecl_ekf.md#gps).

<!--
- Video demonstration would be nice.
- something that shows positioning of base, connection of RTK rover, survey in process. Some sort of short precision survey.
-->

## Додаткова інформація

- [RTK-GPS (Інтеграція PX4)](../advanced/rtk_gps.md): Інформація розробника про інтеграцію підтримки RTK-GPS до PX4.
- [Реально-часова кінематика](https://en.wikipedia.org/wiki/Real_Time_Kinematic) (Wikipedia)

[RaccnLabL1L2ZED-F9P ext_ant]: https://docs.raccoonlab.co/guide/gps_mag_baro/gnss_external_antenna_f9p_v320.html
[RaccoonLab L1/L2 ZED-F9P]: https://docs.raccoonlab.co/guide/gps_mag_baro/gps_l1_l2_zed_f9p.html
[DualF9P]: ../gps_compass/u-blox_f9p_heading.md
[SeptDualAnt]: ../gps_compass/septentrio.md#gnss-based-heading
[UnicoreDualAnt]: ../gps_compass/rtk_gps_holybro_unicore_um982.md#enable-gps-heading-yaw
[DATAGNSS GEM1305 RTK]: ../gps_compass/rtk_gps_gem1305.md

[GPS_YAW_OFFSET]: ../advanced_config/parameter_reference.md#GPS_YAW_OFFSET
[EKF2_GPS_CTRL]: ../advanced_config/parameter_reference.md#EKF2_GPS_CTRL
[fc_orientation]: ../config/flight_controller_orientation.md#calculating-orientation
