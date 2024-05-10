# Fast Markdown AI

O projeto foi pensado para criar um `README.md` com Inteligência artificial, A ideia fundamental é mandar um trecho de código ou um resumo do projeto e ter um modelo inical com comandos do markdown para auxiliar na ciração do `README.md` do projeto!

## Exemplo de readme.md criado pela Fest Markdown AI
---
## Google Generative AI com Gemini-1.5-pro 

Este projeto demonstra a integração da biblioteca `google-generativeai` com o modelo de linguagem avançado `gemini-1.5-pro:latest` para a geração de conteúdo textual. 

### Pré-requisitos 

*   Python 3.7+ 
*   Biblioteca `google-generativeai` 
*   Chave de API do Google Generative AI 

### Instalação 

```sh
pip install -q -U google-generativeai 
```

### Como usar 

1.  **Configurar a API:** 

    Para utilizar este projeto, é necessário obter uma chave de API do Google Generative AI. Você pode gerar essa chave acessando o Google AI Studio [🔗](https://cloud.google.com/generative-ai-studio). Após obter a chave, defina a variável de ambiente `API_KEY` com o valor fornecido. 
    ```python
    import google.generativeai as genai 
    from google.colab import userdata 

    API_KEY = userdata.get('API_KEY') 
    genai.configure(api_key=API_KEY) 
    ```
2.  **Listar Modelos Disponíveis:** 

    Antes de prosseguir, é útil verificar os modelos disponíveis para garantir compatibilidade e escolher o mais adequado para o seu caso de uso. 
    ```python
    for m in genai.list_models(): 
        if 'generateContent' in m.supported_generation_methods: 
            print(m.name) 
    ```
3.  **Configurar as Configurações de Segurança e Geração:** 

    Defina as configurações de segurança e geração conforme necessário para garantir a adequação e segurança da geração de conteúdo. 
    ```python
    safety_settings = [ 
        {"category": "HARM_CATEGORY_HARASSMENT", "threshold": "BLOCK_MEDIUM_AND_ABOVE"}, 
        {"category": "HARM_CATEGORY_HATE_SPEECH", "threshold": "BLOCK_MEDIUM_AND_ABOVE"}, 
        {"category": "HARM_CATEGORY_SEXUALLY_EXPLICIT", "threshold": "BLOCK_MEDIUM_AND_ABOVE"}, 
        {"category": "HARM_CATEGORY_DANGEROUS_CONTENT", "threshold": "BLOCK_MEDIUM_AND_ABOVE"}, 
    ] 

    generation_config = {"candidate_count": 1, "temperature": 0.8} 
    ```
4.  **Inicializar o Modelo:** 

    Utilize as configurações definidas anteriormente para inicializar o modelo para geração de conteúdo. 
    ```python
    system_instruction = "Você foi contratado para fazer o readme do projeto. A partir de um trecho de código ou resumo do projeto você deve extrair dados importantes como: resumo sobre a funcionalidade do sistema e informações de execução do projeto (trazendo exemplos em bloco de código). Entregue somente o markdown do projeto." 

    model = genai.GenerativeModel( 
        model_name='gemini-1.5-pro-latest', 
        safety_settings=safety_settings, 
        generation_config=generation_config, 
        system_instruction=system_instruction 
    ) 
    ```
5.  **Gerar Conteúdo:** 

    Utilize o modelo inicializado para gerar conteúdo com base em um prompt fornecido pelo usuário. 
    ```python
    prompt = input("Informe o código, ou um resumo do seu projeto: ") 

    prompt_parts = [f"input: {prompt}", "output: "] 

    response = model.generate_content(prompt_parts) 
    print(response.text) 
    ```

---

***Este README.md foi gerado com ❤️🤖 por [fast-markdown-ai](https://github.com/Gabriel-Paes/fast-markdown-ai/)*** 
