# ✨ Tutorial: Nodo Bitcoin podado + LiT en Lunanode (Signet)

## 🧠 Índice

1. Introducción  
2. Descripción de las herramientas  
   2.1. ¿Qué es Lunanode?  
   2.2. ¿Qué es LiT (Lightning Terminal)?  
3. Manos a la obra: preparando tu entorno  
   3.1. Crear un par de llaves SSH  
   3.2. Acceso remoto y trabajo desde terminal  
   3.3. Clonar los scripts desde GitHub  
   3.4. Uso de los scripts de FoxtrotZulu  
4. Ventajas y desventajas de esta solución

---

## 🗒️ Introducción

Tener un nodo Bitcoin completo y operativo, ya sea para operar canales Lightning o verificar tus propias transacciones, es una excelente forma de contribuir a la red y de usar Bitcoin con soberanía. Sin embargo, mantenerlo funcionando de manera constante requiere una combinación de recursos que no siempre están disponibles: fluido eléctrico estable, una conexión a internet permanente y una computadora que se pueda dejar encendida durante semanas o incluso meses. Para muchas personas, esto no es viable.

Por eso, soluciones en la nube como **Lunanode** ofrecen una alternativa realista y práctica. Puedes desplegar una **máquina virtual (VM)** en cuestión de minutos, con los recursos necesarios para correr un nodo podado de Bitcoin, un nodo LND y la interfaz web de **LiT (Lightning Terminal)**, todo sobre la red de prueba **Signet** para experimentar sin riesgos.

Este tutorial te guía paso a paso para hacerlo con el plan más económico de Lunanode, utilizando herramientas mantenidas por la comunidad como los **scripts de instalación de FoxtrotZulu**.

---

## 🔧 Descripción de las herramientas

### 2.1 ¿Qué es Lunanode?

**Lunanode** es un proveedor de infraestructura en la nube con enfoque técnico y precios muy accesibles. Ofrece **máquinas virtuales (VMs)** personalizables, pagos con Bitcoin y Lightning, snapshots automáticos, direcciones IP públicas, y almacenamiento adicional. Uno de sus principales atractivos es el **plan de 7 USD mensuales**, que incluye:

- 1 vCPU  
- 1 GB de RAM  
- 20 GB de disco SSD  
- 1 dirección IPv4 pública  
- Transferencia mensual de hasta 1 TB  

Además, Lunanode permite desplegar servidores de forma inmediata, acceder por SSH, montar volúmenes adicionales y automatizar configuraciones. Es ideal para proyectos pequeños, como correr un nodo podado de Bitcoin (con pruning a 2 GB) y un nodo Lightning, especialmente en entornos educativos o de prueba como **Signet**.

### 2.2 ¿Qué es LiT (Lightning Terminal)?

**LiT (Lightning Terminal)** es una suite web desarrollada por Lightning Labs que combina varias herramientas clave para operar y gestionar nodos LND de forma más amigable e integrada. Algunas de sus características más importantes son:

- **Interfaz web**: permite controlar y monitorear tu nodo desde el navegador.
- **Loop**: facilita la entrada y salida de fondos entre Lightning y la cadena.
- **Pool**: un mercado de liquidez para abrir canales de forma eficiente (solo mainnet).
- **Terminal CLI**: acceso remoto vía comandos desde el navegador.
- **Integración total con LND**, sin necesidad de instalar herramientas externas adicionales.
- Funciona perfectamente sobre testnet o signet, ideal para aprender sin riesgo.

---

## ✍️ Manos a la obra: preparando tu entorno

### 3.1 Crear un par de llaves SSH

En tu computadora local (Linux o Mac), abre una terminal y escribe:

```bash
ssh-keygen -t ed25519 -C "tu-correo@example.com"
````

Presiona Enter para aceptar los valores por defecto. Esto creará dos archivos:

* `~/.ssh/id_ed25519` (clave privada)
* `~/.ssh/id_ed25519.pub` (clave pública)

Sube la clave pública en tu cuenta de **Lunanode** y también agrégala a tu cuenta de **GitHub**, si vas a clonar repositorios usando SSH.

### 3.2 Acceso remoto y trabajo desde terminal

Una vez desplegada la VM en Lunanode, conecta usando su IP pública:

```bash
ssh -i ~/.ssh/id_ed25519 ubuntu@IP-DE-TU-VM
```

Una vez dentro de la VM, ya puedes trabajar como si fuera una máquina local.

### 3.3 Clonar los scripts desde GitHub

Desde la terminal de tu VM, clona el repositorio de FoxtrotZulu:

```bash
git clone git@github.com:FedeZupicich/foxtrotzulu.git
cd foxtrotzulu
```

Si usas HTTPS en lugar de SSH:

```bash
git clone https://github.com/FedeZupicich/foxtrotzulu.git
```

### 3.4 Uso de los scripts de FoxtrotZulu

Dentro del repositorio, encontrarás scripts como `install.sh` o carpetas según el sistema que elijas (por ejemplo, `signet-bitcoin-lnd-lit`). Sigue las instrucciones del README correspondiente o ejecuta el script principal:

```bash
cd signet-bitcoin-lnd-lit
chmod +x install.sh
./install.sh
```

Este script automatiza:

* Instalación de Bitcoin Core con pruning a 2 GB
* Instalación y configuración de LND en Signet
* LiT integrado con acceso vía navegador (puerto 8443)

---

## ⚖️ Ventajas y desventajas de esta solución

### ✅ Ventajas

* **Accesibilidad**: Cualquiera con 7 USD al mes puede tener un nodo 24/7.
* **No dependes del clima ni del fluido eléctrico de tu zona.**
* **Facilidad de uso**: Lunanode tiene panel sencillo y permite reinstalar fácilmente.
* **Escalabilidad**: puedes subir a un plan superior si necesitas más recursos.
* **Aprendizaje sin riesgos**: usar Signet te permite probar todo sin perder fondos.
* **LiT es amigable y potente**, ideal para usuarios nuevos y avanzados.

### ❌ Desventajas

* **Dependes de un tercero**: aunque tienes control del sistema, la infraestructura no es tuya.
* **Latencia o caídas ocasionales** si la red de Lunanode presenta problemas.
* **Debes tener cuidado con la seguridad SSH y el manejo de las claves.**
* **Sin acceso gráfico (GUI)**: todo se hace desde terminal o navegador remoto.
