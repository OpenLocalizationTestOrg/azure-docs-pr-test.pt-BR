---
title: aaaUse Visual Studio e .NET tooquery banco de dados do SQL Azure | Microsoft Docs
description: "Este tópico mostra como toouse Visual Studio toocreate um programa que se conecta tooan banco de dados do SQL Azure e a consulta usando instruções Transact-SQL."
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
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="1ef77-103">Use o .NET (c#) com o Visual Studio tooconnect e consultar um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1ef77-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="1ef77-104">Este tutorial de início rápido demonstra como Olá toouse [do .NET framework](https://www.microsoft.com/net/) toocreate c# programar com o banco de dados do Visual Studio tooconnect tooan SQL Azure e usar dados de tooquery de instruções Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="1ef77-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ef77-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ef77-105">Prerequisites</span></span>

<span data-ttu-id="1ef77-106">toocomplete rápido nesse tutorial de início, verifique se você tem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="1ef77-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="1ef77-107">Um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ef77-107">An Azure SQL database.</span></span> <span data-ttu-id="1ef77-108">Esse início rápido usa recursos de saudação criados em um desses inícios rápidos:</span><span class="sxs-lookup"><span data-stu-id="1ef77-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="1ef77-109">Criar Banco de dados - Portal</span><span class="sxs-lookup"><span data-stu-id="1ef77-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="1ef77-110">Criar Banco de dados - CLI</span><span class="sxs-lookup"><span data-stu-id="1ef77-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="1ef77-111">Criar Banco de dados - PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ef77-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="1ef77-112">Um [regra de firewall de nível de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para o endereço IP público de saudação do computador Olá usar para este tutorial de início rápido.</span><span class="sxs-lookup"><span data-stu-id="1ef77-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="1ef77-113">Uma instalação do [Visual Studio Community 2017, Visual Studio Professional 2017 ou Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1ef77-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="1ef77-114">Informações de conexão do servidor SQL</span><span class="sxs-lookup"><span data-stu-id="1ef77-114">SQL server connection information</span></span>

<span data-ttu-id="1ef77-115">Obter Olá conexão informações necessárias tooconnect toohello SQL Azure banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1ef77-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="1ef77-116">Será necessário o nome totalmente qualificado do servidor de saudação, nome do banco de dados e informações de logon em procedimentos Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="1ef77-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="1ef77-117">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ef77-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ef77-118">Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="1ef77-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="1ef77-119">Em Olá **visão geral** página do banco de dados, examine Olá nome totalmente qualificado do servidor conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="1ef77-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="1ef77-120">Você pode focalizar Olá toobring de nome de servidor backup Olá **clique toocopy** opção.</span><span class="sxs-lookup"><span data-stu-id="1ef77-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="1ef77-122">Se você esquecer suas informações de logon do banco de dados SQL server, navegue toohello banco de dados do SQL server página tooview Olá administrador nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="1ef77-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="1ef77-123">Você pode redefinir a senha de saudação se necessário.</span><span class="sxs-lookup"><span data-stu-id="1ef77-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="1ef77-124">Clique em **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="1ef77-125">Saudação de revisão completa **ADO.NET** cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="1ef77-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![Cadeia de conexão do ADO.NET](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="1ef77-127">Você deve ter uma regra de firewall em vigor para o endereço IP público de saudação do computador Olá em que você executa este tutorial.</span><span class="sxs-lookup"><span data-stu-id="1ef77-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="1ef77-128">Se você estiver em um computador diferente ou ter um endereço IP público diferente, crie um [regra de firewall de nível de servidor usando Olá portal do Azure](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="1ef77-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="1ef77-129">Criar um novo projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ef77-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="1ef77-130">No Visual Studio, escolha **Arquivo**, **Novo**, **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="1ef77-131">Em Olá **novo projeto** caixa de diálogo e expanda **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="1ef77-132">Selecione **aplicativo de Console** e digite *sqltest* para nome do projeto hello.</span><span class="sxs-lookup"><span data-stu-id="1ef77-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="1ef77-133">Clique em **Okey** toocreate e Olá Abrir novo projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ef77-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="1ef77-134">No Gerenciador de Soluções, clique com o botão direito do mouse em **sqltest** e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="1ef77-135">Em Olá **procurar**, procure ```System.Data.SqlClient``` e, quando encontrado, selecione-o.</span><span class="sxs-lookup"><span data-stu-id="1ef77-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="1ef77-136">Em Olá **SqlClient** , clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="1ef77-137">Quando Olá instalação for concluída, revise Olá alterações e, em seguida, clique em **Okey** tooclose Olá **visualização** janela.</span><span class="sxs-lookup"><span data-stu-id="1ef77-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="1ef77-138">Se uma janela **Aceitação da Licença** for exibida, clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="1ef77-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="1ef77-139">Insira o banco de dados SQL do código tooquery</span><span class="sxs-lookup"><span data-stu-id="1ef77-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="1ef77-140">Alternar muito (ou abrir se necessário) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="1ef77-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="1ef77-141">Substitua o conteúdo de saudação do **Program.cs** com hello seguinte código e adicionar os valores apropriados para seu servidor, banco de dados, usuário e senha hello.</span><span class="sxs-lookup"><span data-stu-id="1ef77-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="1ef77-142">Executar o código de saudação</span><span class="sxs-lookup"><span data-stu-id="1ef77-142">Run hello code</span></span>

1. <span data-ttu-id="1ef77-143">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="1ef77-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="1ef77-144">Verifique se que 20 linhas de saudação principais são retornadas e, em seguida, feche a janela do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1ef77-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ef77-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ef77-145">Next steps</span></span>

- <span data-ttu-id="1ef77-146">Saiba como muito[se conectar e consultar um banco de dados do SQL Azure usando o .NET core](sql-database-connect-query-dotnet-core.md) no Linux/Windows/macOS.</span><span class="sxs-lookup"><span data-stu-id="1ef77-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="1ef77-147">Saiba mais sobre [guia de Introdução ao .NET Core no Windows/Linux/macOS usando a linha de comando Olá](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="1ef77-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="1ef77-148">Saiba como muito[criar seu primeiro banco de dados SQL do Azure usando o SSMS](sql-database-design-first-database.md) ou [criar seu primeiro banco de dados SQL do Azure usando o .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="1ef77-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="1ef77-149">Para saber mais sobre o .NET, veja a [documentação do .NET](https://docs.microsoft.com/dotnet/).</span><span class="sxs-lookup"><span data-stu-id="1ef77-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>
