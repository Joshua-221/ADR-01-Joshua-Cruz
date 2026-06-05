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

---

## Decisión

Se decide adoptar formalmente el **Modelo de Vistas Arquitectónicas (Lógica, Procesos, Física y Despliegue)** para estandarizar la documentación técnica del sistema Grind Core. 

Como parte de esta definición de vistas, se toman las siguientes determinaciones tecnológicas específicas:
1. **Vista Lógica:** Mantener el patrón **.NET MVC**, pero migrar formalmente el entorno de ejecución de .NET Core a **.NET 10** para aprovechar las optimizaciones de rendimiento del JIT, recolección de basura optimizada y menor consumo de memoria. Los controladores canalizarán las peticiones HTTP y los modelos encapsularán tanto el esquema de PostgreSQL como las fórmulas de Powerlifting.
2. **Vista Física y Despliegue:** Adoptar un modelo híbrido descentralizado donde la base de datos **PostgreSQL** se aloja de manera administrada de forma remota (ej. Supabase/Neon) y el Servidor de Aplicación .NET 10 se despliega de forma independiente para facilitar escalabilidad horizontal futura.

### ¿Por qué?

- **Rendimiento Puro (.NET 10):** El procesamiento dinámico de algoritmos de powerlifting (calcular el e1RM instantáneo basándose en tablas de RPE y alertar sobre sobrecargas indeseadas) requiere la menor latencia de backend posible. .NET 10 ofrece mejoras críticas de compilación nativa AOT y optimizaciones de hardware para procesadores de silicio.
- **Trazabilidad de Procesos:** Definir una Vista de Procesos permite mitigar condiciones de carrera y asegurar que las transacciones de actualización de récords personales (PRs) mantengan una secuencia lógica estricta y predecible.
- **Alineación con Diagramas C1/C2:** Las vistas físicas y lógicas expanden de forma directa el contenedor detallado en nuestro diseño estático previo, permitiendo mapear los componentes en HTML5/Tailwind y .NET de manera fidedigna.

