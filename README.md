# 📘 GUÍA COMPLETA TFG — ARGOS

**Suite Integral de Ciberseguridad, Gestión de Identidad y Auditoría de Redes para el Usuario Final**
Autor: Saúl Álvarez Monzón — 2º DAM
Documento de orientación generado: 2026-04-28

---

## 0. Cómo usar esta guía

Este documento es tu hoja de ruta. Está dividido en bloques que puedes leer de forma independiente:

1. Valoración honesta de la idea (¿es buena? ¿es viable como TFG?)
2. Análisis de competencia por cada módulo de ARGOS
3. Propuesta de diferenciación e innovación
4. Recorte de alcance recomendado (MVP realista para un TFG de DAM)
5. Stack tecnológico recomendado (incluyendo PHP/CI4/Ionic/ddev/n8n que ya manejas)
6. Arquitectura técnica
7. Calendario de trabajo y presupuesto
8. Consideraciones legales y éticas (críticas en este proyecto)
9. Líneas futuras y consejos finales

---

## 1. VALORACIÓN GLOBAL DE LA IDEA

### ✅ Puntos fuertes

- **Tema actual y demandado:** la ciberseguridad doméstica es uno de los sectores con mayor crecimiento (informes de INCIBE, ENISA y el sector privado coinciden). Los ataques al usuario final han crecido año tras año.
- **Enfoque diferencial:** combinar herramientas defensivas + formación bajo el mismo paraguas es una propuesta poco habitual. La mayoría de soluciones del mercado están segmentadas (un gestor de claves por un lado, una academia por otro, un escáner por otro).
- **Branding sólido:** "ARGOS" es excelente. Mitología griega + el "vigilante de los cien ojos" = perfecto para una suite de seguridad. El nombre vende solo.
- **Doble valor:** utilidad inmediata (proteger) + valor a largo plazo (formar). Esto es un argumento comercial muy potente.

### ⚠️ Puntos débiles / problemas

- **El alcance es DEMASIADO ambicioso para un TFG de DAM2.** Cada uno de los 5 objetivos específicos podría ser un TFG completo por sí solo:
  - Un gestor de credenciales con cifrado seguro = nivel Bitwarden
  - Un motor de auditoría WiFi = nivel Nmap/Aircrack
  - Un sistema tipo Hack The Box = años de ingeniería + infraestructura cloud
  - Una plataforma de e-learning gamificada = nivel Cybrary
- **Limitaciones técnicas no contempladas:**
  - **iOS no permite auditar redes WiFi** (Apple bloquea el acceso a la API de WiFi sin entitlements empresariales). Tu app multiplataforma estará coja en iPhone.
  - **Android limita mucho** la captura de paquetes y el escaneo WiFi sin root a partir de Android 9+.
  - **Lanzar máquinas virtuales desde una app móvil/web es inviable.** Lo más cercano son contenedores Docker en backend o redirigir a HTB/TryHackMe.
- **Riesgo legal:** una herramienta de "auditoría de redes" puede vulnerar la LOPDGDD/RGPD si no se acota a la red propia del usuario. Más detalles en la sección 8.
- **Justificación poco fundamentada con datos:** te falta citar fuentes oficiales (INCIBE, ENISA, Eurostat, Verizon DBIR) que respalden las cifras del problema.

### 🎯 Veredicto

**La idea es buena, pero el documento actual la presenta como un producto comercial, no como un TFG entregable.** Necesitas:
1. Reducir alcance al MVP (sección 4)
2. Definir qué partes son "implementadas" y cuáles son "líneas futuras"
3. Documentar las limitaciones técnicas (es un punto a favor, no en contra: demuestra madurez)

---

## 2. ANÁLISIS DE COMPETENCIA POR MÓDULO

> Verifica precios y modelos antes de citarlos en el TFG: pueden cambiar entre 2025 y 2026.

### 2.1. Gestor de credenciales y bóveda de archivos

