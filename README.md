# 🌤️ Telegram Weather Chatbot com n8n

Este projeto implementa um chatbot no Telegram utilizando **n8n** que
consulta a **API OpenWeather** para retornar a temperatura atual de uma
cidade informada pelo usuário.

O bot recebe o nome da cidade via Telegram, consulta a API meteorológica
e responde com a temperatura atual formatada em português.

O projeto também inclui **integração com Google Gemini** para
melhorar a naturalidade da mensagem enviada ao usuário.

------------------------------------------------------------------------

# 🚀 Tecnologias utilizadas

-   n8n
-   Telegram Bot API
-   OpenWeather API
-   Google Gemini

------------------------------------------------------------------------

# ⚙️ Estrutura do Workflow

Telegram Trigger\
↓\
Format Input\
↓\
OpenWeather Request\
↓\
IF Weather OK

TRUE → Format Weather Message → Google Gemini → Send Success
Message\
FALSE → Send Error Message

------------------------------------------------------------------------

# 🔎 Funcionamento

## 1. Recebimento da mensagem

O workflow inicia com o **Telegram Trigger**, que captura mensagens
enviadas ao bot.

## 2. Formatação da entrada

O node **Format Input**:

-   Remove espaços extras
-   Normaliza letras minúsculas
-   Remove acentuação

O texto é salvo na variável:

`queue`

------------------------------------------------------------------------

## 3. Consulta na OpenWeather

Endpoint utilizado:

https://api.openweathermap.org/data/2.5/weather

Parâmetros enviados:

  parâmetro   valor
  ----------- ---------------------
  q           cidade informada
  units       metric
  lang        pt_br
  appid       OPENWEATHER_API_KEY

------------------------------------------------------------------------

## 4. Validação da resposta

O node **IF Weather OK** verifica se existe o campo:

`main.temp`

Se existir → fluxo de sucesso\
Se não existir → fluxo de erro

------------------------------------------------------------------------

## 5. Formatação da resposta

O node **Format Weather Message** gera a mensagem:

🌤️ A temperatura em {cidade} é de {temperatura}°C.

A temperatura é arredondada.

------------------------------------------------------------------------

## 6. Uso do Google Gemini

O node **Google Gemini** reescreve a mensagem de forma mais natural.

Exemplo:

Entrada:

🌤️ A temperatura em São Paulo é de 27°C.

Saída possível:

🌤️ Neste momento a temperatura em São Paulo está em torno de 27°C.

Caso o Gemini não esteja configurado, o workflow utiliza a mensagem
gerada pelo node **Format Weather Message** como fallback.

------------------------------------------------------------------------

# ❌ Tratamento de erro

Se a cidade não for encontrada, o bot retorna:

❌ Cidade não encontrada. Use o formato Cidade,UF (ex.: São Paulo,SP).

------------------------------------------------------------------------

# 🔑 Variáveis de ambiente

O projeto utiliza as seguintes variáveis:

OPENWEATHER_API_KEY\
TELEGRAM_BOT_TOKEN

Opcional:

GEMINI_API_KEY

Nenhuma chave deve ser incluída no repositório.

------------------------------------------------------------------------

# 📦 Como importar o workflow no n8n

1.  Baixe o arquivo `workflow-chatbot-telegram.json`
2.  Abra o **n8n**
3.  Clique em **Import Workflow**
4.  Selecione o arquivo JSON

------------------------------------------------------------------------

# 🔧 Configuração das credenciais

## Telegram

Criar credencial no n8n com:

TELEGRAM_BOT_TOKEN

## OpenWeather

Criar conta em:

https://openweathermap.org/

Gerar API Key e configurar como:

OPENWEATHER_API_KEY

## Google Gemini

Criar chave em:

https://aistudio.google.com/app/apikey

Adicionar credencial no n8n.

------------------------------------------------------------------------

# 🧪 Testes realizados

### Cidade válida

São Paulo,SP\
Salvador,BA\
Rio de Janeiro,RJ

Resposta esperada:

🌤️ A temperatura em São Paulo é de 27°C.

### Cidade inválida

Entrada:

CidadeTeste123

Resposta esperada:

❌ Cidade não encontrada. Use o formato Cidade,UF (ex.: São Paulo,SP).

------------------------------------------------------------------------

# 📌 Observações

-   O workflow não contém credenciais sensíveis.
-   As chaves são configuradas diretamente no ambiente do n8n.
-   A integração com Gemini é opcional e possui fallback determinístico.

------------------------------------------------------------------------

# 👨‍💻 Heráclito Junior

Projeto desenvolvido como atividade da **Rocketseat -- Pós‑graduação em
Inteligência Artificial**.
