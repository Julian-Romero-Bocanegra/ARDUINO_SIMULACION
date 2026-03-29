# ARDUINO_SIMULACION
**Integrantes:** Edwin Stiven Pasto / Julián Romero Bocanegra \
**Docente:** Diego Alejandro Barragán Vargas \
**Institución:** Fundación Universitaria Compensar.

## SIMULACIÓN DE COMPUERTAS LOGICAS CON ARDUINO
### Descripción del Proyecto
El objetivo del proyecto es simular el funcionamiento de las compuertas logicas AND, OR y NOT, utiizando un arduino modelo uno, el sistema se caratceriza por leer las entras digitales (pulsadores) y realiza el proceso de las señales mediante el codigo para activar las salidas visuales (LED's) segun la logica.

### Lista de componente
<img width="601" height="249" alt="image" src="https://github.com/user-attachments/assets/53bf60f6-e2db-4b7d-993a-63da791d80b5" />

### Tablas de Verdad y Lógica Aplicada
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
| 1 | 0 | 1 |
| 0 | 1 | 1 |
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
