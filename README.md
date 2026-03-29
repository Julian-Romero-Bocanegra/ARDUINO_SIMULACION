# ARDUINO_SIMULACION
**Integrantes:** Edwin Stiven Pasto / Julián Romero Bocanegra \
**Docente:** Diego Alejandro Barragán Vargas \
**Institución:** Fundación Universitaria Compensar.

## SIMULACIÓN DE COMPUERTAS LOGICAS CON ARDUINO
### Descripción del Proyecto
El objetivo del proyecto es simular el funcionamiento de las compuertas logicas AND, OR y NOT, utiizando un arduino modelo uno, el sistema se caratceriza por leer las entras digitales (pulsadores) y realiza el proceso de las señales mediante el codigo para activar las salidas visuales (LED's) segun la logica.

### Lista de componentes
<img width="601" height="249" alt="image" src="https://github.com/user-attachments/assets/53bf60f6-e2db-4b7d-993a-63da791d80b5" />

### Tablas de Verdad 
El código evalua cada una de las entradas según las siguientes operaciones:
#### A. Compuerta AND (LED Rojo - Pin 8)
Solo se enciende si A y B están presionados simultáneamente.
| Entrada A | Entrada B | Salida (A && B) |
| :---: | :---: | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |
#### B. Compuerta OR (LED Amarillo - Pin 9)
Se enciende si al menos uno de los pulsadores está presionado.
| Entrada A | Entrada B | Salida (A || B) |
| :---: | :---: | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

#### C. Compuerta NOT (LED Verde - Pin 10)
Es un inversor de la Entrada A. Si no se presiona, el LED brilla; si se presiona, el LED se apaga.
| Entrada A | Salida (!A) |
| :---: | :---: |
| 0 | 1 |
| 1 | 0 |

### Análisis de Funcionamiento Técnico
#### Configuración de Entradas: 
En los pines 2 y 2 estan configurados como el INPUT, el momento de precionar el boton el pin recibe 5V.
#### Procesamiento: 
El comando **digitalRead** captura el estado de los botones. El software realiza las operaciones lógicas ** (&&, ||, !)**.
#### Salida de Datos: 
El comando **digitalWrite** envía la señal a los pines 8, 9 y 10. 
#### Protección de Hardware: 
Se utiliza una resistencia con los LEDs para limitar la corriente según la Ley de Ohm ($V = I \times R$), protegiendo tanto los diodos como los pines del microcontrolador.

### Codigo Usado
void setup() {\
  pinMode(2, INPUT);   // Pulsador A \
  pinMode(3, INPUT);   // Pulsador B \
  pinMode(8, OUTPUT);  // LED Rojo (AND) \
  pinMode(9, OUTPUT);  // LED Amarillo (OR) \
  pinMode(10, OUTPUT); // LED Verde (NOT de A) \
} \
void loop() { \
  int a = digitalRead(2); \ 
  int b = digitalRead(3); \
  // AND: Solo enciende si ambos son 1 \
  digitalWrite(8, (a == HIGH && b == HIGH)); \
  // OR: Enciende si cualquiera es 1 \
  digitalWrite(9, (a == HIGH || b == HIGH)); \
  // NOT: Enciende si A es 0, apaga si A es 1 \
  digitalWrite(10, !a); \
} \
### implementacion del sistema en wokwi
<img width="839" height="658" alt="image" src="https://github.com/user-attachments/assets/03cce754-f36f-4d06-8c48-32499862ea0e" />
<img width="1919" height="713" alt="image" src="https://github.com/user-attachments/assets/37b41b1d-4362-4551-8c4b-8845eb2ec6c7" />

## SIMULACION DEL CONVERSOR BINARIO A HEXADECIMAL
### Descripción del Proyecto
Este ejercicio consiste en un sistema que reiba un numero de 4 bits por medio de un interruptor DIP de 8 posiciones (NOTA: se usa el interruptor de 8 posiciones porque en wokwi no se enuentra el de 4 posiciones) donde solo se debe hacer uso de 4 posiciones y lo traduzca a su representacion equivalente en el sistema hexadecimal por medio de un display de 7 segmentos.

### Lista de componentes
<img width="682" height="274" alt="image" src="https://github.com/user-attachments/assets/99c96032-2ad0-4604-a803-ba971bb6ff14" />

### Tablas de Verdad 
<img width="911" height="316" alt="image" src="https://github.com/user-attachments/assets/db07ab1d-e528-4fd8-aa97-5982b53ea890" />

### Funcionamiento Técnico
#### Lectura de Entradas: 
El programa lee los estados de los pines 2, 3, 4 y 5. Cada pin tiene un "peso" binario que el código suma para obtener un valor decimal entre 0 y 15.

#### Decodificación: 
Se utiliza un arreglo constante llamado **hexMap**. Este contiene la configuración de bits necesaria para encender los segmentos específicos del display (a, b, c, d, e, f, g) según el número calculado.

#### Configuración de Ánodo Común: 
El display utilizado tiene los ánodos conectados a 5V. Por lo tanto, el Arduino enciende cada segmento enviando un estado BAJO (0), permitiendo que la corriente fluya a través del LED correspondiente.

### Lógica de Programación (Fragmento Clave)
Es importante mencionar el uso de la función **bitRead()**, la cual permite extraer cada bit del mapa hexadecimal y enviarlo al pin físico del display de forma secuencial.

### Codigo Usado
const int segmentos[] = {6, 7, 8, 9, 10, 11, 12};\
// Mapa para Ánodo Común (0 enciende, 1 apaga)\
const byte hexMap[16] = {\
  0x40, 0x79, 0x24, 0x30, 0x19, 0x12, 0x02, 0x78, \
  0x00, 0x10, 0x08, 0x03, 0x46, 0x21, 0x06, 0x0E\
};\
void setup() {\
  for (int i = 2; i <= 5; i++) pinMode(i, INPUT);\
  for (int i = 0; i < 7; i++) pinMode(segmentos[i], OUTPUT);\
}\
void loop() {\
  // Leer los 4 bits (1, 2, 4, 8)\
  int valor = digitalRead(2) * 1 + \
              digitalRead(3) * 2 + \
              digitalRead(4) * 4 + \
              digitalRead(5) * 8;\
  byte patron = hexMap[valor];\
  for (int i = 0; i < 7; i++) { \
    digitalWrite(segmentos[i], bitRead(patron, i));\
  }\
  delay(100);\
}\
### implementacion del sistema en wokwi
<img width="670" height="577" alt="image" src="https://github.com/user-attachments/assets/e88cdbfc-84bd-4a5d-8a1c-000922ce0eb7" />
<img width="1918" height="717" alt="image" src="https://github.com/user-attachments/assets/f70835cc-69db-4eb9-bb7a-5b930dd9ea4c" />

## SIMULACION DE SEMAFORO VIAL CON TIEMPO

### Descripción del Proyecto
Este ejercicio consiste en la programación de un sistema de control de tráfico automatizado. El objetivo es emular el ciclo de un semáforo real, gestionando el encendido y apagado secuencial de tres indicadores (Rojo, Amarillo y Verde) mediante el uso de temporizadores programados en el microcontrolador
### Lista de componentes
<img width="704" height="257" alt="image" src="https://github.com/user-attachments/assets/c7ab91a1-212c-4279-98ac-936b3ab3bce6" />

### Secuencia de Funcionamiento y Tiempos
El ciclo de trabajo está diseñado para repetirse indefinidamente (bucle), siguiendo la lógica de seguridad vial estándar:

Análisis Técnico de Programación
Definición de Salidas: Se configuran los pines 11, 12 y 13 como OUTPUT en la función setup() para enviar señales de voltaje a los LEDs.

Control de Estados: Se utiliza la función digitalWrite(pin, HIGH/LOW) para activar o desactivar cada color individualmente.

Gestión de Retardos: Se implementa la función delay(), la cual pausa la ejecución del código por una cantidad específica de milisegundos. Esta pausa es la que determina cuánto tiempo permanece encendido cada color antes de pasar al siguiente bloque de instrucciones.

Estructura Cíclica: Al estar dentro de la función loop(), el semáforo reinicia automáticamente al color verde después de completar la fase roja, garantizando un funcionamiento continuo.

### Codigo Usado
// Definición de pines para el semáforo
const int ledRojo = 13;
const int ledAmarillo = 12;
const int ledVerde = 11;

void setup() {
  // Configurar los pines como salida
  pinMode(ledRojo, OUTPUT);
  pinMode(ledAmarillo, OUTPUT);
  pinMode(ledVerde, OUTPUT);
}

void loop() {
  // 1. VERDE: El tráfico fluye (5 segundos)
  digitalWrite(ledVerde, HIGH);
  digitalWrite(ledAmarillo, LOW);
  digitalWrite(ledRojo, LOW);
  delay(5000); 

  // 2. AMARILLO: Precaución, va a cambiar (2 segundos)
  digitalWrite(ledVerde, LOW);
  digitalWrite(ledAmarillo, HIGH);
  delay(2000);

  // 3. ROJO: El tráfico se detiene (5 segundos)
  digitalWrite(ledAmarillo, LOW);
  digitalWrite(ledRojo, HIGH);
  delay(5000);
}

### implementacion del sistema en wokwi
<img width="601" height="554" alt="image" src="https://github.com/user-attachments/assets/deec2289-4ffd-46ac-a588-1448e30e41ad" />
<img width="1919" height="766" alt="image" src="https://github.com/user-attachments/assets/f16b87cc-37dc-4a40-baaa-d4340dc078c5" />

