# Vue.js Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. Vue.js nedir ve diğer framework'lerden farkı nedir?

**Cevap:** Vue.js, kullanıcı arayüzü geliştirmek için kullanılan progressif bir JavaScript framework'üdür.

Öne çıkan özellikleri:

- **Küçük boyut ve yüksek performans**: Vue.js'in core kütüphanesi sadece ~33KB'dır (gzip)
- **Kolay öğrenme eğrisi**: HTML, CSS ve JavaScript bilgisiyle hızlıca başlanabilir
- **Reaktif veri yönetimi**: İki yönlü veri bağlama (two-way binding) ve reaktif state yönetimi
- **Component-based mimari**: Yeniden kullanılabilir ve modüler component yapısı
- **Template syntax**: HTML tabanlı, anlaşılır template syntax'ı
- **Virtual DOM**: Performanslı DOM güncellemeleri için Virtual DOM kullanımı
- **Tek dosya component yapısı (SFC)**: Template, script ve style'ı tek dosyada tutabilme

React ve Angular'dan farkları:

- React'a göre daha az boilerplate kod
- Angular'a göre daha hafif ve esnek
- Template ve JSX arasında seçim yapabilme
- State management için built-in çözüm (Vuex)

### 2. Vue instance lifecycle hooks nelerdir ve ne zaman kullanılır?

**Cevap:** Lifecycle hooks, component'in yaşam döngüsündeki belirli aşamalarda çalışan metodlardır:

```javascript
export default {
  beforeCreate() {
    // Component instance oluşturulmadan önce çalışır
    // Henüz data ve events aktif değil
    // Kullanım: Plugin veya global config ayarları
  },
  created() {
    // Component instance oluşturuldu
    // Data ve events aktif, DOM henüz oluşmadı
    // Kullanım: API çağrıları, data initialization
  },
  beforeMount() {
    // DOM'a mount edilmeden hemen önce
    // Template derlenmiş durumda
    // Kullanım: DOM manipülasyonu öncesi işlemler
  },
  mounted() {
    // Component DOM'a mount edildi
    // Tüm child componentler de hazır
    // Kullanım: DOM manipülasyonu, third-party library entegrasyonu
  },
  beforeUpdate() {
    // Data değişti, DOM güncellenmeden önce
    // Güncel DOM'a son erişim noktası
    // Kullanım: DOM güncellenmeden önce yapılacak işlemler
  },
  updated() {
    // DOM güncellendi
    // Kullanım: DOM bağımlı işlemler
  },
  beforeUnmount() {
    // Component kaldırılmadan önce
    // Component hala tam fonksiyonel
    // Kullanım: Cleanup işlemleri (event listener'ları kaldırma vb.)
  },
  unmounted() {
    // Component kaldırıldı
    // Tüm directive'ler bağlantısı kesildi
    // Kullanım: Son cleanup işlemleri
  },
};
```

### 3. Vue 3 Composition API nedir ve Options API'den farkı nedir?

**Cevap:** Composition API, Vue 3 ile gelen, logic organizasyonunu daha iyi yapabilmeyi sağlayan yeni bir API'dir.

Options API vs Composition API karşılaştırması:

```javascript
// Options API
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  computed: {
    doubleCount() {
      return this.count * 2
    }
  }
}

// Composition API
import { ref, computed } from 'vue'

export default {
  setup() {
    // Reactive state
    const count = ref(0)

    // Computed property
    const doubleCount = computed(() => count.value * 2)

    // Method
    const increment = () => {
      count.value++
    }

    // Lifecycle hook
    onMounted(() => {
      console.log('Component mounted')
    })

    // Expose to template
    return {
      count,
      doubleCount,
      increment
    }
  }
}
```

Composition API'nin avantajları:

- Daha iyi TypeScript desteği
- Logic'i daha iyi organize edebilme
- Kod tekrarını azaltma
- Composable fonksiyonlar ile logic paylaşımı
- Bundle size optimizasyonu

### 4. Vue Directive'leri nedir ve nasıl kullanılır?

