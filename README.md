# Multiagente · 8 agentes de Claude montando una web

La skill de Claude Code con el equipo de 8 subagentes que monta la web de un negocio a la vez, cada uno experto en lo suyo.

| Agente | Qué hace |
|---|---|
| SEO | título, meta description, H1/H2, schema y textos alternativos |
| Copy | todos los textos con la voz del negocio |
| Imágenes | elige, recorta, optimiza y coloca las fotos |
| Diseño | paleta, tipografías, espaciados y componentes |
| Código | estructura, responsive, accesibilidad |
| Reservas | formulario o botón de reservas/contacto que funciona |
| Velocidad | que cargue rápido (WebP, lazy load, Lighthouse) |
| Revisión | lo revisa todo al final y devuelve cada fallo a su responsable |

Claude Code reparte el trabajo entre los subagentes, trabajan en paralelo y el de Revisión comprueba que todo encaja.

Hecho por Denís Corral · [@deniscorralvillarraso](https://instagram.com/deniscorralvillarraso) · [Sell Your AI](https://sellyourai.io)

## Instalación

```bash
git clone https://github.com/deniscorral3am/multiagente-skill ~/.claude/skills/multiagente
mkdir -p ~/.claude/agents && cp ~/.claude/skills/multiagente/agents/*.md ~/.claude/agents/
```

Reinicia Claude Code y escribe `/multiagente`. Te pedirá la web o el Instagram del negocio y monta la web con los 8 agentes.

## Licencia

MIT
