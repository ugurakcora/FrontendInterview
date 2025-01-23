# React Query Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. React Query nedir ve neden kullanılmalıdır?

**Cevap:** React Query, server state yönetimi için kullanılan güçlü bir kütüphanedir. Özellikle:

- Veri fetching, caching ve senkronizasyon
- Otomatik background updates
- Pagination ve infinite scroll
- Optimistic updates
- Error handling
  gibi özellikleri built-in olarak sunar.

### 2. React Query'nin temel kavramları nelerdir?

**Cevap:**

- Queries: Veri okuma işlemleri
- Mutations: Veri yazma/güncelleme işlemleri
- Query Invalidation: Cache'in yenilenmesi
- Query Cache: Veri önbellekleme
- Stale Time: Verinin "bayat" sayılma süresi
- Cache Time: Verinin cache'te tutulma süresi

### 3. useQuery hook'u nasıl kullanılır?

**Cevap:**

```javascript
const { data, isLoading, error } = useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
  staleTime: 5000,
  cacheTime: 300000,
});
```

### 4. React Query'de error handling nasıl yapılır?

**Cevap:**

```javascript
const { data, error, isError, isLoading } = useQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
  retry: 3,
  onError: (error) => {
    console.log("Error fetching todos:", error);
  },
});
```

## Orta Seviye Sorular

### 5. Query Invalidation ne demektir ve nasıl kullanılır?

**Cevap:**

```javascript
const queryClient = useQueryClient();

// Belirli bir query'yi invalide etme
queryClient.invalidateQueries({ queryKey: ["todos"] });

// Prefix ile eşleşen tüm query'leri invalide etme
queryClient.invalidateQueries({ queryKey: ["todos"] });
```

### 6. Optimistic Updates nasıl yapılır?

**Cevap:**

```javascript
const mutation = useMutation({
  mutationFn: updateTodo,
  onMutate: async (newTodo) => {
    await queryClient.cancelQueries({ queryKey: ["todos"] });
    const previousTodos = queryClient.getQueryData(["todos"]);

    queryClient.setQueryData(["todos"], (old) => [...old, newTodo]);

    return { previousTodos };
  },
  onError: (err, newTodo, context) => {
    queryClient.setQueryData(["todos"], context.previousTodos);
  },
});
```

### 7. Infinite Queries nasıl kullanılır?

**Cevap:**

```javascript
const { data, fetchNextPage, hasNextPage, isFetchingNextPage } =
  useInfiniteQuery({
    queryKey: ["projects"],
    queryFn: fetchProjectPage,
    getNextPageParam: (lastPage) => lastPage.nextCursor,
  });
```

### 8. Parallel Queries nasıl yapılır?

**Cevap:**

```javascript
const results = useQueries({
  queries: userIds.map((id) => ({
    queryKey: ["user", id],
    queryFn: () => fetchUserById(id),
  })),
});
```

## İleri Seviye Sorular

### 9. Custom Hooks ile React Query nasıl kullanılır?

**Cevap:**

```javascript
function useTodos() {
  return useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodos,
    select: (data) => data.sort((a, b) => b.id - a.id),
    staleTime: 5 * 60 * 1000,
  });
}

function useUpdateTodo() {
  const queryClient = useQueryClient();
  return useMutation({
    mutationFn: updateTodo,
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["todos"] });
    },
  });
}
```

### 10. Prefetching ve Preloading nasıl yapılır?

**Cevap:**

```javascript
const queryClient = useQueryClient();

// Prefetching
await queryClient.prefetchQuery({
  queryKey: ["todos"],
  queryFn: fetchTodos,
});

// Preloading data
queryClient.setQueryData(["todos"], todos);
```

### 11. Suspense mode nasıl kullanılır?

**Cevap:**

```javascript
function TodoList() {
  return (
    <Suspense fallback={<Loading />}>
      <Todos />
    </Suspense>
  );
}

function Todos() {
  const { data } = useQuery({
    queryKey: ["todos"],
    queryFn: fetchTodos,
    suspense: true,
  });

  return <div>{/* render todos */}</div>;
}
```

### 12. React Query DevTools nasıl kullanılır?

**Cevap:**

```javascript
import { ReactQueryDevtools } from "@tanstack/react-query-devtools";

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* Your app */}
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  );
}
```

### 13. Offline Support nasıl sağlanır?

**Cevap:**

```javascript
const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 3,
      staleTime: Infinity,
      cacheTime: Infinity,
      refetchOnWindowFocus: false,
      refetchOnReconnect: false,
    },
  },
});

// Offline mutations
const mutation = useMutation({
  mutationFn: updateTodo,
  onMutate: async (variables) => {
    // Optimistic update
  },
  retry: 3,
  retryDelay: (attemptIndex) => Math.min(1000 * 2 ** attemptIndex, 30000),
});
```
