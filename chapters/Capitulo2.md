# Capítulo 2: Sintaxis y Estructura de VHDL

## Introducción

En este capítulo, exploraremos los fundamentos de VHDL (Very High-Speed Integrated Circuit Hardware Description Language), un lenguaje utilizado para describir y modelar circuitos electrónicos. Aunque pueda sonar complejo, comenzaremos desde lo más básico, sin asumir conocimientos previos de programación o diseño digital. Nuestro objetivo es que, al finalizar este capítulo, te sientas cómodo con la sintaxis y la estructura básica de VHDL, preparándote para desarrollar tus primeros diseños.

## 2.1. ¿Qué es VHDL?

VHDL es un lenguaje de descripción de hardware que permite modelar el comportamiento y la estructura de circuitos electrónicos digitales. A diferencia de los lenguajes de programación tradicionales que se ejecutan en un ordenador, VHDL describe cómo se comporta un circuito físico. Esto significa que con VHDL puedes diseñar y simular circuitos antes de construirlos físicamente en un chip o una FPGA.

### 2.1.1. ¿Por qué usar VHDL?

- **Modelado Preciso**: Permite describir exactamente cómo funcionará un circuito.
- **Simulación**: Puedes probar y verificar tus diseños antes de implementarlos.
- **Reutilización**: Los diseños en VHDL pueden ser modulados y reutilizados en proyectos futuros.
- **Estandarización**: Es un lenguaje estandarizado y ampliamente aceptado en la industria.

## 2.2. Conceptos Básicos

Antes de adentrarnos en la sintaxis, es importante entender algunos conceptos fundamentales.

### 2.2.1. Señales y Variables

- **Señales**: Representan conexiones físicas entre componentes en un circuito. Son similares a los cables que transmiten información.
- **Variables**: Almacenan valores temporalmente dentro de un proceso o bloque de código.

### 2.2.2. Entidades y Arquitecturas

- **Entidad**: Define la interfaz externa del circuito, es decir, sus entradas y salidas.
- **Arquitectura**: Describe el funcionamiento interno del circuito, cómo procesa las entradas para generar las salidas.

## 2.3. Estructura Básica de un Archivo VHDL

Un diseño en VHDL generalmente se divide en dos partes principales: la entidad y la arquitectura.

### 2.3.1. Declaración de la Entidad

La entidad define el nombre del circuito y sus puertos (entradas y salidas).

```vhdl
entity NombreEntidad is
    Port (
        -- Declaración de puertos
        entrada1 : in tipo_de_dato;
        salida1  : out tipo_de_dato
    );
end NombreEntidad;
```

- **`entity`**: Palabra clave que indica el inicio de la entidad.
- **`is`**: Indica que estamos definiendo algo sobre la entidad.
- **`Port`**: Sección donde se declaran los puertos.
- **`in`** y **`out`**: Especifican la dirección del puerto (entrada o salida).
- **`end NombreEntidad;`**: Marca el final de la entidad.

### 2.3.2. Declaración de la Arquitectura

La arquitectura describe cómo funciona la entidad.

```vhdl
architecture NombreArquitectura of NombreEntidad is
    -- Declaraciones internas (señales, componentes, etc.)
begin
    -- Comportamiento o estructura del circuito
end NombreArquitectura;
```

- **`architecture`**: Palabra clave que indica el inicio de la arquitectura.
- **`of NombreEntidad`**: Especifica a qué entidad pertenece esta arquitectura.
- **`is`**: Inicio de las declaraciones internas.
- **`begin`**: Inicio de la descripción del comportamiento.
- **`end NombreArquitectura;`**: Final de la arquitectura.

## 2.4. Tipos de Datos Básicos

VHDL ofrece varios tipos de datos para representar señales y variables.

### 2.4.1. Tipo `bit`

Representa un solo bit que puede ser '0' o '1'.

```vhdl
signal señal_bit : bit;
```

### 2.4.2. Tipo `std_logic`

Es más flexible que `bit` y puede representar más estados ('0', '1', 'Z' para alta impedancia, 'X' para indeterminado, etc.).

```vhdl
signal señal_std_logic : std_logic;
```

### 2.4.3. Vectores

Conjuntos de bits, útiles para representar buses o múltiples líneas.

- **`std_logic_vector`**: Vector de señales `std_logic`.

