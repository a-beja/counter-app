# Temas puntuales

En esta app de contador practicamos conceptos básicos de React Native con Expo.

## Resumen general

- **React:** componentes, props y estado para construir y actualizar la pantalla.
- **TypeScript:** `interface Props` y tipos para definir las opciones de `FAB`.
- **React Native:** `View`, `Text` y `Pressable` para la interfaz y los botones.
- **Interacciones:** `onPress`, `onLongPress` y `pressed` para responder a las pulsaciones.
- **Estilos:** `StyleSheet`, Flexbox y estilos dinámicos para acomodar la pantalla.
- **Expo:** Haptics y `StatusBar` para funciones nativas y del sistema.
- **Bun:** instalar dependencias y ejecutar la app.

### Hooks, métodos y callbacks

- `useState(10)` — hook que inicia el estado del contador.
- `setCount(...)` — actualiza el número.
- `StyleSheet.create(...)` — organiza los estilos.
- `Haptics.impactAsync(...)` — solicita la respuesta háptica.
- `registerRootComponent(App)` — registra la pantalla inicial de Expo.
- `onPress` y `onLongPress` — callbacks de eventos; no son métodos de una clase.

## Archivos principales

- `App.tsx` — pantalla, estado y acciones del contador.
- `components/FAB.tsx` — botón flotante reutilizable.
- `index.ts` — punto de entrada de la app en Expo.
- `app.json` — configuración de Expo y plataformas.
- `package.json` — dependencias y scripts ejecutados con Bun:
  - `bun install`
  - `bun run start`, `bun run android`, `bun run ios`, `bun run web`
- `tsconfig.json` — configuración de TypeScript en modo `strict`.

## React y TS

### Componentes y JSX

- **Componentes funcionales** — `function App()` y `function FAB(...)`.
- **JSX** — estructura visual; `{count}` inserta el número.

### Estado y contador

- **`useState`** — guarda el contador: `const [count, setCount] = useState(10)`.
- `setCount` actualiza el estado y React vuelve a dibujar la UI.
- `+1` suma; `-1` resta; `R` y mantener `+1` reinician.
- El estado de `FAB` no se usa; el contador funcional vive en `App`.

### Componente `FAB` y sus props

- **`interface Props`** — define las props que recibe `FAB`.
- **Props:** `label`, `position`, `onPress`, `onLongPress`.
- **Obligatoria/opcionales:** `label: string`; las demás usan `?`.
- **Opciones limitadas:** `position?: 'left' | 'right' | 'center'`.
- **Callbacks:** `onPress` y `onLongPress` son funciones `() => void`.
- **Valor predeterminado:** `position = 'center'`.
- **Desestructuración:** `({ label, position })`.
- **Llamada opcional:** `onPress?.()`.
- `FAB` se reutiliza con distintas etiquetas, posiciones y acciones.
- `App` le pasa callbacks flecha, por ejemplo `onPress={() => setCount(count + 1)}`.

## Componentes de RN

### `View` y `Text`

- `View` — contenedor de la pantalla.
- `Text` — muestra el contador y las etiquetas.

### `Pressable`, eventos y respuesta háptica

- `Pressable` — crea los botones `FAB`.
- `onPress` — acción al tocar; `onLongPress` — acción al mantener presionado.
- `pressed` — indica que el botón está siendo presionado.
- Estilo dinámico: `style={({ pressed }) => [styles.floatingButton, positionStyles[position], pressed ? { opacity: 0.5 } : { opacity: 1 }]}`.
- Los eventos ejecutan los callbacks que `App` pasó mediante props.
- Expo Haptics añade respuesta táctil: `Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Heavy)`.

## Estilos y diseño

- `StyleSheet.create` — agrupa estilos: `StyleSheet.create({ container: { flex: 1 } })`.
- **Flexbox** — centra el contenido: `{ flex: 1, alignItems: 'center', justifyContent: 'center' }`.
- **Posicionamiento absoluto** — ubica el botón: `{ position: 'absolute', bottom: 20 }`.
- **Estilos en línea** — `style={{ color: 'white', fontSize: 20 }}`.
- **Apariencia** — `backgroundColor`, `fontSize`, `fontWeight`.
- **Espaciado y bordes** — `padding`, `borderRadius`.
- **Sombras/elevación** — `shadowOpacity`, `elevation`.

## Expo y configuración

- `registerRootComponent` conecta `App` con Expo.
- `expo-status-bar` y `<StatusBar style="auto" />` configuran la barra de estado.
- `app.json` configura nombre, orientación, iconos y opciones de plataforma.
- Expo permite ejecutar la app en iOS, Android y web.
