# Wati

## Documento Técnico — Hackathon Build With AI 2026

### Categoría: ENERGÍA | Triple Impacto

---

> **Equipo:** Wati  
> **Fecha:** 30 de mayo de 2026  
> **Versión:** 1.0 — Entregable Final  

---

## 1. INVESTIGACIÓN Y CONTEXTO

### 1.1 El problema de la energía eléctrica en Bolivia

Bolivia atraviesa una transición energética crítica. El 71% de su electricidad se genera con gas natural, y el sector domiciliario e industrial crecen a tasas del 6–8% anual de demanda. En Santa Cruz de la Sierra —la ciudad más calurosa del país, con picos de 38°C entre noviembre y marzo— el consumo residencial representa el **45% del consumo eléctrico total del departamento** (Visión 360, julio 2024).

CRE R.L. (Cooperativa Rural de Electrificación) es el distribuidor eléctrico exclusivo de Santa Cruz, con **más de 300,000 socios activos**. Su estructura tarifaria es **escalonada**: el usuario paga más por kWh cuanto más consume en el mes. A pesar de esto, ninguna herramienta disponible en el mercado boliviano muestra al usuario en qué bloque tarifario está *durante* el mes, ni le permite actuar sobre eso en tiempo real.

### 1.2 Brechas detectadas mediante investigación primaria

Mediante entrevistas informales a 20 familias cruceñas de clase media en mayo 2026, identificamos:

| Hallazgo | % de familias entrevistadas |
|---|:---:|
| No saben en qué bloque tarifario de CRE están actualmente | 95% |
| Recibieron alguna vez una factura "sorpresa" más alta de lo esperado | 85% |
| Dejan el AC encendido en habitaciones vacías habitualmente | 75% |
| Nunca han ajustado el uso del AC según el pronóstico climático | 100% |
| Pagarían por una solución que les ahorre Bs 200+/mes | 70% |

### 1.3 Estructura Tarifaria Base CRE R.L. (Resolución AETN Nº 654/2023)

Las tarifas de CRE no tienen un único valor fijo por kWh, sino que varían de acuerdo a bloques de consumo mensual y aplican cargos fijos adicionales. A continuación se detallan los valores específicos para la categoría de **Pequeña Demanda en Baja Tensión (PD BT)**, vigente del período Noviembre 2023 a Octubre 2027:

- **Domiciliaria (11 Domiciliaria PD BT)**:
  - Cargo Fijo (con derecho a 15 kWh): `13,162 Bs/mes`
  - De 16 a 120 kWh: `0,727 Bs/kWh`
  - De 121 a 300 kWh: `0,929 Bs/kWh`
  - De 301 a 1000 kWh y excedentes: `0,978 Bs/kWh`

- **General I (19 General 1 PD BT - Escuelas, hospitales, asociaciones)**:
  - Cargo mínimo (con derecho a 20 kWh): `22,479 Bs/mes`
  - De 21 a 300 kWh: `1,002 Bs/kWh`
  - De 301 a 1000 kWh: `1,471 Bs/kWh`
  - Excedente a 1000 kWh: `1,331 Bs/kWh`

- **General II (28 General 2 PD BT - Bancos, restaurantes, comercios)**:
  - Cargo mínimo (con derecho a 20 kWh): `31,304 Bs/mes`
  - De 21 a 300 kWh: `1,310 Bs/kWh`
  - De 301 a 1000 kWh: `1,720 Bs/kWh`
  - Excedente a 1000 kWh: `1,464 Bs/kWh`

- **Industrial (37 Industrial PD BT)**:
  - Cargo Fijo: `6,033 Bs/mes`
  - De 0 a 1000 kWh: `0,712 Bs/kWh`
  - Excedente a 1000 kWh: `0,607 Bs/kWh`

- **Granjeros (53 Granjeros PD BT - Labores agroindustriales y agrícolas)**:
  - Cargo Fijo: `46,156 Bs/mes`
  - De 0 a 100 kWh: `0,850 Bs/kWh`
  - Excedente a 100 kWh: `0,875 Bs/kWh`

- **Agua Potable (84 Agua Potable PD BT - Bombeo)**:
  - Cargo Fijo: `10,945 Bs/mes`
  - Cargo Variable único: `0,640 Bs/kWh`

*(Nota: Los valores presentados corresponden a la Estructura Tarifaria Base calculada a precios de diciembre de 2022 con impuestos, los cuales se indexan mensualmente según la fórmula aprobada).*

Una familia con 2–3 aires acondicionados puede pagar **Bs 750–1,000/mes en temporada calurosa**, frente a Bs 350–400 en temporada fría. Esa diferencia de Bs 400–600/mes es **completamente evitable** con gestión inteligente del consumo.

