# Modelo de Negocio — Plataforma AI Companion

> **Documento vivo**. Última actualización: 2026-05-04
> Owner: Daniel Fernández
> Estado: Fase de definición estratégica (pre-desarrollo)

---

## 0. Glosario rápido

| Sigla | Significado |
|---|---|
| **AI / IA** | Artificial Intelligence / Inteligencia Artificial |
| **API** | Application Programming Interface (interfaz para llamar servicios) |
| **ARPU** | Average Revenue Per User (ingreso medio por usuario) |
| **AUP** | Acceptable Use Policy (política de uso de un servicio) |
| **CDN** | Content Delivery Network (red para servir archivos rápido) |
| **DAU** | Daily Active Users (usuarios activos diarios) |
| **KYC** | Know Your Customer (verificación de identidad) |
| **LLM** | Large Language Model (modelo de IA generativa de texto) |
| **LTV** | Lifetime Value (valor total que aporta un usuario en su vida útil) |
| **MAU** | Monthly Active Users (usuarios activos mensuales) |
| **MRR** | Monthly Recurring Revenue (ingreso recurrente mensual) |
| **MVP** | Minimum Viable Product (producto mínimo viable) |
| **MoR** | Merchant of Record (intermediario que asume rol de vendedor) |
| **NSFW / SFW** | Not / Safe For Work (contenido sexual / no sexual) |
| **PWA** | Progressive Web App (web instalable como app) |
| **RAG** | Retrieval-Augmented Generation (LLM consulta memoria antes de responder) |
| **ToS** | Terms of Service (términos del servicio) |
| **2257** | Sección 18 USC 2257 — ley EE.UU. que exige guardar prueba de edad de modelos en contenido sexual |

---

## 1. Resumen ejecutivo

Plataforma web (con roadmap a PWA y móvil) donde usuarios chatean con personajes femeninos generados por IA. **SFW soft** (flirteo, sensualidad, lencería/bikini desbloqueables — sin contenido sexual explícito). **Mercado objetivo**: inglés global + español (sin coste extra al usar Claude). **Posicionamiento**: character-first con ambigüedad respetuosa (la IA confirma serlo si se le pregunta, no se vende prominentemente como "AI Companion", la marca se centra en la experiencia y los personajes).

**Diferenciadores clave**:
1. Memoria profunda de calidad (recuerda al usuario semanas/meses)
2. "Vida propia" entre conversaciones (días simulados que afectan a la conversación)
3. Inteligencia emocional (detecta mood del usuario y reacciona)

**Stack técnico previsto**: Next.js + Supabase + Upstash + Vercel + Cloudflare R2 + Claude (Haiku 4.5 default, Sonnet 4.6 premium).

**Monetización**: Freemium con créditos + suscripción.

**Pago**: Lemon Squeezy (Merchant of Record, gestiona impuestos globales).

**Presupuesto inicial**: $200-300.

**Equipo**: solo dev (Daniel).

> 📌 **La decisión SFW vs NSFW está justificada en detalle en la Sección 2**. Es la decisión más importante del proyecto y afecta a procesador de pago, proveedor de LLM, distribución, marketing, legal y mercado total disponible.

---

## 2. Decisión SFW vs NSFW (decisión fundacional)

> **TL;DR**: SFW soft en V1. NSFW como V2 separada queda como posibilidad **post-validación de mercado**, no antes.

### 2.1 Por qué esta decisión es fundacional

La decisión sobre el nivel de contenido **no es una decisión de producto, es la decisión que define la viabilidad del proyecto**. Afecta a:

- **Qué procesador de pago puedes usar** (y cuánto te cuesta)
- **Qué LLM puedes usar** (y por tanto qué calidad de conversación das)
- **Si puedes lanzar app móvil** (App Store / Play Store)
- **Qué canales de marketing tienes disponibles**
- **El tamaño total del mercado al que apuntas**
- **Tu exposición legal y regulatoria**
- **El estigma o legitimidad de tu marca**

Por eso se documenta primero, antes de cualquier otra decisión.

### 2.2 Comparativa exhaustiva SFW vs NSFW

#### 2.2.1 Procesadores de pago

| Procesador | SFW soft | NSFW explícito | Notas |
|---|---|---|---|
| **Stripe** | ✅ Acepta | ❌ Prohibido | Cierre + reserva fondos 180 días si te pillan |
| **PayPal** | ✅ Acepta | ❌ Prohibido | Mismo riesgo + ban de cuenta personal asociada |
| **Lemon Squeezy** (MoR) | ✅ Acepta | ❌ Rechaza | Recomendado para SFW: gestiona impuestos globales |
| **Paddle** (MoR) | ✅ Acepta | ❌ Rechaza | Alternativa a Lemon |
| **FastSpring** (MoR) | ✅ Acepta | ❌ Rechaza | Más caro, más enterprise |
| **CCBill** | ⚠️ Overkill | ✅ Estándar adult | Líder histórico del sector adult |
| **Segpay** | ⚠️ Overkill | ✅ Aceptado | Alternativa a CCBill |
| **Epoch** | ⚠️ Overkill | ✅ Aceptado | Veterano del sector |
| **Verotel** | ⚠️ Overkill | ✅ Aceptado | Europeo |
| **NOWPayments** (cripto) | ✅ Acepta | ✅ Acepta | Acepta 300+ cryptos |
| **Cryptomus** (cripto) | ✅ Acepta | ✅ Acepta | Popular en sector adult |

**Comparativa de costes**:

