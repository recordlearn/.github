# .github

Los archivos que GitHub lee para toda la organización. No hay código acá.

| Ruta | Qué es | Dónde se ve |
|---|---|---|
| `profile/README.md` | El perfil público de la org | [github.com/recordlearn](https://github.com/recordlearn) |
| `CONTRIBUTING.md` | Cómo trabajamos: áreas, ramas, revisión, qué es "terminado" | En todo repo que no tenga el suyo |
| `SECURITY.md` | Qué hacer si se filtra una credencial | Pestaña Security de cada repo |
| `CODE_OF_CONDUCT.md` | Cómo nos tratamos | Enlazado en issues y PRs |
| `.github/ISSUE_TEMPLATE/` | Los tres tipos de issue que abrimos | Al crear un issue en cualquier repo |
| `.github/PULL_REQUEST_TEMPLATE.md` | El checklist de todo PR | Al abrir un PR |
| `demo/banner.png` | El banner del perfil, con su prompt al lado | En el perfil |

## Lo que hay que saber

**El perfil es público.** Los repos de la organización son privados, pero `profile/README.md` lo lee cualquiera. Ahí no van proveedores, precios, identificadores de proyecto ni direcciones de servidores.

**Estos archivos son el valor por defecto, no la ley.** Un repo que tenga su propio `CONTRIBUTING.md` usa el suyo. Estos aplican donde no hay nada más específico.

**El banner se regenera, no se edita.** El prompt está en `demo/banner-prompt.txt`, al lado del `.png`.
