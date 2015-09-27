#Asignación de eventos a un Botón

En esta sección se explica como asignar una acción sencilla a un botón de la interfaz gráfica. En el proyecto [HolaAndroid]() abrir el archivo **layout_main.xml**, cambiar las propiedades del layout a **orientación vertical.**
![](/capturas/layout_diseno.png) 

De la paleta **(Palette)** en la parte izquierda de la pantalla arrastrar un elemento del tipo **Button** en el nodo **Widgets** hacia el layout.
![](/capturas/con_boton_mensaje.png)
Cambiar las siguientes propiedades en la vista de diseño:

* **text:** Mensaje
* **onClick:** saludar

La propiedad **onClick** representa el nombre del método que se ejecuta una vez que se hace click sobre el botón.

Ir a la clase **MainActivity** y agregar un método público con nombre **saludar**

```java
    public void saludar(View v){
    }
```

El argumento **View** del método le dice al sistema que está asociado a la acción de una vista de la interfaz de usuario.

El objetivo es que cuando se presione un botón se presente un mensaje en pantalla, para este fin se utiliza un [**Toast**](http://developer.android.com/reference/android/widget/Toast.html).
Un [**Toast**](http://developer.android.com/reference/android/widget/Toast.html) es un diálogo simple que informa al usuario sobre la realización de acciones en la aplicación.

```java
    public void saludar(View v){
        Toast toast=Toast.makeText(this, R.string.string_saludo, Toast.LENGTH_LONG);
        toast.show();
    }
 }
``` 

Para la implementación del [**Toast**](http://developer.android.com/reference/android/widget/Toast.html) se realiza a través de un método estático, y se pasan como argumentos:

* [**context**](http://developer.android.com/reference/android/content/Context.html), observe que se utiliza la palabra **this** para el **Context**, esto es porque en la cadena de herencia el [**Activity**](http://developer.android.com/reference/android/app/Activity.html) desciende de la clase [**Context**](http://developer.android.com/reference/android/content/Context.html).
* Texto del mensaje, en este caso es el número entero que identifica al recurso de tipo **string** que se crea en la sección [**Internacionalización**](inter.md).
* La duración, hay solo dos posibles, larga y corta. 

Al ejecutar la aplicación y hacer click sobre el botón **Mensaje** se debe presentar el mensaje en la parte inferior de la pantalla.

![](/capturas/emulador_toast.png)

Se puede modificar el atributo **gravity** al [**Toast**](http://developer.android.com/reference/android/widget/Toast.html) para presentarlo en el centro de la pantalla `toast.setGravity(Gravity.CENTER,0,0);` 
![](/capturas/emulador_toast_centro.png)

Si un simple texto no es suficiente para hacer llegar el mensaje entonces se puede [**personalizar el Toast**]().

 