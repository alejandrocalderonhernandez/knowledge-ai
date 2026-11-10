# AI Kata Framework · v1

Un método para que un humano y una AI construyan proyectos juntos sin perder contexto: qué documentos existen, quién escribe cada uno y cómo se combinan para obtener un entregable.

## La idea en una línea

**Reglas (cómo) + Contexto (qué) + Brief (esta vez) = Entregable**

## Conceptos clave

- **Kata:** un flujo reutilizable para un tipo de trabajo (p. ej. presentaciones técnicas).
- **Estáticos:** reglas y builders. No cambian entre proyectos.
- **Dinámicos:** el contexto de cada proyecto. Lo genera la AI con un builder a partir de tus insumos.
- **Brief:** lo que pides en el chat para un entregable concreto. No se guarda.
- **README:** el único archivo para humanos. Todo lo demás está escrito para la AI.

## Cómo se usa

1. **Etapa 1 — Construir:** dale a la AI el builder y tus insumos; di "listo"; responde sus preguntas (máx. 5). Obtienes el archivo de contexto.
2. **Monta el proyecto:** sube reglas + contexto a un proyecto de chat y usa el prompt de proyecto (plantilla en el manifiesto, sección 10).
3. **Etapa 2 — Producir:** manda un brief por cada entregable.

Cuando algo salga mal, corrige la regla o el builder y súbelo a Git. Las lecciones viven en archivos, no en el chat.

## Esta carpeta

| Archivo | Para quién | Qué tiene |
|---|---|---|
| `README.md` | Humanos | Este resumen |
| `MANIFEST.md` | AI (y humanos curiosos) | Las reglas completas del framework v1 |

## Estado

- **v1 resuelve:** entender al humano, archivos estáticos, archivos de salida y prompt de proyecto.
- **Siguiente:** estructura del repo, skills y agentes de Claude Code, portabilidad a otras herramientas.

Kata de referencia: presentaciones técnicas de *Debuggeando Ideas*.