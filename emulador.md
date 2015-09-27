#Configuración de un Emulador para la prueba de las Aplicaciones.

Si no se dispones de [un dispositivo físico debuggable]() es posible ejecutar la aplicación en un emulador, en esta sección se describen los pasos necesarios para conficurar un emulador.

1. En primer lugar se debe ejecutar el **SDK Manager**, esto se puede hacer desde **Android Studio** haciendo click sobre el ícono 
![icono](/capturas/ini_sdk.png). Otra manera es através de la barra de menú **Tools>Android>SDK Manager**
![](/capturas/ini_sdk_menu.png). Se instala la plataforma para la cual se quiere configurar el emulador ![plataformas](/capturas/ini_sdk_instal_platform.png).
2. Iniciar **AVD Manager** ![avd](/capturas/ini_avd.png) al iniciar se presenta una lita de emuladores (si se ha creado alguno con anterioridad) ![lista](/capturas/avd_list.png). Hacer click sobre la opción **+ Create Virtual Device**.
3. Se inicia el diálogo **Select Hardware** que contiene una lista de definiciones de dispositivos según su categoría (teléfono, tableta, reloj o TV).![](/capturas/select_hardware.png) Los detalles que se presentan en pantalla son:
 * **Size:** tamaño de pantalla en pulgadas de la diagonal.
 * **Resolution:** resolución de la pantalla en pixeles.
 * **Density:** La categoría de densidad del dispositivo.

La **densidad de pantalla** es la cantidad de pixeles por unidad de medida, generalmente expresada en puntos por pulgada **(dpi)**, en android se han definido seis grupos generales de densidad:

Identificador | Descripción | Densidad aproximada (dpi)
--- | --- | ---
 **ldpi** | (baja) | 120 
 **mdpi** | (media) | 160 
 **hdpi** | (alta) | 240 
 **xhdpi** | (extra alta) | 320 
 **xxhdpi** | (extra-extra alta) | 480 
 **xxxxhdpi** | (extra-extra-extra alta) | 640 