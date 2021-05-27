# Watson-Assistant-K8s-Deploy :rocket:
En esta aplicación de muestra, se visualiza la interacción con un asistente virtual bancario. El asistente simula algunos escenarios, como realizar un pago con tarjeta de crédito, reservar una cita con un asesor y elegir una tarjeta de crédito. Watson puede comprender sus entradas y responder en consecuencia.
Finalmente se explica como se puede realizar el despliegue de la aplicación en Kubernetes.

## Indice  :book:
1. [Pre-Requisitos](#Pre-Requisitos)
2. [Paso 1. Configurar la aplicación](#Paso-1)
3. [Paso 2. Ejecución local](#Paso-2)
4. [Paso 3. Cambio de credenciales según el servicio creado](#Paso-3)
5. [Paso 4. Ejecución local y prueba](#Paso-4)
6. [Paso 5. Despliegue de aplicación Backend](#Paso-5)
7. [Paso 6. Despliegue de aplicación Frontend](#Paso-6)

## Prerrequisitos

1. Regístrese para obtener una cuenta de IBM Cloud.
2. Descargue la CLI de IBM Cloud.
3. Cree una instancia del servicio Watson Assistant y obtenga sus credenciales:
+ Vaya a la página Watson Assistant en IBM Cloud Catalog.
+ Inicie sesión en su cuenta de IBM Cloud.
+ Haga clic en Crear.
+ Haga clic en Mostrar para ver las credenciales del servicio.
+ Copie el valor de **apikey**. 
+ Copie el valor de la **URL**.
4. Clonar el repositorio en su máquina.

## Paso 1
## Configurar la aplicación
1. En su consola de IBM Cloud, abra la instancia de servicio Watson Assistant.
2. En la pestaña **Skills** de click en el botón **Create skill**.
3. Seleccione la opción **Dialog skill** y luego siguiente.
4. De click en la pestaña **Upload skill**, seleccione el archivo **banking_workspace.json** que se encuentra en la carpeta training y luego de click en **Import**.
5. En la pestaña **Assistants** de click en el botón **Create assistant**.
6. Asigne un nombre al asistente y de click en **Create assistant**.
7. En la ventana del asistente, de click en **Add dialog skill** y seleccione el skill creado con aterioridad.
<p align="center"><img width="600" src="https://github.com/emeloibmco/Watson-Assistant-K8s-Deploy/blob/main/bank/bank1.gif"></p>

8. En el cmd de windows copie el archivo .env.example y cree uno llamado .env con el siguiente comando
```
copy .env.example .env
```
9. Abra el archivo .env y agregue las credenciales del servicio copiadas en los prerequisitos que obtuvo en el paso anterior y el ID del asistente que puede encontar en las configuraciones del asistente.
```
ASSISTANT_ID=
ASSISTANT_IAM_APIKEY=
ASSISTANT_URL=
```
## Paso 2
## Ejecución local
1. Instale las dependencias npm
```
npm install
```
2. Ejecute la aplicación
```
npm start
```
3. Visualice y pruebe la aplicación dirigiendose a desde su navegador a la dirección ```http://localhost:3000/```

## Paso 3
## Despliegue de la aplicación en Kubernetes
1. En la ventana de comandos, donde estaba corriendo la aplicación, debe para el proceso con **Ctrl+C**.
2. Ejecutar el comando ```docker build -t <nombre-imagen:tag> . ```. Establezca cualquier nombre a la imagen y como tag **v1**, posteriormente en docker se debe verificar que aparezca la imagen creada.
3. En Docker, de click en **Run** a la imagen creada, luego **Optional Settings** y digitar 8080 en localhost. Para verificar el funcionamiento nos dirigimos al navegador y colocamos ```http://localhost:8080```, como resultado se puede observar la aplicación nuevamente.
4. Ingrese a su cuenta de IBM por medio del PowerShell ejecutando el comando
```
ibmcloud login --sso
```
>**NOTA**: Se debe tener creado en la cuenta el cluster donde se va a desplegar la app.
7. Ejecutar el comando donde se selecciona el grupo de recursos donde esta el cluster 
```
ibmcloud target -g <nombre-recurso>
```
9. Ingresar al container registry ejecutando el comando 
```
ibmcloud cr login
```
10. Añadir un espacio con el comando 
```
ibmcloud cr namespace-add <nombre-espacio>
```
11. Ejecutar el comando que añade la imagen docker en el espacio creado
```
docker tag <nombre-imagen:tag> us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
```
12. Ejecutar el comando
 ```
 docker push us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
 ```
13. Ingresar al cluster donde se va a desplegar la aplicación  
```
ibmcloud ks cluster config --cluster <nombre-cluster>
```
14. Crear el despliegue con el comando 
```
kubectl create deployment <nombre-despliegue> --image=us.icr.io/<nombre-espacio>/<nombre-imagen:tag>
```
15. Exponer el despliegue
```
kubectl expose deployment/<nombre-despliegue> --type=LoadBalancer --name=<nombre-app>  --port=<puerto-especificado-en-dockerfile> --target-port=<puerto-especificado-en-dockerfile>
```
16. Ingresar desde IBM Cloud al panel de kubernetes y buscar el despliegue, verificar que no existan errores.
17. Ir a la pestaña SERVICES y dar click en la URL mostrada en la columna External Points
>**NOTA**: Debe esperar unos minutos mientras se realiza el despliegue, refresque la página y verifique que no salgan errores de carga
<p align="center"><img width="800" src="https://github.com/emeloibmco/Watson-NLU-NodeJS-Application/blob/main/Imagenes/Picture2.jpg"></p>
