#Iniciar un Activity y esperar un Resultado

En esta sección se estudia como iniciar un [**Activity**](http://developer.android.com/reference/android/app/Activity.html) y manejar el resultrado que este retorne.

Para iniciar un [**Activity**](http://developer.android.com/reference/android/app/Activity.html) y manejar el resultado debe hacerse lo siguiente:

1. Invocar la instrucción `startActivityForResult()`
2. Implementar el método `onActivityResult()` en el **Activity** que invoca la instrucción `startActivityForResult()`.
3. El [**Activity**](http://developer.android.com/reference/android/app/Activity.html) invocado realiza las operaciones para las que es programado, debe invocar la instrucción `setResult(int resultCode, Intent data)`, en esrta instrucción se asigna el código de resultado,( `RESULT_CANCELED` y `RESULT_OK` son dos enteros estáticos de la clase [**Activity**](http://developer.android.com/reference/android/app/Activity.html)), y los datos del resultado obtenido son enviados a través del argumento `Intent data`.

![](/capturas/safr.png)

#Desarrollo

En el proyecto [**HolaAndroid**]() crear un nuevo layout de nombre **layout_resultado.xml**. Utilizar como elemento padre un [**LinearLayout**]() con orientación vertical, añadir un [**EditText**]() y un [**Button**]() con las siguientes propiedades:

* **id**=btn_resultado
* **** 

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent"
    android:orientation="vertical">

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/et_resultado"
        android:hint="Ingresar mensaje aquí"/>

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Aceptar"
        android:id="@+id/btn_resultado"
		android:onClick="generarResultado" />
</LinearLayout>

```
![](/capturas/layout_resultado.png)

Realizar las siguientes tareas:

1. Crear una nueva clase en el paquete `com.prueba.holaAndroid` con el nombre **ResultadoActivity** y extenderla de [**Activity**]().
2.  Implementar el método `onCreate()` y asignar como vista **layout_resultado** y crear una instancia del elemento [**EditText**]() del layout.
3.  Obtener el [**Intent**]() que inicia el [**Activity**]() y recuperar un **String** con la **clave** **"mensaje"**
4.  Cargar el **String** al [**EditText**]() y presentarlo en pantalla.
5.  Cambiar el resultado por defecto a **"Cancelado"** con la instrucción `setResult(RESULT_CANCELED)`
6.  Implementar el método `generarResultado(View)` asociado al botón de la interfaz gráfica, recuperar el dato del [**EditText**]() y enviarlo como resultado satisfactorio.

***

**NOTA:** Debe recordarse que al crear un nuevo componente de aplicación como un [**Activity**](), este debe ser declarado en el manifiesto dentro del nodo **application**

` <activity android:name=".ResultadoActivity"/>`

***

```java

package com.prueba.holaAndroid;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;

public class ResultadoActivity extends Activity {

    private EditText etResultado;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //
        setContentView(R.layout.layout_resultado);
        etResultado= (EditText) findViewById(R.id.et_resultado);
        //recupera el dato String con clave "mensaje" y lo presenta en el EditText
        etResultado.setText(getIntent().getStringExtra("mensaje"));
        //Cambia el resultado por defecto a "Cancelado"
        setResult(RESULT_CANCELED);
    }

    //Genera el resultado satisfactorio al hacer click sobre el botón
    public void generarResultado(View v){
        //Genera un Intent vacío
        Intent intent=new Intent();
        //Guarda el dato del resultado en el Intent con un identificador
        intent.putExtra("resultado",etResultado.getText().toString());
        //cambiar el código de resultado a satisfactorio
        setResult(RESULT_OK,intent);
    }
}


```

Modificar **layout_main.xml** y agregar un [**TextView**]() bajo el elemento [**EditText**]() con las siguientes propiedades:

* text size= 50 sp
* visibility = gone

Con esta última propiedad el [**TextView**]() se mantiene invisible y no ocupa ningún espacio en la pantalla.

Agregar un botón ([Button]()) con las siguientes propiedades:

* **id**=`btn_iniciar_resultado` 
* **text**= Iniciar por Resultado
* **onClick**=iniciarPorResultado

```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="wrap_content"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hola Android"
        android:id="@+id/textView"
        android:textStyle="bold"
        android:textSize="40sp" />

    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/et_mensaje"
        android:layout_gravity="center_horizontal"
        android:hint="Ingresar Mensaje aquí"/>

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="New Text"
        android:textSize="20sp"
        android:visibility="gone"
        android:id="@+id/tv_resultado" />

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Iniciar Activity"
        android:id="@+id/button2"
        android:layout_gravity="center_horizontal"
        android:onClick="iniciarSaludo" />

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Mensaje"
        android:id="@+id/button"
        android:layout_gravity="center_horizontal"
        android:onClick="saludar" />

    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Iniciar por Resultado"
        android:id="@+id/btn_iniciar_resultado"
        android:layout_gravity="center_horizontal"
        android:onClick="iniciarPorResultado"/>

</LinearLayout>

```

![](/capturas/layout_main_por_resultado.png)

Realizar las siguientes modificaciones sobre la clase **MainActivity**

1. Agregando el método `iniciarPorResultado(View v)`.
2. En el método `iniciarPorResultado()` crear un [**Intent**]() que apunte a **ResultadoActivity** `Intent intent=new Inten(this,ResultadoActivity.class)`.
3. Cargar el contenido del [**EditText**]() como dato en el [**Intent**](). `intent.putExtra("mensaje",etMensaje.getText().toString());`
4. Crear enla clase una constante estática entera con el identificador `INICIAR_POR_RESULTADO`. Este identificador sirve para determinar el componente desde el cual se genera el resultado. `public static final int INICIAR_POR_RESULTADO=0;`
5. Invocar la instrucción `startActivityForResult(Intent, int requestCode)` con el código de solicitud (`requestCode`) creado en el paso anterior.
6. Implementar en la clase el método `onActivityResult` para manejar el resultado obtenido.

```java
package com.prueba.holaAndroid;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.Gravity;
import android.view.View;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends Activity{

    private EditText etMensaje;
    private TextView tvResultado;
    //Identificador para el código de solicitud
    public static final int INICIAR_POR_RESULTADO=0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_main);
        etMensaje=(EditText)findViewById(R.id.et_mensaje);
        tvResultado= (TextView) findViewById(R.id.tv_resultado);
    }

    public void saludar(View v){
        Toast toast=Toast.makeText(this, R.string.string_saludo, Toast.LENGTH_LONG);
        toast.setGravity(Gravity.CENTER, 0, 0);
        toast.show();
    }

    public void iniciarSaludo(View v){
        Intent intent=new Intent(this,SaludoActivity.class);
        intent.putExtra("mensaje",etMensaje.getText().toString());
        startActivity(intent);
    }

    public void iniciarPorResultado(View v){
        //Crea un Intent para iniciar ResultadoActivity
        Intent intent =new Intent(this,ResultadoActivity.class);
        //Carga el contenido del EditText en el Intent
        intent.putExtra("mensaje",etMensaje.getText().toString());
        //Inicia un activity por resultado con un código de solicitud
        //el código de solicitud (requestCode) sirve para identificar desde qué Activity se ha
        //generado el resultado recibido en el método onActivityResult
        startActivityForResult(intent,INICIAR_POR_RESULTADO);
    }

    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(resultCode==RESULT_CANCELED){
            Toast.makeText(this,"Cancelado",Toast.LENGTH_LONG).show();
            return;
        }
        if(requestCode==INICIAR_POR_RESULTADO){
            //recupera el dato del resultado y lo carga en el TextView
            tvResultado.setText(data.getStringExtra("resultado"));
            //Hace el TextView visible
            tvResultado.setVisibility(View.VISIBLE);
        }
    }
}

```
![](/capturas/codigo_safr_cap.png)

##Capturas de pantalla

![](/capturas/por_resultado_inicio.png) ![](/capturas/por_resultado_start.png) ![](/capturas/por_resultado_cancelando.png) ![](/capturas/por_resultado_cancelado.png) ![](/capturas/por_resultado_aceptando.png) ![](/capturas/por_resultado_ok.png)