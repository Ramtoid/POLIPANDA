# Análisis Web para Recintos de Congresos — Poliforum León

> Documento de trabajo. Recopila todo lo analizado en la sesión: patrones de las mejores webs de recintos del mundo, cómo se detecta (y se mata) el look "hecho con IA", seguridad defensiva, y la auditoría a fondo de poliforumleon.com.mx (SEO, GEO, rendimiento, UX/conversión).
>
> Fecha: 2026-10-03

---

## ⚠️ Nota sobre el alcance

- **Probing de seguridad de terceros = no.** Entrar a webs ajenas a ver "cómo acceder / romper / bloquear" accesos es hacking no autorizado. No se hace. Lo que sí entrego es el enfoque **defensivo**: cómo blindar TU propia web (Poliforum).
- **Límite técnico del entorno:** el proxy de red bloqueó el fetch directo a los sitios (creorama.com, guanajuato.mx, poliforumleon.com.mx y otros). No pude medir en vivo el peso real, los headers ni los Core Web Vitals. Todo lo "medible" viene con la herramienta exacta (gratis) para que lo cierres en minutos sobre tu propio dominio.

---

# BLOQUE 1 — Patrones de las mejores webs de recintos

Referencias de la industria: Venetian Las Vegas (Virtual Planner), Cvent (3D tours), Prismm, Tripleseat Floorplans, Matterport, y recintos tier RAI Ámsterdam / ExCeL / Fira Barcelona.

**Dato que manda la estrategia:** un organizador (planner) evalúa ~3 recintos y revisa ~10 piezas de información *antes* de contactar. Decide en tu web, no contigo.

## Los 8 patrones que convierten

| # | Patrón | Por qué convierte |
|---|--------|-------------------|
| 1 | **Virtual Planner / configurador de espacios** | Eliges sala → la ves en 3D → guardas layout → mandas RFP desde ahí. El lead llega pre-calificado. (Lo hace el Venetian). |
| 2 | **Tour virtual 3D / Matterport "dollhouse"** | Recorrido tipo videojuego. 66% de planners revisan floor diagrams; 50% room diagrams. |
| 3 | **Calculadora de aforo** | 83% miran capacidad primero. Input: # personas + tipo de montaje → output: salas compatibles. Filtro = lead caliente. |
| 4 | **Floor plans interactivos a escala** | Clic en cada sala → m², aforo, specs técnicas (carga eléctrica, altura, muelle de carga). No PDF muerto. |
| 5 | **Mapa de ubicación + logística** | 62% miran dónde estás: aeropuerto, hoteles, estacionamiento. |
| 6 | **Formulario RFP multi-paso** | Paso 1 = nombre+email (captura lead parcial). Pasos siguientes: fecha, aforo, servicios. Menos fricción. |
| 7 | **Galería por tipo de montaje** | La misma sala "como congreso / como gala / como expo". El cliente se visualiza ahí. |
| 8 | **Promesa de respuesta rápida** | "Respondemos en <2h". Más de 24h mata la conversión. El inbound directo cierra >30% vs plataformas terceras. |

## Qué las hace buenas / débiles
- **Buenas:** herramientas interactivas (no catálogo PDF), 3D real, auto-calificación del lead, imágenes por caso de uso.
- **Débiles casi siempre:** carga lenta por el 3D, formularios largos de golpe, falta de prueba social.
- **Oportunidad de magnetismo (LATAM):** nadie hace storytelling. Video de 15s del recinto lleno de energía en el hero. Vende la *sensación del evento exitoso*, no metros cuadrados.

---

# BLOQUE 2 — Cómo se detecta una web hecha con IA (y cómo matar ese look)

## Los tells (lo que la delata)
1. **Meta-tag firmado** — builders como v0, Lovable, Bolt, Base44, Replit se auto-firman en el código fuente o dejan badge "made with".
2. **Parts bin idéntico** — shadcn/ui + primitivas Radix + iconos lucide + paleta default de Tailwind, todo junto sin personalizar = nadie decidió nada a mano.
3. **Abuso de em-dash (—)** y tono corporativo vacío.
4. **Placeholders olvidados** ("Lorem ipsum", "Your Company Here").
5. **Imágenes IA con fallos** — manos raras, texto de fondo mal escrito, poses antinaturales, mismo stock que todos.
6. **Mismo layout template** — hero + 3 cards + CTA genérico idéntico en mil sitios.

