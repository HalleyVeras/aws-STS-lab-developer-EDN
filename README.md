# 🔐 Laboratório Prático: AWS Security Token Service (STS)

![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/CREATE%7E1.JPG)

**Autor:** Halley Veras  
**Curso: Developer – Escola da Nuvem** 
> Um mergulho prático no mundo das **credenciais temporárias na AWS**. Assuma roles, valide acessos, simule expiração e **surpreenda-se com o poder do STS**!

---

## 📌 Objetivo do Lab

✅ Criar uma Role temporária com acesso total ao S3  
✅ Assumir a Role via Console e CLI  
✅ Gerar credenciais temporárias via script Python  
✅ Simular o uso, expiração e restrições de acesso  
✅ Restaurar configurações ao final

---

## 🚀 Pré-Requisitos

- Conta AWS com permissão para:
  - Criar e assumir roles
  - Usar o **AWS CloudShell**
- Familiaridade com terminal (Linux) e AWS CLI
- Um espírito curioso e aventureiro!

---

## 🧠 Cenário

Você será um **usuário IAM** com superpoderes temporários! Vai criar uma **Role IAM com política de confiança personalizada**, assumir essa role via **Console e CLI**, gerar **tokens temporários** via script em Python e explorar permissões restritas (acesso ao S3, bloqueio ao Lambda, etc).

---

## 🔧 Passo 1: Configuração do Ambiente

```bash
# Abra o AWS CloudShell
sudo yum update -y
sudo yum install -y python3
python3 --version
pip3 install boto3 --upgrade
python3 -c "import boto3; print(boto3.__version__)"
```
---

![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-12.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-15.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-15_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-16.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-16_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-17.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-19.png)

🔐 Passo 2: Criando a Role Temporária
Vá até IAM > Funções > Criar função

Escolha "Política de confiança personalizada"

Adicione o ARN do seu usuário IAM como entidade confiável

Conceda a política AmazonS3FullAccess

Nomeie como SeuNomeRole

![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-20.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-21.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-21_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-29.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-30.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-32.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-32_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-33.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-34.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-35_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-36.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-37.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-37_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-37_2.png)


🔄 Passo 3: Alternando para a Role
Clique no seu nome > "Alternar função"

Insira o ID da conta, SeuNomeRole e uma cor para diferenciar

Valide que você tem acesso ao S3 e não ao Lambda

![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-39.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-42.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-44.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-44_1.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-45.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-47.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_15-37_2.png)

```bash
aws sts get-caller-identity
```
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_16-26.png)

🐍 Passo 4: Executar o Script Python
📥 Baixe o script: credenciais_temporarias.py

# Faça upload para o CloudShell
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_16-31.png)
![1](https://raw.githubusercontent.com/HalleyVeras/aws-STS-lab-developer-EDN/refs/heads/main/arquivos/2025-06-26_16-31_1.png)


```bash
ls
```
# Execute com duração inválida (erro esperado)
python3 credenciais_temporarias.py --role-arn arn:aws:iam::<SEU_ID>:role/SeuNomeRole --session-name Teste --duration 7200

# Execute com duração válida
python3 credenciais_temporarias.py --role-arn arn:aws:iam::<SEU_ID>:role/SeuNomeRole --session-name Teste --duration 3600


🔐 Passo 5: Configurar AWS CLI com as Credenciais Temporárias
```
aws configure
# Cole Access Key, Secret Key e região us-east-1
```
❌ Teste com erro (falta do token):
```
aws s3 ls
```

🔑 Passo 6: Adicionar o Session Token
```
sudo nano ~/.aws/credentials

# Adicione:
aws_session_token = SEU_SESSION_TOKEN

cat ~/.aws/credentials
```

✅ Teste novamente:
```
aws s3 ls
```
🔍 Passo 7: Verificações Finais
```
aws sts get-caller-identity
aws lambda list-functions  # Deve retornar acesso negado
```

⏰ Passo 8: Simular Expiração
Espere 1 hora ou use uptime para verificar. Após isso:

```
aws s3 ls  # Erro de credencial expirada
```

🧼 Passo 9: Restaurar Credenciais Originais

```
sudo nano ~/.aws/credentials  # Comente as linhas temporárias
sudo nano ~/.aws/config       # Comente as linhas de região/output

```
Valide identidade:


```
aws sts get-caller-identity


```


🛡️ Passo 10 a 13: Teste com Política de Confiança Modificada
Vá até a Role > Aba Relações de Confiança

Altere a política para incluir o ARN de outra role

Reexecute o script Python: Você verá um erro de acesso negado

🖼️ [Print com erro após alteração da política]




