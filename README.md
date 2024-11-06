# -Ejercicio_Practico_Integral-
En este repositorio se depositará todas las evidencias de la Segunda Unidad, tanto códigos como documentación. 
-Leonel Alejandro Torres Pérez. 




En esta sección, se evaluará tu capacidad para realizar y documentar ejercicios prácticos, demostrando el dominio de la programación y el uso de la ESP32 junto con distintos componentes electrónicos. Debes completar los siguientes ejercicios:
Realiza el ejercicio integral de la unidad, usando ESP32 y otros sensores de IoT para lograr un funcionamiento completo. Este ejercicio deberá:

    Demostrar el encendido, apagado o control de componentes en respuesta a sensores u otros disparadores.
    Asegúrate de que tu circuito y código estén correctamente conectados y explicados en un video de demostración de máximo 2 minutos.
    Crea una carpeta denominada Ejercicio_Practico_Integral y guarda el código fuente y el circuito correspondiente.
    En el README.md, coloca un enlace a la carpeta junto con una breve descripción del ejercicio y un enlace al video de demostración.

  https://drive.google.com/file/d/1GxbMWeFfWfFLVUm5dFeCWm7_l0nRsinc/view?usp=drive_link

## Código del instrumento de evaluación

    from machine import Pin, ADC, PWM, I2C
    import time
    from ssd1306 import SSD1306_I2C  # Librería OLED, asegúrate de tenerla instalada


    ldr = ADC(Pin(32))  # Entrada analógica para LDR (ajustar el pin según tu conexión)
    servo = PWM(Pin(15), freq=50)  # PWM para el servo motor en el pin 15
    rgb_red = Pin(12, Pin.OUT) 
    rgb_green = Pin(13, Pin.OUT)
    rgb_blue = Pin(14, Pin.OUT)

    i2c = I2C(0, scl=Pin(22), sda=Pin(21))  
    oled = SSD1306_I2C(128, 64, i2c)

    def move_servo(angle):
        duty = 40+int((angle/180)*115)
        servo.duty(duty)


    def led_color(red, green, blue):
        rgb_red.value(red)
        rgb_green.value(green)
        rgb_blue.value(blue)
    

    def read_light():
        return ldr.read() 

    while True:
        light_value = read_light()
    
     
        if light_value < 2000:  
            move_servo(90)  # Ventana abierta
            oled.fill(0)
            oled.text("Ventana: Abierta", 0, 0)
            oled.show()
            led_color(0, 0, 1)  # LED en verde
        else:
            move_servo(0)  # Ventana cerrada
            oled.fill(0)
            oled.text("Ventana: Cerrada", 0, 0)
            oled.show()
            led_color(1, 0, 0)  # LED en rojo

        time.sleep(1)
Como se mencionó en el video, el ejercicio consistía en un servomotor que simulaba una ventana, que al detectar una luz solar o de cualquier indole la ventana se abria, avisaba a una pantalla oled que imprimiera 
el estado de la ventana y un led se encendiera, en caso contrario que este apagada este se mantenía cerrada, la pantalla oled imprime su estado y la luz cambiaba a rojo. 



## Completa todos los ejercicios en clase en el uso de sensores, actuadores y ESP32


## En este primer video solamente hay dos botones y dos leds, al presionar el primer botón hace que los leds se prendan y cuando se presiona el otro botón estos dos leds se apagan.
        https://drive.google.com/file/d/1ghvr5M4oPmDDZDE77zbAuzant3tRIVGT/view?usp=sharing


## En este ejercicio se utilizó un buzzer que reproduce una melodia ya programada en C++
    https://drive.google.com/file/d/1bdu-rsIkUK2jmibtLjlsTaTXy3aoJ-i8/view?usp=drive_link
## lo mismo pero en Python
    https://drive.google.com/file/d/10PuLygDxBGYglh9VcQihmO4RB1_NJ0V_/view?usp=drive_link

## En este ejercicio usamos una matriz y un sensor de proximidad, el sensor al detectar algun movimiento hace que la matriz imprima la distancia en la que se encuentra este objeto.
    https://drive.google.com/file/d/1cajeD5N1127meBxowdPKCHOIagFzJO29/view?usp=sharing

## En esta otra practica  se uso un marca pasos con su componente y lo que hace es girar mientras el valor sea verdadero.
    https://drive.google.com/file/d/1MtrSye_etfeSk7Go_a0QlU6vwq6vJyGZ/view?usp=sharing

## El mismo ejercicio en C
    https://drive.google.com/file/d/1K2Ejocfy8J5qubNlPhXtLbt1v4PgfL7y/view?usp=sharing
## En este ejercicio se usó un servomotor y un sensor de temperatura y humedad. El sensor al detectar un cambio brusco de humedad o temperatura que supere lo establecido hará que el servomotor gire
    https://drive.google.com/file/d/1YG7LKnD1GC_hV3UGMH7PfW3HqQuS2jrP/view?usp=sharing
## En este ejercicio, se uso un joystick y un led rgb, al modificar la dirección del Joystick la luz proveniente del led rbg cambiara de color. Dependiendo de la dirección del joystick
    https://drive.google.com/file/d/1NQOY0ngAr4m_HhxIM3tCnfIlUSgnWhA_/view?usp=sharing
