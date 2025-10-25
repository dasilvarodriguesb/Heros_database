# 🦸‍♂️ Banco de Dados — Universo dos Heróis

Este repositório contém uma base de dados relacional sobre personagens de histórias em quadrinhos, suas editoras, criadores, cidades e grupos.

O projeto foi desenvolvido com fins **didáticos**, servindo de apoio para o ensino de **modelagem de dados** e **comandos SQL**.

---

## 🧩 Modelo Conceitual

O modelo entidade-relacionamento do banco está representado na imagem abaixo:

📄 **Arquivo:** `modelo de dados Herois.png`

O diagrama ilustra as entidades principais e seus relacionamentos, como mostrado a seguir:

| Entidade | Descrição | Atributos principais |
| :--- | :--- | :--- |
| **Editora** | Empresas responsáveis pelos quadrinhos | `cod_editora`, `nome`, `fundador` |
| **Cidade** | Cidades e países de origem dos personagens | `cod_cid`, `nome`, `pais` |
| **Personagem** | Heróis e vilões com suas características | `cod_perso`, `alterego`, `nm_heroi`, `apelido`, `habilidade`, `armas` |
| **Criador** | Autores responsáveis pela criação dos personagens | `cod_criador`, `nome`, `pais` |
| **Grupo** | Equipes e ligas de heróis e vilões | `cod_grupo`, `nome` |

**As tabelas descritas estão relacionadass conforme diagrama abaixo:**

<img src="/IMG/DER.png" alt="DER" width="30%"/>
---

## 🗃️ Estrutura das Tabelas

O script SQL cria e popula as seguintes tabelas:

| Tabela | Função |
| :--- | :--- |
| `editora` | Editoras de HQs (Marvel, DC, Panini, etc.) |
| `cidade` | Cidades e países de origem dos personagens |
| `personagem` | Heróis e vilões com seus atributos |
| `criador` | Criadores dos personagens |
| `criadorpersonagem` | Relação N:N entre criadores e personagens |
| `grupo` | Grupos ou ligas de heróis e vilões |
| `equipe` | Relação N:N entre personagens e grupos |

---

## 🧠 Dependências e Integridade

* Cada **personagem** está vinculado a uma **cidade** e uma **editora**;
* Um **criador** pode ter desenvolvido múltiplos personagens;
* Um **grupo** pode ter múltiplos personagens associados;
* As *constraints* de chave primária e estrangeira garantem integridade referencial.

---

## 🧾 Exemplos de Consultas SQL

1.  **Listar todos os personagens e suas editoras**
    ```sql
    SELECT p.nm_heroi, e.nome AS editora
    FROM personagem p
    JOIN editora e ON e.cod_editora = p.cod_edit;
    ```
2.  **Mostrar criadores e os personagens criados**
    ```sql
    SELECT c.nome AS criador, p.nm_heroi, cp.ano
    FROM criadorpersonagem cp
    JOIN criador c ON c.cod_criador = cp.cod_cria
    JOIN personagem p ON p.cod_perso = cp.cod_persona
    ORDER BY cp.ano;
    ```
3.  **Exibir grupos e seus personagens**
    ```sql
    SELECT g.nome AS grupo, p.nm_heroi
    FROM equipe e
    JOIN grupo g ON g.cod_grupo = e.cod_grup
    JOIN personagem p ON p.cod_perso = e.cod_personag;
    ```
4.  **Listar personagens por país de origem**
    ```sql
    SELECT p.nm_heroi, c.pais
    FROM personagem p
    JOIN cidade c ON c.cod_cid = p.cod_cid
    ORDER BY c.pais;
    ```

---

## 🎓 Objetivo Educacional

O projeto permite explorar:

* Criação de tabelas e relacionamentos;
* Comandos **DDL** e **DML**;
* Consultas SQL com **JOIN**, **GROUP BY**, subconsultas e filtros;
* Interpretação de diagramas E-R.

---
