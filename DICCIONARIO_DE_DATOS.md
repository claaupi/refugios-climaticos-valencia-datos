# Diccionario de datos

Descripción de cada fichero del repositorio y de sus columnas. La clave de unión entre
ficheros tabulares es `cod_ine` (código de sección censal del INE, 10 dígitos).

> Nota: las columnas derivadas de datos de la Fundació Visit València (visitantes por
> monumento) se han eliminado de los ficheros públicos por tratarse de un dato no
> redistribuible. Estas variables fueron evaluadas y **descartadas** del modelo, por lo
> que su ausencia no afecta a la reproducibilidad de los resultados.

## Clave común

| Columna     | Descripción |
|-------------|-------------|
| `cod_ine`   | Código oficial de sección censal del INE (10 dígitos): municipio (5) + distrito (2) + sección (3). |
| `coddistrit`| Código de distrito (2 dígitos). |
| `codbarrio` | Código de barrio. |

---

## Ficheros tabulares (`data/`)

### `poblacion_por_seccion.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `pob_total` | Población total según padrón 2025 (factor de escala `p_k` del modelo). |
| `pob_2023` | Población total según padrón 2023. |

### `pct_65mas_serie.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `pct_65mas_2023/2024/2025` | Porcentaje de población de 65 o más años, por año. |

### `renta_pc.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `renta_pc` | Renta neta media por persona (€), año de referencia 2023. |

### `suhi_por_seccion.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `suhi_2023/2024/2025` | Isla de calor urbana superficial (°C) por verano, derivada de Landsat 8/9. |

### `ndvi_por_seccion.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `ndvi_medio_2023/2024/2025` | NDVI medio estival por sección, derivado de Landsat 8/9. |

### `antiguedad_por_seccion.csv`
Variables del Catastro evaluadas y **descartadas** del HVI (se incluyen por transparencia).
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `n_edificios` | Nº de edificios. |
| `pct_anterior_1980` | % edificios construidos antes de 1980. |
| `pct_posterior_2010` | % edificios construidos después de 2010. |

### `area_edificios_catastro.csv`
| Columna | Descripción |
|---------|-------------|
| `x`, `y` | Coordenadas del edificio. |
| `anio` | Año de construcción catastral. |
| `area_m2` | Área de planta estimada (m²). |
| `area_oficial` | Área oficial catastral (m²). |

### `hvi_base.csv`
Tabla maestra con todas las variables intermedias del HVI y del FP por sección
(normalizaciones, direcciones, series anuales). Columnas autoexplicativas con sufijos:
`_norm` (normalizado min-max), `_hvi` (valor usado en el índice), `_log` (transformación
logarítmica). Incluye el peso de demanda final `wk`.

### `hvi_final.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine`, `coddistrit` | Sección y distrito. |
| `pct_65mas_norm`, `renta_pc_norm`, `suhi_ref_norm`, `ndvi_ref_norm` | Las 4 variables normalizadas y orientadas (renta y NDVI ya invertidas). |
| `HVI` | Índice de vulnerabilidad al calor, [0,1]. |
| `HVI_quintil` | Quintil de vulnerabilidad. |

### `hvi_base.csv` (resumen de uso)
Versión extendida con las series anuales y todas las variables candidatas; `hvi_final.csv`
es su versión depurada.

### `hvi_por_distrito.csv` / `hvi_por_barrio.csv`
HVI medio ponderado agregado por distrito o barrio, con nº de secciones y población.

### `hvi_sensibilidad_pesos.csv`
Resultados del análisis de sensibilidad de pesos del HVI (PCA, cargas, varianza explicada).

### `flujo_peatonal.csv`
Variables candidatas del índice de flujo peatonal por sección (conteos brutos).
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `n_paradas_emt`, `n_lineas_emt_unicas` | Paradas y líneas únicas de autobús EMT. |
| `n_bocas_metro`, `n_lineas_metro_unicas` | Bocas y líneas únicas de metro/tranvía. |
| `n_comercios` | Comercios y restaurantes (OSM). |
| `n_monumentos` | Monumentos municipales. |
| `pct_area_turistica` | % de superficie de la sección en área turística/patrimonial. |

### `fp_final.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `FP` | Índice de flujo peatonal final, [0,1]. |
| `*_log_norm` | Las 4 variables retenidas, transformadas log y normalizadas. |

### `wk_final.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine`, `coddistrit` | Sección y distrito. |
| `pob_total`, `HVI`, `FP` | Componentes. |
| `wk` | Peso de demanda final (α = 0,80), [0,1]. Demanda efectiva = `pob_total` × `wk`. |

### `snap_secciones.csv`
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `nodo_red` | ID del nodo de la red viaria peatonal asignado al centroide. |
| `dist_snap_m` | Distancia de snap (m). |

### `dist_seccion_candidato.csv`
Matriz sección–candidato (pares dentro del radio de 800 m).
| Columna | Descripción |
|---------|-------------|
| `cod_ine` | Sección censal. |
| `id_candidato` | ID del candidato a refugio. |
| `dist_m` | Distancia peatonal real (m) por Dijkstra. |

### `dist_candidato_fuente.csv`
Matriz candidato exterior–fuente (pares dentro del radio de 150 m).
| Columna | Descripción |
|---------|-------------|
| `id_candidato` | Candidato exterior (J2E/J2V). |
| `id_fuente` | Fuente de agua. |
| `tipo_fuente` | Fija (F) o candidata (J3). |
| `dist_m` | Distancia peatonal real (m). |

### `candidatos_ext_activables.csv` / `candidatos_ext_infactibles.csv`
Listas de IDs de candidatos exteriores que cumplen / no cumplen la restricción de agua (R5).

### `pareto_frontera.csv`
Resultados del modelo a lo largo de la frontera de Pareto.
| Columna | Descripción |
|---------|-------------|
| `epsilon` | Tolerancia de cobertura. |
| `estado` | Estado del solver. |
| `O1_pct` | Cobertura (% demanda efectiva). |
| `dist_media_m` | Distancia media ponderada (m). |
| `n_J1`, `n_J2E`, `n_J2V`, `n_J3` | Nº de candidatos activados por tipo. |
| `n_sec_cub` | Secciones cubiertas. |
| `gini` | Índice de Gini entre distritos. |
| `tiempo_s` | Tiempo de resolución (s). |

---

## Ficheros geoespaciales (`data/geo/`)

| Fichero | Descripción |
|---------|-------------|
| `secciones_base.geojson` | 588 secciones censales con geometría. |
| `distritos_base.geojson` | 19 distritos. |
| `barrios_base.geojson` | 88 barrios. |
| `municipio_base.geojson` | Contorno municipal. |
| `candidatos_J1.geojson` | 161 equipamientos municipales interiores. |
| `candidatos_J2E.geojson` | 791 plazas y áreas monumentales. |
| `candidatos_J2V.geojson` | 507 zonas verdes elegibles. |
| `candidatos_J3.geojson` | 1.715 ubicaciones candidatas a fuente. |
| `J0_red_base.geojson` | 18 refugios climáticos ya operativos. |
| `fuentes_base.geojson` | 76 fuentes de agua fijas existentes. |
| `grafo_peatonal.graphml.gz` | Grafo viario peatonal (41.591 nodos, 129.862 aristas), comprimido con gzip. **Derivado de OpenStreetMap — licencia ODbL.** Para leerlo: `gunzip grafo_peatonal.graphml.gz` o, en Python, `osmnx.load_graphml` admite el fichero descomprimido. |
