#Enviar datos entre Activities a través de Intents

En esta sección se estudia como enviar un dato entre Activities utilizando el [Intent]() de inicio del [Activity]().

##Objetivos
1. Obtener el dato desplegado en un [EditText]() y enviarlo a otro [Activity]().
2. Recuperar el dato recibido y deplegarlo en pantalla.

##Desarrollo

En el proyecto [HolaAndroid]() modificar **layout_main.xml** agregando un **TextField** del tipo [EditText](), cambiar el identificador del [EditText]() a `et_mensaje`.

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

</LinearLayout>

```
![](/capturas/layout_main_et.png)

En la clase **MainActivity** instanciar el [EditText]() utilizando la instrucción `findViewById(R.id.et_mensaje)` en el método `onCreate()` después de `setContentView()` 

```java
public class MainActivity extends Activity{

    EditText etMensaje;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_main);
        etMensaje=(EditText)findViewById(R.id.et_mensaje);
    }
           ...

``` 

Modificar el método `iniciarSaludo(View v)` para cargar en el [Intent]() el dato presente en el [EditText]().

```java

    public void iniciarSaludo(View v){
        Intent intent=new Intent(this,SaludoActivity.class);
        intent.putExtra("mensaje",etMensaje.getText());
        startActivity(intent);
    }

```

La instrucción `putExtra(String clave, valor)`, carga un dato al intent, ese dato es identificado por el argumento **"clave"** y el valor puede ser cualquier tipo primitivo de datos, arrays, **Serializable**, **Bundle** entre otros.

Modificar la clase **SaludoActivity** para **recuperar el dato** enviado desde **MainActivity** y presentarlo en pantalla: instanciar el elemento [TextView]() de **layout_saludo.xml**

```java

public class SaludoActivity extends Activity {
    private TextView tvSaludo;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_saludo);
        tvSaludo= (TextView) findViewById(R.id.textView2);
    }
}

```

Requperar el intent que inicia a **SaludoActivity** y su contenido para presentarlo en pantalla al final del **TextView**

```java
package com.prueba.holaAndroid;
import android.app.Activity;
import android.os.Bundle;
import android.widget.TextView;

public class SaludoActivity extends Activity {
    private TextView tvSaludo;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_saludo);
        tvSaludo= (TextView) findViewById(R.id.textView2);
        tvSaludo.append("\n"+ getIntent().getStringExtra("mensaje"));
    }
}

```

La instrucción `tvSaludo.append()` añade la cadena de texto recuperada en una nueva línea.

![](/capturas/ha_intent_inicio.png) ![](/capturas/ha_intent_ingre_mensaje.png) ![](/capturas/ha_intent_click.png) ![](/capturas/ha_intent_mensaje.png)