---

## 2. PROBLEMA IDENTIFICADO

### Framework CDC (Contexto → Dolor → Consecuencia)

**CONTEXTO:**  
Los 300,000 socios de CRE en Santa Cruz tienen acceso a la app oficial "CRE Móvil", que muestra únicamente el historial de facturas pasadas y las tarifas vigentes. No existe ninguna herramienta que conecte el consumo en tiempo real con las tarifas escalonadas, el clima y el control de los electrodomésticos.

**DOLOR (3 puntos concretos):**

1. **Desconocimiento del bloque tarifario en tiempo real.** El usuario no sabe a cuántos kWh del siguiente umbral (más caro) se encuentra hoy, a mitad del mes.

2. **Sin correlación entre clima y consumo.** Nadie avisa: *"Mañana habrá 36°C, tu AC consumirá 20% más, y eso puede subirte de bloque tarifario."* El usuario actúa de forma reactiva, nunca preventiva.

3. **Sin acción automatizada.** Aunque el usuario recibiera la alerta, no tiene mecanismo para actuar sobre sus electrodomésticos de forma inteligente. El AC permanece encendido en habitaciones vacías durante horas.

**CONSECUENCIA:**

- Bs 400–600/mes de sobrecosto evitable por hogar en temporada calurosa.
- A escala: si el 10% de los 300,000 hogares reduce un 20% su consumo, se evitan ~57,600 MWh/año, equivalentes a miles de toneladas de CO₂.
- Pequeños comercios (categoría "Comercial" de CRE, tarifa más alta) tampoco tienen herramientas de gestión disponibles.

---

## 3. SOLUCIÓN PROPUESTA

### Wati: Sistema IoT + Multi-Agente de IA para Optimización del Consumo Eléctrico

Wati es una plataforma que combina **hardware físico** (nodo IoT instalado en el hogar) con **inteligencia artificial multi-agente** en la nube para ayudar a familias y pequeños comercios de Santa Cruz a reducir su factura eléctrica de CRE **entre un 15% y 30% mensual**, sin sacrificar comodidad.

### 3.1 Propuesta de Valor Única

> *"Wati es el único sistema que te dice exactamente cuántos kWh te quedan antes de que tu factura suba de precio —y toma acción automáticamente para que no cruce ese umbral."*

### 3.2 Diferenciación frente a CRE Móvil

| Funcionalidad | CRE Móvil (oficial) | Wati |
|---|:---:|:---:|
| Ver historial de facturas pasadas | ✅ | — (no duplicamos) |
| Proyección de consumo al cierre del mes | ❌ | ✅ |
| Alerta ANTES de cruzar un bloque tarifario | ❌ | ✅ |
| Medición de consumo en tiempo real (Watts) | ❌ | ✅ |
| Control físico del AC desde el celular | ❌ | ✅ |
| Apagado automático por detección de ausencia | ❌ | ✅ |
| Correlación con pronóstico climático | ❌ | ✅ |
| Recomendaciones de IA accionables | ❌ | ✅ |

### 3.3 Componentes del sistema

**Componente 1 — Nodo Wati (Hardware, ~$35 USD)**  
Dispositivo físico basado en ESP32-S3 con sensores integrados:

- PZEM-004T: Medidor de energía real (V, A, W, kWh) con pinza inductiva, sin cortar cables
- DS18B20: Sensor de temperatura interior
- PIR HC-SR501: Detector de presencia en la habitación
- Emisor/Receptor IR: Control remoto del AC (compatible con cualquier marca)

**Componente 2 — Backend + Pipeline de Datos (Nube)**  
FastAPI → Redis → InfluxDB (series temporales) + PostgreSQL (datos de usuario). Cada nodo reporta telemetría cada 30 segundos vía HTTPS.

**Componente 3 — Sistema Multi-Agente de IA (LangGraph)**  
5 agentes coordinados que procesan datos y generan acciones: SensorAgent, TariffAgent, WeatherAgent, InventoryAgent y SchedulerAgent (LLM Gemini 1.5 Pro).

**Componente 4 — App Cliente (PWA / React Native)**  
Dashboard personal en tiempo real, control del AC, notificaciones push inteligentes.

---

## 4. ARQUITECTURA TECNOLÓGICA

### 4.1 Diagrama de Capas

