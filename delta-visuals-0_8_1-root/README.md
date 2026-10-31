# DeltaVisuals 0.8.0

**RU** · [English below](#english)

Клиентский визуальный мод для Minecraft Java Edition на Fabric. Только отрисовка, звук и интерфейс: без автоматических атак, увеличения дальности,
изменения урона и других преимуществ. **Частицы Minecraft не используются**: все эффекты нарисованы цельной геометрией через собственные `RenderPipeline` / `RenderLayer`,
текстуры генерируются кодом.

## Совместимость

| | |
|---|---|
| Minecraft | 1.21.11 (Java Edition) |
| Fabric Loader | 0.18.4 и новее |
| Fabric API | 0.141.1+1.21.11 и новее для 1.21.11 |
| Java | 21 |
| Сторона | только клиент |

## Функции

* **Target ESP**: 8 режимов (Arcs, Petals, Rings, Mechanical, Lightning, Saturn, Ghosts, Helix), цвет Static / Gradient / Rainbow / Health / Fire / Neon, свечение, «сквозь стены».
* **Trails / Blink**: лента за игроком, сглаживание, сужение и затухание к хвосту; режимы Vertical, Horizontal, Spiral, Wave; настройки ширины и длины.
* **Kill Effect**: Decay, Singularity, Abyss.
* **Hit Effects**: звёзды, черепа, сердца, осколки кристалла, молнии, ударная волна; усиленный вариант при убийстве.
* **Damage Indicators**, **Block Overlay**.
* **Custom Sky**: сгенерированное небо (Space, Stormy Sunset, Pink Sunset, Clear Day, Aurora, Black Hole, Sunset Sky, Night Sky, Fantasy Sky, Custom Sky, Gradient Sky, Custom Color Sky), цвета, градиент, облака, звёзды, интенсивность; модуль **Sky Preset Switch** с отдельным хоткеем.
* **Hit Sounds** (категория Combat Visuals): Minecraft Bell, Hit Sound 1–4, собственный звук `config/delta_visuals/sounds/custom.wav`; громкость, высота, задержка, кнопка Play Sound; звук только при удачном ударе.
* **Item Position**: положение, поворот и масштаб предмета в руках отдельно для правой и левой руки и для типов предметов; 23 пресета.
* **HUD**: Info, Armor, Watermark, редактор HUD.
* **Меню** (Right Shift): у каждой функции переключатель, хоткей и настройки; темы; профили; ключи для обмена настройками (Copy Share Key / Load Key From Clipboard).
* **Конфигурация**: JSON-профили в `.minecraft/config/delta_visuals/profiles/`.

## Что нового в 0.8.0

* **Меч не улетает при ударе.** Положение предмета теперь применяется после ванильной анимации замаха, поэтому замах остаётся ванильным. У Item Position безопасные пределы (позиция ±0.7 / −0.6…0.6 / −0.8…0.5, поворот ±90 / ±110 / ±90°, масштаб 0.3–1.6), так что предмет не уходит за экран.
* **Новый интерфейс.** Мягкая тень и тонкая светлая рамка меню, скруглённые углы 12 px, полупрозрачные панели, логотип-кристалл в шапке, аккуратные HUD-панели с акцентной полосой.
* **Язык English / Русский** (Тема → Язык), переключается сразу без перезапуска. Тексты лежат в `assets/delta_visuals/lang/en_us.json` и `ru_ru.json` (ключ = английский текст).
* **Шрифт интерфейса** Carlito (SIL OFL 1.1, поддерживает кириллицу) через font provider: `assets/delta_visuals/font/ui.json` + `carlito-regular.ttf`. Если файла нет или глиф отсутствует, подставляется стандартный шрифт Minecraft. Переключатель: Тема → UI Font. Чтобы взять другой шрифт (например Inter или Roboto), положите TTF в ту же папку и замените имя файла в `ui.json`.
* **Иконка** мода и логотип в меню.
* **Косметика** (категория Cosmetics → модуль Cosmetics): плащ (Classic, Royal, Galaxy, Flame, Frost), крылья (Angel, Dragon, Crystal, Butterfly), шапка (Top Hat, Wizard Hat, Crown, Halo, Cat Ears). Каждый элемент включается отдельно, есть размер, прозрачность и свои цвета. Модели целиком из геометрии, без текстур; видны только вам.

## Что изменилось в 0.7.0

Отдельной версии 6.5 в проекте нет: последняя собранная мной версия это 0.7.0 (до неё была 0.6.0).

* Добавлены Custom Sky, Sky Preset Switch, Hit Sounds (новая категория Combat Visuals) и Item Position.
* В меню: заголовки групп, выбор из списка «чипами» для настроек с большим числом вариантов.
* Миксин `HeldItemRendererMixin` для Item Position (конфиг `delta_visuals.mixins.json`, `required: false`).
* В 0.6.0 были добавлены Hit Effects и более тонкие и короткие Trails (по умолчанию ширина 0.3, длина 12 тиков).

Известные ограничения: туман местности остаётся ванильным (у края дальности прорисовки возможна полоса цвета тумана); пока включён Custom Sky, ванильные облака скрываются видеонастройкой и возвращаются при выключении неба или выходе из игры.

## Установка

1. Установите Fabric Loader для Minecraft 1.21.11 (https://fabricmc.net/use/) и Fabric API.
2. Скопируйте `delta-visuals-0.8.0.jar` в папку модов: `%appdata%\.minecraft\mods` (Windows), `~/Library/Application Support/minecraft/mods` (macOS), `~/.minecraft/mods` (Linux).
3. Запустите игру профилем Fabric 1.21.11 и нажмите **Right Shift**.

## Сборка из исходников

1. Установите JDK 21.
2. В корне проекта выполните: Windows `gradlew.bat build`, macOS / Linux `./gradlew build` (на macOS / Linux один раз `chmod +x gradlew`).
3. Готовый мод: `build/libs/delta-visuals-0.8.0.jar` (файлы `-sources` и `-dev` не нужны).
4. Если в проекте нет `gradle/wrapper/gradle-wrapper.jar`, один раз выполните `gradle wrapper --gradle-version 9.2.0` (нужен установленный Gradle).

Сборка на GitHub: workflow **build** запускается при каждом push; jar лежит в Actions → запуск → Artifacts → `delta-visuals-jar`.
Релиз: тег `v0.8.0` (`git tag v0.8.0 && git push origin v0.8.0`) запускает workflow **release**, который прикладывает jar к GitHub Release.

## Благодарности и лицензия

Благодарность автору(ам) оригинального Delta Visuals за идею и вдохновение. Имя автора укажите здесь сами: в проекте оно нигде не записано.
Код этого проекта написан заново; текстуры и ресурсы чужих пакетов не копировались.

Лицензия: **All Rights Reserved** (как указано в `fabric.mod.json`). Если хотите открытую лицензию (например MIT), замените значение `license` в `src/main/resources/fabric.mod.json` и добавьте файл `LICENSE`.

---

## English

<a id="english"></a>

A client-side visual mod for Minecraft Java Edition (Fabric). Rendering, sound and UI only: no auto-attack, no extra reach, no damage changes, no gameplay advantages.
**No Minecraft particles are used**: every effect is solid geometry drawn through the mod's own `RenderPipeline` / `RenderLayer`, and all visuals are generated in code (no borrowed textures).

## Compatibility

| | |
|---|---|
| Minecraft | 1.21.11 (Java Edition) |
| Fabric Loader | 0.18.4 or newer |
| Fabric API | 0.141.1+1.21.11 or newer for 1.21.11 |
| Java | 21 |
| Side | client only |

## Features

* **Target ESP**: 8 modes (Arcs, Petals, Rings, Mechanical, Lightning, Saturn, Ghosts, Helix), Static / Gradient / Rainbow / Health / Fire / Neon colours, glow, see-through-walls.
* **Trails / Blink**: ribbon behind the player with smoothing, taper and alpha fade; Vertical, Horizontal, Spiral and Wave modes; width and length settings.
* **Kill Effect**: Decay, Singularity, Abyss.
* **Hit Effects**: stars, skulls, hearts, crystal shards, lightning, shockwave; a bigger variant on kills.
* **Damage Indicators**, **Block Overlay**.
* **Custom Sky**: generated sky (Space, Stormy Sunset, Pink Sunset, Clear Day, Aurora, Black Hole, Sunset Sky, Night Sky, Fantasy Sky, Custom Sky, Gradient Sky, Custom Color Sky), colours, gradient, clouds, stars, intensity; **Sky Preset Switch** module with its own hotkey.
* **Hit Sounds** (Combat Visuals): Minecraft Bell, Hit Sound 1-4, your own `config/delta_visuals/sounds/custom.wav`; volume, pitch, delay, Play Sound button; plays only when a hit really lands.
* **Item Position**: position, rotation and scale of the held item, separately for each hand and item type; 23 presets.
* **HUD**: Info, Armor, Watermark, HUD editor.
* **Menu** (Right Shift): every feature has a toggle, a hotkey and settings; themes; profiles; share keys (Copy Share Key / Load Key From Clipboard).
* **Config**: JSON profiles in `.minecraft/config/delta_visuals/profiles/`.

## What's new in 0.8.0

* **The sword no longer flies away on a hit.** The item transform is now applied after the vanilla swing animation, so the swing stays vanilla. Item Position has safe limits (position +-0.7 / -0.6..0.6 / -0.8..0.5, rotation +-90 / +-110 / +-90 deg, scale 0.3-1.6), so the item stays on screen.
* **New interface.** Soft shadow and a thin light border for the menu, 12 px rounded corners, translucent panels, crystal logo in the header, tidy HUD panels with an accent bar.
* **English / Russian language** (Theme -> Language), applied instantly. Texts are in `assets/delta_visuals/lang/en_us.json` and `ru_ru.json` (the key is the English text).
* **Interface font** Carlito (SIL OFL 1.1, Cyrillic) through a font provider: `assets/delta_visuals/font/ui.json` + `carlito-regular.ttf`. If the file or a glyph is missing, the vanilla Minecraft font is used. Toggle: Theme -> UI Font. To use another font (Inter, Roboto...), put the TTF in the same folder and change the file name in `ui.json`.
* **Icon** of the mod and a logo in the menu.
* **Cosmetics** (category Cosmetics -> module Cosmetics): cape (Classic, Royal, Galaxy, Flame, Frost), wings (Angel, Dragon, Crystal, Butterfly), hat (Top Hat, Wizard Hat, Crown, Halo, Cat Ears). Each one has its own toggle, size, opacity and custom colours. Models are pure geometry, no textures; visible only to you.

## What changed in 0.7.0

There is no version 6.5 in this project: the latest version I built is 0.7.0 (0.6.0 came before it).

* Added Custom Sky, Sky Preset Switch, Hit Sounds (new Combat Visuals category) and Item Position.
* Menu: group headers and chip-style pickers for settings with many options.
* `HeldItemRendererMixin` for Item Position (`delta_visuals.mixins.json`, `required: false`).
* 0.6.0 added Hit Effects and thinner, shorter Trails (default width 0.3, length 12 ticks).

Known limits: terrain fog stays vanilla (a band of fog colour may show at the render-distance edge); while Custom Sky is on, vanilla clouds are hidden through the video option and restored when the sky is turned off or the game exits.

## Installation

1. Install Fabric Loader for Minecraft 1.21.11 (https://fabricmc.net/use/) and Fabric API.
2. Copy `delta-visuals-0.8.0.jar` into the mods folder: `%appdata%\.minecraft\mods` (Windows), `~/Library/Application Support/minecraft/mods` (macOS), `~/.minecraft/mods` (Linux).
3. Launch the Fabric 1.21.11 profile and press **Right Shift**.

## Building from source

1. Install JDK 21.
2. In the project root run: Windows `gradlew.bat build`, macOS / Linux `./gradlew build` (run `chmod +x gradlew` once on macOS / Linux).
3. The mod is `build/libs/delta-visuals-0.8.0.jar` (ignore the `-sources` and `-dev` files).
4. If `gradle/wrapper/gradle-wrapper.jar` is missing, run `gradle wrapper --gradle-version 9.2.0` once (needs Gradle installed).

On GitHub: the **build** workflow runs on every push; the jar is under Actions -> run -> Artifacts -> `delta-visuals-jar`.
Release: pushing the tag `v0.8.0` (`git tag v0.8.0 && git push origin v0.8.0`) runs the **release** workflow, which attaches the jar to a GitHub Release.

## Credits and license

Thanks to the author(s) of the original Delta Visuals for the idea and inspiration. Add the author's name here yourself: it is not recorded anywhere in the project.
The code of this project was written from scratch; no textures or assets from other packs were copied.

License: **All Rights Reserved** (as set in `fabric.mod.json`). For an open license (for example MIT), change `license` in `src/main/resources/fabric.mod.json` and add a `LICENSE` file.
