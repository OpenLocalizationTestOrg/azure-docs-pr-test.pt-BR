
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="40c98-101">Exemplo de programa em C#</span><span class="sxs-lookup"><span data-stu-id="40c98-101">C# program example</span></span>

<span data-ttu-id="40c98-102">As próximas seções deste artigo apresentam um programa C# que usa ADO.NET para enviar instruções Transact-SQL para o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="40c98-102">The next sections of this article present a C# program that uses ADO.NET to send Transact-SQL statements to the SQL database.</span></span> <span data-ttu-id="40c98-103">O programa C# executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="40c98-103">The C# program performs the following actions:</span></span>

1. <span data-ttu-id="40c98-104">[Conecta-se ao nosso Banco de Dados SQL usando o ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="40c98-104">[Connects to our SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="40c98-105">[Cria tabelas](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="40c98-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="40c98-106">[Preenche as tabelas com dados, emitindo instruções T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="40c98-106">[Populates the tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="40c98-107">[Atualiza os dados pelo uso de uma união](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="40c98-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="40c98-108">[Exclui os dados pelo uso de uma união](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="40c98-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="40c98-109">[Seleciona as linhas de dados pelo uso de uma união](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="40c98-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="40c98-110">Fecha a conexão (que descarta todas as tabelas temporárias de tempdb).</span><span class="sxs-lookup"><span data-stu-id="40c98-110">Closes the connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="40c98-111">O programa em C# contém:</span><span class="sxs-lookup"><span data-stu-id="40c98-111">The C# program contains:</span></span>

- <span data-ttu-id="40c98-112">Código C# para se conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40c98-112">C# code to connect to the database.</span></span>
- <span data-ttu-id="40c98-113">Métodos que retornam o código-fonte T-SQL.</span><span class="sxs-lookup"><span data-stu-id="40c98-113">Methods that return the T-SQL source code.</span></span>
- <span data-ttu-id="40c98-114">Dois métodos que enviam o T-SQL para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40c98-114">Two methods that submit the T-SQL to the database.</span></span>

#### <a name="to-compile-and-run"></a><span data-ttu-id="40c98-115">Para compilar e executar</span><span class="sxs-lookup"><span data-stu-id="40c98-115">To compile and run</span></span>

<span data-ttu-id="40c98-116">Este programa C# é logicamente um arquivo .cs.</span><span class="sxs-lookup"><span data-stu-id="40c98-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="40c98-117">Mas aqui o programa é dividido fisicamente em vários blocos de código, para facilitar a visualização e a compreensão de cada bloco.</span><span class="sxs-lookup"><span data-stu-id="40c98-117">But here the program is physically divided into several code blocks, to make each block easier to see and understand.</span></span> <span data-ttu-id="40c98-118">Para compilar e executar esse programa, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="40c98-118">To compile and run this program, do the following:</span></span>

1. <span data-ttu-id="40c98-119">Crie um novo projeto em C# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40c98-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="40c98-120">O tipo de projeto deve ser um *console* aplicativo de algo parecido com a seguinte hierarquia: **modelos** > **Visual C#** >  **Área de trabalho clássica do Windows** > **(.NET Framework) do aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="40c98-120">The project type should be a *console* application, from something like the following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="40c98-121">No arquivo **Program.cs**, apague as linhas iniciais do código.</span><span class="sxs-lookup"><span data-stu-id="40c98-121">In the file **Program.cs**, erase the small starter lines of code.</span></span>
3. <span data-ttu-id="40c98-122">Em Program.cs, copie e cole cada um dos blocos a seguir, na mesma sequência em que são apresentados aqui.</span><span class="sxs-lookup"><span data-stu-id="40c98-122">Into Program.cs, copy and paste each of the following blocks, in the same sequence they are presented here.</span></span>
4. <span data-ttu-id="40c98-123">Em Program.cs, edite os seguintes valores no método **principal**:</span><span class="sxs-lookup"><span data-stu-id="40c98-123">In Program.cs, edit the following values in the **Main** method:</span></span>

   - <span data-ttu-id="40c98-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="40c98-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="40c98-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="40c98-125">**cd.UserID**</span></span>
   - <span data-ttu-id="40c98-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="40c98-126">**cb.Password**</span></span>
   - <span data-ttu-id="40c98-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="40c98-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="40c98-128">Verifique se o assembly **System.Data.dll** é referenciado.</span><span class="sxs-lookup"><span data-stu-id="40c98-128">Verify that the assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="40c98-129">Para verificar, expanda o nó **Referências** no painel **Gerenciador de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="40c98-129">To verify, expand the **References** node in the **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="40c98-130">Para criar o programa no Visual Studio, clique no menu **Criar**.</span><span class="sxs-lookup"><span data-stu-id="40c98-130">To build the program in Visual Studio, click the **Build** menu.</span></span>
7. <span data-ttu-id="40c98-131">Para executar o programa do Visual Studio, clique no botão **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="40c98-131">To run the program from Visual Studio, click the **Start** button.</span></span> <span data-ttu-id="40c98-132">A saída do relatório é exibida em uma janela cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="40c98-132">The report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="40c98-133">Você tem a opção de editar a T-SQL para adicionar um líder  **#**  aos nomes de tabela, que cria como tabelas temporárias em **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="40c98-133">You have the option of editing the T-SQL to add a leading **#** to the table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="40c98-134">Isso pode ser útil para fins de demonstração, quando nenhum banco de dados de teste está disponível.</span><span class="sxs-lookup"><span data-stu-id="40c98-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="40c98-135">As tabelas temporárias são excluídas automaticamente quando a conexão é fechada.</span><span class="sxs-lookup"><span data-stu-id="40c98-135">Temporary tables are deleted automatically when the connection closes.</span></span> <span data-ttu-id="40c98-136">Nenhuma REFERÊNCIA a chaves estrangeiras é imposta para tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="40c98-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="40c98-137">Bloco C# 1: conectar-se usando o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="40c98-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="40c98-138">Próximo</span><span class="sxs-lookup"><span data-stu-id="40c98-138">Next</span></span>](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View the report output here, then press any key to end the program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-to-create-tables"></a><span data-ttu-id="40c98-139">Bloco C# 2: T-SQL para criar tabelas</span><span class="sxs-lookup"><span data-stu-id="40c98-139">C# block 2: T-SQL to create tables</span></span>

- <span data-ttu-id="40c98-140">[Anterior](#cs_1_connect) &nbsp; / &nbsp; [Avançar](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="40c98-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="40c98-141">Diagrama de relação de entidade (ERD)</span><span class="sxs-lookup"><span data-stu-id="40c98-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="40c98-142">As instruções CREATE TABLE precedentes envolvem a palavra-chave **REFERÊNCIAS** para criar uma relação *chave estrangeira* (FK) entre duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="40c98-142">The preceding CREATE TABLE statements involve the **REFERENCES** keyword to create a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="40c98-143">Se você estiver usando o tempdb, comente a palavra-chave `--REFERENCES` usando um par de traços à esquerda.</span><span class="sxs-lookup"><span data-stu-id="40c98-143">If you are using tempdb, comment out the `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="40c98-144">Em seguida, é um ERD que exibe a relação entre as duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="40c98-144">Next is an ERD that displays the relationship between the two tables.</span></span> <span data-ttu-id="40c98-145">Os valores da coluna *filho* #tabEmployee.DepartmentCode são limitados aos valores presentes na coluna *pai* #tabDepartment.Department.</span><span class="sxs-lookup"><span data-stu-id="40c98-145">The values in the #tabEmployee.DepartmentCode *child* column are limited to the values present in the #tabDepartment.Department *parent* column.</span></span>

![ERD mostrando chave estrangeira](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-to-insert-data"></a><span data-ttu-id="40c98-147">Bloco C# 3: T-SQL para inserir dados</span><span class="sxs-lookup"><span data-stu-id="40c98-147">C# block 3: T-SQL to insert data</span></span>

- <span data-ttu-id="40c98-148">[Anterior](#cs_2_createtables) &nbsp; / &nbsp; [Avançar](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="40c98-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- The company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- The company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-to-update-join"></a><span data-ttu-id="40c98-149">Bloco C# 4: T-SQL para atualizar com união</span><span class="sxs-lookup"><span data-stu-id="40c98-149">C# block 4: T-SQL to update-join</span></span>

- <span data-ttu-id="40c98-150">[Anterior](#cs_3_insert) &nbsp; / &nbsp; [Avançar](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="40c98-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-to-delete-join"></a><span data-ttu-id="40c98-151">Bloco C# 5: T-SQL para excluir com união</span><span class="sxs-lookup"><span data-stu-id="40c98-151">C# block 5: T-SQL to delete-join</span></span>

- <span data-ttu-id="40c98-152">[Anterior](#cs_4_updatejoin) &nbsp; / &nbsp; [Avançar](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="40c98-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size the Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband the Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-to-select-rows"></a><span data-ttu-id="40c98-153">Bloco C# 6: T-SQL para selecionar linhas</span><span class="sxs-lookup"><span data-stu-id="40c98-153">C# block 6: T-SQL to select rows</span></span>

- <span data-ttu-id="40c98-154">[Anterior](#cs_5_deletejoin) &nbsp; / &nbsp; [Avançar](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="40c98-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all the final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a><span data-ttu-id="40c98-155">Bloco C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="40c98-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="40c98-156">[Anterior](#cs_6_selectrows) &nbsp; / &nbsp; [Avançar](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="40c98-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="40c98-157">Esse método foi projetado para executar a instrução T-SQL SELECT que é criada com o método **Build_6_Tsql_SelectEmployees**.</span><span class="sxs-lookup"><span data-stu-id="40c98-157">This method is designed to run the T-SQL SELECT statement that is built by the **Build_6_Tsql_SelectEmployees** method.</span></span>


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="40c98-158">Bloco C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="40c98-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="40c98-159">[Anterior](#cs_6b_datareader) &nbsp; / &nbsp; [Avançar](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="40c98-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="40c98-160">Esse método é chamado para operações que modificam o conteúdo das tabelas de dados sem retornar nenhuma linha de dados.</span><span class="sxs-lookup"><span data-stu-id="40c98-160">This method is called for operations that modify the data content of tables without returning any data rows.</span></span>


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL to {0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-to-the-console"></a><span data-ttu-id="40c98-161">Bloco C# 8: saída de teste real para o console</span><span class="sxs-lookup"><span data-stu-id="40c98-161">C# block 8: Actual test output to the console</span></span>

- [<span data-ttu-id="40c98-162">Anterior</span><span class="sxs-lookup"><span data-stu-id="40c98-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="40c98-163">Esta seção captura a saída que o programa enviou ao console.</span><span class="sxs-lookup"><span data-stu-id="40c98-163">This section captures the output that the program sent to the console.</span></span> <span data-ttu-id="40c98-164">Somente os valores de guid variam entre as execuções de teste.</span><span class="sxs-lookup"><span data-stu-id="40c98-164">Only the guid values vary between test runs.</span></span>


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
