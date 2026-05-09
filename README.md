# Plan de crecimiento profesional — Eduardo / dev-7.com

**Horizonte:** 12 meses
**Punto de partida:** Mid-Senior con dominio fuerte en Django + Vue + SAP B1
**Meta:** Senior consolidado + primer producto SaaS en producción + operación menos dependiente de ti

---

## Filosofía del plan

Tres principios no negociables:

1. **Menos frentes, más profundidad.** Cada nuevo proyecto que aceptes este año debe servir a uno de los objetivos de abajo. Si no, di que no o súbele 40% al precio.
2. **Sistemas, no heroísmos.** Cada problema que resuelves dos veces se convierte en plantilla, script o documento.
3. **Activos sobre horas.** Cada hora trabajada debe dejar algo reutilizable: código, contenido, proceso o cliente recurrente.

---

## Bloque 1 — Fundamentos técnicos a reforzar (meses 1-3)

### 1.1 Testing serio en Django

Hoy mencionas pytest pero no veo cobertura sistemática. Esto es lo que separa Mid de Senior.

**Qué aprender / aplicar:**
- pytest-django con factories (factory_boy)
- Tests de integración para vistas y APIs (DRF test client)
- Tests con bases de datos reales (no SQLite en testing si producción es PostgreSQL)
- Mocking de servicios externos (responses, pytest-mock) — crítico para SAP B1 y APIs externas
- Cobertura mínima 70% en código de negocio (coverage.py)

**Entregable:** SAP-Flexy WMS con suite de tests >70% cobertura, ejecutándose en GitHub Actions en cada push.

### 1.2 CI/CD y GitHub Actions

**Qué aprender / aplicar:**
- Workflows de GitHub Actions: lint, test, build
- Despliegue automatizado a tu VPS vía SSH + rsync o Docker
- Versionado semántico y changelogs automáticos
- Branch protection rules y PR templates

**Entregable:** Pipeline funcional en al menos 3 proyectos (SAP-Flexy, mantis/peisol, kosmo) con deploy automático a staging.

### 1.3 Observabilidad

Operas 7+ servicios sin observabilidad real. Esto es deuda técnica grave.

**Qué aprender / aplicar:**
- Sentry para captura de errores (Django + Vue)
- Logs estructurados con structlog o python-json-logger
- Healthchecks endpoints + UptimeRobot o BetterStack
- Métricas básicas con Prometheus + Grafana, o alternativa simple como Netdata
- Alertas a Slack o Telegram cuando algo se cae

**Entregable:** Dashboard único donde ves el estado de tus 7 servicios + alertas activas.

### 1.4 Docker y orquestación

Ya usas Docker para SGI. Falta sistematizarlo.

**Qué aprender / aplicar:**
- Dockerfiles multi-stage optimizados para Django y Vue
- docker-compose para entornos de desarrollo idénticos a producción
- Volúmenes y networking correctamente
- Despliegue con docker-compose en VPS o migración futura a algo como Coolify o Dokploy

**Entregable:** Template base dev-7 con docker-compose que cualquier nuevo proyecto pueda heredar.

---

## Bloque 2 — Sistemas internos de dev-7.com (meses 1-4)

### 2.1 Template base de proyecto (cookiecutter)

Hoy cada proyecto arranca de cero. Esto te quema 2-3 días por proyecto.

**Qué construir:**
- Cookiecutter con Django 4.2 + DRF + PostgreSQL + Vue 3 + Pinia + Tailwind + Vite
- Pre-configurado: Sentry, structlog, GitHub Actions, docker-compose, pytest, ruff/black
- Variables de configuración por entorno (django-environ)
- Modelo base con auditoría (created_at, updated_at, created_by)
- Sistema de permisos base (Grappelli configurado)
- Documentación de uso del template

**Entregable:** `cookiecutter dev7-django-vue` que crea proyecto listo en 5 minutos.

### 2.2 Catálogo de soluciones reutilizables

Eres bueno adaptando — formaliza ese activo.

**Qué hacer:**
- Repositorio privado `dev-7/snippets` con: integración SAP DI API, autenticación JWT con refresh, exportación a Excel, importación desde Excel, generación PDF (xhtml2pdf o WeasyPrint), CRUDs estándar Django+Vue, integración n8n
- Cada snippet con: README de uso, ejemplo funcional, tests
- Commit nuevo cada vez que resuelvas algo que hayas resuelto antes

