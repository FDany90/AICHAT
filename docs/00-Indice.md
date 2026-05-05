# Índice de Documentación — Proyecto AI Companion

> Documento maestro que lista todos los documentos del proyecto, su orden y propósito.
> Última actualización: 2026-05-04
> Owner: Daniel Fernández

---

## Cómo leer este índice

- ✅ **Hecho** — documento creado y completado (puede seguir vivo, pero está listo para usar)
- 🟡 **En curso** — documento en proceso de redacción
- ⬜ **Pendiente** — documento no iniciado aún
- 🔮 **Futuro** — para fase post-lanzamiento, no urgente

Numeración por bloques:
- **00-09**: Índice y estrategia
- **10-19**: Producto y diseño
- **20-29**: Arquitectura y desarrollo
- **30-39**: Lanzamiento, crecimiento y operación

---

## 📘 Bloque 1 — Estrategia (00-09)

### ✅ 00 — Índice (este documento)
Mapa maestro de toda la documentación.

### ✅ 01 — Modelo de Negocio
Visión, posicionamiento, segmentos, diferenciadores, monetización, simulación de costes y proyección de ingresos. Documento estratégico de referencia.
→ [01-Modelo-de-Negocio.md](01-Modelo-de-Negocio.md)

### ⬜ 02 — Marca e Identidad Visual
Nombre de marca, dominio, tagline, paleta de colores, tipografía, logo, tono de voz. Lo que el usuario ve y siente al primer contacto.

### ⬜ 03 — Análisis Competitivo Detallado
Estudio a fondo de qkkie, Character.AI, Talkie, Replika, Chai, Janitor, Candy.AI. UX, monetización, onboarding, paywalls, calidad de personajes. Decisiones de "qué copiar / qué evitar / dónde diferenciarnos".

---

## 🎨 Bloque 2 — Producto y Diseño (10-19)

### ⬜ 10 — Diseño de Personajes
Arquetipos, biografías, personalidades, voz propia, prompt completo de cada personaje, mood states, fechas/eventos personales, fotos requeridas. **5-8 personajes para lanzamiento**, plantilla replicable para los siguientes. Documento crítico — la calidad del producto depende de aquí.

### ⬜ 11 — Diseño de Producto y UX
Flujos de usuario completos: onboarding, primera conversación, paywall, compra de créditos, suscripción, gestión de cuenta, galería, perfil de personaje. Wireframes o mockups por pantalla. Decisiones de copy.

### ⬜ 12 — Sistema de Diseño y Componentes
Componentes de UI reutilizables (botones, cards, modal, chat bubble, etc.), tokens de diseño (colores, espaciados, tipografías), iconografía. Base para construir rápido y consistente.

### ⬜ 13 — Estrategia de Imágenes
Cómo se generan, organizan y sirven. Cuántas fotos por personaje, qué variedad (ropa, escenarios, mood), workflow de generación en Promptchan, sistema de tags, qué fotos van en galería visible vs desbloqueable, tamaños y formatos.

---

## ⚙️ Bloque 3 — Arquitectura y Desarrollo (20-29)

### ⬜ 20 — Arquitectura Técnica General
Stack final, diagrama de componentes, flujos de datos, decisiones de hosting, observabilidad, seguridad, escalado. Documento de referencia técnica del sistema entero.

### ⬜ 21 — Esquema de Base de Datos
Tablas, columnas, relaciones, índices, restricciones, políticas RLS de Supabase. Modelo de datos completo: usuarios, personajes, conversaciones, mensajes, memoria, créditos, suscripciones.

### ⬜ 22 — Motor de Conversación y Prompt Engineering
Cómo se construye el system prompt para cada llamada al LLM. Estructura: contexto del personaje + mood actual + memoria recuperada + vida del día + últimos mensajes + instrucciones especiales. Templates y ejemplos. Estrategia de prompt caching.

### ⬜ 23 — Sistema de Memoria
Diseño del RAG: qué se guarda, cómo se resume, cómo se recupera, qué embedding model, jerarquía (memoria a corto / medio / largo plazo), gestión de "hechos sobre el usuario" vs "narrativa de relación", política de borrado/edición.

### ⬜ 24 — Sistema de Mood e Inteligencia Emocional
Máquina de estados de mood del personaje, clasificador del mood del usuario, transiciones, cómo afecta al prompt, modo apoyo automático, detección de crisis. Diferenciador estratégico #3.

### ⬜ 25 — Sistema de Vida Propia y Mensajes Proactivos
Cron job nocturno, generación de "día simulado" por personaje, almacenamiento como memoria, cuándo se mencionan en conversación, lógica de mensajes proactivos (cuándo, qué, a quién). Diferenciador estratégico #2.