| Producto | Modelo | Precio (orientativo) | Fortalezas | Debilidades |
|---|---|---|---|---|
| **Bitwarden** | Open Source / Freemium | Gratis - 10 €/año Premium | Auditado, multiplataforma, self-hostable | Interfaz mejorable para no técnicos |
| **1Password** | Comercial | ~3 €/mes | UX excelente, integración familiar | Cerrado, sin tier gratis real |
| **KeePassXC** | Open Source | Gratis | Local, sin nube, muy seguro | UX intimidante para usuarios casuales |
| **Dashlane** | Comercial | ~5 €/mes | VPN incluida, monitoreo dark web | Caro, suscripción obligatoria |
| **NordPass** | Comercial | ~2 €/mes | Marketing fuerte, integración con NordVPN | Joven, menos auditado |
| **Proton Pass** | Freemium | Gratis - 5 €/mes | E2E, Suiza, integrado con ProtonMail | Joven, menos features |

**Tu hueco:** un gestor en español pensado para no técnicos, con tutoriales integrados y enfoque didáctico ("¿qué es una contraseña fuerte y por qué?"). Bitwarden y resto van al grano; tú puedes acompañar.

### 2.2. Auditoría WiFi / análisis de red

| Producto | Modelo | Plataforma | Notas |
|---|---|---|---|
| **Fing** | Freemium | iOS, Android, escritorio | Líder en consumo doméstico, muy pulido |
| **Nmap / Zenmap** | Open Source | Escritorio | Estándar de facto, demasiado técnico |
| **Wireshark** | Open Source | Escritorio | Captura de paquetes, muy técnico |
| **Aircrack-ng** | Open Source | Linux | Auditoría WiFi seria, requiere conocimiento |
| **NetSpot** | Freemium | macOS/Windows | Mapas de calor WiFi, comercial |
| **WiFi Analyzer** (Android) | Gratis | Android | Solo análisis básico de canales |

**Tu hueco:** una vista de "salud de mi red" en lenguaje natural. No mostrar paquetes ni MACs, sino "Tienes 4 dispositivos desconocidos conectados — revisar". Convertir Nmap en un asistente conversacional.

### 2.3. Detección de phishing

| Producto | Tipo | Notas |
|---|---|---|
| **Google Safe Browsing** | API gratis | Estándar, puedes integrarlo |
| **PhishTank** | API gratis | Base colaborativa de URLs phishing |
| **VirusTotal** | API freemium | Análisis multi-motor de URLs/archivos |
| **OpenPhish** | Freemium | Feeds de phishing en tiempo real |
| **Bitdefender TrafficLight** | Extensión gratis | Reactivo en navegador |
| **PhishER (KnowBe4)** | Empresarial | Caro, no para usuarios |

**Tu hueco:** un analizador *educativo* — no solo "esta URL es maliciosa", sino "fíjate en el dominio: dice paypa1.com en vez de paypal.com, eso es typosquatting".

### 2.4. Plataformas de aprendizaje en ciberseguridad

| Producto | Modelo | Precio | Notas |
|---|---|---|---|
| **Hack The Box** | Freemium | Gratis - 14 €/mes (HTB Academy) | Líder técnico, curva alta |
| **TryHackMe** | Freemium | Gratis - 10 €/mes | Más amigable que HTB, en inglés |
| **PortSwigger Academy** | Gratis | Gratis | Excelente para web hacking |
| **Cybrary** | Freemium | 59 €/mes Insider Pro | Vídeo + labs, en inglés |
| **OffSec (OSCP)** | Comercial | ~1.500 € certificación | Industria pro |
| **INCIBE / Hack the Hacker** | Gratis | Gratis | Recursos en español, dispersos |
| **roadmap.sh** | Gratis (open source) | Gratis | Solo roadmaps, sin labs |
| **Atenea (CCN-CERT)** | Gratis | Gratis | CTF español, técnico |

**Tu hueco:** **roadmap.sh + TryHackMe simplificado en español, para principiantes absolutos.** Esto es lo más realista y diferenciable.

### 2.5. Suites integrales (competencia directa)

| Producto | Notas |
|---|---|
| **Norton 360** | AV + VPN + gestor claves + dark web monitor. Caro (~80 €/año) y orientado al usuario sin formación técnica. No tiene componente educativo. |
| **Bitdefender Total Security** | Similar a Norton, sin formación. |
| **Kaspersky Premium** | Suite completa, problemas geopolíticos en EU. |
| **Avast One** | Freemium con módulos integrados, sin componente formativo. |

**Conclusión:** ningún suite generalista combina protección + formación. Esa es tu ventana de oportunidad real.

