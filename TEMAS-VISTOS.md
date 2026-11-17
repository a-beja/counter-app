# Temas vistos: Counter App (React Native + Expo)

Esta guía reúne los conceptos que aparecen en esta app de contador. Para cada uno se indica dónde se usa, qué hace aquí y en qué otros tipos de apps puede servir.

## Índice

- [1. Estructura de la app](#1-estructura-de-la-app)
  - [Punto de entrada de Expo](#punto-de-entrada-de-expo)
  - [Componente raíz](#componente-raíz)
  - [Componentes reutilizables](#componentes-reutilizables)
  - [Importaciones y exportación por defecto](#importaciones-y-exportación-por-defecto)
- [2. React y TypeScript](#2-react-y-typescript)
  - [Componentes funcionales y JSX](#componentes-funcionales-y-jsx)
  - [Estado con `useState`](#estado-con-usestate)
  - [Props y componentes configurables](#props-y-componentes-configurables)
  - [Tipos de TypeScript](#tipos-de-typescript)
  - [Valores por defecto y encadenamiento opcional](#valores-por-defecto-y-encadenamiento-opcional)
  - [Funciones flecha y callbacks](#funciones-flecha-y-callbacks)
- [3. Interfaz de React Native](#3-interfaz-de-react-native)
  - [Componentes nativos básicos](#componentes-nativos-básicos)
  - [Eventos: pulsar y mantener pulsado](#eventos-pulsar-y-mantener-pulsado)
  - [Estilos y Flexbox](#estilos-y-flexbox)
  - [Posicionamiento y estilos dinámicos](#posicionamiento-y-estilos-dinámicos)
  - [Sombras y apariencia](#sombras-y-apariencia)
  - [Estilos en línea](#estilos-en-línea)
- [4. Expo](#4-expo)
  - [`expo-haptics`](#expo-haptics)
  - [Barra de estado](#barra-de-estado)
  - [Configuración del proyecto](#configuración-del-proyecto)
  - [Comandos del proyecto](#comandos-del-proyecto)
- [5. Flujo del contador](#5-flujo-del-contador)
- [6. Herramientas y dependencias](#6-herramientas-y-dependencias)
- [7. Lo que todavía no se usa en esta app](#7-lo-que-todavía-no-se-usa-en-esta-app)

## 1. Estructura de la app

| Tema | Dónde aparece | Uso en esta app | Otros usos |
|---|---|---|---|
| Punto de entrada de Expo | `index.ts` | `registerRootComponent(App)` registra `App` como componente raíz para ejecutar la app en Expo Go o en una compilación nativa. | Normalmente se conserva como entrada y se cambia el componente raíz que importa. |
| Componente raíz | `App.tsx` | `App` compone la pantalla del contador y mantiene el estado principal. | Puede contener la navegación y las pantallas principales de una app. |
| Componentes reutilizables | `components/FAB.tsx` | `FAB` encapsula la apariencia y las interacciones de un botón flotante. | Se pueden extraer tarjetas, campos, barras de navegación y otros elementos que se repiten. |
| Importaciones y exportación por defecto | `App.tsx`, `components/FAB.tsx` | Se importan React, componentes, estilos y el `FAB`; cada archivo exporta su componente principal. | Permite organizar una app en módulos pequeños y reutilizables. |

## 2. React y TypeScript

### Componentes funcionales y JSX

`App` y `FAB` son funciones que devuelven JSX, una sintaxis para describir la interfaz. Las llaves `{...}` permiten insertar expresiones de JavaScript, como `{count}` o una función manejadora.

- **Aquí:** se muestra el contador y se construye cada botón con sus propiedades.
- **También sirve para:** describir pantallas, listas, formularios y componentes de interfaz.

### Estado con `useState`

En `App.tsx`:

```tsx
const [count, setCount] = useState(10);
```

`useState` crea un valor de estado y una función para actualizarlo. El valor inicial del contador es `10`. Al llamar a `setCount`, React vuelve a renderizar el componente con el valor actualizado.

- **Aquí:** guarda el número del contador.
- **También sirve para:** controlar un menú abierto, un formulario, una selección o el estado de carga de una pantalla.
- En `FAB.tsx` también hay un `useState(10)` para `count`, pero ese estado no se lee ni se actualiza: no participa en el comportamiento del botón. El contador visible pertenece a `App`.

### Props y componentes configurables

`FAB` recibe `label`, `position`, `onPress` y `onLongPress`. Sus props permiten que cada instancia tenga un texto, posición y acciones diferentes.

- **Aquí:** se reutiliza el mismo componente para `+1`, `R` y `-1`.
- **También sirve para:** configurar un componente genérico sin duplicar su estructura.

### Tipos de TypeScript

En `FAB.tsx`, `interface Props` describe las props. `label` es obligatorio; `position` solo acepta `'left'`, `'right'` o `'center'`; `?` indica que una prop es opcional; y `() => void` describe una función que no recibe argumentos ni devuelve un valor útil.

- **Aquí:** se limita qué posiciones son válidas y se documentan las acciones del botón.
- **También sirve para:** detectar errores de tipos y hacer más claro cómo se usa un componente.

### Valores por defecto y encadenamiento opcional

- `position = 'center'` da una posición predeterminada cuando no se proporciona la prop.
- `onPress?.()` y `onLongPress?.()` llaman a la función solo si fue proporcionada.
- **También sirve para:** crear componentes flexibles con configuraciones opcionales sin tener que comprobarlas manualmente antes de cada llamada.

### Funciones flecha y callbacks

Las funciones flecha aparecen al definir componentes, generar estilos dinámicos y pasar acciones mediante props.

- **Aquí:** los botones pasan acciones que modifican el contador.
- **También sirve para:** responder a eventos, transformar datos y pasar comportamiento a componentes reutilizables.

## 3. Interfaz de React Native

### Componentes nativos básicos

| Componente | Uso en esta app | Otros usos |
|---|---|---|
| `View` | Contenedor principal de la pantalla. | Agrupar y organizar otros elementos. |
| `Text` | Mostrar el número y las etiquetas de los botones. | Presentar títulos, instrucciones y datos de texto. |
| `Pressable` | Crear botones que responden a pulsaciones y pulsaciones largas. | Hacer interactivos tarjetas, filas, iconos u otras zonas de la interfaz. |

Son componentes de React Native, no etiquetas HTML. Su aspecto y comportamiento se traducen a las plataformas nativas compatibles.

### Eventos: pulsar y mantener pulsado

`Pressable` recibe `onPress` y `onLongPress`.

- **Aquí:** `+1` suma uno al contador, `R` lo restablece y `-1` resta uno. Mantener pulsado `+1` también lo restablece.
- **También sirve para:** acciones principales y secundarias, menús contextuales o atajos mediante pulsación larga.

### Estilos y Flexbox

`StyleSheet.create` agrupa los estilos en `App.tsx` y `FAB.tsx`. En el contenedor se usan `flex: 1`, `alignItems` y `justifyContent` para ocupar la pantalla y centrar el contenido.

- **Aquí:** se centra el contador y se define el aspecto de los botones.
- **También sirve para:** organizar diseños adaptables usando Flexbox en pantallas de distintos tamaños.

### Posicionamiento y estilos dinámicos

El botón usa `position: 'absolute'` para flotar cerca de la parte inferior. `positionStyles` selecciona estilos a izquierda, derecha o ninguno; en el centro el botón queda centrado por el diseño del contenedor. `Pressable` también recibe una función de estilo que usa `pressed` para cambiar la opacidad mientras se presiona.

- **Aquí:** se distribuyen los tres botones y se ofrece una señal visual al tocar.
- **También sirve para:** botones flotantes de acción, controles superpuestos y estados visuales de interacción.

### Sombras y apariencia

El estilo del botón combina color, relleno (`padding`), esquinas redondeadas (`borderRadius`) y propiedades de sombra/elevación.

- **Aquí:** se da apariencia de botón flotante.
- **También sirve para:** dar jerarquía visual a controles y superficies. La representación de sombras puede variar entre plataformas.

### Estilos en línea

Se usan objetos de estilo directamente en el JSX, por ejemplo el color y tamaño del texto, y la opacidad según el estado de pulsación.

- **Aquí:** sirven para estilos breves o que dependen de una condición.
- **También sirve para:** estados visuales dinámicos; para estilos compartidos o más extensos conviene agruparlos en `StyleSheet.create`.

## 4. Expo

### `expo-haptics`

`expo-haptics` se importa como `Haptics`; `impactAsync(Haptics.ImpactFeedbackStyle.Heavy)` solicita una respuesta háptica cuando se pulsa el botón o se mantiene presionado.

- **Aquí:** agrega una vibración/impacto táctil a las interacciones del contador.
- **También sirve para:** confirmar acciones, selecciones o interacciones importantes. La disponibilidad e intensidad dependen del dispositivo y la plataforma.

### Barra de estado

`StatusBar` de `expo-status-bar` se incluye con `style="auto"`.

- **Aquí:** deja que Expo elija el estilo de la barra de estado según el tema.
- **También sirve para:** configurar la apariencia de la barra superior del sistema.

### Configuración del proyecto

`app.json` contiene metadatos y opciones de Expo, entre ellas nombre, orientación, icono, pantalla de inicio, soporte para tabletas iOS, icono adaptable Android y favicon web.

- **Aquí:** configura la identidad visual y algunas opciones de las plataformas.
- **También sirve para:** ajustar propiedades generales del proyecto Expo sin cambiar los componentes de la pantalla.

### Comandos del proyecto

En `package.json`:

- `bun run start`: inicia Expo.
- `bun run android`: inicia Expo intentando abrir Android.
- `bun run ios`: inicia Expo intentando abrir iOS.
- `bun run web`: inicia Expo para web.
- `bun install`: instala las dependencias del proyecto.

## 5. Flujo del contador

1. `App` inicializa `count` en `10`.
2. `App` muestra ese estado dentro de `Text`.
3. `App` crea tres `FAB` y les pasa etiquetas, posiciones y callbacks.
4. Al pulsar un botón, `FAB` solicita el efecto háptico y ejecuta el callback recibido, si existe.
5. El callback llama a `setCount`; React actualiza el estado y vuelve a mostrar el número.

Este flujo —estado en un componente, acciones pasadas a componentes hijos mediante props— es un patrón útil para mantener el dato en un solo lugar y reutilizar la interfaz.

## 6. Herramientas y dependencias

- **React:** biblioteca para construir la interfaz y administrar estado.
- **React Native:** componentes y estilos para interfaces móviles nativas.
- **Expo:** herramientas y configuración para desarrollar y ejecutar la app en varias plataformas.
- **Bun:** gestor de paquetes y runtime usado en este proyecto para instalar dependencias y ejecutar los scripts de `package.json`.
- **TypeScript:** tipos estáticos; este proyecto hereda la configuración base de Expo y activa `strict`.
- **`expo-haptics`:** API de Expo para retroalimentación háptica.
- **`expo-status-bar`:** componente de Expo para la barra de estado.

## 7. Lo que todavía no se usa en esta app

No hay navegación entre pantallas, llamadas a una API, almacenamiento persistente, listas, formularios ni gestión global de estado. El contador vive en memoria dentro de `App`, por lo que vuelve a `10` al reiniciar la app.