| Procesador | Comisión | Setup fee | Reserva | Tiempo aprobación |
|---|---|---|---|---|
| **Stripe** (SFW) | 2.9% + $0.30 | $0 | 0% | Instantáneo |
| **PayPal** (SFW) | 2.9-3.5% | $0 | 0% | Instantáneo |
| **Lemon Squeezy** (SFW MoR) | 5% + $0.50 | $0 | 0% | Días |
| **CCBill** (NSFW) | 10-15% | $500-1.500 | 5-10% durante 6 meses | 2-8 semanas |
| **Segpay** (NSFW) | 10-15% | $500-2.000 | 5-10% durante 6 meses | 2-8 semanas |
| **NOWPayments** (cripto) | 0.5% | $0 | 0% | Días |

**Impacto económico** simulado con $10.000 ingresos/mes:

| Vía | Comisión | Reserva retenida | **Neto al mes** |
|---|---|---|---|
| SFW + Stripe | $290 | $0 | **$9.710** |
| SFW + Lemon Squeezy | $500 | $0 | **$9.500** |
| NSFW + CCBill | $1.250 | $750 (recuperable a 6m) | **$8.000** |
| NSFW + cripto only | $50 | $0 | **$9.950** (pero pool de usuarios menor) |

**Conclusión 2.2.1**: SFW reduce costes de pago, elimina setup fee y permite operar desde día 1.

#### 2.2.2 Proveedores de IA (LLM)

| Proveedor | Modelo | SFW | NSFW | Coste $/M tokens (in / out) | Calidad |
|---|---|---|---|---|---|
| **Anthropic** | Claude Haiku 4.5 | ✅ | ❌ AUP prohíbe | $1 / $5 | Alta |
| **Anthropic** | Claude Sonnet 4.6 | ✅ | ❌ AUP prohíbe | $3 / $15 | Muy alta |
| **OpenAI** | GPT-4o-mini | ✅ | ❌ ToS prohíbe | $0.15 / $0.60 | Alta |
| **OpenAI** | GPT-4o | ✅ | ❌ ToS prohíbe | $5 / $15 | Muy alta |
| **Google** | Gemini 2.5 Flash | ✅ | ❌ ToS prohíbe | $0.30 / $2.50 | Alta |
| **OpenRouter** | Lumimaid 70B | ✅ | ✅ | ~$0.80 / $0.80 | Media-Alta (NSFW) |
| **OpenRouter** | Magnum v4 72B | ✅ | ✅ | ~$1.50 / $1.50 | Alta (NSFW) |
| **Mistral** | Nemo 12B | ✅ | ⚠️ con prompts cuidadosos | $0.10 / $0.30 | Media |
| **DeepSeek** | DeepSeek V3 | ✅ | ⚠️ zona gris según provider | $0.30 / $1.10 | Alta |

**Calidad comparada para chat emocional/companion**:

SFW (libre acceso a top tier):
- 🥇 Claude Sonnet 4.6 — el mejor para conexión emocional, calidez, memoria larga
- 🥈 GPT-4o — muy bueno
- 🥉 Claude Haiku 4.5 — 90% calidad de Sonnet a 1/3 del precio (modelo principal recomendado)
- Gemini 2.5 Flash — bueno y barato
- DeepSeek V3 — bueno, multi-idioma fuerte, barato

NSFW (limitado a uncensored):
- 🥇 Magnum v4 72B — mejor calidad NSFW del mercado open
- 🥈 Lumimaid 70B — popular y equilibrado
- 🥉 Llama 3.3 70B fine-tunes uncensored — variable

**Conclusión 2.2.2**: la calidad NSFW disponible es **inferior** a la calidad SFW de Claude/GPT. Hacer NSFW = renunciar a usar los mejores modelos del mundo.

#### 2.2.3 Distribución y marketing

| Canal | SFW | NSFW |
|---|---|---|
| App Store (Apple) | ✅ Aceptado | ❌ Prohibido (regla 1.1.4 de la App Review Guidelines) |
| Play Store (Google) | ✅ Aceptado | ❌ Prohibido o relegado a sideload |
| Google Ads | ✅ Permitido | ❌ Prohibido |
| Meta Ads (Facebook/Instagram) | ✅ Permitido | ❌ Prohibido |
| TikTok Ads | ✅ Permitido | ❌ Prohibido |
| Reddit Ads | ✅ Permitido | ⚠️ Solo en subs adult específicos |
| YouTube partnerships | ✅ Posible | ❌ No viable |
| Influencers mainstream | ✅ Posible | ❌ Limitado a nichos adult |
| SEO Google (orgánico) | ✅ Sin penalización | ⚠️ Penalizado parcialmente (SafeSearch) |
| Tráfico afiliados adult | ⚠️ Irrelevante | ✅ Ecosistema establecido |
| Email marketing (Resend, etc.) | ✅ Sin restricción | ⚠️ Mayoría de proveedores rechazan |

**Conclusión 2.2.3**: SFW tiene acceso a todos los canales escalables. NSFW depende de canales especializados con menor alcance.

#### 2.2.4 Legal y regulatorio

| Aspecto | SFW | NSFW |
|---|---|---|
| **18 USC 2257** (record-keeping EE.UU.) | No aplica | Aplica con exención AI declarada (riesgo si mal documentado) |
| **EU AI Act** | Aplica disclosure | Aplica disclosure + restricciones extra |
| **GDPR** | Aplica estándar | Aplica con extra cuidado en datos sensibles |
| **Verificación edad** | Checkbox 18+ | Verificación robusta (DNI, servicio externo $0.50-2/usuario) |
| **DMCA** | Aplica con baja incidencia | Aplica con alta incidencia (más reportes) |
| **Restricciones país** | Mínimas | Prohibido en Indonesia, Tailandia, partes Asia/África/Oriente Medio |
| **Riesgo demanda psicológica** | Bajo | Alto (especialmente si usuario menor o vulnerable) |
| **Estructura legal recomendada** | Autónomo o SL | SL (separación patrimonial obligatoria) |

