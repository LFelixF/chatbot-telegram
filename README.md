# 🤖 Bot de Clima no Telegram com N8N

## 📋 Descrição

Este projeto implementa um chatbot no Telegram utilizando o N8N para consultar e informar a temperatura atual de qualquer cidade do Brasil.

O usuário envia uma mensagem contendo o nome da cidade e o estado, o workflow consulta a API do OpenWeather, processa os dados recebidos e responde com uma mensagem simples, clara e amigável contendo a temperatura atual da localidade informada.

---

## 🚀 Funcionalidades

* Receber mensagens via Telegram.
* Identificar cidade e estado informados pelo usuário.
* Consultar coordenadas geográficas da cidade utilizando a API OpenWeather.
* Consultar a temperatura atual da localização encontrada.
* Retornar uma resposta amigável diretamente no Telegram.
* Utilizar apenas serviços gratuitos.

---

## 🏗️ Arquitetura

```text
Usuário
   │
   ▼
Telegram Bot
   │
   ▼
N8N Workflow
   │
   ├── Consulta Latitude/Longitude
   │      (OpenWeather Geocoding API)
   │
   └── Consulta Temperatura Atual
          (OpenWeather Weather API)
   │
   ▼
Resposta para o Telegram
```

---

## 🔗 Integrações

| Integração  | Finalidade                          |
| ----------- | ----------------------------------- |
| Telegram    | Receber e enviar mensagens          |
| OpenWeather | Consultar localização e temperatura |

---

## 📦 Pré-requisitos

Antes de importar e executar o workflow, você precisará de:

* Instância do N8N funcionando.
* Conta no Telegram.
* Bot criado através do BotFather.
* Conta no OpenWeather.
* Chave de API do OpenWeather.

---

# ⚙️ Configuração das Credenciais

## 1. Telegram

### Criar o Bot

1. Abra o Telegram.
2. Procure por **@BotFather**.
3. Execute o comando:

```text
/newbot
```

4. Informe o nome do bot.
5. Informe o username do bot.
6. O BotFather retornará um token semelhante a:

```text
123456789:AAEXEMPLO_TOKEN_DO_BOT
```

Guarde esse valor.

### Variável esperada

```env
TELEGRAM_BOT_TOKEN=123456789:AAEXEMPLO_TOKEN_DO_BOT
```

### Configurar no N8N

1. Acesse:

```text
Credentials → New Credential
```

2. Selecione:

```text
Telegram API
```

3. Informe o valor da variável:

```text
TELEGRAM_BOT_TOKEN
```

4. Salve a credencial.

---

## 2. OpenWeather

### Criar conta

1. Acesse:

https://openweathermap.org/api

2. Crie uma conta gratuita.
3. Gere uma API Key.

Exemplo:

```text
abc123xyz456789
```

### Variável esperada

```env
OPENWEATHER_API_KEY=abc123xyz456789
```

### Configurar no Workflow

Os nós HTTP abaixo utilizam a chave através do parâmetro:

```text
appid
```

Nós:

* OpenWeather - Lat/Lon
* OpenWeather - Previsão

Substitua o valor do parâmetro:

```text
appid={{OPENWEATHER_API_KEY}}
```

ou informe diretamente sua chave conforme o padrão adotado no seu ambiente.

---

# 📥 Importando o Workflow no N8N

1. Abra o N8N.
2. Clique em:

```text
Workflows
```

3. Clique em:

```text
Import from File
```

4. Selecione o arquivo JSON do workflow.
5. Aguarde a importação.
6. Abra o workflow importado.

---

# 🔧 Vinculando as Credenciais

Após a importação:

## Telegram Trigger

Selecione a credencial criada:

```text
Telegram API
```

## Telegram Send Message

Selecione a mesma credencial:

```text
Telegram API
```

## OpenWeather

Verifique os nós:

```text
OpenWeather - Lat/Lon
OpenWeather - Previsão
```

Confirme que o parâmetro:

```text
appid
```

está preenchido com sua chave válida.

---

# ▶️ Executando o Chatbot

1. Abra o workflow.
2. Clique em:

```text
Activate
```

3. Localize seu bot no Telegram.
4. Envie uma mensagem contendo:

```text
São Paulo, SP
```

ou

```text
Campina, SP
```

ou

```text
Rio de Janeiro, RJ
```

---

# 💬 Exemplo de Uso

### Mensagem enviada

```text
São Paulo, SP
```

### Resposta esperada

```text
🌤️ A temperatura em São Paulo é de 22°C.
```

---

# 📁 Estrutura do Workflow

```text
Telegram Trigger
        │
        ▼
Extrair Cidade/Estado
        │
        ▼
OpenWeather - Lat/Lon
        │
        ▼
OpenWeather - Previsão
        │
        ▼
Formatar Mensagem
        │
        ▼
Telegram Send Message
```

---

# 🛠️ Tecnologias Utilizadas

* N8N
* Telegram Bot API
* OpenWeather API
* HTTP Request Nodes

---

# 📝 Observações

* A API gratuita do OpenWeather possui limites de requisições.
* Algumas cidades podem possuir nomes duplicados. Informar o estado ajuda a melhorar a precisão da consulta.
* O primeiro uso da API pode levar alguns minutos após a geração da chave para ficar disponível.

---

# 📄 Licença

Este projeto é disponibilizado para fins educacionais e de demonstração.

Sinta-se livre para adaptar e utilizar conforme sua necessidade.
