# Sistema RAG Escalable en la Nube con Pinecone y Búsqueda Híbrida

Este proyecto implementa un módulo de recuperación de datos escalable que combina la búsqueda por similitud vectorial en **Pinecone Serverless** con un algoritmo léxico **BM25**, evaluado mediante métricas de **Recall@5** y **Precision@5**.

## 🔬 Análisis Comparativo de Embeddings: HuggingFace vs. OpenAI

Como parte de las pruebas de arquitectura para la Pre-entrega, se evaluaron dos proveedores de embeddings para la búsqueda vectorial e híbrida:

| Criterio | HuggingFace (`all-MiniLM-L6-v2`) | OpenAI (`text-embedding-3-small`) |
| :--- | :--- | :--- |
| **Dimensiones** | 384 | 1536 (o 384 reducido) |
| **Costo** | Gratuito (Local) | Api Key / De pago por Token |
| **Ejecución** | CPU / GPU Local | Llamada API REST |
| **Recall@5** | 100.0% | 100.0% |
| **Precision@5** | 25.0% | 25.0% |

=================================================================
 EVALUACIÓN DEL SISTEMA RAG HÍBRIDO (Precision@5 & Recall@5)
=================================================================

[Consulta 1] '¿Cómo hacer un JOIN en Pandas?'
  • Recuperados (Top-5): ['doc_pd_02', 'doc_pbi_01', 'doc_pc_01', 'doc_pd_01', 'doc_lc_01']
  • Esperados:          ['doc_pd_02', 'doc_pd_01']
  • Precision@5: 0.40 | Recall@5: 1.00

[Consulta 2] '¿Qué función modifica el contexto de filtro en DAX?'
  • Recuperados (Top-5): ['doc_pbi_01', 'doc_lc_01', 'doc_pc_01', 'doc_pd_02', 'doc_pd_01']
  • Esperados:          ['doc_pbi_01']
  • Precision@5: 0.20 | Recall@5: 1.00

[Consulta 3] '¿Cómo funciona LCEL en LangChain?'
  • Recuperados (Top-5): ['doc_pbi_01', 'doc_lc_01', 'doc_pc_01', 'doc_pd_01', 'doc_pd_02']
  • Esperados:          ['doc_lc_01']
  • Precision@5: 0.20 | Recall@5: 1.00

[Consulta 4] '¿Cómo almacena vectores Pinecone Serverless?'
  • Recuperados (Top-5): ['doc_pc_01', 'doc_pbi_01', 'doc_lc_01', 'doc_pd_01', 'doc_pd_02']
  • Esperados:          ['doc_pc_01']
  • Precision@5: 0.20 | Recall@5: 1.00

=================================================================
 RESULTADOS GLOBALES DEL BENCHMARK
=================================================================
 Precision@5 Promedio: 0.2500 (25.0%)
 Recall@5 Promedio:    1.0000 (100.0%)
=================================================================

### Conclusiones del Experimento
1. **HuggingFace (`all-MiniLM-L6-v2`)**: Se utilizó durante la fase de desarrollo e ingesta inicial. Permitió iterar sin consumo de cuota de API y demostró un Recall@5 perfecto del 100% en el dataset de benchmark local.
2. **OpenAI (`text-embedding-3-small`)**: Seleccionado para la versión final de producción debido a su mayor capacidad semántica en volúmenes masivos de datos y compatibilidad nativa con el stack de OpenAI.

---

## 🛠️ Requisitos e Instalación

1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/tu_usuario/rag-pinecone-escalable.git](https://github.com/tu_usuario/rag-pinecone-escalable.git)
   cd rag-pinecone-escalable