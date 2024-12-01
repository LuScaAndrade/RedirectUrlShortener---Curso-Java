# RedirectUrlShortener---Curso-Java
## Redirecionador de URLs

Este projeto implementa um serviço de encurtamento de URLs utilizando AWS Lambda e Amazon S3.

## 📋 Descrição

O serviço busca a URL original no S3 usando o código da URL curta, verifica sua validade e redireciona o cliente.

---

## 🚀 Funcionalidades

1. Recebe um corpo JSON contendo:
1. Recebe uma solicitação HTTP com o código da URL curta no caminho da requisição.
2. Busca os dados correspondentes no Amazon S3.
3. Verifica a validade da URL:
   - Retorna status HTTP `410` (Gone) se a URL expirou.
   - Retorna um redirecionamento HTTP `302` com a URL original.

---

## 🛠️ Tecnologias Utilizadas

- **Java** com AWS Lambda
- **Amazon S3** para armazenamento
- **Jackson** para serialização JSON
- **Lombok** para simplificação de código

---

## 📝 Requisitos

- Configurar o nome do bucket no seguinte trecho:
  ```java
  GetObjectRequest getObjectRequest = GetObjectRequest.builder()
      .bucket("SEU_BUCKET_NAME")
      .key(shortUrlCode + ".json")
      .build();
  ```
- Ter as dependências necessárias para o projeto:
  - software.amazon.awssdk
  - com.fasterxml.jackson.databind
  - lombok

---

## 🗂️ Estrutura do Código
- Main: Classe principal que processa a solicitação e gerencia o redirecionamento.
- UrlData: Classe que representa os dados da URL.

---

## 📥 Exemplo de Entrada
- URL: https://{lambda-endpoint}/{shortUrlCode}

## 📥 Exemplo de Saída
- URL válida: 
 ```json
  {
    "statusCode": 302,
    "headers": {
       "Location": "https://example.com"
    }
  }
  ```

- URL expirada:
 ```json
  {
    "statusCode": 410,
    "body": "This URL has expired"
  }
  ```
--- 
## 🛠️ Como Executar
1. Configure as permissões necessárias na AWS para Lambda e S3.
2. Compile o código e faça o deploy na AWS Lambda.
3. Faça chamadas HTTP para o Lambda com o JSON no corpo da requisição.
