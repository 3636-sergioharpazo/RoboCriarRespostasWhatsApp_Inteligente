# 🤖 RoboCriarRespostasWhatsApp_Inteligente

Este projeto é um **robô inteligente de atendimento via WhatsApp** desenvolvido no **n8n**, que utiliza **Inteligência Artificial (Google Gemini)** para interpretar mensagens recebidas e responder automaticamente de forma personalizada e contextual.  

Ele atua como um **assistente virtual da Smart Software**, identificando o tipo de negócio do cliente e recomendando o sistema mais adequado com base em palavras-chave e contexto conversacional.

---

## 🚀 Funcionalidades

- 📩 Recebe mensagens via **Webhook** integrado ao **WAHA (WhatsApp API Gateway)**  
- 🧠 Processa o conteúdo da mensagem com **Google Gemini AI (LangChain)**  
- 💬 Gera respostas automáticas personalizadas conforme o tipo de negócio do cliente  
- 🧾 Mantém contexto das conversas usando **Redis Memory**  
- 👀 Marca mensagens como "visualizadas" e envia respostas automáticas no WhatsApp  
- 🏢 Atua como consultor virtual da empresa **Smart Software**

---

## 🧩 Fluxo de Execução

O fluxo é composto por **7 nós principais**:

| Etapa | Nó | Função |
|-------|----|--------|
| 1️⃣ | **Webhook** | Recebe a mensagem do WhatsApp via WAHA |
| 2️⃣ | **Set (Dados)** | Extrai e organiza os dados da mensagem (session, chatId, pushName, event, message etc.) |
| 3️⃣ | **Switch** | Verifica se o evento recebido é do tipo `"message"` |
| 4️⃣ | **AI Agent (LangChain)** | Analisa a mensagem e gera a resposta inteligente usando o contexto e instruções da Smart Software |
| 5️⃣ | **Google Gemini Chat Model** | Modelo de linguagem responsável pela geração da resposta |
| 6️⃣ | **Redis Chat Memory** | Armazena contexto de conversas para respostas mais naturais e coerentes |
| 7️⃣ | **WAHA - Send Seen / Send Text** | Marca como visualizado e envia a resposta ao usuário via WhatsApp |

---

## 🧠 Inteligência Artificial

O agente de IA está configurado com o **modelo Google Gemini** através do nó `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`, com **temperature = 0.4**, garantindo respostas consistentes e com pouca aleatoriedade.

O prompt principal instrui o agente a:

- Ser o **assistente oficial da Smart Software**  
- Identificar o tipo de negócio do usuário  
- Recomendar o sistema adequado (Churrascaria, Pizzaria, Ponto, Agendamento, Ensino ou Automação)  
- Utilizar o nome do usuário (`pushName`) sempre que possível  
- Responder de forma simpática e profissional  

---

## 💾 Requisitos

Antes de importar o fluxo, certifique-se de ter os seguintes componentes configurados:

### Dependências do n8n
- `@n8n/n8n-nodes-langchain`
- `n8n-nodes-waha` (para integração WhatsApp)
- `redis` (opcional, mas recomendado para contexto)
- Conta com **Google Gemini API (PaLM)** configurada

### Credenciais Necessárias
| Serviço | Nome no n8n | Descrição |
|----------|-------------|------------|
| 🧠 Google Gemini (PaLM) | `Google Gemini(PaLM) Api account` | Geração de texto e respostas |
| 💬 WAHA API | `WAHA account` | Comunicação com WhatsApp |
| 🧠 Redis | `Redis account` | Armazenamento de contexto de conversas |

---

## ⚙️ Configuração

1. Abra o **n8n** no navegador  
