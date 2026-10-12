# MediaFlow — Modern YouTube MP3 / MP4 Dönüştürücü

React, TypeScript, Tailwind CSS ile oluşturulmuş modern medya dönüştürücü web sitesi. Vercel üzerinde çalışır.

## Özellikler

- ⚡ **Modern tasarım**: Koyu tema, cam efekti (glassmorphism), gradient efektler
- 🔒 **Güvenli**: Whitelist tabanlı URL doğrulama, SSRF koruması
- 📱 **Responsive**: Mobil, tablet, masaüstü desteği
- 🌐 **Türkçe**: Tüm metinler Türkçe
- 🎬 **Simülasyon**: Gerçek dönüştürme için arka uç işçisi hazır
- 🛡️ **Rate limiting**: İstek sınırlandırması

## Notlar (Önemli)

**Gerçek video işleme (FFmpeg)** Vercel Functions üzerinde doğrudan çalıştırılamaz. Bu projeyi Vercel'de çalıştırmak için:

1. **Ön Uç (Frontend)**: Bu Next.js uygulaması Vercel'de çalışır.
2. **Arka Uç İşçisi (Worker)**: Gerçek MP3/MP4 dönüştürme için aşağıdaki seçeneklerden birini kurmalısınız:
   - **AWS Lambda + FFmpeg** (Node.js 18/20 runtime)
   - **Google Cloud Run** (FFmpeg kurulu container)
   - **Render / Railway** (Özel sunucu)
   - **Kendi sunucunuz** (Node.js + FFmpeg + Redis)

**Örnek entegrasyon noktası:**
- `src/app/api/convert/route.ts` — URL doğrulama ve video bilgisi endpoint'i
- `src/app/api/download/[id]/[file]/route.ts` — İndirme adaptör endpoint'i

## Kurulum

```bash
git clone <repo-url>
cd mediaflow
npm install
cp .env.example .env.local
npm run dev
```

## Çevre Değişkenleri (.env.local)

```env
# Uygulama URL (Vercel için otomatik ayarlanır)
NEXT_PUBLIC_APP_URL=https://mediaflow.app

# API erişim anahtarı (isteğe bağlı, gerçek arka uç için)
API_SECRET_KEY=your-secret-api-key

# Eğer gerçek arka uç işçisi kullanıyorsanız:
WORKER_URL=https://your-worker.example.com
WORKER_API_KEY=your-worker-key
```

## Vercel Dağıtım Talimatları

1. GitHub repo'sunu Vercel'e bağlayın
2. Ortam değişkenlerini `.env.local` ile Vercel dashboard'a ekleyin
3. **Build settings**: `npm run build` (varsayılan)
4. **Output directory**: `.next` (varsayılan)

## Teknik Kalite

- TypeScript ile yazılmıştır
- ESLint kuralları dahil
- `lucide-react` ikonları
- `framer-motion` animasyonları
- Tailwind CSS v4

## Geliştirme

```bash
npm run dev      # Geliştirme sunucusu
npm run build    # Üretim build'i
npm run lint     # Lint kontrolü
```

## Lisans

MIT — Kişisel kullanım ve eğitim amaçlıdır.
