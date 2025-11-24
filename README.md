# Projeto Conceitual de Banco de Dados - E-commerce

Este repositório contém o Modelo Conceitual e Lógico de banco de dados para um sistema de E-commerce: 'PC e-commerce.mwb' - Arquivo original do MySQL Workbench com o diagrama EER completo. O projeto foca na criação e no refinamento de um modelo, aplicando regras de negócios e melhores práticas de modelagem relacional (SQL).

## 📋 Visão Geral do Projeto

O objetivo deste projeto foi desenvolver e evoluir um diagrama entidade-relacionamento (DER) básico para um cenário realista de mercado, resolvendo conflitos de dados comuns em sistemas de vendas online, como a distinção legal entre diferentes entidades e a gestão de relacionamentos. Este projeto foi criado para cumprimento do Desafio 01 - Refinando um Projeto Conceitual de Banco de Dados E-commerce, proposto pela professora Juliana Mascarenhas, do curso de Formação SQL Database Specialist, da plataforma de ensino DIO (Digital Innovation One).

## 🛠 Ferramentas Utilizadas
* **MySQL Workbench** (Modelagem EER e criação do arquivo `.mwb`)
* **SQL** (Linguagem de Consulta Estruturada)

## 📜 Diretrizes e Regras de Negócio

O modelo deste projeto inicialmente foi desenvolvimento respeitando estritamente as narrativas e regras de negócio originais estabelecidas para o contexto comercial, levando em consideração os atrivutos e as entidades Cliente, Pedido, Produto, Fornecedor e Estoque. Durante o desenvolvimento, também foram adicionadas novas entidades principais (contendo chaves primárias), diferentes tipos de relacionamentos (1:1, 1:n e n:m) e entidades secundárias (contendo chaves estrangeiras) para melhorar a lógica do modelo.

## 🚀 Refinamentos e Decisões de Arquitetura

Abaixo estão as principais alterações implementadas no modelo original para atender aos requisitos de negócio e aprimorar a estrutura:

### 1. Gestão de Identidade (Cliente PF e PJ)

Para resolver o requisito de que uma conta pode ser PJ ou PF (nunca amabas), foi aplicada a técnica de **Especialização/Generalização (Herança)**:

* **Entidade Pai:** `Cliente` (Dados comuns: ID, Nome, dados de contato).
* **Entidades Filhas:** `Pessoa Fisica` e `Pessoa Juridica`.
* **Integridade:** Relacionamento 1:1 onde a Chave Primária (PK) das tabelas filhas também atua como Chave Estrangeira (FK), garantindo unicidade e evitando colunas nulas desnecessárias (como um campo CNPJ vazio para um cliente comum).

### 2. Múltiplos Meios de Pagamento

O modelo foi normalizado para permitir que um cliente cadastre múltiplas formas de pagamento (ex: dois cartões de crédito e uma chave Pix), em vez de limitar o pagamento a um único atributo do pedido.

* **Relacionamento:** 1:N (Um Cliente possui N Formas de Pagamento).
* **Segurança:** Separação de dados sensíveis com campos para detalhes anonimizados (tokens ou 4 últimos dígitos).
* **Observação Técnica:** Foi utilizado `TINYINT(1)` para controle de status (`ativo/inativo`), seguindo padrões do MySQL.

### 3. Logística e Entrega

A entrega foi desacoplada do pedido para permitir rastreamento granular e gestão de status independente (ex: um pedido pago pode ainda não ter sido enviado).

* **Entidade:** `Entrega` contendo Código de Rastreio e Status (`ENUM`).
* **Relacionamento:** Vinculado ao Pedido, permitindo expansão futura para múltiplas entregas por pedido (Split Shipment).

## 👣 Como Visualizar

1. Baixe e instale o [MySQL Workbench](https://www.mysql.com/products/workbench/).
2. Clone este repositório.
3. Abra o arquivo `.mwb` no MySQL Workbench para visualizar o diagrama e as propriedades das tabelas.

*Projeto desenvolvido como parte de desafio técnico de modelagem de dados.*
