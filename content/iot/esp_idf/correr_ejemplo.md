---
title: "Hello World!"
description: ""
date: 2023-08-10T15:09:25Z
lastmod: 2023-08-10T15:09:25Z
draft: false
images: []
weight: 10
---

## Primer proyecto

Una vez que hayan instalado el ESP-IDF, estaremos listos para comenzar con nuestro primer proyecto. Usaremos el ejemplo `get-starded` (El Hello World de ESP-IDF) disponible en el repositorio.

## 1. Copiar el ejemplo a un directorio de trabajo

La carpeta a copiar se descargó durante la instalación. Pueden encontrarla en el directorio donde se almacenó el repositorio. Por ejemplo:

- En Windows: `C:\Users\MiUsuario\Espressif\releases`
- En Linux: `~/esp/esp-idf`

La ruta exacta dentro del repo será `examples/get-started`.

## 2. Conectar la ESP32

- Conecten el dispositivo a su computador usando un puerto USB.

- Es posible que deban otorgar permisos al puerto para comunicarse (sobre todo en Linux):

```bash
sudo chown <tu usuario> /dev/<puerto de conexión>
```

- Verifiquen por qué puerto se ha establecido la conexión.

- En Windows: `COM<N°>`

- En Linux: `dev\ttyUSB<N°>`

- [Más información sobre la conexión serial](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/establish-serial-connection.html).

## 3. Configurar el proyecto

**Importante** - Recuerda que para utilzar las herramientas de ESP-IDF, debes abrir una terminal en la carpeta donde se encuentra el proyecto y configurar el entorno. Para esto, en la terminal, ejecuten:

```bash
. $HOME/esp/esp-idf/export.sh
```

Esto les permitirá usar las herramientas de ESP-IDF en la terminal actual ya que exporta las variables de entorno necesarias.

Para no tener que recordar esta ruta pueden generar un alias en su archivo `.bashrc` o `.zshrc` (dependiendo de su shell) con el siguiente comando:

```bash
alias get_idf='. $HOME/esp/esp-idf/export.sh'
```

Especifiquen qué dispositivo están usando y accedan a la configuración del proyecto:

```bash
cd ~/esp/examples/get-started/hello_world
idf.py menuconfig
```

Para usar las herramientas ESP-IDF, la estructura de comando es `idf.py <Comandos>`.

- [Información sobre comandos disponibles](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-py.html).

## 4. Buildear el proyecto

Compilen el programa con el comando:

```bash
idf.py build
```

Si surgen errores de compilación o necesitan reconstruir el proyecto, utilicen:

```bash
idf.py fullclean # Elimina todos los archivos generados de la compilación
```

## 5. Flashear el proyecto

Tras la compilación, procedan a cargarlo en el ESP32:

```bash
idf.py -p PORT flash
```

Durante la ejecución, mantengan presionado el botón de `boot` en el dispositivo. Una vez establecida la conexión, pueden soltarlo.

## 6. Monitor la ESP32

Observen el comportamiento del dispositivo con el comando:

```bash
idf.py -p <PORT> monitor
```

Por lo general, el puerto de conexión es el mismo que se usó para flashear el dispositivo y en caso de que solo tengan una ESP32 conectada, no es necesario especificarlo y su comando quedaría (lo mismo para los comandos anteriores):

```bash
idf.py monitor
```

Este comando les permitirá ver la salida del programa en la consola. Para salir, presionen `Ctrl + ]`.

Deberían ver un mensaje similar a:

```bash
Hello world!
This is esp32 chip with 2 CPU core(s), WiFi/BT/BLE, silicon revision 1, 2 MB external flash
Minimum free heap size: 298968 bytes
Restarting in ... seconds...
```

¡Felicidades! Han ejecutado con éxito su primer proyecto de ejemplo en el dispositivo. Ahora es el momento de trabajar en su propio proyecto para la tarea. Consulten la [documentación](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/index.html) y prueben los ejemplos del repositorio para familiarizarse con las funcionalidades de la ESP32 que usarán en el curso.

### Resumen de comandos mas usados

- `idf.py build`: Compila el proyecto.

- `idf.py flash`: Carga el proyecto en el dispositivo.

- `idf.py monitor`: Muestra la salida del programa en la consola.

- `idf.py menuconfig`: Abre el menú de configuración del proyecto.

Por lo general si solo tienen una ESP-32 conectada a su computador no necesitan especificar el puerto de conexión. En caso de que tengan más de una, pueden especificar el puerto con el argumento `-p <puerto>`.

Tambien se pueden ejecutar varios comandos en una sola linea. Por ejemplo:

```bash
idf.py build flash monitor
```
