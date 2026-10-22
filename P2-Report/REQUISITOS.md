# Requisitos para renderizar P2-Report.qmd (solo Python)

## 1. Instalar

1. **Quarto**: https://quarto.org/docs/get-started/
2. **TinyTeX** (para generar el PDF), desde una terminal:
   ```
   quarto install tinytex
   ```
3. **Python 3.10+**: https://www.python.org/downloads/
4. **Librerías de Python** (en una terminal, dentro de la carpeta del proyecto):
   ```
   pip install pandas numpy matplotlib seaborn scikit-learn scipy jupyter ipykernel tabulate
   ```
   `jupyter`/`ipykernel` son obligatorios: Quarto los usa para ejecutar los chunks de Python.
   `scikit-learn` y `scipy` son necesarios para los modelos y las pruebas de la P2.
   `tabulate` es necesario como alternativa para mostrar tablas (ver punto 3).

A diferencia de la P1, la P2 carga el dataset desde `datos/smartphone_use.csv`
(incluido en esta carpeta), así que **no se necesita `kagglehub` ni internet**.

## 2. Renderizar

Desde la carpeta `P2-Report/`:
```
quarto render P2-Report.qmd
```
Esto genera `P2-Report.pdf`. Si falla, correr primero `quarto check` para confirmar que Python y TinyTeX están bien instalados.

## 3. Cómo mostrar tablas de pandas (para que se vean bien en el PDF)

Dejar el `DataFrame` como última línea del chunk (por ejemplo, `df` solo, sin `print()`) ya es suficiente: Quarto lo convierte automáticamente en una tabla con formato correcto en el PDF (esto se probó y funciona en la P1).

Si con muchas columnas o decimales la tabla se ve mal, como alternativa se puede usar:
```python
from IPython.display import Markdown
Markdown(df.to_markdown(index=False))
```
(requiere el paquete `tabulate`, ya incluido en el paso 1).

En este informe, además, está disponible la función `tabla()` (heredada de la P1),
que imprime DataFrames en estilo booktabs con filas alternadas.
