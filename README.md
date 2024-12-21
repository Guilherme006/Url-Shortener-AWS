## Sobre o Projeto

Este projeto implementa um serviço de encurtador de URLs usando AWS Lambda e AWS S3. O serviço contém duas funcionalidades principais:

**1. Criar uma URL encurtada**

**2. Redirecionar para a URL original**

### Funcionalidades

**1. Criar uma URL Encurtada**

A função Lambda responsável pela criação de URLs encurtadas realiza as seguintes operações:

- Recebe uma requisição com uma URL original e um tempo de expiração.
- Gera um código curto único para a URL usando UUID.
- Armazena os dados no S3 em formato JSON, incluindo a URL original e o tempo de expiração.
- Retorna o código curto que pode ser usado para redirecionar.

**Exemplo de Requisição:**

  ```sh
{
  "body": {
      "originalUrl": "https://exemplo.com",
      "expirationTime": "172800" // Tempo em segundos (2 dias)
    }
}
  ```

**Exemplo de Resposta:**

  ```sh
{
  "code": "a1b2c3d4"
}
```

**2. Redirecionar para a URL Original**

- A função Lambda responsável pelo redirecionamento realiza as seguintes operações:
- Recebe uma requisição com o código curto da URL no caminho.
- Busca os dados correspondentes no S3.
- Verifica se a URL ainda é válida (não expirou).
  * Se a URL expirou, retorna um erro HTTP 410.
  * Se ainda for válida, retorna um redirecionamento HTTP 302 para a URL original.

### Como Testar

1. Configure o bucket S3 na AWS e configure permissões apropriadas.
2. Use ferramentas como Postman para enviar uma requisição POST com o corpo necessário.
3. Verifique no bucket S3 se o arquivo foi criado corretamente.
4. Faça uma requisição GET com o código curto.
5. Verifique se a resposta redireciona corretamente ou informa que a URL expirou.