## Cómo QUITAR el look IA (checklist anti-genérico)
- Paleta y tipografía propias (no Inter + colores default). 1 color de marca fuerte.
- Fotografía/video REAL del recinto. Una imagen propia vence a 50 generadas.
- Textos con voz humana: anécdotas, nombres de eventos reales, cifras concretas. Humanizar y bajar em-dash.
- Micro-detalles a mano: cursor custom, animación scroll propia, un dato curioso.
- Borrar cualquier badge/meta del builder.

---

# BLOQUE 3 — Seguridad (blindar TU web, no romper ajenas)

Córrelo tú (pasivo, sobre tu dominio):
- `securityheaders.com` → nota A–F de headers
- `ssllabs.com/ssltest` → calidad SSL/TLS
- `observatory.mozilla.org` → scan completo

| Revisar | Fix |
|---|---|
| HTTPS + TLS 1.3, redirección HTTP→HTTPS | Forzar en servidor/CDN; desactivar TLS viejo |
| `HSTS` | Header `Strict-Transport-Security` |
| `Content-Security-Policy` | El más importante vs XSS |
| `X-Content-Type-Options: nosniff` | 1 línea |
| WAF + anti-DDoS | **Cloudflare gratis** = 80% resuelto, y acelera el sitio |
| WordPress | 2FA admin, ocultar `/wp-login`, borrar plugins muertos, todo actualizado |
| Formularios | Honeypot/captcha invisible + rate limiting |

---

# AUDITORÍA A FONDO — poliforumleon.com.mx

## Lo confirmado del sitio

**Mapa real** (URLs limpias y semánticas — bien):
- `/` — Home: "Congresos, convenciones, ferias y exposiciones"
- `/poliforum-leon` — "transformación de un recinto magnífico"
- `/conjunto-poliforum` + `/conjunto-poliforum/area-recreaciones`
- `/recinto/congresos-convenciones` · `/recinto/exposiciones`
- `/historia` · `/servicios-adicionales` · `/alimentos-bebidas`
- `/noticias` + artículos mensuales de agenda

**Activos fuertes:**
- ⭐ **4.7 con 7,851 reseñas en Google** — mayor activo SEO local.
- 📝 **Blog `/noticias` activo** con agenda mensual — buena base SEO.
- 🏗️ 42,000 m², edificios A/B/C, recién remodelado (fachada, vestíbulo, accesos, edificios A y B), 45+ años.
- Datos: salas de 10 a 5,000 personas en una planta, +20 breakouts simultáneos, 4 salas gemelas en edificio C (11 m sin columnas, 4,536 m², carga 5 ton/m²), cocina para banquetes de hasta 7,500.
- Dirección: Blvd. Adolfo López Mateos esq. Blvd. Francisco Villa, Oriental, 37510 León, Gto. Tel +52 477 710 7000.

## 1) Seguridad
Ver BLOQUE 3. No pude escanear headers en vivo → corre `securityheaders.com`, `ssllabs.com/ssltest`, `observatory.mozilla.org`. Mete Cloudflare (seguridad + velocidad).

## 2) SEO — aparecer en Google
Prioridad de arriba a abajo:
1. **Schema markup (JSON-LD)** — CRÍTICO: `EventVenue`/`Place`, `Event` en cada evento (resultados enriquecidos), `Organization`+`LocalBusiness` con las 4.7★.
2. **Landings por intención de búsqueda** (donde está el dinero): "renta de salón para eventos en León", "sede para congresos Guanajuato", "centro de convenciones León", "salón para expo León". Una por keyword de alquiler, no solo páginas institucionales.
3. **Meta titles/descriptions** optimizados por página (verificar; varios parecen genéricos).
4. **`sitemap.xml` + `robots.txt`** en Search Console.
5. **Versión en inglés + `hreflang`** (recibes eventos internacionales: ANPIC, congresos mundiales).
6. **Alt text + nombres de imagen** descriptivos.
7. **Backlinks**: ya enlazan songkick, nferias, tripadvisor, medios. Capitaliza con notas de prensa por evento.

