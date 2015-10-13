# Creación de Vistas Personalizadas en Android

##Objetivo:
Crear una vista personalizada a partir de la clase [**View**](http://developer.android.com/reference/android/view/View.html) de **Adroid**

## Procedimiento

Uno de los métodos utilizados para crear una vista personalizada en [**Android**](http://developer.android.com/guide/index.html) es extendiendo de la clase [**View**](http://developer.android.com/reference/android/view/View.html), los pasos necesarios se enumeran a continuación:

1. Crear una clase que herede de la clase [**View**](http://developer.android.com/reference/android/view/View.html).
2. Implementar en la clase un constructor que reciba como argumentos el [**context**](http://developer.android.com/reference/android/content/Context.html) y los atributos del **xml** ([**AttributeSet**](http://developer.android.com/reference/android/util/AttributeSet.html)).
3. Implementar el método [`onMeasure()`](http://developer.android.com/reference/android/view/View.html#onMeasure(int, int)), a través de este método la vista ajustará sus dimensiones y la de sus hijos a las requeridas por el padre.
4. Instanciar un objeto [**Paint**](http://developer.android.com/reference/android/graphics/Paint.html) global en la clase.
4. Implementar el método [`onDraw()`](http://developer.android.com/reference/android/view/View.html#onDraw(android.graphics.Canvas)) y escribir en este las instrucciones para dibujar en pantalla.
5. Añadir la vista a un layout para implementarla en la interfaz gráfica.

## Desarrollo

El sistema de referencia del dispositivo **Android** se presenta en la siguiente figura ![](/capturas/referencias.png).

El origen del sistema de coordenadas se encuentra en la parte superior izquierd de la pantalla, el eje x positivo a la derecha y el eje Y positivo hacia abajo.

Las dimensiones de la vista se ajustan en el método `onMeasure` utilizando la instrucción `setMeasuredDimension()`

```java
    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        setMeasuredDimension(MeasureSpec.getSize(widthMeasureSpec),MeasureSpec.getSize(heightMeasureSpec));
    }
```
 con este método se asegura que la vista se adapta al elemnto contenedor.

Si se quiere por ejemplo dibujar un circulo en el centro de la pantalla se hace a través del método `onDraw`, este método recibe como parámetro un objeto `Canvas` que en español se traduce como "lienzo", sobre ese lienzo se dibuja con un objeto  [**Paint**](http://developer.android.com/reference/android/graphics/Paint.html) (pintura), para esto es necesario determinar las coordenadas del centro de la pantalla.

![](/capturas/referencias_dimensiones.png)

Con las coordenadas del centro de la pantalla se ejecuta la instrucción `canvas.drawCircle`, que recibe como parámetros las coordenadas del centro del circulo, el radio y el objeto [**Paint**](http://developer.android.com/reference/android/graphics/Paint.html) 

```java
    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
		//Estilo trazo
        p.setStyle(Paint.Style.STROKE);
        //Ancho del trazo
        p.setStrokeWidth(3);
        //Color del trazo
        p.setColor(Color.BLUE);
        canvas.drawCircle(getWidth() / 2, getHeight() / 2, getWidth() / 4, p);
    }
```

### Estilos del Paint
 1. **Style.STROKE**: Estilo trazo, solo dibuja el perímetro de las figuras.
 2. **Style.FILL**: Estilo relleno, dibuja el relleno de la figura
 3. **Style.FILL_AND_STROKE**: Dibuja el perímetro y el relleno de la figura.

Para dibujar un texto alrededor del circulo se utiliza la instrucción ` canvas.drawTextOnPath`, el objeto [**`Path`**]() define una trayectoria en el área de dibujo.

* Offset horizontal: $$(3/2)*%pi*R-anchoMensaje/2$$, donde `anchoMensaje` es el ancho total del mensaje.
* Offset vertical: -40

El código completo de la clase queda:

```java
package com.prueba.holaAndroid;

import android.content.Context;
import android.graphics.Canvas;
import android.graphics.Color;
import android.graphics.Paint;
import android.graphics.Path;
import android.util.AttributeSet;
import android.view.View;

public class VistaPersonal extends View {

    private Paint p=new Paint();
    public VistaPersonal(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
        setMeasuredDimension(MeasureSpec.getSize(widthMeasureSpec),MeasureSpec.getSize(heightMeasureSpec));
    }

    @Override
    protected void onDraw(Canvas canvas) {
        super.onDraw(canvas);
        //mensaje a ser presentado en pantalla
        String mensaje="¡Hola Android!";
        //Tamaño del texto
        p.setTextSize(40);
        //buffer para almacenar las dimensiones del texto
        float[] bf=new float[32];
        int nl=p.getTextWidths(mensaje, bf);
        float anchoMensaje=0;
        for(int i=0;i<nl;i++){
            anchoMensaje+=bf[i];
        }
        //Estilo  trazo
        p.setStyle(Paint.Style.STROKE);
        //Ancho del trazo
        p.setStrokeWidth(3);
        //Color del trazo
        p.setColor(Color.BLUE);
        canvas.drawCircle(getWidth() / 2, getHeight() / 2, getWidth() / 4, p);
        Path path=new Path();
        p.setColor(Color.RED);
        canvas.drawPath(path,p);
        path.addCircle(getWidth() / 2, getHeight() / 2, getWidth() / 4, Path.Direction.CW);
        p.setStyle(Paint.Style.FILL);
        canvas.drawTextOnPath(mensaje, path, (float) ((3.0 / 2) * Math.PI * getWidth() / 4 - anchoMensaje / 2.0), -40, p);
    }
}
```

Por último se añade la vista personalizada a un layout:

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent" android:layout_height="match_parent">

    <view
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        class="com.prueba.holaAndroid.VistaPersonal"
        android:id="@+id/view"
        android:layout_gravity="center" />
</FrameLayout>
```

Crear un [**Activity**]() de nombre **PersonalActivity** y cargar como vista el layout anterior

```java
package com.prueba.holaAndroid;

import android.app.Activity;
import android.os.Bundle;


public class PersonalActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.layout_vista_personal);
    }
}
```
Añadir al **layout_main** un botón con el texto **"Iniciar Vista Personal"** e iniciar con el **PersonalActivity.class** desde **MainActivity**

```java
    public void iniciarVistaPersonal(View v){
        startActivity(new Intent(this,PersonalActivity.class));
    }
```

![](/capturas/personal1.png) ![](/capturas/personal2.png) ![](/capturas/personal3.png)
