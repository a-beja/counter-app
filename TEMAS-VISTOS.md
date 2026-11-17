# Temas puntuales

En esta app de contador practicamos conceptos básicos de React Native con Expo. La pantalla muestra un número y permite aumentarlo, disminuirlo o reiniciarlo.

## React y TypeScript

- Componentes funcionales: `App` y `FAB`
- JSX y expresiones dentro de `{ }`
- Estado con `useState` y actualización con `setCount`
- Props para configurar componentes
- `interface Props` para definir las props de `FAB`
- Props obligatorias y opcionales (`?`)
- Tipos de opciones limitadas: `'left' | 'right' | 'center'`
- Props de función (callbacks): `onPress` y `onLongPress`
- Parámetros de función: `() => void`
- Valores predeterminados: `position = 'center'`
- Desestructuración de props
- Encadenamiento opcional: `onPress?.()`
- Funciones flecha para callbacks

## Componentes de React Native

- `View` — contenedor de la pantalla
- `Text` — muestra el número y las etiquetas
- `Pressable` — crea botones interactivos

## Eventos e interacción

- `onPress` — acción al tocar un botón
- `onLongPress` — acción al mantenerlo presionado
- `pressed` — estado de `Pressable` mientras se presiona
- Estilos dinámicos según el estado de pulsación
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

- `StyleSheet.create`
- Flexbox: `flex`, `alignItems` y `justifyContent`
- Posicionamiento absoluto para los botones flotantes
- Estilos combinados en un arreglo
- Estilos en línea
- Opacidad, color, tamaño de texto y tipografía
- Espaciado, bordes redondeados y sombras/elevación
- Posiciones izquierda, derecha y centro como opciones del componente

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