## 3) GEO — aparecer en buscadores de IA (ChatGPT, Gemini, Perplexity, AI Overviews)
Ventaja de primer movimiento; casi nadie lo trabaja:
1. **Contenido pregunta-respuesta**: FAQ real ("¿cuántas personas caben?", "¿qué servicios incluye?", "¿cómo cotizar un congreso?").
2. **Datos concretos citables en texto plano** (no solo imágenes/PDF): m², aforos por montaje, specs de carga.
3. **Schema `FAQPage` + `Event`**.
4. **Consistencia de NAP** (nombre, dirección, teléfono idénticos en todos lados).
5. **Presencia en fuentes que rastrean las IA**: Wikipedia, Wikidata, directorios, prensa.

## 4) Rendimiento / peso
No medible desde aquí → corre `pagespeed.web.dev` y `webpagetest.org`.
Metas 2026: peso home < 2 MB · LCP < 2.5s · CLS < 0.1 · INP < 200ms.
Asesino #1 en recintos: **imágenes sin optimizar** → WebP/AVIF, lazy load, tamaños responsive. Cloudflare como CDN.

## 5) Animaciones / UX / conversión — qué falta vs top mundial

| Falta | Impacto |
|---|---|
| Calculadora de aforo (personas + montaje → salas) | 83% filtran por capacidad |
| Tour 3D / Matterport | 66% revisan planos antes de contactar |
| Planos interactivos por edificio (A/B/C) con m²/aforo/specs | Hoy probablemente texto o PDF |
| Cotizador / RFP multi-paso (paso 1: nombre+email) | Captura leads parciales; responde <2h |
| Galería por tipo de montaje | El cliente se visualiza |
| Prueba social arriba (+45 años · 7,851 reseñas 4.7★ · ANPIC, Feria de León) | Autoridad inmediata |
| Video hero del recinto lleno | Vende la sensación, no m² |
| Micro-animaciones en scroll (reveal, parallax sutil) | Percepción premium, sin matar peso |

## Resumen ejecutivo — qué tiene vs qué falta

**TIENE:** estructura clara · blog activo · GBP 4.7★/7,851 · historia/autoridad · URLs limpias · backlinks de medios.

**FALTA (orden de prioridad para vender más):**
1. Schema markup `Event` + `FAQPage` (SEO + GEO de un golpe)
2. Calculadora de aforo + cotizador RFP multi-paso
3. Landings por keyword de alquiler
4. Tour 3D + planos interactivos
5. Versión en inglés + hreflang
6. Headers de seguridad + Cloudflare
7. Optimización de imágenes (WebP, lazy)
8. Prueba social y video en el hero

---

# PROMPTS Y COMANDOS LISTOS

### Generar la web del recinto (v0 / Lovable / Cursor)
```
Crea una landing para un recinto de congresos y convenciones premium.
NO uses look genérico de IA: paleta de marca propia (un color fuerte + neutros),
tipografía con personalidad, nada de cards default.
Secciones: (1) Hero con video del recinto lleno de energía + CTA "Cotiza tu evento".
(2) Calculadora de aforo: input personas + tipo de montaje (auditorio/banquete/escuela/expo)
→ muestra salas compatibles. (3) Grid de salas: cada una con m², aforo, altura,
specs técnicas y galería por tipo de montaje. (4) Tour 3D embebido (placeholder Matterport).
(5) Formulario RFP MULTI-PASO (paso 1 solo nombre+email). (6) Prueba social:
logos de eventos, cifras "+X congresos", testimonios. (7) Mapa + logística.
Promesa visible: "Respondemos en menos de 2 horas".
Mobile-first, carga rápida, micro-animaciones en scroll.
```

