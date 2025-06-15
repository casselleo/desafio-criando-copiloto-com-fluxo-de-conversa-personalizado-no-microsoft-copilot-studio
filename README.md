# Desafio: Criando um Copiloto com Fluxo de Conversa Personalizado no Microsoft Copilot Studio

Este módulo explorou a criação de Copilots com fluxos de conversa personalizados no Microsoft Copilot Studio, abordando os cenários ideais para sua aplicação na plataforma.

---

## 1. Criando um Copiloto em Branco

Iniciamos a construção de um agente do zero no Microsoft Copilot Studio. Para a arquitetura base desse copiloto, seguimos os passos de configuração iniciais, definindo as seguintes características:

* **Idioma:** Embora o idioma de interação seja o português, é **altamente recomendado utilizar o inglês** durante a criação na plataforma, devido à maior facilidade de compreensão do Copilot Studio nesse idioma.
* **Nome:** O agente foi nomeado **"Agente da DIO"**.
* **Descrição:** A função do agente é buscar conteúdos sobre o Copilot Studio na documentação oficial da Microsoft. Todas as suas respostas serão apresentadas sob a persona **"Agente da DIO"**.
* **Instruções:** Para guiar o comportamento do agente, definimos o seguinte prompt:
    "Você é o agente chamado 'Agente da DIO' e vai agir em tom formal com o idioma em português, para retornar informações relevantes da documentação oficial da Microsoft, o Microsoft Learn. Ao retornar uma resposta para a pergunta do usuário você deve considerar:
    * Buscar a melhor resposta na documentação.
    * Retornar a resposta apropriada e amigável de tom formal.
    * Retornar uma ou mais citações da documentação."

Para este copiloto, a base de **Conhecimento (Knowledge)** não foi implementada inicialmente, pois o foco era a arquitetura base. No entanto, é possível incluir o Microsoft Learn como fonte de conhecimento posteriormente, se necessário.

---

## 2. Customizando um Tópico

Adicionamos um novo tópico em branco ao nosso agente para criar um fluxo de conversa personalizado.

* **Frases de Gatilho:** Definimos os seguintes termos para acionar o tópico: "buscar informações de ai builder", "o que é ai builder", "onde encontro informações da ferramenta de AI da Power Platform".
* **Ação:** Dentro desse tópico, criamos uma nova ação que utiliza respostas generativas. Nela, a variável **`Activity.Text`** foi configurada para armazenar o texto da última mensagem digitada pelo usuário no chatbot, permitindo que a IA generativa processe a consulta.
* **Mensagem de Encerramento:** Para indicar a conclusão do tópico, adicionamos uma mensagem final: "Tópico de AI Builder encerrado!".

---

## 3. Personalizando Mensagens de Erro de Tópico

Existem duas opções principais para personalizar mensagens de erro quando o copiloto não compreende a entrada do usuário:

1.  **Configuração no Conversational Boosting:**
    * Neste cenário, se o agente não entender uma mensagem, ele primeiro tenta responder com base nas respostas generativas.
    * Se a resposta do usuário não estiver em branco (ou seja, se houver alguma entrada), o tópico pode ser encerrado. Caso contrário, o fluxo direciona para um campo configurado para a mensagem de erro padrão.
2.  **Configuração no Fallback:**
    * Todas as mensagens que o agente falhar em compreender e que não forem tratadas por outras regras, cairão no tópico de *Fallback*.

Nesse caso específico, a maioria das ocorrências de erro será tratada pelo *Conversational Boosting*. Por isso, configuramos a seguinte mensagem personalizada: "Olá, `User.PrincipalName` (variável para identificar o nome do usuário), desculpa, mas não foi possível encontrar a resposta que você estava esperando. Entre em contato com o: (11) 4000-4000 ou contato@dio.com.br".

---

## 4. Aumentando e Diminuindo a Qualidade da Resposta com GenAI

As configurações de IA Generativa permitem ajustar a qualidade e o comportamento das respostas do copiloto.

* **Fontes de Dados (Conversational Boosting):** Em "Conversational Boosting", é possível clicar em "Edit data sources" para selecionar as bases de conhecimento específicas que o agente deve utilizar.
* **Conhecimento Geral da IA:** Há uma opção para permitir que a IA utilize seu conhecimento geral (GPT-4 por padrão). Se essa opção for desabilitada, a IA usará exclusivamente as bases de conhecimento configuradas por você.
* **Customização do Prompt:** É possível personalizar o prompt da IA, adicionando variáveis para buscar dados com base na pergunta do usuário.
* **Nível de Moderação de Conteúdo:**
    * Ajustar para **"High" (alto)** torna a IA menos criativa e mais precisa, buscando documentos com alta probabilidade de relevância.
    * Ajustar para **"Low" (baixo)** torna a IA mais criativa, podendo retornar documentos com menor probabilidade de relevância, mas também com maior flexibilidade.

### Configuração da Qualidade da Resposta em Nível de Ambiente/Agente:

Além das configurações por tópico, nas definições gerais do Copilot Studio, em "Generative AI", é possível habilitar a IA generativa e definir a moderação do conteúdo para ser mais criativa ou mais precisa em todo o ambiente do copiloto.
