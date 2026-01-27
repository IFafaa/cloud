# DB (Bancos de Dados na AWS)

A AWS também fornece serviços de bancos de dados dos mais variados tipos, para se adequar à sua necessidade.

## Tipos de Banco de Dados

### NoSQL
- DynamoDB
- CassandraDB
- MongoDB

### SQL - RDS (Relational Database Service)
- AuroraDB
- MySQL
- PostgreSQL
- MariaDB
- Microsoft SQL Server
- Oracle
- IBM DB

## DynamoDB (Destaque)

Em especial o **DynamoDB** (que foi analisado com mais atenção):

- Não é uma máquina EC2 rodando banco
- É um serviço totalmente gerenciado
- Extremamente rápido e escalável

## Bancos SQL Gerenciados

- A maioria dos bancos SQL são **máquinas EC2 rodando por trás**
- Em especial o **AuroraDB**:
  - Compatível com MySQL e PostgreSQL
  - Mais performático que ambos

## ElastiCache

Serviço de **cache** da AWS.

- Utiliza:
  - Redis
  - Memcached
- Recomendado para:
  - Diminuir o gargalo do banco de dados
  - Aumentar a performance das aplicações

## Amazon Neptune

Serviço de banco de dados **orientado a grafos**.

- Recomendado para:
  - Mídias sociais
  - Aplicações com muitas relações entre dados
  - Exemplo: Wikipedia

## AWS Glue

Serviço de **ETL (Extract, Transform, Load)**, recomendado para analytics.

- Extrai dados (ex: RDS ou S3)
- Transforma os dados com o Glue
- Carrega os dados no Redshift para visualização