**Cevap:** Directive'ler, DOM elementlerine özel davranışlar ekleyen özel atribütlerdir.

Built-in Directive'ler:

```html
<!-- v-if: Koşullu render, element tamamen kaldırılır -->
<div v-if="isVisible">Bu element koşul true olduğunda render edilir</div>

<!-- v-show: Koşullu görünürlük, display:none ile gizlenir -->
<div v-show="isVisible">
  Bu element her zaman render edilir, sadece görünürlüğü değişir
</div>

<!-- v-for: Liste render -->
<div v-for="(item, index) in items" :key="item.id">
  {{ index }}: {{ item.name }}
</div>

<!-- v-model: İki yönlü veri bağlama -->
<input v-model="message" />
<!-- = -->
<input :value="message" @input="message = $event.target.value" />

<!-- v-on (@): Event binding -->
<button v-on:click="handleClick">Tıkla</button>
<button @click="handleClick">Kısa syntax</button>

<!-- v-bind (:): Attribute binding -->
<img v-bind:src="imageUrl" />
<img :src="imageUrl" />
<!-- Kısa syntax -->
```

Custom Directive Oluşturma:

```javascript
// Global directive
app.directive('focus', {
  mounted: (el) => el.focus()
})

// Local directive
export default {
  directives: {
    focus: {
      // Directive hooks
      beforeMount(el, binding, vnode, prevVnode) {
        // binding.value ile directive'e geçilen değere erişim
        // binding.arg ile argümana erişim
        // binding.modifiers ile modifier'lara erişim
      },
      mounted(el) {
        el.focus()
      },
      updated(el, binding) {
        // Element veya bağlı değer güncellendiğinde
      }
    }
  }
}

// Kullanımı
<input v-focus>
<input v-focus:arg.modifier="value">
```

## Orta Seviye Sorular

### 5. Vuex nedir ve nasıl kullanılır?

**Cevap:** Vuex, Vue.js uygulamaları için merkezi state yönetim kütüphanesidir.

Temel Kavramlar:

```javascript
// store/index.js
import { createStore } from 'vuex'

export default createStore({
  // State: Uygulamanın merkezi state'i
  state: {
    count: 0,
    todos: [],
    user: null
  },

  // Mutations: State'i değiştiren senkron fonksiyonlar
  mutations: {
    INCREMENT(state) {
      state.count++
    },
    SET_TODOS(state, todos) {
      state.todos = todos
    },
    SET_USER(state, user) {
      state.user = user
    }
  },

  // Actions: Asenkron işlemler ve mutation tetikleyicileri
  actions: {
    async fetchTodos({ commit }) {
      try {
        const response = await api.getTodos()
        commit('SET_TODOS', response.data)
      } catch (error) {
        console.error('Error fetching todos:', error)
      }
    },
    async login({ commit }, credentials) {
      const user = await api.login(credentials)
      commit('SET_USER', user)
    }
  },

  // Getters: State'ten türetilen değerler
  getters: {
    completedTodos: state => {
      return state.todos.filter(todo => todo.completed)
    },
    todoCount: state => state.todos.length,
    isLoggedIn: state => !!state.user
  },

  // Modules: Store'u parçalara ayırma
  modules: {
    auth: authModule,
    products: productsModule
  }
})

// Component içinde kullanımı
import { mapState, mapGetters, mapActions } from 'vuex'

export default {
  computed: {
    // State'e erişim
    ...mapState(['count', 'todos']),
    // Getter'lara erişim
    ...mapGetters(['completedTodos', 'isLoggedIn'])
  },
  methods: {
    // Action'ları çağırma
    ...mapActions(['fetchTodos', 'login']),
    async loadTodos() {
      await this.fetchTodos()
    }
  }
}
```

### 6. Vue Router nasıl kullanılır ve özellikleri nelerdir?

**Cevap:** Vue Router, Vue.js uygulamalarında sayfa yönetimi ve navigasyon için kullanılan resmi router kütüphanesidir.

