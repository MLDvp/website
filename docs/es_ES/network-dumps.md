# Capturas de Red
Una de las mejores maneras de apoyar el proyecto es ayudando a recopilar capturas de red de juegos. Estas capturas pueden ser utilizadas por los desarrolladores para comprender cómo operan los servidores en un entorno en vivo. Este tipo de datos simplifica enormemente el desarrollo de los servidores, ya que elimina una gran cantidad de conjeturas e ingeniería inversa.

Para facilitar este proceso, hemos desarrollado una suite de herramientas internas para capturar y leer tráfico de red, además de utilizar varias herramientas disponibles en el mercado. Este documento detalla cómo capturar estos paquetes por tu cuenta y cómo puedes enviarlos para su uso en investigación y desarrollo. Este documento es bastante largo, por favor léelo completamente antes de enviar cualquier captura.

## Tabla de Contenidos
1. [Envíos](#envíos)
2. [Paquetes del Juego](#paquetes-del-juego)
   - [Wii U (HokakuCafe)](#wii-u-hokakucafe)
   - [3DS (HokakuCTR)](#3ds-hokakuctr)
   - [Todos (WireShark)](#todos-wireshark)
3. [Paquetes HTTP](#paquetes-http)
4. [SpotPass](#spotpass)
5. [Juegos de Alta Prioridad](#juegos-de-alta-prioridad)

<div class="tip red">
   <h2>Advertencia de Seguridad</h2>
   <strong>Las capturas de red pueden contener información sensible, incluyendo correos electrónicos, contraseñas, nombres de usuario, direcciones IP, etc. Por esta razón, asegúrate de proporcionar capturas de red solo a personas de confianza. Al enviar capturas a los desarrolladores de Pretendo Network, estas se suben y almacenan en un canal privado al que solo un pequeño grupo de personas tiene acceso, ni siquiera todos los desarrolladores pueden acceder.</strong>
</div>

# Envíos
Hay dos formas de enviar capturas de red. Puedes contactar directamente a un desarrollador o usar el comando `/upload-network-dump` en nuestro servidor de Discord.

Al enviar una captura, pedimos lo siguiente:

1. Realiza la menor cantidad de acciones posible por sesión. Cada sesión debe centrarse en un aspecto específico del juego para minimizar el "ruido" (paquetes no relacionados) que dificulta el análisis. Por ejemplo, en lugar de enviar una sesión jugando cursos aleatorios en *Super Mario Maker*, sería más útil enfocarse en una parte del juego, como el *Desafío 100 Marios* o marcando un curso como favorito.
2. Proporciona una descripción detallada de lo que hiciste en la sesión. Por ejemplo: "Cargué el mundo de cursos, jugué un curso aleatorio, lo marqué como favorito y luego jugué un curso recomendado".
3. Renombra los archivos de captura con un nombre significativo, como `jugado-y-marcado-curso-smm-jpn.pcap` en lugar de `hice-algo.pcap` o `12-20-23.pcap`. Esto no aplica a los archivos BIN de HokakuCafe, ya que deben mantener su nombre original.

# Paquetes del Juego
Las capturas de paquetes de juego son los paquetes enviados durante una sesión a un servidor de juego. Estos paquetes suelen estar cifrados, por lo que se requiere información adicional para poder descifrarlos.

### Wii U (HokakuCafe)
La manera más sencilla de capturar paquetes de un servidor de juegos en Wii U es utilizando [HokakuCafe](https://github.com/PretendoNetwork/HokakuCafe). Este es un módulo de configuración para Aroma que parchea IOSU para escribir todos los paquetes en un archivo `.pcap` en la tarjeta SD.

1. Descarga la [última versión](https://github.com/PretendoNetwork/HokakuCafe/releases/latest) del módulo de configuración (`30_hokaku_cafe.rpx`).
2. Coloca el archivo en `wiiu/environments/[ENTORNO]/modules/setup` en la tarjeta SD.
3. Inserta la tarjeta en la Wii U, enciéndela una vez y apágala.
4. Abre el archivo `HokakuCafe/config.ini` en la SD y establece `Mode` en `UDP` o `ALL` (evita `PRUDP` debido a un error).
5. Vuelve a insertar la SD en la Wii U; todo el tráfico de red ahora se capturará en un archivo `.pcap`.

Los archivos PCAP se guardan en la carpeta `HokakuCafe` en la SD, junto con un archivo BIN (`nexServiceToken-AAAAAAAAAA-BBBBBBBB.bin`), necesario para descifrar los paquetes. **Ambos archivos deben ser enviados**.

### 3DS (HokakuCTR)
Para capturar paquetes en 3DS, usa [HokakuCTR](https://github.com/PretendoNetwork/HokakuCTR). Este homebrew captura tráfico del juego directamente desde la consola.

1. Asegúrate de que tienes la última versión de Luma instalada (soporta plugins 3GX).
2. Descarga la [última versión](https://github.com/PretendoNetwork/HokakuCTR/releases/latest).
3. Coloca el archivo en `luma/plugins` y renómbralo `default.3gx`.
4. Al iniciar un juego, verás `Not Ready` (no compatible) o `Ready` (compatible).
5. Si ves `Detected NEX buffer type: V0` o `V1`, significa que el tráfico está siendo capturado.
6. Los archivos `.pcap` se guardarán en `HokakuCTR/[NOMBRE DEL JUEGO]`.

Las capturas de HokakuCTR ya están descifradas y pueden enviarse tal cual.

### Todos (WireShark)
Si las opciones anteriores no funcionan, puedes capturar el tráfico con WireShark y un punto de acceso Wi-Fi en tu PC. 

1. Configura un punto de acceso Wi-Fi en tu PC con WireShark instalado.
2. Conéctate con la consola a este punto de acceso.
3. Captura el tráfico de red con WireShark.

Estos paquetes estarán cifrados y requerirán las credenciales NEX para descifrarlos.

- **3DS:** Descarga y ejecuta [este homebrew](https://9net.org/~stary/get_3ds_pid_password.3dsx) para extraer el usuario y contraseña de NEX.
- **Wii U:** Usa un cliente FTP y descarga `/storage_mlc/usr/save/system/act`, busca tu NNID y extrae `PrincipalId` (usuario NEX) y `NfsPassword` (contraseña NEX).

# Paquetes HTTP
Algunos juegos usan solicitudes HTTP para ciertas funciones. Para capturar estos paquetes, se necesita un servidor proxy HTTP. La opción más sencilla es usar nuestro [contenedor Docker de mitmproxy](https://github.com/PretendoNetwork/mitmproxy-nintendo).

Consulta la documentación completa en el [repositorio de mitmproxy-nintendo](https://github.com/PretendoNetwork/mitmproxy-nintendo).

# SpotPass
SpotPass usa HTTP para descargar contenido adicional. La manera más fácil de enviarnos información de SpotPass es proporcionando la base de datos BOSS de tu consola.

- **Wii U:** Conéctate por FTP y copia `/storage_mlc/usr/save/system/boss`.
- **3DS:** Usa [GodMode9](https://github.com/d0k3/GodMode9) y extrae `00000000` desde `SYSNAND CTRNAND > data > longstring > sysdata > 00010034`.

# Juegos de Alta Prioridad
Estos juegos tienen protocolos específicos que dificultan su implementación. Las capturas de estos juegos son altamente prioritarias:

## 3DS
- *Animal Crossing - Happy Home Designer*
- *Kid Icarus: Uprising*
- *Pokémon X/Y, ORAS, Sun/Moon, Ultra Sun/Ultra Moon*
- *Super Smash Bros. for Nintendo 3DS*
- *Super Mario Maker for Nintendo 3DS*

## Wii U
- *Mario Kart 8*
- *Splatoon* y sus variantes (*Testfire*, *Demo*, *Pre-Launch Review*)
- *Super Mario Maker*
- *Super Smash Bros. for Wii U*
- *Xenoblade Chronicles X*
