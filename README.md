# Librería para angular

[Ir a Repositorio (Verdaccio)](http://vps183761.vps.ovh.ca:4873)

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

## Publicación de la librería

### 1) Mediante un archivo ***tgz*** e instándolo en el directorio correspodiente:

```
cd dist/weather
npm pack
```
**Nota: hacer un script**

Obtendríamos el fichero dentro de la carpeta dist, para instalar la librería tan sólo tendríamos que hacer un:

```
npm install ./dist/weather/weather-0.0.1.tgz 
```

Finalizada su instalación tendremos la librería instalada en nuestro package.json.

Podemos comprobarlo comentando del tsconfig.json el path donde se encuentra la librería.

```
  "weather": "file:dist/weather/weather-0.0.1.tgz",
```

Si hacemos --> ng build weathertest y servimos desde la carpeta generada el proyecto dist/weathertest con un servidor (http-server)

### 2) Mediante un repositorio propio Verdaccio

#### Instalacón del repositorio

Instalación de Verdaccio [Verdaccio-docker-compose](verdaccio/docker-compose.yml)

Configuración de Verdaccio [Verdaccio-config](verdaccio/config/config.yaml)

*Nota: recordar cambiar los permisos al fichero (htpasswd)*

#### Publicación en Verdaccio

- Lo primero que tendríamos que hacer es modificar la versión de nuestra librería (weather/package.json).
    
  package de la librería: [package.joson](projects/weather/package.json)


- Extenderemos el script del package.json para poder publicar la librería en nuestro repo.
  
  package del proyecto general: [package.json](package.json)

```
  "weatherbuild": "ng build weather && cd dist/weather && npm publish --registry http://vps183761.vps.ovh.ca:4873"
```

- Lanzamos ahora el script --> npm run weatherbuild

- Para hacer una instalación del paquete basta con 

```
  npm install @balsalobre/weather
  npm i @balsalobre/weather --registry http://vps183761.vps.ovh.ca:4873 --save
```

Nota:

```
npm config set registry http://vps183761.vps.ovh.ca:4873/
npm config set always-auth true
npm login

yarn config set registry http://vps183761.vps.ovh.ca:4873/
yarn config get registry
yarn config get always-auth
yarn login (no-funciona)
yarn add ngx-map-lib

```