Temel Özellikler ve Kullanım:

```javascript
import { createRouter, createWebHistory } from "vue-router";

// Route tanımlamaları
const routes = [
  {
    path: "/",
    component: Home,
    name: "home",
  },
  {
    path: "/user/:id",
    component: UserProfile,
    props: true, // URL parametrelerini props olarak geçme
    // Route bazlı guard
    beforeEnter: (to, from) => {
      // return false -> navigasyonu engeller
      // return true -> devam eder
      // return { path: '/login' } -> yönlendirme yapar
    },
    // Nested routes
    children: [
      {
        path: "posts",
        component: UserPosts,
      },
    ],
  },
  {
    path: "/admin",
    component: Admin,
    // Meta fields
    meta: { requiresAuth: true },
    // Lazy loading
    component: () => import("./views/Admin.vue"),
  },
  // 404 sayfası
  {
    path: "/:pathMatch(.*)*",
    component: NotFound,
  },
];

// Router instance
const router = createRouter({
  history: createWebHistory(),
  routes,
  scrollBehavior(to, from, savedPosition) {
    // Sayfa geçişlerinde scroll davranışı
    return savedPosition || { top: 0 };
  },
});

// Global navigation guards
router.beforeEach((to, from, next) => {
  if (to.meta.requiresAuth && !isAuthenticated) {
    next("/login");
  } else {
    next();
  }
});

// Component içinde kullanım
export default {
  methods: {
    goToUser(id) {
      // Programmatik navigasyon
      this.$router.push(`/user/${id}`);
    },
  },
  computed: {
    // Route bilgilerine erişim
    userId() {
      return this.$route.params.id;
    },
  },
};
```

### 7. Props ve Events nasıl kullanılır ve best practice'ler nelerdir?

**Cevap:** Props ve Events, Vue.js'te component'ler arası iletişimi sağlayan temel mekanizmalardır.

Props:

```javascript
// Child.vue
export default {
  props: {
    // Basit prop tanımı
    title: String,

    // Detaylı prop tanımı
    user: {
      type: Object,
      required: true,
      // Default değer (object/array için factory function kullanılmalı)
      default: () => ({}),
      // Özel validation
      validator(value) {
        return value.id && value.name
      }
    },

    // Multiple type
    status: [String, Number],

    // Required prop
    message: {
      type: String,
      required: true
    },

    // Default value
    count: {
      type: Number,
      default: 0
    }
  }
}

// Parent.vue
<template>
  <child-component
    :title="pageTitle"
    :user="currentUser"
    :status="status"
    :message="message"
    :count="count"
  />
</template>
```

Events:

```javascript
// Child.vue
export default {
  methods: {
    // Event emit
    sendUpdate() {
      this.$emit('update', {
        id: 1,
        data: 'New Value'
      })

      // Multiple arguments
      this.$emit('change', value1, value2)
    }
  },
  // Event tanımlama (Vue 3)
  emits: {
    // Basit event listesi
    update: null,

    // Validation ile
    change: (value) => {
      if (!value) return false
      return true
    }
  }
}

// Parent.vue
<template>
  <child-component
    @update="handleUpdate"
    @change="handleChange"
  />
</template>

<script>
export default {
  methods: {
    handleUpdate(payload) {
      console.log(payload.id, payload.data)
    },
    handleChange(value1, value2) {
      // Multiple arguments
    }
  }
}
</script>
```

### 8. Computed, Methods ve Watch arasındaki farklar nelerdir?

**Cevap:** Her biri farklı senaryolar için kullanılan önemli Vue.js özellikleridir:

