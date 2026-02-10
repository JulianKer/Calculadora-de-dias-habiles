# Calculadora de Dias Habiles - Argentina   <img src="https://github.com/JulianKer/Calculadora-de-dias-habiles/blob/main/icons/calendar-detail.svg" alt="Calendar logo" title="Calendar logo" width="50" align="center"/>

Calculadora web estatica que permite obtener una fecha final a partir de una fecha de inicio y una cantidad de dias habiles, excluyendo automaticamente **fines de semana** y **feriados nacionales de Argentina**.

---

## Vista previa

| Calculadora | Listado de Feriados |
|---|---|
| Ingresa fecha de inicio y cantidad de dias habiles para obtener la fecha final con un resumen detallado. | Al cargar la pagina se muestra automaticamente el listado completo de feriados del anio actual con nombre, tipo y dia de la semana. |

---

## Caracteristicas

- **Calculo preciso de dias habiles** - Excluye sabados, domingos y feriados nacionales argentinos.
- **Feriados en tiempo real** - Consume la API publica de [ArgentinaDatos](https://argentinadatos.com) para obtener los feriados del anio actual de forma dinamica.
- **Listado visual de feriados** - Muestra todos los feriados del anio en una tarjeta dedicada con fecha, nombre, tipo y dia de la semana, visible sin necesidad de calcular.
- **Resumen detallado** - Muestra fecha de inicio, fecha final, dias habiles, dias naturales transcurridos, fines de semana omitidos y feriados omitidos.
- **Responsive** - Adaptado a cualquier pantalla (desktop, tablet, mobile).

---

## API utilizada

La aplicacion consume la siguiente API publica:

```
GET https://api.argentinadatos.com/v1/feriados/{anio}
```

**Respuesta de ejemplo:**

```json
[
  {
    "fecha": "2026-01-01",
    "tipo": "inamovible",
    "nombre": "Ano Nuevo"
  },
  {
    "fecha": "2026-02-16",
    "tipo": "inamovible",
    "nombre": "Carnaval"
  }
]
```

- La API se llama automaticamente al cargar la pagina con el anio actual.
- Al calcular, si el rango de dias abarca mas de un anio, se consultan los feriados de todos los anios involucrados.
- Los resultados se cachean en memoria para evitar llamadas duplicadas.
- Si la API falla o no hay conexion, el calculo continua sin feriados y se muestra un mensaje de error en la tarjeta de feriados.

> Documentacion completa de la API: [https://argentinadatos.com](https://argentinadatos.com)

---

## Como funciona el calculo

1. El usuario ingresa una **fecha de inicio** y una **cantidad de dias habiles**.
2. Se obtienen los feriados del anio (o anios) correspondiente(s) desde la API.
3. A partir de la fecha de inicio, se avanza dia por dia:
   - Si es **sabado o domingo** → se omite (no cuenta como dia habil).
   - Si es **feriado nacional** → se omite (no cuenta como dia habil).
   - Si es **dia habil** → se suma al contador.
4. Se repite hasta alcanzar la cantidad de dias habiles solicitados.
5. Se muestra la **fecha final** y un resumen con el desglose completo.

---


![Readme by:](https://img.shields.io/badge/Readme%20by:-00A1E0?style=for-the-badge&logo=account&logoColor=white)
[![JulianKer](https://img.shields.io/badge/JulianKer-000000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/JulianKer)
