# Temas puntuales

En esta app de contador practicamos conceptos básicos de React Native con Expo. La pantalla muestra un número y permite aumentarlo, disminuirlo o reiniciarlo.

## React y TypeScript

### Componentes y JSX

- **Componentes funcionales** — funciones que dibujan la UI: `function App()` y `function FAB(...)`.
- **JSX** — estructura visual; `{count}` inserta el valor del contador.

### Estado y contador

- `useState` guarda el contador: `const [count, setCount] = useState(10)`.
- Sumar uno con `+1`
- Restar uno con `-1`
- Reiniciar con `R`
- Reiniciar al mantener presionado `+1`
- `setCount` cambia el valor y React actualiza la UI.
- El contador funcional está en `App`; el `useState` de `FAB` no se utiliza

### Componente reutilizable `FAB` y sus props

- `FAB` se reutiliza con distintas etiquetas, posiciones y acciones.
- `interface Props` define lo que puede recibir el componente.
- **Props:** `label`, `position`, `onPress`, `onLongPress`.
- **Obligatoria/opcionales:** `label: string`; las demás usan `?`.
- **Opciones limitadas:** `position?: 'left' | 'right' | 'center'`.
- `positionStyles[position]` aplica el estilo de la posición elegida.
- **Callbacks:** `onPress` y `onLongPress` tienen tipo `() => void`.
- **Predeterminado:** `position = 'center'`.
- **Desestructuración:** `({ label, position })`.
- **Llamada opcional:** `onPress?.()`.
- `App` pasa callbacks flecha, como `onPress={() => setCount(count + 1)}`.

## Componentes de React Native

### `View` y `Text`

- `View` — contenedor de la pantalla.
- `Text` — muestra el contador y las etiquetas de los botones.

### `Pressable`, eventos y respuesta háptica

- `Pressable` — crea cada botón `FAB`.
- `onPress` — acción al tocar; `onLongPress` — acción al mantener presionado.
- `pressed` — indica que se está presionando el botón.
- Estilo dinámico combinado: `style={({ pressed }) => [styles.floatingButton, positionStyles[position], pressed ? { opacity: 0.5 } : { opacity: 1 }]}`.
- Los eventos ejecutan los callbacks que `App` pasó mediante props.
- Expo Haptics añade respuesta táctil: `Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Heavy)`.

## Estilos y diseño

- `StyleSheet.create` — agrupa estilos: `StyleSheet.create({ container: { flex: 1 } })`
- **Flexbox** — ocupa y centra el contenido: `{ flex: 1, alignItems: 'center', justifyContent: 'center' }`
- **Posicionamiento absoluto** — ubica un botón flotante: `{ position: 'absolute', bottom: 20 }`
- **Estilos en línea** — se escriben directamente en JSX: `style={{ color: 'white', fontSize: 20 }}`
- **Apariencia** — color y texto: `backgroundColor: '#65558F'`, `fontSize: 120`, `fontWeight: '100'`
- **Espaciado y bordes** — `padding: 20`, `borderRadius: 15`
- **Sombras/elevación** — `shadowOpacity: 0.3`, `elevation: 3`

## Expo y configuración

- Punto de entrada con `registerRootComponent`
- `expo-status-bar` para la barra de estado
- `StatusBar` con estilo automático: `<StatusBar style="auto" />`
- `app.json` para nombre, orientación, iconos y opciones de plataforma
- Expo para ejecutar la app en iOS, Android y web

## Herramientas del proyecto

- TypeScript con modo `strict` en `tsconfig.json`
- Bun para instalar dependencias y ejecutar scripts
- `bun install`
- `bun run start`
- `bun run android`
- `bun run ios`
- `bun run web`

## Archivos principales

- `App.tsx` — pantalla y estado del contador
- `components/FAB.tsx` — componente del botón flotante
- `index.ts` — entrada de la app en Expo
- `app.json` — configuración de Expo
- `package.json` — dependencias y scripts
- `tsconfig.json` — configuración de TypeScript

Con estos conceptos se construyó la pantalla, se reutilizó un botón personalizado y se conectaron sus interacciones con el estado de React.
