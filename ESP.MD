![Twitter Follow](https://img.shields.io/twitter/follow/fgvilches?style=social)
![GitHub followers](https://img.shields.io/github/followers/fgvilches?style=social)

<div align="left">
  <br>
  <img src="ant_final.png" alt="Ant Logo" width="15%">
  <br>
</div>

# Proyecto Antbook: La computadora personal totalmente basada en cloud computing
### Felipe González Vilches - Desarrollado en marzo del 2018

El proyecto de antbook, como se describe en su [abstract](https://github.com/fgvilches/antbook/blob/master/pj_ab_abs.pdf) consistió en diseñar una computadora personal (acompañada de un servicio de suscripción) que era 100% basado en cloud computing.
```
Este proyecto fue desarrollado durante el primer semestre de 2018 por mí y el Ant team,
y aunque no alcanzó más que un modelo TRL 5 y un paper (del cual el abstract
adjunto en esta publicación es parte y si lo necesitas no dudes en escribirme un email) 
la idea vale la pena de ser compartida, por lo que creé la siguiente publicación.

Tenga en cuenta que todo lo que sigue fue escrito y desarrollado en 2018.
```

<div align="center">
  <br>
  <img src="antbook.png" alt="Antbook Logo" width="45%">
  <br>
</div>

### 🚀 Primero que nada ... Some background

Hoy en día no existe ninguna empresa tecnológica que no tenga un producto, solución o servicio adaptado a la nube. Es lo más moderno y actual y parece que quien no está en la nube no tendrá nada que hacer en el mundo tecnológico en el futuro. Como ejemplo de lo anterior tenemos las nubes de datos más usadas, 
¿Qué sería de los Universitarios a la hora de enviar apuntes sin la transmisión de archivos de WhatsApp o Airdrop? 
O más aún ¿sin las opciones de co-work de Google Drive?
Probablemente no se logre concebir el mismo flujo de trabajo que se ve hoy en las universidades sin dichas herramientas. 

Pero, ¿por qué si la nube es "tan poderosa" como se ve en el papel, seguimos transportando computadoras pesadas para tener un buen poder de computo y una tarjeta gráfica decentes?



- [ ] ¿Es acaso Imposible lo que se sugiere arriba?
- [ ] ¿Acaso no se nos habia ocurrido algo así?
- [ ] O es que... ¿Existe una limitación real?

Así es me puse a investigar sobre sistemas similares que funcionaban 100% "basados en la nube", y me encontré con varias sorpresas como el Nvidia Shield, que es capaz de transmitir una gran biblioteca de juegos de consola con la potencia de un teléfono celular (Nvidia Tegra 2). O plataformas latinoamericanas como GLOUD que (aunque a 720p) logran transmitir juegos fluidos y trabajan con un sistema de suscripción similar.
Pero el que más  me llamó la atención fue Parsec (el cual no funciona con un sistema de suscripción) ofrecido para transmitir tus propias computadoras, consolas y otros sin inputlag, a largas distancias y con una conexión de 10 Mbps.

Entonces, todo lo anterior me llevó a pensar que no había una limitación real para no llevar a cabo una computadora portátil basada en la nube, así que comencé a investigar la conexión a Internet (esa quizás es la limitación por la cual algo como esto no existe actualmente) y descubrí que las velocidades promedio para 4g en Chile (Mi país) son de 17.36Mbps de descarga y 8.55Mbps de carga (según Speedtest.net basado en la velocidad promedio de Claro Chile en su red 4g en la Región Metropolitana) y conexión fija Los ISP tienen una descarga promedio de 52Mbps y 10Mbps de carga (según Speedtest.net basado en la velocidad promedio de Vtr Chile en su Red de Fibra Óptica en la Región Metropolitana), de esta manera parece difícil imaginar que Internet pueda ser un limitación.

Al final, no encontramos limitaciones tecnológicas hoy (aún más pensando en un mundo que se está preparando para recibir 5G en los próximos años **)

### ⚡️ Sooooooooo La idea

En primer lugar, debo aclarar que esta tarea no es nueva en absoluto, es algo que se ha llevado a cabo dentro de oficinas durante años a través de una estructura de thin clients (con protocolos como PCOIP o RDP) conectada a un único servidor donde todas las aplicaciones y programas son ejecutados.

![Alt text](Thin_clients.png?raw=true "Thin Clents Structure")

Wikipedia define un thin client como "una computadora liviana que ha sido optimizada para establecer una conexión remota con un entorno informático basado en el servidor. El servidor realiza la mayor parte del trabajo, que puede incluir la ejecución de programas de software, la realización de cálculos y el almacenamiento de datos"

Soooooo la idea es hacer que una computadora personal basada en una estructura tipo thin client utilizando una motherboard con un bajo poder de cómputo (tipo Raspberry, Intel IoT Kit o similar), pantalla Amoled para reducir el consumo de energía, batería de litio que genera una autonomía de aproximadamente 3 horas (en ese momento sabíamos que era poco pero lo dejamos así para mantener el peso bajo), Wifi, ethernet (posiblemente similar a la implementación XJACK de 3com), Bluetooth, GPS, 4G/5G (dependiendo del contacto con los operadores).

Todo lo anterior permitiría que el antbook sea especialmente ligero y barato.

### 🔌 On the SaaS Side...

La idea es un servicio de suscripción pero un poco diferente de los que existen actualmente como Netflix o Spotify (Cabe señalar que en la fecha en que esto se escribió no era de mi conocimiento servicios como Stadia), el servicio ofrece al cliente diferentes tipos de planes a través de los cuales el usuario accede a una mayor poder de computo (Procesador/Tarjeta gráfica/Ram), lo que obviamente es una aproximación porque a nivel del servidor no se utilizan los mismos nombres de hardware que el cliente conoce comúnmente.

El sistema operativo debe estar idealmente basado en Linux (la distribución se seleccionará más adelante) para ejecutar Chromium y predeterminar la instalación de aplicaciones como Google Docs, Google Slides y/u otras para usar cuando el usuario no tiene acceso a Internet, además de facilitar el desarrollo del cliente local que reproducirá la imagen del servidor localmente.

Los datos generados cuando el usuario está "Desconectado" se almacenarán en el almacenamiento eMMC de la máquina que no será de mas de 64 gb o inferior a 16 gb. Cuando el usuario se conecta a Internet, estos datos se cargarán en su máquina en la nube y se mantendrán dentro de su computadora de la misma manera. Según el uso, un algoritmo determinará si estos archivos deben eliminarse permanentemente del almacenamiento local y pasarse solo al almacenamiento en la máquina en la nube. En el caso de que los archivos locales sean fotos o música, se aplicará un algoritmo de compresión para dejar una muestra local del archivo en caso de que el usuario lo necesite. Esta copia de seguridad local comprimida permanecerá como se muestra hasta que el usuario elimine el archivo original en su máquina en la nube o lo elimine manualmente de su almacenamiento local. El hecho de que todo el software se ejecute en una distribución de Linux nos permite crear fácilmente una tienda gratuita TinyApps (básicamente un administrador de paquetes) para cumplir sin conexión (para cuando el usuario no tiene acceso a Internet o no pagó por su suscripción) necesidades de los usuarios, (Pequeño editor de fotos, Pequeño Rar / Zip Compressor) Algunos fácilmente transportables desde Programas de codigo abierto.

**Plataforma**: El usuario debe poder acceder a ella mediante el botón "Ir a la plataforma" en la ventana de inicio de sesión al encender su Antbook. Al acceder a la plataforma, debe poder modificar su tipo de cuenta (prepago - pospago) además de poder modificar
El plan de equipamiento. Como usuario prepago, debe poder comprar créditos para agregar a su cuenta. La opción de conectividad (wifi, 4g/5g, Bluetooth) debe estar habilitada dentro de la plataforma para que el usuario pueda acceder a estas opciones.

### ✨ Bottomline

**¿Por qué es esto necesario?**: En el mundo de hoy, el Antbook se hace necesario para responder a las necesidades de **conectividad** y **portabilidad** ya que podríamos llevar un poder de computo muy alto (incluso un poder de computo a inimaginable para transportar fácilmente) en poco peso.

**Portabilidad**: Podríamos simplemente olvidarnos de llevar nuestro Antbook si es que en el lugar al que vamos sabemos que habrá otro, puesto que gracias a la plataforma simplemente haríamos Login con nuestro usuario y continuamos trabajando de donde lo dejamos cuando estábamos en casa, por que es cloud computing.

**Seguridad**: Con Antbook la seguridad ya no sería algo de lo que preocuparnos puesto que en caso de algún robo nuestro Antbook sería fácil de triangular con su modulo GPS. Además de esto, dentro de él los datos locales estarían encriptados. Cabe destacar que nuestro pc completa continuaría estando en la nube por ende en caso de no recuperarla solo tendríamos que reemplazar el dispositivo y nuestro pc continuaría tal y como lo dejamos el ultimo día que lo vimos. Seguro y Confiable. 

**Soporte**: El soporte es un plus en el Antbook, puesto que al ser un equipo que vive dentro de un ambiente técnico, el usuario tendría soporte total. Además, siempre podría generar Tickets de Soporte para solicitar ayuda los cuales serían respondidos a la brevedad. 

**Bottomline**: Todo Esto beneficiaria a Diseñadores, Ingenieros, Gamers, Productores, Publicistas, Programadores y un sinfín de gente que necesita Gran poder de computo y portabilidad a la vez, o personas que simplemente quieren que se vele por la seguridad de su información. 

--

Yyyyyyy, básicamente, este es el final de la publicación, si estás interesado en cómo continuó este proyecto o deseas obtener el paper
no dude en escribirme un email a -> hola@fgvilches.info

That's all, See ya sound🔈!🔈!

--
```

     |` _   .| _|_  _  _
    ~|~(_|\/||(_| |(/__\
        _|         
© Proyecto Desarrollado entre Mar. y Jun. 2018, Re-editado en Nov. 2019.
```