---

## 3. PROPUESTAS DE INNOVACIÓN Y DIFERENCIACIÓN

### 3.1. Diferenciadores claros que SÍ puedes implementar

1. **Idioma y contexto local.** El 90 % del contenido formativo de calidad en ciberseguridad está en inglés. Un producto **en castellano (y opcionalmente gallego, dado tu centro)** orientado al usuario español es ya un diferenciador.
2. **Onboarding por nivel de conocimiento.** Test inicial → ARGOS adapta el lenguaje y las recomendaciones. La gente abandona apps de seguridad porque "no entiende nada".
3. **Sistema de "logros y rachas" tipo Duolingo** aplicado a higiene digital: 7 días sin reutilizar contraseñas, 1ª URL sospechosa detectada, etc.
4. **Asistente IA didáctico.** Integra un LLM (Claude, GPT-4o-mini, Llama local) que explique en lenguaje natural los hallazgos: "He encontrado este dispositivo desconocido en tu red, ¿quieres que te explique cómo investigarlo?". Esto es 2026 — usuarios esperan IA conversacional.
5. **Generador de planes de respuesta a incidentes para usuarios domésticos.** "Mi cuenta de Gmail ha sido hackeada, ¿qué hago?" → checklist guiado paso a paso. Nadie del mercado de consumo lo ofrece.
6. **Integración con HIBP (Have I Been Pwned)** para chequear si los emails/contraseñas del usuario aparecen en filtraciones. API gratis, muy fácil de integrar, gran impacto visual.
7. **Roadmap visual interactivo** con nodos desbloqueables. Inspírate en roadmap.sh pero con quizzes integrados y enlaces a labs externos (TryHackMe, HTB, PortSwigger).
8. **Modo familiar / "padres-hijos".** Un padre configura ARGOS para su hijo adolescente. El padre ve el dashboard de hábitos digitales (sin invadir privacidad: agregados, no contenidos). Hueco enorme y poco explotado.
9. **Notificaciones proactivas vía n8n.** Cuando aparezca un nuevo CVE crítico que afecte a Windows/Android, ARGOS te avisa con explicación traducida. n8n es perfecto para orquestar esto.
10. **Modo "auditoría de mi vida digital"** — revisión anual donde la app analiza emails registrados, contraseñas en filtraciones, dispositivos en tu red, etc., y entrega un informe PDF.

### 3.2. Diferenciadores que SUENAN bien pero hay que descartar

- ❌ **Crear tu propia infraestructura tipo Hack The Box.** Imposible en un TFG. Mejor: enlazar a HTB/THM con tracking de progreso vía API si la exponen, o con autoevaluación.
- ❌ **Lanzar máquinas virtuales desde la app.** Reemplaza por: tutorial paso a paso de cómo configurar VirtualBox + scripts de aprovisionamiento descargables (Vagrant/Ansible).
- ❌ **Detección activa de phishing por análisis del correo del usuario.** Implica acceso IMAP + tratamiento de datos personales sensibles → RGPD complejo. Mejor: el usuario pega una URL/cabecera y ARGOS la analiza puntualmente.
- ❌ **VPN propia.** No es viable mantener infraestructura. Si quieres VPN, recomienda en la app productos de terceros.

---

## 4. ALCANCE RECOMENDADO: MVP REALISTA PARA TU TFG

Te propongo dividir ARGOS en **3 capas**: lo que entregas, lo que prototipas, lo que documentas como "futuro".

### 🟢 NÚCLEO ENTREGABLE (lo que SÍ debe estar funcionando)

1. **Bóveda de credenciales y archivos cifrados**
   - Cifrado AES-256 con clave maestra derivada (Argon2id o PBKDF2-SHA256, mínimo 600.000 iteraciones).
   - Sincronización con tu backend (CodeIgniter4 + MySQL).
   - Cifrado **client-side** (zero-knowledge): el servidor nunca ve la contraseña maestra ni los datos en claro.
   - Generador de contraseñas configurable.
2. **Verificador de filtraciones (HIBP)**
   - Integración con Have I Been Pwned API.
   - Dashboard de "tu salud digital".
3. **Analizador de URLs / phishing educativo**
   - Endpoint propio que consulta Google Safe Browsing + PhishTank.
   - Explicación heurística (typosquatting, IDN homograph, certificado, edad del dominio vía WHOIS).
