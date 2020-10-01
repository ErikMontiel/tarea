# Modelo Vista Controlador (MVC)

## Introducción


Existen múltiples procesos o estándares que permiten asegurar la calidad de un producto de software, la cual atiende a parámetros que son deseables, o más bien, necesarios para todo el proceso de desarrollo, como la estructuración de programas y la posibilidad de reutilización de códigos que son aspectos frecuentemente utilizados en metodologías de desarrollo. 

Una de las soluciones para mejorar el proceso de desarrollo ha sido la arquitectura basada en “capas” que separan el código de un programa en función de sus responsabilidades. 
Por lo que se vio a la necesidad de aplicar una arquitectura útil como es el Modelo Vista-Controlador (MVC), que requiere de la separación del código de un programa en capas atendiendo a sus responsabilidades.
#


### MVC y  su relación con los patrones de diseño de software


##### Modelo: 
- Representa los datos que el usuario está esperando ver, pero no contiene ninguna lógica que describa cómo presentar los datos a un usuario.

##### Vista: 
- Se encarga de transformar el modelo para que sea visualizada por el usuario, ya sea un archivo de texto normal o en una página Web que el navegador pueda desplegar. El propósito de la Vista es convertir los datos para que el usuario le sean significativos y los pueda interpretar fácilmente.

##### Controlador:
- Es la parte lógica que es responsable de procesamiento y comportamiento de acuerdo a las peticiones (request) del usuario construyendo un modelo apropiado, y pasándolo a la vista para su correcta visualización.


# Marco Teórico

El patrón Modelo, Vista y Controlador (mvc) es el más extendido para el desarrollo de aplicaciones donde se deben manejar interfaces de usuarios, éste se centra en la separación de los datos o modelo, y la vista, mientras que el controlador es el encargado de relacionar a estos dos y su principal característica es aislar la vista del modelo.

#### Se pueden encontrar muchas implementaciones de MVC, pero generalmente el flujo de datos se describe de la siguiente forma

1. El usuario interactúa con la interfaz de usuario de alguna forma (por ejemplo, el usuario pulsa un botón, enlace, etc.).
#####
2. El controlador recibe (por parte de los objetos de la interfaz-vista) la notificación de la acción solicitada por el usuario. El controlador gestiona el evento que llega, frecuentemente a través de un gestor de evento(handler) o callback.
#####
3. El controlador accede al modelo, actualizándolo, posiblemente modificándolo de forma adecuada a la acción solicitada por el usuario. Los controladores complejos están a menudo estructurados usando un patrón de comando que encapsula las acciones y simplifica su extensión.
#####
4. El controlador delega a los objetos de la vista la tarea de desplegar la interfaz de usuario. La vista obtiene sus datos del modelo para generar la interfaz
apropiada para el usuario donde se reflejan los cambios en el modelo. El modelo no debe tener conocimiento directo sobre la vista. Sin embargo, se podría utilizar el patrón Observador para proveer cierta indirección entre el modelo y la vista, permitiendo al modelo notificar a los interesados de cualquier cambio.
#####
5. La interfaz de usuario espera nuevas interacciones del usuario, comenzando el 
ciclo nuevamente.

## Existen dos tipos de patrón MVC


##### MVC tipo 1:
Las paginas JSP están en el centro de aplicación y contiene tanto la lógica de control como la de presentación. Este tipo de arquitectura funciona de la siguiente manera: el cliente hace una petición o una página JSP, se construye la lógica de la página, generalmente en objetos java y se transforma el modelo para ser desplegado una vez más.

