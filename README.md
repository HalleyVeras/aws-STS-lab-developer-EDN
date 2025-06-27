# 🔐 Laboratório Prático: AWS Security Token Service (STS)

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

🖼️ [Insira aqui um print do CloudShell aberto com boto3 instalado]

🔐 Passo 2: Criando a Role Temporária
Vá até IAM > Funções > Criar função

Escolha "Política de confiança personalizada"

Adicione o ARN do seu usuário IAM como entidade confiável

Conceda a política AmazonS3FullAccess

Nomeie como SeuNomeRole

🖼️ [Insira print da configuração da Role]


🔄 Passo 3: Alternando para a Role
Clique no seu nome > "Alternar função"

Insira o ID da conta, SeuNomeRole e uma cor para diferenciar

Valide que você tem acesso ao S3 e não ao Lambda


```bash
aws sts get-caller-identity
```
🖼️ [Print com tela colorida indicando que está com a Role ativa]

🐍 Passo 4: Executar o Script Python
📥 Baixe o script: credenciais_temporarias.py

# Faça upload para o CloudShell
ls

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




