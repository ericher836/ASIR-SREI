**¿Quién, dónde y cuándo se crea el primer servidor web?**

El primer servidor web lo crea Tim Berners Lee, físico del CERN, en 1990. 

**¿Qué es pila de protocolos usados por http?**

TCP/IP. 

**¿Componentes de una URL?**

Protocolo, dominio o anfitrión, puerto, ruta de archivos o recursos y cadena de búsquedas. 

**¿Pasos en la recuperación de una página web mediante HTTP?**

El cliente manda una petición hacia el servidor web, y este envía una respuesta junto con un código de 
respuesta. La petición suele ser del tipo GET para obtener páginas web. 

**Diferencia entre páginas dinámicas y estáticas.**

Una página dinámica es aquella que se construye sobre la marcha, mientras que una estática suele ser un 
fichero, una página que no cambia y siempre está ahí. 

**Request. Métodos principales.**

GET, que solicita un recurso; POST, que envía datos para que sean procesados por el recurso; HEAD, igual 
que GET, pero solo recibe la cabecera; PUT, igual que POST, pero hace referencia a los datos y no al recurso; 
y DELETE, que borra el recurso 

**Response. Códigos.**

Códigos con formato 1xx son respuestas informativas. Indica que la petición ha sido recibida y se está 
procesando. 
Códigos con formato 2xx son respuestas correctas. Indica que la petición ha sido procesada correctamente. 
Códigos con formato 3xx son respuestas de redirección. Indica que el cliente necesita realizar más acciones 
para finalizar la petición. 
Códigos con formato 4xx son errores causados por el cliente. Indica que ha habido un error en el procesado de 
la petición a causa de que el cliente ha hecho algo mal. 
Códigos con formato 5xx son errores causados por el servidor. Indica que ha habido un error en el procesado 
de la petición a causa de un fallo en el servidor.            

**Content type. Tipos principales.**

El Content-Type indica el tipo de contenido de la petición en POST o PUT; consiste en un tipo: type y un 
subtipo: subtype. Los tipos principales son: text/html, text/css, audio/aac e image/jpeg.
