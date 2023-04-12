# React Native

## Primeros pasos
Pasos para la preparación de una App creada con React Native CLI.

Antes de todo, se debe tener ya configurado el emulador o dispositivo móvil. 
Si es su primera vez corriendo la aplicación en su dispositivo móvil debe asegurarse de que tiene habilitada la Opción de desarrollador para permitir la Depuración de USB. 

También debe tener permitido desde Android Studio el permiso para tener acceso al modo de depuración en su dispositivo móvil.
Se puede hacer creando una aplicación en una actividad vacía y teniendo su dispositivo móvil conectado, luego abrir la aplicación en su dispositivo.

![](https://i.stack.imgur.com/4g9Bd.png)

### Crear un proyecto

- `npx react-native@latest init AwesomeProject`

Referencia [https://reactnative.dev/docs/environment-setup](https://reactnative.dev/docs/environment-setup)

### Generar icon

Generador https://romannurik.github.io/AndroidAssetStudio/icons-launcher.html
-
Descargamos y descomprimimos el archivo. 
Copiamos el contenido de res a `/android/app/src/main/res/`

### Configurar Splash Screen

- Instalar `npm i react-native-splash-screen`

##### Opcional
- Instalar `npm install @react-navigation/native-stack`

Nuesto Archivo App se vería más o menos así.

```javascript
import React, { useEffect } from 'react';
import { NavigationContainer, DefaultTheme } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import SplashScreen from "react-native-splash-screen";
import HomeScreen from './screens/Home';

const Stack = createNativeStackNavigator();

function App() {
    const theme = {
        ...DefaultTheme,
        colors: {
            ...DefaultTheme.colors,
            border: "transparent",
        }
    }
    useEffect(() => {
        SplashScreen.hide()
    }, []);
    return (
        <NavigationContainer>
            <Stack.Navigator>
                <Stack.Screen name="Home" component={HomeScreen} options={{ headerShown: false }} />
            </Stack.Navigator>
        </NavigationContainer>
    );
}

export default App;
```

Si es nuevo debe leer [https://reactnavigation.org/docs/getting-started](https://reactnavigation.org/docs/getting-started)


------------



##### Imagen para el Splash

Hay varias plataformas o programas que facilitan la creación de Imagen Splash.
En mi caso usaré [https://www.photopea.com/](https://www.photopea.com/)

Si en photopea hacemos clic en `Proyecto Nuevo` veremos que en la sesión de marcos hay una opción llamada `Movil`. Podemos elegir la plantilla IPhone 5 para probar o modificarla. Recordar descargarla en formato .PNG con el nombre splash.

La imagen debemos guardarla en el directorio: `/android/app/src/main/res/drawable`.


------------


##### MainActivity

Abriremos `/android/app/src/main/java/com/[nombre_app]MainActivity.java`

Agregaremos lo siguiente.
```javascript
import android.os.Bundle;
import org.devio.rn.splashscreen.SplashScreen;
```

```javascript
@Override
protected void onCreate(Bundle savedInstanceState) {
    SplashScreen.show(this); 
    super.onCreate(savedInstanceState);
}
```


------------


##### launch_screen.xml
En `/android/app/src/main/res/` crearemos una carpeta llamada `layout` y dentro de esta un archivo llamado `launch_screen.xml`

Agregaremos lo siguiente.

```xml
<?xml version="1.0" encoding="utf-8"?>
	<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    android:orientation="vertical" android:layout_width="match_parent"
	    android:layout_height="match_parent">
	    <ImageView android:layout_width="match_parent" android:layout_height="match_parent" android:src="@drawable/splash" android:scaleType="fitXY" />
	</RelativeLayout>
```


------------

##### colors.xml

Luego vamos a la carpeta values. Si no existe la creamos y dentro un archivo llamado `colors.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
	<resources>
	    <color name="colorBackground">#FFFFFF</color>
	</resources>
```

------------


##### Implementar Icons Vectors

`npm install react-native-vector-icons --save`

Referencias: 
[https://github.com/oblador/react-native-vector-icons](https://github.com/oblador/react-native-vector-icons)
-
[https://aboutreact.com/react-native-vector-icons/](https://aboutreact.com/react-native-vector-icons/)
-
[https://oblador.github.io/react-native-vector-icons/](https://oblador.github.io/react-native-vector-icons/)


``` 
import Icon from 'react-native-vector-icons/MaterialIcons'
```
```
<Icon name='home' size={30} color='#900' />
```

------------


##### Implementar Imagenes Gif

Agregar en `dependencies` de `/android/app/build.gradle`

```
implementation 'com.facebook.fresco:fresco:2.0.0'
implementation 'com.facebook.fresco:animated-gif:2.6.0'
```

------------

##### Run

Intente correr la aplicación.

Comando `npm run start`

En caso de algún error que no se deba a alguna dependencia, intente correr la aplicación nuevamente.


------------

#### Compilaciones

### Generar APK:

> npx react-native run-android --variant=release
cd android && ./gradlew assembleRelease

Este comando genera un archivo APK para su app en el folder android/app/build/outputs/apk/release

Referencia: [https://www.quora.com/How-can-I-generate-an-APK-of-a-React-Native-app-and-set-the-app-directly-to-my-Android-phone](https://www.quora.com/How-can-I-generate-an-APK-of-a-React-Native-app-and-set-the-app-directly-to-my-Android-phone)

