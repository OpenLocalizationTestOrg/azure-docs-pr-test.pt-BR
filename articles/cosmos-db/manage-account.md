---
title: Gerenciar uma conta do Azure Cosmos DB pelo Portal do Azure | Microsoft Docs
description: Saiba como gerenciar sua conta do Azure Cosmos DB pelo Portal do Azure. Encontre um guia sobre como usar o Portal do Azure para exibir, copiar, excluir e acessar contas.
keywords: Portal do Azure, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="1a824-105">Como gerenciar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a824-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="1a824-106">Saiba como definir a consistência global, trabalhar com chaves e excluir uma conta do Azure Cosmos DB no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a824-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="1a824-107"><a id="consistency"></a>Gerenciar as configurações de consistência do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a824-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="1a824-108">A seleção do nível certo de consistência depende da semântica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1a824-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="1a824-109">Familiarize-se com os níveis de consistência disponíveis no Azure Cosmos DB lendo [Usando níveis de consistência para maximizar a disponibilidade e o desempenho no Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="1a824-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="1a824-110">O Azure Cosmos DB fornece garantias de consistência, disponibilidade e desempenho, em cada nível de consistência disponível para sua conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1a824-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="1a824-111">A configuração da conta do banco de dados com um nível de consistência Strong exige que seus dados sejam confinados em uma única região do Azure, e não globalmente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1a824-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="1a824-112">Por outro lado, os níveis de consistência flexíveis — bounded staleness, session ou eventual — permitem associar qualquer número de regiões do Azure à sua conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1a824-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="1a824-113">As etapas simples a seguir mostram como selecionar o nível de consistência padrão para sua conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1a824-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="1a824-114">Para especificar a consistência padrão de uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a824-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="1a824-115">No [portal do Azure](https://portal.azure.com/), acesse sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="1a824-116">Na folha da conta, clique em **Consistência padrão**.</span><span class="sxs-lookup"><span data-stu-id="1a824-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="1a824-117">Na folha **Consistência Padrão**, selecione o novo nível de consistência e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1a824-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="1a824-118">![Sessão de consistência padrão][5]</span><span class="sxs-lookup"><span data-stu-id="1a824-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="1a824-119"><a id="keys"></a>Exibir, copiar e regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="1a824-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="1a824-120">Quando você cria uma conta do Azure Cosmos DB, o serviço gera duas chaves de acesso mestras que podem ser usadas para autenticação quando a conta do Azure Cosmos DB é acessada.</span><span class="sxs-lookup"><span data-stu-id="1a824-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="1a824-121">Ao fornecer duas chaves de acesso, o Azure Cosmos DB permite regenerar as chaves sem nenhuma interrupção na conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="1a824-122">No [portal do Azure](https://portal.azure.com/), acesse a folha **Chaves** no menu de recursos da folha **Conta do Azure Cosmos DB** para exibir, copiar e regenerar as chaves de acesso que são usadas para acessar sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Captura de tela do Portal do Azure, folha Chaves](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="1a824-124">A folha **Chaves** também inclui cadeias de conexão primárias e secundárias que podem ser usadas para se conectar à sua conta na [Ferramenta de Migração de Dados](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="1a824-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="1a824-125">Chaves somente leitura também estão disponíveis nessa folha.</span><span class="sxs-lookup"><span data-stu-id="1a824-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="1a824-126">Leituras e consultas são operações somente leitura, ao contrário de criações, exclusões e substituições.</span><span class="sxs-lookup"><span data-stu-id="1a824-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="1a824-127">Copiar uma chave de acesso no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1a824-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="1a824-128">Na folha **Chaves**, clique no botão **Copiar** à direita da chave que você quer copiar.</span><span class="sxs-lookup"><span data-stu-id="1a824-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="1a824-130">Regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="1a824-130">Regenerate access keys</span></span>
<span data-ttu-id="1a824-131">Você deve alterar as chaves de acesso de sua conta do Azure Cosmos DB periodicamente para ajudar a manter as conexões mais seguras.</span><span class="sxs-lookup"><span data-stu-id="1a824-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="1a824-132">Duas chaves de acesso são atribuídas para permitir que você mantenha conexões com a conta do Azure Cosmos DB usando uma chave de acesso enquanto regenera a outra.</span><span class="sxs-lookup"><span data-stu-id="1a824-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="1a824-133">A regeneração de suas chaves de acesso afeta quaisquer aplicativos que são dependentes da chave atual.</span><span class="sxs-lookup"><span data-stu-id="1a824-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="1a824-134">Todos os clientes que usam a chave de acesso para acessar a conta do Azure Cosmos DB devem ser informados para usarem a nova chave.</span><span class="sxs-lookup"><span data-stu-id="1a824-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="1a824-135">Se você tiver aplicativos ou serviços de nuvem que usam a conta do Azure Cosmos DB, perderá as conexões se regenerar as chaves, a menos que você as reverta.</span><span class="sxs-lookup"><span data-stu-id="1a824-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="1a824-136">As etapas a seguir descrevem o processo envolvido ao reverter suas chaves.</span><span class="sxs-lookup"><span data-stu-id="1a824-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="1a824-137">Atualize a chave de acesso no código do aplicativo para referenciar a chave de acesso secundária da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="1a824-138">Regenere a chave de acesso primária de sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="1a824-139">No [Portal do Azure](https://portal.azure.com/), acesse sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="1a824-140">Na folha **Conta do Azure Cosmos DB**, clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="1a824-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="1a824-141">Na folha **Chaves**, clique no botão Regenerar e clique em **Ok** para confirmar que você quer gerar uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="1a824-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="1a824-142">![Regenerar chaves de acesso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="1a824-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="1a824-143">Uma vez que você verificou que a nova chave está disponível para uso(aproximadamente 5 minutos após a regeneração), atualize a chave de acesso em seu código do aplicativo para fazer referência à nova chave de acesso principal.</span><span class="sxs-lookup"><span data-stu-id="1a824-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="1a824-144">Regenere a chave de acesso secundária.</span><span class="sxs-lookup"><span data-stu-id="1a824-144">Regenerate the secondary access key.</span></span>
   
    ![Regenerar chaves de acesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="1a824-146">Poderá levar alguns minutos para que a chave recém-gerada possa ser usada para acessar sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="1a824-147">Obtenha a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="1a824-147">Get the  connection string</span></span>
<span data-ttu-id="1a824-148">Para recuperar sua cadeia de conexão, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1a824-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="1a824-149">No [portal do Azure](https://portal.azure.com), acesse sua conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1a824-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="1a824-150">No menu de recursos, clique em **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="1a824-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="1a824-151">Clique no botão **Copiar** ao lado da caixa **Cadeia de conexão primária** ou **Cadeia de conexão secundária** caixa.</span><span class="sxs-lookup"><span data-stu-id="1a824-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="1a824-152">Se você estiver usando a cadeia de conexão na [Ferramenta de Migração de Banco de Dados do Azure Cosmos DB](import-data.md), acrescente o nome do banco de dados ao final da cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="1a824-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="1a824-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="1a824-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="1a824-154"><a id="delete"></a> Excluir uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a824-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="1a824-155">Para remover uma conta do Azure Cosmos DB no Portal do Azure que não está mais sendo usada, clique com o botão direito do mouse no nome da conta e, depois, clique em **Excluir conta**.</span><span class="sxs-lookup"><span data-stu-id="1a824-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Como excluir uma conta do Azure Cosmos DB no Portal do Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="1a824-157">No [portal do Azure](https://portal.azure.com/), acesse a conta do Azure Cosmos DB que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="1a824-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="1a824-158">Na folha **Conta do Azure Cosmos DB**, clique com o botão direito do mouse na conta e, depois, clique em **Excluir Conta**.</span><span class="sxs-lookup"><span data-stu-id="1a824-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="1a824-159">Na folha de confirmação resultante, digite o nome da conta do Azure Cosmos DB para confirmar que você deseja excluir a conta.</span><span class="sxs-lookup"><span data-stu-id="1a824-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="1a824-160">Clique no botão **Excluir** .</span><span class="sxs-lookup"><span data-stu-id="1a824-160">Click the **Delete** button.</span></span>

![Como excluir uma conta do Azure Cosmos DB no Portal do Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="1a824-162"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a824-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="1a824-163">Saiba como [começar a usar sua conta do Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="1a824-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
