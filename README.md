# Entrega de Ejercicios de Unity

Repositorio que contiene las entregas de los ejercicios prácticos de Unity (Ejercicio 1 y Ejercicio 2), organizados en paquetes exportados (`.unitypackage`) listos para importar.

---

## 📁 Estructura del Proyecto

- **`Ejercicio1/`**:
  - `ejerciciosUnity1.unitypackage`: Paquete con las escenas, scripts y materiales de los ejercicios 1.3, 1.4 y 1.5.
- **`Ejercicio2/`**:
  - `Ejercicio2.unitypackage`: Paquete con las escenas, scripts y recursos de los ejercicios 2.2, 2.3, 2.4 y 2.5.

---

## 🎮 Ejercicio 1: Introducción, Físicas y Rotación

Contenido del paquete `ejerciciosUnity1.unitypackage`:

- **Ejercicio 1.3 (`Assets/Scenes/Ejercicio1.3.unity`)**:
  - Configuración básica de una escena con suelo (plano), iluminación y objeto primitivo (cubo).
  - Creación y aplicación de un material propio (`material azul.mat`).
- **Ejercicio 1.4 (`Assets/Scenes/Ejercicio1.4.unity`)**:
  - Escena con un plano y tres esferas con componentes `Rigidbody`.
  - Configuración de materiales de física (`Physic Material`) evaluando distintos valores de rebote (*bounciness*) y fricción.
- **Ejercicio 1.5 (`Assets/Scenes/Ejercicio1.5.unity`)**:
  - Escena con cilindro animado mediante script.
  - Script `Spinner.cs` (`Assets/Scripts/Spinner.cs`) que aplica rotación continua al objeto en base a `Time.deltaTime`.

---

## 🎮 Ejercicio 2: Input, Movimiento con Inercia, Salto y Mecánicas

### 2.1. Métodos de Input en Unity

Tabla de referencia de los métodos y propiedades del sistema clásico de `Input`:

| Función | Qué devuelve | Cuándo usarla | Ejemplo de una línea |
| :--- | :--- | :--- | :--- |
| `Input.GetKeyDown` | `bool` (true solo en el primer frame al pulsar la tecla) | Acciones de un solo toque con una tecla específica (saltar, pausar, recargar). | `if (Input.GetKeyDown(KeyCode.Space)) Saltar();` |
| `Input.GetKey` | `bool` (true todos los frames mientras mantengas pulsada la tecla) | Acciones continuas manteniendo la tecla (correr, acelerar un coche). | `if (Input.GetKey(KeyCode.LeftShift)) Correr();` |
| `Input.GetKeyUp` | `bool` (true solo en el frame en que sueltas la tecla) | Acciones al soltar una tecla (soltar una flecha cargada, dejar de cubrirse). | `if (Input.GetKeyUp(KeyCode.C)) Levantarse();` |
| `Input.GetButtonDown` | `bool` (true en el frame en que pulsas el botón virtual) | Igual que `GetKeyDown`, pero usando los nombres del Input Manager ("Jump", "Fire1"). | `if (Input.GetButtonDown("Jump")) Saltar();` |
| `Input.GetButton` | `bool` (true mientras mantengas pulsado el botón virtual) | Acciones continuas vinculadas al Input Manager (disparo en ráfaga). | `if (Input.GetButton("Fire1")) DispararContinuo();` |
| `Input.GetButtonUp` | `bool` (true en el frame en que sueltas el botón virtual) | Al soltar un botón configurado en el Input Manager. | `if (Input.GetButtonUp("Fire1")) LanzarGranada();` |
| `Input.GetAxis` | `float` entre `-1.0f` y `1.0f` (con aceleración/suavizado) | Movimiento suave de personaje o cámara (sube poco a poco de 0 a 1). | `float movX = Input.GetAxis("Horizontal");` |
| `Input.GetAxisRaw` | `float` (`-1`, `0` o `1` en seco, sin suavizado) | Movimiento instantáneo sin derrape al frenar (muy usado en juegos 2D o Arcade). | `float dirX = Input.GetAxisRaw("Horizontal");` |
| `Input.GetMouseButtonDown` | `bool` (true en el frame en que haces clic) | Detectar un clic del ratón (0 izquierdo, 1 derecho, 2 rueda). | `if (Input.GetMouseButtonDown(0)) Disparar();` |
| `Input.GetMouseButton` | `bool` (true mientras mantienes el clic pulsado) | Mantener apuntado con clic derecho o arrastrar objetos. | `if (Input.GetMouseButton(1)) Apuntar();` |
| `Input.GetMouseButtonUp` | `bool` (true en el frame en que sueltas el clic) | Soltar un objeto que estabas arrastrando con el ratón. | `if (Input.GetMouseButtonUp(0)) SoltarObjeto();` |
| `Input.mousePosition` | `Vector3` (posición X, Y en píxeles de la pantalla) | Saber dónde está el puntero del ratón en la pantalla. | `Vector3 posRaton = Input.mousePosition;` |

