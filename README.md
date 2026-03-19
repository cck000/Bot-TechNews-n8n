# Bot-TechNews-n8n | Bot resumidor de notícias de tecnologia automatizado com n8n, Groq e Telegram

Um pipeline de automação de dados projetado para capturar, tratar e resumir feeds de notícias de tecnologia em tempo real usando Inteligência Artificial (LLM), entregando insights concisos diretamente via Telegram.

## O Problema
Acompanhar o volume diário de artigos técnicos, atualizações de hardware e papers de inteligência artificial consome muito tempo. Ler artigos completos muitas vezes resulta em sobrecarga de informação.

## A Solução
Este projeto utiliza o **n8n** para orquestrar um fluxo que monitora feeds RSS (como o VentureBeat), extrai os dados essenciais da notícia, processa o texto através de um modelo de linguagem de grande escala (LLM) hospedado no **Groq** para gerar um resumo executivo, e envia o resultado final formatado para um bot do **Telegram**.

## ⚙️ Arquitetura e Fluxo de Dados

1. **Trigger (RSS Read):** Monitora o feed RSS alvo em intervalos programados.
2. **Data Filtering (Limit):** Limita os itens do array JSON retornado pelo feed para processamento unitário, evitando sobrecarga de chamadas de API.
3. **Payload Optimization (Edit Fields):** Extrai estritamente o `contentSnippet` (resumo limpo da notícia) em vez do `content` completo (com tags HTML), otimizando o uso de tokens da IA.
4. **AI Processing (Summarization Chain + Groq):** Envia o texto otimizado para a API do Groq utilizando o modelo `llama3.1-8b-instant` para gerar um resumo.
5. **Delivery (Telegram API):** Formata o output da IA e o link original, enviando via requisição HTTP para a API do Telegram Bot.

## Tecnologias Utilizadas
* **Orquestração:** n8n (Node-based workflow automation)
* **Inteligência Artificial:** Groq API (Llama 3.1 8B instant) / LangChain Nodes
* **Integração:** Webhooks, REST APIs, RSS, JSON
* **Mensageiro:** Telegram Bot API

---
*Projeto desenvolvido para exploração prática de orquestração de APIs
