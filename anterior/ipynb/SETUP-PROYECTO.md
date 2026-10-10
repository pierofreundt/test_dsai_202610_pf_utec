# Setup de entorno Python + Jupyter (con uv)

Guía reutilizable para configurar cualquier carpeta de proyecto nueva.

## 1. Crear la carpeta y entrar en ella

```powershell
mkdir "MiProyecto"
cd "MiProyecto"
```

## 2. Crear el entorno virtual con uv

```powershell
uv venv --python 3.14 ".venv"
```

Cambia `3.14` por la versión de Python que necesites.

## 3. Instalar los paquetes que vayas a usar

Para notebooks, como mínimo `ipykernel`:

```powershell
uv pip install --python ".venv\Scripts\python.exe" ipykernel
```

Y cualquier otro paquete (pandas, numpy, etc.):

```powershell
uv pip install --python ".venv\Scripts\python.exe" pandas numpy
```

## 4. Registrar el entorno como kernel de Jupyter

```powershell
& ".venv\Scripts\python.exe" -m ipykernel install --user --name="mi-proyecto" --display-name="Python 3.14 (MiProyecto)"
```

- `--name`: identificador interno (sin espacios).
- `--display-name`: lo que verás en el selector de kernel de VS Code.

## 5. Crear/abrir el notebook y seleccionar el kernel

- Abre o crea el `.ipynb` en VS Code.
- Click en el selector de kernel (arriba a la derecha) → elige el `--display-name` que pusiste.

## 6. (Opcional) Guardar dependencias para reproducibilidad

```powershell
uv pip freeze --python ".venv\Scripts\python.exe" > requirements.txt
```

Para recrear el entorno en otra máquina, repite los pasos 2 y luego:

```powershell
uv pip install --python ".venv\Scripts\python.exe" -r requirements.txt
```

## Notas

- Cada carpeta/proyecto nuevo debería tener su propio `.venv` para evitar conflictos de versiones entre proyectos.
- Si `pip install` falla con el error `externally-managed-environment`, es porque estás instalando sobre el Python global gestionado por `uv` en vez de sobre el `.venv` del proyecto. Solución: usa siempre `--python ".venv\Scripts\python.exe"` como en los comandos de arriba.
