# Passo a Passo para Criar uma Instância EC2 com Terraform

## Pré-Requisitos
- Acesso a uma consta de desenvolvimento no [AWS Academy](https://awsacademy.instructure.com/)

## Instalando o Terraform CLI no Ubuntu
Verificação e instalação de dependências:
```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```
Instalando a HashiCorp GPG key:
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```
Verificação da instalação da chave:
```bash
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```
O reultado do passo anterior deve ser assim:
```
/usr/share/keyrings/hashicorp-archive-keyring.gpg
-------------------------------------------------
pub   rsa4096 XXXX-XX-XX [SC]
AAAA AAAA AAAA AAAA
uid           [ unknown] HashiCorp Security (HashiCorp Package Signing) <security+packaging@hashicorp.com>
sub   rsa4096 XXXX-XX-XX [E]
```
Adicione o repositório da HashiCorp:
```bash
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```
Fazendo o download dos pacotes do HashiCorp:
```bash
sudo apt update
```
Instalando o Terraform:
```bash
sudo apt-get install terraform
```

## Instalando o AWS CLI
Comando para instalar o AWS CLI:
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
## Configurando as Credenciais da AWS
Utilize o comando 
```bash
aws configure
```
Após inicar as configurações do CLI, vá para a pasta de instalação:
```bash
cd ~\.aws\
```
Acesse o arquivo: credentials. Altere suas informações para as fornecidas dentro da AWS Academy:
```
[default]
aws_access_key_id = YOUR_ACCESS_KEY_ID
aws_secret_access_key = YOUR_SECRET_ACCESS_KEY
aws_session_token = YOUR_SESSION_TOKEN
```
## Criando uma Instância EC2 com Terraform
Crie um arquivo de configuração Terraform chamado main.tf com o seguinte conteúdo:
```
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

## Inicializando o Terraform
Abra o PowerShell no diretório onde está o arquivo main.tf e execute:
```
terraform init
```

## Planejando a Infraestrutura
Para ver o que será criado, execute:
```
terraform plan
```

## Aplicando a Configuração
Para criar a instância EC2, execute:
```
terraform apply
```
Digite YES quando solicitado para confirmar a aplicação da configuração.