4. **Escáner básico de red local**
   - Solo Android (porque iOS no deja). Listado de dispositivos en la LAN, fabricantes por OUI/MAC.
   - No prometas "auditoría WiFi profesional"; promete "qué hay en mi red".
5. **Roadmap de aprendizaje interactivo**
   - 3-5 itinerarios estáticos en JSON (Principiante, Pentest Web, Hardening Linux, Red Team intro, Defensa SOC).
   - Cada nodo: descripción + recursos enlazados (gratis: PortSwigger, TryHackMe gratuito, INCIBE, etc.) + mini-quiz.
6. **Panel de noticias**
   - Agregador RSS desde Hispasec, INCIBE-CERT, BleepingComputer, The Hacker News, Krebs on Security.
   - Orquestado con **n8n** que cachea el feed en tu base de datos cada hora.
7. **Gamificación básica**
   - Puntos, logros, racha diaria de "hábitos seguros".
8. **Cuentas de usuario + autenticación 2FA**
   - JWT + TOTP (RFC 6238). Demuestra que sabes lo que predicas.

### 🟡 PROTOTIPO / DEMO (suficiente con que se vea funcionando)

- Asistente IA para explicar hallazgos (con OpenAI/Anthropic API y créditos limitados).
- Modo familiar (UI mockup + 1 caso de uso real).
- Generador de informe PDF de "auditoría de vida digital".

### 🔵 LÍNEAS FUTURAS (documentas en sección 9 del TFG)

- App de escritorio (Electron/Tauri) para escaneo Nmap real.
- Laboratorios virtuales propios.
- Versión empresarial multi-usuario.
- Integración con Active Directory / SSO.
- Marketplace de cursos.

**Esto te da una memoria honesta y madura, que es lo que califica bien en un TFG.**

---

## 5. STACK TECNOLÓGICO RECOMENDADO

Aprovecho que ya conoces **PHP, CodeIgniter4, Ionic, ddev y n8n** porque te ahorrará semanas de aprendizaje y son perfectamente válidas. Te razono cada elección.

### 5.1. Frontend (multi-plataforma)

**🥇 Recomendación: Ionic + Angular (o React si prefieres) + Capacitor**

- **Por qué:** ya lo usas, es exactamente para apps multiplataforma, y Capacitor permite acceder a APIs nativas (WiFi en Android, almacenamiento seguro, biometría) que necesitarás.
- **Plugins clave de Capacitor:**
  - `@capacitor/preferences` o `@capawesome/capacitor-secure-storage` (claves cifradas con Keychain/Keystore).
  - `@capacitor-community/network` (info de red).
  - `@capacitor/biometric-auth` (Face ID / huella).
  - `@capacitor/local-notifications`.
  - Para WiFi en Android: `@capacitor-community/wifi` o un plugin custom envolviendo `WifiManager`.

**Alternativas (no las recomiendo, pero por contraste):**
- Flutter: más rendimiento, pero no lo manejas → coste de aprendizaje alto.
- React Native: similar a Flutter en pros/contras.

### 5.2. Backend / API

**🥇 Recomendación: CodeIgniter 4 + PHP 8.2+**

- **Por qué:** lo manejas de tu empresa. CI4 tiene Shield (autenticación), validación, ORM (Query Builder), filtros... suficiente para todo lo que necesitas.
- **Librerías clave:**
  - **Shield** (auth oficial CI4) → 2FA, password policy, sesiones.
  - **libsodium** (extensión PHP nativa) → todo el cifrado server-side.
  - **firebase/php-jwt** → JWT.
  - **chillerlan/php-qrcode** → QR para configurar TOTP.
  - **PragmaRX/Google2FA** → TOTP/2FA.

> Importante: para cifrado **prefiere libsodium sobre OpenSSL/mcrypt**. Es lo moderno, lo que recomiendan PHP, OWASP y los criptógrafos.

### 5.3. Base de datos

**🥇 Recomendación: MariaDB 10.11+ o MySQL 8**

- Encaja con CI4, ddev y tu flujo de trabajo.
- **Importante:** los blobs cifrados (bóveda) van como `LONGBLOB` o `MEDIUMTEXT` (base64).
- Plantéate añadir **Redis** para cache de feeds y rate limiting (n8n + CI4 lo usan bien).

