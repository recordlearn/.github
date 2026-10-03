<!-- Público: lo lee cualquiera. Nada de proveedores, precios, identificadores de proyecto ni direcciones de servidores. -->
<div align="center">

<img src="https://raw.githubusercontent.com/recordlearn/.github/main/demo/banner.png" alt="recordlearn — de la voz en el aula al apunte que sirve: audio grabado en clase que se transcribe, se resume y se convierte en apuntes enlazados" width="100%"/>

**Grabás la clase y seguís atendiendo. Al salir tenés la transcripción, el resumen y los apuntes enlazados esperándote donde ya estudiás.**

<br/>

<table>
<tr>
<td align="center"><strong>3</strong><br/><sub>superficies</sub></td>
<td align="center"><strong>2</strong><br/><sub>flujos</sub></td>
<td align="center"><strong>3</strong><br/><sub>personas</sub></td>
<td align="center"><strong>1</strong><br/><sub>contrato</sub></td>
</tr>
</table>

</div>

---

## El problema

En una clase de dos horas no se puede hacer las dos cosas. O escuchás y entendés, o escribís y copiás. Quien toma apuntes buenos se pierde la explicación; quien atiende se queda sin registro.

La grabadora del teléfono no lo resuelve: cambia un problema por otro. Ahora tenés 47 archivos de audio que nunca vas a volver a escuchar, con nombres como `Nueva grabación 12`.

Transcribir con IA tampoco alcanza. Una transcripción cruda de dos horas son 18.000 palabras sin estructura — es la clase otra vez, igual de larga, y ahora sin la cara del profesor explicando cuál era la parte importante.

## Qué estamos construyendo

Un ecosistema donde el audio de una clase termina siendo **material de estudio real**, en la herramienta donde ya trabajás, sin que tengas que mover un archivo.

```
   grabar  ──>  transcribir  ──>  entender  ──>  apuntes que te sirven
     │                                                    │
  el teléfono en el bolsillo                     en Obsidian, con su grafo,
                                                 sus conceptos enlazados
                                                 y sus tarjetas de repaso
```

Tres superficies, cada una con un trabajo:

| Superficie | Para qué | Estado |
|---|---|---|
| **App móvil** | Grabar la clase y ver cómo avanza el procesamiento | Funciona, en pruebas |
| **Dashboard web** | Ver todo: transcripciones, resúmenes, apuntes, uso | Funciona, en pruebas |
| **Plugin de Obsidian** | Bajar los apuntes a tu vault, con el grafo ya armado | Funciona, sin publicar |

## Dos flujos, no uno

**El diferido.** Grabás, subís, y el sistema trabaja mientras vos hacés otra cosa. Al rato están la transcripción, el resumen y la nota. Es el flujo que ya funciona.

**El de en vivo.** La clase se escucha mientras ocurre. A medida que avanza van apareciendo los conceptos, las tarjetas de repaso, y las preguntas que el profesor tiró al aire.

Ese segundo flujo es el que nos interesa de verdad, y tiene un caso de uso muy concreto: **el profesor pregunta algo, vos no estabas atento, y la app sí.** Escuchó, transcribió, entendió la pregunta y te muestra la respuesta para que **vos** contestes.

No queremos que hable por vos. Solo que sepas qué decir.

## La regla que gobierna todo: nada de alucinaciones

Un apunte inventado es peor que no tener apunte. Si el modelo cita una fuente que el profesor nunca mencionó, el estudiante se lo lleva al examen y pierde puntos por confiar en nosotros.

Cuando medimos modelos para esto, el hallazgo fue incómodo: **los modelos más capaces alucinaron más.** El que más mundo tiene adentro es el que más contamina un apunte con cosas que en esa clase nunca se dijeron.

Por eso la fidelidad es una guarda: un modelo que inventa queda fuera, por más capaz o barato que sea. Entre los que pasan, elegimos por costo.

## Dónde está cada cosa

Cuatro repositorios activos, pero **sólo dos son el producto**. Si venís llegando, entrá por ahí.

```
                    EL PRODUCTO
   ┌──────────────────────────────────────────────┐
   │                                              │
   │   DB                    plataforma           │
   │   la base de datos      el contrato,         │
   │                         el worker            │
   │        │                y las dos apps       │
   │        └───── genera ──────> los tipos       │
   │                                              │
   └──────────────────────────────────────────────┘

              obsidian           el plugin
              .github            esta portada y las plantillas
```

| Repositorio | Qué hay adentro | Dueño |
|---|---|---|
| **`DB`** | El esquema, las migraciones, las políticas de acceso y el almacenamiento. De acá salen los tipos que consumen todos los clientes | José Antonio |
| **`plataforma`** | `spec/` el contrato · `apps/worker/` el pipeline · `apps/mobile/` la app · `apps/web/` el dashboard | los tres |
| **`obsidian`** | El plugin que baja los apuntes al vault. Privado hasta publicar la primera versión | Mateo |
| **`.github`** | Esta portada y las plantillas de issues y pull requests | los tres |

### Por dónde empezar

| Si venís a… | Entrá por |
|---|---|
| entender **qué se puede guardar y quién lo puede leer** | `DB` → `README.md` |
| escribir **código nuevo** de cualquier área | `plataforma` → `spec/` |
| saber **por qué el sistema es así y no de la forma obvia** | `plataforma` → `docs/adr/` |
| saber **qué toca ahora** | `plataforma` → `docs/etapas.md` |
| ver **los números** detrás de la elección de modelo | `plataforma` → `docs/experimentos/` |

---

## Cómo trabajamos

Somos tres, y ninguno puede avanzar solo si cada uno inventa su propia versión de la verdad. Así que hay **un solo contrato** —el esquema de datos y las convenciones que lo rodean— y todo lo demás se deriva de ahí:

- Los tipos del cliente se **generan** del esquema. No se escriben a mano.
- Cada uno puede levantar el sistema entero en su máquina y trabajar sin esperar a nadie.
- Cambiar el contrato es un pull request que revisan los tres. Es la única fricción, y está donde tiene que estar.

Lo escribimos primero, lo implementamos después, y el spec evoluciona con el proyecto en vez de quedar viejo en la segunda semana.

## Estado

**Funciona de punta a punta en un entorno de pruebas**: grabar, subir, transcribir, resumir y bajar los apuntes al vault. Falta el cobro para abrirlo a usuarios.

El MVP con el que empezamos está archivado (`recordlearn`): demostró la idea y no es fuente de verdad de nada.

---

<div align="center">
<sub>Mateo · Said · José Antonio</sub>
</div>
