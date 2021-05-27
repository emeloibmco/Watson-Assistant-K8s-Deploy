# Watson-Assistant-K8s-Deploy :rocket:
En esta aplicación de muestra, se visualiza la interacción con un asistente virtual bancario. El asistente simula algunos escenarios, como realizar un pago con tarjeta de crédito, reservar una cita con un asesor y elegir una tarjeta de crédito. Watson puede comprender sus entradas y responder en consecuencia.
Finalmente se explica como se puede realizar el despliegue de la aplicación en Kubernetes.

## Indice  :book:
1. [Pre-Requisitos](#Pre-Requisitos)
2. [Paso 1. Configurar la aplicación](#Paso-1)
3. [Paso 2. Despliegue del modelo Machine Learning](#Paso-2)
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
4. Descargar en su máquina el archivo **banking_workspace.json**, lo puede hacer clonando este repositorio.

## Paso 1
## Configurar la aplicación
1. En su consola de IBM Cloud, abra la instancia de servicio Watson Assistant.
2. En la pestaña **Skills** de click en el botón **Create skill**.
3. Seleccione la opción **Dialog skill** y luego siguiente.
4. De click en la pestaña **Upload skill**, seleccione el archivo **banking_workspace.json** y luego de click en **Import**.
5. En la pestaña **Assistants** de click en el botón **Create assistant**.
6. Asigne un nombre al asistente y de click en **Create assistant**.
7. En la ventana del asistente, de click en **Add dialog skill** y seleccione el skill creado con aterioridad.
<p align="center"><img width="600" src="https://github.com/emeloibmco/IBM-Cloud-Monitoring-Windows-Agent-VM/blob/main/windowssysdig/Paso1.gif"></p>
