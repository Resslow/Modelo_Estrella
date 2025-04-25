# Modelo_Estrella
Este documento describe la transformación del modelo entidad-relación original hacia un modelo dimensional tipo estrella, diseñado específicamente para optimizar consultas analíticas sobre datos migratorios. El modelo estrella facilita el análisis multidimensional de la información relacionada con el nivel educativo de migrantes colombianos.
# Documentación del Modelo Estrella para Análisis Migratorio

## Estructura del Modelo Estrella

El modelo estrella consta de una tabla central de hechos conectada a múltiples tablas de dimensiones. Este diseño permite un acceso eficiente a los datos para análisis y reportes.

### Tabla de Hechos

**HECHOS_MIGRACION**
- Tabla central que contiene las métricas clave sobre eventos migratorios
- Cada registro representa un evento migratorio específico
- Campos principales:
  - `id_hecho_migracion`: Identificador único del hecho (clave primaria)
  - `id_tiempo`: Referencia a la dimensión de tiempo (cuándo ocurrió la migración)
  - `id_persona`: Referencia a la dimensión de persona (quién migró)
  - `id_ubicacion_origen`: Referencia a la dimensión de ubicación (desde dónde)
  - `id_ubicacion_destino`: Referencia a la dimensión de ubicación (hacia dónde)
  - `id_oficina`: Referencia a la dimensión de oficina (dónde se registró)
  - `id_conocimiento`: Referencia a la dimensión de conocimiento (formación académica)
  - `cantidad_personas`: Métrica que indica el número de personas en el registro
  - `edad_al_migrar`: Edad de la persona al momento de la migración

### Tablas de Dimensiones

**DIM_PERSONA**
- Contiene información desnormalizada sobre las personas migrantes
- Incluye atributos demográficos para facilitar análisis por segmentos
- Campos principales:
  - `id_persona`: Identificador único (clave primaria)
  - Identificadores originales (para trazabilidad)
  - Atributos descriptivos desnormalizados:
    - `nivel_academico`, `genero`, `etnia`, `estado_civil`, `grupo_edad`
  - Atributos numéricos: `edad`, `estatura`

**DIM_CONOCIMIENTO**
- Agrupa la información sobre áreas y subáreas de conocimiento académico
- Permite análisis por especialidad o campo de estudio
- Campos principales:
  - `id_conocimiento`: Identificador único (clave primaria)
  - `id_area`, `id_subarea`: Identificadores originales
  - `area_conocimiento`: Nombre del área de conocimiento
  - `subarea_conocimiento`: Nombre de la subárea específica

**DIM_UBICACION**
- Representa lugares geográficos (origen o destino)
- Incluye jerarquías geográficas para permitir drill-down/roll-up
- Campos principales:
  - `id_ubicacion`: Identificador único (clave primaria)
  - `id_pais`, `id_ciudad`: Identificadores originales
  - `pais`, `ciudad`: Nombres descriptivos
  - `continente`, `region`: Agrupaciones geográficas de mayor nivel

**DIM_TIEMPO**
- Contiene desgloses temporales para análisis por periodos
- Facilita análisis de tendencias y patrones temporales
- Campos principales:
  - `id_tiempo`: Identificador único (clave primaria)
  - `fecha_completa`: Fecha en formato DATE
  - Desgloses temporales: `anio`, `mes`, `dia`, `nombre_mes`, `trimestre`, `semestre`
  - `dia_semana`: Nombre del día de la semana

**DIM_OFICINA**
- Contiene información sobre las oficinas de registro migratorio
- Campos principales:
  - `id_oficina`: Identificador único (clave primaria)
  - `nombre_oficina`: Nombre descriptivo de la oficina
  - `tipo_oficina`: Clasificación de la oficina
  - `ubicacion`: Ubicación geográfica general
  - 
  ![image](https://github.com/user-attachments/assets/e555c5fc-a83c-466d-91c9-b01f1187769f)


