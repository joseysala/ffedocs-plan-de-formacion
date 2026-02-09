# 📝 Automatización FFE - Planes de formación

👨‍🏫 IES: Ciudad Escolar

📥 Depto: Informática y Comunicaciones

🧑‍💻 Profesor: José Sala Gutiérrez

---

El objetivo de este proyecto no es otro que facilitar el trabajo burocrático de los docentes tutores de prácticas de FFE (Fase de Formación en Empresa) de los ciclos formativos de FP en centros de la Comunidad de Madrid.

En la primera versión de este proyecto, se automatiza la creación de **los planes formativos** de los alumnos a partir de la plantilla publicada en la Comunidad de Madrid y de dos ficheros de texto:

- `datos_alumnos.txt`: fichero con registros de cada alumno cuyos campos están delimitados por  "|".
- `datos_ciclo.txt`: fichero con registros de los atributos comunes de todos los planes para un determinado ciclo. Los campos están delimitados por ":".
- `anexo_plan_de_formacion_editable.pdf`: plantilla propia de la Comunidad de Madrid.

Al finalizar la ejecución, se habrán creado un plan formativo por cada alumno usando la nombreclatura solicitada por jefatura de estudios para subir los ficheros al formulario:

```text
    Apellido1Alumno_Apellido2Alumno_CodigoCiclo.pdf
```

## Releases

Para facilitar la distribución de la herramienta se ha generado una release con todo lo necesario para poder ejecutarlo. La puedes encontrar en la sección  `releases` dentro de este repositorio de GitHub como un fichero ZIP.

## Manual de instrucciones

Para poder utilizar esta herramienta, sigue los siguientes pasos:

1) Descarga la release publicada

2) Descomprime el fichero en tu directorio personal de trabajo (ej. C:\Users\xxx)

3) Modifica el fichero `datos_alumnos.txt` ubicado en "RellenaPlanFormacionFFE\app\data" añadiendo los registros con los datos de cada alumno que vaya a realizar la FFE

4) Modifica el fichero `datos_ciclo.txt` ubicado en "RellenaPlanFormacionFFE\app\data" modificando los registros de acuerdo al IES, Ciclo, Módulos evaluados, RAs involucrados, tutor docente...

5) Ejecuta el fichero `RellenaPlanFormacionFFE.exe`

6) Revisa que todos los planes se han generado y que el contenido se ajusta a lo esperado

7) Si hubiera algun error, actualiza de nuevo los ficheros txt y re-ejecuta la aplicación. Los planes generados se sobreescriben.

## 🔧 Tecnologías utilizadas

- Maven + Java 23
- Log slf4j + Logback
- itextpdf
- jpackage + signtool

## 📁 Estructura del proyecto

```text
src/
├─ main/
│ ├─ es/ciudadescolar/
│ │ ├─ ffedoc/
│ │ │   └─ PdfManager.java
│ └─ resources/
│    ├─ data/
│    │    ├─ datos_alumnos.txt
│    │    └─ datos_ciclo.txt   
│    ├─ templates/
│    │    └─ anexo_plan_de_formacion_editable.txt   
│    └─ logback.xml
├─ .gitignore
├─ pom.xml
├─ ffe_docs_plan_formacion.log
└─ readme.md
```
