
# MiniTransformer Didáctico — *Attention Is All You Need* (versión académica)

Este repositorio contiene una implementación **didáctica y explicable** de un modelo **Transformer Encoder–Decoder**, basada directamente en el paper:

> *Vaswani et al., 2017 — Attention Is All You Need*

El objetivo **NO** es competir con modelos grandes (GPT, BERT), sino **entender profundamente**:
- cómo fluye la información en un Transformer
- cómo se conectan las cajas del diagrama con código real en Python
- cómo un modelo pequeño puede *parecer que entiende* lenguaje natural dentro de un dominio acotado

---

## 📚 Contenido del repositorio

- `MiniTransformer_Didactico_AttentionIsAllYouNeed.ipynb`
  - Notebook principal con:
    - explicación teórica paso a paso
    - implementación en PyTorch
    - entrenamiento y generación token a token
- `dataset_emocional_*.txt`
  - Conjunto de datasets en formato texto (input \t output)
- `README.md`
  - Este documento

---

## 🎯 Dominio del modelo

El modelo trabaja sobre un **dominio acotado**:

> **Asistente emocional + cortesía básica + observaciones positivas/negativas**

Ejemplos de comportamiento esperado:

```text
IN : hola
OUT: hola

IN : me siento triste
OUT: lo siento

IN : el sol brilla
OUT: que bueno

IN : a pesar del esfuerzo no funciono
OUT: que triste
```

📌 El modelo **no entiende el mundo**, pero **aprende patrones estadísticos coherentes** dentro del dominio.

---

## 🧠 Diseño didáctico

Este proyecto prioriza:

- claridad conceptual sobre optimización
- correspondencia 1 a 1 con el diagrama del paper
- vocabulario controlado
- datasets explicables

### Simplificaciones conscientes

- Tokenización simple (`lower().split()`)
- Respuestas cortas (1–3 tokens)
- Dominio cerrado
- Tamaño reducido del modelo

Estas decisiones permiten **enseñar Transformers sin ruido innecesario**.

---

## 🏗️ Arquitectura del modelo

El modelo implementa un **Transformer Encoder–Decoder completo**:

```
Inputs
  ↓
Input Embedding
  ↓
Positional Encoding
  ↓
Encoder (N×)
  ↓
─────────────── memory ───────────────▶
                                       ↓
Outputs (shifted right)
  ↓
Output Embedding
  ↓
Positional Encoding
  ↓
Decoder (N×, masked self-attention + cross-attention)
  ↓
Linear
  ↓
Softmax
```

### Componentes clave

- **Multi-Head Self-Attention**
- **Masked Self-Attention (decoder)**
- **Cross-Attention (decoder → encoder memory)**
- **Feed Forward Networks**
- **Residual connections + LayerNorm**
- **Positional Encoding sinusoidal**

Todo está implementado usando `nn.Transformer` de PyTorch.

---

## ⚙️ Configuración recomendada (7,000 ejemplos)

```python
d_model = 48
nhead = 4
num_encoder_layers = 2
num_decoder_layers = 2
dim_feedforward = 128
dropout = 0.1

batch_size = 64
epochs = 30
learning_rate = 1e-3
max_len = 20
max_gen_len = 5
temperature = 0.8
```

📌 Esta configuración mantiene el modelo:
- suficientemente expresivo
- estable en entrenamiento
- explicable en pizarra

---

## 📊 Conteo de parámetros

El notebook incluye un bloque para contar **parámetros reales** del modelo:

```text
🔢 Total de parámetros        : ~70K
🧠 Parámetros entrenables     : ~70K
```

Esto permite comparar directamente con:
- GPT (billones)
- BERT (cientos de millones)

y entender **escala vs capacidad**.

---

## 🧪 Dataset

Formato de cada archivo `.txt`:

```text
<input_text>\t<output_text>
```

Ejemplo:

```text
me siento cansado    lo siento
el clima esta agradable    que bueno
gracias por tu ayuda    de nada
```

Todos los archivos pueden concatenarse directamente.

---

## ▶️ Ejecución

1. Instalar dependencias:
```bash
pip install torch
```

2. Abrir el notebook:
```bash
jupyter notebook MiniTransformer_Didactico_AttentionIsAllYouNeed.ipynb
```

3. Entrenar el modelo y probar en modo interactivo.

Para salir del loop interactivo:
```text
XEND
```

---

## 🎓 Público objetivo

Este proyecto está pensado para:

- estudiantes de ML / DL
- ingenieros de datos
- personas que **quieren entender Transformers desde dentro**
- docentes y workshops académicos

No se asumen conocimientos previos avanzados de NLP.

---

## 🧩 Qué NO es este proyecto

❌ No es un LLM de propósito general  
❌ No es un chatbot productivo  
❌ No usa embeddings preentrenados  
❌ No usa BPE / WordPiece (intencionalmente)

---

## 🧠 Mensaje clave

> *Los Transformers no son magia: son arquitectura, datos y escala.*

Este repositorio muestra **la arquitectura** y **el flujo real de información**, sin abstracciones innecesarias.

---

## 📖 Referencias

- Vaswani et al. (2017): *Attention Is All You Need*
- PyTorch Documentation: `torch.nn.Transformer`
- The Illustrated Transformer — Jay Alammar

---

## ✍️ Autor

Proyecto creado con fines **educativos y académicos** para explicar Transformers de forma clara, honesta y reproducible.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Miguel%20Cotrina-blue?logo=linkedin&style=flat-square)](https://www.linkedin.com/in/mcotrina/)

> IA & Data con propósito