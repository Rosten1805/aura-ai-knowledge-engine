# AURA — AI Knowledge Engine

Proyecto final de Bootcamp y pieza de portfolio profesional orientada a los perfiles **Cloud Engineer**, **DevOps Engineer** y **AI Engineer**.

AURA es una plataforma de inteligencia documental: convierte archivos (PDF, DOCX, TXT, Markdown) en conocimiento consultable mediante **Amazon Bedrock** y una arquitectura **RAG** (Retrieval-Augmented Generation), desplegada sobre infraestructura real en AWS con automatización DevSecOps completa.

> **Estado actual: Fase 1 — Diseño.** Aún no hay código de aplicación ni infraestructura desplegada. El diseño detallado de la arquitectura, los diagramas, el presupuesto y las decisiones técnicas están en [ARCHITECTURE.md](ARCHITECTURE.md).

---

## ¿Qué hace AURA?

- **Gestión documental** — subir, almacenar en S3, indexar y eliminar documentos; consultar el estado de procesamiento.
- **Smart Chat** — preguntar sobre los documentos subidos y recibir respuestas generadas por Bedrock, con las fuentes citadas y reconocimiento explícito de cuándo falta información.
- **Document Compare** — comparar dos documentos para detectar diferencias, coincidencias y posibles contradicciones.
- **Deep Research** — responder preguntas complejas sintetizando evidencia de múltiples documentos en un informe con referencias verificables.
- **AI Evaluation** — medir calidad de recuperación y respuesta, latencia, tokens y coste estimado, y detectar regresiones al cambiar prompts o modelos.

Estas funcionalidades se construyen de forma progresiva: primero el motor RAG (Gestión documental + Smart Chat), y después las capacidades avanzadas.

## Stack tecnológico

| Capa | Tecnología |
|---|---|
| Backend | Python 3.12, FastAPI, Pydantic, Boto3 (LangChain solo donde aporta valor real) |
| IA | Amazon Bedrock (modelo Nova + embeddings), Bedrock Knowledge Bases, S3 Vectors |
| Infraestructura | Terraform, VPC multi-AZ, Amazon EKS, ALB, ECR, S3, Secrets Manager |
| CI/CD | Jenkins (Pipeline as Code) con SAST, SCA, secret scanning, IaC scanning, DAST y security gates |
| Observabilidad | Prometheus + Grafana + CloudWatch |

Detalle completo de la arquitectura, diagramas (infraestructura, flujo RAG, pipeline DevSecOps), presupuesto estimado y decisiones técnicas: ver [ARCHITECTURE.md](ARCHITECTURE.md).

## Metodología

El proyecto avanza en 10 fases verificables (diseño → backend → motor RAG → frontend → contenedorización → infraestructura AWS → Jenkins → observabilidad → funcionalidades avanzadas → entrega). No se avanza de fase sin verificar lo construido en la anterior. El detalle de cada fase y su estado está en [ARCHITECTURE.md](ARCHITECTURE.md#8-orden-de-implementación-resumen-de-fases).

## Restricciones del proyecto

- No se despliega ni destruye infraestructura en AWS sin aprobación explícita.
- No se inventan precios ni resultados de pruebas: todo coste y toda afirmación de funcionamiento se verifica antes de documentarse.
- Sin credenciales ni secretos permanentes en el repositorio; gestión vía AWS Secrets Manager e IAM de mínimos privilegios.

## Estructura del repositorio

```text
aura-ai-knowledge-engine/
├── backend/            # FastAPI, lógica de negocio, tests
├── frontend/           # Interfaz de usuario
├── infrastructure/     # Terraform (bootstrap, environments, modules)
├── kubernetes/         # Manifests de despliegue en EKS
├── jenkins/            # Jenkinsfile y pipeline DevSecOps
├── monitoring/         # Prometheus y Grafana
├── security/           # Políticas y configuración de seguridad
├── evaluations/        # Framework de evaluación de IA
├── docs/               # Diagramas y documentación adicional
└── scripts/            # Automatizaciones (arranque, apagado, utilidades)
```

## Próximos pasos

Con la Fase 1 aprobada, el siguiente paso es la **Fase 2**: definición de los endpoints FastAPI, los modelos Pydantic y la suite de tests del backend, sin tocar todavía infraestructura AWS.
