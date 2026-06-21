# Datos derivados: Optimización de la red de espacios climáticos de València

Este repositorio contiene los **datos derivados** (elaboración propia) generados en el
Trabajo de Fin de Grado sobre la planificación de la expansión de la red de espacios
climáticos (refugios climáticos) de València mediante optimización espacial multiobjetivo.

Su finalidad es dar acceso público y reproducible a los conjuntos de datos que alimentan
el modelo de optimización, en cumplimiento de los requisitos de publicación de datos del
trabajo.

## Naturaleza de los datos

- Todos los datos están **agregados a nivel de sección censal, distrito o barrio**, o bien
  son catálogos de ubicaciones candidatas (equipamientos, plazas, zonas verdes, fuentes).
- **No se incluye ningún dato de carácter personal.** La escala mínima de agregación es la
  sección censal, que impide identificar a personas concretas. No es de aplicación el RGPD
  ni la LOPDGDD.
- Estos ficheros son **elaboración propia** obtenida a partir de fuentes públicas y abiertas.
  Las fuentes originales **no se redistribuyen** aquí; se enlazan en
  [`FUENTES.md`](FUENTES.md).

## Estructura del repositorio

```
.
├── data/              Datos derivados tabulares (CSV)
│   └── geo/           Datos derivados geoespaciales (GeoJSON) y grafo viario (GraphML)
├── DICCIONARIO_DE_DATOS.md   Descripción de cada fichero y de sus columnas
├── FUENTES.md         Tabla de fuentes originales (URL, fecha de acceso, licencia)
├── LICENSE            Licencia de los datos derivados (CC BY 4.0)
├── LICENSE-OSM-DERIVED.md   Nota de licencia ODbL para los derivados de OpenStreetMap
└── README.md
```

## Metodología

La construcción de cada conjunto de datos se describe en detalle en la memoria del TFG.
Como guía rápida:

| Fichero / conjunto                | Dónde se explica en la memoria              |
|-----------------------------------|---------------------------------------------|
| Índice de vulnerabilidad (HVI)    | Cap. 5, "Índice de vulnerabilidad al calor" |
| Variables del HVI (pct65, renta, SUHI, NDVI) | Cap. 5, subsecciones por variable |
| Índice de flujo peatonal (FP)     | Cap. 5, "Flujo peatonal y peso de demanda"  |
| Peso de demanda `wk`              | Cap. 5, "Flujo peatonal y peso de demanda"  |
| Catálogos de candidatos (J1, J2E, J2V, J3) | Cap. 5, "Candidatos a intervención y red viaria" |
| Red base y fuentes fijas          | Cap. 5, "Candidatos a intervención y red viaria" |
| Grafo viario y matrices de distancia | Cap. 5, "Red viaria peatonal y matrices de distancias" |
| Frontera de Pareto                | Cap. 7, "Solución de referencia y frontera de Pareto" |

## Sistema de referencia

Salvo que se indique lo contrario, las geometrías se distribuyen en **EPSG:4326** (WGS84)
para máxima interoperabilidad. Los cálculos espaciales del trabajo se realizaron en
**EPSG:25830** (UTM 30N, ETRS89). Las distancias de los ficheros de matrices están en metros.

## Licencia

- Datos derivados: **CC BY 4.0** (ver [`LICENSE`](LICENSE)).
- Excepción: el grafo viario y las capas derivadas de OpenStreetMap se rigen por **ODbL**
  (ver [`LICENSE-OSM-DERIVED.md`](LICENSE-OSM-DERIVED.md)).
