<!--
  Choose ONE language and delete the other half. / Elige UN idioma y borra la otra mitad.
  English: keep everything above the separator. / Español: conserva todo lo que está debajo del separador.
-->

<!--
Mandatory sections: Summary, Scope and impact, Verification, Checklist.
Delete the optional sections that don't apply. Short is fine.
-->

## Summary
<!--
What does this PR do and why? 2 to 5 sentences.
Link the issue, client request or lead if there is one (e.g. "Closes #12", "Lead: CIDRE").
-->


## Scope and impact
<!-- What this touches and, just as important, what it does NOT touch. Write "None" where it doesn't apply. -->
- **Changes:**
- **Does not change:** <!-- e.g. "No change to the model, predictors or prices", "Doesn't touch the server cron or Actions" -->
- **Data / infrastructure:** <!-- buckets, S3 paths, Earth Engine assets, scheduled jobs, workflows -->
- **Breaking changes:** <!-- renamed variables or params, changed URLs or schemas, outputs that would differ on a rerun -->

## How it works (optional)
<!--
Design decisions, data sources, edge cases and how they are handled.
Group by purpose or component, not file by file: GitHub already lists the changed files.
-->


## Usage (optional)
<!-- How to run or try it: command, notebook, new parameters. For env variables, give the names only, never the values. -->
```bash

```

## Results (optional)
<!-- Measurements, timings, metrics, before/after comparisons. Tables welcome. -->


## Verification
<!-- How you know it works. Tick what you did, remove what doesn't apply, and add items for the reviewer. -->
- [ ] Tests pass: <!-- suite, new tests -->
- [ ] Ran on real data: <!-- period, lead, region -->
- [ ] Outputs checked against a reference: <!-- previous version, direct read of the source, known values -->
- [ ] Reviewer:

## Notes for reviewers (optional)
<!-- Risks, open questions, things to check before merging, merge method if it must not be squashed. -->


## Checklist
- [ ] No secrets in code, notebooks, configs or this description (credentials come from env variables or `~/.netrc`; `.env` is not committed)
- [ ] No client-identifiable data exposed (client names, plot locations, public assets or buckets)
- [ ] New dependencies are listed above and pinned or optional
- [ ] README or docs updated if usage or behavior changed
- [ ] Notebook diffs are reviewable (outputs cleared or intentionally kept)

<!--
████████████████████████████████████████████████████████████████████
██  SEPARATOR / SEPARADOR                                          ██
██  ENGLISH: delete everything BELOW this block.                   ██
██  ESPAÑOL: borra todo lo que está ARRIBA de este bloque.         ██
████████████████████████████████████████████████████████████████████
-->

<!--
Secciones obligatorias: Resumen, Alcance e impacto, Verificación, Lista de control.
Borra las secciones opcionales que no apliquen. Breve está bien.
-->

## Resumen
<!--
¿Qué hace este PR y por qué? De 2 a 5 oraciones.
Enlaza el issue, pedido del cliente o lead si existe (ej. "Closes #12", "Lead: CIDRE").
-->


## Alcance e impacto
<!-- Qué toca y, igual de importante, qué NO toca. Escribe "Nada" donde no aplique. -->
- **Cambia:**
- **No cambia:** <!-- ej. "No cambia el modelo, los predictores ni los precios", "No toca el cron del server ni Actions" -->
- **Datos / infraestructura:** <!-- buckets, rutas de S3, assets de Earth Engine, jobs programados, workflows -->
- **Cambios que rompen compatibilidad:** <!-- variables o parámetros renombrados, URLs o esquemas cambiados, salidas que cambiarían al re-correr -->

## Cómo funciona (opcional)
<!--
Decisiones de diseño, fuentes de datos, casos borde y cómo se manejan.
Agrupa por propósito o componente, no archivo por archivo: GitHub ya lista los archivos modificados.
-->


## Uso (opcional)
<!-- Cómo correrlo o probarlo: comando, notebook, parámetros nuevos. Para variables de entorno, solo los nombres, nunca los valores. -->
```bash

```

## Resultados (opcional)
<!-- Mediciones, tiempos, métricas, comparaciones antes/después. Las tablas son bienvenidas. -->


## Verificación
<!-- Cómo sabes que funciona. Marca lo que hiciste, quita lo que no aplique y agrega ítems para quien revisa. -->
- [ ] Los tests pasan: <!-- suite, tests nuevos -->
- [ ] Corrido con datos reales: <!-- período, lead, región -->
- [ ] Salidas comparadas contra una referencia: <!-- versión anterior, lectura directa de la fuente, valores conocidos -->
- [ ] Revisor/a:

## Notas para revisión (opcional)
<!-- Riesgos, preguntas abiertas, qué revisar antes de mergear, método de merge si no debe hacerse squash. -->


## Lista de control
- [ ] Sin secretos en código, notebooks, configs ni en esta descripción (las credenciales salen de variables de entorno o `~/.netrc`; el `.env` no se commitea)
- [ ] Sin datos que identifiquen al cliente (nombres de clientes, ubicación de lotes, assets o buckets públicos)
- [ ] Las dependencias nuevas están listadas arriba y fijadas u opcionales
- [ ] README o documentación actualizados si cambió el uso o el comportamiento
- [ ] Los diffs de notebooks son revisables (outputs limpiados o conservados a propósito)
