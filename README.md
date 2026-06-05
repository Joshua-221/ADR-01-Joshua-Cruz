# ADR-02: Definición y Documentación de Vistas Arquitectónicas y Actualización de Runtime

| Campo  | Valor |
|--------|-------|
| Autor  | Joshua Cruz |
| Fecha  | 05/06/2026 |
| Estado | `Aceptado` |

---

## Contexto

Grind Core es una plataforma web centralizada diseñada para la gestión de atletas de Powerlifting y la optimización de entrenamientos basados en autorregulación. El sistema cuenta con dos roles principales definidos en nuestro modelo de contexto (C1): el **Atleta**, quien registra pesos, repeticiones y RPE; y el **Coach**, quien configura rutinas y supervisa cargas de trabajo. 

Para avanzar en el desarrollo y garantizar un estándar técnico riguroso, se va a documentar formalmente las decisiones de diseño mediante el modelo de vistas arquitectónicas, asegurando una separación clara de responsabilidades lógicas, dinámicas y de infraestructura. Además, surge la necesidad de evaluar el entorno de ejecución idóneo para mitigar la latencia en cálculos matemáticos pesados en tiempo real (estimaciones de fuerza y fatiga).


