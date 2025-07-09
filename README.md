# Locadora-de-Filmes
locadora-de-filmes/
│
├── der/
│   └── der_locadora_filmes.png    # imagem ou PDF do DER (modelo entidade-relacionamento)
│
├── scripts/
│   ├── criacao_tabelas.sql        # script SQL para criar tabelas (modelo físico)
│   ├── manipulacao_dados.sql      # scripts de inserção, atualização, exclusão
│   └── consultas.sql              # consultas SQL (mínimo 6 queries)
│
├── README.md                      # descrição do projeto e instruções
└── .gitignore                     # opcional, para ignorar arquivosdesnecessários

#Exemplo

# Projeto Banco de Dados: Locadora de Filmes

## 1. Nome e Tema do Projeto
**Locadora de Filmes** — Sistema para gerenciamento de aluguel de filmes, clientes e funcionários.

## 2. Descrição do Problema Modelado
Este projeto visa modelar e implementar um banco de dados para uma locadora de filmes que controla clientes, funcionários, filmes e locações, permitindo registrar quais filmes foram alugados, por quais clientes, em qual data, e o funcionário responsável.

## 3. Explicação das Entidades e Relacionamentos
- **Cliente**: armazena informações dos clientes da locadora.
- **Filme**: informações dos filmes disponíveis para aluguel.
- **Funcionario**: funcionários responsáveis pelas locações.
- **Locacao**: registros de aluguel feitos pelos clientes, associando cliente, funcionário e data.
- **Item_Locacao**: filmes específicos alugados em cada locação (resolve relação N:N entre locação e filme).

Os relacionamentos são:
- Um cliente pode fazer várias locações.
- Um funcionário registra várias locações.
- Uma locação pode conter vários filmes.
- Um filme pode ser alugado em várias locações.

## 4. Prints ou Exemplos das Consultas Realizadas

### Consulta 1: Listar todos os clientes
```sql
SELECT * FROM Cliente;

SELECT f.titulo
FROM Filme f
JOIN Item_Locacao il ON f.id_filme = il.id_filme
JOIN Locacao l ON il.id_locacao = l.id_locacao
WHERE l.id_cliente = 1;

SELECT id_locacao, valor_total FROM Locacao;

SELECT DISTINCT f.nome
FROM Funcionario f
JOIN Locacao l ON f.id_funcionario = l.id_funcionario
WHERE l.data_locacao = '2025-07-09';

SELECT c.nome, COUNT(il.id_filme) AS total_filmes
FROM Cliente c
JOIN Locacao l ON c.id_cliente = l.id_cliente
JOIN Item_Locacao il ON l.id_locacao = il.id_locacao
GROUP BY c.id_cliente;

SELECT titulo FROM Filme WHERE genero = 'Ação';