### 5.4. Entorno de desarrollo

**🥇 Recomendación: ddev**

- Te da PHP + MariaDB + Nginx + Mailhog en docker, configurado, idéntico en todos los entornos.
- Repositorio reproducible: `git clone` + `ddev start` y listo.
- Buen punto en el TFG: demuestra DevOps básico.

### 5.5. Automatizaciones / orquestación

**🥇 Recomendación: n8n**

Tu n8n es el cerebro del **panel de noticias y alertas proactivas**:
- Workflow 1: Cron horario → fetch RSS de fuentes (Hispasec, BleepingComputer, INCIBE) → normaliza → guarda en MySQL.
- Workflow 2: Cron diario → consulta CVE NVD API por palabras clave (Windows, Android, Chrome) → notifica vía push si hay críticos.
- Workflow 3: webhook desde la app cuando un usuario reporta una URL → análisis enriquecido + respuesta.
- Workflow 4: cron semanal → genera "tu informe semanal de seguridad" por email.

> Punto fuerte para tu TFG: demuestras integración de microservicios y orquestación moderna.

### 5.6. Inteligencia Artificial / LLM

**🥇 Recomendación: API de Anthropic (Claude Haiku 4.5) o OpenAI (gpt-4o-mini)**

- Para el asistente didáctico. Coste real: céntimos por usuario.
- Si quieres self-hosted (interesante para el TFG): **Ollama + Llama 3.1 8B** o **Mistral 7B** en una VPS. Más complejo pero impresiona.
- **No le pidas al LLM cosas críticas de seguridad** (verificar URLs maliciosas). El LLM explica; el motor heurístico decide.

### 5.7. APIs externas (gratuitas o freemium)

| API | Uso | Coste |
|---|---|---|
| **Have I Been Pwned** | Filtraciones | 4 €/mes (acceso v3) |
| **Google Safe Browsing** | URLs maliciosas | Gratis |
| **PhishTank** | URLs phishing | Gratis (registro) |
| **VirusTotal** | Análisis archivos/URLs | Gratis 4 req/min |
| **NVD CVE API** | Vulnerabilidades | Gratis |
| **WHOIS / RDAP** | Edad y datos de dominio | Gratis (ICANN) |
| **NewsAPI** | Noticias | Gratis con límite |
| **OUI lookup (IEEE)** | Fabricante por MAC | Gratis (offline DB) |

### 5.8. Otras tecnologías a considerar

- **Tailwind CSS** + **Ionic UI components** → estética rápida y limpia.
- **PostHog / Plausible** → analítica anónima respetuosa con privacidad. Coherente con la filosofía de la app.
- **Sentry** → monitorización de errores.
- **GitHub Actions** → CI/CD básico.

### 5.9. Lo que NO recomiendo

- ❌ **Java/Kotlin nativo + Swift nativo**: doble código para una persona.
- ❌ **Laravel** en lugar de CI4: añade aprendizaje sin beneficio claro para tu caso.
- ❌ **MongoDB**: relacional encaja mejor con usuarios/credenciales/permisos.
- ❌ **Spring Boot / .NET**: te alejan de tu zona de confort sin necesidad.

---

## 6. ARQUITECTURA TÉCNICA PROPUESTA

```
┌────────────────────────────────────────────────────────────────┐
│                       CLIENTE (Ionic)                          │
│  - Cifrado client-side (libsodium.js / WebCrypto API)          │
│  - Almacenamiento seguro (Keychain / Keystore vía Capacitor)   │
│  - Biometría / PIN local                                       │
└──────────────────┬─────────────────────────────────────────────┘
                   │ HTTPS + JWT
                   ▼
┌────────────────────────────────────────────────────────────────┐
│              API REST (CodeIgniter 4 + PHP 8.2)                │
│  - /auth (Shield + 2FA TOTP)                                   │
│  - /vault (CRUD blobs cifrados — el server NUNCA descifra)     │
│  - /scan/url, /scan/email (consultas a APIs externas)          │
│  - /roadmap, /news, /achievements                              │
└─────────┬──────────────────────────────────────┬───────────────┘
          │                                      │
          ▼                                      ▼
   ┌──────────────┐                       ┌─────────────────┐
   │  MariaDB     │                       │  n8n            │
   │  (cifrada)   │                       │  - RSS fetcher  │
   └──────────────┘                       │  - CVE watcher  │
                                          │  - Notif. push  │
                                          └────────┬────────┘
                                                   │
                                                   ▼
                                          ┌─────────────────┐
                                          │  APIs externas  │
                                          │  HIBP, GSB,     │
                                          │  PhishTank,     │
                                          │  NVD, RSS       │
                                          └─────────────────┘
```

