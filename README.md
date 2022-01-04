# Comandos Básicos Routers Cisco

- [Comandos Básicos Routers Cisco](#comandos-básicos-routers-cisco)
  - [Propósito general](#propósito-general)
  - [Edición y operaciones básica](#edición-y-operaciones-básica)
  - [Configuración Interfaces](#configuración-interfaces)
  - [Enrutamiento](#enrutamiento)
    - [Rutas estáticas](#rutas-estáticas)
    - [Protocolo Enrutamiento RIP](#protocolo-enrutamiento-rip)
## Propósito general

Habilitar el modo privilegiado:

``` Console
Router# Enable
```

Configurar (el router) desde la Terminal (teclado):

``` Console
Router# Config T
```

Renombrar el router :

``` Console
Router (config)# Hostname MIROUTER
```

Establecer la contraseña cifrada (secreta) para el modo privilegiado como “class”:

``` Console
MIROUTER(config)# Enable Secret Class
```

Establecer la contraseña  de texto del modo Usuario:

``` Console
MIROUTER(config)# Enable Password Cisco
```

Desactivar la busqueda DNS:

``` Console
MIROUTER(config)# No ip domain lookup
```

Seleccionar la interfaz E0:

``` Console
MIROUTER(config)# Interface Ethernet
```

Suministrar una descripción:

``` Console
MIROUTER(config-if)# Descripción
```

Visualizar las últimas 10 líneas de comandos en el búfer de historial:

``` Console
show history
```

Verificar el software y el hardware del router:

``` Console
Show version
```

Reiniciar el router (guardando previamente la configuración):

``` Console
Router# Reload
```

Establecer el tamaño del búfer de historial en x lineas:

``` Console
terminal history size 70
```

Desactivar el historial de comandos:

``` Console
terminal no history
```

Activar los Logs del sistema operativo en la Consola:

``` Console
Router1# Terminal monitor
```

Mostrar la tabla MAC:

``` Console
show mac-address-table
```

Encriptar las contraseñas almacenadas:

``` Console
service password-encryption
```

Mostrar estado de las interfaces del router:

``` Console
Router> show ip interface nombreinterfaz
```

Mostrar información de los vecinos:

``` Console
Router1# show cdp neighbors detail
```

Inhabilitar cdp:

``` Console
Router1(config)# no cdp run
```

Habilitar interfaces:

``` Console
Router1(config-if)# no shutdown
```

Encriptacion de contraseña:

``` Console
Router1(config)# enable password 123456
```

Guardar la configuracion del router:

``` Console
Router1# copy running-config startup-config
```

Configuracion NVRAM:

``` Console
show startup-config
```

Mostrar la configuración actual almacenada en la RAM del router:

``` Console
Router1# show running-config
```

Mostrar protocolos:

``` Console
Router1# show ip protocols
```

Borrar la configuración de inicio:

``` Console
Router1# erase startup config
```

Configurar una descripción para una interfaz, para ayudar a documentar la red:

``` Console
Router1(config-if)# description
```

## Edición y operaciones básica

Entrar al modo privilegiado:

``` Console
enable
```

Volver al modo de usuario desde el modo privilegiado:

``` Console
disable
```

Cerrar sesión o salir:

``` Console
exit router
```

Volver a mostrar el último comando:

``` Console
flecha hacia arriba o Ctrl + P
```

Volver a mostrar el siguiente comando:

``` Console
flecha hacia abajo o Ctrl + N
```

Suspender o abortar:

``` Console
Mayús y Ctrl y 6 y luego x
```

Refrescar la salida por pantalla:

``` Console
Ctrl + R
```

Completar el comando ingresado parcialmente:

``` Console
<Tab> (tecla Tabulador)
```

Desplazarse una palabra hacia atrás:

``` Console
Esc+B
```

Regresar al modo EXEC Privilegiado estando en cualquier modo de configuración :

``` Console
Ctrl+Z (o end)
```

Cancelar la ejecución del Dialogo de configuración inicial o Setup :

``` Console
Ctrl+C
```

## Configuración Interfaces

```Console
Router1(config)# Interface Serial0//
Router1(config-if)#ip address 192.168.3.1 255.255.255.0
```

## Enrutamiento

Mostrar Tabla de enrutamiento:

``` Console
Router1# show ip route
```

Comienza debuging para enrutamiento ip y se muestran los cambios de ip route:

``` Console
Router1# debug ip routing
```

Deshabilitar debugging:

``` Console
Router1# undebug all
```

Deshabilitar debuging para ip routing:

``` Console
Router1# undebug ip routing
```

Habilitar la frecuencia de sincronización para las interfaces SERIAL:

``` Console
Router1(config-if)# clock rate 64000
```

### Rutas estáticas

Añadir una ruta estatica a la tabla de enrutamiento:

``` Console
Router1(config) #ip route red mascara-de-subred interfaz
```

Borrar ruta estatica:

``` Console
Router1(config)# no ip route
```

### Protocolo Enrutamiento RIP

RIP es un protocolo de enrutamiento por vector de distancia. RIP carece de la sofisticación de los protocolos de enrutamiento más avanzados, pero su simplicidad y amplia utilización representa el testimonio de su persistencia.

- RIP es un protocolo de enrutamiento por vector de distancia.
- RIP utiliza el conteo de saltos como su única métrica para la selección de rutas.
- Las rutas publicadas con conteo de saltos mayores que 15 son inalcanzables.
- Se transmiten mensajes cada 30 segundos.

Cada vez que agregue un router al de enrutamiento RIP, tendría que configurar otra ruta estática por defecto. En varios protocolos de enrutamiento, incluido RIP, usted puede utilizar el comando `default-information originate` en el modo de configuración de router para especificar que este router originará la información predeterminada, al propagar la ruta estática por defecto en las actualizaciones RIP.

- RIP v1:No soporta subredes ni CIDR (Encaminamiento Inter-Dominios sin Clases, estándar para la interpretación de direcciones IP). Tampoco incluye ningún mecanismo de autentificación de los mensajes. Actualmente en desuso. Se rige por la RFC 1058.
- RIP v2: Soporta subredes, CIDR y VLSM. Soporta autenticación utilizando uno de los siguientes mecanismos: no autentificación, autentificación mediante contraseña, autentificación mediante contraseña codificada mediante MD5 (desarrollado por Ronald Rivest). Se rige por la RFC 1723-2453.
- RIPng: RIP para IPv6. Se rige por la RFC 2080.

Habilitar rip:

``` Console
Router1(config)#router rip
```

Mostrar actualizaciones:

``` Console
Router1#debug ip rip
```

No enviar actualizaciones RIP desde una interfaz:

``` Console
Router1(config-router)# passive-interface tipo-interfaz número-interfaz
```

Habilitar rip en todas las interfaces que pertenecen a una red específica:

``` Console
Router1(config-router)# network dirección-red
```

Desahabilitar rip:

``` Console
Router1(config)# no router rip
```

Router va a originar información por defecto mediante la propagación de la ruta estática por defecto en la actualización RIP:

```Console
Router1(config-router)# default-information originate
```

Redistribuir la ruta estática:

``` Console
Router1(config-router)# redistribute static
```

Establece una ruta estática en la interfaz null:

``` Console
Router1(config-router)# ip route 192.168.0.0 255.255.0.0 null interface
```

Difundir ruta estática mediante un protocolo de enrutamiento:

``` Console
Router1(config)# redistribute static
```

Habilitar v2:

``` Console
Router1(config-router)# version 2
```

Deshabilitar sumarizacion automática de ruta por defecto en Ripv2:

``` Console
Router1(config-router)# no auto-summary
```

Cambia el modo de enrutamiento del router a enrutamiento con clase:

``` Console
Router1(config)# no ip classless
```