**Entregable:** Mínimo 15 snippets documentados en 4 meses.

### 2.3 Documentación de operaciones

Eres SPOF. Si te enfermas, todo se cae.

**Qué hacer:**
- Runbook por servicio: cómo desplegar, cómo reiniciar, qué hacer si X falla, dónde están las credenciales (referencias, no valores)
- Mapa de infraestructura: qué corre dónde, qué dominio apunta a qué, qué backup tiene cada DB
- Lista de dependencias críticas con SLAs (DigitalOcean, Cloudflare, registros DNS, certificados)
- Procedimiento de recovery por escenario (DB caída, VPS caída, certificado expirado, etc.)

**Entregable:** Wiki interna en Notion o BookStack autoalojado con runbooks de los 7 servicios.

---

## Bloque 3 — SaaS: del proyecto al producto (meses 3-12)

### 3.1 Decisión: cuál SaaS primero

Tienes 3 ideas: inventario, mantenimiento, flores. **Elige una. Solo una.**

Criterios para decidir:
- ¿Cuál tiene clientes que ya pagarían hoy en tu red? (Recomendación inicial: inventario, dado tu expertise SAP B1)
- ¿Cuál puedes lanzar como MVP en 8 semanas?
- ¿Cuál tiene menos competencia hispanohablante en LATAM?

**Entregable mes 3:** documento de 2 páginas eligiendo el SaaS, con: problema, segmento, 5 prospects nombrados, pricing tentativo, MVP scope.

### 3.2 MVP del SaaS (meses 4-8)

**Estructura sugerida (asumiendo SaaS de auditoría de inventario SAP):**

- Multitenancy en Django (django-tenants o esquema de filtros)
- Onboarding self-service con conexión a SAP B1 vía DI API o Service Layer
- Dashboard Vue 3 con métricas clave de inventario
- Reporte automatizado semanal por email
- Stripe o local payment gateway (PayPhone para Ecuador) para suscripciones
- Plan free + plan pago desde el día 1

**Disciplina:** 10 horas a la semana bloqueadas en calendario. No negociables. Mismo día y hora cada semana.

**Entregable mes 8:** MVP funcional con primer cliente pagando, aunque sea USD 50/mes.

### 3.3 Distribución (meses 6-12)

Construir producto sin distribución es el error #1.

**Qué hacer en paralelo al MVP:**
- 1 post técnico mensual en LinkedIn sobre SAP B1 + Python (autoridad en nicho)
- Lista de email con suscriptores interesados (ConvertKit free, MailerLite)
- Caso de estudio del primer cliente (con su permiso)
- Presencia en comunidades: foros SAP B1, grupos Telegram/WhatsApp de consultores SAP en LATAM

**Entregable mes 12:** 3-5 clientes pagando, USD 500-1500 MRR. Es el inicio, no el final.

---

## Bloque 4 — Modelo de negocio y pricing (meses 1-12, transversal)

### 4.1 Reestructura de pricing

**Qué cambiar ya:**
- Tu próxima propuesta nueva: +25% sobre lo que ibas a cobrar. Justifica scope, no negocies.
- Define 3 paquetes claros para clientes nuevos: Diagnóstico (USD fijo bajo, 1 semana), Proyecto (USD fijo medio, 4-8 semanas), Retainer mensual (USD fijo recurrente)
- Nunca más cobres por hora puntual sin retainer.

**Entregable:** Página de servicios en dev-7.com con 3 paquetes y rangos de precio públicos.

### 4.2 Filtro de clientes

**Reglas:**
- No aceptes proyecto < USD 3,000 a menos que sea estratégico (entrada a un cliente grande)
- No aceptes cliente que no firma SOW antes de empezar
- No aceptes proyecto sin 50% upfront

### 4.3 Contratación de junior part-time (mes 6-9)

Cuando el cashflow lo permita:
- Junior Django/Vue, 20 hrs/semana, remoto
- Empieza con tareas mecánicas: tests, documentación, fixes pequeños, mantenimiento de servicios
- Tu tiempo liberado va exclusivamente al SaaS

**Entregable:** Junior contratado y produciendo antes del mes 9.

---

## Bloque 5 — Marca personal y autoridad (meses 1-12)

### 5.1 Posicionamiento

dev-7.com no compite con cualquier desarrollador genérico. Posicionate como:

> **"Integración SAP Business One con stack moderno (Django + Vue) para empresas en LATAM"**

