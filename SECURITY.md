# Seguridad

## Si se filtró una credencial

Pasa. Lo que importa es qué hacés en los primeros diez minutos.

**Avisá primero, arreglá después.** Un `git commit --amend` no borra nada: si la clave llegó a GitHub, ya está en el historial, en los forks y posiblemente en el índice de alguien. Reescribir la historia antes de rotar la clave solo hace que nadie sepa qué se filtró.

El orden es:

1. **Decilo en el grupo.** Qué clave, en qué commit, desde cuándo.
2. **Rotala.** En el panel del proveedor. La vieja deja de valer y el problema se termina ahí.
3. **Recién ahora** limpiá el repo.

Rotar una clave son dos minutos. Descubrir en noviembre que estuvo expuesta desde agosto no tiene arreglo.

## Lo que más nos puede doler

**La clave de servicio en un cliente.** Salta todas las políticas por fila. Si llega a un bundle de la app móvil o al JavaScript del dashboard, cualquiera con el APK lee el audio de todos los usuarios. Es el único error de esta arquitectura que no tiene arreglo después de publicar: el bundle ya está en los teléfonos.

Los clientes llevan la clave pública. Siempre.

**Audio de clases reales en el repo.** Es la voz de un profesor que no eligió estar acá. No va en un commit, ni en un issue, ni en una captura.

## Reportar algo desde afuera

Todavía no tenemos usuarios, así que no hay un programa formal. Si encontraste algo, abrí un issue **sin el exploit**: describí la clase de problema y esperá a que te contestemos para los detalles.