```
┌──────────────────────────────────────────────────────┐
│  CAPA 1 — EDGE (Nodo físico en el hogar)            │
│  ESP32-S3 + PZEM-004T + DS18B20 + PIR + IR          │
│  → Telemetría cada 30s por HTTPS                     │
└──────────────────────┬───────────────────────────────┘
                       │ HTTPS / TLS
┌──────────────────────▼───────────────────────────────┐
│  CAPA 2 — INGEST (FastAPI + Redis Streams)          │
│  Validación → Cola → Worker de procesamiento         │
└──────────────────────┬───────────────────────────────┘
                       │
┌──────────────────────▼───────────────────────────────┐
│  CAPA 3 — DATA LAKE + IA                            │
│  InfluxDB (telemetría) + PostgreSQL (usuarios)       │
│  LangGraph — Orquestador de Agentes IA               │
└──────┬───────────────────────────────────┬───────────┘
       │                                   │
┌──────▼──────────┐               ┌────────▼──────────┐
│ Dashboard Admin │               │  App del Cliente  │
│ (flota + KPIs)  │               │  + Notif. Push    │
└─────────────────┘               └───────────────────┘
```

El flujo completo del pipeline de datos e infraestructura en Google Cloud Platform está disponible en el siguiente diagrama:

![Pipeline de Arquitectura en GCP](gcp_pipeline_wati.svg)

### 4.2 Stack Tecnológico Completo

| Capa | Tecnología | Justificación |
|---|---|---|
| Firmware | C++ (Arduino/ESP-IDF) en ESP32-S3 | Control preciso de sensores, bajo consumo |
| API | FastAPI (Python 3.11) | Async nativo, tipado, OpenAPI automático |
| Cola de mensajes | Redis Streams | Ligero, suficiente para < 10k dispositivos |
| DB Telemetría | InfluxDB Cloud | Optimizado para series temporales IoT |
| DB Relacional | PostgreSQL | Usuarios, dispositivos, facturas, configuraciones |
| Orquestador IA | LangGraph (LangChain) | Grafos de agentes con estado persistente |
| LLM | Gemini 1.5 Pro (Google) | Costo < $0.001/usuario/día, razonamiento rápido |
| OCR Facturas | Google Cloud Vision API | DOCUMENT_TEXT_DETECTION para facturas CRE |
| Notificaciones | Firebase Cloud Messaging (FCM) | Gratuito, nativo iOS/Android, deeplinks |
| App Cliente | React (PWA) → React Native (Fase 2) | Demo rápida en hackathon, escalable |
| Deploy | Railway (Docker) | Gratuito para MVP, escala sin reconfigurar |
| Almacenamiento | Supabase Storage | Imágenes temporales de facturas (< 60 seg) |
| Setup BLE | Web Bluetooth API / Captive Portal | Onboarding sin técnico desde el celular |

### 4.3 Sistema Multi-Agente IA (Detalle)

```
TRIGGER → SensorAgent → [TariffAgent + WeatherAgent + InventoryAgent]
                                        ↓
                                SchedulerAgent (LLM)
                                        ↓
                    [Acción IR al ESP32-S3] + [Notificación FCM]
```

**SensorAgent:** Lee InfluxDB de las últimas 2h. Calcula kWh acumulados del mes. Detecta presencia y picos de consumo.

**TariffAgent:** Aplica la estructura tarifaria de CRE. Determina el bloque actual y los kWh restantes para el siguiente umbral.

**WeatherAgent:** Consulta OpenWeatherMap (forecast 48h para Santa Cruz). Calcula el impacto esperado de la temperatura en el consumo del AC.

**InventoryAgent:** Estima el consumo esperado por electrodoméstico según el inventario declarado por el usuario.

**SchedulerAgent (Gemini Pro):** Recibe el contexto de todos los agentes anteriores y genera:

- Acción concreta para el dispositivo (ej: `AC_SET_TEMP: 26°C`)
- Notificación push redactada en lenguaje natural para el usuario
- Plan del día con recomendaciones horarias

**Ejemplo de razonamiento real:**

```
Input: {bloque: "Bloque 4", kwh_restantes: 35, temp_ext: 33°C,
        forecast_mañana: 36°C, presencia: true, ac_encendido: true}

Output: {
  accion: "AC_SET_TEMP → 26°C",
  notificacion: "⚠️ Te quedan 35 kWh antes de subir de bloque.
                 Subí el AC a 26°C — seguís cómodo y ahorrás
                 hasta Bs 45 este mes. Mañana: 36°C, buen día
                 para conservar margen."
}
```

---

## 5. APLICACIÓN DE IA

### 5.1 Capas de inteligencia del sistema

**IA en el Edge (ESP32-S3):**

- TensorFlow Lite Micro para detección local de patrones de consumo anómalos
- Reglas de automatización locales que funcionan sin conexión a internet
- Aprendizaje de códigos IR de cualquier marca de AC (modo raw learning)

**IA en la Nube (LangGraph + Gemini Pro):**

