El módulo `bright_control` implementa el PWM para controlar el brillo de los LEDs RGB.

En el archivo `bright_control.cpp` se definen los pines de salida digital que se utilizan para el manejo de los LEDs:

```cpp
    DigitalOut RGBLed[] = {(PB_4), (PA_0), (PD_12)};
```

# Implementación del PWM
Para implementar el PWM hace uso de un ticker del microcontrolador asociado a un timer.
Define un período y un duty cycle y establece como callback de la interrupción del ticker al método `tickerCallbackBrightControl`.

Este método compara la cuenta actual de ticks y establece el estado de las salidas digitales de acuerdo a Ton y Toff calculados a partid del duty cycle y el período.

La resolución de esta implementación en el duty cycle del PWM se encuentra afectada por el casteo a int en la función `setDutyCycle`.
Esto se debe debido a que el ticker genera una interrupción cada una cantidad entera de milisegundos.


# Árbol de funciones

brightControlInit()
    ├── setPeriod()
    ├── setDutyCycle()
    └── mbed (library) para el manejo del ticker

tickerCallbackBrightControl()
    └── mbed (library) para el manejo de las salidas digitales

El PWM se actualiza automáticamente y no requiere de llamar una función update() en el módulo.
