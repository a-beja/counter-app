# Temas puntuales

En esta app de contador practicamos conceptos básicos de React Native con Expo. La pantalla muestra un número y permite aumentarlo, disminuirlo o reiniciarlo.

## React y TypeScript

- **Componentes funcionales** — funciones que dibujan la UI: `function App()` y `function FAB(...)`.
- **JSX** — estructura visual; `{count}` inserta el valor del contador.
- **Estado (`useState`)** — recuerda datos y actualiza la UI: `const [count, setCount] = useState(10)`.
- **Props** — datos que recibe un componente: `label`, `position`.
- **`interface Props`** — define qué props acepta `FAB`.
- **Props obligatorias/opcionales** — `label: string` es requerida; `position?: 'left' | 'right' | 'center'` puede omitirse.
- **Opciones limitadas** — solo admite estos valores: `'left' | 'right' | 'center'`.
- **Callbacks** — props que reciben acciones: `onPress`, `onLongPress`.
- **Tipo de función** — `() => void` significa función sin argumentos ni valor de retorno.
- **Valor predeterminado** — `position = 'center'` se usa si no se proporciona la prop.
- **Desestructuración** — extrae props directamente: `({ label, position })`.
- **Encadenamiento opcional** — llama solo si existe: `onPress?.()`.
- **Funciones flecha** — definen acciones breves: `() => setCount(count + 1)`.

## Componentes de React Native

- `View` — contenedor de la pantalla
- `Text` — muestra el número y las etiquetas
- `Pressable` — crea botones interactivos

## Eventos e interacción

- `onPress` — acción al tocar un botón
- `onLongPress` — acción al mantenerlo presionado
- `pressed` — estado de `Pressable` mientras se presiona
- Estilo dinámico con `style={({ pressed }) => [...]}` según la pulsación
- Retroalimentación háptica al tocar

## Componentes personalizados

- Componente reutilizable `FAB`
- Uso de una interfaz para describir sus props
- Mismo componente con distintas etiquetas, posiciones y acciones
- Separación entre la pantalla (`App`) y el botón (`FAB`)
- Callbacks para que `FAB` comunique acciones a `App`

## Estado y comportamiento del contador

- Estado inicial del contador: `10`
- Sumar uno con `+1`
- Restar uno con `-1`
- Reiniciar con `R`
- Reiniciar al mantener presionado `+1`
- Actualización de la interfaz cuando cambia el estado
- El contador funcional está en `App`; el `useState` de `FAB` no se utiliza

## Estilos y diseño

- `StyleSheet.create` — agrupa estilos: `StyleSheet.create({ container: { flex: 1 } })`
- **Flexbox** — ocupa y centra el contenido: `{ flex: 1, alignItems: 'center', justifyContent: 'center' }`
- **Posicionamiento absoluto** — ubica un botón flotante: `{ position: 'absolute', bottom: 20 }`
- **Estilos combinados en un arreglo** — mezcla base, posición y estado: `[styles.floatingButton, positionStyles[position], pressed ? { opacity: 0.5 } : { opacity: 1 }]`
- **Estilos en línea** — se escriben directamente en JSX: `style={{ color: 'white', fontSize: 20 }}`
- **Apariencia** — color y texto: `backgroundColor: '#65558F'`, `fontSize: 120`, `fontWeight: '100'`
- **Espaciado y bordes** — `padding: 20`, `borderRadius: 15`
- **Sombras/elevación** — `shadowOpacity: 0.3`, `elevation: 3`
- **Posiciones disponibles** — `positionStyles = { left: ..., right: ..., center: null }`

## Expo y configuración

- Punto de entrada con `registerRootComponent`
- `expo-haptics` para el efecto háptico (`ImpactFeedbackStyle.Heavy`)
- `expo-status-bar` para la barra de estado
- Componente `StatusBar` con estilo automático
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
