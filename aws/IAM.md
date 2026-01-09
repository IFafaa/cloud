# 🔐 AWS IAM — Resumo Completo

## 📌 O que é o AWS IAM
O **AWS IAM (Identity and Access Management)** é o serviço da AWS responsável por **gerenciar identidades, acessos e permissões** dentro de uma conta AWS.

Com o IAM, é possível controlar **quem pode acessar o console da AWS**, **quais serviços pode usar** e **quais ações pode executar**.

---

## 👥 Casos de Uso Comuns

O IAM permite criar usuários específicos para diferentes perfis dentro da empresa, por exemplo:

- **Desenvolvedor**
  - Acesso a serviços como:
    - AWS Lambda
    - EC2
    - S3
  - Sem acesso a informações financeiras

- **Funcionário do Financeiro**
  - Acesso apenas à:
    - Visualização de custos
    - Relatórios financeiros
  - Sem permissões técnicas ou administrativas

👉 Cada usuário possui permissões **mínimas e específicas**, seguindo o princípio do **menor privilégio**.

---

## 🧱 Usuários, Grupos e Roles

### 👤 Usuários (Users)
- Representam pessoas ou sistemas
- Possuem credenciais próprias (login e senha ou access keys)

---

### 👥 Grupos (Groups)
Permitem agrupar usuários com permissões semelhantes.

#### Exemplo:
- Grupo: `financial`
  - Contém todos os funcionários do financeiro
  - Facilita a gestão de permissões

---

### 🎭 Roles (Funções)
As **Roles** definem **o que pode ser feito** dentro da conta AWS.

- Grupos são associados a **políticas**
- Políticas definem permissões
- Roles são utilizadas por:
  - Serviços AWS
  - Aplicações
  - Usuários assumindo funções temporárias

#### Exemplo prático:
- Grupo `financial`
  - Associado a policies de:
    - Visualização de custos
    - Billing
  - Usuários herdam essas permissões automaticamente

---

## 📜 Policies (Políticas)

As **Policies** são documentos em **JSON** que definem permissões.

Elas controlam:
- Quais serviços podem ser acessados
- Quais ações são permitidas ou negadas
- Em quais recursos
- Sob quais condições

---

## 🔐 Segurança no IAM

### 🔑 MFA (Multi-Factor Authentication)
- Adiciona uma camada extra de segurança
- Requer algo que o usuário **sabe** (senha) + algo que **possui** (token/app)

👉 Altamente recomendado para todos os usuários  
👉 **Obrigatório para a conta root**

---

### 🔒 Política de Senhas
É possível configurar regras como:
- Tempo de expiração da senha
- Bloqueio de reutilização de senhas antigas
- Tamanho mínimo
- Complexidade (letras, números, símbolos)

---

## ⚠️ Conta Root — Atenção Máxima

- A conta **root** possui acesso total à conta AWS
- **Nunca deve ser usada no dia a dia**
- Deve ser usada apenas para:
  - Configurações iniciais
  - Atividades críticas da conta
  
---

## 🧠 Resumo Mental (Visão Geral)

- AWS IAM
  - Gerenciamento de Identidade
  - Controle de Acesso
  - Usuários
  - Grupos
  - Roles
  - Policies (JSON)
  - Segurança
    - MFA
    - Política de Senhas
  - Conta Root
    - MFA obrigatório
    - Uso restrito