### Headlines magnéticos para el hero
```
Escribe 5 headlines para el hero de un recinto de congresos.
Ángulo: vender el ÉXITO del evento y el prestigio del organizador,
no los metros cuadrados. Tono directo, magnético, memorable.
Máx 8 palabras cada uno. Sin em-dash, sin clichés corporativos.
```

### Auditar si una web parece IA
```
Analiza esta web [URL]. Dime: ¿parece hecha con IA? Lista los tells que encuentres
(meta-tags de builder, componentes default, abuso de em-dash, imágenes genéricas,
layout template). Dame 5 cambios concretos para que se vea hecha a mano por un pro.
```

### Schema de evento (pégalo en cada evento, reemplaza datos)
```html
<script type="application/ld+json">
{"@context":"https://schema.org","@type":"Event",
"name":"ANPIC León 2026","startDate":"2026-10-21","endDate":"2026-10-23",
"eventStatus":"https://schema.org/EventScheduled",
"location":{"@type":"Place","name":"Poliforum León",
"address":"Blvd. Adolfo López Mateos esq. Blvd. Francisco Villa, Oriental, 37510 León, Gto."},
"organizer":{"@type":"Organization","name":"Poliforum León","url":"https://www.poliforumleon.com.mx"}}
</script>
```

### Landing SEO de alquiler
```
Escribe una landing SEO para "renta de salón para congresos en León Gto".
Público: organizadores de eventos. Incluye: H1 con keyword, aforos por montaje,
specs de los edificios A/B/C de Poliforum León (42,000 m²), bloque FAQ con
preguntas reales de búsqueda, CTA "Cotiza en menos de 2 horas". Tono directo,
cifras citables, sin relleno.
```

### Auditar tú mismo en 10 min (pega tu URL)
```
securityheaders.com   → seguridad
ssllabs.com/ssltest   → SSL
pagespeed.web.dev     → velocidad + peso + Core Web Vitals
search.google.com/test/rich-results → si tu schema funciona
```

---

# Para cerrar lo no medible
Pégame cualquiera y lo analizo al detalle:
1. Resultado de **PageSpeed** → diagnóstico de peso/velocidad exacto.
2. **Código fuente del home** (Ctrl+U) → meta tags, schema, CMS, scripts, look-IA real.
3. Reporte de **securityheaders.com** → priorizo los fixes.

O construyo el **prototipo de la web mejorada** (calculadora de aforo + RFP + schema + estructura anti-IA).

---

# Fuentes
- https://www.poliforumleon.com.mx/
- https://www.poliforumleon.com.mx/recinto/congresos-convenciones
- https://www.poliforumleon.com.mx/noticias
- https://www.poliforumleon.com.mx/historia
- Google (4.7★ / 7,851): https://www.google.com.mx/travel/hotels/entity/ChoIttKJrID-0_CHARoNL2cvMTFweHNiM3M3bhAE
- https://sic.cultura.gob.mx/ficha.php?table=auditorio&table_id=806
- https://eventosleongto.com/recintos/poliforum-leon/
- Venetian Virtual Planner: https://www.venetianlasvegas.com/meetings/planning/virtual-planner.html
- Cvent 3D Tours: https://www.cvent.com/en/supplier-venue/3d-virtual-tour-software
- Prismm: https://www.prismm.com/solutions/event-design-software/floor-planning-software-venues-planners-vendors
- Cvent conversión: https://www.cvent.com/en/blog/hospitality/hotel-website-conversions
- Amadeus booking conversion: https://www.amadeus-hospitality.com/insight/improve-website-booking-conversion/
- Detectar webs IA: https://aiwebsitedetector.net/blog/signs-a-website-was-built-by-ai
- Originality.ai: https://originality.ai/blog/how-to-identify-ai-generated-websites
- Guía seguridad web 2025: https://beaglesecurity.com/blog/article/guide-to-web-server-security.html
- Website hardening: https://www.siteguarding.com/security-blog/the-complete-guide-to-website-hardening-protect-your-site-from-cyber-threats/