### Principios clave

- **Zero-knowledge en la bóveda**: el servidor recibe blobs ya cifrados. Si te roban la BBDD, los datos siguen seguros.
- **Defense in depth**: TLS + JWT + 2FA + cifrado client-side + cifrado en reposo en BBDD.
- **Privacy by design**: nada de tracking invasivo, analítica anónima y agregada.
- **Separation of concerns**: la app no consume directamente las APIs externas (n8n hace de proxy + cache).

---

## 7. CALENDARIO Y PRESUPUESTO

### 7.1. Calendario realista (Gantt orientativo, 4-5 meses)

Asume 4h/día × 20 días/mes = ~80h/mes. Total ~320-400h.

| Mes | Bloque |
|---|---|
| **Mes 1** | Investigación, diseño UX/UI (Figma), modelado BBDD, mockups, redacción de memoria parte 1-4. |
| **Mes 2** | Backend CI4 base + auth + bóveda con cifrado. Pruebas unitarias del módulo cripto. |
| **Mes 3** | Frontend Ionic core + integración auth + bóveda. Inicio módulos URL scanner y HIBP. |
| **Mes 4** | n8n flujos noticias + CVE. Roadmap interactivo. Gamificación. Asistente IA. |
| **Mes 5** | Pulido, testing, redacción final memoria, vídeo demo, defensa. |

### 7.2. Recursos humanos (TFG individual)

- 1 desarrollador (tú): ~360 h × ~15 €/h estudiante junior = **5.400 €** (coste imputado, no real).

### 7.3. Recursos materiales (presupuesto orientativo)

