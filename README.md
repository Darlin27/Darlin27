int pinArray[] = {3, 4, 5, 6, 7, 8, 9, 10, 11}; // Vector donde se van a declarar los LEDs
int waitStart = 50;                            // Tiempo entre encender un LED y otro
int tailLength = 3;                            // Numero de LEDs activos
int lineSize = 9;                              // Numero total de LEDs

int LED = 13;
int pulsador = 2;
int estado = 0;

void setup() {
  // Se indica que cada pin es de salida OUTPUT.
  int i;
  for (i = 0; i < lineSize; i++) {
    pinMode(pinArray[i], OUTPUT);
  }

  pinMode(LED, OUTPUT);
  pinMode(pulsador, INPUT_PULLUP);
}

void loop() {
  // Espera hasta que el pulsador se presione
  while (digitalRead(pulsador) == HIGH);
  
  // Cambia el estado del LED principal y de la secuencia de LEDs
  estado = !estado;
  
  // Si el estado es HIGH, enciende el LED principal y la secuencia de LEDs
  if (estado == HIGH) {
    digitalWrite(LED, HIGH); // Enciende el LED principal
    // Enciende la secuencia de LEDs
    for (int i = 0; i < tailLength; i++) {
      digitalWrite(pinArray[i], HIGH);
      delay(waitStart);
    }
  }
  // Si el estado es LOW, apaga el LED principal y la secuencia de LEDs
  else {
    digitalWrite(LED, LOW); // Apaga el LED principal
    // Apaga la secuencia de LEDs
    for (int i = 0; i < tailLength; i++) {
      digitalWrite(pinArray[i], LOW);
      delay(waitStart);
    }
  }
  
  // Espera hasta que el pulsador se suelte
  while (digitalRead(pulsador) == LOW);
}
