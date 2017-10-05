---
title: "Atualizar para a biblioteca de cliente de banco de dados elástico mais recente | Microsoft Docs"
description: Atualizar aplicativos e bibliotecas usando o Nuget
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 7e28d128645e856c0efa6e4f78d8f9f36982a76c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="affcb-103">Atualizar um aplicativo para usar a biblioteca de cliente de banco de dados elástico mais recente</span><span class="sxs-lookup"><span data-stu-id="affcb-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="affcb-104">Novas versões da [biblioteca de cliente de Banco de Dados Elástico](sql-database-elastic-database-client-library.md) estão disponíveis por meio do NuGet e da interface do Gerenciador de Pacotes NuGet no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="affcb-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="affcb-105">Atualizações contêm correções de bugs e suporte para novos recursos de biblioteca de cliente.</span><span class="sxs-lookup"><span data-stu-id="affcb-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="affcb-106">**Para obter a versão mais recente:** acesse [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="affcb-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="affcb-107">Recompile seu aplicativo com a nova biblioteca, além de alterar os metadados do Gerenciador de Mapa de Fragmentos existentes armazenados em seus Bancos de Dados SQL do Azure para dar suporte aos novos recursos.</span><span class="sxs-lookup"><span data-stu-id="affcb-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="affcb-108">Executar estas etapas nesta ordem garante que as versões antigas da biblioteca de cliente não estejam mais presentes em seu ambiente quando objetos de metadados são atualizados, o que significa que os objetos de metadados da versão antiga não serão criados após a atualização.</span><span class="sxs-lookup"><span data-stu-id="affcb-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="affcb-109">Etapas de atualização</span><span class="sxs-lookup"><span data-stu-id="affcb-109">Upgrade steps</span></span>
<span data-ttu-id="affcb-110">**1. Atualize seus aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="affcb-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="affcb-111">No Visual Studio, baixe e referencie a versão mais recente da biblioteca do cliente em todos os seus projetos de desenvolvimento que usam a biblioteca. Em seguida, recrie e implante.</span><span class="sxs-lookup"><span data-stu-id="affcb-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="affcb-112">Em sua solução do Visual Studio, selecione **Ferramentas** --> **NuGet Package Manager** -->  **Gerenciar pacotes NuGet para solução**.</span><span class="sxs-lookup"><span data-stu-id="affcb-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="affcb-113">(Visual Studio 2013) No painel esquerdo, escolha **Atualizações** e selecione o botão **Atualizar** no pacote **Biblioteca de cliente de escala elástica do Banco de dados SQL do Azure** que aparece na janela.</span><span class="sxs-lookup"><span data-stu-id="affcb-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="affcb-114">(Visual Studio 2015) Defina a caixa de Filtro para **Atualização disponível**.</span><span class="sxs-lookup"><span data-stu-id="affcb-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="affcb-115">Selecione o pacote para atualizar e clique no botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="affcb-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="affcb-116">(2017 do visual Studio) Na parte superior da caixa de diálogo, selecione **Atualizações**.</span><span class="sxs-lookup"><span data-stu-id="affcb-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="affcb-117">Selecione o pacote para atualizar e clique no botão **Atualizar** .</span><span class="sxs-lookup"><span data-stu-id="affcb-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="affcb-118">Criar e implantar.</span><span class="sxs-lookup"><span data-stu-id="affcb-118">Build and Deploy.</span></span> 

