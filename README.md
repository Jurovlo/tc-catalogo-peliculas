# Catálogo de películas · Team Challenge

> Renombrad este fichero a `README.md` y completad las partes entre `<...>`.

**Equipo:** `<Ángel Martínez>`, `<Sergio Di-Lolli>`, `<Sergio Mesa Franco>`, `<Julio Rovira Lozano>`

Catálogo de películas enriquecido a partir del dataset MovieLens: análisis con Pandas, sinopsis y web oficial desde la API de TMDB, y sinopsis en español generadas con Gemini.

## Reparto de funciones

| Persona | Rol | Notebook / tarea |
|---|---|---|
| Julio Rovira Lozano | A.Responsable de repo y datos | 01_ingesta_limpieza,  README y Bonus  |
| Sergio Di-Lolli | B.Analista de datos | 02_analisis y Bonus |
| Ángel Martínez | C.Integración con APIs | 03_tmdb y Bonus |
| Sergio Mesa Franco | D.IA generativa | 04_gemini y Bonus |

## Instalación

```bash
git clone https://github.com/Jurovlo/tc-catalogo-peliculas.git #SSH:git@github.com:Jurovlo/tc-catalogo-peliculas.git
cd tc-catalogo-peliculas
python -m venv venv #Con python 3.13: py -3.13 -m venv venv
source venv/bin/activate # Windows: venv\Scripts\activate y Git bash: source venv/Scripts/activate
pip install -r requirements.txt
cp .env.example .env            # y rellenad las claves
```

## Claves necesarias

| Variable | Dónde se obtiene |
|---|---|
| `TMDB_READ_ACCESS_TOKEN` o `TMDB_API_KEY` | themoviedb.org → Settings → API |
| `GEMINI_API_KEY` | aistudio.google.com |

## Ejecución

Ejecutad los notebooks **en este orden** (cada uno genera un CSV en `data/processed/` que usa el siguiente):

1. `01_ingesta_limpieza.ipynb` → `movies_clean.csv`
2. `02_analisis.ipynb`
3. `03_tmdb.ipynb` → `movies10.csv`
4. `04_gemini.ipynb` → `movies10_es.csv`

## Resultados principales

* Lo que más me ha sorprendido es que, al poner las tags todas en minúsculas y quitar los espacios, cambian los números. Y la que más sale, “In Netflix queue”, ni describe una película, así que ahí me he dado cuenta de que hay que mirar muy bien los datos antes de fiarse.
* También me ha llamado la atención lo de == y str.contains. Con “Batman” me salían solo 2 películas si buscaba el título exacto y 22 si buscaba la palabra dentro del título. No pensaba que un detalle tan pequeño podría cambiar tanto el resultado.
* Lo de las décadas también me ha parecido curioso porque las películas de los 80, 90 y 2000 tienen muchas más valoraciones, pero las antiguas de los años 20 a los años 70 tienen mejor nota media , así que tener más valoraciones no quiere decir que la nota sea mejor.
* Una de las cosas que más me ha interesado ha sido el uso de getpass, ya que permite solicitar información sensible, como una API Key, de forma oculta y segura sin mostrarla en pantalla. No lo conocía hasta ahora, así que me ha parecido muy interesante.
* También me ha parecido muy interesante el uso de response.raise_for_status(), ya que permite detectar errores en las peticiones a una API y gestionarlos de forma controlada. Además de este código, me ha parecido interesante el resto del código porque como hay un except request.RequestException, cada vez que el raise_for_status() salte con un error directamente lo pasará al dicho except para devolver cual es el error y cual es la id que falla.
