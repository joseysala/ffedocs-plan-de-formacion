# 📝 Automatización FFE - Planes de formación

👨‍🏫 IES: Ciudad Escolar

📥 Depto: Informática y Comunicaciones

🧑‍💻 Profesor: José Sala Gutiérrez

---

El objetivo de este proyecto no es otro que facilitar el trabajo burocrático de los docentes tutores de prácticas de FFE (Fase de Formación en Empresa) de los ciclos formativos de FP en centros de la Comunidad de Madrid.

En la nueva versión de este proyecto, se automatiza la creación de **los planes formativos** de los alumnos a partir de la plantilla publicada en la Comunidad de Madrid y de un fichero Excel:

- `datos_ffe_plan_de_formacion.xlsx`: fichero excel con dos tabs. El primero con los atributos comunes de todos los planes para un determinado ciclo y el segundo con los registros de cada alumno.
- `anexo_plan_de_formacion_editable.pdf`: plantilla propia de la Comunidad de Madrid.

Al finalizar la ejecución, se habrán creado un plan formativo por cada alumno usando la nombreclatura solicitada por jefatura de estudios para subir los ficheros al formulario:

```text
    Apellido1Alumno_Apellido2Alumno_CodigoCiclo.pdf
    Apellido1Alumno_CodigoCiclo.pdf (alumnos con un único apellido)
```

## Releases

Para facilitar la distribución de la herramienta se ha generado una release con todo lo necesario para poder ejecutarlo. La puedes encontrar en la sección  `releases` dentro de este repositorio de GitHub como un fichero ZIP.

## Manual de instrucciones

Para poder utilizar esta herramienta, sigue los siguientes pasos:

1) Descarga la release publicada

2) Descomprime el fichero en tu directorio personal de trabajo (ej. C:\Users\xxx)

3) Modifica el fichero `datos_ffe_plan_de_formacion.xlsx` ubicado en "RellenaYFirmaPlanFormacionFFE\app\data" añadiendo los registros con los datos de cada alumno que vaya a realizar la FFE y también modificando los datos comunes de acuerdo al IES, Ciclo, Módulos evaluados, RAs involucrados, tutor docente...

4) **Paso opcional no bloqueante**: Si se quiere firmar el pdf con firma FNMT, se deben añadir como variables de entorno:
    - *CERT_PATH*: La ruta absoluta del certificado .PK12. Ejemplo en windows: setx CERT_PATH "C:\\Users\\jsala\\mi_certificado.p12"
    - *CERT_PASSWORD*: la contraseña de la clave privada de dicho certificado. Ejemplo en windows: setx CERT_PASSWORD "contraseña"

    **Nota**: El registro de variables puedes hacerlo en Windows desde "ventanita negra": `cmd` o `powershell`. Si no se registran esas variables de entorno, se generarán los pdfs pero no se procederá a su firma.

5) Ejecuta el fichero `RellenaYFirmaPlanFormacionFFE.exe`

6) Revisa que todos los planes se han generado y que el contenido se ajusta a lo esperado. Los pdfs sin firmar estarán en una carpeta `<codigo_ciclo>_planes_sin_firmar` y los pdfs firmados en `<codigo_ciclo>_planes_firmados`.

7) Si hubiera algun error, actualiza de nuevo el fichero Excel y re-ejecuta la aplicación. Los planes generados se sobreescriben.

8) No olvides "vaciar" las variables de entorno si has firmado digitalmente los documentos:
   -Ejemplo en windows: setx CERT_PATH "" y posteriormente:  reg delete HKCU\Environment /V CERT_PATH /F
   -Ejemplo en windows: setx CERT_PASSWORD "" y posteriormente: reg delete HKCU\Environment /V CERT_PASSWORD /F

## 🔧 Tecnologías utilizadas

- Maven + Java 23
- Log slf4j + Logback
- itextpdf
- jpackage + signtool
- java security + bouncycastle
- apache poi

## 📁 Estructura del proyecto

```text
src/
├─ main/
│ ├─ es/ciudadescolar/
│ │ ├─ ffedoc/
│ │ │   └─ PdfManager.java
│ └─ resources/
│    ├─ data/
│    │    └─ datos_ffe_plan_de_formacion.xlsx   
│    ├─ templates/
│    │    └─ anexo_plan_de_formacion_editable.pdf   
│    └─ logback.xml
├─ .gitignore
├─ pom.xml
├─ ffe_docs_plan_formacion.log
└─ readme.md
```

## ✅ Bug fixing

- Adaptación de los ficheros de entrada:
  - Se eliminan los nombres de los pié de firmas
  - Se añade email de empresa
  - De acuerdo a jefatura de estudios (11/02/26), el periodo de FFEs en 2º será siempre `periodo número 2`


## ✅ Versiones

v1.0.1: Permite generar los planes de formación con el formato antiguo a partir de dos ficheros txt.
v2.0.1: Permite generar los planes de formación con el formato nuevo y posteriormente firmarlos a partir de dos ficheros txt.
v3.0.0: Permite generar los planes de formación con el formato nuevo y posteriormente firmarlos a partir de un fichero excel.