```javascript
export default {
  data() {
    return {
      firstName: "John",
      lastName: "Doe",
      items: [],
      searchQuery: "",
    };
  },

  // Computed: Bağımlılıklara dayalı hesaplanmış değerler
  computed: {
    // Değer değişmedikçe cache'lenir
    fullName() {
      return `${this.firstName} ${this.lastName}`;
    },
    // Getter ve setter ile
    fullNameWithSetter: {
      get() {
        return `${this.firstName} ${this.lastName}`;
      },
      set(newValue) {
        [this.firstName, this.lastName] = newValue.split(" ");
      },
    },
    // Filtreleme örneği
    filteredItems() {
      return this.items.filter((item) => item.title.includes(this.searchQuery));
    },
  },

  // Methods: Her çağrıldığında çalışan fonksiyonlar
  methods: {
    // Event handler'lar
    handleClick() {
      // Her tıklamada çalışır
    },
    // Veri manipülasyonu
    formatDate(date) {
      return new Date(date).toLocaleDateString();
    },
    // API çağrıları
    async fetchItems() {
      this.items = await api.getItems();
    },
  },

  // Watch: Veri değişikliklerini izleme
  watch: {
    // Basit watch
    searchQuery(newValue, oldValue) {
      // searchQuery değiştiğinde çalışır
      this.fetchSearchResults(newValue);
    },

    // Deep watch
    items: {
      handler(newItems) {
        // items veya alt özellikleri değiştiğinde
        console.log("Items updated:", newItems);
      },
      deep: true,
    },

    // Immediate watch
    $route: {
      handler(newRoute) {
        // Route değişimlerini izle
        this.fetchPageData(newRoute.params.id);
      },
      immediate: true, // Component oluşturulduğunda da çalışır
    },
  },
};
```

Kullanım senaryoları:

- **Computed**: Bir veya birden fazla değişkene bağlı hesaplamalar için
- **Methods**: Event handling ve tekrar kullanılabilir fonksiyonlar için
- **Watch**: Veri değişikliklerinde side effect'ler için (API çağrıları, DOM manipülasyonu vb.)

## İleri Seviye Sorular

### 9. Vue.js'te Performance Optimizasyonu nasıl yapılır?

**Cevap:** Vue.js uygulamalarında performans optimizasyonu için çeşitli teknikler:

1. Lazy Loading:

```javascript
// Component lazy loading
const AdminPanel = () => import("./components/AdminPanel.vue");

// Route lazy loading
const routes = [
  {
    path: "/admin",
    component: () => import("./views/Admin.vue"),
    // Chunk naming
    chunkName: "admin",
  },
];
```

2. Component Caching:

```html
<!-- Keep-alive ile component cache -->
<keep-alive>
  <component :is="currentComponent" />
</keep-alive>

<!-- Include/exclude belirli componentler -->
<keep-alive :include="['ComponentA', 'ComponentB']">
  <router-view />
</keep-alive>
```

3. v-show vs v-if Kullanımı:

```html
<!-- v-show: Sık değişen içerik için (display: none ile gizler) -->
<div v-show="isVisible">Sık değişen, ama DOM'da kalması gereken içerik</div>

<!-- v-if: Nadir değişen içerik için (DOM'dan kaldırır) -->
<div v-if="isVisible">Nadir değişen veya ağır component'ler</div>
```

4. Büyük Listeler için Virtual Scrolling:

```html
<virtual-list :items="items" :height="400" :item-height="40">
  <template v-slot:item="{ item }">
    <div class="item">{{ item.name }}</div>
  </template>
</virtual-list>
```

5. Computed Property Optimizasyonu:

```javascript
export default {
  computed: {
    // Pahalı işlemler için computed cache
    expensiveComputation: {
      cache: false, // Cache'i devre dışı bırakma
      get() {
        return this.items.filter(/* karmaşık filtreleme */);
      },
    },
  },
};
```

### 10. Custom Plugin Geliştirme

**Cevap:** Vue.js plugin'leri, uygulamaya global özellikler eklemek için kullanılır:

```javascript
// plugins/toast.js
export default {
  install: (app, options = {}) => {
    // Global property ekleme
    app.config.globalProperties.$toast = (message) => {
      // Toast implementation
    };

    // Global component
    app.component("Toast", ToastComponent);

    // Directive ekleme
    app.directive("toast", {
      mounted(el, binding) {
        // Directive implementation
      },
    });

    // Provide/Inject için değer sağlama
    app.provide("toast", {
      show: (message) => {
        // Toast implementation
      },
    });

    // Mixin ekleme
    app.mixin({
      mounted() {
        // Mixin logic
      },
    });
  },
};

// Plugin kullanımı
import ToastPlugin from "./plugins/toast";

const app = createApp(App);
app.use(ToastPlugin, {
  duration: 3000,
  position: "top-right",
});
```