- Orquestación multi-agente con estado persistente entre ejecuciones
- Razonamiento contextual: combina tarifa + clima + presencia + historial
- Generación de lenguaje natural para notificaciones personalizadas
- Proyección de factura al cierre del mes con error < 10%

**IA para Onboarding (Google Cloud Vision):**

- OCR de facturas físicas de CRE: extrae kWh, categoría, período e importe
- La imagen se elimina de la nube en < 60 segundos post-procesamiento
- Fallback siempre disponible: ingreso manual de datos

### 5.2 Modelo de invocación responsable del LLM

El LLM no se invoca en polling continuo, sino por eventos:

- Nuevo dato de telemetría con anomalía detectada
- Umbral tarifario próximo (< 50 kWh para el siguiente bloque)
- Solicitud explícita del usuario
- Cron diario a las 7:00 AM (resumen y plan del día)

Throttle: máximo 10 llamadas LLM por dispositivo por día. Costo estimado: < $0.001 USD/usuario/día con Gemini Pro.

---

## 6. ANÁLISIS FODA

### Fortalezas

- **Diferenciación real:** Ninguna solución equivalente existe en el mercado boliviano ni latinoamericano para esta tarifa específica.
- **Hardware + Software integrado:** La combinación de IoT físico con IA en la nube crea una barrera de entrada alta para competidores.
- **Modelo de ingresos doble:** Hardware (venta única) + SaaS (suscripción recurrente). El hardware subsidia la adquisición del cliente de suscripción.
- **ROI demostrable:** El ahorro de Bs 200–400/mes justifica ampliamente la suscripción de Bs 26/mes. Payback del hardware en < 3 meses.
- **Escalabilidad técnica:** La arquitectura soporta desde 1 hasta 300,000 dispositivos con ajustes mínimos de infraestructura.
- **Setup sin técnico:** BLE 5.0 del ESP32-S3 permite configuración desde el celular en < 10 minutos.

### Debilidades

- **Dependencia de WiFi:** El nodo requiere red WiFi estable. En hogares con WiFi débil o zonas con cortes frecuentes, el funcionamiento se degrada.
- **Costo inicial de hardware:** Los $35 USD del nodo pueden ser una barrera en segmentos de ingresos bajos.
- **Instalación del CT del PZEM:** Aunque no requiere cortar cables, el usuario debe acceder al tablero eléctrico, lo que puede generar fricción.
- **Equipo técnico pequeño:** El desarrollo simultáneo de firmware, backend, IA y frontend en 48 horas requiere coordinación precisa.
- **Pregunta legal abierta (OCR):** Subir imágenes de facturas a Google Cloud Vision requiere clarificación respecto a las políticas de CRE y la Ley 453 de Bolivia.

### Oportunidades

- **Mercado virgen:** 300,000 socios de CRE sin ninguna herramienta de optimización disponible. TAM inmediato de $10.8M USD/año (a $3/mes).
- **Crisis energética boliviana:** Bolivia importa electricidad desde Argentina y Brasil en temporadas pico, lo que convierte al ahorro energético en política pública, no solo en conveniencia del usuario.
- **Expansión a ELFEC y ENDE:** Las estructuras tarifarias de ELFEC (Cochabamba) y ENDE (La Paz, resto del país) son similares. El modelo es replicable a escala nacional.
- **Segmento comercial:** Pequeños comercios con categoría tarifaria "Comercial" pagan tarifas más altas y tienen mayor disposición a pagar por herramientas de optimización.
- **Alianzas con instaladores de AC:** Los 500+ instaladores de AC en SCZ pueden ser canal de distribución e instalación del hardware.
- **CRE como cliente institucional:** CRE podría financiar los dispositivos para sus socios como parte de un programa de eficiencia energética, creando un canal B2B masivo.

### Amenazas

- **Competencia de soluciones globales:** Shelly, Sense o Emporia podrían adaptarse al mercado boliviano, aunque ninguno conoce la tarifa escalonada de CRE.
- **Cambio de política tarifaria de CRE:** Si CRE modifica su estructura de bloques, el motor de optimización debe actualizarse.
- **Dependencia de APIs de terceros:** Google Cloud Vision, OpenWeatherMap y Gemini son servicios de terceros. Un cambio de precios o una interrupción afecta el servicio.
- **Variabilidad del tipo de cambio:** El hardware (ESP32-S3, sensores) se cotiza en USD. Una devaluación del boliviano encarece el costo de reposición.
- **Marco regulatorio IoT:** Bolivia no tiene regulación clara sobre dispositivos IoT conectados a redes eléctricas residenciales. AGETIC podría eventualmente requerir certificaciones.

---

## 7. ANÁLISIS PESTEL

### Político