**Conclusión 2.2.4**: NSFW multiplica obligaciones legales y exposición a demandas.

### 2.3 Tamaño y características del mercado

| Aspecto | SFW companion | NSFW companion |
|---|---|---|
| Tamaño mercado global | **5-10x más grande** | Más pequeño pero pago/usuario mayor |
| Competencia | Alta pero diferenciable | Alta y agresiva |
| Tipo de usuario | Diverso (soledad, curiosidad, romance) | Concentrado (hombres 18-45) |
| ARPU paying | $15-30/mes | $30-100/mes |
| Conversión free→paid | 4-7% | 6-12% |
| Churn mensual | 15-25% | 25-40% (más alto) |
| LTV paying | $80-180 | $120-300 |
| Reputación social | Neutra/positiva (wellness) | Negativa/estigma |
| Capacidad de PR/medios | Alta | Difícil |
| Casos de éxito recientes | Replika 30M users, Character.AI vendida $2.7B (2024) | Candy.AI, DreamGF (privadas, sin datos públicos confirmables) |

### 2.4 Por qué se eligió SFW soft (los 10 motivos)

1. **Procesador de pago disponible desde día 1** sin pagar $500-1.500 de setup ni esperar 2-8 semanas. Crítico con presupuesto $200-300.
2. **LLM de máxima calidad disponible** (Claude Haiku/Sonnet vs uncensored de calidad media).
3. **Marketing escalable** — Google Ads, Meta Ads, TikTok, App Stores cuando llegue el momento.
4. **Mercado total 5-10x mayor** — Replika 30M, Character.AI vendida por $2.7B.
5. **Posicionamiento de marca limpio** — sin estigma, mediabilidad alta, partnerships posibles.
6. **Riesgo legal inferior** — sin 2257, sin lawsuits por contenido sexual, sin requisito KYC fuerte.
7. **Menor coste operativo** — sin reserva del 5-10% de CCBill, churn más bajo, soporte más sencillo.
8. **Margen de NSFW soft permitido** — fotos de lencería/bikini son SFW para Stripe/Lemon (ver caso qkkie con PayPal). No se renuncia al "premium" desbloqueable.
9. **Compatibilidad con apps móviles a futuro** — fundamental para escalar.
10. **Capacidad de operar como solo dev** — NSFW realmente requiere equipo o partnership con procesador adult, gestión legal, etc. Solo dev + NSFW = inviable con $300.

### 2.5 Visión a futuro: posible versión NSFW (V2)

**No se descarta**. Si la versión SFW valida product-market fit y genera caja, podría considerarse una versión NSFW separada.

**Cuándo tendría sentido lanzarla**:
- Tras 12-18 meses de operación SFW estable
- Con $5.000-10.000 MRR consolidados (caja para invertir)
- Con base de usuarios SFW que demande ese tipo de contenido (señal de demanda real)
- Con tiempo / equipo para gestionar las complicaciones operativas extra

**Cómo se haría (arquitectura V2 NSFW)**:
- **Dominio separado** (ej: `marca.com` SFW, `marca-plus.com` o entidad legal distinta para NSFW)
- **Empresa legal separada** o subsidiaria para aislar riesgo del negocio SFW
- **Procesador CCBill / Segpay** + cripto (ya factible con caja consolidada)
- **Modelos uncensored vía OpenRouter** (Magnum, Lumimaid)
- **Verificación de edad robusta** (servicio tipo Yoti, AgeVerify, $0.50-2/verificación)
- **Compliance 2257-exempt declaration** (porque personajes son IA, no personas reales — debe ir formal y visible)
- **Reutilización de tecnología SFW** (motor de memoria, mood, vida propia, todo aplica)
- **Migración voluntaria de usuarios** ("desbloquear modo adulto" con verificación adicional y consentimiento explícito)

**Lo que NO se hará nunca**:
- ❌ Mezclar contenido NSFW en la app SFW (riesgo de cierre instantáneo de Stripe/Lemon → muerte del negocio)
- ❌ Ambigüedad legal de tipo "está en gris" — o claramente SFW o claramente NSFW separado
- ❌ Lanzar V2 NSFW antes de tener V1 SFW estable y rentable

### 2.6 Resumen de la decisión

> **SFW soft V1 ahora. NSFW V2 quizás en 12-18 meses tras validar SFW.**
>
> Razón principal: **viabilidad económica y operativa con $300 y solo dev**. NSFW requiere $1.500+ setup, equipo legal, procesador adult, modelos LLM de menor calidad, y opera en mercado más pequeño con peor reputación. SFW desbloquea Stripe/Lemon, Claude/GPT, App Stores, marketing legítimo y un mercado 5-10x mayor.
>
> La V2 NSFW se contemplará si y solo si la V1 SFW valida product-market fit. Se haría con entidad legal separada y dominio independiente, reutilizando tecnología pero aislando riesgo.

---

## 3. Visión y posicionamiento

### 3.1 Visión
Crear un compañero de IA que se sienta tan auténtico, presente y atento que el usuario establezca un vínculo emocional real, sostenido en el tiempo, sin necesidad de que el usuario crea que es humana.

### 3.2 Posicionamiento — "Character-first / respectful ambiguity"
Modelo intermedio entre la honestidad explícita (Replika) y el engaño (qkkie agresivo). Usado con éxito por Character.AI, Talkie, Chai, Janitor.

