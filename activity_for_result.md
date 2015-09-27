#Iniciar un Activity y esperar un Resultado

En esta sección se estudia como iniciar un [**Activity**](http://developer.android.com/reference/android/app/Activity.html) y manejar el resultrado que este retorne.

Para iniciar un [**Activity**](http://developer.android.com/reference/android/app/Activity.html) y manejar el resultado debe hacerse lo siguiente:

1. Invocar la instrucción `startActivityForResult()`
2. implementar el método `onActivityResult()` en el **Activity** que invoca la instrucción `startActivityForResult()`.

En el proyecto [HolaAndroid]() crear un nuevo layout