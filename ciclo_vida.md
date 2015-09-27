#Ciclo de Vida del Activity

El **Activity** posee un ciclo de vida que determina el orden de ejecución de sus métodos. Conocer el ciclo de vida del **Activity** es importante para controlar el comportamiento esperado de la aplicación, por ejemplo, es necesario conocer lo que ocurre si otro el **Activity** que se despliega en pantalla en un momento determinado pasa a segundo plano y en su lugar se despliega otro **Activity**.

Para observar el ciclo de vida del Activity se sugieren lo siguientes pasos (se continua trabajando con el proyecto [HolaAndroid]()):

1. Con el cursor posicionado dentro de la clase Activity (fuera de cualquier método) en la barra de menú hacer click en **code>override Implement...**![](/capturas/click_override.png)
2. En el diálogo **Select Methods**
![](/capturas/select_metodos.png)
seleccionar:
 * `onStart()`
 * `onPause()`
 * `onResume()`
 * `onRestart()`
 * `onStop()`
 * `onDestroy()`
 