# Taller Final: Sistema de Control de Acceso y Climatización

**Curso:** Estructuras Computacionales (4100901)  

**Universidad Nacional de Colombia - Sede Manizales** 

**Modalidad:** Parejas  

---

## 🎯 Objetivo

Implementar un sistema funcional de control de acceso y climatización utilizando la placa NUCLEO-L476RG, integrando los conocimientos adquiridos durante el semestre sobre arquitecturas ARM, drivers embebidos, y sistemas reactivos.

## 📋 Estructura del Taller

### **Módulo A: Sistema de Control de Acceso (3 horas)**

**Descripción:** Implementar un sistema de acceso controlado por contraseña con interfaz visual.

**Funcionalidades a implementar:**
- **Estado LOCKED:** Mostrar "SISTEMA BLOQUEADO" en pantalla OLED
- **Estado INPUT_PASSWORD:** Capturar 4 dígitos del teclado, mostrar asteriscos (****)
- **Estado UNLOCKED:** Mostrar "ACCESO CONCEDIDO", encender LED de estado
- **Estado ACCESS_DENIED:** Mostrar "ACCESO DENEGADO" por 3 segundos
- **Timeout:** Si no se completa la contraseña en 10 segundos, regresar a LOCKED
- **Validación:** Contraseña por defecto "1234"

**Archivos a modificar:**
- `Core/Src/room_control.c`: Función `room_control_process_key()`
- `Core/Src/room_control.c`: Lógica de máquina de estados en `room_control_update()`

### **Módulo B: Sistema de Climatización (3 horas)**

**Descripción:** Implementar control automático de ventilador basado en temperatura.

**Funcionalidades a implementar:**
- **Sensor de temperatura:** Configurar ADC para leer sensor analógico (Pueden usar un pontenciometro para simular un sensor de temperatura)
- **Control de ventilador:** PWM con 4 niveles discretos:
  - Nivel 0 (0%): Temp < 25°C
  - Nivel 1 (30%): 25°C ≤ Temp < 28°C
  - Nivel 2 (70%): 28°C ≤ Temp < 31°C
  - Nivel 3 (100%): Temp ≥ 31°C
- **Visualización:** Mostrar temperatura actual y nivel del ventilador en OLED

**Archivos a modificar:**
- `Core/Src/room_control.c`: Función `room_control_update_fan()`
- `Core/Src/room_control.c`: Agregar lectura de temperatura
- Configurar ADC en STM32CubeMX (si es necesario)

### **Módulo C: Conectividad Remota (Bonus +0.5)**

**Descripción:** Implementar parser de comandos para control remoto del sistema.

**Comandos a implementar:**
- `GET_TEMP`: Devolver temperatura actual
- `GET_STATUS`: Devolver estado del sistema (Locked/Unlocked, nivel ventilador)
- `SET_PASS:XXXX`: Cambiar contraseña de acceso
- `FORCE_FAN:N`: Forzar velocidad del ventilador (N=0,1,2,3)

**Archivos a modificar:**
- `Core/Src/room_control.c`: Función `room_control_parse_command()`
- `Core/Src/main.c`: Integrar parser con USART2

---

## 🛠️ Recursos Disponibles

### **Drivers YA Implementados:**
- **Keypad:** `keypad_init()`, `keypad_scan()` - Teclado 4x4 con interrupciones
- **OLED:** `ssd1306_Init()`, `ssd1306_WriteString()`, `ssd1306_UpdateScreen()`
- **LED:** `led_init()`, `led_on()`, `led_off()`, `led_toggle()`
- **Ring Buffer:** Para manejo de datos UART y del teclado

### **Hardware Configurado:**
- **I2C1:** Display OLED (PB8/PB9)
- **TIM3:** PWM para ventilador (PA6)
- **USART2:** Debug/ST-Link
- **GPIO:** Teclado matricial y LED de estado

### **Framework Disponible:**
- **Máquina de estados:** Estructura básica implementada
- **Super Loop:** Bucle principal no bloqueante
- **Interrupciones:** Keypad y UART configuradas

---

## 📊 Evaluación

### **Criterios de Calificación:**

| Componente | Puntos | Descripción |
|------------|---------|-------------|
| **Módulo A** | 3.0/5.0 | Sistema de acceso funcionando completamente |
| **Módulo B** | 1.5/5.0 | Control de climatización funcionando |
| **Calidad del código** | 0.5/5.0 | Código limpio, comentarios, manejo de errores |
| **Módulo C (Bonus)** | +0.5 | Parser de comandos funcionando |

### **Escala de Notas:**
- **2.0-3.0:** Módulo A con funcionalidad básica
- **3.0-4.5:** Módulos A+B completos
- **4.5-5.0:** Módulos A+B con excelente calidad de código

---

## 🚀 Instrucciones de Implementación

### **1. Configuración Inicial**
```bash
# Clonar el repositorio
git clone [URL_DEL_REPOSITORIO]
cd Room_Control_Final_2025_1
```

### **2. Flujo de Trabajo Recomendado**

#### **Fase 1: Análisis (30 min)**
- Revisar código existente en `Core/Src/room_control.c`
- Entender la estructura de la máquina de estados
- Probar funcionalidad de drivers existentes

#### **Fase 2: Módulo A (3 horas)**
- Implementar lógica de estados
- Probar entrada de contraseña
- Validar timeout y transiciones

#### **Fase 3: Módulo B (3 horas)**
- Configurar sensor de temperatura
- Implementar control PWM del ventilador
- Integrar con visualización OLED

#### **Fase 4: Integración y Documentación (1 hora)**
- Pruebas completas del sistema
- Crear documentación básica
- Limpieza del código

#### **Fase 5: Módulo C (Opcional)**
- Implementar parser de comandos
- Probar comunicación remota

---

## 🎯 Entregables

### **Al Final del Taller:**
1. **Código fuente** funcionando en la placa NUCLEO-L476RG
2. **Demostración en vivo** del sistema completo
3. **Archivo README.md** con:
   - Nombres de los integrantes
   - Descripción de funcionalidades implementadas
   - Instrucciones de compilación y uso
   - Explicación de decisiones de diseño

### **Formato de Entrega:**
- **Repositorio Git** con todos los cambios
- **Presentación oral** (3 minutos) explicando implementación
- **Código ejecutándose** en tiempo real en la placa

---

## ⚠️ Reglas Importantes

1. **Trabajo en parejas obligatorio**
2. **Uso exclusivo del código base proporcionado**
3. **Prohibido usar HAL_Delay() en el bucle principal**
4. **Documentar todas las funciones implementadas**
5. **Probar funcionamiento antes de la entrega**

---

## 🏆 Consejos para el Éxito

### **Gestión del Tiempo:**
- Dedica 30 min iniciales a entender las instrucciones
- Implementa funcionalidad básica antes de optimizar
- Deja tiempo para pruebas e integración

### **Estrategia de Implementación:**
- Usa `printf()` para debug a través de USART2
- Prueba cada función por separado antes de integrar
- Mantén código simple y funcional

### **Trabajo en Equipo:**
- Divide tareas: uno enfocado en lógica, otro en hardware
- Revisa código del compañero antes de integrar
- Documenta mientras implementas

---

**¡Éxito en el taller! Este es el momento de demostrar todo lo aprendido durante el semestre.**

---

*Para dudas técnicas durante el taller, consulta primero la documentación del proyecto y luego solicita ayuda al instructor.*