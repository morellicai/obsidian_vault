#### Resumo da Estratégia de Tecnologia e Fluxo

1. **Frontend**: Formulário simples e com design mobile-first. Ele fará uma requisição **POST** para o endpoint no FastAPI.    
2. **Backend (FastAPI)**:
    - Um endpoint `/contrato` que recebe os dados do formulário com um modelo **Pydantic**.
    - **Regras de Negócio**:
        - Gere o HTML a partir do template Jinja2 e os dados do Pydantic.
        - Converta o HTML em PDF (com WeasyPrint).
        - Faça o upload do PDF para o Google Drive.
        - Adicione uma nova linha com os dados na sua planilha do Google Sheets.
        - Envie o e-mail com o PDF anexado para o cliente.
    - Retorne uma resposta simples para o frontend, como um **JSON** indicando que o processo foi concluído com sucesso.
3. **Checkout**: Implementado no próprio frontend, talvez com uma tela de confirmação antes de enviar a requisição para o backend.
---
# Tecnologias
### Front-end
- HTML simples
- Tailwind CSS framework para a renderização do template
- CSS para o modelo da saida do PDF
- Javascript para checkout e validação de dados antes de mandar para o backend
> Tudo isso usando o Jinja2 do python para o render das informações
### Back-end
- FastAPI -> Para tratar dados
- Pydantic -> Validação de Dados
- Jinja2 -> para renderizar dados no front
- WeasyPrint -> Para exportar o PDF com css de forma facil
- google-api-python-client -> Para o envio ao google drive
	> - Autenticação: Configure a autenticação via OAuth 2.0. Isso é um pouco chato no começo, mas é a forma segura de acessar os serviços do Google. Você precisa criar credenciais na Google Cloud Console
	> - Upload do PDF: Use a API do Google Drive para fazer o upload do arquivo PDF gerado. Você pode definir a pasta de destino para manter tudo organizado.
	> - Usar a biblioteca `gspread` para atualizar a planilha online do google sheets
- smtplib -> Para enviar contrato para o cliente
	- É preciso das crecenciais (Usuário e Senha do provedor de email)
	- E do servidor SMTP (`smtp.gmail.com` para gmail)
---
# Estrutura

``` bash
/contratos_project
 ├── app.py                   # Ponto de entrada do FastAPI
 ├── models.py                # Modelos Pydantic para validação
 ├── routes.py                # Rotas do backend
 ├── services
 │    ├── pdf_service.py      # Funções para gerar PDF
 │    ├── excel_service.py    # Funções para gerar Excel
 │    ├── drive_service.py    # Funções para enviar ao Google Drive
 │    └── email_service.py    # Funções para envio de email
 ├── templates                # Templates Jinja2 para HTML e PDF
 │    ├── contrato.html
 │    └── form.html
 └── static                   # CSS, imagens, JS
```

