# Cómo trabajamos

Somos tres y el sistema tiene más partes que personas. Esto es lo que evita que nos pisemos.

---

## La única regla que importa

**Nadie depende del código de nadie. Todos dependemos del contrato.**

El contrato es el esquema de la base más las convenciones que lo rodean, y vive en [`plataforma/spec`](https://github.com/recordlearn/plataforma/tree/main/spec). De ahí se **generan** los tipos que consume cada cliente.

De esa regla salen dos consecuencias prácticas:

1. Ninguna app importa código de otra app. Ni una función, ni un tipo, ni una constante. Si necesitás algo de otra área, o está en el contrato o hay que ponerlo en el contrato.
2. Los tipos generados **no se editan a mano**. Si abriste `packages/contrato` para arreglar algo, el problema está en el esquema.

Suena rígido. Es lo que hace que puedas trabajar un martes entero sin escribirle a nadie.

---

## Quién es dueño de qué

Ser dueño de un área significa dos cosas: **decidís cómo se hace por dentro**, y **revisás lo que otro toque ahí**.

| Área | Dueño | Decide |
|---|---|---|
| `spec/` | **los tres** | Nada entra sin tres aprobaciones |
| `db/` | **José Antonio** | Esquema, RLS, migraciones, seed, auth |
| `apps/worker/` | **Said** | Pipeline, prompts, modelos, reintentos, costes |
| `apps/mobile/`, `apps/web/` | **Mateo** | Clientes, estado local, offline, UI |
| `packages/contrato/` | **generado** | Nadie. Sale del esquema |

Lo aplica `CODEOWNERS`, no la buena voluntad. Si tocás el área de otro, GitHub le pide la revisión solo.

### Cómo se ve una dependencia real

Lo que **no** es una dependencia: "necesito que José cree la tabla para empezar". Podés correr las migraciones vos, en tu máquina, hoy.

Lo que **sí** es una dependencia: "necesito una columna que todavía no existe en el contrato". Eso es un [cambio de contrato](https://github.com/recordlearn/plataforma/issues/new?template=01-cambio-de-spec.yml), lo revisamos los tres, y mientras tanto seguís con otra cosa.

---

## Trabajar sin esperar a nadie

Cada uno puede levantar **el sistema entero** en su máquina. No hay un entorno compartido del que dependa tu tarde.

```bash
supabase start          # Postgres + Auth + Storage, desde db/migraciones
supabase db reset       # aplica migraciones y carga db/seed.sql
```

El seed no es decorativo: trae un usuario conocido, una clase, y **tomas en cada estado — incluida una fallada**. Eso es lo que te deja dibujar la pantalla de error sin pedirle a nadie que rompa algo a mano.

Si necesitás probar contra algo remoto sin tocar lo de los demás, usá una **rama de base de datos**. Son efímeras y son tuyas.

### Y si lo que necesitás todavía no existe

Cada puerto del contrato tiene un **doble en memoria**. Se comporta como el real, no habla con la red, y sirve para construir contra algo antes de que ese algo exista.

Es cómo Said arma el worker sin tablas y cómo Mateo arma pantallas sin worker.

---

## Ramas y commits

Ramas: `área/lo-que-hace`.

```
db/tablas-de-entitlement
worker/claim-atomico
mobile/cola-en-disco
spec/origen-de-la-toma
```

Los commits dicen **qué cambia para quien usa el sistema**, no qué archivos tocaste.

```
✅ fix: una toma que falla por red vuelve a la cola en vez de morir
✅ feat: el worker reclama las tomas colgadas de un worker muerto
❌ fix: worker.py
❌ cambios varios
❌ wip
```

Si no podés escribir el commit sin la palabra "varios", son dos commits.

---

## Qué significa "terminado"

Un issue no se cierra porque el código esté escrito. Se cierra cuando **alguien más puede verificarlo sin preguntarte nada**.

Por eso todo issue de trabajo lleva un criterio observable. "Que funcione" no es criterio. Esto sí:

> El worker levanta una toma en `recorded`, la deja en `done`, y `pytest -q` pasa.

En el PR va **el comando que corriste y lo que devolvió**. Pegado, no descrito.

---

## Revisión

- **Tu área, cambio interno:** una aprobación. La de quien tenga tiempo.
- **Área de otro:** la aprobación del dueño. GitHub la pide solo.
- **`spec/` o `db/`:** los tres. Sin excepción, y sin "después lo miro".

Revisar no es buscar errores de estilo — eso lo hace el linter. Es responder una pregunta: **¿esto le va a romper algo a alguien dentro de dos semanas?**

---

## Lo que nunca entra en un commit

- Claves, tokens, `service_role`, cadenas de conexión.
- IPs de servidores, identificadores de proyecto, rutas de infraestructura.
- Audio o transcripciones de una clase real. Es la voz de un profesor que no eligió estar en un repo.

Los `.env` viven fuera del árbol y cada repo trae su `.env.example` con los nombres y sin los valores.

Si algo de esto se te escapó: **avisá antes de arreglarlo**. Rotar una clave filtrada es rápido; descubrirla en tres meses no.

---

## El dinero cambia las reglas

Todo lo que **cuesta plata** o **otorga acceso** pasa por el servidor. Sin excepciones.

El cliente pide y el servidor decide. Nunca al revés, porque el cliente corre en un teléfono que no controlamos:

- La duración que declara el cliente **no es la que se cobra**. La real la reporta el proveedor, y solo el worker la ve.
- El plan de una cuenta es de **solo lectura** para el cliente. Si un `PATCH` puede ascenderte a Pro, no hay producto.

Todo lo demás —leer tus clases, subir el audio, editar tu propio apunte— sigue yendo directo. Esa parte está bien resuelta y no la vamos a romper por simetría.

---

## Cuando algo no está definido

Preguntá antes de inventar. Una decisión tomada solo, que después hay que deshacer en tres repos, cuesta más que el mensaje que no mandaste.

Y cuando la respuesta valga para el futuro, no la dejes en el chat: **escribila como decisión** en `docs/adr/`. Corta, con la evidencia que la respalda. Es lo que nos va a evitar volver a discutirla en noviembre.
