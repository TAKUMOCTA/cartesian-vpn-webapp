<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
    <title>Cartesian VPN</title>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: var(--tg-theme-bg-color, #0a0a0f);
            color: var(--tg-theme-text-color, #ffffff);
            padding: 16px;
            min-height: 100vh;
        }

        .container {
            max-width: 500px;
            margin: 0 auto;
            padding-bottom: 30px;
        }

        /* Language Selector */
        .lang-selector {
            position: fixed;
            top: 10px;
            right: 10px;
            z-index: 1000;
            background: var(--tg-theme-secondary-bg-color, #1f1f2a);
            border-radius: 40px;
            padding: 6px 12px;
            font-size: 12px;
            border: none;
            color: var(--tg-theme-text-color, #ffffff);
            cursor: pointer;
            font-weight: 500;
            backdrop-filter: blur(10px);
        }

        .lang-selector option {
            background: var(--tg-theme-bg-color, #0a0a0f);
        }

        /* Header */
        .header {
            text-align: center;
            padding: 20px 0 24px;
            margin-top: 30px;
        }

        .logo {
            font-size: 36px;
            font-weight: 800;
            background: linear-gradient(135deg, #3b82f6, #a855f7, #ec489a);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 8px;
            letter-spacing: -0.5px;
        }

        .subtitle {
            font-size: 13px;
            color: var(--tg-theme-hint-color, #6b7280);
        }

        /* Connection Status Card */
        .status-card {
            background: linear-gradient(135deg, rgba(59,130,246,0.1), rgba(168,85,247,0.1));
            border-radius: 24px;
            padding: 20px;
            margin-bottom: 20px;
            text-align: center;
            border: 1px solid rgba(59,130,246,0.2);
            backdrop-filter: blur(10px);
        }

        .status-icon {
            font-size: 48px;
            margin-bottom: 12px;
        }

        .status-text {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 6px;
        }

        .status-subtext {
            font-size: 13px;
            color: var(--tg-theme-hint-color, #9ca3af);
        }

        .timer {
            margin-top: 12px;
            padding: 8px 16px;
            background: rgba(0,0,0,0.3);
            border-radius: 40px;
            display: inline-block;
            font-size: 14px;
            font-weight: 600;
            color: #f59e0b;
        }

        /* Stats Row */
        .stats-row {
            display: flex;
            gap: 12px;
            margin-bottom: 24px;
        }

        .stat-card {
            flex: 1;
            background: var(--tg-theme-secondary-bg-color, #1f1f2a);
            border-radius: 16px;
            padding: 12px;
            text-align: center;
        }

        .stat-value {
            font-size: 24px;
            font-weight: 700;
            color: #3b82f6;
        }

        .stat-label {
            font-size: 11px;
            color: var(--tg-theme-hint-color, #9ca3af);
            margin-top: 4px;
        }

        /* Tab Bar */
        .tab-bar {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            background: var(--tg-theme-secondary-bg-color, #1f1f2a);
            padding: 4px;
            border-radius: 60px;
        }

        .tab {
            flex: 1;
            text-align: center;
            padding: 10px;
            border-radius: 40px;
            font-weight: 600;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
            color: var(--tg-theme-hint-color, #9ca3af);
        }

        .tab.active {
            background: var(--tg-theme-button-color, #3b82f6);
            color: white;
        }

        /* Server Grid */
        .servers-grid {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-bottom: 24px;
            max-height: 450px;
            overflow-y: auto;
        }

        .server-card {
            background: var(--tg-theme-secondary-bg-color, #1f1f2a);
            border-radius: 16px;
            padding: 14px 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: pointer;
            transition: all 0.2s;
            border: 2px solid transparent;
        }

        .server-card.selected {
            border-color: #3b82f6;
            background: rgba(59,130,246,0.1);
        }

        .server-info {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
        }

        .server-flag {
            font-size: 28px;
            width: 44px;
            text-align: center;
        }

        .server-details {
            flex: 1;
        }

        .server-name {
            font-weight: 700;
            margin-bottom: 4px;
            font-size: 15px;
        }

        .server-locations {
            font-size: 10px;
            color: var(--tg-theme-hint-color, #9ca3af);
        }

        .server-badge {
            font-size: 11px;
            padding: 4px 10px;
            border-radius: 20px;
            background: rgba(59,130,246,0.2);
            color: #3b82f6;
            white-space: nowrap;
        }

        .server-badge.locked {
            background: rgba(239,68,68,0.2);
            color: #ef4444;
        }

        .server-badge.premium {
            background: rgba(245,158,11,0.2);
            color: #f59e0b;
        }

        .server-badge.prime {
            background: linear-gradient(135deg, #f59e0b, #ec489a);
            color: white;
        }

        /* Premium Cards */
        .premium-card {
            background: linear-gradient(135deg, #1e293b, #0f172a);
            border-radius: 20px;
            padding: 16px;
            margin-bottom: 12px;
            cursor: pointer;
            transition: transform 0.2s;
            border: 1px solid rgba(59,130,246,0.3);
        }

        .premium-card:active {
            transform: scale(0.98);
        }

        .premium-title {
            font-size: 18px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 8px;
        }

        .premium-price {
            font-size: 24px;
            font-weight: 800;
            color: #f59e0b;
        }

        .premium-features {
            font-size: 12px;
            color: var(--tg-theme-hint-color, #9ca3af);
            margin-top: 8px;
            line-height: 1.5;
        }

        /* Button */
        .connect-btn {
            width: 100%;
            background: linear-gradient(135deg, #3b82f6, #a855f7);
            color: white;
            border: none;
            border-radius: 60px;
            padding: 18px;
            font-size: 18px;
            font-weight: 700;
            margin-top: 20px;
            cursor: pointer;
            transition: opacity 0.2s, transform 0.1s;
        }

        .connect-btn:active {
            transform: scale(0.98);
        }

        /* Footer */
        .footer {
            text-align: center;
            padding: 20px 0;
            margin-top: 20px;
            font-size: 11px;
            color: var(--tg-theme-hint-color, #6b7280);
        }

        .footer a {
            color: var(--tg-theme-link-color, #3b82f6);
            text-decoration: none;
        }

        /* Offline Badge */
        .offline-badge {
            background: #ef4444;
            color: white;
            padding: 6px 12px;
            border-radius: 40px;
            font-size: 12px;
            font-weight: 600;
            display: inline-block;
            margin-bottom: 12px;
        }

        .servers-grid::-webkit-scrollbar {
            width: 4px;
        }

        .servers-grid::-webkit-scrollbar-track {
            background: var(--tg-theme-secondary-bg-color, #1f1f2a);
            border-radius: 4px;
        }

        .servers-grid::-webkit-scrollbar-thumb {
            background: #3b82f6;
            border-radius: 4px;
        }
    </style>
</head>
<body>
    <div class="container" id="app">
        <div style="text-align: center; padding: 40px;">Loading...</div>
    </div>

    <script>
        // ==================== TELEGRAM INIT ====================
        const tg = window.Telegram.WebApp;
        tg.expand();
        tg.ready();
        
        const user = tg.initDataUnsafe?.user;
        const userId = user?.id || null;
        const username = user?.username || user?.first_name || "User";
        
        // ==================== ЯЗЫКИ ====================
        
        const languages = {
            ru: { name: "Русский", flag: "🇷🇺", code: "ru" },
            en: { name: "English", flag: "🇬🇧", code: "en" },
            zh: { name: "中文", flag: "🇨🇳", code: "zh" },
            ja: { name: "日本語", flag: "🇯🇵", code: "ja" },
            ko: { name: "한국어", flag: "🇰🇷", code: "ko" },
            kk: { name: "Қазақша", flag: "🇰🇿", code: "kk" },
            fr: { name: "Français", flag: "🇫🇷", code: "fr" },
            pl: { name: "Polski", flag: "🇵🇱", code: "pl" },
            de: { name: "Deutsch", flag: "🇩🇪", code: "de" }
        };
        
        // ==================== ПЕРЕВОДЫ ====================
        
        const translations = {
            // Общие
            connecting: { ru: "Подключение...", en: "Connecting...", zh: "连接中...", ja: "接続中...", ko: "연결 중...", kk: "Қосылу...", fr: "Connexion...", pl: "Łączenie...", de: "Verbindung..." },
            disconnected: { ru: "Отключено", en: "Disconnected", zh: "已断开", ja: "切断済み", ko: "연결 끊김", kk: "Ажыратылған", fr: "Déconnecté", pl: "Rozłączono", de: "Getrennt" },
            connected: { ru: "Подключено", en: "Connected", zh: "已连接", ja: "接続済み", ko: "연결됨", kk: "Қосылған", fr: "Connecté", pl: "Połączono", de: "Verbunden" },
            selectServer: { ru: "Выберите сервер", en: "Select a server", zh: "选择服务器", ja: "サーバーを選択", ko: "서버 선택", kk: "Серверді таңдаңыз", fr: "Choisissez un serveur", pl: "Wybierz serwer", de: "Wählen Sie einen Server" },
            
            // Статус
            statusOffline: { ru: "Отключено", en: "Disconnected", zh: "已断开", ja: "切断済み", ko: "연결 끊김", kk: "Ажыратылған", fr: "Déconnecté", pl: "Rozłączono", de: "Getrennt" },
            statusOnline: { ru: "Подключено", en: "Connected", zh: "已连接", ja: "接続済み", ko: "연결됨", kk: "Қосылған", fr: "Connecté", pl: "Połączono", de: "Verbunden" },
            
            // Статистика
            gbLeft: { ru: "ГБ осталось", en: "GB left", zh: "剩余GB", ja: "残りGB", ko: "남은 GB", kk: "Қалған ГБ", fr: "GB restants", pl: "Pozostało GB", de: "GB übrig" },
            gbLimit: { ru: "ГБ лимит", en: "GB limit", zh: "GB限制", ja: "GB制限", ko: "GB 한도", kk: "ГБ шегі", fr: "Limite GB", pl: "Limit GB", de: "GB-Limit" },
            tariff: { ru: "Тариф", en: "Plan", zh: "套餐", ja: "プラン", ko: "요금제", kk: "Тариф", fr: "Forfait", pl: "Taryfa", de: "Tarif" },
            
            // Вкладки
            tabServers: { ru: "Серверы", en: "Servers", zh: "服务器", ja: "サーバー", ko: "서버", kk: "Серверлер", fr: "Serveurs", pl: "Serwery", de: "Server" },
            tabPlans: { ru: "Тарифы", en: "Plans", zh: "套餐", ja: "プラン", ko: "요금제", kk: "Тарифтер", fr: "Forfaits", pl: "Taryfy", de: "Tarife" },
            
            // Кнопки
            btnConnect: { ru: "Подключиться", en: "Connect", zh: "连接", ja: "接続", ko: "연결", kk: "Қосу", fr: "Se connecter", pl: "Połącz", de: "Verbinden" },
            btnDisconnect: { ru: "Отключиться", en: "Disconnect", zh: "断开", ja: "切断", ko: "연결 끊기", kk: "Ажырату", fr: "Se déconnecter", pl: "Rozłącz", de: "Trennen" },
            btnManage: { ru: "Управление подпиской", en: "Manage subscription", zh: "管理订阅", ja: "サブスクリプション管理", ko: "구독 관리", kk: "Жазылымды басқару", fr: "Gérer l'abonnement", pl: "Zarządzaj subskrypcją", de: "Abonnement verwalten" },
            
            // Тарифы
            planFree: { ru: "Бесплатный", en: "Free", zh: "免费", ja: "無料", ko: "무료", kk: "Тегін", fr: "Gratuit", pl: "Darmowy", de: "Kostenlos" },
            planPremium: { ru: "Premium", en: "Premium", zh: "高级", ja: "プレミアム", ko: "프리미엄", kk: "Premium", fr: "Premium", pl: "Premium", de: "Premium" },
            planPrime: { ru: "Prime", en: "Prime", zh: "至尊", ja: "プライム", ko: "프라임", kk: "Prime", fr: "Prime", pl: "Prime", de: "Prime" },
            perMonth: { ru: "/ месяц", en: "/ month", zh: "/月", ja: "/月", ko: "/월", kk: "/ай", fr: "/mois", pl: "/miesiąc", de: "/Monat" },
            perYear: { ru: "/ год", en: "/ year", zh: "/年", ja: "/年", ko: "/년", kk: "/жыл", fr: "/an", pl: "/rok", de: "/Jahr" },
            
            // Особенности тарифов
            featureData: { ru: "ГБ трафика", en: "GB traffic", zh: "GB流量", ja: "GBトラフィック", ko: "GB 트래픽", kk: "ГБ трафик", fr: "GB de trafic", pl: "GB ruchu", de: "GB Traffic" },
            featureCountries: { ru: "стран на выбор", en: "countries available", zh: "个国家可选", ja: "か国から選択", ko: "개국 선택 가능", kk: "елден таңдау", fr: "pays au choix", pl: "krajów do wyboru", de: "Länder zur Auswahl" },
            featureAllCountries: { ru: "Все страны", en: "All countries", zh: "所有国家", ja: "全地域", ko: "모든 국가", kk: "Барлық елдер", fr: "Tous les pays", pl: "Wszystkie kraje", de: "Alle Länder" },
            featureGaming: { ru: "Игровые серверы", en: "Gaming servers", zh: "游戏服务器", ja: "ゲームサーバー", ko: "게임 서버", kk: "Ойын серверлері", fr: "Serveurs gaming", pl: "Serwery gamingowe", de: "Gaming-Server" },
            featureWhitelist: { ru: "Белые списки", en: "Whitelists", zh: "白名单", ja: "ホワイトリスト", ko: "화이트리스트", kk: "Ақ тізімдер", fr: "Listes blanches", pl: "Białe listy", de: "Whitelists" },
            featureSpeedBasic: { ru: "Базовая скорость", en: "Basic speed", zh: "基础速度", ja: "基本速度", ko: "기본 속도", kk: "Негізгі жылдамдық", fr: "Vitesse de base", pl: "Podstawowa prędkość", de: "Basisgeschwindigkeit" },
            featureSpeedHigh: { ru: "Высокая скорость", en: "High speed", zh: "高速", ja: "高速", ko: "고속", kk: "Жоғары жылдамдық", fr: "Haute vitesse", pl: "Wysoka prędkość", de: "Hohe Geschwindigkeit" },
            featureSpeedMax: { ru: "Максимальная скорость", en: "Maximum speed", zh: "最高速度", ja: "最高速度", ko: "최고 속도", kk: "Максималды жылдамдық", fr: "Vitesse maximale", pl: "Maksymalna prędkość", de: "Höchstgeschwindigkeit" },
            saving: { ru: "Экономия", en: "Savings", zh: "节省", ja: "節約", ko: "절약", kk: "Үнемдеу", fr: "Économies", pl: "Oszczędność", de: "Ersparnis" },
            
            // Офлайн-режим
            offlineMode: { ru: "ОФЛАЙН-РЕЖИМ", en: "OFFLINE MODE", zh: "离线模式", ja: "オフラインモード", ko: "오프라인 모드", kk: "ОФФЛАЙН РЕЖИМІ", fr: "MODE HORS LIGNE", pl: "TRYB OFFLINE", de: "OFFLINE-MODUS" },
            offlineTime: { ru: "Осталось", en: "Time left", zh: "剩余时间", ja: "残り時間", ko: "남은 시간", kk: "Қалған уақыт", fr: "Temps restant", pl: "Pozostało", de: "Verbleibende Zeit" },
            offlinePopupTitle: { ru: "Офлайн-режим", en: "Offline Mode", zh: "离线模式", ja: "オフラインモード", ko: "오프라인 모드", kk: "Оффлайн режимі", fr: "Mode hors ligne", pl: "Tryb offline", de: "Offline-Modus" },
            offlinePopupMsg: { ru: "Доступны серверы: Россия (Москва), США (Нью-Йорк), Нидерланды (Амстердам). Время: 1.5 часа.", en: "Available servers: Russia (Moscow), USA (New York), Netherlands (Amsterdam). Time: 1.5 hours.", zh: "可用服务器：俄罗斯（莫斯科）、美国（纽约）、荷兰（阿姆斯特丹）。时间：1.5小时。", ja: "利用可能なサーバー：ロシア（モスクワ）、アメリカ（ニューヨーク）、オランダ（アムステルダム）。時間：1.5時間。", ko: "사용 가능한 서버: 러시아(모스크바), 미국(뉴욕), 네덜란드(암스테르담). 시간: 1.5시간.", kk: "Қолжетімді серверлер: Ресей (Мәскеу), АҚШ (Нью-Йорк), Нидерланды (Амстердам). Уақыт: 1.5 сағат.", fr: "Serveurs disponibles : Russie (Moscou), USA (New York), Pays-Bas (Amsterdam). Durée : 1h30.", pl: "Dostępne serwery: Rosja (Moskwa), USA (Nowy Jork), Holandia (Amsterdam). Czas: 1.5 godziny.", de: "Verfügbare Server: Russland (Moskau), USA (New York), Niederlande (Amsterdam). Zeit: 1.5 Stunden." },
            
            // Попапы
            serverUnavailable: { ru: "Сервер недоступен", en: "Server unavailable", zh: "服务器不可用", ja: "サーバーが利用できません", ko: "서버를 사용할 수 없음", kk: "Сервер қолжетімсіз", fr: "Serveur indisponible", pl: "Serwer niedostępny", de: "Server nicht verfügbar" },
            dataLimitExceeded: { ru: "Лимит трафика исчерпан", en: "Data limit exceeded", zh: "流量限制已用完", ja: "データ制限超過", ko: "데이터 한도 초과", kk: "Трафик шегі асып кетті", fr: "Limite de données dépassée", pl: "Limit danych przekroczony", de: "Datenlimit überschritten" },
            connectedPopup: { ru: "Подключено", en: "Connected", zh: "已连接", ja: "接続しました", ko: "연결됨", kk: "Қосылды", fr: "Connecté", pl: "Połączono", de: "Verbunden" },
            
            // Футер
            privacy: { ru: "Политика конфиденциальности", en: "Privacy Policy", zh: "隐私政策", ja: "プライバシーポリシー", ko: "개인정보 처리방침", kk: "Құпиялылық саясаты", fr: "Politique de confidentialité", pl: "Polityka prywatności", de: "Datenschutzerklärung" }
        };
        
        function t(key, lang = currentLang) {
            return translations[key]?.[lang] || translations[key]?.ru || key;
        }
        
        // ==================== КОНФИГУРАЦИЯ СЕРВЕРОВ ====================
        
        const allServers = [
            { id: "ru_moscow", name: "Россия (Москва)", flag: "🇷🇺", locations: ["Москва"], category: "free", tier: "free", offlineAvailable: true, gaming: false, whitelist: false },
            { id: "ru_moscow_whitelist", name: "Россия (Москва Белые списки)", flag: "✅", locations: ["Москва (WL)"], category: "whitelist", tier: "prime", offlineAvailable: false, gaming: false, whitelist: true },
            { id: "us_newyork", name: "США (Нью-Йорк)", flag: "🇺🇸", locations: ["Нью-Йорк"], category: "free", tier: "free", offlineAvailable: true, gaming: false, whitelist: false },
            { id: "us_chicago", name: "США (Чикаго)", flag: "🇺🇸", locations: ["Чикаго"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "us_atlanta", name: "США (Атланта)", flag: "🇺🇸", locations: ["Атланта"], category: "free", tier: "free", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "us_newjersey", name: "США (Нью-Джерси)", flag: "🇺🇸", locations: ["Нью-Джерси"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "nl_amsterdam", name: "Нидерланды (Амстердам)", flag: "🇳🇱", locations: ["Амстердам"], category: "free", tier: "free", offlineAvailable: true, gaming: false, whitelist: false },
            { id: "nl_rotterdam", name: "Нидерланды (Роттердам)", flag: "🇳🇱", locations: ["Роттердам"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "nl_hague", name: "Нидерланды (Гаага)", flag: "🇳🇱", locations: ["Гаага"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "de_berlin", name: "Германия (Берлин)", flag: "🇩🇪", locations: ["Берлин"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "de_hamburg", name: "Германия (Гамбург)", flag: "🇩🇪", locations: ["Гамбург"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "de_frankfurt", name: "Германия (Франкфурт)", flag: "🇩🇪", locations: ["Франкфурт-на-Майне"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "sg", name: "Сингапур", flag: "🇸🇬", locations: ["Сингапур"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "ca_toronto", name: "Канада (Торонто)", flag: "🇨🇦", locations: ["Торонто"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "ca_montreal", name: "Канада (Монреаль)", flag: "🇨🇦", locations: ["Монреаль"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "ca_ottawa", name: "Канада (Оттава)", flag: "🇨🇦", locations: ["Оттава"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "uk_london", name: "Великобритания (Лондон)", flag: "🇬🇧", locations: ["Лондон"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "fr_paris", name: "Франция (Париж)", flag: "🇫🇷", locations: ["Париж"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "fr_arles", name: "Франция (Арль)", flag: "🇫🇷", locations: ["Арль"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "fr_rouen", name: "Франция (Руан)", flag: "🇫🇷", locations: ["Руан"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "no_oslo", name: "Норвегия (Осло)", flag: "🇳🇴", locations: ["Осло"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "no_bergen", name: "Норвегия (Берген)", flag: "🇳🇴", locations: ["Берген"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "jp_tokyo", name: "Япония (Токио)", flag: "🇯🇵", locations: ["Токио"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "jp_fukuoka", name: "Япония (Фукуока)", flag: "🇯🇵", locations: ["Фукуока"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "jp_kyoto", name: "Япония (Киото)", flag: "🇯🇵", locations: ["Киото"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "cn_beijing", name: "Китай (Пекин)", flag: "🇨🇳", locations: ["Пекин"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "cn_shanghai", name: "Китай (Шанхай)", flag: "🇨🇳", locations: ["Шанхай"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "hk", name: "Гонконг", flag: "🇭🇰", locations: ["Гонконг"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "kr_seoul", name: "Южная Корея (Сеул)", flag: "🇰🇷", locations: ["Сеул"], category: "premium", tier: "premium", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "kr_busan", name: "Южная Корея (Пусан)", flag: "🇰🇷", locations: ["Пусан"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "kz_astana", name: "Казахстан (Астана)", flag: "🇰🇿", locations: ["Астана"], category: "free", tier: "free", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "tr_istanbul", name: "Турция (Стамбул)", flag: "🇹🇷", locations: ["Стамбул"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "cz_prague", name: "Чехия (Прага)", flag: "🇨🇿", locations: ["Прага"], category: "free", tier: "free", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "pl_warsaw", name: "Польша (Варшава)", flag: "🇵🇱", locations: ["Варшава"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "ph_manila", name: "Филиппины (Манила)", flag: "🇵🇭", locations: ["Манила"], category: "premium", tier: "prime", offlineAvailable: false, gaming: false, whitelist: false },
            { id: "gaming_ru", name: "Игровой (Россия)", flag: "🎮", locations: ["Москва"], category: "gaming", tier: "premium", offlineAvailable: false, gaming: true, whitelist: false },
            { id: "gaming_eu", name: "Игровой (Европа)", flag: "🎮", locations: ["Франкфурт"], category: "gaming", tier: "premium", offlineAvailable: false, gaming: true, whitelist: false },
            { id: "gaming_us", name: "Игровой (США)", flag: "🎮", locations: ["Нью-Йорк"], category: "gaming", tier: "premium", offlineAvailable: false, gaming: true, whitelist: false },
            { id: "gaming_asia", name: "Игровой (Азия)", flag: "🎮", locations: ["Токио"], category: "gaming", tier: "prime", offlineAvailable: false, gaming: true, whitelist: false },
            { id: "whitelist_ru", name: "Белый список (Россия)", flag: "✅", locations: ["Москва"], category: "whitelist", tier: "prime", offlineAvailable: false, gaming: false, whitelist: true },
            { id: "whitelist_us", name: "Белый список (США)", flag: "✅", locations: ["Нью-Йорк"], category: "whitelist", tier: "prime", offlineAvailable: false, gaming: false, whitelist: true },
            { id: "whitelist_eu", name: "Белый список (Европа)", flag: "✅", locations: ["Амстердам"], category: "whitelist", tier: "prime", offlineAvailable: false, gaming: false, whitelist: true }
        ];
        
        // ==================== ТАРИФЫ ====================
        
        const plans = {
            free: { nameKey: "planFree", price: "0 ₽", dataLimit: 50, tier: "free", features: ["50 GB", "5 countries", "basic speed"] },
            premium_monthly: { nameKey: "planPremium", price: "299 ₽", dataLimit: 100, tier: "premium", features: ["100 GB", "asia + france", "gaming servers", "high speed"] },
            prime_yearly: { nameKey: "planPrime", price: "1 990 ₽", dataLimit: 200, tier: "prime", features: ["200 GB", "all countries", "all gaming", "whitelists", "max speed", "45% saving"] }
        };
        
        // ==================== СОСТОЯНИЕ ====================
        
        let currentLang = localStorage.getItem("cartesian_lang") || "ru";
        let state = {
            isConnected: false,
            selectedServerId: "ru_moscow",
            userTier: "free",
            usedData: 0,
            offlineMode: false,
            offlineTimeLeft: 90,
            connectionTimer: null
        };
        
        let activeTab = "servers";
        let offlineTimerInterval = null;
        
        // ==================== ФУНКЦИИ ====================
        
        function checkOfflineMode() {
            if (!navigator.onLine) {
                state.offlineMode = true;
                startOfflineTimer();
                return true;
            }
            return false;
        }
        
        function startOfflineTimer() {
            if (offlineTimerInterval) clearInterval(offlineTimerInterval);
            offlineTimerInterval = setInterval(() => {
                if (state.offlineMode && state.offlineTimeLeft > 0) {
                    state.offlineTimeLeft--;
                    if (state.offlineTimeLeft <= 0) {
                        state.offlineMode = false;
                        if (state.isConnected) disconnectVPN();
                        clearInterval(offlineTimerInterval);
                        tg.showPopup({
                            title: t("offlinePopupTitle"),
                            message: t("offlinePopupMsg"),
                            buttons: [{ type: "ok" }]
                        });
                    }
                    render();
                }
            }, 60000);
        }
        
        function getAvailableServers() {
            let servers = [...allServers];
            if (state.offlineMode) {
                const offlineIds = ["ru_moscow", "us_newyork", "nl_amsterdam"];
                servers = servers.filter(s => offlineIds.includes(s.id));
            } else {
                if (state.userTier === "free") servers = servers.filter(s => s.tier === "free");
                else if (state.userTier === "premium") servers = servers.filter(s => s.tier === "free" || s.tier === "premium");
            }
            return servers;
        }
        
        function checkDataLimit() {
            const limit = state.userTier === "free" ? 50 : (state.userTier === "premium" ? 100 : 200);
            return state.usedData < limit;
        }
        
        function connectVPN() {
            if (state.isConnected) { disconnectVPN(); return; }
            const selectedServer = allServers.find(s => s.id === state.selectedServerId);
            const availableServers = getAvailableServers();
            if (!availableServers.find(s => s.id === state.selectedServerId)) {
                tg.showPopup({ title: t("serverUnavailable"), message: `${selectedServer?.name} ${t("serverUnavailable")}`, buttons: [{ type: "ok" }] });
                return;
            }
            if (!checkDataLimit()) {
                tg.showPopup({ title: t("dataLimitExceeded"), message: t("dataLimitExceeded"), buttons: [{ type: "ok" }] });
                return;
            }
            state.isConnected = true;
            tg.sendData(JSON.stringify({ action: "connect", server: state.selectedServerId, server_name: selectedServer?.name, user_id: userId, plan: state.userTier }));
            tg.showPopup({ title: t("connectedPopup"), message: `${selectedServer?.name}`, buttons: [{ type: "ok" }] });
            tg.HapticFeedback.notificationOccurred('success');
            render();
        }
        
        function disconnectVPN() {
            state.isConnected = false;
            tg.sendData(JSON.stringify({ action: "disconnect", user_id: userId }));
            render();
        }
        
        function selectPlan(planKey) {
            if (planKey === state.userTier) return;
            if (planKey !== "free") {
                tg.sendData(JSON.stringify({ action: "purchase", plan: planKey, user_id: userId, price: plans[planKey]?.price }));
                tg.showPopup({ title: "💎", message: `${t(plans[planKey]?.nameKey)}`, buttons: [{ type: "ok" }] });
            } else {
                state.userTier = "free";
                render();
            }
        }
        
        function changeLanguage(lang) {
            currentLang = lang;
            localStorage.setItem("cartesian_lang", lang);
            render();
        }
        
        // ==================== СОБЫТИЯ СЕТИ ====================
        
        window.addEventListener('online', () => {
            state.offlineMode = false;
            if (offlineTimerInterval) clearInterval(offlineTimerInterval);
            state.offlineTimeLeft = 90;
            tg.showPopup({ title: "🔄", message: t("offlinePopupMsg"), buttons: [{ type: "ok" }] });
            render();
        });
        
        window.addEventListener('offline', () => {
            state.offlineMode = true;
            startOfflineTimer();
            tg.showPopup({ title: t("offlinePopupTitle"), message: t("offlinePopupMsg"), buttons: [{ type: "ok" }] });
            render();
        });
        
        // ==================== РЕНДЕР ====================
        
        function getBadgeClass(server) {
            if (state.offlineMode) return "";
            if (server.tier === "prime") return "prime";
            if (server.tier === "premium") return "premium";
            return "";
        }
        
        function getBadgeText(server) {
            if (state.offlineMode) return "🌙 Offline";
            if (server.gaming) return "🎮 Gaming";
            if (server.whitelist) return "✅ Whitelist";
            if (server.tier === "prime") return "👑 Prime";
            if (server.tier === "premium") return "⭐ Premium";
            return "Free";
        }
        
        function render() {
            const offline = state.offlineMode;
            const availableServers = getAvailableServers();
            const selectedServer = allServers.find(s => s.id === state.selectedServerId);
            const dataLimit = state.userTier === "free" ? 50 : (state.userTier === "premium" ? 100 : 200);
            const dataLeft = Math.max(0, dataLimit - state.usedData);
            
            const langSelectorHtml = `
                <select id="langSelect" class="lang-selector" onchange="changeLanguage(this.value)">
                    ${Object.entries(languages).map(([code, lang]) => `
                        <option value="${code}" ${currentLang === code ? 'selected' : ''}>${lang.flag} ${lang.name}</option>
                    `).join('')}
                </select>
            `;
            
            const html = `
                ${langSelectorHtml}
                ${offline ? `<div style="text-align: center;"><span class="offline-badge">📡 ${t("offlineMode")} (${Math.floor(state.offlineTimeLeft / 60)}ч ${state.offlineTimeLeft % 60}мин)</span></div>` : ''}
                
                <div class="header">
                    <div class="logo">Cartesian VPN</div>
                    <div class="subtitle">Secure & Fast VPN</div>
                </div>
                
                <div class="status-card">
                    <div class="status-icon">${state.isConnected ? (selectedServer?.flag || '🔒') : '🔓'}</div>
                    <div class="status-text">${state.isConnected ? t("connected") : t("disconnected")}</div>
                    <div class="status-subtext">${state.isConnected ? selectedServer?.name : t("selectServer")}</div>
                    ${offline && state.offlineTimeLeft > 0 ? `<div class="timer">⏱️ ${t("offlineTime")}: ${Math.floor(state.offlineTimeLeft / 60)}ч ${state.offlineTimeLeft % 60}мин</div>` : ''}
                </div>
                
                <div class="stats-row">
                    <div class="stat-card"><div class="stat-value">${dataLeft}</div><div class="stat-label">${t("gbLeft")}</div></div>
                    <div class="stat-card"><div class="stat-value">${dataLimit}</div><div class="stat-label">${t("gbLimit")}</div></div>
                    <div class="stat-card"><div class="stat-value">${state.userTier === "free" ? t("planFree") : (state.userTier === "premium" ? t("planPremium") : t("planPrime"))}</div><div class="stat-label">${t("tariff")}</div></div>
                </div>
                
                <div class="tab-bar">
                    <div class="tab ${activeTab === 'servers' ? 'active' : ''}" data-tab="servers">🌍 ${t("tabServers")} (${availableServers.length})</div>
                    <div class="tab ${activeTab === 'plans' ? 'active' : ''}" data-tab="plans">💎 ${t("tabPlans")}</div>
                </div>
                
                ${activeTab === 'servers' ? `
                    <div class="servers-grid">
                        ${availableServers.map(server => `
                            <div class="server-card ${state.selectedServerId === server.id ? 'selected' : ''}" data-server-id="${server.id}">
                                <div class="server-info">
                                    <div class="server-flag">${server.flag}</div>
                                    <div class="server-details">
                                        <div class="server-name">${server.name}</div>
                                        <div class="server-locations">📍 ${server.locations.join(', ')}</div>
                                    </div>
                                </div>
                                <div class="server-badge ${getBadgeClass(server)}">${getBadgeText(server)}</div>
                            </div>
                        `).join('')}
                    </div>
                    <button class="connect-btn" id="connectBtn">${state.isConnected ? t("btnDisconnect") : t("btnConnect")}</button>
                ` : `
                    <div>
                        <div class="premium-card" data-plan="free">
                            <div class="premium-title">🎁 ${t("planFree")}</div>
                            <div class="premium-price">0 ₽</div>
                            <div class="premium-features">📦 50 ${t("featureData")}<br>🌍 5 ${t("featureCountries")}<br>⚡ ${t("featureSpeedBasic")}</div>
                        </div>
                        <div class="premium-card" data-plan="premium_monthly">
                            <div class="premium-title">⭐ ${t("planPremium")}</div>
                            <div class="premium-price">299 ₽${t("perMonth")}</div>
                            <div class="premium-features">📦 100 ${t("featureData")}<br>🌍 ${t("featureCountries")}<br>🎮 ${t("featureGaming")}<br>⚡ ${t("featureSpeedHigh")}</div>
                        </div>
                        <div class="premium-card" data-plan="prime_yearly">
                            <div class="premium-title">👑 ${t("planPrime")}</div>
                            <div class="premium-price">1 990 ₽${t("perYear")}</div>
                            <div class="premium-features">📦 200 ${t("featureData")}<br>🌍 ${t("featureAllCountries")}<br>🎮 ${t("featureGaming")}<br>✅ ${t("featureWhitelist")}<br>⚡ ${t("featureSpeedMax")}<br>💰 ${t("saving")} 45%</div>
                        </div>
                    </div>
                    ${state.userTier !== 'free' ? `<button class="connect-btn" id="manageSubBtn">📋 ${t("btnManage")}</button>` : ''}
                `}
                
                <div class="footer">
                    <a href="#" id="privacyLink">${t("privacy")}</a>
                    <span style="margin: 0 8px">•</span>
                    <span>@ARELLANOSILVANO</span>
                </div>
            `;
            
            document.getElementById('app').innerHTML = html;
            
            // Обработчики
            document.querySelectorAll('.tab').forEach(tab => {
                tab.addEventListener('click', (e) => {
                    activeTab = e.target.dataset.tab;
                    render();
                });
            });
            
            if (activeTab === 'servers') {
                document.querySelectorAll('.server-card').forEach(card => {
                    card.addEventListener('click', (e) => {
                        const serverId = card.dataset.serverId;
                        state.selectedServerId = serverId;
                        render();
                        tg.HapticFeedback.impactOccurred('light');
                    });
                });
                document.getElementById('connectBtn')?.addEventListener('click', connectVPN);
            }
            
            if (activeTab === 'plans') {
                document.querySelectorAll('.premium-card').forEach(card => {
                    card.addEventListener('click', (e) => {
                        const plan = card.dataset.plan;
                        selectPlan(plan);
                    });
                });
                document.getElementById('manageSubBtn')?.addEventListener('click', () => {
                    tg.sendData(JSON.stringify({ action: "manage_subscription", user_id: userId }));
                });
            }
            
            document.getElementById('privacyLink')?.addEventListener('click', (e) => {
                e.preventDefault();
                tg.openLink("https://telegra.ph/Privacy-Policy-Cartesian-VPN-03-22");
            });
        }
        
        // Инициализация
        checkOfflineMode();
        render();
        tg.sendData(JSON.stringify({ action: "init", user_id: userId, username: username, lang: currentLang }));
    </script>
</body>
</html>
