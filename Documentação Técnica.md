## ⚙️Documentação Técnica

Este programa em Python utiliza o poder do Google Generative AI para analisar e melhorar cenários de teste escritos no formato BDD (Behavior Driven Development). O programa pode processar dados de um Google Sheet ou de texto colado diretamente pelo usuário.

## Fluxo do Programa

1. **Instalação de Dependências:** O programa começa instalando as bibliotecas necessárias, incluindo `google-generativeai`, `gspread` e `oauth2client`.
2. **Autenticação:** O usuário precisa fornecer sua chave de API do Google para usar o serviço Generative AI.
3. **Processamento de Entrada:** O programa solicita ao usuário a URL de um Google Sheet ou o texto do BDD. 
    - Se for fornecida uma URL, o programa usa a biblioteca `gspread` para acessar e ler os dados da planilha.
    - Se for fornecido texto, o programa o processa diretamente.
4. **Análise do BDD:** O conteúdo processado é então passado para a função `analisar_conteudo`. Esta função formata o conteúdo em uma tabela Markdown e envia um prompt para o modelo de linguagem `gemini-1.5-pro-latest`. O prompt instrui o modelo a analisar o BDD e fornecer:
    - **Pontos Positivos:** Aspectos que contribuem para testes eficazes.
    - **Pontos Negativos:** Falhas que podem prejudicar os testes.
    - **Sugestões de Melhoria:** Recomendações para aprimorar o BDD.
5. **Correção do BDD (Opcional):** O usuário pode optar por corrigir o BDD com base nas sugestões do modelo. Se o usuário escolher corrigir, o programa envia outro prompt para o modelo, solicitando que ele reescreva o BDD com base nas sugestões.
6. **Correção do Português (Opcional):** O usuário pode optar por corrigir a ortografia e gramática do BDD corrigido. Se o usuário escolher corrigir, o programa envia o BDD corrigido para o modelo, solicitando que ele corrija os erros de português.
7. **Exibição dos Resultados:** A análise do BDD, o BDD corrigido (se solicitado) e o BDD corrigido com o português revisado (se solicitado) são exibidos para o usuário em formato Markdown.

## Funções Principais

- **`processar_arquivo(url_ou_bdd)`:** Processa a entrada do usuário, seja uma URL do Google Sheet ou texto.
- **`analisar_conteudo(conteudo_processado)`:** Analisa o BDD usando o Google Generative AI.
- **`corrigir_bdd(conteudo_processado)`:** Reescreve o BDD com base nas sugestões do modelo.
- **`corrigir_portugues(conteudo_processado)`:** Corrige a ortografia e gramática do conteúdo.
- **`exibir_resultado(texto, titulo)`:** Exibe o texto formatado em Markdown.

## Bibliotecas Utilizadas

- **`google-generativeai`:** Para acessar o Google Generative AI.
- **`gspread`:** Para interagir com o Google Sheets.
- **`oauth2client`:** Para autenticação com o Google APIs.
- **`requests`:** Para fazer solicitações HTTP.
- **`json`:** Para lidar com dados JSON.
- **`pandas`:** Para manipulação de dados (não utilizado neste código, mas incluído nas dependências).
- **`io`:** Para lidar com fluxos de entrada e saída.
- **`google.colab`:** Para acessar dados do Google Colab (específico para o ambiente Colab).
- **`textwrap`:** Para formatação de texto.
- **`IPython.display`:** Para exibir Markdown no notebook.

## Observações

- O programa requer uma chave de API válida do Google Cloud para acessar o serviço Generative AI.
- O modelo de linguagem usado é o `gemini-1.5-pro-latest`, mas pode ser alterado para outros modelos compatíveis.
- O programa assume que o BDD está no formato CTFL.
- As configurações de segurança do modelo podem ser ajustadas na variável `safety_settings`.

## Guia API's

Este guia detalhado explica como configurar o acesso ao Google Sheets e ao Gemini através do Google Cloud Platform.

### Parte 1: Configurando o Google Cloud Platform para Acessar Google Sheets

