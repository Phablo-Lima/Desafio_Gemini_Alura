![BDD Automator](https://github.com/Phablo-Lima/Desafio_Gemini_Alura/blob/main/imagens/BDD%20Automator.png)

## Descubra o Que o BDD Automator Pode Fazer por Você:

* **Análise Automatizada de BDDs:** Diga adeus à fadiga da revisão manual! O BDD Automator analisa seus BDDs automaticamente, identificando potenciais falhas e gargalos.
* **Detecção de Falhas Ocultas:** Nosso algoritmo de IA, impulsionado pelo Google Gemini, identifica problemas que você pode ter perdido, garantindo uma cobertura de testes completa e eficaz.
* **Sugestões Inteligentes de Melhoria:** O BDD Automator vai além de apenas apontar as falhas. Ele oferece sugestões personalizadas para aprimorar seus BDDs, tornando-os mais robustos e eficientes.
* **Geração Automática de BDDs Otimizados:** Com um clique, o BDD Automator reescreve seus BDDs com base nas sugestões da IA, criando testes mais eficazes e menos propensos a erros.
* **Correção Ortográfica e Gramatical:** Garanta que seus BDDs estejam impecáveis! O BDD Automator corrige erros de português, assegurando clareza e profissionalismo.

## Simples, Poderoso e Personalizado:

* **Fácil de Usar:** Basta fornecer o texto do BDD ou a URL do Google Sheet e o BDD Automator cuida do resto!
* **Tecnologia de Ponta:** A IA do Google Gemini garante uma análise precisa, eficaz e sugestões inteligentes.
* **Adaptável às suas Necessidades:** Receba sugestões personalizadas que se adequam ao seu contexto e estilo de desenvolvimento.

## BDD Automator: A Evolução dos Testes com BDD Começa Aqui!

Experimente agora o BDD Automator e descubra como a inteligência artificial pode transformar seus testes de software, tornando-os mais rápidos, eficientes e confiáveis.

---

## Documentação Simplificada:

### Descrição:

O BDD Automator é um programa Python que utiliza a inteligência artificial do Google Gemini para analisar e aprimorar BDDs. Ele automatiza o processo de revisão, identificando falhas e sugerindo melhorias para aumentar a cobertura dos testes.

### Funcionamento:

O programa é dividido em módulos principais:

1. **Processamento de Dados:**
   - `processar_arquivo(url_ou_bdd)`: Recebe a URL de um Google Sheet ou o texto do BDD.
   - Utiliza a biblioteca `gspread` para extrair dados do Google Sheet (se aplicável).

2. **Análise com IA:**
   - `analisar_conteudo(conteudo_processado)`: Formata os dados do BDD e envia um prompt para o modelo `gemini-1.5-pro-latest` do Google Gemini.
   - O modelo analisa o BDD como um especialista em QA, buscando pontos positivos, negativos e sugestões de melhoria.

3. **Correção do BDD:**
   - `corrigir_bdd(conteudo_processado)`: Reescreve o BDD com base nas sugestões de melhoria da IA.

4. **Revisão de Português:**
   - `corrigir_portugues(conteudo_processado)`: Corrige erros de português no BDD.

5. **Interface do Usuário:**
   - `exibir_resultado(texto, titulo)`: Formata a saída do modelo em Markdown e exibe para o usuário.
   - `main()`: Gerencia o fluxo do programa.

### Bibliotecas Utilizadas:

* `google-generativeai`
* `gspread`
* `oauth2client`
* `requests`
* `pandas`
* `textwrap`
* `IPython.display`

### Fluxo do Programa:

1. O usuário fornece a URL do Google Sheet ou o texto do BDD.
2. O programa processa os dados.
3. O BDD formatado é enviado para o Google Gemini para análise.
4. O modelo retorna a análise com sugestões de melhoria.
5. O usuário decide se quer corrigir o BDD.
6. Se sim, o BDD original e as sugestões são enviados ao Google Gemini para correção.
7. O usuário pode optar por revisar o português do BDD corrigido.
8. O programa exibe a análise e o BDD corrigido (se solicitado). 

---

## Quer saber mais?

Visite a [**Documentação Técnica Completa**](https://github.com/Phablo-Lima/Desafio_Gemini_Alura/blob/main/Documenta%C3%A7%C3%A3o%20T%C3%A9cnica.md) para informações detalhadas, tutoriais e exemplos de uso.

**⟶** [**Acesse o Código do Programa BDD Automator AQUI**](https://github.com/Phablo-Lima/Desafio_Gemini_Alura/blob/main/BDD_IA.ipynb) **⟵**

---