**Principios**:
- La marca se centra en los **personajes y la experiencia**, no en "AI Companion"
- La IA **confirma ser IA si se le pregunta directamente** (en system prompt)
- Existe **disclosure formal** en Terms / FAQ / footer (cumple EU AI Act)
- El marketing puede ser inmersivo sin engañar

**Líneas rojas (no cruzar)**:
- ❌ "5 millas de distancia" (engaño geográfico)
- ❌ "Vista por última vez hace 3 min" (engaño de presencia humana)
- ❌ Personajes < 18 años (riesgo legal grave)
- ❌ Afirmar que la IA es una persona real
- ✅ "Online" / "Offline" como estado abstracto está OK
- ✅ Delay realista en respuestas está OK
- ✅ Footer discreto "AI character" en chat
- ✅ Mención de IA al menos una vez en onboarding

### 3.3 Frame de marca
NO se vende como "AI girlfriend" ni como "AI companion app". Se vende por:
- Personajes con personalidad fuerte
- Experiencia inmersiva
- Conexión que crece con el tiempo

Ejemplos de posicionamiento posible (a desarrollar):
- *"Meet someone who actually remembers"*
- *"Conversations that grow with you"*
- *"The character you'll think about all day"*

---

## 4. Mercado y segmentos de usuario

### 4.1 Tamaño del mercado (referencias)
- **Replika**: 30M usuarios, ~$65M revenue (2023)
- **Character.AI**: 20M+ MAU, adquirida por Google por $2.700M (2024)
- **Chai App**: ~$40M revenue (2023)
- **Mercado SFW companion** crece anualmente en doble dígito; segmento muy underserved en español/portugués

### 4.2 Segmentos de usuario objetivo

| Segmento | % aprox | Qué busca | Disposición a pagar |
|---|---|---|---|
| **Solos / aislados** | 35% | Compañía, alguien con quien hablar | Media-Alta (suscripción) |
| **Curiosos / tech** | 15% | Probar la tecnología | Baja (free) |
| **Practicantes sociales** | 15% | Practicar conversación, ligue, idiomas | Baja-Media |
| **Románticos / fantasiosos** | 25% | Vivir un romance que no tienen | Alta (créditos + suscripción) |
| **Vulnerables** | 10% | Confunden IA con realidad | NO target — riesgo |

**Foco**: segmentos 1, 4 y secundariamente 3.

### 4.3 Mercados geográficos
- **Inglés global**: mercado más grande, más competencia
- **Español (ESP + LatAm)**: mercado grande y MENOS competido (la mayoría de apps están mal localizadas)
- **Portugués (Brasil)**: oportunidad bonus si Claude lo maneja bien (lo hace)

**Estrategia**: lanzar bilingüe ES+EN desde día 1 (Claude lo soporta sin coste extra) y medir de dónde llegan los usuarios.

---

## 5. Lo que el mercado quiere (validado por estudios y reseñas)

### 5.1 Features que generan engagement (ordenadas por impacto)

1. **Memoria real** — la queja #1 de usuarios de Replika es que "se olvida"
2. **Voz** — mensajes de audio aumentan engagement reportado en +300%
3. **Iniciativa** — que la IA escriba primero, sin esperar
4. **Evolución temporal** — la relación cambia con el tiempo
5. **Personalización** — que "mi" IA sea diferente a la tuya
6. **Empatía detectada** — que note si estoy mal y reaccione
7. **No-servilismo** — que tenga opiniones, días malos, lleve la contraria
8. **Fotos contextuales** — "selfie desde la cafetería", no porno
9. **Rutina y ritual** — buenos días, buenas noches automáticos
10. **Continuidad** — lo que pasó ayer importa hoy

### 5.2 Quejas recurrentes (oportunidad)

| Queja | Oportunidad para nosotros |
|---|---|
| "Replika se olvida en 2 semanas" | **Memoria de calidad** (RAG + resúmenes jerárquicos) |
| "Character.AI tiene 1000 personajes pero ninguno se siente real" | **Pocos personajes, profundidad enorme** |
| "Todo es en inglés y suena raro en español" | **Nativo ES+EN, no traducido** |
| "Es demasiado servil, siempre de acuerdo" | **Personalidad real con opiniones** |
| "Pides una foto y siempre es la misma cara" | **Galería contextual generada** |
| "No hay continuidad, cada chat empieza de cero" | **Vida propia entre sesiones** |
| "Se siente fake / es obvio que es IA" | **Imperfecciones humanas** (typos, "perdona estaba cocinando") |

---

## 6. Diferenciadores estratégicos (3 ejes elegidos)

### 🥇 Eje 1 — Memoria profunda
**Promesa**: "Te conoce mejor que tu mejor amigo. Recuerda todo. Crece contigo."

**Implementación técnica**:
- pgvector (extensión de Postgres) para búsqueda semántica
- Resumen automático de cada sesión guardado como "memoria de largo plazo"
- "Diario interno" donde la IA registra lo que aprende del usuario
- Fechas importantes detectadas y guardadas (cumpleaños, eventos)
- Callbacks espontáneos: "¿al final fuiste al médico el martes?"
- Página transparente "lo que ella sabe de ti" → editable/borrable por el usuario (gana confianza + cumplimiento GDPR)

**Coste extra**: ~$0 (solo buen diseño técnico).

### 🥈 Eje 2 — Vida propia entre conversaciones
**Promesa**: "Ella no te está esperando. Tiene su vida, te la cuenta, te incluye."

