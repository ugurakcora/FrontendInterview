# Redux Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. Redux nedir ve ne zaman kullanılmalıdır?

**Cevap:** Redux, JavaScript uygulamaları için öngörülebilir bir state yönetim kütüphanesidir. Özellikle:

- Büyük ölçekli uygulamalarda
- Karmaşık state yönetimi gerektiren durumlarda
- Birden fazla componentin aynı state'i kullandığı durumlarda
- State değişimlerinin takip edilmesi gereken durumlarda kullanılır

### 2. Redux'ın temel prensipleri nelerdir?

**Cevap:**

- Single source of truth (Tek bir store)
- State is read-only (State sadece okunabilir)
- Changes are made with pure functions (Değişiklikler pure reducer'lar ile yapılır)

### 3. Redux'ın temel bileşenleri nelerdir?

**Cevap:**

- Store: Uygulamanın state'ini tutan obje
- Action: State değişikliği için gönderilen objeler
- Reducer: State'i güncelleyen pure fonksiyonlar
- Dispatch: Action'ları store'a gönderen fonksiyon

## Orta Seviye Sorular

### 4. Redux Toolkit nedir ve klasik Redux'tan farkları nelerdir?

**Cevap:**
Redux Toolkit, Redux'ın resmi, opinionated toolset'idir:

- Daha az boilerplate kod
- Built-in ImmerJS desteği
- createSlice API
- Built-in Thunk middleware
- DevTools entegrasyonu

### 5. Redux Middleware nedir ve nasıl kullanılır?

**Cevap:** Middleware, action'lar dispatch edildiğinde reducer'a ulaşmadan önce araya giren fonksiyonlardır:

```javascript
const logger = (store) => (next) => (action) => {
  console.log("dispatching", action);
  let result = next(action);
  console.log("next state", store.getState());
  return result;
};
```

### 6. Redux Thunk nedir ve ne için kullanılır?

**Cevap:** Redux Thunk, asenkron işlemleri yönetmek için kullanılan bir middleware'dir:

```javascript
const fetchUser = (id) => async (dispatch) => {
  dispatch({ type: "FETCH_USER_REQUEST" });
  try {
    const response = await api.fetchUser(id);
    dispatch({ type: "FETCH_USER_SUCCESS", payload: response.data });
  } catch (error) {
    dispatch({ type: "FETCH_USER_FAILURE", error });
  }
};
```

## İleri Seviye Sorular

### 7. Redux Saga vs Redux Thunk: Hangisi ne zaman kullanılmalı?

**Cevap:**
Redux Thunk:

- Basit asenkron işlemler için
- Hızlı geliştirme gereken durumlar
- Küçük/orta ölçekli projeler

Redux Saga:

- Karmaşık asenkron işlemler
- İş akışı kontrolü gereken durumlar
- Test edilebilirlik önemli olduğunda
- Büyük ölçekli projeler

### 8. Redux'ta performans optimizasyonu nasıl yapılır?

**Cevap:**

- Reselect ile memoized selector'lar kullanma
- Normalize edilmiş state yapısı
- Gereksiz render'ları önlemek için React.memo kullanımı
- Action batch işlemleri
- Code splitting ve lazy loading

### 9. Redux DevTools nasıl kullanılır ve debugging sürecine katkısı nedir?

**Cevap:**

- State değişimlerini izleme
- Time-travel debugging
- Action history
- State diff görüntüleme
- Network isteklerini izleme

### 10. Redux ile büyük ölçekli uygulama mimarisi nasıl oluşturulur?

**Cevap:**

- Feature-based folder structure
- Duck pattern veya Re-ducks pattern kullanımı
- Slice'ların modüler organizasyonu
- Type-safety için TypeScript kullanımı

```javascript
// Feature based structure
src / features / auth / authSlice.js;
authSelectors.js;
authSaga.js;
products / productsSlice.js;
productsSelectors.js;
productsSaga.js;
```

### 11. Redux-Persist nasıl kullanılır?

**Cevap:**

```javascript
const persistConfig = {
  key: "root",
  storage,
  whitelist: ["auth", "settings"],
};

const persistedReducer = persistReducer(persistConfig, rootReducer);
const store = configureStore({
  reducer: persistedReducer,
  middleware: [thunk],
});

const persistor = persistStore(store);
```

### 12. RTK Query nedir ve ne için kullanılır?

**Cevap:** RTK Query, Redux Toolkit'in data fetching ve caching çözümüdür:

- Otomatik caching ve invalidation
- Polling ve real-time updates
- Optimistic updates
- Type safety
- DevTools entegrasyonu