- **Política energética nacional:** El gobierno boliviano promueve la eficiencia energética como parte de su agenda de transición hacia energías renovables. Un producto que demuestre reducción de demanda pico tiene alineación con políticas públicas.
- **AGETIC y regulación tecnológica:** La Agencia de Gobierno Electrónico y Tecnologías de la Información no tiene regulación específica para dispositivos IoT residenciales a la fecha. Riesgo bajo a corto plazo.
- **Relación CRE–Estado:** CRE es una cooperativa con fuerte respaldo municipal. Una alianza con CRE podría acelerar la adopción masiva vía programas de subsidio o financiamiento.

### Económico

- **Contexto de inflación:** Bolivia mantiene una política de control de cambios que genera presión sobre las reservas. El costo del hardware en USD puede encarecerse si el boliviano se deprecia.
- **Clase media cruceña en expansión:** Santa Cruz tiene el mayor PIB per cápita del país. El segmento objetivo (familias con 2+ ACs) tiene capacidad de pago para hardware de $35 USD y suscripción de $3/mes.
- **ROI del usuario:** El ahorro promedio estimado de Bs 200–400/mes tiene un payback del hardware de 2.5–3 meses. Esto crea un argumento de venta cuantificable y concreto.
- **Mercado de ACs en crecimiento:** Las ventas de aires acondicionados en Bolivia crecieron ~25% en 2025 por las olas de calor récord. Más ACs = mayor problema de consumo = mayor demanda por Wati.

### Social

- **Conciencia ambiental emergente:** La generación joven (25–40 años) en Santa Cruz muestra mayor sensibilidad al consumo responsable de energía, especialmente post-sequías de 2024.
- **Penetración de smartphones:** > 85% de la población urbana de SCZ tiene smartphone. La app es el canal de interacción natural.
- **WhatsApp como cultura de comunicación:** Aunque FCM es la elección técnica correcta, la cultura boliviana de comunicación vía WhatsApp puede requerir un canal de soporte en ese formato.
- **Desconfianza hacia la tecnología doméstica:** Una porción del segmento mayor de 50 años puede mostrar resistencia a instalar un dispositivo que "controla la electricidad del hogar". El diseño UX del onboarding debe ser extremadamente simple.

### Tecnológico

- **Ecosistema ESP32 maduro:** El ESP32-S3 tiene una comunidad global activa, librerías probadas y precio en caída ($4–6 USD por unidad). La cadena de suministro es confiable via AliExpress/Mercado Libre.
- **LLMs asequibles:** Gemini 1.5 Pro ofrece capacidad de razonamiento de clase mundial a fraccción del costo de GPT-4 ($0.075 USD / 1M tokens input). Esto hace el modelo de IA económicamente sostenible desde el día 1.
- **Cobertura WiFi en SCZ:** La penetración de WiFi doméstico en Santa Cruz urbana supera el 75%, suficiente para el mercado objetivo inicial.
- **5G y conectividad futura:** La expansión de 5G en Bolivia abre la posibilidad futura de nodos Wati con conectividad celular, eliminando la dependencia del WiFi del usuario.

### Ecológico

- **Impacto directo en emisiones:** Bolivia genera el 71% de su electricidad con gas natural. Cada kWh no consumido evita directamente emisiones de CO₂. El impacto ambiental es cuantificable y comunicable.
- **Objetivo de reducción:** Si el 10% de los 300,000 hogares CRE reduce un 20% su consumo, se evitan ~57,600 MWh/año ≈ 28,800 toneladas de CO₂eq/año (usando factor de emisión de 0.5 kgCO₂/kWh para Bolivia).
- **LEED y certificaciones verdes:** Edificios comerciales que demuestren reducción de consumo mediante Wati pueden aplicar a certificaciones de eficiencia que valorizan sus inmuebles.
- **Cambio climático como acelerador:** Las olas de calor cada vez más intensas en Santa Cruz (2024: 43°C récord) aumentan el consumo de AC, lo que aumenta el ahorro potencial de Wati y su relevancia comercial.

### Legal

- **Ley 453 (Bolivia):** Ley General de los Derechos de las Usuarias y los Usuarios. Requiere consentimiento informado para el procesamiento de datos personales, incluyendo imágenes de facturas. Mitigación: eliminación de la imagen en < 60 segundos + consentimiento explícito en los ToS.
- **Contrato de suministro CRE:** Revisar si el contrato de suministro de CRE prohíbe el uso de dispositivos de terceros en el circuito eléctrico del socio. El PZEM-004T usa pinza inductiva (no invasiva), lo que minimiza el riesgo legal.
- **Ley de Telecomunicaciones (Bolivia):** Los dispositivos que transmiten datos por WiFi deben cumplir con las regulaciones de la ATT (Autoridad de Telecomunicaciones y Transportes). Revisión pendiente para comercialización.
- **Responsabilidad civil por automatización:** El apagado automático del AC (vía presencia PIR) genera una pregunta legal: ¿qué sucede si se apaga en un contexto inadecuado? Mitigación: cláusula de exención de responsabilidad en ToS + notificación push con botón de "Re-encender" inmediato.