###
![MVC_Tipo1](https://user-images.githubusercontent.com/72040398/94766892-52c8a100-0371-11eb-80f1-dcbd4acc6407.png)
###

##### MVC tipo 2:
Aquí ya existe una clara separación entre el Controlador y el Vista, ya que ahora es directamente el Controlador quien recibe la petición, prepara el modelo y lo transforma para que sea desplegado en la vista. Esta arquitectura se utiliza para aplicaciones complejas.
###

![MVC_Tipo2](https://user-images.githubusercontent.com/72040398/94766938-56f4be80-0371-11eb-968e-2fa858618814.png)

###
# ¿Qué ventajas ofrece el modelo MVC?

- **Proceso de desarrollo más rápido:** MVC apoya el desarrollo rápido y paralelo, ya que al utilizar el patrón, se desarrolla de una forma más eficiente debido a que una persona puede trabajar en la vista, mientras que otra puede trabajar en el controlador y así crear la lógica.

- **La modificación no afecta a todo el modelo:** Cualquier cambio en el modelo no afectará a toda la arquitectura de la aplicación, porque la parte del modelo no es dependiente de algún otro componente como las vistas.

- **Soporte para la técnica asíncrona:** MVC es compatible con la técnica asíncrona, la cual ayuda al programador a desarrollar, y permite que la aplicación pueda tener un rendimiento superior al cargar su contenido.

# ¿Qué otros modelos/frameworks existen de patrones de diseño?



- [Java Swing](https://www.oracle.com/technical-resources/articles/javase/swingappfr.html), Java Enterprise Edition
- [XForms](https://www.w3.org/community/xformsusers/wiki/XForms_2.0) (formato XML estándar para la especificación de un modelo de
proceso de datos XML e interfaces de usuario como formularios web).
- [GTK+](https://www.gtk.org/)(escrito en C, toolkit creado por Gnome para construir aplicaciones
gráficas, inicialmente para el sistema X Window)
- [Google Web Toolkit](http://www.gwtproject.org/), [Apache Struts](https://struts.apache.org/).



# Resultados

### (Ejemplo) Modelo MVC en el lenguaje de preferencia 

###

#### Organización de los archivos

:page_facing_up: - index.php
#####
:open_file_folder:  - app/conexion.php
#####
:open_file_folder:  - modelo/personas_model.php
#####
:open_file_folder:  - vista/personas_view.html
#####
:open_file_folder:  - controlador/personas_controller.php
####

##

#### index.php :page_facing_up:

```
<?php
    require_once("db/db.php");
    require_once("controllers/personas_controller.php");
?>
```

####  app/conexion.php :open_file_folder:
```
<?php

    function conexion(){
        $conexion = new mysqli('127.0.0.1','root',' ','personas');

            if($conexion->connect_errno){
                echo 'Error en la conexion a nuestro Schema :' .$conexion->connect_error;
            }
             $conexion->set_charset('utf8');
             return $conexion;
    }
?>
```

#### model/personas_model.php :open_file_folder: 
```
<?php
    class personas_model{
    private $db;
    private $personas;
 
    public function __construct(){
        $this->db=Conectar::conexion();
        $this->personas=array();
    }
    public function get_personas(){
        $consulta=$this->db->query("select * from personas;");
        while($filas=$consulta->fetch_assoc()){
            $this->personas[]=$filas;
        }
        return $this->personas;
    }
}
?>
```

####  controller/personas_controller.php :open_file_folder: 

```
<?php

    require_once("models/personas_model.php");
    $per=new personas_model();
    $datos=$per->get_personas();
 
    require_once("views/personas_view.html");
?>

```
#### view/personas_view.html :open_file_folder: 

```
<!DOCTYPE html>
<html lang="es">
    <head>
        <meta charset="UTF-8" />
        <title>Personas</title>
    </head>
    <body>
        <?php
            foreach ($datos as $dato) {
                echo $dato["nombre"]."<br/>";
            }
        ?>
    </body>
</html>
```



###




#### Frameworks

- Es un término utilizado en la computación en general, para referirse a un conjunto de bibliotecas utilizadas para implementar la estructura estándar de una aplicación. 

#### ¿Qué frameworks utiliza el modelo MVC? 

- [Ruby on Rails](https://rubyonrails.org/).
- [Rhodes](http://docs.rhomobile.com/en/2.2.0/rhodes/introduction).
- [JavaServerFaces](http://www.javaserverfaces.org/).
- [Sails.JS](https://sailsjs.com/).
- [FuelPHP](https://fuelphp.com/).
- [Symfony](https://symfony.es/).
- [Django](https://www.djangoproject.com/).
- [Interface Java Objects](https://docs.oracle.com/javase/8/docs/technotes/guides/collections/overview.html).

# Conclusiones

Este patrón para el diseño y desarrollo permite producir software de alta calidad,
convirtiendo una aplicación en un módulo fácil de mantener y mejora la rapidez de su
desarrollo. La separación de capas en modelos, vistas y controladores hace que las
aplicaciones sean fáciles de entender. 

