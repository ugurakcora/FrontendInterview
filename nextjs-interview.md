# Next.js Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. Next.js nedir ve React'tan farkı nedir?

**Cevap:** Next.js, React tabanlı bir web framework'üdür. React'a ek olarak:

- Server-side rendering (SSR)
- Static site generation (SSG)
- File-based routing
- API routes
- Built-in CSS ve Sass desteği
  gibi özellikler sunar.

### 2. Next.js'de routing nasıl çalışır?

**Cevap:** Next.js file-based routing kullanır. `pages` dizinindeki dosya yapısı direkt olarak route'ları belirler. Örneğin:

- `pages/index.js` → `/`
- `pages/about.js` → `/about`
- `pages/blog/[id].js` → `/blog/1`, `/blog/2` vb.

### 3. getStaticProps ve getServerSideProps arasındaki fark nedir?

**Cevap:**

- `getStaticProps`: Build time'da çalışır, statik sayfalar oluşturur
- `getServerSideProps`: Her request'te server-side'da çalışır, dinamik data gerektiğinde kullanılır

### 4. Next.js'de optimizasyon yöntemleri nelerdir?

**Cevap:**

- Image Optimization (`next/image`)
- Automatic code splitting
- Dynamic imports
- Built-in CSS optimization
- Font optimization

## Orta Seviye Sorular

### 5. Next.js middleware nedir ve ne için kullanılır?

**Cevap:** Middleware, sayfa render edilmeden önce çalışan bir fonksiyondur. Authentication, redirects, rewrite, response manipulation gibi işlemler için kullanılır.

### 6. ISR (Incremental Static Regeneration) nedir?

**Cevap:** Statik sayfaları belirli aralıklarla yeniden oluşturma özelliğidir. `revalidate` parametresi ile kullanılır ve hybrid bir yaklaşım sunar.

### 7. Next.js'de API routes nasıl çalışır?

**Cevap:** `pages/api` dizininde oluşturulan dosyalar otomatik olarak API endpoint'leri olur. Serverless functions olarak çalışır ve full-stack uygulamalar geliştirmeyi kolaylaştırır.

### 8. \_app.js ve \_document.js arasındaki fark nedir?

**Cevap:**

- `_app.js`: Tüm sayfalar için ortak layout, state management, global CSS
- `_document.js`: HTML yapısını özelleştirme, `<head>`, `<body>` etiketlerini modifiye etme

## İleri Seviye Sorular

### 9. Next.js 13'ün app directory'si ne gibi yenilikler getirdi?

**Cevap:**

- Server Components varsayılan olarak
- Nested layouts
- Streaming
- Yeni data fetching sistemi
- Turbopack (beta)

### 10. Edge Runtime vs Node.js Runtime farkı nedir?

**Cevap:**

- Edge: Daha hızlı cold start, sınırlı API erişimi
- Node.js: Tam API erişimi, daha yavaş cold start

### 11. Next.js'de caching mekanizmaları nelerdir?

**Cevap:**

- Full Route Cache
- Router Cache
- Data Cache
- Request Memoization
- Full Route Cache Revalidation

### 12. Next.js'de internationalization nasıl yapılır?

**Cevap:**

- Built-in i18n routing desteği
- Locale detection
- Domain routing
- Sub-path routing
- Auto locale detection