---

## 8. LEAN CANVAS

```
┌──────────────────┬───────────────────────────┬─────────────────────────────┐
│  PROBLEMA        │  SOLUCIÓN                 │  PROPUESTA DE VALOR ÚNICA   │
│                  │                           │                             │
│ 1. No saben en   │ Nodo IoT (ESP32-S3)       │ "El único sistema que te    │
│ qué bloque       │ con medición real +       │ dice exactamente cuántos    │
│ tarifario están  │ agentes de IA que:        │ kWh te quedan antes de que  │
│ durante el mes   │ • Proyectan la factura    │ tu factura suba de precio   │
│                  │ • Alertan antes de        │ —y actúa automáticamente    │
│ 2. El clima      │   cruzar umbrales         │ para que no lo cruce."      │
│ impacta el       │ • Controlan el AC         │                             │
│ consumo sin      │   automáticamente         ├─────────────────────────────┤
│ que lo noten     │ • Correlacionan clima     │  VENTAJA INJUSTA            │
│                  │   y consumo               │                             │
│ 3. El AC         │                           │ Integración profunda con    │
│ funciona en      ├───────────────────────────┤ la estructura tarifaria     │
│ habitaciones     │  MÉTRICAS CLAVE           │ específica de CRE +         │
│ vacías sin       │                           │ hardware propio calibrado   │
│ control          │ • kWh ahorrados/mes       │ para la red 220V/50Hz de    │
│                  │ • Bs ahorrados/mes        │ Santa Cruz.                 │
│ ├────────────────┤ • % reducción factura     │                             │
│ │  SEGMENTOS     │ • NPS del usuario         │                             │
│ │  DE CLIENTES   │ • Churn mensual           │                             │
│ │                │ • Dispositivos activos    │                             │
│ │ Primario:      ├───────────────────────────┴─────────────────────────────┤
│ │ Familias SCZ   │  CANALES                                                │
│ │ clase media    │                                                         │
│ │ con 2–3 ACs    │ • App Store / Google Play (descarga)                    │
│ │ (200k hogares) │ • Instaladores de AC (canal físico)                     │
│ │                │ • Redes sociales (demos en vivo)                        │
│ │ Secundario:    │ • Alianza con CRE Ltda. (canal institucional)           │
│ │ Pequeños       ├─────────────────────────────────────────────────────────┤
│ │ comercios con  │  ESTRUCTURA DE COSTOS          FLUJO DE INGRESOS        │
│ │ tarifa CRE     │                                                         │
│ │ Comercial      │ • Hardware: $18 COGS/nodo      • Venta hardware: $35    │
│ └────────────────┴─────────────────────────────────────────────────────────┘
```

---

## 9. ANÁLISIS FINANCIERO

### 9.1 Estructura de Costos (Por Unidad de Hardware)

| Componente | Costo (USD) |
|---|:---:|
| ESP32-S3-N8R8 (módulo) | $4.50 |
| PZEM-004T V3.0 (sensor energía) | $6.00 |
| DS18B20 (sensor temperatura) | $0.80 |
| PIR HC-SR501 (sensor presencia) | $0.60 |
| IR Emisor TSAL6200 + Receptor TSOP38238 | $0.80 |
| Caja enclosure (impresión 3D o plástico) | $2.00 |
| PCB, resistencias, conectores | $1.50 |
| Empaque, manual, accesorios | $1.50 |
| **COGS Total por nodo** | **$17.70** |
| **Precio de venta sugerido** | **$35.00** |
| **Margen bruto hardware** | **~49%** |

### 9.2 Proyecciones de Ingresos (Modelo SaaS)

**Supuestos:**

- Precio hardware: $35 USD (Bs ~242)
- Suscripción básica: $3 USD/mes (Bs ~21)
- Plan Comercial (negocios): $8 USD/mes
- Churn mensual: 3% (optimista, asumiendo ROI demostrado)
- Tasa de conversión free → paid: 60%

| Mes | Dispositivos Activos | Suscriptores Paid | MRR (USD) | ARR (USD) |
|:---:|:---:|:---:|:---:|:---:|
| 3 | 50 | 30 | $90 | $1,080 |
| 6 | 200 | 120 | $360 | $4,320 |
| 12 | 1,000 | 600 | $1,800 | $21,600 |
| 18 | 5,000 | 3,000 | $9,000 | $108,000 |
| 24 | 15,000 | 9,000 | $27,000 | $324,000 |

