# CSS Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. CSS Box Model nedir?

**Cevap:** Box Model, HTML elementlerinin kapladığı alanı tanımlayan modeldir:

- Content: İçeriğin gösterildiği alan
- Padding: İçerik ile border arasındaki boşluk
- Border: Padding'i çevreleyen çizgi
- Margin: Dış boşluk, diğer elementlerle arasındaki mesafe

### 2. Position özellikleri nelerdir?

**Cevap:**

- `static`: Default pozisyon
- `relative`: Normal pozisyonuna göre konumlandırma
- `absolute`: En yakın positioned parent'a göre konumlandırma
- `fixed`: Viewport'a göre sabit konumlandırma
- `sticky`: Scroll pozisyonuna göre yapışkan konumlandırma

### 3. Flexbox ve Grid arasındaki fark nedir?

**Cevap:**

- Flexbox: Tek boyutlu layout için (satır VEYA sütun)
- Grid: İki boyutlu layout için (satır VE sütun)
- Flexbox daha esnek, Grid daha yapısal
- Flexbox içerik odaklı, Grid layout odaklı

### 4. CSS Specificity nasıl çalışır?

**Cevap:** Specificity (özgüllük) sıralaması:

1. Inline styles (1000)
2. ID selectors (100)
3. Class selectors, attributes, pseudo-classes (10)
4. Element selectors ve pseudo-elements (1)

## Orta Seviye Sorular

### 5. CSS Preprocessor'lar nedir ve neden kullanılır?

**Cevap:** SASS, LESS gibi preprocessor'lar CSS'e ek özellikler ekler:

- Variables
- Nesting
- Mixins
- Functions
- Modülerlik
- Import/Export

### 6. CSS-in-JS nedir ve avantajları nelerdir?

**Cevap:**

- Scoped styles
- Dynamic styling
- JavaScript ile style yönetimi
- Component-based styling
- Dead code elimination
- Type safety (TypeScript ile)

### 7. Responsive Design teknikleri nelerdir?

**Cevap:**

```css
/* Media Queries */
@media screen and (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}

/* Fluid Typography */
html {
  font-size: calc(16px + 0.5vw);
}

/* Container Queries */
@container (min-width: 400px) {
  .card {
    display: grid;
    grid-template-columns: 2fr 1fr;
  }
}
```

### 8. CSS Architecture yaklaşımları nelerdir?

**Cevap:**

- BEM (Block Element Modifier)
- SMACSS (Scalable and Modular Architecture for CSS)
- OOCSS (Object-Oriented CSS)
- Atomic CSS
- CSS Modules

## İleri Seviye Sorular

### 9. CSS Animations ve Transitions farkı nedir?

**Cevap:**

```css
/* Transition */
.button {
  transition: all 0.3s ease;
}

/* Animation */
@keyframes slide-in {
  from {
    transform: translateX(-100%);
  }
  to {
    transform: translateX(0);
  }
}

.element {
  animation: slide-in 0.5s ease-out;
}
```

### 10. CSS Performance optimizasyonu nasıl yapılır?

**Cevap:**

- Selector optimizasyonu
- Critical CSS
- CSS bundle size optimizasyonu
- will-change property kullanımı
- Layout thrashing'den kaçınma
- GPU acceleration

### 11. Modern CSS özellikleri nelerdir?

**Cevap:**

```css
/* CSS Variables */
:root {
  --primary-color: #007bff;
}

/* CSS Grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

/* CSS Custom Properties */
.theme-dark {
  --bg-color: #1a1a1a;
  --text-color: #ffffff;
}

/* CSS Logical Properties */
.container {
  margin-inline: auto;
  padding-block: 1rem;
}
```

### 12. CSS Hacks ve Browser Compatibility nasıl yönetilir?

**Cevap:**

- Feature queries (@supports)
- Vendor prefixes
- Polyfills
- Fallback değerler
- Modernizr kullanımı

```css
@supports (display: grid) {
  .container {
    display: grid;
  }
}

@supports not (display: grid) {
  .container {
    display: flex;
  }
}
```
