:arrow_left: [Regresar](https://github.com/ErikMontiel/tarea/blob/master/README.md)
# Metodos de Peticion  HTTPs

## Introducción
##### HTTP define un conjunto de métodos de petición para indicar la acción que se desea realizar para un recurso determinado. Aunque estos también pueden ser sustantivos, estos métodos de solicitud a veces son llamados HTTP verbs.
##

### GET
##### El método GET se emplea para leer una representación de un resource. En caso de respuesta positiva (200 OK), GET devuelve la representación en un formato concreto: HTML, XML, JSON o imágenes, JavaScript, CSS, etc. En caso de respuesta negativa devuelve 404 (not found) o 400 (bad request). Por ejemplo en la carga de una página web, primero se carga la url solicitada:

_Los formularios también pueden usarse con el método GET, donde se añaden los keys y values buscados a la URL del header:_ 

```
<form action="formget.php" method="get">
    Nombre: <input type="text" name="nombre"><br>
    Email: <input type="text" name="email"><br>
    <input type="submit" value="Enviar">
</form>
```
### POST
##### Aunque se puedan enviar datos a través del método GET, en muchos casos se utiliza POST por las limitaciones de GET. En caso de respuesta positiva devuelve 201 (created). Los POST requests se envían normalmente con formularios:
```
<form action="formpost.php" method="post">
    Nombre: <input type="text" name="nombre"><br>
    Email: <input type="text" name="email"><br>
    <input type="submit" value="Enviar">
</form>
```

### PUT
##### Utilizado normalmente para actualizar contenidos, pero también pueden crearlos. Tampoco muestra ninguna información en la URL. En caso de éxito devuelve 201 (created, en caso de que la acción haya creado un elemento) o 204 (no response, si el servidor no devuelve ningún contenido). A diferencia de POST es idempotente, si se crea o edita un resource con PUT y se hace el mismo request otra vez, el resource todavía está ahí y mantiene el mismo estado que en la primera llamada. Si con una llamada PUT se cambia aunque sea sólo un contador en el resource, la llamada ya no es idempotente, ya que se cambian contenidos.
```
PUT ejemplo.com/usuario/peter HTTP/1.1

```
### PATCH
##### El método HTTP PATCH aplica modificaciones parciales a un recurso. Las peticiones identicas sucesivas pueden tener efectos diferentes. Sin embargo,  es posible emitir peticiones PATCH de tal forma que sean idempotentes.
```
PATCH /file.txt HTTP/1.1 
Host: www.example.com
Content-Type: application/example
If-Match: "e0023aa4e"
Content-Length: 100

[description of changes]
```

### DELETE
##### Simplemente elimina un resource identificado en la URI. Si se elimina correctamente devuelve 200 junto con un body response, o 204 sin body. DELETE, al igual que PUT y GET, también es idempotente.
```
DELETE ejemplo.com/usuario/peter HTTP/1.1
```

### HEAD
##### Es idéntido a GET, pero el servidor no devuelve el contenido en el HTTP response. Cuando se envía un HEAD request, significa que sólo se está interesado en el código de respuesta y los headers HTTP, no en el propio documento. Con este método el navegador puede comprobar si un documento se ha modificado, por razones de caching. Puede comprobar también directamente si el archivo existe.

##### El método HEAD es muy similar al GET (funcionalmente hablando), a excepción de que el servidor responde con líneas y headers, pero no con el body de la respuesta.

```
GET /index.html HTTP/1.1  
User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
Host: www.yosoy.dev
Accept-Language: es-mx
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
```

### OPTIONS
##### El método OPTIONS es utilizado para describir las opciones de comunicación para el recurso de destino.

##### Se necesita saber cuáles métodos de solicitud soporta el servidor de nuestra profesora, podemos utilizar curl y una solicitud OPTIONS:
```
curl -X OPTIONS https://yosoy.dev -i
```

### Mensajes de Peticiones HTTPs

##### Los códigos de estado de respuesta HTTP indican si se ha completado satisfactoriamente una solicitud HTTP específica. Las respuestas se agrupan en cinco clases:
##

- Respuestas informativas (100–199)
- Respuestas satisfactorias (200–299)
- Redirecciones (300–399)
- Errores de los clientes (400–499)
- Errores de los servidores (500–599)

##

- "100"; [Sección 10.1.1](https://tools.ietf.org/html/rfc2616#section-10.1.1) : Continuar
- "101"; [Sección 10.1.2](https://tools.ietf.org/html/rfc2616#section-10.1.2) : Protocolos de conmutación
- "200"; [Sección 10.2.1](https://tools.ietf.org/html/rfc2616#section-10.2.1): OK
- "201"; [Sección 10.2.2](https://tools.ietf.org/html/rfc2616#section-10.2.2) : Creado
- "202"; [Sección 10.2.3](https://tools.ietf.org/html/rfc2616#section-10.2.3) : Aceptado
- "203"; [Sección 10.2.4](https://tools.ietf.org/html/rfc2616#section-10.2.4) : Información no autorizada
- "204"; [Sección 10.2.5](https://tools.ietf.org/html/rfc2616#section-10.2.5) : Sin contenido
- "205"; [Sección 10.2.6](https://tools.ietf.org/html/rfc2616#section-10.2.6) : Restablecer contenido
- "206"; [Sección 10.2.7](https://tools.ietf.org/html/rfc2616#section-10.2.7) : Contenido parcial
- "300"; [Sección 10.3.1](https://tools.ietf.org/html/rfc2616#section-10.3.1) : Opciones múltiples
- "301"; [Sección 10.3.2](https://tools.ietf.org/html/rfc2616#section-10.3.2) : Movido permanentemente
- "302"; [Sección 10.3.3](https://tools.ietf.org/html/rfc2616#section-10.3.3) : Encontrado
- "303"; [Sección 10.3.4](https://tools.ietf.org/html/rfc2616#section-10.3.4) : Ver otros
- "304"; [Sección 10.3.5](https://tools.ietf.org/html/rfc2616#section-10.3.5) : No modificado
- "305"; [Sección 10.3.6](https://tools.ietf.org/html/rfc2616#section-10.3.6) : Usar proxy
- "307"; [Sección 10.3.8](https://tools.ietf.org/html/rfc2616#section-10.3.8) : Redireccionamiento temporal
- "400"; [Sección 10.4.1](https://tools.ietf.org/html/rfc2616#section-10.4.1) : Solicitud incorrecta
- "401"; [Sección 10.4.2](https://tools.ietf.org/html/rfc2616#section-10.4.2) : No autorizado
- "402"; [Sección 10.4.3](https://tools.ietf.org/html/rfc2616#section-10.4.3) : Pago requerido
- "403"; [Sección 10.4.4](https://tools.ietf.org/html/rfc2616#section-10.4.4) : Prohibido
- "404"; [Sección 10.4.5](https://tools.ietf.org/html/rfc2616#section-10.4.5) : No encontrado
- "405"; [Sección 10.4.6](https://tools.ietf.org/html/rfc2616#section-10.4.6) : Método no permitido
- "406"; [Sección 10.4.7](https://tools.ietf.org/html/rfc2616#section-10.4.7) : No aceptable
- "407"; [Sección 10.4.8](https://tools.ietf.org/html/rfc2616#section-10.4.8) : Se requiere autenticación de proxy
- "408"; [Sección 10.4.9](https://tools.ietf.org/html/rfc2616#section-10.4.9) : Solicitar tiempo de espera
- "409"; [Sección 10.4.10](https://tools.ietf.org/html/rfc2616#section-10.4.10) : Conflicto
- "410"; [Sección 10.4.11](https://tools.ietf.org/html/rfc2616#section-10.4.11) : Desaparecido
- "411"; [Sección 10.4.12](https://tools.ietf.org/html/rfc2616#section-10.4.12) : Longitud requerida
- "412"; [Sección 10.4.13](https://tools.ietf.org/html/rfc2616#section-10.4.13) : Precondición fallida
- "413"; [Sección 10.4.14](https://tools.ietf.org/html/rfc2616#section-10.4.14) : Entidad de solicitud demasiado grande
- "414"; [Sección 10.4.15](https://tools.ietf.org/html/rfc2616#section-10.4.15) : Request-URI demasiado grande
- "415"; [Sección 10.4.16](https://tools.ietf.org/html/rfc2616#section-10.4.16) : Tipo de papel no admitido
- "416"; [Sección 10.4.17](https://tools.ietf.org/html/rfc2616#section-10.4.17) : Rango solicitado no satisfactorio
- "417"; [Sección 10.4.18](https://tools.ietf.org/html/rfc2616#section-10.4.18) : Expectativa fallida
- "500"; [Sección 10.5.1](https://tools.ietf.org/html/rfc2616#section-10.5.1) : Error interno del servidor
- "501"; [Sección 10.5.2](https://tools.ietf.org/html/rfc2616#section-10.5.2) : No implementado
- "502"; [Sección 10.5.3](https://tools.ietf.org/html/rfc2616#section-10.5.3) : Puerta de enlace incorrecta
- "503"; [Sección 10.5.4](https://tools.ietf.org/html/rfc2616#section-10.5.4) : Servicio no disponible
- "504"; [Sección 10.5.5](https://tools.ietf.org/html/rfc2616#section-10.5.5) : Tiempo de espera de la puerta de enlace
- "505"; [Sección 10.5.6](https://tools.ietf.org/html/rfc2616#section-10.5.6) : Versión HTTP no compatible


## Conclusiones
##### Estos metodos permiten al cliente y al servidor enviar información adicional junto a una petición o respuesta para asi identificar el tipo de mensaje. 
