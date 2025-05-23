# Asus X99 A-II ReBAR
[**English**](/README.md) | [**Русский**](./docs/ru/README.ru.md)

Проверенный способ активации ReBAR (Resizable BAR) на ASUS X99 A-II.

# Предыстория гайда
Упрощенный и безопасный способ через `ASUS Flashback`, давал у меня, сдедующую реакцию **(удержание 3-сек, отпустить, три-мигания, постоянное свечение)**, что означает, что он отвергает файл прошивки, и отказывается его прошивать из-за сигнатуры.

В этом гайде я буду рассматривать менее безопасный способ через оболочку `FreeDOS`, что обходит этот метод защиты, и успешно прошивает прошивку даже с измененной защитной сигнатурой.

# Исходники
Этот гайд является упрощенной (до одного метода) и структурированной версией этого гайда:
- https://github.com/Mak3rde/AsusX99A-II-RezisableBar (by @Mak3rde)

xCuri0 / ReBarUEFI
- https://github.com/xCuri0/ReBarUEFI

terminatorul / NvStrapsReBar
- https://github.com/terminatorul/NvStrapsReBar

# Прошивка
> [!CAUTION]
> Только если у вас нет собственных модификаций BIOS (иначе, что вы забыли тут?)
## 1. Подготовка
- Загрузите файл `X99-A-II-ASUS-2101_ROM_STOCKROM` из [основного гайда](https://github.com/Mak3rde/AsusX99A-II-RezisableBar) из секции `ready to use efi Downloads`.
- Загрузите [AFUDOS](https://disk.yandex.ru/d/lW3H05ggRWaGiA), может быть удалена из-за жалоб правообладателей (искать в интернете).
- Подготовьте флешку и отформатируйте её при помощи [Rufus](https://rufus.ie/en/) в вид `FreeDOS` формат FAT 32 MBR.
- После подгтовки, перекиньте все файлы из архива `AFUDOS` на флешку в корневую папку.
- Перекиньте файл прошивки `.rom` из архива `X99-A-II-ASUS-2101_ROM_STOCKROM` на флешку в корневую папку.
- Переименуйте его в `bios.rom` для упрощения работы с ним в среде DOS.
- Выключите компьютер, (опционально: включите CSM в настройках BIOS) загрузитесь с флешки с FreeDOS.
## 2. FreeDOS
- Выберите **Английскую раскладку клавиатуры** после запуска FreeDOS
![FreeDOS Language](http://xeonlive.ru/images/materials/instructions/afudos/3.jpg)
- Сделайте бекап текущей прошивки (на всякий случай):
```
afudos backup.rom /o
```
- Ожидайте завершение процесса, по окончанию у вас появиться файл `backup.rom`
- Теперь, прошиваем наш новый биос командой:
```
afudos bios.rom /gan
``` 
- Ожидаете завершение процесса прошивки.
- По окончанию прошивки, перезагружайтесь в BIOS и вынимайте флешку.
## 3. BIOS
Все настройки сбросились до стандартных, так и должно быть.
- Зайдите в раздел `Boot` и включите `Above 4G Decoding` (установите положение `Enabled`) для работы ReBAR.
- Перейдите в раздел `CSM` и установите значение `Disabled` для работы ReBAR.
- Если вам нужно восстановить еще какие-то настройки, то восстановите их.
- Сохраняем изменения и загружаемся в `Windows`.
## 4. Windows
На видеокартах NVIDIA всё еще будет отображаться, что ReBAR не включен в BIOS, для этого:
#### Если у вас видеокарта NVIDIA RTX 30-й серии (или новее), используйте `ReBarState.exe`
- Загрузите к себе на компьютер программу  `ReBarState.exe` из релизов [ReBAR UEFI](https://github.com/xCuri0/ReBarUEFI/releases).
- Запускаем программу и вводим значение `32` (неограниченный размер Bar) и нажимаем `Enter`.
- Если никаких ошибок не выдало, перезагружаем компьютер.
#### Если у вас видеокарта NVIDIA Turing (20-й или 16-й серии), используйте `NvStrapsReBar.exe`
- Загружаем к себе на компьютер программу `NvStrapsReBar.exe` из релизов [NvStrapsReBar](https://github.com/terminatorul/NvStrapsReBar/releases/tag/v0.3).
- Запускаем программу, ожидаем отображения всей информации.
- Находим цифру напротив модели вашего GPU и вбиваем её и нажимаем `Enter`.
- Если всё успешно, и не было ошибок, перезагружаем компьютер.

В обоих случаях, теперь у вас должен работать ReBAR для всех GPU (AMD / NVIDIA) которые его поддерживают.
> [!NOTE] 
> **NVIDIA**: серия Geforce GTX 16XX, RTX 20XX, RTX 30XX и выше. <br>
> **AMD**: серия RX 6000 и выше.
- Вы можете проверить это при помощи `GPU-Z` запустив и нажав на **Resizable BAR** элемент.
> В GPU-Z во вкладке Advanced → Bus Interface должно отображаться:
"Resizable BAR: Enabled" (а не "Disabled" или "Not Supported")
- При помощи NVIDIA Control Panel (для NVIDIA) нажав на `Информация о системе` - **Resizable BAR**.
> Если ReBAR активен, в строке "Resizable BAR" будет значение "Да".

![GPU-Z Nvidia ReBAR](https://github.com/DenisSolicen/Asus-X99-A-II-ReBAR/blob/main/img/gpuz.png?raw=true)
![Nvidia Control Panel](https://github.com/DenisSolicen/Asus-X99-A-II-ReBAR/blob/main/img/nvidiacontrol.png?raw=true)

*Поздравляю, теперь у вас стабильно работает ReBAR на той плате, что изначально не имела его поддержки!*
- Если гайд был полезен, прошу вас поставить *звезду репозиторию (тыкнуть на звезду `Star` справа сверху)*.
- Сделайте тоже самое с [изначальным гайдом](https://github.com/Mak3rde/AsusX99A-II-RezisableBar), без него, этого бы гайда не было, спасибо!
