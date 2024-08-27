# PowerBIAnalyst

## Desafio Azure

Descrição do desafio módulo 3 – Processamento de Dados Simplificado com Power BI

### 1. Criação de uma instância na Azure para MySQL

- Feito a criação do mesmo.

### 2. Criar o Banco de Dados com Base Disponível no GitHub

- Criado e inserido os dados.

### 3. Integração do Power BI com MySQL no Azure

- Feita a integração.

### 4. Verificar Problemas na Base a Fim de Realizar a Transformação dos Dados

#### Diretrizes para Transformação dos Dados

1. **Verifique os cabeçalhos e tipos de dados**
   - Feito.

2. **Modifique os valores monetários para o tipo double preciso**
   - Feito.

3. **Verifique a existência dos nulos e analise a remoção**
   - Feito.

4. **Os employees com nulos em `Super_ssn` podem ser os gerentes. Verifique se há algum colaborador sem gerente**
   - Feito.

5. **Verifique se há algum departamento sem gerente**
   - Feito.

6. **Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas**
   - Ok.

7. **Verifique o número de horas dos projetos**
   - Ok.

8. **Separar colunas complexas**
   - Ok.

9. **Mesclar consultas `employee` e `department` para criar uma tabela `employee` com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela `employee`. Fique atento, essa informação influencia no tipo de junção**
   - Ok.

10. **Neste processo elimine as colunas desnecessárias**
    - Ok.

11. **Realize a junção dos colaboradores e respectivos nomes dos gerentes. Isso pode ser feito com consulta SQL ou pela mescla de tabelas com Power BI. Caso utilize SQL, especifique no README a query utilizada no processo**

    ```sql
    SELECT 
        e.Fname, 
        e.Lname, 
        e.Ssn, 
        e.Super_ssn,
        (SELECT CONCAT(supervisor.Fname, ' ', supervisor.Lname)
         FROM azure_company.employee AS supervisor
         WHERE supervisor.Ssn = e.Super_ssn
        ) AS Supervisor_Name
    FROM 
        azure_company.employee AS e;
    ```

12. **Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores**
    - Ok.

13. **Mescle os nomes de departamentos e localização. Isso fará com que cada combinação departamento-local seja única. Isso irá auxiliar na criação do modelo estrela em um módulo futuro**
    - Ok.

14. **Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir**

    Neste caso, não queremos adicionar ou modificar o conteúdo de uma coluna existente ou nova. Estamos apenas combinando dados de duas ou mais colunas em uma única coluna. Isso não altera o número de linhas na tabela. Como a intenção é consolidar informações para simplificar a análise e visualização dos dados, utilizamos o processo de mesclar.

15. **Agrupe os dados a fim de saber quantos colaboradores existem por gerente**

    ```sql
    SELECT 
        (SELECT CONCAT(supervisor.Fname, ' ', supervisor.Lname)
         FROM azure_company.employee AS supervisor
         WHERE supervisor.Ssn = e.Super_ssn
        ) AS Supervisor_Name, 
        COUNT(e.Fname) AS Quantidade
    FROM 
        azure_company.employee AS e
    GROUP BY 
        Supervisor_Name;
    ```

16. **Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela**
    - Ok.
