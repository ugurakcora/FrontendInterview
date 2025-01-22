# React Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. React nedir ve neden kullanılır?

**Cevap:** React, Facebook tarafından geliştirilen açık kaynaklı bir JavaScript kütüphanesidir. Kullanıcı arayüzü oluşturmak için kullanılır. Component-based yapısı, Virtual DOM kullanımı ve tek yönlü veri akışı gibi özellikleri sayesinde performanslı ve yönetilebilir uygulamalar geliştirmeyi sağlar.

### 2. Virtual DOM nedir?

**Cevap:** Virtual DOM, gerçek DOM'un hafızada tutulan sanal bir kopyasıdır. React, değişiklikleri önce Virtual DOM üzerinde yapar, sonra gerçek DOM ile karşılaştırır ve sadece değişen kısımları günceller. Bu yaklaşım performansı artırır.

### 3. Component'ler arası veri aktarımı nasıl yapılır?

**Cevap:**

- Props ile üst componentten alt componente
- Context API ile global state yönetimi
- Redux, Zustand gibi state management araçları ile
- Callback fonksiyonları ile alt componentten üst componente

### 4. useEffect Hook'u ne işe yarar?

**Cevap:** useEffect, component lifecycle'ını yönetmek için kullanılır. Componentin mount, update ve unmount durumlarında yan etkileri (side effects) yönetmemizi sağlar.

### 5. useState ve useRef arasındaki fark nedir?

**Cevap:**

- useState re-render tetikler, useRef tetiklemez
- useState her render'da yeni bir değer oluşturur, useRef aynı referansı korur
- useState anlık değeri tutar, useRef değeri mutate edebilir

## Orta Seviye Sorular

### 6. React'ta performans optimizasyonu nasıl yapılır?

**Cevap:**

- React.memo ile gereksiz render'ları önleme
- useCallback ve useMemo kullanımı
- Code splitting ve lazy loading
- Key prop'larının doğru kullanımı
- Virtual scrolling büyük listeler için

### 7. Custom Hook nedir? Neden kullanılır?

**Cevap:** Custom Hook'lar, logic'i componentler arasında paylaşmak için kullanılan özel JavaScript fonksiyonlarıdır. "use" prefix'i ile başlarlar ve React Hook kurallarına uyarlar.

### 8. React'ta state yönetimi yaklaşımları nelerdir?

**Cevap:**

- Local state (useState)
- Context API
- Redux
- Zustand
- Recoil
- Jotai

## İleri Seviye Sorular

### 9. React Fiber nedir?

**Cevap:** React'ın yeni reconciliation motoru olup, render işlemini bölebilen ve önceliklendiren bir yapıdır. Animasyonlar ve kullanıcı etkileşimleri için daha akıcı bir deneyim sağlar.

### 10. Error Boundary nedir?

**Cevap:** Alt componentlerde oluşan JavaScript hatalarını yakalayan ve hata durumunda fallback UI gösterebilen component'lerdir. Prodüksiyonda hataların kullanıcı deneyimini bozmasını engeller.

### 11. Server Components ile Client Components arasındaki fark nedir?

**Cevap:**

- Server Components sunucuda render edilir
- Bundle size'ı etkilemez
- JavaScript interaktivitesi içermez
- Veri tabanına direkt erişebilir

### 12. Concurrent Mode nedir?

**Cevap:** React'ın render işlemlerini bölebilme ve önceliklendirme yeteneğidir. Kullanıcı deneyimini iyileştirmek için uzun süren render işlemlerini böler ve kullanıcı etkileşimlerine öncelik verir.