**Punto de equilibrio operativo:** ~800 suscriptores activos (cubriendo costos de infraestructura, LLM y soporte de 1 persona).

### 9.3 ROI para el Usuario Final

| Concepto | Valor |
|---|---|
| Factura promedio familia con 2 ACs (temporada calurosa) | Bs 800/mes |
| Ahorro estimado con Wati (20% optimista / 15% conservador) | Bs 120–160/mes |
| Costo mensual Wati (hardware amortizado 12 meses + suscripción) | Bs 42/mes |
| **Ahorro neto mensual para el usuario** | **Bs 78–118/mes** |
| **Payback del hardware** | **< 3 meses** |
| **ROI año 1** | **> 220%** |

### 9.4 Escenario de Alianza B2B con CRE

Si CRE R.L. adopta Wati como herramienta de gestión de demanda para sus socios:

- CRE puede reducir la demanda pico en verano, evitando importar electricidad cara desde Argentina/Brasil.
- Modelo propuesto: CRE financia el hardware a sus socios a Bs 0/mes (subsidiado) + paga a Wati una tarifa B2B de $1.5/dispositivo/mes.
- A 30,000 dispositivos (10% de la base de socios): **$45,000 USD/mes de MRR B2B**.

---

## 10. IMPACTO ESPERADO

### 10.1 Impacto Económico (Para el Usuario)

- Ahorro promedio estimado: **Bs 150–300/mes** por hogar en temporada calurosa.
- A 10,000 hogares: **Bs 1.5M–3M/mes** devueltos al poder adquisitivo de familias cruceñas.
- Pequeños comercios: reducción de hasta 25% en factura eléctrica comercial, con impacto directo en la rentabilidad del negocio.

### 10.2 Impacto Ambiental

- Reducción de consumo estimada por dispositivo: **80–150 kWh/mes** (20% de 400–750 kWh/mes promedio).
- CO₂ evitado por dispositivo/año: **~60–90 kgCO₂** (factor 0.5 kgCO₂/kWh, Bolivia).
- A 10,000 dispositivos activos: **600–900 toneladas de CO₂/año** evitadas.
- A 30,000 dispositivos (10% base CRE): **~57,600 MWh/año** de reducción de demanda = ~**28,800 tCO₂/año**.

### 10.3 Impacto Social

- **Democratización del ahorro energético:** Herramientas de gestión que antes solo existían para empresas industriales, ahora disponibles para el hogar boliviano.
- **Educación en consumo responsable:** Las notificaciones diarias educan al usuario sobre el impacto de sus hábitos en la factura y en el medio ambiente.
- **Generación de empleo local:** Ensamblaje de hardware, soporte técnico e instalación pueden generar empleos en Santa Cruz.
- **Reducción de la pobreza energética:** Familias en el límite del segmento Bloque 4–5 pueden mantenerse en bloques más económicos con gestión activa.

### 10.4 Impacto Sistémico (Para CRE y Bolivia)

- **Gestión de demanda pico:** Reducir el consumo en las horas pico (12:00–20:00 en verano) tiene un impacto económico directo en los costos de operación de CRE.
- **Bolivia como referente regional:** Si el modelo funciona en CRE SCZ, puede replicarse en ELFEC (Cochabamba), ENDE (La Paz) y en cooperativas eléctricas de Argentina, Perú y Ecuador con estructuras tarifarias similares.
- **Datos para política pública:** El mapa de calor de consumo agregado de Wati puede ser compartido con CRE y el Ministerio de Energía para planificación de infraestructura eléctrica.

### 10.5 Triple Impacto — Resumen

| Dimensión | Indicador | Meta (12 meses) |
|---|---|---|
| **ECONÓMICO** | Ahorro acumulado para usuarios | Bs 18M (1,000 dispositivos × Bs 1,500/año) |
| **AMBIENTAL** | CO₂ evitado | 900 tCO₂/año (1,000 dispositivos) |
| **SOCIAL** | Hogares con acceso a optimización energética | 1,000 familias en SCZ |

---

## 11. PLAN DE VALIDACIÓN POST-HACKATHON

### Hipótesis críticas a validar (primeras 4 semanas)

1. **H1 — Adopción:** ¿50 familias de SCZ instalan el dispositivo sin asistencia técnica presencial?
2. **H2 — Retención:** ¿El 70%+ sigue usando la app tras 30 días?
3. **H3 — Ahorro real:** ¿El ahorro medido con datos reales es ≥ 15% de la factura?
4. **H4 — NPS:** ¿El Net Promoter Score supera 50 (excelente)?

### Próximos pasos concretos

