# python_blockchain_app

Aplicacion funcional para localhost.

## Qué es blockchain? Cómo debo implementarlo? y cómo funciona?

Please read the [step-by-step implementation tutorial](https://www.ibm.com/developerworks/cloud/library/cl-develop-blockchain-app-in-python/index.html) to get your answers :)

## Instrucciones para que ande

Clonar el proyecto,

```sh
$ git clone https://github.com/avilaroman/python_blockchain_app.git
```
Instalar las dependencias,

`` sh
$ cd python_blockchain_app
$ pip install -r require.txt
`` `

Inicie un servidor de nodo blockchain,

`` sh
# Los usuarios de Windows pueden seguir esto: https://flask.palletsprojects.com/en/1.1.x/cli/#application-discovery
$ export FLASK_APP = node_server.py
$ frasco ejecutar --port 8000
`` `

Una instancia de nuestro nodo blockchain ahora está en funcionamiento en el puerto 8000.


Ejecute la aplicación en una sesión de terminal diferente,

`` sh
$ python run_app.py
`` `

La aplicación debe estar en funcionamiento en [http: // localhost: 5000] (http: // localhost: 5000).

Aquí hay algunas capturas de pantalla

1. Publicar algún contenido

! [image.png] (https://github.com/avilaroman/python_blockchain_app/raw/master/screenshots/1.png)

2. Solicitar el nodo para minar

! [image.png] (https://github.com/avilaroman/python_blockchain_app/raw/master/screenshots/2.png)

3. Resincronizando con la cadena para datos actualizados

! [image.png] (https://github.com/avilaroman/python_blockchain_app/raw/master/screenshots/3.png)

Para jugar girando varios nodos personalizados, use el punto final `register_with /` para registrar un nuevo nodo.

Aquí hay un escenario de muestra que quizás quieras probar,

`` sh
# ya corriendo
$ frasco ejecutar --port 8000 y
# activando nuevos nodos
$ frasco ejecutar --port 8001 y
$ matraz --port 8002 y
`` `

Puede utilizar las siguientes solicitudes de cURL para registrar los nodos en el puerto `8001` y` 8002` con el `8000` ya en ejecución.

`` sh
curl -X POST \
  http://127.0.0.1:8001/register_with \
  -H 'Tipo de contenido: aplicación / json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'
`` `

`` sh
curl -X POST \
  http://127.0.0.1:8002/register_with \
  -H 'Tipo de contenido: aplicación / json' \
  -d '{"node_address": "http://127.0.0.1:8000"}'
`` `

Esto hará que el nodo en el puerto 8000 conozca los nodos en el puerto 8001 y 8002, y hará que los nodos más nuevos sincronicen la cadena con el nodo 8000, de modo que puedan participar activamente en el proceso de minería posterior al registro.

Para actualizar el nodo con el que se sincroniza la aplicación frontend (el valor predeterminado es el puerto localhost 8000), cambie el campo `CONNECTED_NODE_ADDRESS` en el archivo [views.py] (/ app / views.py).

Una vez que haga todo esto, puede ejecutar la aplicación, crear transacciones (publicar mensajes a través de la interfaz web), y una vez que extraiga las transacciones, todos los nodos de la red actualizarán la cadena. La cadena de los nodos también se puede inspeccionar invocando el punto final `/ chain` usando cURL.

`` sh
$ curl -X GET http: // localhost: 8001 / chain
$ curl -X GET http: // localhost: 8002 / chain
`` `