<span data-ttu-id="affcb-119">**2. Atualize seus scripts.**</span><span class="sxs-lookup"><span data-stu-id="affcb-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="affcb-120">Se você estiver usando scripts do **PowerShell** para gerenciar os fragmentos, [baixe a nova versão da biblioteca](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) e copie-a para o diretório de onde você executa scripts.</span><span class="sxs-lookup"><span data-stu-id="affcb-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="affcb-121">**3. Atualize o seu serviço de mesclagem de divisão.**</span><span class="sxs-lookup"><span data-stu-id="affcb-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="affcb-122">Se você usar o serviço de mesclagem de divisão de banco de dados elástico para reorganizar dados fragmentados, [baixe e implante a versão mais recente do serviço](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span><span class="sxs-lookup"><span data-stu-id="affcb-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="affcb-123">Etapas detalhadas de atualização para o serviço podem ser encontradas [aqui](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="affcb-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="affcb-124">**4. Atualizar seus bancos de dados do Gerenciador do Mapa de Fragmentos**.</span><span class="sxs-lookup"><span data-stu-id="affcb-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="affcb-125">Atualizar os metadados que suportam seus mapas de fragmento no banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="affcb-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="affcb-126">Há duas maneiras que você pode fazer isso, usando o PowerShell ou C#.</span><span class="sxs-lookup"><span data-stu-id="affcb-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="affcb-127">Ambas as opções são mostradas abaixo.</span><span class="sxs-lookup"><span data-stu-id="affcb-127">Both options are shown below.</span></span>

<span data-ttu-id="affcb-128">***Opção 1: Atualizar os metadados usando o PowerShell***</span><span class="sxs-lookup"><span data-stu-id="affcb-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="affcb-129">Baixar o utilitário de linha de comando mais recente para NuGet [aqui](http://nuget.org/nuget.exe) e salvar em uma pasta.</span><span class="sxs-lookup"><span data-stu-id="affcb-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="affcb-130">Abra um Prompt de Comando, navegue para a mesma pasta e execute o comando: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="affcb-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="affcb-131">Navegue até a subpasta que contém a nova versão DLL do cliente que acabou de baixar, por exemplo: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="affcb-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="affcb-132">Baixe o scriptlet da atualização de clientes de banco de dados elástico do [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)e salve-o na mesma pasta que contém a DLL.</span><span class="sxs-lookup"><span data-stu-id="affcb-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="affcb-133">Nessa pasta, execute "PowerShell .\upgrade.ps1" no prompt de comando e siga os prompts.</span><span class="sxs-lookup"><span data-stu-id="affcb-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="affcb-134">***Opção 2: Atualizar os metadados usando C#***</span><span class="sxs-lookup"><span data-stu-id="affcb-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="affcb-135">Como alternativa, crie um aplicativo do Visual Studio que abre sua ShardMapManager, itera em todos os fragmentos e executa a atualização de metadados chamando os métodos [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) e [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="affcb-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="affcb-136">Essas técnicas para atualizações de metadados podem ser aplicadas várias vezes sem danos.</span><span class="sxs-lookup"><span data-stu-id="affcb-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="affcb-137">Por exemplo, se uma versão mais antiga do cliente cria inadvertidamente um fragmento depois que você atualizou, você pode executar a atualização novamente entre todos os fragmentos para garantir que a versão mais recente de metadados está presente em toda a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="affcb-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="affcb-138">**Observação:** Novas versões da biblioteca de cliente atualizadas continuam a funcionar com as versões anteriores dos metadados do Gerenciador de Mapa de Fragmentos no Banco de Dados SQL do Azure e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="affcb-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="affcb-139">No entanto, para aproveitar alguns dos novos recursos mais recente do cliente, os metadados precisam ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="affcb-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="affcb-140">Observe que as atualizações de metadados não afetarão nenhum dados do usuário ou dados específicos do aplicativo, somente os objetos criados e usados pelo Gerenciador de mapa de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="affcb-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="affcb-141">E os aplicativos continuam a operar na sequência de atualização descrita acima.</span><span class="sxs-lookup"><span data-stu-id="affcb-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="affcb-142">O histórico de versões de cliente do banco de dados elástico</span><span class="sxs-lookup"><span data-stu-id="affcb-142">Elastic database client version history</span></span>
<span data-ttu-id="affcb-143">Para ver o histórico de versão, vá para [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="affcb-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

