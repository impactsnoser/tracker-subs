# Renewly — трекер подписок (SwiftUI + SwiftData)

iOS 17+ приложение для учёта подписок с брендовыми иконками популярных сервисов в РФ.

> ⚠️ Сборка распространяется **unsigned IPA** через GitHub Actions. Официального релиза в App Store нет — установка идёт через **SideStore** (временное решение, без джейлбрейка).

---

## 📲 Установка через SideStore

Ниже — полный путь от нуля до запущенного приложения на iPhone. Все ссылки кликабельны.

### Шаг 1. Установи SideStore на iPhone

SideStore ставится один раз с компьютера (Mac, Windows или Linux) — дальше телефон сможет обновлять сертификат сам, без ПК.

1. Открой официальную инструкцию: **[sidestore.io/#get-started](https://sidestore.io/#get-started)**
2. Установи спутник **[AltServer](https://altstore.io/)** (или **[SideStore AltServer-Linux](https://github.com/SideStore/AltServer-Linux)**, если у тебя Linux) на компьютер и подключи iPhone кабелем.
3. Через AltServer установи саму **SideStore** на телефон (пункт *Install SideStore* в меню AltServer).
4. На телефоне зайди в **Настройки → Основные → VPN и управление устройством** и подтверди доверие профилю разработчика SideStore.
5. Установи из App Store приложение **[WireGuard](https://apps.apple.com/app/wireguard/id1441195209)** — оно нужно SideStore для фонового обновления подписи.
6. Открой SideStore на телефоне, войди с Apple ID (подойдёт обычный бесплатный аккаунт) и нажми **Refresh**, чтобы убедиться, что всё работает.

Подробный разбор со скриншотами и Discord-поддержка есть на той же странице: **[sidestore.io](https://sidestore.io/)**.

### Шаг 2. Скачай IPA-файл Renewly

1. Открой вкладку **[Actions в репозитории](https://github.com/impactsnoser/tracker-subs/actions/workflows/build-ipa.yml)**.
2. Выбери самый свежий успешный запуск (зелёная галочка) workflow **Build IPA**.
3. В самом низу страницы запуска найди раздел **Artifacts** и скачай архив вида `Subscriptions-ipa-<commit>.zip` **прямо на iPhone** (через Safari — так файл сразу попадёт в «Файлы», и его будет проще выбрать в SideStore).
4. Распакуй архив (Safari/Файлы сделают это автоматически или через приложение «Файлы» → долгий тап → «Извлечь»). Внутри будет `Subscriptions-unsigned.ipa`.

Если хочешь собрать IPA сам — можно запустить workflow вручную: **[Run workflow →](https://github.com/impactsnoser/tracker-subs/actions/workflows/build-ipa.yml)** (кнопка *Run workflow* справа сверху).

### Шаг 3. Установи IPA через SideStore

1. Открой **SideStore** → вкладка **My Apps**.
2. Нажми **+** в левом верхнем углу.
3. Выбери файл `Subscriptions-unsigned.ipa` (в «Недавние»/«Файлы»).
4. Дождись, пока SideStore подпишет и установит приложение — иконка **Renewly** появится на главном экране.

### Шаг 4. Не забывай обновлять подпись

Бесплатный Apple ID подписывает приложения на **7 дней**. Раз в неделю:

- Открой SideStore → **Apps** → **Renewly** → **Refresh** (или включи автообновление по расписанию в настройках SideStore — оно работает в фоне через WireGuard, без компьютера).

Если сертификат всё же истёк и приложение отказывается открываться — просто повтори Шаг 3 с тем же или новым IPA.

---

## 🛠 Частые проблемы

| Проблема | Решение |
|---|---|
| SideStore пишет `AFC was unable to manage files` | Проверь, что Wi-Fi и `LocalDevVPN`/WireGuard включены, затем повтори Refresh |
| Приложение не открывается, «Untrusted Developer» | Настройки → Основные → VPN и управление устройством → довериться профилю |
| IPA не устанавливается из SideStore | Убедись, что скачал файл именно на iPhone, а не на компьютер |
| Публичный Anisette-сервер блокирует Apple ID | В настройках SideStore смени Anisette-сервер на другой или подними свой |

---

## Локальная разработка (Mac)

```bash
brew install xcodegen
xcodegen generate
open Subscriptions.xcodeproj
```

## Структура проекта

| Файл | Назначение |
|------|------------|
| `SubscriptionApp.swift` | Точка входа |
| `ContentView.swift` | Главный экран, списки, группировка |
| `SubscriptionModel.swift` | SwiftData модель |
| `SubscriptionBrand.swift` | Сопоставление названий и брендов |
| `BrandArtwork.swift` | Отрисовка логотипов |
| `project.yml` | Конфиг XcodeGen для CI |

## Заливка на GitHub (PowerShell)

Установлены Git и GitHub CLI. В терминале:

```powershell
gh auth login
.\scripts\push-to-github.ps1
```

Или вручную после `gh auth login`:

```powershell
gh repo create tracker-subs --public --source=. --remote=origin --push
```
