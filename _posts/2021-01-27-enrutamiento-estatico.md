---
title: "Red"
toc: true
toc_sticky: true
permalink: /enrutamiento-estatico/
---

- **1.** Situar los host, switches, Routers (agregar routers que acepten mas de dos puertos FastEthernet) si no añadirle un módulo extra con más puertos FastEthernet.
- **2.** Segregar el dibujo por redes. Cada grupo de router + switch + hosts es una red. Cada conexión entre routers es otra red.

![](https://i.ibb.co/kKXDwXq/mapa-redes-1.jpg)
*Imagen de distribución de redes por colores creada by, Emilio Pazos 👏*

- **3.** Dar IPs a cada red. Comenzando por dar una IP a cada puerto que tenga cable dentro de cada router.
	- **3.1.** Los hosts / PC deben llevar una IP de la red en la que estén.
						La puerta de enlace debe ser la IP del router al que estén enlazados.
	- **3.2.** Agregar la IP de los router. Tanto del puerto que va hacía los Switches. Como de las Redes entre los Routers.
    - **3.3.** Encender los puertos con IP. Salvar la configuración del Router.
- **4.** Comprobar que los hosts/PC dentro de cada red independiente se vean (192.168.1.xxx, 192.168.2.xxx).
- **5.** Enrutamiento estático..
	- **5.1.** Cada router debe llevar una orden para el resto de redes que contengan hosts / PC.
	- **5.2.** Configuración: Network (red a la que quiero llegar 192.168.x.0).
      					Next Hop: IP del primer puerto del siguiente Router de hacía el lugar hacía donde quiero llegar.
	  					Mask (máscara, por defecto, en principio 255.255.255.0).
- **6.** Comprobar que cada red se vea entre sí.
				Comenzando por comprobar: Desde las redes que estén más cercanas, a las más lejanas.
				Esto nos debería ayudar a identificar posibles problemas.. 👀