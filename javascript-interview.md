# JavaScript Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. var, let ve const arasındaki farklar nelerdir?

**Cevap:**

- `var`: Function-scoped, hoisting özelliği var
- `let`: Block-scoped, hoisting yok, tekrar tanımlanabilir
- `const`: Block-scoped, hoisting yok, değeri değiştirilemez (ama obje içeriği değiştirilebilir)

### 2. Closure nedir?

**Cevap:** Bir fonksiyonun kendi scope'u dışındaki değişkenlere erişebilme özelliğidir. İç fonksiyon, dış fonksiyonun değişkenlerine erişebilir ve bu değişkenleri "hatırlar".

### 3. Event bubbling ve event capturing nedir?

**Cevap:**

- Event bubbling: Event'in en içteki elementten dışa doğru ilerlemesi
- Event capturing: Event'in en dıştaki elementten içe doğru ilerlemesi
- `addEventListener`'ın üçüncü parametresi ile kontrol edilir

### 4. this keyword'ü nedir ve nasıl çalışır?

**Cevap:** `this`, çağrıldığı context'e göre değeri değişen bir keyword'dür:

- Global scope'da window objesini
- Metod içinde objeyi
- Constructor'da yeni oluşturulan instance'ı
- Event handler'da event'i tetikleyen elementi gösterir

### 5. Promise nedir ve callback'lerden farkı nedir?

**Cevap:** Promise, asenkron işlemleri yönetmek için kullanılan bir objedir. Callback hell'i önler ve `.then()`, `.catch()`, `.finally()` metodları ile daha okunabilir kod yazılmasını sağlar.

## Orta Seviye Sorular

### 6. Prototypal inheritance nasıl çalışır?

**Cevap:** JavaScript'te her obje bir prototype'a sahiptir ve bu prototype zinciri sayesinde kalıtım sağlanır. Bir obje, kendi prototype'ındaki özelliklere ve metodlara erişebilir.

### 7. Event loop nedir?

**Cevap:** JavaScript'in asenkron işlemleri yönetme mekanizmasıdır:

- Call stack
- Callback queue
- Microtask queue
- Event loop bu kuyrukları yönetir

### 8. Map ve Set veri yapıları ne işe yarar?

**Cevap:**

- `Map`: Key-value pairs, herhangi bir tip key kullanılabilir
- `Set`: Unique değerler koleksiyonu
- Her ikisi de iterasyon ve size yönetimi için built-in metodlar sunar

### 9. async/await nedir ve Promise'lerden farkı nedir?

**Cevap:** async/await, Promise'leri daha senkron görünümlü kod yazarak kullanmamızı sağlayan syntax sugar'dır. Kod okunabilirliğini artırır ve hata yönetimini try/catch ile yapabilmeyi sağlar.

## İleri Seviye Sorular

### 10. Memory leak'ler nasıl oluşur ve nasıl önlenir?

**Cevap:**

- Gereksiz global değişkenler
- Unutulan event listener'lar
- Kapatılmayan timer'lar
- Döngüsel referanslar
  Bu durumları engellemek için cleanup yapmak gerekir.

### 11. Web Workers nedir ve ne için kullanılır?

**Cevap:** Ana thread'i bloklamadan arka planda işlem yapmayı sağlayan JavaScript API'ıdır. Hesaplama yoğun işlemler için kullanılır.

### 12. JavaScript Modules (ESM) nedir?

**Cevap:** Modern JavaScript'te kod organizasyonu için kullanılan sistemdir:

- `import` ve `export` statement'ları
- Kod modülerliği
- Tree shaking imkanı
- Scope isolation

### 13. Generators ve Iterators nasıl çalışır?

**Cevap:**

- Generator'lar `function*` syntax'ı ile tanımlanır
- `yield` keyword'ü ile değer üretir
- İterasyon kontrolü sağlar
- Lazy evaluation imkanı verir

### 14. TypeScript ile JavaScript arasındaki temel farklar nelerdir?

**Cevap:**

- Static typing
- Interface ve Type tanımlama
- Generics
- Decorators
- Access modifiers
- Compile-time type checking