1. **Criar um Projeto no Google Cloud Platform:**
   - Acesse o Google Cloud Console: [https://console.cloud.google.com](https://console.cloud.google.com)
   - Crie um novo projeto ou selecione um existente.

2. **Habilitar a API do Google Sheets:**
   - No menu de navegação, vá para "APIs e Serviços" > "Biblioteca".
   - Procure por "Google Sheets API" e selecione-a.
   - Clique em "Ativar".

3. **Criar Credenciais da Conta de Serviço:**
   - No menu de navegação, vá para "APIs e Serviços" > "Credenciais".
   - Clique em "Criar Credenciais" > "Conta de serviço".
   - Preencha os detalhes da conta de serviço (nome, ID, etc.).
   - Na etapa "Conceder a esta conta de serviço acesso ao projeto", clique em "Concluído". **Não é necessário atribuir função específica nesta etapa.**

4. **Conceder permissões à conta de serviço no Google Sheets:**
   - **Importante:** Este passo requer acesso de administrador ao Google Sheet que você deseja acessar.
   - Abra o Google Sheet que você deseja usar.
   - Clique em "Compartilhar" no canto superior direito.
   - No campo "Compartilhar com pessoas e grupos", insira o endereço de e-mail da conta de serviço que você criou (ele termina com `@gcp-project-id.iam.gserviceaccount.com`).
   - Selecione a permissão "Editor" ou mais restritiva, dependendo das necessidades do seu aplicativo.
   - Clique em "Enviar".

5. **Baixar o Arquivo de Chave da Conta de Serviço:**
   - No Google Cloud Console, na página "Credenciais", localize a conta de serviço que você criou.
   - Clique nos três pontos verticais à direita da conta de serviço e selecione "Gerenciar chaves".
   - Clique em "Adicionar chave" > "Criar nova chave".
   - Selecione o tipo de chave "JSON" e clique em "Criar".
   - Um arquivo JSON será baixado para o seu computador. Este arquivo contém as credenciais da sua conta de serviço.

6. **Utilizar as Credenciais no seu Código:**
   - No seu código Python, utilize o arquivo JSON baixado para autenticar o acesso ao Google Sheets. Veja o exemplo abaixo:
     ```python
     import gspread
     from oauth2client.service_account import ServiceAccountCredentials

     # Substitua 'caminho/para/seu/arquivo.json' pelo caminho real do arquivo JSON baixado
     scope = ['https://spreadsheets.google.com/feeds', 'https://www.googleapis.com/auth/drive']
     creds = ServiceAccountCredentials.from_json_keyfile_name('caminho/para/seu/arquivo.json', scope)
     client = gspread.authorize(creds)

     # Agora você pode acessar o Google Sheet usando o cliente gspread
     spreadsheet = client.open_by_key('ID_da_sua_planilha')
     ```

### Parte 2: Obtendo uma API Key do Google Generative AI (Gemini)

1. **Acessar a Seção de APIs e Serviços:**
   - No Google Cloud Console, navegue até "APIs e Serviços" no menu de navegação.
   - Certifique-se de que você está no projeto correto onde deseja usar o Gemini.

2. **Habilitar a API do Google Generative AI:**
   - Na "Biblioteca", procure por "Google Generative AI API".
   - Selecione a API e clique em "Ativar".

3. **Criar uma API Key:**
   - Na página "Credenciais", clique em "Criar Credenciais" > "Chave de API".
   - Uma nova chave de API será gerada e exibida. **Copie esta chave, pois você não poderá visualizá-la novamente.**

4. **Utilizar a API Key no seu Código:**
   - Armazene sua API Key de forma segura (evite colocá-la diretamente no código).
   - Utilize a API Key para autenticar suas solicitações à API do Gemini. Veja o exemplo abaixo:

     ```python
     import google.generativeai as genai

     # Substitua 'SUA_API_KEY' pela sua chave de API real
     genai.configure(api_key='SUA_API_KEY')

     # Agora você pode usar a biblioteca genai para interagir com o Gemini
     ```

### Considerações de Segurança:

- **Nunca compartilhe suas chaves de API publicamente.**
- Armazene suas chaves de API de forma segura, utilizando cofres de chaves ou variáveis de ambiente.
- Implemente o princípio de privilégio mínimo, concedendo apenas as permissões necessárias às suas contas de serviço e API Keys.

Seguindo estes passos, você poderá usar o Google Cloud Platform para ler dados do Google Sheets e interagir com o Google Generative AI (Gemini) em seus projetos.

### Conclusão

Este programa fornece uma maneira eficiente de analisar e melhorar cenários de teste BDD usando inteligência artificial. Ele automatiza o processo de revisão de código e ajuda a garantir que os testes sejam abrangentes e eficazes. 