**Implementación técnica**:
- Cron job nocturno: para cada personaje, generar un "día simulado" (3-5 eventos)
- Eventos guardados como memoria del personaje
- Cuando hablas con ella, los trae naturalmente
- Mensajes proactivos contextuales: foto del café de la mañana, buenas noches
- Si "tuvo un mal día simulado", está más reservada (afecta mood)

**Coste extra**: ~$0.05-0.10/usuario/día (varias llamadas LLM de fondo). **El diferenciador más fuerte**.

### 🥉 Eje 3 — Inteligencia emocional
**Promesa**: "Detecta cómo estás antes de que se lo digas. Reacciona como reaccionaría alguien que te quiere."

**Implementación técnica**:
- Análisis de sentimiento del mensaje del usuario antes de responder (Haiku 4.5 barato como clasificador)
- System prompt dinámico según mood detectado
- Recordatorio si el usuario lleva días bajo: "no me has contado lo del trabajo, ¿estás bien?"
- Modo "apoyo": si dice "lo estoy pasando mal", desactiva flirteo automáticamente

**Coste extra**: ~$0.001/mensaje (clasificador Haiku).

---

## 7. Producto — MVP scope (versión "producto digno", 8-12 semanas)

### 7.1 Features CORE (lanzamiento)

**Cuentas y autenticación**
- Registro con email + contraseña
- Login social (Google) opcional
- Verificación 18+ (checkbox legal)
- Recuperación de contraseña

**Personajes**
- 5-8 personajes diseñados a fondo en lanzamiento
- Galería con foto de perfil + tags (edad, personalidad, intereses)
- Bio extensa al hacer click
- Galería de fotos: algunas visibles, otras bloqueadas (desbloquear con créditos)

**Chat 1-a-1**
- Conversación persistente con memoria
- Mensajes troceados en múltiples burbujas
- Delay simulado realista (1-30s, según hora del día y mood)
- Indicador "escribiendo..." discreto
- Estado "online/offline" del personaje (basado en horario simulado)
- Envío de fotos por parte del personaje (las desbloqueadas o "regaladas" en momentos clave)

**Memoria** (eje diferenciador 1)
- Resumen automático de sesión cada 50 mensajes
- pgvector para búsqueda semántica
- Página "Lo que ella sabe de ti" con edición/borrado

**Mood básico** (eje diferenciador 3, versión simple en MVP)
- 4-5 estados: cariñosa, juguetona, melancólica, enérgica, pensativa
- Detección simple del sentimiento del usuario (clasificador Haiku)
- Modo apoyo activado si detecta tristeza grave

**Vida propia** (eje diferenciador 2, versión simple en MVP)
- Cron diario que genera 1-3 eventos del día por personaje
- Mensajes proactivos limitados (1-2 al día como máximo)

**Monetización**
- Sistema de créditos (compra one-shot)
- Suscripción mensual con beneficios
- Paywall después de N mensajes/día en plan free
- Galería desbloqueable con créditos
- Integración Lemon Squeezy

**Compliance y legal**
- Terms of Service
- Privacy Policy
- AI Disclosure (footer + FAQ)
- Política de datos (borrar cuenta = borrar todo)
- 18+ obligatorio

**Idiomas**
- Inglés + Español desde día 1 (Claude lo hace gratis)
- UI traducida con react-i18next o similar

**Email transaccional**
- Confirmación de registro
- Recibos de pago
- Alertas básicas (mensaje proactivo de personaje)

### 7.2 Features FUERA del MVP (roadmap)

**Mes 2-3 post-lanzamiento**
- Mensajes de voz (ElevenLabs) — solo en plan premium
- PWA instalable
- Personalización del nombre del usuario por la IA ("¿cómo prefieres que te llame?")
- Más personajes (escalar a 15-20)
- Analítica de comportamiento (Posthog)

**Mes 4-6**
- App nativa móvil (React Native o similar)
- Llamadas de voz tiempo real (más caro técnicamente)
- Generación de imagen on-demand para usuarios premium
- Sistema de "regalos" virtuales

**Roadmap lejano**
- Personajes user-generated (marketplace)
- Vídeo
- Multi-personaje (chat de grupo)
- AR/VR
- **V2 NSFW** (entidad y dominio separados, ver Sección 2.5)

---

## 8. Arquitectura técnica (alto nivel)

### 8.1 Stack
- **Frontend**: Next.js 14 (App Router) + Tailwind + shadcn/ui
- **Backend**: Next.js API Routes + Worker separado (Railway/Fly.io)
- **DB principal**: Supabase (Postgres) con extensión pgvector
- **Auth**: Supabase Auth
- **Storage de imágenes**: Cloudflare R2 (gratis hasta 10GB, sin coste de salida)
- **Cache / colas**: Upstash Redis
- **Email**: Resend (3000/mes free)
- **LLM gateway**: Anthropic SDK directo (o OpenRouter como abstracción)
- **Pagos**: Lemon Squeezy
- **Analítica**: Posthog (free tier)
- **Monitoring**: Sentry (free tier)
- **Hosting**: Vercel (free tier)

### 8.2 Componentes lógicos clave

```
[ Web Next.js ]
      ↓
[ API Routes ] ──→ [ Supabase: users, characters, chats, memory, credits ]
      ↓                       ↑
[ Redis Queue ]                │
      ↓                       │
[ Worker ]                    │
      ├─ Mood classifier (Haiku) ──┐
      ├─ Memory retrieval (pgvector RAG)
      ├─ Main response (Haiku 4.5 / Sonnet 4.6)
      ├─ Message splitter
      └─ Delayed delivery
      ↓
[ Daily cron ]
      ├─ Generate "simulated day" per character
      └─ Schedule proactive messages
```

