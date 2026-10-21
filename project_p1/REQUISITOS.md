# Requisitos para renderizar Project-Report.qmd (solo Python)

## 1. Instalar

1. **Quarto**: https://quarto.org/docs/get-started/
2. **TinyTeX** (para generar el PDF), desde una terminal:
   ```
   quarto install tinytex
   ```
3. **Python 3.10+**: https://www.python.org/downloads/
4. **Librerías de Python** (en una terminal, dentro de la carpeta del proyecto):
   ```
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter ipykernel tabulate
   ```
   `jupyter`/`ipykernel` son obligatorios: Quarto los usa para ejecutar los chunks de Python.
   `tabulate` es necesario para mostrar tablas bonitas (ver punto 3).

## 2. Renderizar

Desde la carpeta `Project-Report/`:
```
quarto render Project-Report.qmd
```
Esto genera `Project-Report.pdf`. Si falla, correr primero `quarto check` para confirmar que Python y TinyTeX están bien instalados.

## 3. Cómo mostrar tablas de pandas (para que se vean bien en el PDF)

Dejar el `DataFrame` como última línea del chunk (por ejemplo, `df` solo, sin `print()`) ya es suficiente: Quarto lo convierte automáticamente en una tabla con formato correcto en el PDF (esto se probó y funciona). El chunk de verificación al inicio del `.qmd` (con los integrantes y sus mascotas) sirve justamente para confirmar esto al renderizar por primera vez.

Si con muchas columnas o decimales la tabla se ve mal, como alternativa se puede usar:
```python
from IPython.display import Markdown
Markdown(df.to_markdown(index=False))
```
(requiere el paquete `tabulate`, ya incluido en el paso 1).