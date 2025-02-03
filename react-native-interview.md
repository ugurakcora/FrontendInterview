# React Native Mülakat Soruları ve Cevapları

## Temel Sorular

### 1. React Native nedir ve nasıl çalışır?

**Cevap:** React Native, Facebook tarafından geliştirilen, native mobil uygulamalar geliştirmek için kullanılan bir framework'tür.

Temel özellikleri:

- **Cross-platform**: Tek kod tabanıyla iOS ve Android için native uygulama geliştirme
- **JavaScript/React**: Web React bilgisiyle mobil uygulama geliştirebilme
- **Hot Reloading**: Anlık kod değişikliklerini görebilme
- **Native Bileşenler**: Platform spesifik native UI bileşenleri
- **Bridge Mimarisi**: JS ve Native kod arasındaki iletişimi sağlama
- **Native Modüller**: Native özelliklere doğrudan erişim

Web React'tan farkları:

- DOM yerine native bileşenler kullanır (`<View>`, `<Text>`, `<Image>` vb.)
- CSS yerine StyleSheet API kullanır
- Platform spesifik kodlar yazılabilir
- Native modüller ile cihaz özelliklerine erişim sağlar

### 2. Core Components nelerdir?

**Cevap:** React Native'in temel bileşenleri:

```jsx
// Temel Layout Components
<View>  // div benzeri container
<ScrollView>  // scroll özellikli container
<SafeAreaView>  // güvenli alan için container
<FlatList>  // performanslı liste görünümü

// Temel UI Components
<Text>  // metin gösterimi
<Image>  // resim gösterimi
<TextInput>  // input alanı
<TouchableOpacity>  // dokunma efektli buton
<Pressable>  // modern dokunma komponenti
<Button>  // platform spesifik buton

// Örnek Kullanım
import { View, Text, StyleSheet } from 'react-native';

const MyComponent = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello React Native</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center'
  },
  text: {
    fontSize: 20,
    color: 'black'
  }
});
```

### 3. Flexbox Layout nasıl çalışır?

**Cevap:** React Native'de layout yönetimi Flexbox ile yapılır:

```jsx
const styles = StyleSheet.create({
  // Ana Container
  container: {
    flex: 1, // Tüm alanı kapla
    flexDirection: "column", // Dikey yönlendirme (default)
    justifyContent: "center", // Dikey hizalama
    alignItems: "center", // Yatay hizalama
  },

  // Row Layout
  row: {
    flexDirection: "row", // Yatay yönlendirme
    justifyContent: "space-between", // Elemanlar arası boşluk
    alignItems: "center",
  },

  // Nested Flex
  box: {
    flex: 1, // Oransal alan kullanımı
    padding: 10,
    margin: 5,
  },

  // Absolute Positioning
  overlay: {
    position: "absolute",
    top: 0,
    left: 0,
    right: 0,
    bottom: 0,
  },
});

// Kullanım örneği
const Layout = () => (
  <View style={styles.container}>
    <View style={styles.row}>
      <View style={[styles.box, { backgroundColor: "red" }]} />
      <View style={[styles.box, { backgroundColor: "blue" }]} />
    </View>
    <View style={styles.overlay}>
      <Text>Overlay Content</Text>
    </View>
  </View>
);
```

### 4. Platform Spesifik Kod nasıl yazılır?

**Cevap:** React Native'de platform spesifik kod yazmanın birkaç yolu vardır:

```jsx
// 1. Platform.select kullanımı
import { Platform, StyleSheet } from "react-native";

const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        shadowColor: "black",
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.25,
      },
      android: {
        elevation: 5,
      },
    }),
  },
});

// 2. Platform.OS kontrolü
const MyComponent = () => {
  const buttonColor = Platform.OS === "ios" ? "blue" : "#2196F3";
  return <Button color={buttonColor} />;
};

// 3. Platform spesifik dosyalar
// MyComponent.ios.js
// MyComponent.android.js
import MyComponent from "./MyComponent"; // Otomatik doğru dosyayı alır

// 4. Platform spesifik API'ler
if (Platform.OS === "ios") {
  // iOS spesifik kod
} else {
  // Android spesifik kod
}
```

## Orta Seviye Sorular

### 5. Navigation nasıl yapılır?

**Cevap:** React Navigation, React Native'de en popüler navigasyon çözümüdür:

