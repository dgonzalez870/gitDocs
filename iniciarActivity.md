#Iniciar un Activity

En esta sección se explica como iniciar un nuevo [**Activity**](http://developer.android.com/reference/android/app/Activity.html) una vez que la aplicación está en ejecución.

El método para iniciar un [**Activity**](http://developer.android.com/reference/android/app/Activity.html) es utilizando la instrucción `startActivity(Intent)`, el argumento [**Intent**](http://developer.android.com/reference/android/content/Intent.html) representa la descripción de la operación a ser ejecutada, en este caso ejecutar el  [**Activity**](http://developer.android.com/reference/android/app/Activity.html) cuyo nombre se pasa como argumento.

En el proyecto [HolaAndroid]() crear un nuevo layout.
![](/capturas/crear_layout.png).

Colocar en nombre **layout_saludo** y en **Root Tag** **RelativeLayout**, envista de diseño arrastrar un elemento **TextView** al centro del Layout, modificar las siguientes propiedades en el **TextView:**

* **text:** @string/string_saludo
* **textSize:** 40 sp.

El resultado se presenta en la siguiente figura

![](/capturas/layout_saludo.png)

Crear una nueva clase **SaludoActivity** 
![](/capturas/nueva_clase.png)

Extender la clase **saludoActivity** de la clase [**Activity**](http://developer.android.com/reference/android/app/Activity.html), implementar el método `onCreate(Bundle)` y asignar como vista **layout_saludo.**

```java
package com.prueba.holaAndroid;
import android.app.Activity;
import android.os.Bundle;

public class SaludoActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_saludo);
    }
}
```

Modificar el layout **layout_main** agregando un segundo botón y modificando las siguientes propiedades al botón:

* **layout__width:** match_parent
* **text:** Iniciar Activity
* **onClick:** iniciarSaludo

![](/capturas/layout_iniciar_activity.png)


En **MainActivity** agregar el método público `public void iniciarSaludo(View v)` y en ese método ejecutar la instrucción de inicio del [**Activity**](http://developer.android.com/reference/android/app/Activity.html).


```java
package com.prueba.holaAndroid;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.Gravity;
import android.view.View;
import android.widget.Toast;

public class MainActivity extends Activity{
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_main);
    }

    public void saludar(View v){
        Toast toast=Toast.makeText(this, R.string.string_saludo, Toast.LENGTH_LONG);
        toast.setGravity(Gravity.CENTER, 0, 0);
        toast.show();
    }

	//Al hacer click sobre el botón se inicia SaludoActivity	
    public void iniciarSaludo(View v){
        Intent intent=new Intent(this,SaludoActivity.class);
        startActivity(intent);
    }
 }
```

Agregar el [**Activity**](http://developer.android.com/reference/android/app/Activity.html) **SaludoActivity** al manifiesto y ejecutar la aplicación.

![](/capturas/edit_manifiesto.png)