### 8.3 Flujo de un mensaje
1. Usuario envía mensaje vía WebSocket o polling
2. API valida (créditos disponibles, no abuse)
3. Encolar en Redis para procesamiento
4. Worker:
   a. Clasificar mood del usuario (Haiku, ~$0.001)
   b. Recuperar memoria relevante (pgvector)
   c. Construir system prompt dinámico (personaje + mood + memoria + vida del día)
   d. Llamar a LLM (Haiku 4.5 normal, Sonnet 4.6 si premium)
   e. Trocear respuesta en burbujas
   f. Calcular delays (1-30s)
   g. Emitir mensajes con delay realista
5. Guardar conversación + actualizar memoria

---

## 9. Modelo de monetización

### 9.1 Tiers

**FREE**
- 30 mensajes/día por personaje
- Memoria de 7 días
- 0 créditos iniciales (gana 5 al día por login)
- Sin voz
- Respuesta normal (cola gratuita)
- Acceso a 5 personajes (de 8)

**BASIC — $9.99/mes**
- 200 mensajes/día por personaje
- Memoria de 30 días
- 50 créditos/mes incluidos
- Respuesta más rápida (cola prioritaria)
- Acceso a todos los personajes
- 5 desbloqueos de foto al mes incluidos

**PREMIUM — $19.99/mes**
- Mensajes ilimitados
- Memoria ilimitada
- 200 créditos/mes incluidos
- Mensajes de voz incluidos (limitados)
- Modelo Sonnet 4.6 en momentos clave
- Acceso prioritario a personajes nuevos
- Personalización (cómo te llama, etc.)

### 9.2 Créditos (compra suelta)
- Pack pequeño: 100 créditos = $4.99
- Pack mediano: 500 créditos = $19.99
- Pack grande: 2000 créditos = $49.99 (mejor margen)
- Pack mega: 5000 créditos = $99.99

### 9.3 Coste de extras en créditos
- Foto SFW desbloqueada: 20 créditos
- Foto sensual desbloqueada: 50 créditos
- Mensaje de voz: 30 créditos
- Foto personalizada (futuro): 200 créditos
- Llamada (futuro): 100 créditos/min

### 9.4 Métricas objetivo (industria SFW companion)
- Conversión free → paid: 4-7%
- ARPU paying: $20-30/mes
- ARPU global: $1-2/mes
- Churn mensual paying: 15-25%
- LTV paying: $80-180

---

## 10. Simulación de costes

### 10.1 Costes fijos mensuales (independiente de usuarios)

| Concepto | Coste/mes |
|---|---|
| Dominio | $1 |
| Vercel (free tier hasta cierto punto) | $0 |
| Supabase free tier | $0 |
| Upstash free tier | $0 |
| Cloudflare R2 (10GB free) | $0 |
| Resend (3k emails free) | $0 |
| Worker (Railway hobby) | $5 |
| Sentry, Posthog (free tiers) | $0 |
| **Total fijo inicial** | **~$6/mes** |

A partir de ~500 DAU empezarás a salir del free tier de varios servicios. A 1000 DAU rondará $50-80/mes de fijos.

### 10.2 Coste variable principal: LLM

**Asumiendo Claude Haiku 4.5** (referencia ~$1/M tokens input, ~$5/M tokens output):

Por mensaje típico:
- Input: ~2000 tokens (system prompt + memoria + historial reciente) → $0.002
- Output: ~300 tokens → $0.0015
- Clasificador mood (Haiku): ~500 in / 50 out → $0.0008
- **Total por mensaje**: ~$0.004

Por usuario al día según uso:
- Free agresivo (10 msg/día): $0.04/día → $1.20/mes
- Free típico (30 msg/día): $0.12/día → $3.60/mes
- Paying típico (100 msg/día): $0.40/día → $12/mes
- Power user (300 msg/día): $1.20/día → $36/mes

**Vida propia (cron diario)**: ~$0.02/personaje/día. Con 8 personajes = $0.16/día = $5/mes total (independiente de usuarios).

### 10.3 Escenarios de coste total

#### Escenario A — 100 DAU (mes 1-2)
- 95 free × $1.20 = $114
- 5 paying × $12 = $60
- Vida propia: $5
- Fijos: $6
- **Total: ~$185/mes**

#### Escenario B — 1.000 DAU (mes 4-6 si crece bien)
- 940 free × $1.20 = $1.128
- 60 paying × $12 = $720
- Vida propia: $5
- Fijos: ~$60
- **Total: ~$1.913/mes**

#### Escenario C — 10.000 DAU (año 2 optimista)
- 9.300 free × $1.20 = $11.160
- 700 paying × $12 = $8.400
- Vida propia: $5
- Fijos: ~$300
- Voz (50% paying con voz, $5/mes coste) = $1.750
- **Total: ~$21.615/mes**

### 10.4 Optimizaciones de coste posibles
- **Caching de prompts** (Anthropic prompt caching): -50% en input tokens repetidos. Crítico.
- **Resúmenes en lugar de historial completo**: -60-80% en input tokens
- **Modelo barato para usuarios free** (DeepSeek V3, Gemini Flash): -80% coste
- **Throttling agresivo de free tier**: clave para no quemar dinero
- **Rate limit por IP** para evitar abuso

---

## 11. Proyección de ingresos

### 11.1 Asumiendo conversion 5%, ARPU paying $22 (mix subs + créditos)