### 11. Composables Pattern ve Best Practices

**Cevap:** Composables, logic'i paylaşılabilir fonksiyonlara ayırma pattern'idir:

```javascript
// composables/useCounter.js
import { ref, computed, onMounted, onUnmounted } from "vue";

export function useCounter(initialValue = 0) {
  // State
  const count = ref(initialValue);

  // Computed
  const doubleCount = computed(() => count.value * 2);

  // Methods
  function increment() {
    count.value++;
  }

  function decrement() {
    count.value--;
  }

  // Lifecycle hooks
  onMounted(() => {
    console.log("Counter mounted");
  });

  onUnmounted(() => {
    console.log("Counter unmounted");
  });

  // Expose managed state
  return {
    count,
    doubleCount,
    increment,
    decrement,
  };
}

// composables/useFetch.js
export function useFetch(url) {
  const data = ref(null);
  const error = ref(null);
  const loading = ref(false);

  async function fetchData() {
    loading.value = true;
    try {
      const response = await fetch(url);
      data.value = await response.json();
    } catch (e) {
      error.value = e;
    } finally {
      loading.value = false;
    }
  }

  onMounted(fetchData);

  return { data, error, loading, refresh: fetchData };
}

// Component kullanımı
import { useCounter, useFetch } from "@/composables";

export default {
  setup() {
    // Counter logic
    const { count, increment } = useCounter(10);

    // Fetch logic
    const { data, loading, error } = useFetch("/api/data");

    return {
      count,
      increment,
      data,
      loading,
      error,
    };
  },
};
```

### 12. Unit Testing Best Practices

**Cevap:** Vue.js component'lerinin test edilmesi:

```javascript
import { mount, shallowMount } from "@vue/test-utils";
import Counter from "@/components/Counter.vue";

describe("Counter.vue", () => {
  // Component mounting
  test("mounts component", () => {
    const wrapper = mount(Counter);
    expect(wrapper.exists()).toBe(true);
  });

  // Props testing
  test("renders props correctly", () => {
    const wrapper = mount(Counter, {
      props: {
        initialCount: 5,
      },
    });
    expect(wrapper.text()).toContain("5");
  });

  // User interaction
  test("increments counter when button is clicked", async () => {
    const wrapper = mount(Counter);
    const button = wrapper.find("button");
    const text = wrapper.find("p");

    expect(text.text()).toContain("0");

    await button.trigger("click");

    expect(text.text()).toContain("1");
  });

  // Events testing
  test("emits update event", () => {
    const wrapper = mount(Counter);
    wrapper.vm.$emit("update", 15);

    expect(wrapper.emitted().update[0]).toEqual([15]);
  });

  // Slots testing
  test("renders default slot content", () => {
    const wrapper = mount(Counter, {
      slots: {
        default: "Counter Value",
      },
    });
    expect(wrapper.text()).toContain("Counter Value");
  });

  // Vuex testing
  test("works with vuex store", () => {
    const store = createStore({
      state: {
        count: 0,
      },
      mutations: {
        increment: (state) => state.count++,
      },
    });

    const wrapper = mount(Counter, {
      global: {
        plugins: [store],
      },
    });
  });

  // Router testing
  test("works with router", () => {
    const router = createRouter({
      history: createWebHistory(),
      routes: [],
    });

    const wrapper = mount(Counter, {
      global: {
        plugins: [router],
      },
    });
  });
});
```

Bu detaylı açıklamalar, Vue.js'in temel ve ileri seviye konularını daha iyi anlamanıza yardımcı olacaktır. Her bir konu için pratik örnekler ve best practice'ler eklenmiştir.