```jsx
// Navigation kurulumu
import { NavigationContainer } from "@react-navigation/native";
import { createStackNavigator } from "@react-navigation/stack";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";

const Stack = createStackNavigator();
const Tab = createBottomTabNavigator();

// Stack Navigator
const AppNavigator = () => (
  <NavigationContainer>
    <Stack.Navigator>
      <Stack.Screen
        name="Home"
        component={HomeScreen}
        options={{
          title: "Ana Sayfa",
          headerStyle: {
            backgroundColor: "#f4511e",
          },
          headerTintColor: "#fff",
        }}
      />
      <Stack.Screen name="Details" component={DetailsScreen} />
    </Stack.Navigator>
  </NavigationContainer>
);

// Tab Navigator
const TabNavigator = () => (
  <Tab.Navigator>
    <Tab.Screen
      name="Home"
      component={HomeScreen}
      options={{
        tabBarIcon: ({ color, size }) => (
          <Icon name="home" color={color} size={size} />
        ),
      }}
    />
    <Tab.Screen name="Profile" component={ProfileScreen} />
  </Tab.Navigator>
);

// Screen içinde kullanım
const HomeScreen = ({ navigation, route }) => {
  return (
    <View>
      <Button
        title="Details'a Git"
        onPress={() => navigation.navigate("Details", { id: 123 })}
      />
      <Button title="Geri Git" onPress={() => navigation.goBack()} />
    </View>
  );
};

// Route params kullanımı
const DetailsScreen = ({ route }) => {
  const { id } = route.params;
  return <Text>Details Screen: {id}</Text>;
};
```

### 6. State Management nasıl yapılır?

**Cevap:** React Native'de birkaç state yönetim çözümü vardır:

```jsx
// 1. Redux Toolkit kullanımı
import { configureStore, createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
  },
});

const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
  },
});

// Component kullanımı
import { useSelector, useDispatch } from "react-redux";

const CounterComponent = () => {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <View>
      <Text>{count}</Text>
      <Button onPress={() => dispatch(increment())} title="Artır" />
    </View>
  );
};

// 2. Context API kullanımı
const AppContext = React.createContext();

const AppProvider = ({ children }) => {
  const [state, setState] = useState(initialState);

  return (
    <AppContext.Provider value={{ state, setState }}>
      {children}
    </AppContext.Provider>
  );
};

// 3. Zustand kullanımı
import create from "zustand";

const useStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
}));
```

### 7. Performance Optimizasyonu nasıl yapılır?

**Cevap:**

```jsx
// 1. FlatList Optimizasyonu
<FlatList
  data={items}
  renderItem={({ item }) => <ItemComponent item={item} />}
  keyExtractor={item => item.id}
  initialNumToRender={10}
  maxToRenderPerBatch={10}
  windowSize={5}
  removeClippedSubviews={true}
  getItemLayout={(data, index) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  })}
/>

// 2. useMemo ve useCallback kullanımı
const MemoizedComponent = React.memo(({ data, onPress }) => {
  return <TouchableOpacity onPress={onPress}><Text>{data}</Text></TouchableOpacity>
});

const ParentComponent = () => {
  const data = useMemo(() => expensiveCalculation(), []);
  const handlePress = useCallback(() => {
    // handle press
  }, []);

  return <MemoizedComponent data={data} onPress={handlePress} />;
};

// 3. Image Optimizasyonu
<Image
  source={{ uri: imageUrl }}
  style={{ width: 100, height: 100 }}
  resizeMode="cover"
  fadeDuration={300}
  onLoadStart={() => setLoading(true)}
  onLoadEnd={() => setLoading(false)}
/>

// 4. Lazy Loading
const MyLazyComponent = React.lazy(() => import('./MyComponent'));

// 5. Hermes Engine Kullanımı
// android/app/build.gradle
def enableHermes = true
```

### 8. Native Modüller nasıl yazılır?

**Cevap:**

```jsx
// iOS Native Modül (Swift)
@objc(CalendarManager)
class CalendarManager: NSObject {
  @objc
  func addEvent(_ name: String, location: String, date: Date) {
    // Native implementation
  }

  @objc
  static func requiresMainQueueSetup() -> Bool {
    return true
  }
}

// Android Native Modül (Kotlin)
class CalendarModule(reactContext: ReactApplicationContext) :
  ReactContextBaseJavaModule(reactContext) {

  override fun getName() = "CalendarManager"

  @ReactMethod
  fun addEvent(name: String, location: String, date: Double) {
    // Native implementation
  }
}

// JavaScript Bridge
import { NativeModules } from 'react-native';
const { CalendarManager } = NativeModules;

// Kullanım
CalendarManager.addEvent(
  'Birthday Party',
  'My House',
  new Date().getTime()
);
```

## İleri Seviye Sorular

### 9. Debugging ve Testing nasıl yapılır?

**Cevap:**

