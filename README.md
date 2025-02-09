# Sistema de Gerenciamento de Ordens de Serviço - Oficina Mecânica

## Descrição

Este projeto foi desenvolvido como parte de um desafio de design de banco de dados. O objetivo é modelar e implementar um sistema para o gerenciamento de ordens de serviço em uma oficina mecânica. 

## Objetivos do Projeto

- **Cliente PJ e PF**: Implementar um modelo onde os clientes possam ser pessoas físicas (PF) ou jurídicas (PJ), mas nunca ambos.
- **Formas de Pagamento**: Permitir que os clientes cadastrem múltiplas formas de pagamento.
- **Entrega**: Associar cada ordem de serviço (OS) a um status de entrega e código de rastreio.

## Modelo Conceitual

O modelo conceitual foi desenvolvido usando a ferramenta diagrams.net e pode ser encontrado na pasta `diagramas`.

## Atributos das Entidades

### Cliente
- `id_cliente` (PK)
- `tipo_cliente` (ENUM: "PJ" ou "PF")
- `CPF` (Apenas se PF)
- `CNPJ` (Apenas se PJ)

### Forma de Pagamento
- `id_pagamento` (PK)
- `tipo_pagamento` (Ex: "Cartão", "PIX", "Boleto")
- `detalhes_pagamento` (Informações adicionais)

### Entrega
- `id_entrega` (PK)
- `status` (Ex: "Pendente", "A caminho", "Entregue")
- `codigo_rastreio` (Identificação única)

### OS (Ordem de Serviço)
- `id_os` (PK)
- `data_emissao`
- `valor`
- `status`
- `data_conclusao`

## Relacionamentos

1. **Cliente - Forma de Pagamento**: Um cliente pode ter várias formas de pagamento.
2. **OS - Entrega**: Cada OS pode estar associada a uma única entrega.
3. **Cliente - OS**: Uma OS está sempre associada a um único cliente.

## Configuração

1. Baixe ou clone este repositório:

- 
![Image](https://github.com/user-attachments/assets/7f5d5e98-fed1-451e-b3c8-a0862ff34035)

 postgresql rsss ;)

-- Tabela Cliente
CREATE TABLE Cliente (
    id_cliente SERIAL PRIMARY KEY,
    tipo_cliente VARCHAR(2) CHECK (tipo_cliente IN ('PJ', 'PF')) NOT NULL,
    CPF VARCHAR(14) UNIQUE,  -- Apenas para PF
    CNPJ VARCHAR(18) UNIQUE  -- Apenas para PJ
);

-- Tabela Forma de Pagamento
CREATE TABLE FormaPagamento (
    id_pagamento SERIAL PRIMARY KEY,
    tipo_pagamento VARCHAR(50) NOT NULL,
    detalhes_pagamento TEXT,
    id_cliente INT NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente) ON DELETE CASCADE
);

-- Tabela OS (Ordem de Serviço)
CREATE TABLE OS (
    id_os SERIAL PRIMARY KEY,
    valor_total DECIMAL(10,2) NOT NULL,
    status VARCHAR(15) CHECK (status IN ('Aberta', 'Em Andamento', 'Finalizada')) NOT NULL,
    data_emissao TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Tabela Entrega
CREATE TABLE Entrega (
    id_entrega SERIAL PRIMARY KEY,
    status VARCHAR(10) CHECK (status IN ('Pendente', 'Entregue')) NOT NULL,
    codigo_rastreio VARCHAR(50) UNIQUE,
    id_os INT UNIQUE NOT NULL,  -- 1:1 com OS
    FOREIGN KEY (id_os) REFERENCES OS(id_os) ON DELETE CASCADE
);


## 🚀 Próximos Passos
✅ **Atualizar o diagrama conceitual** utilizando ferramentas como **Draw.io** ou **brModelo**.
✅ **Gerar um novo arquivo de diagrama** e adicioná-lo ao repositório GitHub.
✅ **Atualizar este `README.md`** com a explicação detalhada do modelo refinado.
✅ **Publicar as mudanças no GitHub**.

Caso tenha, vontade para contribuir! 💡

2. Acesse o arquivo do diagrama na pasta `diagramas/`.

## 👨‍💻 Autor
- **Bruno Molina Souza**  
Bruno Molina, Uma Pessoa com Deficiência Auditiva - PcD, curso de análise de dados,
estudante do curso superior de Tecnologia em Análise e Desenvolvimento de Sistemas. Unicesumar. 2024 - 2026
- [GitHub](https://github.com/brumab) | [LinkedIn](https://www.linkedin.com/in/brumab1122/) | [cv](https://brumab.github.io/cur/)