| Hito | Plazo | Acción |
|---|---|---|
| Piloto 10 hogares | Mes 1 | Instalar 10 nodos en familias voluntarias de SCZ |
| Consulta legal (OCR + IoT) | Mes 1 | Revisar Ley 453 y contrato CRE con abogado |
| Publicar en Google Play (Beta) | Mes 2 | Migrar PWA a React Native |
| Acuerdo con 3 instaladores AC | Mes 2 | Canal de distribución e instalación |
| Presentación a CRE | Mes 3 | Propuesta de alianza B2B para programa de eficiencia |
| 50 dispositivos activos | Mes 3 | Primer batch de producción |

## 12. ROADMAP DE EXPANSIÓN A FUTURO (PLAN A 5 AÑOS)

Con el fin de expandir el impacto del proyecto, Wati evolucionará de una solución dirigida principalmente a la clase media residencial hacia un ecosistema B2B e Industrial completo enfocado en la eficiencia operativa corporativa y el control de calidad ambiental.

### Hitos de la Evolución Tecnológica e Industrial

#### 🟢 6 Meses — Optimización Edge & Onboarding Autónomo (Wati Residencial Pro)
* **Aprovisionamiento BLE Autónomo**: Desarrollo de un firmware ESP32-S3 que permita la configuración y emparejamiento Wi-Fi "Zero-Touch" directamente desde la aplicación mediante **Bluetooth Low Energy (BLE)**. El usuario podrá enlazar el dispositivo sin intervención de un técnico especializado y sin lidiar con portales cautivos.
* **Módulo de Control Infrarrojo (IR) Inteligente**: Incorporación al hardware de emisores y receptores infrarrojos para aires acondicionados y televisores. Esto posibilitará apagar dispositivos o modular de forma autónoma la temperatura de enfriamiento según la presencia humana local y los umbrales de consumo definidos por el motor de IA.
* **Consola de Administración Web (Backoffice Operator)**: Despliegue de un portal de control para operadores del sistema Wati, permitiendo ver a los clientes activos, diagnosticar la conectividad de la flota IoT de forma proactiva y gestionar incidencias centralizadamente.

#### 🔵 1 Año — Wati Business (Pivote hacia Oficinas y Locales Comerciales)
* **Enfoque en Oficinas y Negocios**: Salida del nicho residencial para dirigir el producto a oficinas corporativas, sucursales bancarias, restaurantes, farmacias y comercios (categorías de tarifa General I y II de la CRE con tarifas de consumo significativamente más elevadas).
* **Consola Multi-Dispositivo & Multi-Tenant**: Habilitación de una interfaz administrativa unificada para gerentes de sucursales o administradores de edificios. Permitirá monitorear, apagar o programar de manera automatizada decenas de equipos de aire acondicionado y consumo eléctrico general desde una sola pantalla corporativa.
* **Algoritmos B2B en Gemini 1.5 Pro**: Entrenamiento del SchedulerAgent para optimizar perfiles de consumo según horarios comerciales de atención y mitigar picos bruscos de demanda en horas punta industriales/comerciales.

#### 🟠 3 Años — Wati Industrial (Monitoreo de Calidad del Aire y Entornos Industriales)
* **Adición del Módulo de Calidad del Aire**: Modificación del hardware de los nodos Wati para integrar sensores de partículas en suspensión (`PM2.5 / PM10`), dióxido de carbono (`CO₂`), humedad y compuestos orgánicos volátiles (COVs).
* **Expansión a Plantas y Naves Industriales**: Control y correlación activa entre el funcionamiento de sistemas de extracción de aire y ventilación industrial con la concentración de partículas del entorno. Esto garantiza un ambiente seguro que cumple con normas de seguridad ocupacional bolivianas e internacionales (OSHA) a la vez que maximiza la eficiencia energética.
* **Integración con Ecosistemas Industriales (SCADA / ERP)**: Conectividad nativa a través de interfaces industriales (Modbus, MQTT y REST APIs) para la automatización fluida de los procesos en plantas manufactureras.

#### 🔴 5 Años — Plataforma Integral Smart Cities & ESG Enterprise
* **Monitoreo y Reporte de Sostenibilidad (ESG)**: Consolidación de Wati como la plataforma SaaS líder en Sudamérica para auditorías de eficiencia energética corporativa y medición directa de la huella de carbono asociada al consumo eléctrico en tiempo real.
* **Control Predictivo HVAC Centralizado**: Gestión inteligente de grandes sistemas centralizados de climatización comercial basados en gemelos digitales térmicos y predicciones automáticas con Vertex AI.

---

*Documento generado para Hackathon Build With AI 2026 — Santa Cruz de la Sierra, Bolivia.*  
*Versión 1.0 | 30 de mayo de 2026*  
*Equipo Wati*
