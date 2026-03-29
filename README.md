# ARDUINO_SIMULACION
**Integrantes:** Edwin Stiven Pasto / Julián Romero Bocanegra
**Docente:** Diego Alejandro Barragán Vargas
**Institución:** Fundación Universitaria Compensar.

CODIGO UTILIZADO
void setup() {
  pinMode(2, INPUT);   // Pulsador A
  pinMode(3, INPUT);   // Pulsador B
  pinMode(8, OUTPUT);  // LED Rojo (AND)
  pinMode(9, OUTPUT);  // LED Amarillo (OR)
  pinMode(10, OUTPUT); // LED Verde (NOT de A)
}

void loop() {
  int a = digitalRead(2);
  int b = digitalRead(3);

  // AND: Solo enciende si ambos son 1
  digitalWrite(8, (a == HIGH && b == HIGH));

  // OR: Enciende si cualquiera es 1
  digitalWrite(9, (a == HIGH || b == HIGH));

  // NOT: Enciende si A es 0, apaga si A es 1
  digitalWrite(10, !a);
}


<img width="839" height="658" alt="image" src="https://github.com/user-attachments/assets/03cce754-f36f-4d06-8c48-32499862ea0e" />

<img width="1919" height="713" alt="image" src="https://github.com/user-attachments/assets/37b41b1d-4362-4551-8c4b-8845eb2ec6c7" />
