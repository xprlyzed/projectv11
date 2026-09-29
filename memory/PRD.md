# artirdim.com — PRD (Laravel 12 + Inertia + Vue 3)

## Kaynak & Kurulum
- Repo: github.com/xprlyzed/projectv9 → Laravel projesi `/app/projectv9/projecct`
- Stack: Laravel 12, Inertia+Vue3, MariaDB, Redis, LiveKit, Vite
- Ortam: PHP 8.2 + Composer + MariaDB + Redis apt ile kuruldu; serve :3000 + scheduler (supervisor)
- DB: auction/auction/auction123; seed'ler yüklü; build: `yarn build`
- Test hesapları: admin@seller/buyer @test.com / password

## 2026-09-29 — 7 Görev Oturumu (kullanıcı geri bildirimiyle revize)
1. **Görev 1 (Teklif avatarı):** `auction-show.js` `addBidToFeed` → ui-avatars `<img class="bid-avatar">` kaldırıldı, inline style'lar `.bid-info-col`/`.bid-mine-tag` class'larına çevrildi (auction-show.css; ölü `.bid-avatar` kuralı silindi). Admin/Auctions/Show.vue bid listesi avatarı kaldırıldı; backend ölü `avatar` alanları temizlendi (General/BidController, Admin/AuctionController). Canlı odalarda (Mobile/DesktopLiveRoom) teklif feed'i zaten avatarsızdı — değişiklik gerekmedi.
2. **Görev 2 (Canlı halka):** theme-new.css'e `.avatar-live-ring` (conic-gradient #ff2d55→#a855f7 dönen halka + pulse, reduced-motion korumalı). Uygulandı: Auctions/Show (sss-ava-link + seller-ava-link, koşul `a.is_live && !a.has_finished`), Desktop/MobileLiveRoom (connState==='live'), Profile/Show (pf-avatar-outer, koşul `pf.user.is_live` — backend'e `is_live` eklendi, ProfileController). E2E doğrulama YAPILAMADI: backend heartbeat mekanizması is_live'ı yayıncısızda false'a çekiyor (kapsam dışı).
3. **Görev 3 (Mesaj listesi):** Messages/Index.vue — `convList` reaktif kopya; `bumpConversation()` (last_body güncelle + en üste taşı + aktif değilse unread++) send/poll/echo message.sent içinde çağrılıyor; props.conversations watch ile senkron.
4. **Görev 4 (Skeleton):** Yeni `SkeletonStoryBar.vue`; StoryBar üç-durumlu: `loading` prop → skeleton, stories boş → tamamen gizli (mevcut davranış korundu), yüklü → gerçek içerik. Ana sayfa verisi Inertia ile senkron geldiği için loading prop varsayılan false (ileride async'e geçilirse hazır).
5. **Görev 5 (Kod kalitesi):** Değiştirilen dosyalarda inline style → class; ölü kod temizlendi; test edilen sayfalarda konsol hatası yok.
6. **Görev 6 (Turuncu→altın accent):** `--color-accent` (#e0a92e dark / #c9971f light) + `--color-accent-soft` tanımlandı; tüm turuncu hex'ler (buy-now, yıldızlar, rozetler, hata sayfaları, confetti, status-pending) accent'e bağlandı. Doğrulandı: buy-now = rgb(224,169,46), 404 sayfası gradyanı altın.
7. **Görev 7 (Footer):** `.app-footer` margin-top: 28px (layout seviyesi) — KORUNDU, doğrulandı. **Kullanıcı talebiyle modernizasyon GERİ ALINDI** (pf-stat mini-kartlar, info-row hiyerarşisi, icon chip'ler eski halinde).

## Backlog / Sonraki
- P1: Canlı halka e2e doğrulaması (yayıncı aktifken), mesaj listesi iki oturumlu realtime test.
- P1: Admin detay modernizasyonu (kullanıcı istemedi — tekrar gündeme gelirse farklı tasarım dili öner).
- P2: Görev 4 loading state'in gerçek async veri akışına bağlanması (şu an senkron prop).
- Not: Git push kullanıcıya ait; submodule kontrolleri (find .git / ls-files 160000) push öncesi yapılmalı.
