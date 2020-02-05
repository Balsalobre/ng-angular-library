# Librería para angular

## Creación de librería

```
ng new weatherwidget --createApplication=false
```

Proyecto vacío (no iniciado).

```
ng generate library weather
```

Dentro del directorio **projects/weather/src/lib** nos encontramos el fichero **public-api.ts** punto de entrada a nuestra librería.

Necesitaremos una aplicación, para probar la biblioteca que estamos creando. La generamos mediante:

```
ng generate application weathertest
```

- En el fichero **angular.json** tenemos referenciado, tanto el proyecto de la librería como el que acabamos de crear.

- En el fichero **package.json** tenemos también una nueva dependencia del módulo que empaqueta nuestra librería.

```
    "ng-packagr": "^5.4.0",
```

- En el fichero **tsconfig.json** tenemos la referencia del punto de salida de la librería.

```
"paths": {
      "weather": [
        "dist/weather"
      ],
      "weather/*": [
        "dist/weather/*"
      ]
    }
```

- Agregamos nuestro componente a la librería ./projects/weather/src/lib/
- Agregamos también al **package.json** el siguiente script:
- Y lo lanzamos npm run weatherbuild
  
```
    "weatherbuild": "ng build weather",
```

- Se puede observar como se crea la carpeta dist donde tendremos la librería lista para usar.

## Proyecto de prueba importar librería

- Importamos el módulo *[ import { WeatherModule } from 'weather'; ]* desde la librería --> Recordar que el la ruta introducida en tsconfig nos está ayudando a resolver este directorio.
- En el *app.component.html* nos llevamos la etiqueta **<app-weather></app-weather>** y servimos el proyecto.