```jsx
// 1. Jest ile Unit Testing
import { render, fireEvent } from "@testing-library/react-native";

describe("MyComponent", () => {
  it("renders correctly", () => {
    const { getByText } = render(<MyComponent />);
    expect(getByText("Hello")).toBeTruthy();
  });

  it("handles press events", () => {
    const onPress = jest.fn();
    const { getByText } = render(<MyComponent onPress={onPress} />);
    fireEvent.press(getByText("Press Me"));
    expect(onPress).toHaveBeenCalled();
  });
});

// 2. E2E Testing (Detox)
describe("Example", () => {
  beforeEach(async () => {
    await device.reloadReactNative();
  });

  it("should show welcome screen", async () => {
    await expect(element(by.id("welcome"))).toBeVisible();
  });
});

// 3. Performance Testing
import { PerformanceObserver, performance } from "react-native";

const obs = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  entries.forEach((entry) => {
    console.log(`${entry.name}: ${entry.duration}`);
  });
});
obs.observe({ entryTypes: ["measure"] });

// 4. Error Boundary
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Log error to service
  }

  render() {
    if (this.state.hasError) {
      return <Text>Something went wrong</Text>;
    }
    return this.props.children;
  }
}
```

### 10. Animasyonlar nasıl yapılır?

**Cevap:**

```jsx
// 1. Animated API
import { Animated } from "react-native";

const FadeInView = () => {
  const fadeAnim = useRef(new Animated.Value(0)).current;

  useEffect(() => {
    Animated.timing(fadeAnim, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true,
    }).start();
  }, []);

  return (
    <Animated.View style={{ opacity: fadeAnim }}>
      <Text>Fade In</Text>
    </Animated.View>
  );
};

// 2. Reanimated 2
import Animated, {
  useAnimatedStyle,
  withSpring,
  useSharedValue,
} from "react-native-reanimated";

const AnimatedComponent = () => {
  const offset = useSharedValue(0);

  const animatedStyles = useAnimatedStyle(() => {
    return {
      transform: [{ translateX: offset.value }],
    };
  });

  return (
    <Animated.View style={animatedStyles}>
      <Text>Animated Content</Text>
    </Animated.View>
  );
};

// 3. Gesture Handler ile Animasyon
import { PanGestureHandler } from "react-native-gesture-handler";

const DraggableCard = () => {
  const translateX = useSharedValue(0);
  const translateY = useSharedValue(0);

  const gestureHandler = useAnimatedGestureHandler({
    onStart: (_, ctx) => {
      ctx.startX = translateX.value;
      ctx.startY = translateY.value;
    },
    onActive: (event, ctx) => {
      translateX.value = ctx.startX + event.translationX;
      translateY.value = ctx.startY + event.translationY;
    },
    onEnd: (_) => {
      translateX.value = withSpring(0);
      translateY.value = withSpring(0);
    },
  });

  return (
    <PanGestureHandler onGestureEvent={gestureHandler}>
      <Animated.View style={[styles.card, animatedStyle]} />
    </PanGestureHandler>
  );
};
```

### 11. Security Best Practices

**Cevap:**

```jsx
// 1. Secure Storage
import EncryptedStorage from "react-native-encrypted-storage";

async function storeSecureData(key, value) {
  try {
    await EncryptedStorage.setItem(key, JSON.stringify(value));
  } catch (error) {
    console.error("Error storing secure data:", error);
  }
}

// 2. API Security
const api = axios.create({
  baseURL: "https://api.example.com",
  headers: {
    "Content-Type": "application/json",
    Accept: "application/json",
  },
});

api.interceptors.request.use(async (config) => {
  const token = await getSecureToken();
  if (token) {
    config.headers.Authorization = `Bearer ${token}`;
  }
  return config;
});

// 3. SSL Pinning
import ssl from "react-native-ssl-pinning";

fetch("https://api.example.com/data", {
  method: "GET",
  headers: {
    Accept: "application/json",
    "Content-Type": "application/json",
  },
  sslPinning: {
    certs: ["cert1"], // Sertifika adları
  },
});

// 4. Kod Obfuscation
// metro.config.js
module.exports = {
  transformer: {
    minifierConfig: {
      keep_classnames: false,
      keep_fnames: false,
      mangle: true,
      toplevel: true,
    },
  },
};
```

### 12. CI/CD ve Deployment

**Cevap:**

```yaml
# fastlane Fastfile örneği
default_platform(:ios)

platform :ios do
  desc "Push a new beta build to TestFlight"
  lane :beta do
    increment_build_number
    build_ios_app(
      scheme: "MyApp",
      export_method: "app-store",
      export_options: {
        provisioningProfiles: {
          "com.example.app" => "MyApp Distribution"
        }
      }
    )
    upload_to_testflight
  end
end

# GitHub Actions workflow örneği
name: React Native CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Install dependencies
      run: yarn install
    - name: Run tests
      run: yarn test
    - name: Build Android
      run: cd android && ./gradlew assembleRelease
```

Bu doküman, React Native'in temel ve ileri seviye konularını kapsamlı bir şekilde ele almaktadır. Her bölüm için pratik örnekler ve best practice'ler eklenmiştir.