```vhdl
signal bus_datos : std_logic_vector(7 downto 0); -- Vector de 8 bits
```

- **`(7 downto 0)`**: Indica que el vector va desde el bit 7 hasta el 0.

## 2.5. Operadores Básicos

### 2.5.1. Operadores Lógicos

- **AND**: Conjunción lógica.
- **OR**: Disyunción lógica.
- **NOT**: Negación lógica.
- **NAND**, **NOR**, **XOR**, **XNOR**: Operadores lógicos adicionales.

### 2.5.2. Operadores Relacionales

- **=**: Igual a.
- **/=**: Distinto de.
- **<**, **<=**, **>**, **>=**: Menor que, menor o igual que, mayor que, mayor o igual que.

## 2.6. Asignaciones

### 2.6.1. Asignación Concurrente

Se utiliza para describir conexiones directas entre señales.

```vhdl
señal_salida <= señal_entrada1 AND señal_entrada2;
```

### 2.6.2. Asignación Secuencial

Se utiliza dentro de procesos para asignar valores a variables o señales.

```vhdl
variable_temp := señal_entrada1 OR señal_entrada2;
```

## 2.7. Procesos

Los procesos permiten describir comportamientos secuenciales.

```vhdl
process (señal_entrada1, señal_entrada2)
begin
    -- Código secuencial
end process;
```

- **`process`**: Inicia un bloque de código secuencial.
- **`(señal_entrada1, señal_entrada2)`**: Lista de sensibilidad; el proceso se ejecuta cuando estas señales cambian.
- **`begin`** y **`end process;`**: Delimitan el bloque del proceso.

## 2.8. Estructuras de Control

### 2.8.1. Sentencia `if`

Permite tomar decisiones basadas en condiciones.

```vhdl
if condición then
    -- Código si la condición es verdadera
elsif otra_condición then
    -- Código si la otra condición es verdadera
else
    -- Código si ninguna condición es verdadera
end if;
```

### 2.8.2. Sentencia `case`

Selecciona entre múltiples opciones basándose en el valor de una expresión.

```vhdl
case expresión is
    when valor1 =>
        -- Código para valor1
    when valor2 =>
        -- Código para valor2
    when others =>
        -- Código para cualquier otro valor
end case;
```

## 2.9. Ejemplo Completo: Puerta AND de Dos Entradas

Veamos un ejemplo sencillo para consolidar lo aprendido.

### 2.9.1. Definición de la Entidad

```vhdl
entity PuertaAND is
    Port (
        A : in std_logic;
        B : in std_logic;
        Y : out std_logic
    );
end PuertaAND;
```

- **Nombre de la entidad**: `PuertaAND`.
- **Puertos**:
  - `A` y `B`: Entradas de tipo `std_logic`.
  - `Y`: Salida de tipo `std_logic`.

### 2.9.2. Definición de la Arquitectura

```vhdl
architecture Comportamiento of PuertaAND is
begin
    Y <= A AND B;
end Comportamiento;
```

- **Nombre de la arquitectura**: `Comportamiento`.
- **Descripción**: La salida `Y` es el resultado lógico AND de las entradas `A` y `B`.

## 2.10. Práctica: Diseñando una Puerta OR de Tres Entradas

Te animamos a que intentes diseñar una puerta OR con tres entradas siguiendo los pasos anteriores.

### Pasos a seguir:

1. **Definir la entidad** con tres entradas y una salida.
2. **Definir la arquitectura** utilizando la operación OR.
3. **Escribir el código en VHDL** y comentar cada línea para reforzar el aprendizaje.

## 2.11. Resumen del Capítulo

En este capítulo, hemos:

- Introducido los conceptos básicos de VHDL y su propósito en el diseño de hardware.
- Aprendido la estructura fundamental de un archivo VHDL, incluyendo entidades y arquitecturas.
- Explorado los tipos de datos básicos y cómo declarar señales y variables.
- Comprendido cómo utilizar operadores y realizar asignaciones.
- Visto cómo funcionan los procesos y las estructuras de control en VHDL.
- Practicado con un ejemplo sencillo para consolidar los conceptos.

---

En el próximo capítulo, profundizaremos en el modelado de circuitos combinacionales, aplicando lo aprendido aquí para diseñar sistemas más complejos. ¡Sigue adelante y no dudes en repasar este capítulo si tienes alguna duda!