---
name: multiagente
description: El equipo de 8 agentes de Claude Code que monta una web entera a la vez, cada uno experto en lo suyo - SEO, Copy, Imágenes, Diseño, Código, Reservas (o contacto), Velocidad y Revisión. Claude Code reparte el trabajo entre subagentes que trabajan en paralelo sobre el mismo proyecto y el de Revisión comprueba que todo encaja antes de enseñarla. Sirve para llegar a la llamada con la web del negocio ya hecha. Úsala cuando digan /multiagente, «comenta MULTIAGENTE», «el equipo de agentes», «8 agentes montando una web», «monta la web con agentes» o pasen la web o el Instagram de un negocio para hacerle una web nueva.
---

# /multiagente: 8 agentes montando una web a la vez

Al terminar, el usuario tiene la web del negocio funcionando en local (y, si quiere, publicada en Vercel), hecha por
8 subagentes en paralelo. Habla en español de España, cercano y corto. Una pregunta cada vez.
**Nunca publiques ni envíes nada sin que el usuario lo diga.**

## Paso 0. Los agentes
Comprueba que existen en `~/.claude/agents/` los 8 archivos de esta skill (`web-seo.md`, `web-copy.md`, `web-imagenes.md`,
`web-diseno.md`, `web-codigo.md`, `web-reservas.md`, `web-velocidad.md`, `web-revision.md`). Si faltan, cópialos desde
la carpeta `agents/` de esta skill: `cp ~/.claude/skills/multiagente/agents/*.md ~/.claude/agents/`. Pide reiniciar
Claude Code si acabas de copiarlos.

## Paso 1. El brief (4 preguntas, una a una)
1. La web o el Instagram del negocio (o su nombre y ciudad). Léelos tú: qué venden, a quién, tono, colores, opiniones reales.
2. Qué tiene que conseguir la web: reservas, llamadas, presupuestos, ventas…
3. Fotos: ¿tiene fotos propias (carpeta o enlace)? Si no, usa las de su web/Instagram con permiso o deja huecos marcados.
   **Nunca inventes opiniones, precios ni datos**: si no los tienes, deja un marcador `[[pendiente: …]]`.
4. Estilo: enséñale 2 webs de referencia del sector y que elija.

Guarda el brief en `~/Webs/<negocio>/BRIEF.md`.

## Paso 2. El esqueleto (tú, antes de repartir)
Crea el proyecto en `~/Webs/<negocio>/` (Next.js o HTML estático, lo que el usuario prefiera; por defecto HTML + CSS
en un solo `index.html` con secciones). Escribe `PLAN.md` con las secciones (cabecera, portada, servicios/carta,
sobre nosotros, opiniones, reservas/contacto, pie) y qué agente toca cada una. Cada agente solo edita sus zonas para
no pisarse: usa comentarios `<!-- zona:copy -->` / archivos separados (`textos.json`, `estilos.css`, `img/`, `seo.html`).

## Paso 3. Repartir en paralelo
Lanza los 8 subagentes **a la vez** (en un único mensaje con 8 llamadas a la herramienta Task/Agent), cada uno con
el `BRIEF.md`, el `PLAN.md` y su zona:

| Agente | Hace |
|---|---|
| web-seo | título, meta description, H1/H2, schema (LocalBusiness/Restaurant…), sitemap y textos alternativos |
| web-copy | todos los textos con la voz del negocio, sin inventar datos |
| web-imagenes | escoge, recorta y coloca las fotos (WebP, tamaños, `alt` con el SEO) |
| web-diseno | paleta, tipografías, espaciados y componentes; que no parezca hecha con IA |
| web-codigo | estructura, responsive, accesibilidad y que todo compile |
| web-reservas | formulario o botón de reservas/contacto (WhatsApp, email, Calendly…) que funcione |
| web-velocidad | carga rápida: imágenes ligeras, lazy load, nada que bloquee; mide con Lighthouse si está |
| web-revision | al final: revisa todo contra el brief, enlaces, móvil y escritorio, faltas y datos inventados |

Primero los 7 primeros en paralelo; cuando acaben, `web-revision`. Si Revisión encuentra fallos, reenvía cada fallo
al agente responsable y vuelve a revisar.

## Paso 4. Enseñarla
Ábrela en local (`npx serve` o `python3 -m http.server`) y saca capturas en móvil y escritorio. Lista los
`[[pendiente: …]]` que quedan. Cambios que pida: pásalos al agente de esa zona.

## Paso 5. Publicar (solo si lo pide)
`vercel --prod` (o Netlify/Cloudflare Pages). Dale el enlace. Idea para vender: llega a la llamada con la web hecha.
