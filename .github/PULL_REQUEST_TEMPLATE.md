## Qué cambia

<!-- Una o dos frases. Qué hace el sistema ahora que antes no hacía. -->

Cierra #

## Área

<!-- Marcá solo las que tocás. Si marcás `spec`, esto lo revisamos los tres. -->

- [ ] `spec` — el contrato compartido
- [ ] `apps/worker`
- [ ] `apps/mobile`
- [ ] `apps/web`
- [ ] `packages/contrato` (¿generado o escrito a mano? si es a mano, algo está mal)

## Cómo lo probaste

<!-- El comando que corriste y lo que devolvió. No "lo probé y anda". -->

```
```

## Checklist

- [ ] No importo código de otra app. Solo de `packages/*`.
- [ ] Si dependo de un cambio de esquema, ya entró en `DB` y llegó por el PR de `sincronizar-tipos`.
- [ ] Si agregué algo que cuesta plata, pasa por el servidor y no por el cliente.
- [ ] No hay claves, tokens ni IPs en el diff.