| Mes | DAU | % paying | Paying users | Ingreso bruto | Lemon 5% | Coste | **Profit** |
|---|---|---|---|---|---|---|---|
| 1 | 50 | 2% | 1 | $22 | -$1 | $100 | **-$79** |
| 2 | 200 | 3% | 6 | $132 | -$7 | $250 | **-$125** |
| 3 | 500 | 4% | 20 | $440 | -$22 | $700 | **-$282** |
| 4 | 1.000 | 5% | 50 | $1.100 | -$55 | $1.900 | **-$855** |
| 6 | 2.500 | 5% | 125 | $2.750 | -$138 | $4.500 | **-$1.888** |
| 9 | 5.000 | 6% | 300 | $6.600 | -$330 | $9.000 | **-$2.730** |
| 12 | 10.000 | 7% | 700 | $15.400 | -$770 | $21.600 | **-$6.970** |

⚠️ **Conclusión incómoda**: con estos parámetros conservadores, **NO llegas a profit aún a 10k DAU**. La economía no funciona.

### 11.2 Por qué — y cómo arreglarlo

El problema: **el coste del free tier se come los ingresos**. 90%+ usuarios free generan coste de LLM y no pagan.

**Palancas para arreglarlo**:

1. **Reducir free tier a 10 msg/día** (en vez de 30):
   - Coste free: $0.40/mes vs $1.20/mes (-66%)
   - Trade-off: peor "first taste"

2. **Modelo aún más barato para free** (DeepSeek V3, ~$0.30/M input):
   - Coste free: ~$0.12/mes (-90%)
   - Trade-off: calidad ligeramente menor en free (puede ser argumento de upsell)

3. **Subir conversión vía mejor UX**:
   - Industry top: 8-12% conversión
   - Cada 1% = +200 paying con 10k DAU

4. **Subir ARPU con créditos bien diseñados**:
   - $22 → $30 ARPU es factible si el sistema de créditos funciona

### 11.3 Escenario realista con optimizaciones

Aplicando: free agresivo 10 msg/día + modelo barato para free + conversión 7% + ARPU $28:

| Mes | DAU | Paying | Ingreso | Coste | **Profit** |
|---|---|---|---|---|---|
| 3 | 500 | 35 | $980 | $300 | **+$631** |
| 6 | 2.500 | 175 | $4.900 | $1.000 | **+$3.745** |
| 9 | 5.000 | 350 | $9.800 | $1.700 | **+$7.760** |
| 12 | 10.000 | 700 | $19.600 | $3.000 | **+$15.620** |

✅ **Mucho mejor**. Con las optimizaciones correctas, **break-even al mes 2-3** y profit creciente.

### 11.4 Realismo del crecimiento DAU

Llegar a **10.000 DAU en 12 meses solo y sin presupuesto de ads es ambicioso pero no imposible**. Comparativas:
- Replika llegó a 1M users en 18 meses con marketing
- Apps virales pueden hacerlo en semanas
- Realista para indie sin ads: 1.000-3.000 DAU al final del año 1

**Escenario realista año 1**:
- Mes 6: 500-1.000 DAU
- Mes 12: 2.000-5.000 DAU
- Profit estimado fin de año 1: **$200-2.000/mes** (cubre costes y deja modesto)

**Escenario optimista (viralidad o ads pagados)**:
- Mes 12: 10.000-20.000 DAU
- Profit: $5.000-15.000/mes

---

## 12. Roadmap y timeline

### Fase 0 — Definición (en curso)
- ✅ Posicionamiento, modelo, arquitectura
- ✅ Decisión SFW vs NSFW documentada (Sección 2)
- ⏳ Diseño de personajes (siguiente paso)
- ⏳ Marca y dominio
- ⏳ Setup legal (estructura, ToS, etc.)

### Fase 1 — MVP (semanas 1-12 desde inicio dev)
- Semana 1-2: setup técnico (Next, Supabase, Auth, deploy)
- Semana 3-4: chat básico + integración LLM
- Semana 5-6: memoria (pgvector + RAG)
- Semana 7: mood + clasificador
- Semana 8: galería de fotos + desbloqueo
- Semana 9: créditos + Lemon Squeezy
- Semana 10: vida propia (cron, mensajes proactivos)
- Semana 11: pulido UI, onboarding, compliance
- Semana 12: testing + lanzamiento privado (beta cerrada)

### Fase 2 — Iteración temprana (mes 4-6)
- Pulido en base a feedback de beta
- Lanzamiento público
- Optimización de funnel y conversión
- Mensajes de voz (ElevenLabs)

### Fase 3 — Escalar (mes 7-12)
- PWA
- Más personajes
- Optimización agresiva de coste LLM
- Acquisition channels (TikTok, Reddit, SEO)

### Fase 4 — Expansión (año 2)
- App móvil nativa
- Llamadas de voz
- Imagen on-demand premium
- Internacionalización ampliada
- **Evaluación de V2 NSFW** (si SFW está validado y consolidado)

---

## 13. Decisiones tomadas (resumen)

| Decisión | Valor | Referencia |
|---|---|---|
| **Contenido** | **SFW soft** (sensual no explícito) | Sección 2 |
| Versión NSFW futura | Posible V2 separada en 12-18 meses si SFW valida PMF | Sección 2.5 |
| Posicionamiento | Character-first / ambigüedad respetuosa | Sección 3 |
| Disclosure IA | En ToS/FAQ/footer + AI confirma si se le pregunta | Sección 3.2 |
| Mercado | Inglés + Español (desde día 1) | Sección 4.3 |
| LLM principal | Claude Haiku 4.5 | Sección 2.2.2, 8 |
| LLM premium | Claude Sonnet 4.6 | Sección 2.2.2, 8 |
| LLM gateway | Anthropic SDK directo, evaluar OpenRouter como backup | Sección 8 |
| Pago | Lemon Squeezy (Merchant of Record) | Sección 2.2.1 |
| Stack | Next.js + Supabase + Upstash + Vercel + Cloudflare R2 | Sección 8 |
| Imágenes | Pre-generadas en Promptchan | — |
| Personajes lanzamiento | 5-8 (calidad > cantidad) | Sección 7.1 |
| Diferenciadores | Memoria + Vida propia + Inteligencia emocional | Sección 6 |
| Modelo monetización | Freemium con créditos + suscripción mensual | Sección 9 |
| Equipo | Solo (Daniel) | — |
| Presupuesto inicial | $200-300 | — |
| Tipo de MVP | "Producto digno" (8-12 semanas) | Sección 7 |

