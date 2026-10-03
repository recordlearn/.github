## Qué cambia

<!-- Una o dos frases. Qué hace el sistema ahora que antes no hacía. -->

<!-- En inglés a propósito: GitHub sólo cierra la issue con «Closes». «Cierra» no cierra nada. -->

Closes #

## Área

<!-- Marcá solo las que tocás. Si marcás `spec` o `recordlearn/DB`, avisá en el chat del equipo y esperá el OK de los tres antes de mergear. -->

- [ ] `spec` — el contrato compartido
- [ ] `apps/worker`
- [ ] `apps/mobile`
- [ ] `apps/web`
- [ ] `packages/contrato` (¿generado o escrito a mano? si es a mano, algo está mal)
- [ ] `recordlearn/DB` — esquema, migraciones, RLS
- [ ] `obsidian` — el plugin

## Cómo lo probaste

<!-- El comando que corriste y lo que devolvió. No "lo probé y anda". -->

```
```

## Checklist

- [ ] No importo código de otra app. Solo de `packages/*`.
- [ ] Si dependo de un cambio de esquema, ya entró en `DB` y llegó por el PR de `sincronizar-tipos`.
- [ ] Si agregué algo que cuesta plata, pasa por el servidor y no por el cliente.
- [ ] No hay claves, tokens ni IPs en el diff.