---

### 2.2. Descripción de las Escenas y Scripts

Contenido del paquete `Ejercicio2.unitypackage`:

- **Ejercicio 2.2: Movimiento 3D con inercia (`Assets/Scenes/Ejercicio2.2.unity`)**:
  - Scripts `PlayerController.cs` y `PlayerMover3D_Inertia.cs`.
  - Captura los ejes horizontal y vertical con `Input.GetAxis` en `FixedUpdate` y calcula la velocidad objetivo.
  - Aplica inercia y suavizado mediante interpolación lineal (`Vector3.Lerp`) sobre la velocidad del `Rigidbody`.

- **Ejercicio 2.3: Sistema de Salto (`Assets/Scenes/Ejercicio2.3.unity`)**:
  - Script `Jump.cs`.
  - Permite al personaje saltar al pulsar la barra espaciadora (`Input.GetKeyDown(KeyCode.Space)`) aplicando una fuerza impulsiva (`ForceMode.Impulse`).
  - Detección de contacto con el suelo mediante `OnCollisionStay` y `OnCollisionExit` para impedir el doble salto o salto infinito en el aire.

- **Ejercicio 2.4: Plataforma Unidireccional / One-Way Platform (`Assets/Scenes/Ejercicio2.4.unity`)**:
  - Script `OneWayPlatform.cs`.
  - Permite al jugador saltar y atravesar la plataforma desde abajo, pero posarse sobre ella al caer.
  - Determina si los pies del jugador (`playerCollider.bounds.min.y`) están por encima o por debajo de la superficie de la plataforma (`plataformaCollider.bounds.max.y`) e ignora o activa dinámicamente las colisiones con `Physics.IgnoreCollision`.

- **Ejercicio 2.5: Coleccionable / Monedas (`Assets/Scenes/Ejercicio2.5.unity`)**:
  - Script `CoinScript.cs`.
  - Rotación continua de la moneda en cada frame (`transform.Rotate`).
  - Detección de recogida mediante `OnTriggerEnter(Collider other)` utilizando `other.CompareTag("Player")` y destrucción de la moneda con `Destroy(gameObject)`.
  - **Uso de `CompareTag` vs Comparación por Nombre**:
    1. Si se renombra o duplica el GameObject del jugador en la escena, sigue funcionando siempre que conserve la etiqueta `Player`.
    2. Evita errores silenciosos por erratas tipográficas (Unity avisa en consola si la etiqueta no existe).
    3. Es computacionalmente más rápido y eficiente que comparar cadenas de texto con `name`.

---

## 🚀 Cómo Importar los Paquetes en Unity

1. Abre un proyecto en **Unity Editor** (compatible con versiones URP / 3D).
2. En el menú superior, ve a:  
   `Assets` > `Import Package` > `Custom Package...`
3. Selecciona el archivo `.unitypackage` deseado (`Ejercicio1/ejerciciosUnity1.unitypackage` o `Ejercicio2/Ejercicio2.unitypackage`).
4. En la ventana emergente, asegúrate de marcar todos los elementos y pulsa **Import**.
5. Abre la escena correspondiente en la carpeta `Assets/Scenes/` y pulsa **Play**.
