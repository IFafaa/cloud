# 💾 EC2 — Armazenamento (Resumo Completo)

## 📌 Visão Geral
Dentro das **instâncias EC2**, é possível configurar diferentes tipos de **armazenamento**, de acordo com a necessidade da aplicação.

De forma geral, o armazenamento pode ser dividido em:
- **SSD** → melhor desempenho
- **HDD** → menor custo por GB

👉 A escolha depende do tipo de workload e do custo-benefício desejado.

---

## ⚙️ Tipos de Disco (SSD x HDD)

### 🟦 SSD (Solid State Drive)
- Alta performance
- Baixa latência
- Ideal para:
  - Bancos de dados (ex: SQL Server, PostgreSQL, MySQL)
  - Aplicações que exigem alto IOPS
- Custo por GB mais elevado

---

### 🟫 HDD (Hard Disk Drive)
- Menor custo por GB
- Performance inferior ao SSD
- Ideal para:
  - Backups
  - Dados raramente acessados
  - Workloads que não exigem alta performance

📌 No EC2, você paga pelo **armazenamento provisionado**, não pelo uso.

---

## 🗄️ Serviços de Armazenamento

### 📦 Amazon EBS (Elastic Block Store)
- Armazenamento em bloco
- Pode ser anexado a **apenas uma instância EC2 por vez**
- Persistente (não é apagado ao desligar a instância, por padrão)
- Ideal para:
  - Sistema operacional
  - Bancos de dados
  - Aplicações que precisam de disco dedicado

---

### 📁 Amazon EFS (Elastic File System)
- Sistema de arquivos gerenciado
- Pode ser montado em:
  - Uma ou várias instâncias EC2
  - Múltiplas Zonas de Disponibilidade
- Alta disponibilidade e escalabilidade automática
- Ideal para:
  - Aplicações distribuídas
  - Compartilhamento de arquivos

---

### 🗃️ Amazon FSx
- Similar ao EFS, porém voltado para:
  - Windows
  - Sistemas de arquivos específicos
- Exemplos:
  - FSx for Windows File Server
  - FSx for Lustre
- Ideal para workloads corporativos ou de alta performance

---

## 📸 Snapshot

O **Snapshot** é um **backup do volume (EBS)**.

### Como funciona:
- O snapshot captura o estado atual do disco
- Fica armazenado no Amazon S3 (de forma gerenciada)
- Pode ser usado para:
  - Restaurar um volume
  - Criar um novo volume idêntico
  - Anexar o disco a outra instância

### Exemplo prático:
1. Criar um snapshot de um volume EBS
2. Deletar a instância original
3. Criar um novo volume a partir do snapshot
4. Anexar esse volume a uma nova instância

---

## 🧠 Resumo Mental (Visão Geral)

- EC2 Armazenamento
  - Tipos de Disco
    - SSD (Performance)
    - HDD (Custo)
  - Serviços
    - EBS
      - 1 instância por vez
    - EFS
      - Múltiplas instâncias
      - Multi-AZ
    - FSx
      - Windows e workloads específicos
  - Snapshot
    - Backup de volumes
    - Recuperação de dados

