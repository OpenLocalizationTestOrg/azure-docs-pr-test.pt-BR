
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="d5643-101">Exemplo de programa em C#</span><span class="sxs-lookup"><span data-stu-id="d5643-101">C# program example</span></span>

<span data-ttu-id="d5643-102">próximas seções Olá deste artigo apresentam um programa c# que usa ADO.NET toosend Transact-SQL instruções toohello banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d5643-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="d5643-103">programa de saudação c# executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5643-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="d5643-104">[Conecta-se o banco de dados do SQL tooour usando o ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="d5643-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="d5643-105">[Cria tabelas](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="d5643-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="d5643-106">[Preenche as tabelas de saudação com dados, emitindo instruções T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="d5643-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="d5643-107">[Atualiza os dados pelo uso de uma união](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="d5643-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="d5643-108">[Exclui os dados pelo uso de uma união](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="d5643-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="d5643-109">[Seleciona as linhas de dados pelo uso de uma união](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="d5643-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="d5643-110">Fecha a conexão de saudação (que descarta todas as tabelas temporárias de tempdb).</span><span class="sxs-lookup"><span data-stu-id="d5643-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="d5643-111">programa Hello c# contém:</span><span class="sxs-lookup"><span data-stu-id="d5643-111">hello C# program contains:</span></span>

- <span data-ttu-id="d5643-112">C# código tooconnect toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d5643-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="d5643-113">Métodos que retornam o código-fonte Olá T-SQL.</span><span class="sxs-lookup"><span data-stu-id="d5643-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="d5643-114">Dois métodos que enviam Olá banco de dados do T-SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="d5643-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="d5643-115">toocompile e execução</span><span class="sxs-lookup"><span data-stu-id="d5643-115">toocompile and run</span></span>

