# 🤖 Telegram Weather Chatbot (n8n + OpenWeather + Gemini)

Chatbot desenvolvido em **n8n** que consulta o clima de uma cidade
informada pelo usuário via **Telegram**, utilizando a **API
OpenWeather** e refinando a resposta com **Google Gemini**.

O bot recebe o nome de uma cidade enviado pelo usuário, consulta a API
meteorológica e retorna uma resposta amigável com as condições
climáticas.

------------------------------------------------------------------------

# 📌 Arquitetura do Workflow

Fluxo principal do chatbot:

    Telegram Trigger
          ↓
    Input Processor
          ↓
    OpenWeather Request
          ↓
    Validate Weather Response
       ├── TRUE  → Round Temperature → Gemini → Fallback Handler → Telegram Send Message
       └── FALSE → Telegram Error Message

Descrição dos nodes:

  Node                        Função
  --------------------------- --------------------------------------
  Telegram Trigger            Recebe mensagens enviadas ao bot
  Input Processor             Limpa e normaliza o texto da cidade
  OpenWeather Request         Consulta o clima na API OpenWeather
  Validate Weather Response   Verifica se a cidade existe
  Round Temperature           Arredonda os dados meteorológicos
  Message a Model (Gemini)    Melhora a resposta do chatbot
  Gemini Fallback Handler     Garante resposta caso o Gemini falhe
  Telegram Send Message       Envia resposta final ao usuário

------------------------------------------------------------------------

# ⚙️ Requisitos

Antes de executar o projeto você precisa de:

-   **n8n instalado**
-   Conta no **Telegram**
-   Conta no **OpenWeather**
-   Conta no **Google AI Studio (Gemini)**

------------------------------------------------------------------------

# 🔑 Variáveis de Ambiente

O workflow espera as seguintes variáveis:

    OPENWEATHER_API_KEY
    TELEGRAM_BOT_TOKEN

Exemplo:

``` bash
OPENWEATHER_API_KEY=your_openweather_api_key
TELEGRAM_BOT_TOKEN=your_telegram_bot_token
```

------------------------------------------------------------------------

# 🔧 Como importar o Workflow no n8n

1.  Abra o **n8n**
2.  Vá em:

```{=html}
<!-- -->
```
    Workflows → Import

3.  Selecione o arquivo:

```{=html}
<!-- -->
```
    workflow-chatbot-telegram.json

4.  Clique em **Import**
5.  Salve o workflow

------------------------------------------------------------------------

# 🤖 Criando o Bot no Telegram

1.  Abra o Telegram
2.  Procure por:

```{=html}
<!-- -->
```
    @BotFather

3.  Execute os comandos:

```{=html}
<!-- -->
```
    /start
    /newbot

4.  Escolha:

-   Nome do bot
-   Username do bot

5.  O BotFather retornará um **Bot Token**.

Exemplo:

    123456789:AAEXAMPLE_TOKEN

Esse token será usado no n8n.

------------------------------------------------------------------------

# 🔐 Configurando credenciais no n8n

## Telegram

1.  Vá em **Credentials**
2.  Clique em **New Credential**
3.  Selecione:

```{=html}
<!-- -->
```
    Telegram API

4.  Insira:

```{=html}
<!-- -->
```
    Bot Token = TELEGRAM_BOT_TOKEN

5.  Salve a credencial

------------------------------------------------------------------------

## OpenWeather

1.  Crie uma conta em:

https://openweathermap.org/api

2.  Gere uma **API Key**

3.  Configure a variável:

```{=html}
<!-- -->
```
    OPENWEATHER_API_KEY

------------------------------------------------------------------------

# 🚀 Como executar o chatbot

1.  Ative o workflow no n8n:

```{=html}
<!-- -->
```
    Activate Workflow

2.  Abra o Telegram

3.  Procure pelo seu bot

4.  Envie o nome de uma cidade.

Exemplos:

    Petrolina

ou

    Petrolina, PE

------------------------------------------------------------------------

# 📩 Exemplo de resposta

Entrada do usuário:

    Petrolina

Resposta esperada:

    🌤️ Petrolina

    Hoje o clima está agradável com temperatura em torno de 31°C.
    A sensação térmica é de 33°C e o céu está parcialmente limpo.
    A umidade do ar está em 45%.

------------------------------------------------------------------------

# ❌ Exemplo de erro

Entrada:

    CidadeInexistente

Resposta:

    ❌ Cidade não encontrada. Use o formato: Cidade, UF, BR

------------------------------------------------------------------------

# 🧠 Tratamento da entrada do usuário

O workflow executa automaticamente:

-   Remoção de acentos
-   Conversão para minúsculas
-   Remoção de espaços extras
-   Conversão para formato aceito pela API

Exemplo:

    São Paulo
    → sao paulo,br

------------------------------------------------------------------------

# 🛡️ Recursos de resiliência

O chatbot possui:

-   Fallback caso o Gemini falhe
-   Tratamento de erro da API
-   Validação de cidade inexistente
-   Continuidade do fluxo mesmo em falhas de requisição

------------------------------------------------------------------------

# 📦 Tecnologias utilizadas

-   **n8n**
-   **Telegram Bot API**
-   **OpenWeather API**
-   **Google Gemini**

------------------------------------------------------------------------

# 👨‍💻 Autor

Heráclito Jr