---

## 14. Decisiones pendientes

### Críticas (bloqueantes)
- [ ] **Marca + dominio** (nombre del proyecto)
- [ ] **Estructura legal** (autónomo, sociedad, fiscalidad para Lemon Squeezy)
- [ ] **Diseño de personajes** (arquetipos, personalidades, biografías, prompts)
- [ ] **Identidad visual** (logo, paleta, estilo)

### Tácticas (segundo nivel)
- [ ] Verificación de edad: ¿simple checkbox o servicio externo?
- [ ] ¿Login social desde día 1 o solo email?
- [ ] Decisión final modelo LLM para free tier (Haiku vs DeepSeek/Gemini)
- [ ] ¿Caching de prompts activo desde día 1? (sí, recomendado)
- [ ] Estructura del system prompt de cada personaje (template a definir)
- [ ] Política de imágenes desbloqueables: ¿aleatoria o curada?
- [ ] Diseño exacto del onboarding (cuántos pasos, qué pide)

### Estratégicas (a definir antes de lanzamiento)
- [ ] Estrategia de adquisición primeros 100 usuarios
- [ ] Métricas a medir desde día 1 (KPIs)
- [ ] Política de moderación de abuso (jailbreaks, contenido prohibido del usuario)
- [ ] Plan de soporte (cómo se atiende al usuario)

---

## 15. Riesgos identificados

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| Anthropic suspende API por AUP | Media | Alto | Usar OpenRouter como abstracción, plan de migración a otro modelo |
| Lemon Squeezy cierra cuenta | Baja | Alto | Mantener producto claramente SFW, plan B con cripto |
| Coste LLM se descontrola | Media | Alto | Caching agresivo, free tier limitado, modelo barato para free |
| No alcanzamos masa crítica de usuarios | Alta | Alto | Estrategia de adquisición orgánica, contenido viral, partnerships |
| Burnout de solo founder | Alta | Crítico | Scope MVP realista, no sobrecomprometerse |
| Demanda legal por daño psicológico | Baja | Crítico | Disclosure claro, modo apoyo, derivar a recursos reales si detecta crisis |
| Calidad de personajes insuficiente | Media | Alto | Inversión grande en diseño de los 5-8 iniciales |
| Competidor copia el diferenciador | Alta | Medio | First mover advantage + ejecución continua |
| Cambio regulatorio (EU AI Act endurece) | Media | Medio | Cumplimiento desde día 1, monitoreo legal |
| Tentación de meter NSFW en V1 | Media | Crítico | Disciplina: NSFW solo en V2 con dominio/entidad separados (Sección 2.5) |

---

## 16. Próximos pasos inmediatos

**Por hacer Daniel** (acción asincrónica):
1. Probar más a fondo qkkie y 1-2 competidores (Talkie, Character.AI) y anotar:
   - UX del onboarding
   - Diseño del paywall (cuándo aparece, cómo)
   - Cómo presentan los personajes
2. Pensar 3-5 nombres de marca candidatos + verificar dominios disponibles
3. Crear cuenta de prueba en Lemon Squeezy y revisar requisitos
4. Decidir estructura fiscal (autónomo / sociedad)

**Por hacer juntos** (siguientes sesiones):
1. **Diseño de personajes**: arquetipos, personalidades, biografías, prompts (próxima sesión propuesta)
2. **Diseño del onboarding**: flujo paso a paso desde landing → primera conversación → primer paywall
3. **Esquema de base de datos**: tablas, relaciones, índices
4. **Diseño del system prompt template**: estructura común para todos los personajes
5. **Estrategia de adquisición**: cómo conseguir los primeros 100 usuarios sin presupuesto

---

## 17. Apéndices

### A. Referencias de competencia
- **qkkie.com** — SFW soft (probable) con ambigüedad calculada, ~100-200 personajes, créditos + PayPal/Visa, principal referencia operacional
- **Character.AI** — character-first, masivo, gratis con plan paid, adquirido por Google
- **Replika** — honest companion, memoria mejorable, ~30M users
- **Talkie AI** — character-first, top App Store
- **Chai App** — character-first, monetización agresiva
- **Janitor AI** — NSFW, comunidad fuerte
- **Candy.AI / DreamGF** — NSFW explícito, modelo a evitar para V1

### B. Enlaces y recursos para revisar
- Anthropic AUP: anthropic.com/legal/aup
- Lemon Squeezy adult/companion content policy
- EU AI Act Article 50 (disclosure obligations)
- Promptchan.com (generación de imágenes)
- Apple App Review Guidelines 1.1.4 (contenido sexual)

### C. Historial de decisiones
- 2026-05-04: Pivote de NSFW a SFW soft (motivos detallados en Sección 2)
- 2026-05-04: Pivote de "honest companion" a "character-first ambiguo respetuoso"
- 2026-05-04: Decisión de "producto digno" (MVP 8-12 semanas) vs MVP mínimo
- 2026-05-04: Documentación formal de la decisión SFW vs NSFW con comparativa exhaustiva (esta versión)