Es un nicho con alta demanda, baja competencia hispanohablante, y exactamente donde tienes ventaja real.

### 5.2 Contenido público

**Disciplina mensual:**
- 1 post técnico largo en LinkedIn (800-1200 palabras): caso real, problema, solución, resultado
- 2-4 posts cortos por semana sobre aprendizajes pequeños
- 1 README/repo público útil cada 2 meses (snippets, plantillas, herramientas)

**Temas que tienes y pocos cubren:**
- DI API vs Service Layer en SAP B1: cuándo usar cuál
- Patrón outbox aplicado a integración SAP
- n8n vs Django para lógica de negocio: cuándo cada uno
- Optimización PostgreSQL para apps Django con SAP B1 como fuente
- Despliegues sin Kubernetes: Nginx + Gunicorn + systemd que funciona

### 5.3 Página dev-7.com como activo

Hoy parece marca operativa. Conviértela en captador de leads:
- Casos de estudio (con métricas: "reducimos query de 9 min a 30s")
- Blog técnico con SEO en español ("integrar SAP B1 con Python", "alternativas a iVend para SAP")
- Lead magnet: "Guía: Integrar SAP B1 con Django paso a paso" a cambio de email
- Testimonios de clientes actuales

**Entregable mes 6:** Sitio renovado con casos, blog y lead magnet activos.

---

## Cronograma resumido

| Mes | Foco principal | Hito clave |
|-----|----------------|------------|
| 1 | Testing + observabilidad en SAP-Flexy | Sentry y healthchecks corriendo |
| 2 | CI/CD + Docker base | Pipeline en 3 proyectos |
| 3 | Cookiecutter dev-7 + decisión SaaS | Template usable + SaaS elegido |
| 4 | Snippets + diseño MVP SaaS | 5 snippets + spec del MVP |
| 5 | MVP SaaS desarrollo | Auth, multitenancy, dashboard básico |
| 6 | Sitio dev-7 + MVP avanzado | Sitio nuevo + MVP integración SAP funciona |
| 7 | MVP beta cerrado + contenido | 3 betatesters usando + 6 posts publicados |
| 8 | Lanzamiento MVP + primer cliente | Primer USD/mes recurrente |
| 9 | Contratación junior + retainers | Junior on-board + 1-2 retainers firmados |
| 10 | Iteración SaaS + casos de estudio | 3 clientes en SaaS + 2 casos publicados |
| 11 | Optimización y autoridad | MRR USD 500+ + presencia consolidada |
| 12 | Revisión y plan año 2 | Decisiones sobre escalar SaaS o seguir consultoría |

---

## Métricas de éxito al mes 12

**Técnicas:**
- Cobertura de tests >70% en proyectos principales
- 0 servicios sin observabilidad activa
- Tiempo de despliegue < 5 minutos automatizado
- Template base usado en 100% de proyectos nuevos

**Negocio:**
- MRR del SaaS: USD 500-1500
- Pricing promedio por proyecto: +25% sobre línea base actual
- 1 junior contratado y productivo
- 2 retainers mensuales activos

**Marca:**
- 12 posts técnicos largos publicados
- Sitio dev-7.com con 3+ casos de estudio reales
- Lista de email > 200 suscriptores en nicho

**Personal:**
- Capacidad de tomar 2 semanas de vacaciones sin que nada crítico falle
- 10 horas semanales fijas en producto, no negociables

---

## Reglas de oro durante el plan

1. **Si algo te toma más de 2 horas y lo has hecho antes, mételo a snippets.**
2. **Cada cliente nuevo paga con el pricing nuevo, sin excepciones.**
3. **Las 10 horas semanales del SaaS son sagradas. No se mueven por urgencias de clientes.**
4. **Cada problema resuelto en producción genera un runbook nuevo.**
5. **Cada mes revisa este plan. Lo que no avanzó, pregúntate por qué.**

---

## Cierre franco

Este plan es ambicioso pero realista para alguien con tu base técnica. El 80% del éxito no será aprender cosas nuevas — eso lo haces bien. Será **decir que no, mantener disciplina semanal, y resistir la tentación de aceptar un proyecto urgente que rompa el bloque del SaaS**.

El que ejecuta este plan en 12 meses no es el mismo profesional que lo empezó. Es un Senior consolidado con un activo propio y opcionalidad real sobre su carrera.

A ejecutar.
