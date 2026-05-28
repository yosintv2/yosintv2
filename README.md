Build a premium dark-themed React Native mobile app called YoSinTV using Expo (~54), expo-router (~6), TypeScript, and @tanstack/react-query inside a pnpm monorepo.

Purpose: Live cricket & football scores, news articles, streaming links, and community links for a Nepali sports audience.

Tech Stack

Expo ~54, expo-router ~6, React Native, TypeScript
@tanstack/react-query for data fetching
pnpm monorepo — mobile app lives in artifacts/mobile/
Dark-only UI (userInterfaceStyle: "dark")
Package name: net.yosintv.tv, version: 1.1
newArchEnabled: false (for Android compatibility)
Remote Config
Fetch config JSON from https://api.singhs.com.np/api/main-config.json at launch (5s timeout), fallback to alt_config_url. Merge with defaultConfig. Config controls everything:

{
  "review_mode": false,
  "streaming_enabled": true,
  "streaming_url": "https://www.yosintv.net/{match_id}.json",
  "ads_enabled": true,
  "banner_enabled": true,
  "rewarded_enabled": true,
  "app_open_enabled": true,
  "interstitial_enabled": true,
  "banner_ad_id": "ca-app-pub-5525538810839147/3825132304",
  "rewarded_ad_id": "ca-app-pub-5525538810839147/6942250234",
  "app_open_ad_id": "ca-app-pub-5525538810839147/1223019695",
  "interstitial_ad_id": "ca-app-pub-5525538810839147/4446428920",
  "analytics_enabled": true,
  "google_analytics_id": "G-XXXXXXXXXX",
  "maintenance_mode": false,
  "maintenance_message": "App is under maintenance. Please try again later.",
  "app_message": "Welcome to YoSinTV v1.1.0!",
  "app_message_type": "info",
  "whatsapp_link": "https://wa.me/1234567890",
  "telegram_link": "https://t.me/yosintv",
  "popup_enabled": true,
  "popup_title": "Welcome to YoSinTV!",
  "popup_text": "Join our WhatsApp and Telegram groups for match updates!",
  "football_api_url": "https://api.singhs.com.np/api/match-football.json",
  "cricket_api_url": "https://api.singhs.com.np/api/match-cricket.json",
  "articles_api_url": "https://api.singhs.com.np/api/articles.json",
  "alt_config_url": "https://api.singhs.com.np/api/alt-config.json",
  "google_services_json_url": "https://api.singhs.com.np/api/google-services.json",
  "app_update": {
    "latest_version": "1.2.0",
    "force_update": false,
    "update_url": "https://play.google.com/store/apps/details?id=net.yosintv.tv",
    "popup_title": "New Update Available!",
    "popup_message": "Update now for the best experience!"
  }
}

5 Tab Screens

Home — featured matches (cricket + football combined), top articles
Cricket — live/upcoming/FT cricket matches
Football — live/upcoming/FT football matches
News — articles list with images, tags, external links
Settings — app info, WhatsApp/Telegram links, version
On iOS use SymbolView (SF Symbols). On Android use Ionicons from @expo/vector-icons. Load Ionicons.font explicitly in useFonts for Android compatibility.

Match Card Behavior

LIVE badge (red pulsing dot) for in-progress matches
Countdown (e.g. "2h 15m") for upcoming matches
FT badge for 72h after match end, hidden after 72h
"Click to open" bar at the bottom opens StreamLinksSheet
StreamLinksSheet fetches stream links from streaming_url (replace {match_id} with slug extracted from details_url), shows list of links, opens in browser
Rewarded ad fires randomly (50% chance) after 2s delay when sheet opens
Football API returns {"matches": [...]} not a bare array — handle with toArray() helper
Stream Link Parsing
The stream JSON can be shaped as:

{ "events": [{ "name": "...", "link": "url" }] } — cricket
{ "events": [{ "name": "...", "links": ["url1", "url2"] }] } — football (flatten nested links)
Bare array of objects or strings
All parsing is in utils/streamLinks.ts — shared by StreamLinksSheet, WatchModal, and match-detail.

Splash Screen
Animated custom splash (no image): "YoSinTV" wordmark springs in, blue bar expands, "24x7 Cricket | Football" tagline rises. Background #08090f. SplashScreen.hideAsync() called on first paint. After splash → update popup (if newer version) → welcome popup (if popup_enabled).

Ads (react-native-google-mobile-ads)

Banner ad on match list screens
Interstitial on article open
Rewarded ad when stream links sheet opens
App open ad on cold start
All use lazy require() inside try-catch (Expo Go safe)
Web stubs as .web.ts files
review_mode: true hides all Watch Live / streaming buttons for App Store review
AdMob App IDs (app.json plugin)

"androidAppId": "ca-app-pub-5525538810839147~XXXXXXXXXX",
"iosAppId": "ca-app-pub-5525538810839147~XXXXXXXXXX"

Analytics
GA4 Measurement Protocol in utils/analytics.ts. AnalyticsTracker component in _layout.tsx tracks all screen changes via usePathname(). Only fires if analytics_enabled: true and google_analytics_id is set.

Key Architecture Rules

No KeyboardProvider wrapper — causes silent crashes on Android
return null during font loading replaced with <View style={{ flex:1, backgroundColor:"#08090f" }} />
newArchEnabled: false — required for Android stability
Do NOT nest FlatList inside ScrollView
useNativeDriver: false for all opacity animations
Football API shape: {"matches":[...]} — use toArray() to normalize
