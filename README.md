# Criando uma instância EC2 com Terraform

## Pré-requisitos:

awsCLI e terraform instalados

![Print do PowerShell mostrando o comando terraform destroy](/assets/1.jpeg.jpeg)
![Print do PowerShell mostrando o comando terraform destroy](/assets/2.jpeg.jpeg)

## Configurando as Credenciais da AWS

1.Para configurar minhas credenciais da AWS, eu iniciei o laboratório da AWS e copiei minhas credenciais de ID, secret_access_key, nome da região e token da sessão.

![Print do PowerShell mostrando o comando terraform destroy](/assets/4.jpeg.jpeg)

2. Após isso executei o comando abaixo e forneci minhas credenciais de acesso solicitadas:

   ```
   aws configure
   ```

3. Então é preciso configurar o token de acesso manualmente, abrindo o arquivo de credenciais no diretório da aws em um editor de texto e colocando o token copiado anteriormente.

   - Abra o arquivo `credentials` em um editor de texto:

     ```
     notepad credentials
     ```

   - Adicione ou edite a seção com o seguinte conteúdo:

     ```
     [default]
     aws_access_key_id = YOUR_ACCESS_KEY_ID
     aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
     aws_session_token = YOUR_SESSION_TOKEN
     ```

![Print do PowerShell mostrando o comando terraform destroy](/assets/5.jpeg.jpeg)


## Terraform


Para criar uma instância EC2 usando Terraform, é necessário criar um diretório com um arquivo ".tf", no caso, criei um com o nome "main.tf" com o seguinte conteúdo:

   ```hcl
   provider "aws" {
     region = "us-east-1"
   }

   resource "aws_instance" "example" {
     ami           = "ami-0c02fb55956c7d316"  # Amazon Linux 2 AMI (HVM), SSD Volume Type
     instance_type = "t2.micro"

     tags = {
       Name = "TerraformExample"
     }
   }
   ```

Pode-se notar que as partes de "ami" e "instance_type" indicam qual o tipo de máquina será criada na aws.

---

## Inicializando o Terraform

 Agora para iniciar o terraform, rodei o comando:

   ```
   terraform init
   ```

   ![Print do PowerShell mostrando o comando terraform init](/assets/10.jpeg.jpeg)

   ![Print do PowerShell mostrando o comando terraform plan](/assets/6.jpeg.jpeg)

## Aplicando a Configuração

Por fim, para aplicar a configuração desejada por mim à instância que será criada, utilizei o comando:

```
terraform apply
```

![Print do PowerShell mostrando o comando terraform apply](/assets/5.jpeg.jpeg)

Agora, ao irmos até a página da AWS, poderemos ver a instância criada:

![Print do PowerShell mostrando o comando terraform apply](/assets/7.jpeg.jpeg)

---

## Limpando a Infraestrutura

Para destruir a instância criada e limpar a infraestrutura, executei:

```
terraform destroy
```

![Print do PowerShell mostrando o comando terraform destroy](/assets/8.jpeg.jpeg)
![Print do PowerShell mostrando o comando terraform destroy](/assets/9.jpeg.jpeg)
