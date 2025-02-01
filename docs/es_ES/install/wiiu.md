# Wii U

Puedes conectar tu Wii U a Pretendo utilizando uno de los dos métodos disponibles. Cada método tiene ventajas y desventajas, las cuales se describen en sus respectivas secciones.

- [SSSL (sin hack)](#sssl)
- [Inkay (homebrew)](#inkay)

Una vez que hayas seleccionado un método de conexión y configurado tu Wii U, consulta la sección ["Configuración de PNID"](#pnid-setup).

Si tienes datos guardados de una Nintendo Network ID que deseas transferir a tu Pretendo Network ID, sigue esta sección: ["Transferencia de datos guardados a tu cuenta de Pretendo Network"](#transferring-save-data-to-your-pretendo-network-account).

---

## SSSL  
**Ventajas:**  
- No requiere homebrew  
- Muy fácil de configurar  

**Desventajas:**  
- Solo admite un subconjunto de servicios  
- Carece de funciones y parches adicionales  
- Puede no funcionar en ciertas condiciones de ISP (se está desarrollando una herramienta de DNS autoalojada)  
- Es necesario cambiar la configuración de red para desconectarse  

SSSL es un método limitado pero sin hack para acceder a la mayoría de los servicios, aprovechando un error en el módulo SSL de la Wii U. Todos los juegos de Nintendo Network producidos por Nintendo son compatibles con SSSL, así como las funciones de Miiverse dentro del juego. Sin embargo, la aplicación principal de Miiverse, la aplicación de publicación en el juego y cualquier juego que utilice su propia pila SSL (como YouTube o WATCH_DOGS) **NO** son compatibles con este método, ya que no se ven afectados por el exploit SSL.  

### Cómo conectarse con SSSL  
1. Abre `Configuración de la consola > Internet > Conectarse a Internet`.  
2. Abre la configuración de tu conexión de red y accede a `DNS`.  
3. Selecciona `No obtener automáticamente`.  
4. Ingresa `88.198.140.154` como `DNS primario`.  
5. Ingresa otro servidor de DNS público como `DNS secundario`, por ejemplo:  
   - `8.8.8.8` (Google Public DNS)  
   - `1.1.1.1` (Cloudflare DNS)  
6. Ahora deberías poder configurar e iniciar sesión en tu Pretendo Network ID con normalidad.  

### Cómo desconectarse de Pretendo Network  
Para desconectarte, elimina la dirección `DNS primario` o cambia la configuración de DNS a `Obtener automáticamente`.  

---

## Inkay  
**Ventajas:**  
- Compatible con todos los servicios  
- Incluye funciones y parches adicionales  
- No tiene problemas con ISP  
- Se puede activar y desactivar fácilmente  

**Desventajas:**  
- Requiere homebrew  
- La configuración tiene varios pasos  

> ℹ️ **Este método asume que tu Wii U tiene homebrew con Aroma.**  
> Puedes seguir esta [guía](https://wiiu.hacks.guide/) para instalar homebrew en tu consola y luego instalar Aroma con [esta guía](https://wiiu.hacks.guide/#/aroma/getting-started).  

### Versiones disponibles  
- **Estable:** Probada ampliamente para garantizar su funcionamiento. Descarga la última versión desde [aquí](https://github.com/PretendoNetwork/Inkay/releases/latest).  
- **Bleeding Edge:** No está completamente probada y puede ser inestable. Descarga la última versión desde [aquí](https://nightly.link/PretendoNetwork/Inkay/workflows/ci/main/inkay).  

### Instalación  
1. Descarga el archivo `Inkay-pretendo.wps`.  
2. Copia el archivo en `sd:/wiiu/environments/aroma/plugins`.  
3. Inserta la tarjeta SD en tu consola y enciéndela.  
4. Verás una notificación confirmando la conexión a Pretendo Network.  

### Cómo desconectarse de Pretendo Network  
1. Pulsa `L + Abajo + SELECT` en el GamePad para abrir el menú de plugins de Aroma.  
2. Selecciona `Inkay` y luego `Patching`.  
3. Cambia la opción `Connect to the Pretendo Network` a **false**.  
4. Pulsa `B` dos veces y luego `HOME` para reiniciar la consola con las conexiones de Pretendo desactivadas.  
5. Para volver a conectarte, repite el proceso y cambia `Connect to the Pretendo Network` a **true**.  

---

## Configuración de PNID  
Después de instalar Pretendo, debes registrar una Pretendo Network ID (PNID). Hay dos formas de hacerlo:  

- **Desde la web:** Registra una cuenta [aquí](/account) y selecciona `¿No tienes una cuenta?` para crear una.  
- **Desde la Wii U:** Crea la PNID como si fuera una Nintendo Network ID.  

> ⚠️ **Advertencia:**  
> No puedes usar el mismo nombre de usuario que una cuenta de Nintendo Network ID ya vinculada a tu Wii U. Si tienes una cuenta con el mismo nombre, primero debes eliminarla de la consola.  

---

## Transferencia de datos guardados a tu cuenta de Pretendo Network  

Pretendo Network no es compatible con las cuentas de Nintendo Network ID existentes. Esto significa que debes crear una cuenta nueva. Si deseas conservar tu progreso en los juegos, puedes transferir los datos guardados a tu nueva cuenta.  

> ⚠️ **Nota:**  
> Solo funciona con datos guardados localmente. Los datos almacenados en los servidores de Nintendo **no** se pueden transferir.  

### Pasos para transferir datos guardados  
1. Descarga la aplicación de homebrew **SaveMii** desde [GitHub](https://github.com/Xpl0itU/savemii/releases) o desde la [Homebrew App Store](https://hb-app.store).  
2. Abre la aplicación desde el menú de inicio.  
3. Selecciona `Wii U Save Management`.  
4. Elige el juego cuyos datos deseas transferir y selecciona `Backup savedata`.  
5. Selecciona una ranura vacía para hacer la copia de seguridad.  
6. Escoge el perfil de tu **Nintendo Network ID**.  
7. Opcionalmente, puedes respaldar los datos compartidos (`common save data`).  
8. Pulsa `A` para iniciar la copia de seguridad.  

### Restauración de datos en la cuenta de Pretendo  
1. Vuelve al menú de juegos en SaveMii y selecciona `Restore savedata`.  
2. **⚠️ Advertencia:** Esto sobrescribirá los datos guardados existentes para ese usuario. Procede con cuidado.  
3. Selecciona la ranura de respaldo que creaste anteriormente.  
4. Escoge el perfil de tu **Pretendo Network ID**.  
5. Pulsa `A` para transferir los datos y confirma la acción.  
6. Una vez finalizado el proceso, sal de SaveMii y verifica que el juego funcione correctamente con la cuenta de Pretendo.  

Repite este proceso para cada juego cuyos datos desees transferir.
