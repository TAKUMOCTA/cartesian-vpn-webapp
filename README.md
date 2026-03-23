# cartesian-vpn-webapp
The Internet Accelerator
# 🌐 Cartesian VPN — Telegram Mini App

![Cartesian VPN](https://img.shields.io/badge/Cartesian-VPN-blue?style=for-the-badge&logo=telegram)
![Status](https://img.shields.io/badge/status-beta-yellow?style=flat-square)

> **Cartesian VPN** — это Telegram Mini App (Web App) для управления VPN-сервисом. Приложение позволяет подключаться к VPN-серверам по всему миру, выбирать тарифы, отслеживать трафик и пользоваться офлайн-режимом.

---

## 📱 О проекте

Cartesian VPN — это удобный интерфейс внутри Telegram, который позволяет:

- 🔐 **Подключаться к VPN** одним нажатием
- 🌍 **Выбирать серверы** из 18 стран с разбивкой по городам
- 📊 **Отслеживать трафик** (остаток ГБ)
- 💎 **Оформлять подписки** (Free / Premium / Prime)
- 📡 **Использовать офлайн-режим** при отсутствии интернета
- 🎮 **Подключаться к игровым серверам** и **белым спискам** (для пользователей из России)

---

## 🚀 Функционал

### 🔌 Подключение к VPN
- Выбор сервера из 46+ локаций
- Отображение статуса подключения
- Автоматический подсчёт использованного трафика

### 💎 Тарифы и лимиты

| Тариф | Цена | Лимит | Доступные серверы | Особенности |
|-------|------|-------|-------------------|-------------|
| **Free** | 0 ₽ | 50 ГБ | 5 стран (Россия, США, Нидерланды, Казахстан, Чехия) | Базовая скорость |
| **Premium** | 299 ₽/мес | 100 ГБ | Страны Азии + Франция + Игровые серверы | Высокая скорость, игровые серверы |
| **Prime** | 1 990 ₽/год | 200 ГБ | Все страны + Все игровые + Белые списки | Максимальная скорость, экономия 45% |

### 📡 Офлайн-режим
При полном отсутствии интернета:
- Доступны серверы: 🇷🇺 Россия (Москва), 🇺🇸 США (Нью-Йорк), 🇳🇱 Нидерланды (Амстердам)
- Время работы: **1.5 часа**
- Автоматическое отключение по истечении времени

### 🌍 Доступные серверы

<details>
<summary><b>🇷🇺 Россия</b></summary>

- Москва (Free)
- Москва (Белые списки — Prime)
</details>

<details>
<summary><b>🇺🇸 США</b></summary>

- Нью-Йорк (Free)
- Атланта (Free)
- Чикаго (Prime)
- Нью-Джерси (Prime)
</details>

<details>
<summary><b>🇳🇱 Нидерланды</b></summary>

- Амстердам (Free)
- Роттердам (Prime)
- Гаага (Prime)
</details>

<details>
<summary><b>🇩🇪 Германия</b></summary>

- Берлин (Premium)
- Гамбург (Prime)
- Франкфурт-на-Майне (Prime)
</details>

<details>
<summary><b>🇸🇬 Сингапур</b></summary>

- Сингапур (Premium)
</details>

<details>
<summary><b>🇨🇦 Канада</b></summary>

- Торонто, Монреаль, Оттава (Prime)
</details>

<details>
<summary><b>🇬🇧 Великобритания</b></summary>

- Лондон (Prime)
</details>

<details>
<summary><b>🇫🇷 Франция</b></summary>

- Париж (Premium)
- Арль, Руан (Prime)
</details>

<details>
<summary><b>🇳🇴 Норвегия</b></summary>

- Осло, Берген (Prime)
</details>

<details>
<summary><b>🇯🇵 Япония</b></summary>

- Токио (Premium)
- Фукуока, Киото (Prime)
</details>

<details>
<summary><b>🇨🇳 Китай</b></summary>

- Пекин (Premium)
- Шанхай (Prime)
</details>

<details>
<summary><b>🇭🇰 Гонконг</b></summary>

- Гонконг (Premium)
</details>

<details>
<summary><b>🇰🇷 Южная Корея</b></summary>

- Сеул (Premium)
- Пусан (Prime)
</details>

<details>
<summary><b>🇰🇿 Казахстан</b></summary>

- Астана (Free)
</details>

<details>
<summary><b>🇹🇷 Турция</b></summary>

- Стамбул (Prime)
</details>

<details>
<summary><b>🇨🇿 Чехия</b></summary>

- Прага (Free)
</details>

<details>
<summary><b>🇵🇱 Польша</b></summary>

- Варшава (Prime)
</details>

<details>
<summary><b>🇵🇭 Филиппины</b></summary>

- Манила (Prime)
</details>

<details>
<summary><b>🎮 Игровые серверы</b></summary>

- Россия (Premium)
- Европа (Premium)
- США (Premium)
- Азия (Prime)
</details>

<details>
<summary><b>✅ Белые списки</b></summary>

- Россия (Prime)
- США (Prime)
- Европа (Prime)
</details>

---

## 🛠️ Технологии

- **HTML5** — структура приложения
- **CSS3** — адаптивный дизайн с поддержкой тем Telegram
- **JavaScript (ES6)** — логика приложения
- **Telegram Web App API** — интеграция с Telegram

---

## 📦 Установка и запуск

### 1. Клонирование репозитория
```bash
git clone https://github.com/ваш-username/cartesian-vpn-webapp.git
cd cartesian-vpn-webapp
