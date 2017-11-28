---
title: Use o Visual Studio e o .NET para consultar o Banco de Dados SQL do Azure | Microsoft Docs
description: "Este tópico mostra como usar o Visual Studio para criar um programa que se conecta a um banco de dados SQL do Azure e consultá-lo usando instruções Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 105dab17823a7e7f6957a604833f4ecad35c14bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-c-with-visual-studio-to-connect-and-query-an-azure-sql-database"></a><span data-ttu-id="1f47e-103">Usar o .NET (C#) com o Visual Studio para se conectar e consultar um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1f47e-103">Use .NET (C#) with Visual Studio to connect and query an Azure SQL database</span></span>

<span data-ttu-id="1f47e-104">Este tutorial de início rápido demonstra como usar o [.NET framework](https://www.microsoft.com/net/) para criar um programa C# com o Visual Studio para se conectar a um banco de dados SQL do Azure e usar instruções Transact-SQL para consultar dados.</span><span class="sxs-lookup"><span data-stu-id="1f47e-104">This quick start tutorial demonstrates how to use the [.NET framework](https://www.microsoft.com/net/) to create a C# program with Visual Studio to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f47e-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1f47e-105">Prerequisites</span></span>

<span data-ttu-id="1f47e-106">Para concluir este tutorial de início rápido, tenha o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1f47e-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="1f47e-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f47e-107">An Azure SQL database.</span></span> <span data-ttu-id="1f47e-108">Este início rápido usa os recursos criados em um destes inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="1f47e-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="1f47e-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="1f47e-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="1f47e-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="1f47e-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="1f47e-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f47e-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="1f47e-112">Uma [regra de firewall no nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público do computador usado neste tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="1f47e-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="1f47e-113">Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1f47e-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="1f47e-114">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="1f47e-114">SQL server connection information</span></span>

<span data-ttu-id="1f47e-115">Obtenha as informações de conexão necessárias para se conectar ao Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f47e-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="1f47e-116">Você precisará do nome totalmente qualificado do servidor, nome do banco de dados e informações de logon nos próximos procedimentos.</span><span class="sxs-lookup"><span data-stu-id="1f47e-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="1f47e-117">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1f47e-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1f47e-118">Selecione **Bancos de Dados SQL** no menu à esquerda e clique em seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="1f47e-119">Na página **Visão geral** do banco de dados, examine o nome totalmente qualificado do servidor, como mostrado na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f47e-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="1f47e-120">Você pode passar o mouse sobre o nome do servidor para abrir a opção **Clique para copiar**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="1f47e-122">Se você esquecer as informações de logon para o servidor do Banco de Dados SQL do Azure, navegue até a página do servidor do Banco de Dados SQL para exibir o nome de administrador do servidor.</span><span class="sxs-lookup"><span data-stu-id="1f47e-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="1f47e-123">Você pode redefinir a senha, se necessário.</span><span class="sxs-lookup"><span data-stu-id="1f47e-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="1f47e-124">Clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="1f47e-125">Examine a cadeia de conexão completa do **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-125">Review the complete **ADO.NET** connection string.</span></span>

    ![Cadeia de conexão do ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="1f47e-127">Você deve ter uma regra de firewall em vigor para o endereço IP público do computador em que você executa este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1f47e-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="1f47e-128">Se você estiver em um computador diferente ou se tiver um endereço IP público diferente, crie uma [regra de firewall no nível de servidor usando o portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="1f47e-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="1f47e-129">Criar um novo projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f47e-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="1f47e-130">No Visual Studio, escolha **Arquivo**, **Novo**, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="1f47e-131">No diálogo **Novo Projeto** e expanda **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-131">In the **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="1f47e-132">Selecione **Aplicativo de Console** e insira *sqltest* como o nome do projeto.</span><span class="sxs-lookup"><span data-stu-id="1f47e-132">Select **Console App** and enter *sqltest* for the project name.</span></span>
4. <span data-ttu-id="1f47e-133">Clique em **OK** para criar e abrir o novo projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f47e-133">Click **OK** to create and open the new project in Visual Studio</span></span>
4. <span data-ttu-id="1f47e-134">No Gerenciador de Soluções, clique com o botão direito do mouse em **sqltest** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="1f47e-135">Em **Procurar**, procure ```System.Data.SqlClient``` e, quando encontrado, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="1f47e-135">On the **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="1f47e-136">Na página **System.Data.SqlClient**, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-136">In the **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="1f47e-137">Quando a instalação for concluída, revise as alterações e então clique em **OK** para fechar a janela **Visualização**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-137">When the install completes, review the changes and then click **OK** to close the **Preview** window.</span></span> 
8. <span data-ttu-id="1f47e-138">Se uma janela **Aceitação da Licença** for exibida, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="1f47e-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="1f47e-139">Inserir código para consultar o banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="1f47e-139">Insert code to query SQL database</span></span>
1. <span data-ttu-id="1f47e-140">Alternar para (ou abrir, se necessário) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="1f47e-140">Switch to (or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="1f47e-141">Substitua o conteúdo de **Program.cs** pelo código a seguir e adicione os valores apropriados para seu servidor, banco de dados, usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="1f47e-141">Replace the contents of **Program.cs** with the following code and add the appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-the-code"></a><span data-ttu-id="1f47e-142">Executar o código</span><span class="sxs-lookup"><span data-stu-id="1f47e-142">Run the code</span></span>

1. <span data-ttu-id="1f47e-143">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f47e-143">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="1f47e-144">Verifique se as 20 linhas superiores são retornadas e, em seguida, feche a janela do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f47e-144">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f47e-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f47e-145">Next steps</span></span>

- <span data-ttu-id="1f47e-146">Saiba como [se conectar e consultar um banco de dados SQL do Azure usando o .NET core](sql-database-connect-query-dotnet-core.md) no Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="1f47e-146">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="1f47e-147">Saiba mais sobre a [Introdução ao .NET Core no Windows/Linux/macOS usando a linha de comando](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="1f47e-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="1f47e-148">Saiba como [Projetar seu primeiro banco de dados SQL do Azure usando o SSMS](sql-database-design-first-database.md) ou [Projetar seu primeiro banco de dados SQL do Azure usando o .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1f47e-148">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="1f47e-149">Para saber mais sobre o .NET, veja a [documentação do .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="1f47e-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
