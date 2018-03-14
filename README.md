1.  
  - **Universidad Icesi**
  - **Christian David Cárdenas**
  - **A00212740**
  - **Parcial 1 sistemas distribuidos**
  - **URL Repositorio:** https://github.com/cdcardenas/sd-exam1

Diagrama de despliegue

![][7]




2. Para el balaceador de cargas se utilizo nginx y se debieron automatizar 2 tareas, primero su instalacion para lo cual se creo una receta que se encargo de modificar los permisos de ejecución, otorgandoselos a vagrant. Posteriormente se habilita nginx con el comando enable y segundo una receta para la configuracion de nginx que se encarga de sobreescribir el archivo de configuración por defecto y define las variables que corresponden a las direcciones ip de los servidores web que se van a balancear
comandos usados:


~~~
  yum install nginx
  sudo systemtcl start nginx
  sudo vim /etc/yum.repos.d/nginx.repo
  sudo vim /etc/nginx/conf.d/load-balancer.conf

  yum install httpd
  sudo systemctl start httpd.service


~~~
En los archivos de configuracion de nginx se modifico el puerto de escucha a puerto 80, tambien se modifico el upstream backend, donde se añadieron las ips de ambos servidores.


![][1]

Para aprovisionar los dos servidores web se creo una receta para httpd (Apache server), que se encarga de mostrar el nombre del servidor y su direccion ip.

![][2]
![][6]

3. Archivo Vagrantfile
- Balanceador de carga
![][3]

- servidor 1
![][4]

- servidor 2
![][5]

4.Los cookbooks fueron 2: El primero para el balanceador de carga y el segundo es para los servidores web. Se anexan los cookbooks a la entrega.




7.Uno de los problemas encontrados en el despligue de el multiambiente fue que debido a que desde el archivo Vagrant se enviaban las variables directamente para las direcciones ip de los servidores cuando se intentaba aprovisionar todo con el comando "vagrant up" ocurrian errores en el despliegue de los dos servidores web. Sin embargo, esto se pudo solucionar haciendo el aprovisionamiento por pasos. Es decir, maquina a maquina.



8.Funcionamiento(gif pesado ~90mbs demora cargando)

https://media.giphy.com/media/1AIgrCnWHEG5NAds2I/giphy.gif





[1]:images/1.png
[2]:images/2.png
[3]:images/3.png
[4]:images/4.png
[5]:images/5.png
[6]:images/6.png
[7]:images/7.png
