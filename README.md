# 📄 **README — Orquestração Multi-Agente RAG para Atendimento em Clínica Odontológica**

### *(Todo o pipeline orquestrado exclusivamente com modelos Google Gemini)*

---

# 🧠 **Visão Geral do Projeto**

Este projeto implementa um sistema inteligente para **atendimento automatizado de uma clínica odontológica**, utilizando:

* **Arquitetura Multi-Agente**
* **RAG (Retrieval-Augmented Generation) com Qdrant**
* **Orquestração completa baseada em modelos Gemini**
* **Atendimento cordial e profissional**
* **Resolução de perguntas conflitantes (multi-intent)**
* **Busca estritamente baseada nos documentos internos da clínica**

Toda a solução roda via **Docker Compose**, garantindo reprodutibilidade e fácil implantação.

---

# 🎯 **Objetivo**

## ✔ **1. Atendimento cordial e humanizado**

O agente principal, impulsionado pelo Gemini, é capaz de:

* Responder de forma educada e clara
* Orientar o paciente sobre procedimentos
* Evitar linguagem técnica desnecessária
* Seguir boas práticas de comunicação em saúde

---

## ✔ **2. RAG alimentado por documentos internos**

O modelo Gemini consulta apenas:

* protocolos da clínica
* orientações
* descrições de tratamentos
* explicações de procedimentos
* informações gerais pré-e pós-atendimento

Evita “alucinações” e mantém as respostas dentro do escopo autorizado.

---

## ✔ **3. Perguntas com múltiplos assuntos (multi-intent)**

Quando o usuário faz perguntas como:

> **“Quanto custa clareamento e como funciona o implante dentário?”**

O sistema Gemini:

* Identifica múltiplas intenções
* Divide a pergunta
* Aciona agentes especializados
* Consulta o RAG individualmente
* Recompõe a resposta natural e coerente

---

## ✔ **4. Arquitetura multi-agente com orquestração Gemini**

O pipeline contém:

* Agente de Intenções (Gemini)
* Agente RAG (Gemini + Qdrant)
* Agente de Resposta Natural (Gemini)
* Agente de Oversight / Consistência (Gemini)
* Agente de Workflow (n8n)
* Camada backend (Flask)

**Todos os módulos decisórios e de raciocínio são alimentados por modelos Gemini.**

---

# 🧩 **Arquitetura do Sistema**

| Serviço        | Tecnologia | Função                                  |
| -------------- | ---------- | --------------------------------------- |
| Flask App      | Python     | Orquestra agentes e serve API           |
| Gemini         | Google AI  | Raciocínio, RAG, classificação, geração |
| Qdrant         | Vector DB  | Busca semântica                         |
| MinIO          | S3 Storage | Repositório de documentos da clínica    |
| PostgreSQL     | DB         | Memória de histórico de diálogos        |
| n8n            | Workflow   | Automação avançada                      |
| Docker Compose | Infra      | Subida e isolamento de serviços         |

---

# 📦 **Estrutura de Pastas**

```
pln-CEUB/
├── docker-compose.yml
├── Dockerfile
├── src/
├── static/
├── templates/
├── scripts/
├── uploads/
├── volumes/
│   ├── qdrant/
│   ├── minio/
│   ├── postgres/
│   └── n8n/
└── README.md
```

A pasta `volumes/` contém os dados persistentes dos containers.

---

# 🚀 **Como Rodar o Projeto**

## **1. Clonar o repositório**

```bash
git clone https://github.com/CDML-CEUB-GeorgeKurokiJr/entrega-final-pln-jmanacleto.git
cd entrega-final-pln-jmanacleto
```

---

## **2. Configurar variáveis de ambiente**

```bash
cp env.example .env
```

Preencha:

* **GEMINI_API_KEY** (obrigatória — todos os agentes usam Gemini)
* **MODEL_QA_GENERATOR**
* **N8N_WEBHOOK_URL**
* **QDRANT_API_KEY**

---

## **3. Subir os serviços**

```bash
docker compose up --build
```

A aplicação estará disponível em:

```
http://localhost:5000
```

---

# 🧪 **Como Testar o Sistema**

Experimente perguntas com múltiplas intenções:

```
Meu tratamento de cárie é aceito pelo plano AMIL? (SULAMERICA/ENTRE OUTROS)
```

```
Vocês fazem limpeza infantil e orientam sobre sensibilidade dentária?
```

```
Posso fazer implante e depois colocar aparelho?
```

O sistema deve:

* identificar que existem duas ou mais perguntas
* processar cada uma separadamente usando Gemini
* consultar os documentos com RAG
* montar resposta educada, clara e completa

---

# 🔐 **Segurança e Limitações**

* O sistema não substitui diagnóstico
* Respostas seguem apenas o conteúdo dos documentos usados no RAG
* Não inventa serviços ou recomendações fora do escopo
* Mantém postura profissional e ética no atendimento

---

# 👨‍⚕️ **Conclusão**

Este projeto demonstra:

* Aplicação prática de Gemini como motor de orquestração e raciocínio
* Integração de multi-agentes inteligentes
* Implementação de RAG real com Qdrant
* Comunicação humanizada simulando atendimento odontológico
* Arquitetura robusta com Docker, Flask, MinIO, PostgreSQL e n8n

Desenvolvido como **projeto final da disciplina de Processamento de Linguagem Natural (PLN)** — CEUB.
