# Create URL Shortener API

## Overview

This project implements a serverless API for creating short URLs using AWS Lambda and S3. It allows generating unique codes for original URLs and storing them with an expiration time.

## Features

- Generation of unique short codes for long URLs
- Support for configuring expiration time
- Storage of data in S3 bucket
- Response with the generated short URL code

## Architecture

The application consists of:

1. **AWS Lambda Function**: Processes HTTP requests to create short URLs
2. **Amazon S3**: Stores the mapping data between short URLs and original ones
3. **Data Model**: Representation of URL data with expiration time

## How It Works

1. The client sends a POST request containing the original URL and expiration time
2. The Lambda function generates a unique 8-character code (based on UUID)
3. The function creates a JSON object with the original URL and expiration time
4. The object is stored in the S3 bucket with the name `{code}.json`
5. The API returns the generated code to the client

## File Structure

- `Main.java`: Main class that implements the Lambda function handler
- `UrlData.java`: Model class for URL data

## Request Format

```json
{
    "originalUrl": "https://example.com/page-with-very-long-url",
    "expirationTime": "1640995200"
}
```

Where `expirationTime` is the Unix timestamp (in seconds) that defines when the URL expires.

## Response Format

```json
{
    "code": "a1b2c3d4"
}
```

This code should be used to compose the final short URL, for example: `https://yourdomain.com/a1b2c3d4`

## Technologies Used

- Java
- AWS Lambda
- Amazon S3
- Jackson (for JSON processing)
- Lombok (for boilerplate reduction)
- AWS SDK for Java v2

## Requirements

- JDK 11 or higher
- Maven
- AWS CLI configured with appropriate credentials
- S3 bucket configured for data storage

## Configuration

To use this application, you need to:

1. Create an S3 bucket named `url-shortener-devjf` (or change the name in the code)
2. Configure Lambda to be triggered by HTTP requests via API Gateway
3. Set up the necessary permissions for Lambda to access the S3 bucket
4. Configure API Gateway to accept POST requests with JSON body

## Integration

This service works in conjunction with the short URL redirection API. After creating a short URL with this API, the returned code can be used with the redirection service to access the original URL.

## Security Considerations

- The code generation uses UUID to minimize collisions
- No URL validation is performed - consider implementing validation to prevent malicious redirects
- No authentication/authorization is implemented in this basic example

---

# Criar URL Encurtada (pt-br)

## Visão Geral

Este projeto implementa uma API serverless para criação de URLs curtas utilizando AWS Lambda e S3. Ele permite gerar códigos únicos para URLs originais e armazená-los com tempo de expiração.

## Funcionalidades

- Geração de códigos curtos únicos para URLs longas
- Suporte para configuração de tempo de expiração
- Armazenamento dos dados em bucket S3
- Resposta com o código de URL curta gerado

## Arquitetura

A aplicação é composta por:

1. **AWS Lambda Function**: Processa as requisições HTTP para criar URLs curtas
2. **Amazon S3**: Armazena os dados de mapeamento entre URLs curtas e originais
3. **Modelo de dados**: Representação dos dados de URL com tempo de expiração

## Como Funciona

1. O cliente envia uma requisição POST contendo a URL original e o tempo de expiração
2. A função Lambda gera um código único de 8 caracteres (baseado em UUID)
3. A função cria um objeto JSON com a URL original e o tempo de expiração
4. O objeto é armazenado no bucket S3 com nome `{código}.json`
5. A API retorna o código gerado ao cliente

## Estrutura de Arquivos

- `Main.java`: Classe principal que implementa o handler da função Lambda
- `UrlData.java`: Classe de modelo para os dados da URL

## Formato da Requisição

```json
{
    "originalUrl": "https://exemplo.com/pagina-com-url-muito-longa",
    "expirationTime": "1640995200"
}
```

Onde `expirationTime` é o timestamp Unix (em segundos) que define quando a URL expira.

## Formato da Resposta

```json
{
    "code": "a1b2c3d4"
}
```

Este código deve ser utilizado para compor a URL curta final, por exemplo: `https://seudominio.com/a1b2c3d4`

## Tecnologias Utilizadas

- Java
- AWS Lambda
- Amazon S3
- Jackson (para processamento JSON)
- Lombok (para redução de boilerplate)
- AWS SDK para Java v2

## Requisitos

- JDK 11 ou superior
- Maven
- AWS CLI configurado com credenciais apropriadas
- Bucket S3 configurado para armazenamento dos dados

## Configuração

Para utilizar esta aplicação, você precisa:

1. Criar um bucket S3 chamado `url-shortener-devjf` (ou alterar o nome no código)
2. Configurar o Lambda para ser acionado por requisições HTTP via API Gateway
3. Configurar as permissões necessárias para o Lambda acessar o bucket S3
4. Configurar o API Gateway para aceitar requisições POST com corpo JSON

## Integração

Este serviço trabalha em conjunto com a API de redirecionamento de URLs curtas. Após criar uma URL curta com esta API, o código retornado pode ser usado com o serviço de redirecionamento para acessar a URL original.

## Considerações de Segurança

- A geração de códigos utiliza UUID para minimizar colisões
- Nenhuma validação de URL é realizada - considere implementar validação para evitar redirecionamentos maliciosos
- Não há autenticação/autorização implementada neste exemplo básico
