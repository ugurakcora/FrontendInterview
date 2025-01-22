# Context API Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. Context API nedir ve ne zaman kullanılmalıdır?

**Cevap:** Context API, React'ta prop drilling sorununu çözmek için kullanılan bir state yönetim çözümüdür. Özellikle:

- Global state yönetimi gerektiren durumlarda
- Tema değişimi gibi uygulama genelinde paylaşılan verilerde
- Dil değişimi gibi kullanıcı tercihlerinde
- Authentication bilgisi gibi birçok componentin erişmesi gereken durumlarda kullanılır

### 2. Context API'nin temel bileşenleri nelerdir?

**Cevap:**

- `createContext`: Context oluşturmak için kullanılır
- `Provider`: Context değerlerini sağlar
- `Consumer`: Context değerlerine erişim sağlar
- `useContext`: Hook olarak context'e erişim sağlar

### 3. Context API vs Props drilling nedir?

**Cevap:** Props drilling, verilerin üst componentten alt componente kadar her seviyede prop olarak geçilmesidir. Context API, bu zincirleme prop geçişini ortadan kaldırır ve verilere doğrudan erişim sağlar.

## Orta Seviye Sorular

### 4. Context API'de performans optimizasyonu nasıl yapılır?

**Cevap:**

- Context'i küçük parçalara bölme
- Gereksiz render'ları önlemek için `useMemo` ve `useCallback` kullanımı
- Context değerlerini mümkün olduğunca alt seviyelerde tutma
- Multiple context kullanımı

### 5. Context API'de state güncellemesi nasıl yapılır?

**Cevap:**

```jsx
const MyContext = createContext();

function MyProvider({ children }) {
  const [state, setState] = useState(initialState);

  const updateState = useCallback((newValue) => {
    setState((prev) => ({ ...prev, ...newValue }));
  }, []);

  return (
    <MyContext.Provider value={{ state, updateState }}>
      {children}
    </MyContext.Provider>
  );
}
```

### 6. Context API'de type safety nasıl sağlanır?

**Cevap:** TypeScript ile context tanımlarken interface veya type kullanılarak:

```typescript
interface MyContextType {
  user: User;
  updateUser: (user: User) => void;
}

const MyContext = createContext<MyContextType | undefined>(undefined);
```

## İleri Seviye Sorular

### 7. Multiple Context kullanımının avantajları ve dezavantajları nelerdir?

**Cevap:**
Avantajlar:

- Daha granüler kontrol
- Gereksiz render'ların önlenmesi
- Daha iyi performans

Dezavantajlar:

- Kod karmaşıklığı artabilir
- Context Provider wrapper sayısı artar
- Yönetimi zorlaşabilir

### 8. Context API'de memoization nasıl kullanılır?

**Cevap:**

```jsx
const MyContext = createContext();

function MyProvider({ children }) {
  const [state, setState] = useState(initialState);

  const value = useMemo(
    () => ({
      state,
      updateState: (newValue) => setState((prev) => ({ ...prev, ...newValue })),
    }),
    [state]
  );

  return <MyContext.Provider value={value}>{children}</MyContext.Provider>;
}
```

### 9. Context API ile global error handling nasıl yapılır?

**Cevap:**

```jsx
const ErrorContext = createContext();

function ErrorProvider({ children }) {
  const [error, setError] = useState(null);

  const handleError = useCallback((err) => {
    setError(err);
    // Hata loglama, kullanıcı bildirimi vb.
  }, []);

  return (
    <ErrorContext.Provider value={{ error, handleError }}>
      {children}
    </ErrorContext.Provider>
  );
}
```

### 10. Context API'de nested providers nasıl yönetilir?

**Cevap:**

- Compose Providers pattern kullanımı
- Higher Order Component oluşturma
- Custom Provider component oluşturma

```jsx
const ComposeProviders = ({ providers, children }) => {
  return providers.reduceRight(
    (acc, Provider) => <Provider>{acc}</Provider>,
    children
  );
};
```
