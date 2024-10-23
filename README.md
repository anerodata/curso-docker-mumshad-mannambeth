# Curso de Docker

Curso básico de Docker Udemy [Docker for the Absolute Beginner - Hands On - DevOps](https://www.udemy.com/course/learn-docker/)
Escenario en el que Docker puede ser realmente útil

## 1 Introducción

El texto describe cómo el autor fue introducido a Docker en un proyecto anterior. Al desarrollar una aplicación que combinaba varias tecnologías (NodeJS, MongoDB, Redis), enfrentó problemas de compatibilidad entre componentes, bibliotecas y sistemas operativos. Cada vez que actualizaban o cambiaban un componente, debían revisar todas las compatibilidades, lo que dificultaba el desarrollo y despliegue, además de la configuración de entornos de desarrollo para nuevos miembros del equipo.

Docker resolvió estos problemas al permitir que cada componente se ejecute en un contenedor aislado, con sus propias dependencias y bibliotecas, pero compartiendo el mismo kernel del sistema operativo. Esto facilitó el desarrollo, permitiendo que los entornos sean consistentes independientemente del sistema operativo subyacente. Docker, aunque no es nuevo, usa tecnologías como LXC y proporciona una herramienta fácil de usar para manejar estos contenedores. A diferencia de las máquinas virtuales, los contenedores son más ligeros y rápidos, ya que comparten el kernel del sistema operativo, pero tienen menos aislamiento. Docker permite empaquetar aplicaciones y ejecutarlas en cualquier entorno sin preocuparse por la compatibilidad, fomentando la cultura DevOps.

Los contenederes son entornos completamente aislados que tienen sus propios procesos, interfaces de red y montajes, al igual que las máquinas virtuales, pero todos comparten el mismo kernel del sistema operativo. Docker no inventó los contenedores, que han existido durante al menos 10 años, pero hizo que su uso fuera más accesible al proporcionar herramientas de alto nivel y potentes funcionalidades.

El autor también hace una distinción importante entre el kernel del sistema operativo y el software. Por ejemplo, en sistemas operativos como Ubuntu o Fedora, todos comparten el mismo kernel Linux, pero es el software por encima del kernel lo que los diferencia. Docker aprovecha esta arquitectura compartida del kernel para ejecutar contenedores basados en diferentes distribuciones de Linux en la misma máquina host. Sin embargo, los contenedores de Docker no pueden ejecutar sistemas operativos con kernels diferentes (como Windows) en un host Linux, a menos que se utilice una máquina virtual de Linux en un host Windows para correr contenedores de Linux.

Diferencia enre máquinas virtuales (VMs) y contenedores de Docker. Las máquinas virtuales tienen un mayor aislamiento porque cada una tiene su propio sistema operativo completo y kernel, pero esto también genera una sobrecarga, ya que consumen más recursos y espacio en disco, generalmente en gigabytes. En contraste, los contenedores de Docker son más ligeros, ocupan solo megabytes y se inician mucho más rápido (en segundos, frente a los minutos que toma una máquina virtual). Sin embargo, los contenedores comparten el kernel, lo que reduce el aislamiento entre ellos.

Ambas tecnologías pueden coexistir. En grandes infraestructuras con miles de contenedores, a menudo se utilizan máquinas virtuales para alojar varios contenedores Docker, aprovechando lo mejor de ambas tecnologías: la facilidad de virtualizar máquinas para provisionar o eliminar hosts, y la capacidad de Docker para escalar rápidamente las aplicaciones.

Muchas aplicaciones ya están "containerizadas" y disponibles en repositorios públicos como Docker Hub, lo que facilita aún más la implementación. Las imágenes de Docker, que son plantillas de sistemas operativos o servicios, se pueden ejecutar fácilmente con el comando docker run. Esto permite, por ejemplo, levantar instancias de servicios como MongoDB o Node.js con un solo comando. Si se necesitan múltiples instancias de un servicio, se pueden agregar fácilmente y configurar un balanceador de carga para gestionarlas.

Por último, se describe la diferencia entre imágenes y contenedores. Las imágenes son plantillas estáticas que se utilizan para crear contenedores, mientras que los contenedores son instancias en ejecución de esas imágenes. Los desarrolladores pueden crear sus propias imágenes y compartirlas en Docker Hub para que otros las utilicen. Esto facilita la colaboración entre los equipos de desarrollo y operaciones, ya que una vez que una imagen está configurada correctamente, puede ejecutarse en cualquier entorno con Docker instalado sin problemas de compatibilidad.

Tradicionalmente, los desarrolladores creaban aplicaciones y luego las entregaban al equipo de operaciones para desplegarlas y gestionarlas en entornos de producción. Esto requería que el equipo de operaciones siguiera instrucciones sobre cómo configurar el host, instalar dependencias y demás. Sin embargo, como no desarrollaban la aplicación, solían tener problemas durante la configuración y dependían de los desarrolladores para resolverlos. Con Docker, ambos equipos colaboran para crear un archivo Docker que contiene todos los requisitos. Este archivo se convierte en una imagen que puede ejecutarse en cualquier host con Docker, garantizando que funcione de manera uniforme en todos los entornos. Esto facilita el despliegue y refuerza la cultura DevOps.

## 2 Comandos básicos

- `docker run [image]` ejecuta un contenedor desde una imagen. Cuando el proceso termina el contenedor se detiene
- `docker run centos`: tras haber hecho un pull de centos. Ejecutaría el SO y terminaría. Docker ejecuta procesos
- `docker run centos sleep 20`: Lo mantendría en ejecución durante 20 segundos
- `docker run -it centos bash`: Ejecutaríamos el SO y después, el terminal de centos. Estaríamos en el contenedor
- `docker ps`: lista los contenedores en ejecución
- `docker ps -a`: lista los contenedores en ejecución y parados
- `docker stop [name]`: detiene un contenedor. Podemos listarlo con `docker ps -a`
- `docker rm [name]`: borra un contenedor. No podemos listarlo
- `docker images`: lista las imágenes
- `docker rmi [image]`: borra una imágen. Debemos asegurarnos de que ningún contenedor depende de esa imagen. Hay que detener y borrar dichos contenedores con el comando anterior antes de borrar
- `docker pull [image]`: descarga la imagen sin ejecutar su contenedor
- `docker exec [container_name] cat /etc/hosts`: Ejecuta el comando cat para mostrar el contenido del fichero `/etc/hosts` del contenedor en cuestión
- `docker run -d kodekloud/simple-webapp`: ejecutaría el contenedor de la imagen alojada en ese repositorio en modo _detached_. El output del servidor no se mostraría ya que se estaría ejecutando en el _background_
- `docker attach [id or name]`: Vuelve a la ejecución del docker