<span data-ttu-id="d5643-116">Este programa C# é logicamente um arquivo .cs.</span><span class="sxs-lookup"><span data-stu-id="d5643-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="d5643-117">Mas aqui programa hello fisicamente é dividido em vários blocos de código, toomake cada bloco toosee mais fácil e entender.</span><span class="sxs-lookup"><span data-stu-id="d5643-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="d5643-118">toocompile e executar este programa, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5643-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="d5643-119">Crie um novo projeto em C# no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d5643-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="d5643-120">tipo de projeto Olá deve ser um *console* aplicativo de algo como Olá hierarquia a seguir: **modelos** > **Visual C#** > **Área de trabalho clássica do Windows** > **(.NET Framework) do aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="d5643-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="d5643-121">No arquivo hello **Program.cs**, apagar Olá starter pequenas linhas de código.</span><span class="sxs-lookup"><span data-stu-id="d5643-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="d5643-122">Em Program.cs, copiar e colar Olá seguinte blocos, em Olá mesma sequência que são apresentados aqui.</span><span class="sxs-lookup"><span data-stu-id="d5643-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="d5643-123">Em Program.cs, a seguir Olá editar valores hello **principal** método:</span><span class="sxs-lookup"><span data-stu-id="d5643-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="d5643-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="d5643-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="d5643-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="d5643-125">**cd.UserID**</span></span>
   - <span data-ttu-id="d5643-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="d5643-126">**cb.Password**</span></span>
   - <span data-ttu-id="d5643-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="d5643-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="d5643-128">Verifique se esse assembly hello **System.Data.dll** é referenciado.</span><span class="sxs-lookup"><span data-stu-id="d5643-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="d5643-129">tooverify, expanda Olá **referências** nó Olá **Solution Explorer** painel.</span><span class="sxs-lookup"><span data-stu-id="d5643-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="d5643-130">programa de saudação toobuild no Visual Studio, clique em Olá **criar** menu.</span><span class="sxs-lookup"><span data-stu-id="d5643-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="d5643-131">programa de saudação toorun do Visual Studio, clique em Olá **iniciar** botão.</span><span class="sxs-lookup"><span data-stu-id="d5643-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="d5643-132">saída de relatório de saudação é exibida em uma janela de cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="d5643-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="d5643-133">Você tem a opção de saudação de edição Olá T-SQL tooadd um principal  **#**  toohello nomes de tabela, que cria tabelas temporárias como no **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="d5643-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="d5643-134">Isso pode ser útil para fins de demonstração, quando nenhum banco de dados de teste está disponível.</span><span class="sxs-lookup"><span data-stu-id="d5643-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="d5643-135">Tabelas temporárias são excluídas automaticamente quando a conexão Olá fecha.</span><span class="sxs-lookup"><span data-stu-id="d5643-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="d5643-136">Nenhuma REFERÊNCIA a chaves estrangeiras é imposta para tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="d5643-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="d5643-137">Bloco C# 1: conectar-se usando o ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d5643-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="d5643-138">Próximo</span><span class="sxs-lookup"><span data-stu-id="d5643-138">Next</span></span>](#cs_2_createtables)


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
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="d5643-139">Bloco c# 2: tabelas de toocreate T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5643-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="d5643-140">[Anterior](#cs_1_connect) &nbsp; / &nbsp; [Avançar](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="d5643-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="d5643-141">Diagrama de relação de entidade (ERD)</span><span class="sxs-lookup"><span data-stu-id="d5643-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="d5643-142">instruções CREATE TABLE precedentes Hello envolvem Olá **referências** toocreate de palavra-chave um *chave estrangeira* relação (FK) entre duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="d5643-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="d5643-143">Se você estiver usando o tempdb, comente Olá `--REFERENCES` palavra-chave usando um par de traços à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d5643-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="d5643-144">Em seguida, é um ERD que exibe Olá relação entre duas tabelas de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5643-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="d5643-145">Olá valores hello #tabEmployee.DepartmentCode *filho* coluna são toohello limita os valores presentes na Olá #tabDepartment.Department *pai* coluna.</span><span class="sxs-lookup"><span data-stu-id="d5643-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![ERD mostrando chave estrangeira](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="d5643-147">C# bloco 3: dados de tooinsert T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5643-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="d5643-148">[Anterior](#cs_2_createtables) &nbsp; / &nbsp; [Avançar](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="d5643-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="d5643-149">C# bloco 4: junção tooupdate T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5643-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="d5643-150">[Anterior](#cs_3_insert) &nbsp; / &nbsp; [Avançar](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="d5643-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="d5643-151">Bloco c# 5: junção toodelete T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5643-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="d5643-152">[Anterior](#cs_4_updatejoin) &nbsp; / &nbsp; [Avançar](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="d5643-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="d5643-153">Bloco c# 6: linhas de tooselect T-SQL</span><span class="sxs-lookup"><span data-stu-id="d5643-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="d5643-154">[Anterior](#cs_5_deletejoin) &nbsp; / &nbsp; [Avançar](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="d5643-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="d5643-155">Bloco C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="d5643-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="d5643-156">[Anterior](#cs_6_selectrows) &nbsp; / &nbsp; [Avançar](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="d5643-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="d5643-157">Esse método é projetado toorun Olá T-SQL SELECT instrução que é criada pelo Olá **Build_6_Tsql_SelectEmployees** método.</span><span class="sxs-lookup"><span data-stu-id="d5643-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="d5643-158">Bloco C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="d5643-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="d5643-159">[Anterior](#cs_6b_datareader) &nbsp; / &nbsp; [Avançar](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="d5643-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="d5643-160">Esse método é chamado para operações que modificar o conteúdo dos dados das tabelas Olá sem retornar nenhuma linha de dados.</span><span class="sxs-lookup"><span data-stu-id="d5643-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="d5643-161">C# bloco 8: console de toohello de saída do teste real</span><span class="sxs-lookup"><span data-stu-id="d5643-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="d5643-162">Anterior</span><span class="sxs-lookup"><span data-stu-id="d5643-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="d5643-163">Esta seção captura saída Olá Olá programa enviado toohello console.</span><span class="sxs-lookup"><span data-stu-id="d5643-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="d5643-164">Somente os valores de guid Olá variam entre as execuções de teste.</span><span class="sxs-lookup"><span data-stu-id="d5643-164">Only hello guid values vary between test runs.</span></span>


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
