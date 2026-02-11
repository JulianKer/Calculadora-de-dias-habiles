# Calculadora de Dias Habiles - Argentina   <img src="https://github.com/JulianKer/Calculadora-de-dias-habiles/blob/main/icons/calendar-detail.svg" alt="Calendar logo" title="Calendar logo" width="50" align="center"/>

Calculadora web que permite obtener una fecha final a partir de una fecha de inicio y una cantidad de días hábiles, excluyendo automáticamente **fines de semana** y **feriados nacionales de Argentina** y excluir el mes de **enero**. Ideal para calcular fechas de plazos para abogados y escribanos.   

---

> [!TIP]
> Visita la siguiente web para ver su funcionamiento: <a href="https://calculadora-de-dias-habiles.vercel.app/" target="_blank"> Calculadora de Dias Habiles - Argentina</a>


---

## Vista previa

| Calculadora | Listado de Feriados |
|---|---|
| Ingresa fecha de inicio y cantidad de dias habiles para obtener la fecha final con un resumen detallado. Además, tienes la opción de exluir el mes de Enero. | Al cargar la pagina se muestra automaticamente el listado completo de feriados del año actual con nombre, tipo y dia de la semana. |

---

## Características

- **Cálculo preciso de días hábiles** - Excluye sábados, domingos y feriados nacionales argentinos.
- **Feriados en tiempo real** - Consume la API pública de [ArgentinaDatos](https://argentinadatos.com) para obtener los feriados del año actual de forma dinámica.
- **Listado visual de feriados** - Muestra todos los feriados del año en una tarjeta dedicada con fecha, nombre, tipo y dia de la semana, visible sin necesidad de calcular.
- **Resumen detallado** - Muestra fecha de inicio, fecha final, días hábiles, días naturales transcurridos, fines de semana omitidos y feriados omitidos.
- **Responsive** - Adaptado a cualquier pantalla (desktop, tablet, mobile).

---

## API utilizada

La aplicación consume la siguiente API publica:

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

- La API se llama automáticamente al cargar la página con el año actual.
- Al calcular, si el rango de días abarca mas de un año, se consultan los feriados de todos los años involucrados.
- Los resultados se cachean en memoria para evitar llamadas duplicadas.
- Si la API falla o no hay conexión, el cálculo continua sin feriados y se muestra un mensaje de error en la tarjeta de feriados.

> Documentación completa de la API: [https://argentinadatos.com](https://argentinadatos.com)

---

## Como funciona el cálculo

1. El usuario ingresa una **fecha de inicio** y una **cantidad de días hábiles**.
2. Selecciona si desea **excluir el mes de Enero** para el recuento de días hábiles.
3. Se obtienen los feriados del año (o años) correspondiente(s) desde la API.
4. A partir de la fecha de inicio, se avanza día por día:
   - Si es **sábado o domingo** → se omite (no cuenta como día hábil).
   - Si es **feriado nacional** → se omite (no cuenta como día hábil).
   - Si es **día hábil** → se suma al contador.
5. Se repite hasta alcanzar la cantidad de día hábiles solicitados.
6. Se muestra la **fecha final** y un resumen con el desglose completo.

---


![Readme by:](https://img.shields.io/badge/Readme%20by:-00A1E0?style=for-the-badge&logo=account&logoColor=white)
[![JulianKer](https://img.shields.io/badge/JulianKer-000000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/JulianKer)
