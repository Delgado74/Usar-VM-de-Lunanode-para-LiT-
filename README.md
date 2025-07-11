# ✨ Tutorial: Nodo Bitcoin podado + LiT en Lunanode (Signet)

## 🧠 Índice

1. Introducción
2. Descripción de las herramientas

   * 2.1. ¿Qué es Lunanode?
   * 2.2. ¿Qué es LiT (Lightning Terminal)?
3. Manos a la obra: preparando tu entorno

   * 3.1. Crear un par de llaves SSH
   * 3.2. Crear una máquina virtual (VM)
   * 3.3. Acceso remoto y trabajo desde terminal
   * 3.4. Clonar los scripts desde GitHub
   * 3.5. Uso de los scripts
4. Ventajas y desventajas de esta solución

---

## 🗒️ Introducción

Tener un nodo Bitcoin completo y operativo, ya sea para operar canales Lightning o verificar tus propias transacciones, es una excelente forma de contribuir a la red y usar Bitcoin con soberanía. Sin embargo, mantenerlo funcionando de manera constante requiere recursos que no siempre están disponibles: fluido eléctrico estable, conexión a internet permanente y una computadora que pueda estar encendida durante semanas o meses. Para muchas personas, esto no es viable.

Por eso, soluciones en la nube como **Lunanode** ofrecen una alternativa realista y práctica. Puedes desplegar una **máquina virtual (VM)** en minutos, con los recursos necesarios para correr un nodo podado de Bitcoin, un nodo LND y la interfaz web de **LiT (Lightning Terminal)**, todo sobre la red de prueba **Signet**, ideal para experimentar sin riesgos.

Este tutorial te guía paso a paso para lograrlo con el plan más económico de Lunanode, utilizando herramientas mantenidas por la comunidad como los **scripts de instalación de FoxtrotZulu**.

---

## 🔧 Descripción de las herramientas

### 2.1 ¿Qué es Lunanode?

**Lunanode** es un proveedor de infraestructura en la nube con enfoque técnico y precios accesibles. Ofrece **máquinas virtuales (VMs)** personalizables, pagos con Bitcoin y Lightning, snapshots automáticos, direcciones IP públicas y almacenamiento adicional. Uno de sus principales atractivos es el **plan de 7 USD mensuales**, que incluye:

* 1 vCPU
* 2 GB de RAM
* 20 GB de disco SSD
* 1 dirección IPv4 pública
* Transferencia mensual de hasta 1 TB

Lunanode permite desplegar servidores de forma inmediata, acceder por SSH, montar volúmenes adicionales y automatizar configuraciones. Es ideal para proyectos pequeños como correr un nodo podado de Bitcoin (con pruning a 2 GB) y un nodo Lightning, especialmente en entornos educativos o de prueba como **Signet**.

### 2.2 ¿Qué es LiT (Lightning Terminal)?

**LiT (Lightning Terminal)** es una suite web desarrollada por Lightning Labs que combina varias herramientas clave para operar y gestionar nodos LND de forma amigable e integrada. Algunas de sus funciones más destacadas:

* **Interfaz web** para controlar y monitorear tu nodo desde el navegador
* **Loop**: facilita la entrada y salida de fondos entre Lightning y la cadena
* **Pool**: mercado de liquidez para abrir canales (solo disponible en mainnet)
* **Terminal CLI**: acceso remoto por comandos desde el navegador
* **Integración total con LND**, sin herramientas externas adicionales

Funciona perfectamente sobre testnet o signet, ideal para aprender sin riesgo.

---

## ✍️ Manos a la obra: preparando tu entorno

### 3.1 Crear un par de llaves SSH

En tu computadora local (Linux o Mac), abre una terminal y ejecuta:

```bash
ssh-keygen -t ed25519 -C "tu-correo@example.com"
```

Presiona Enter para aceptar los valores por defecto. Esto creará dos archivos:

* `~/.ssh/id_ed25519` (clave privada)
* `~/.ssh/id_ed25519.pub` (clave pública)

Para copiar la clave pública, ejecuta:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copia toda la línea que se muestra y pégala en:

* El panel de Lunanode (sección SSH Keys)
* GitHub (si vas a clonar con SSH)
* El servidor, si se requiere autenticación manual

**Ejemplo:**

```
ssh-ed25519 AAAAC3... usuario@mail.com
```

### 3.2 Crear una máquina virtual (VM)

1. Ingresa a [https://www.lunanode.com](https://www.lunanode.com) y crea una cuenta.
2. Accede al panel de control y agrega saldo.
3. Ve a “Virtual Machines” → “Create VM”.
4. Selecciona la región (ej. Montreal) y escoge Ubuntu 22.04.
5. Elige el plan de \$7 USD/mes (1 vCPU, 2 GB RAM, 20 GB SSD).
6. Asigna un nombre a tu VM.
7. Añade la clave pública SSH en el panel izquierdo, sección SSH.

Opcional: puedes configurar una contraseña temporal que luego reemplazarás con acceso SSH.

### 3.3 Acceso remoto y trabajo desde terminal

Conecta a tu VM usando la IP pública:

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@IP-DE-TU-VM
```

Ya puedes trabajar en tu VM como si fuera una máquina local.

### 3.4 Clonar los scripts desde GitHub

Desde la terminal de tu VM:

Ir al repositorio:

https://github.com/LibreriadeSatoshi/ejecuta-litd

Seguir todas las instrucciones desde el mismo y podrás tener acceso a los scripts creados por FoxtrotZulu (https://github.com/Foxtrot-Zulu?tab=repositories)

### 3.5 Uso de los scripts

Antes de ejecutarlos, edita los siguientes archivos ubicados en la carpeta `scripts`:

```bash
cd scripts
nano bitcoin_setup.sh            # si vas a compilar Bitcoin desde fuente
nano bitcoin_setup_binary.sh     # si vas a usar binarios precompilados
```

Modifica estas líneas según los recursos de tu VM:

```bash
dbcache=3000   # cambia a 1000
prune=50000    # cambia a 2000
```

Estas configuraciones están pensadas para:

* Usar solo 1 GB de RAM para el cache de la base de datos
* Limitar el espacio ocupado por la cadena a 2 GB en disco

Luego sigue las instrucciones del archivo `README.md` del repositorio para ejecutar los scripts, que instalarán:

* Bitcoin Core con pruning
* LND configurado para la red Signet
* LiT accesible vía navegador en el puerto `8443`

---

## ⚖️ Ventajas y desventajas de esta solución

### ✅ Ventajas

* **Accesible**: por solo 7 USD al mes puedes tener tu nodo funcionando 24/7
* **Independencia del entorno físico**: no dependes del clima ni del fluido eléctrico local
* **Fácil de usar**: el panel de Lunanode es intuitivo y permite reinstalar en minutos
* **Escalable**: puedes mejorar los recursos si el proyecto crece
* **Ambiente de pruebas sin riesgo**: al usar Signet puedes experimentar sin perder fondos
* **LiT ofrece una interfaz amigable y poderosa**, ideal para principiantes y usuarios avanzados

### ❌ Desventajas

* **Dependes de un tercero**: aunque tienes control del sistema, la infraestructura no es tuya
* **Posibles caídas o latencia** si hay problemas en la red de Lunanode
* **Seguridad**: debes proteger bien tus llaves SSH y acceso a la VM
* **Sin entorno gráfico (GUI)**: todo se hace desde la terminal o el navegador