## En python, usamos la pantalla neopixel para imprimir un mensaje
    https://drive.google.com/file/d/1SfWO8CfvNTYT7hn1qaQF0XMBU2Q359Eg/view?usp=sharing
## En este trabajo, usamos otra vez el sensor de proximidad y 3 leds, el sensor detectará la distancia y dependiendo de los rangos establecidos dentro del código cambiará entre azúl que es lejana, amarillo una distancia media y finalmente rojo que es una distancia muy cercana. 
    https://drive.google.com/file/d/1myegby3cJUzzHFE4-8HOtv0mYrFTV9YH/view?usp=sharing


# Presenta tu avance en el proyecto navideño mediante una demostración en clase para el docente y tus compañeros, mostrando el prototipo y explicando las mejoras realizadas en el diseño, los materiales y el software utilizado. Durante la presentación en clase:
Bueno, la explicacióna groso modo es que se trata de un árbol navideño que gracias a un marcapasos este irá girando, mientras que una serie de leds simularan una serie navideña, además que el árbol contará con una estrella que es un led rgb que cambiará de color. Abajo del árbol se encontrará un regalo de naviddad y un sensor de proximidad. El sensor al detectar algo hará que el regalo se abra accionando un servomotor y dentro del regalo se deseara un feliz navidad en una pantalla oled que estará dentro de la caja de regalo. 




# Esta sección evalúa tu avance en el  y la aplicación de los conocimientos adquiridos en el contexto de IoT.
Completa todas las lecciones del curso de Python en NetAcad
![imagen](https://github.com/user-attachments/assets/fd19eaa1-e937-4398-8089-4c1b84cd5d3b)


Aplicaciones del curso de Python en mi proyecto y en mi carrera profesional.

    Este documento lo dividiré en segmentos para una más fácil comprensión del documento y para organizar de una forma más cómoda la información y expresar las mejoras que afectó en mi proyecto. Empezaré indudablemente con el primer módulo.
    Primer módulo “Bienvenido a fundamentos de Python 1”
    En este primer módulo reforzó mis conocimientos que ya sé tenían sobre el lenguaje de programación, y en general no hay mucho que explicar. Pero esto me quedó la idea más clara que los lenguajes de programación son parecidos entre sí.
     Este punto engloba más que es Python y en donde se puede programar, mencionando uno de los IDE que usamos para el proyecto: Thonny.
    
    Módulo 2. Tipos de datos, variables, operaciones básicas de entrada y salida, Operadores básicos.
    En este segundo módulo se reforzó el conocimiento en los tipos de datos que se usan en el proyecto a la hora de definir por ejemplo, una medición de temperatura, de alguna distancia, etc. 
    Además de las funciones, aunque este tema relucirá en módulos más adelante, aunque se destaca el método print(), que nos puede ayudar a ver las mediciones de los sensores. Ya se tenía la idea, y finalmente otro tema relevante fue los argumentos posicionales. Todos estos temas pueden ser guardados en variables, otro tema que es de gran importancia para mi proyecto y su lógica de programación en general.
    
    Módulo 3. Valores Booleanos, Ejecución Condicional, Bucles, Listas y su procesamiento, Operaciones lógicas y de Bit a Bit.
    En este módulo se refiere a varios puntos esenciales para los proyectos y en general, para cada proyecto en IoT, los valores booleanos ó de una forma más práctica; si algo este trabajando, o no. Un falso o un verdadero, esto enlazado con este tema. Ahora no es si trabaja algo o no. Sino que se mantiene una condición para que funcione o pare. En el caso de mi proyecto es cuando el el sensor de proximidad detecte algo todo el proyecto funcionará. Ahora, el mismo tema mantiene la lógica y continuidad, los Bucles, ahora es que trabaje cuando siga pasando alguna condición. Como menciono, importante para el funcionamiento para el funcionamiento de IoT.
    
    Módulo 4. Funciones, Tuplas diccionarios, Excepciones y Procesamiento de datos.
    Este módulo, aunque complejo y útil en mi proyecto no tuvo mucha influencia a excepción de las funciones. Yo lo definiría en “Piezas de un rompecabezas que al unirlas correctamente este crea un código ordenado y funcional” ya que al definir las funciones, se dividen por partes el código 


![imagen](https://github.com/user-attachments/assets/08ee5d0c-4ff0-4150-b249-38116ef77465)

## Este criterio se enfoca en la co-evaluación. Deberás observar el trabajo de uno de tus compañeros y proporcionar retroalimentación constructiva y respetuosa. 
    Karen Anahí Padrón es muy buena compañera de trabajo, enfocada en el proyecto y siempre trata de realizar las actividades de la mejor manera posible, aunque suele ponerse nerviosa y dudar mucho de si misma. Recomendaría trabajar en ello ya que aunque no conmigo, a algunos compañeros puede molestar eso ó retrasar algún otro proyecto. Pero en todos los aspectos es muy responsable y buena en lo que hace.
    10/9.5.