### ⬜ 26 — Pipeline de Mensajes (Cola, Delay, Splitter)
Cómo se procesa un mensaje: validación → encolado → procesamiento → trozeado → emisión con delay realista. Implementación con Redis. Estrategia de prioridad (paying > free).

### ⬜ 27 — Sistema de Monetización
Implementación técnica: integración Lemon Squeezy, webhooks, gestión de créditos, suscripciones, paywalls, gestión de cuotas, periodos gratis, recuperación de pagos fallidos.

### ⬜ 28 — Sistema de Moderación y Anti-abuso
Filtro previo de mensajes (jailbreaks, contenido ilegal, intentos de extraer prompt), rate limiting, detección de bots/scraping, gestión de usuarios problemáticos, política de baneos.

### ⬜ 29 — Internacionalización (i18n)
Estructura de traducciones, detección de idioma, fallbacks, gestión de copy con react-i18next o similar. Cómo se mantiene UI en ES + EN sin duplicar trabajo.

---

## 🚀 Bloque 4 — Legal, Lanzamiento y Crecimiento (30-39)

### ⬜ 30 — Legal y Compliance
Terms of Service, Privacy Policy, AI Disclosure, política de cookies, política de retención de datos, GDPR, EU AI Act, verificación 18+, política DMCA, políticas de uso aceptable del usuario. Plantillas adaptadas.

### ⬜ 31 — Plan de Desarrollo MVP
Sprints semana a semana (12 semanas), tareas concretas, dependencias, criterios de "hecho". Convertir el roadmap del modelo de negocio en un plan ejecutable.

### ⬜ 32 — Plan de Lanzamiento
Estrategia beta cerrada → beta abierta → lanzamiento público. Checklist de pre-lanzamiento (legal, infra, contenido, soporte). Cómo se gestionan los primeros 50-100 usuarios beta. Métricas a vigilar.

### ⬜ 33 — Plan de Adquisición y Crecimiento
Cómo conseguir los primeros 100, 1.000, 10.000 usuarios sin presupuesto de ads. Canales: Reddit, TikTok, SEO, partnerships, contenido viral. Plan editorial. Estrategia de referidos.

### ⬜ 34 — KPIs y Analítica
Qué se mide desde día 1, herramientas (Posthog, Mixpanel), eventos clave, embudos de conversión, dashboards. Definición de "éxito" en cada fase.

### ⬜ 35 — Operaciones, Soporte y Moderación Humana
Cómo se atiende al usuario (email, formulario, chat), tiempos de respuesta objetivo, FAQ, gestión de incidencias, escalado ante crisis (usuario en riesgo, demanda legal, problema técnico).

---

## 🔮 Bloque 5 — Post-MVP (40+)

### 🔮 40 — Roadmap Post-MVP
Features que no entran en MVP pero están en pipeline: voz en producción, app móvil nativa, llamadas de voz, generación de imagen on-demand, vídeo, multi-personaje, marketplace.

### 🔮 41 — Plan de Internacionalización Avanzada
Más allá de ES+EN: portugués, francés, italiano, alemán, árabe. Localización cultural de personajes (no solo traducción).

### 🔮 42 — Plan de Optimización de Coste LLM
Caching avanzado, fine-tuning de modelos propios, evaluación de proveedores alternativos (Together, Fireworks, self-hosted), reducción del coste por mensaje a la mitad.

### 🔮 43 — Estrategia de Monetización Avanzada
Más allá de freemium + créditos: tier "creator" donde usuarios crean su personaje, tipping virtual, contenido exclusivo de creators, marketplace.

### 🔮 44 — Plan de Salida / Escalado
Cuando el proyecto valide product-market fit: contratación, levantamiento de capital o bootstrap agresivo, expansión geográfica, posibles partnerships estratégicos.

---

## 📋 Estado actual de la documentación

| Estado | Cantidad |
|---|---|
| ✅ Hecho | 2 |
| 🟡 En curso | 0 |
| ⬜ Pendiente (MVP) | 18 |
| 🔮 Futuro (post-MVP) | 5 |
| **Total** | **25** |

---

## 🎯 Próximo documento sugerido

**10 — Diseño de Personajes**

Razón: ya tenemos modelo de negocio, posicionamiento y arquitectura conceptual. El siguiente bloqueante es **definir los personajes**, porque:
- Son la cara visible del producto
- Sus prompts son la base técnica del motor de IA
- Las imágenes a generar dependen de cómo sean los personajes
- El tono y voz de la marca se calibra a partir de ellos

Alternativas viables como "siguiente":
- **02 — Marca e Identidad** (si quieres cerrar el nombre/dominio antes)
- **03 — Análisis Competitivo Detallado** (si quieres más datos antes de diseñar)
- **11 — Diseño de Producto y UX** (si prefieres pensar primero en flujos)
