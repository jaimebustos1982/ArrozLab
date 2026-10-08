# ArrozLab

Planta Virtual de Procesos Agroindustriales · Molino de arroz
Programa de Ingeniería Agroindustrial · Universidad Surcolombiana · Ing. Jaime Daniel Bustos, D.Sc.

```
index.html                        la aplicación completa (un solo archivo)
manifest.json                     datos para instalarla como aplicación en el PC
sw.js                             funcionamiento sin conexión y actualización automática
icon-192.png, icon-512.png        íconos (panícula de paddy y grano blanco)
registro_arrozlab_apps_script.gs  backend del registro de uso (va en Google Apps Script, no en GitHub)
```

## Publicar en GitHub Pages (igual que las otras plantas)

1. En GitHub, crea un repositorio público llamado `ArrozLab`.
2. **Add file → Upload files**: sube `index.html`, `manifest.json`, `sw.js`, `icon-192.png` e `icon-512.png`.
3. **Settings → Pages → Deploy from a branch → main / (root) → Save**.
4. En uno o dos minutos queda en `https://jaimebustos1982.github.io/ArrozLab/`.

En el PC, Chrome o Edge muestran el botón **Instalar** en la barra de direcciones: así queda como aplicación de escritorio, con su ícono, y funciona sin conexión. El escudo de la USCO va incrustado en `index.html`.

## Activar el registro central (hoja exclusiva de ArrozLab)

Cada Lab tiene su propia Google Sheet. No pegues este script en la hoja de otra planta.

1. Crea una Google Sheet nueva llamada **Registro ArrozLab**.
2. **Extensiones → Apps Script**. Borra el contenido y pega todo `registro_arrozlab_apps_script.gs`. Guarda.
3. **Implementar → Nueva implementación → tipo Aplicación web**.
   - Ejecutar como: **Yo**.
   - Quién tiene acceso: **Cualquier usuario**.
4. Autoriza y copia la URL que termina en `/exec`.
5. En `index.html`, busca `const SHEET_WEBAPP_URL="";` y pega la URL entre las comillas.
6. Sube de nuevo `index.html` y `sw.js` con la versión cambiada en los dos: `VERSION` en `index.html` y `CACHE_NAME` en `sw.js` (de `2026.10.08-R1` a `-R2`).

Cada vez que edites el Apps Script: **Implementar → Gestionar implementaciones → editar → Nueva versión** (la URL no cambia).

## Código de acceso docente

`ARROZ-2026`. Está en `DOCENTE_CODE` (index.html) y en `SECRET` (Apps Script); si cambias uno, cambia el otro. El código viaja dentro del archivo, así que protege de curiosos, no de alguien que lea el código fuente.

## La planta

Nave de 96 × 40 m con 16 m libres bajo la cercha, para que los equipos queden a escala real: báscula camionera de 18 m con volquetas, secadora de torre de 14 m con horno de cascarilla, dos silos de 9,2 m de diámetro (500 t cada uno), trilla, tolvas de producto de 40 t y empaque. Doce estaciones, en el orden del proceso:

1. Recibo y báscula camionera · 2. Laboratorio de recibo · 3. Prelimpiadora · 4. Secadora de torre y horno de cascarilla · 5. Limpiadora de zarandas · 6. Silos de almacenamiento · 7. Descascaradoras y mesa separadora · 8. Blanqueo y pulido · 9. Clasificación y selección por color · 10. Tolvas de producto · 11. Empaque y bodega · 12. Laboratorio de calidad.

La cascarilla que sale de la trilla viaja por un ducto neumático hasta el horno de la secadora, igual que en un molino colombiano.

## Turnos (10 turnos · 30 estrellas)

| Turno | Producto | Variables que ajusta el estudiante | Cálculo de la bitácora |
|---|---|---|---|
| 1 | Paddy verde aceptado | aceptar o rechazar 6 volquetas | paddy seco equivalente a 13 % |
| 2 | Paddy prelimpio | criba de escalpe, aire de aspiración, caudal | impurezas residuales |
| 3 | Paddy seco | temperatura del aire, pasadas, reposo | agua evaporada del lote |
| 4 | Paddy limpio | aire de aspiración, ranura de la zaranda | vanos retirados (distribución normal) |
| 5 | Paddy almacenado | HR máxima de aireación, caudal específico | humedad de equilibrio (isoterma) |
| 6 | Arroz integral | luz entre rodillos, diferencia de velocidad | carga de las descascaradoras |
| 7 | Arroz blanco pulido | presión de la blanqueadora, agua del pulidor | rendimiento de pilada |
| 8 | Arroz excelso clasificado | alvéolo del cilindro, sensibilidad óptica | excelso producido |
| 9 | Arroz excelso y popular | partido en cada mezcla | granza sobrante (balance de mezcla) |
| 10 | Arroz empacado | puntos de ajuste y velocidad | arroz regalado |

## Normas y referencias

- **NTC 671** (arroz elaborado blanco): se usa el requisito de humedad < 14 %, verificado en las fichas técnicas del ICBF que la citan. El texto completo es de ICONTEC.
- **Codex CXS 198-1995**, Norma para el arroz: humedad ≤ 15 %, materia extraña y grados de elaboración.
- **Resolución 32209 de 2020 (SIC)**: contenido neto de preempacados.
- **Isoterma de desorción del paddy**: Oliveira, D. E. C.; Resende, O.; Campos, R. C.; Donadon, J. R. (2014). *Científica* 42(3): 203–210. doi:10.15361/1984-5529.2014v42n3p203-210 (modelo de Henderson).
- Los límites de recibo, secado, limpieza, aireación, descascarado, blancura y las categorías excelso y popular son estándares de fábrica del molino, no de una norma. Los parámetros de los modelos son ilustrativos.

## Qué registra

Cada ingreso, cada lote producido y cada cierre de sesión, con: integrantes y códigos, modalidad, grupo, turno, producto, número de intento, estrellas, puntos, predicción y valor real, resultado por categoría (inocuidad y operación, norma, cliente, eficiencia), fallas, tiempo activo en el turno, tiempo activo total y las variables que fijó el equipo.

El panel docente muestra el resumen por estudiante (10 turnos, 30 estrellas), la dificultad por turno y los últimos lotes, y exporta tres archivos CSV (separador `;`). Desde el panel se cambian los precios unitarios (paddy verde y seco, arroz excelso, popular y partido, salvado, energía, cascarilla, rodillos de caucho) y se pueden habilitar todos los turnos. Los precios mueven el óptimo económico de cada turno.

## Para verificar que un cambio llegó

El pie del panel docente muestra la versión (`2026.10.08-R1`). Cámbiala en `VERSION` dentro de `index.html` y en `CACHE_NAME` de `sw.js` cada vez que publiques.