| Concepto | Coste |
|---|---|
| Portátil / equipo (ya disponible) | 0 € |
| VPS para backend + n8n (Hetzner CX22, 12 meses) | ~50 € |
| Dominio | 12 € |
| Certificado TLS (Let's Encrypt) | 0 € |
| HIBP API key (1 año) | 48 € |
| Anthropic / OpenAI créditos demo | 30 € |
| Cuenta Apple Developer (si vas a iOS) | 99 € |
| Cuenta Google Play Console (one-time) | 25 € |
| Licencias software (todo libre o gratis) | 0 € |
| **Total material** | **~265 €** |

### 7.4. Presupuesto total

| Partida | Importe |
|---|---|
| Personal (imputado) | 5.400 € |
| Material e infraestructura | 265 € |
| Imprevistos (10 %) | 567 € |
| **TOTAL** | **~6.232 €** |

> Para tu TFG, este presupuesto es ficticio (eres tú quien trabaja). Pero ese es el formato que pide el centro.

---

## 8. CONSIDERACIONES LEGALES Y ÉTICAS — CRÍTICAS

Tu TFG va de **ciberseguridad para usuarios**. Si no tratas estos puntos, el tribunal te va a preguntar.

### 8.1. RGPD / LOPDGDD

- **Tratas datos personales** (emails, posiblemente contraseñas hash): debes incluir política de privacidad + términos.
- **Consentimiento explícito** para consultar HIBP con el email del usuario.
- **Derecho al olvido**: el usuario puede borrar su cuenta y sus datos.
- **Cifrado en reposo** y minimización de datos.
- **DPO (Delegado de Protección de Datos)**: un usuario individual no necesita, pero si comercializas como empresa, sí.

### 8.2. Auditoría de redes — frontera legal

- Escanear **tu propia red doméstica** = legal.
- Escanear redes de terceros sin permiso = **delito (art. 197 bis CP en España, intrusión informática)**.
- **La app debe forzar el consentimiento** al iniciar el escáner ("Confirmo ser propietario o tener autorización"). Documenta esto en la memoria.

### 8.3. Distribución y licencias

- Si liberas como open source: **GPL v3** o **AGPL v3** (recomendado para evitar que un tercero monetice sin contribuir).
- Si comercializas: licencia propietaria + términos claros.

### 8.4. Seguridad de tu propia infraestructura

- Tu app es de seguridad: si te hackean a ti, el daño reputacional es enorme.
- Mínimo: **HTTPS estricto, HSTS, CSP, rate limiting, logging de accesos, backups cifrados, plan de respuesta a incidentes**.
- Documenta el modelo de amenazas (STRIDE) en la memoria. Eso impresiona al tribunal.

---

## 9. CAMBIOS Y MEJORAS RECOMENDADAS AL DOCUMENTO ACTUAL

Tu documento actual (PDF) tiene la estructura correcta del centro, pero le falta contenido. Te detallo qué completar en cada sección:

### 9.1. Cambios al título y subtítulo

- ✅ "ARGOS" perfecto.
- 🔧 Subtítulo actual: *"Suite Integral de Ciberseguridad, Gestión de Identidad y Auditoría de Redes para el Usuario Final"* — está bien pero promete demasiado. Considera: *"Plataforma educativa y de protección digital para el usuario doméstico"*.

### 9.2. Justificación

- Añade **datos** (con fuentes citadas):
  - Informe INCIBE de balance anual (incidentes en hogares).
  - Verizon DBIR (Data Breach Investigations Report).
  - ENISA Threat Landscape.
  - "El 82 % de las brechas implican el factor humano" (DBIR).
- Define **público objetivo** concreto: usuario doméstico de 25-65 años con uso intensivo digital pero sin formación técnica + estudiantes que se inician.
- Añade **una persona/usuario tipo** (Anabel, 38 años, autónoma, le hicieron phishing en su Gmail...).

### 9.3. Plan de trabajo

Te falta *todo* el plan. Convierte el calendario de la sección 7.1 en tu plan de trabajo, dividiendo en etapas con la plantilla del centro:

```
Etapa 1: Análisis y diseño
Ref: E1
Objetivo: Definir requisitos, arquitectura y diseño UX
Trabajos:
  - Estudio de mercado (competencia)
  - Diagrama de casos de uso
  - Modelado entidad-relación
  - Wireframes en Figma
  - Modelo de amenazas STRIDE
Dificultades previsibles: alcance excesivo, decidir qué descartar
Resultados esperados: documento de requisitos + diseño aprobado
Duración: 4 semanas
RR.HH.: 1 desarrollador (160h)
RR.MM.: portátil, Figma, draw.io
Presupuesto: 1.500 €
Responsable: Saúl Álvarez Monzón
```

Replica esta plantilla para cada bloque (Backend, Frontend, Integraciones, Pruebas, Memoria).

### 9.4. Calendario / Gantt

- Construye el Gantt **real** con 18-20 semanas y dependencias (la implementación frontend depende del modelado de la API).
- Herramientas gratuitas: TeamGantt (limitado), GanttProject (open source), o tabla manual en Markdown/Sheets.

### 9.5. Evaluación

- Define **KPIs**:
  - Cobertura de tests > 70 %.
  - Tiempo de respuesta API < 300 ms p95.
  - Score Lighthouse PWA > 85.
  - 0 vulnerabilidades críticas en `composer audit` y `npm audit`.
  - Test de usuario con 5 personas no técnicas: tiempo en completar onboarding < 10 min.
- Hitos de control: revisión cada 2 semanas con tutor.

### 9.6. Conclusiones

Cuando llegues, asegúrate de:
- Responder **uno a uno** a los objetivos específicos: "Objetivo 1 alcanzado al X %, Objetivo 2 parcialmente porque...".
- Reconocer **limitaciones** (gran punto a favor):
  - "iOS no permite escaneo WiFi sin entitlement empresarial".
  - "El alcance de los entornos de laboratorio se redujo a enlaces externos por viabilidad técnica".
- Líneas futuras (sección 4 "🔵" de esta guía).

---

## 10. CONSEJOS FINALES

### 10.1. De producto

- **Demo > documentación**. Un vídeo de 3 min con la app funcionando vale más que 50 páginas. Empieza pronto a pensar en la demo.
- **Mide en usuarios reales**. Pídeles a 5 amigos no técnicos que usen ARGOS 1 semana. El feedback es oro y sale en la memoria.
- **Diseña primero la UI** (Figma), construye después. Cambia 100x más barato en Figma que en código.
- **Mantén un changelog** desde el día 1. El tribunal puede preguntarte cómo evolucionó tu enfoque.

### 10.2. De memoria del TFG

- **Cita fuentes con norma APA o IEEE**. Tu centro probablemente exige una.
- **Capturas de pantalla constantes** del producto en construcción.
- **Diagramas claros**: flujo de cifrado, arquitectura, ER de BBDD, sequence diagrams para flujos críticos (login + 2FA, cifrado de bóveda).
- **Justifica TODA decisión técnica**: "elegí libsodium en lugar de OpenSSL porque OWASP recomienda...".
- **Anexa el código** o link al repo (privado con acceso al tribunal).

### 10.3. De gestión personal

- **Empieza ya con la memoria**, no la dejes para el último mes. Escribe un poco cada semana.
- **Versionalo todo en Git desde día 1**, con commits limpios. El historial Git puede formar parte del anexo.
- **Backup off-site**: GitHub privado + copia local + copia en Drive. Un disco duro muerto a 2 semanas de la entrega arruina TFGs.
- **Habla con tu tutor cada 2 semanas**. Sin sorpresas el día de la entrega.

### 10.4. De cara a la defensa

- **3-4 minutos de demo en vivo + 3 min de slides + 4 min de preguntas**.
- Prepara el "**plan B**": si la app cae en directo, ten un vídeo grabado de respaldo.
- Practica explicando el cifrado **a alguien NO técnico**. Si te entiende tu madre, te entiende el tribunal.

### 10.5. De carrera profesional

- **ARGOS puede ser tu portfolio** después del TFG. Súbelo como demo pública (con disclaimer de proyecto académico).
- **Habla en LinkedIn del proceso** mientras lo haces. Atrae empleo.
- **Considera certificaciones complementarias**: eJPT (gratis-barata), CompTIA Security+, INCIBE-CERT cursos gratis. Refuerzan el currículum más allá del TFG.

---

## 11. PRÓXIMOS PASOS INMEDIATOS PARA TI

En este orden, dedícale ~1 semana a cada uno:

1. **Decide el alcance final** usando la sección 4 (núcleo / prototipo / futuro). Cierra qué SÍ y qué NO entra.
2. **Reescribe la justificación** con datos, persona-usuario y un párrafo claro de competencia y diferenciación.
3. **Diseña la arquitectura y BBDD** sobre papel/Figma antes de escribir código.
4. **Monta `ddev` con CI4 vacío + n8n + MariaDB**. Versionalo en Git.
5. **Implementa el primer slice vertical**: registro + login + crear una entrada en bóveda + verla. End-to-end. Eso te da confianza y valida el stack.
6. **A partir de ahí**, itera por módulos (HIBP → URL scanner → roadmap → noticias → gamificación).

---

## 12. RESUMEN EJECUTIVO

| Pregunta | Respuesta corta |
|---|---|
| ¿La idea es buena? | Sí, sólida y con hueco real de mercado. |
| ¿El alcance actual es viable? | No, tienes que recortarlo al MVP de la sección 4. |
| ¿Stack recomendado? | Ionic + CodeIgniter4 + MariaDB + ddev + n8n + APIs externas. |
| ¿Mayor diferenciador realista? | Idioma español + onboarding por nivel + gamificación + asistente IA + agregador de noticias propio. |
| ¿Mayor riesgo? | Ámbito legal de "auditoría de redes". Acotar a red propia + consentimiento explícito. |
| ¿Tiempo total estimado? | 360-400 h (4-5 meses a media jornada). |
| ¿Coste real material? | ~265 €. |
| ¿Competidores directos? | Norton/Bitdefender (sin formación) + HTB/THM (sin protección práctica). Ninguno combina las dos cosas. |

---

> **Nota final:** este documento es una guía orientativa. Las decisiones técnicas y de alcance las tomas tú con tu tutor del TFG. Mi recomendación más importante: **recorta alcance, ejecuta menos pero mejor, y documenta todo**. Un proyecto pequeño bien hecho > un proyecto enorme a medias.

¡Mucho éxito con ARGOS, Saúl! 🛡️
