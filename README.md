# Recomendador — instrucciones rápidas

Versión breve para ejecutar `main.ipynb` y obtener las comparaciones (juegos que le gustan al usuario vs juegos recomendados por SVD).

1) Crear y activar un entorno (PowerShell):

```powershell
python -m venv .venv ; .\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

2) Abrir Jupyter en la carpeta del proyecto:

```powershell
jupyter lab
# o
jupyter notebook
```

3) En el notebook, ejecuta las celdas en orden: carga de datos, utilidades, split (make_holdout_by_user), generación de candidatos (`build_eval_candidates`) y el/los modelos que quieras.

4) Para ejecutar los gráficos no es necesario correr toda la plantilla ya que el punto 4 contiene todos los datos recolectados con anterioridad.
