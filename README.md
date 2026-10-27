# ZeroxSMP Site

Bu klasör ZeroxSMP web sitesinin **yayına hazır** dosyalarını içerir.

## Klasör yapısı

```
zeroxsmp-site/
  index.html                 Ana sayfa
  panel.html                 Hesap paneli (giriş / görev kodu / mağaza)
  android.html               Android tanıtım sayfası
  assets/
    style.css                Tema
    landing.js               Ana sayfa etkileşimleri
    panel.js                 Panel / API işlemleri
    config.js                Canlı API adresi (Cloudflare Tunnel)
    logo.svg                 Logo
  download/
    ZeroxLauncher.exe        Windows launcher v1.4.7
  .nojekyll                  GitHub Pages için
```

## Çalışan canlı adres

Site şu anda Cloudflare Tunnel üzerinden herkesin erişimine açık:

- Ana sayfa: https://hiring-english-role-rounds.trycloudflare.com/
- Panel: https://hiring-english-role-rounds.trycloudflare.com/panel
- Launcher: https://hiring-english-role-rounds.trycloudflare.com/download/launcher

> Tunnel, bu bilgisayar ve sunucu açık olduğu sürece çalışır. Bilgisayar kapanırsa
> veya cloudflared yeniden başlarsa adres değişebilir. Adres değişince
> `assets/config.js` içindeki `window.ZEROX_API` satırını güncelle.

## GitHub Pages'e yükleme

1. GitHub'da yeni bir **public** repo oluştur (ör. `zeroxsmp-site`).
2. Bu klasördeki dosyaları repo köküne yükle.
   - GitHub web arayüzünde tek dosya sınırı 25 MB olduğu için 66 MB'lık
     `download/ZeroxLauncher.exe` dosyasını web arayüzüyle yükleyemezsin.
   - Launcher'ı **Releases** bölümüne yükle veya ana sayfadaki indirme linkini
     çalışan tunnel adresine (`/download/launcher`) çevir.
3. Repo → **Settings → Pages** → **Deploy from a branch** → `main` / `root`
   seç ve kaydet.
4. Yayın adresi: `https://<kullanıcı>.github.io/zeroxsmp-site/`

### GitHub Pages'te panel nasıl çalışır?

GitHub Pages sadece statik dosya sunar; Java sunucusunu çalıştıramaz. Bu yüzden
`assets/config.js` panelin API isteklerini canlı Cloudflare Tunnel adresine
yönlendirir. GitHub Pages'te site açıldığında giriş, görev kodu, mağaza ve
envanter işlemleri tunnel üzerinden gerçek sunucuya gider.

Tunnel kapalıysa panel "Sunucuya ulaşılamadı" hatası verir; ana sayfa ve
launcher indirme yine açılır.

## Yerel çalıştırma

Site, Minecraft sunucusunun içindeki HTTP sunucusundan da servis edilir:

- http://127.0.0.1:8765/
- http://127.0.0.1:8765/panel

`config.js` yerelde API adresini boş bırakır; böylece panel aynı sunucuya
(`/api/site/...`) istek atar.

## Notlar

- Site hesabı = launcher hesabı. Ayrı site kaydı yoktur.
- Görev kodları `ZX-...`, TL kodları `TL-...` formatındadır.
- TL kodları sitedeki görev kodu alanına değil, oyunda `/code <kod>` olarak
  girilir.
- Admin bilgileri bu klasörde tutulmaz; sunucudaki `ADMIN-GIRIS.txt` dosyasına
  bakılır.
