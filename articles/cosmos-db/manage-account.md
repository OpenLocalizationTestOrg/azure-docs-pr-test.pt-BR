---
title: "aaaManage uma conta de banco de dados do Azure Cosmos por meio de saudação Portal do Azure | Microsoft Docs"
description: "Saiba como toomanage seu banco de dados do Azure Cosmos conta por meio de saudação Portal do Azure. Localize um guia sobre como usar o hello Azure Portal tooview, copiar e excluir contas de acesso."
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="7e837-105">Como toomanage uma conta de banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="7e837-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="7e837-106">Saiba como trabalhar com chaves tooset de consistência global e excluir uma conta de banco de dados do Azure Cosmos Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e837-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="7e837-107"><a id="consistency"></a>Gerenciar as configurações de consistência do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e837-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="7e837-108">Selecionar um nível de consistência direita Olá depende da semântica de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e837-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="7e837-109">Você deve se familiarizar com níveis de consistência disponível Olá no banco de dados do Azure Cosmos lendo [usar consistência níveis toomaximize disponibilidade e desempenho no banco de dados do Azure Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="7e837-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="7e837-110">O Azure Cosmos DB fornece garantias de consistência, disponibilidade e desempenho, em cada nível de consistência disponível para sua conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e837-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="7e837-111">Configurar sua conta de banco de dados com um nível de consistência de alta segurança exige que seus dados são restrita tooa única região do Azure e não está disponível globalmente.</span><span class="sxs-lookup"><span data-stu-id="7e837-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="7e837-112">Olá outro lado, Olá níveis de consistência reduzida - desatualização associada, sessão ou eventual habilitar você tooassociate qualquer número de regiões do Azure com sua conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e837-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="7e837-113">Olá simples etapas a seguir mostra como tooselect Olá nível de consistência de padrão para sua conta de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e837-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="7e837-114">consistência do toospecify saudação padrão para uma conta de banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="7e837-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="7e837-115">Em Olá [portal do Azure](https://portal.azure.com/), acessar sua conta do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7e837-116">Na folha de conta hello, clique em **padrão consistência**.</span><span class="sxs-lookup"><span data-stu-id="7e837-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="7e837-117">Em Olá **consistência padrão** folha, o novo nível de consistência Olá selecione e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e837-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="7e837-118">![Sessão de consistência padrão][5]</span><span class="sxs-lookup"><span data-stu-id="7e837-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="7e837-119"><a id="keys"></a>Exibir, copiar e regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="7e837-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="7e837-120">Quando você cria uma conta de banco de dados do Azure Cosmos, o serviço de hello gera duas chaves de acesso principal que podem ser usadas para autenticação quando hello Azure Cosmos DB conta é acessada.</span><span class="sxs-lookup"><span data-stu-id="7e837-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="7e837-121">Fornecendo duas chaves de acesso, o banco de dados do Azure Cosmos permite chaves de saudação tooregenerate com tooyour sem interrupção conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="7e837-122">Em Olá [portal do Azure](https://portal.azure.com/), Olá acesso **chaves** folha no menu recursos Olá Olá de **conta de banco de dados do Azure Cosmos** tooview de folha, copiar e regenerar Olá chaves de acesso que são usados tooaccess sua conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Captura de tela do Portal do Azure, folha Chaves](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="7e837-124">Olá **chaves** folha também inclui primário e cadeias de caracteres de conexão secundário que podem ser usado tooconnect tooyour conta de saudação [ferramenta de migração de dados](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7e837-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="7e837-125">Chaves somente leitura também estão disponíveis nessa folha.</span><span class="sxs-lookup"><span data-stu-id="7e837-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="7e837-126">Leituras e consultas são operações somente leitura, ao contrário de criações, exclusões e substituições.</span><span class="sxs-lookup"><span data-stu-id="7e837-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="7e837-127">Copiar uma chave de acesso no hello Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e837-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="7e837-128">Em Olá **chaves** folha, clique em Olá **cópia** toohello botão à direita da chave de saudação desejar toocopy.</span><span class="sxs-lookup"><span data-stu-id="7e837-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Exibir e copiar uma chave de acesso no Portal do Azure, folha de chaves de saudação](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="7e837-130">Regenerar chaves de acesso</span><span class="sxs-lookup"><span data-stu-id="7e837-130">Regenerate access keys</span></span>
<span data-ttu-id="7e837-131">Você deve alterar a conta de banco de dados do Azure Cosmos Olá acesso chaves tooyour periodicamente toohelp manter suas conexões mais segura.</span><span class="sxs-lookup"><span data-stu-id="7e837-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="7e837-132">Duas chaves de acesso atribuídas tooenable você toomaintain conexões toohello conta de banco de dados do Azure Cosmos usando uma chave de acesso enquanto você regenera Olá outra chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="7e837-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="7e837-133">Regenerar suas chaves de acesso afeta todos os aplicativos que dependem da chave atual hello.</span><span class="sxs-lookup"><span data-stu-id="7e837-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="7e837-134">Clientes que usam a conta de banco de dados do Azure Cosmos Olá acesso à chave tooaccess Olá devem ser a nova chave de saudação toouse atualizado.</span><span class="sxs-lookup"><span data-stu-id="7e837-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="7e837-135">Se você tiver aplicativos ou serviços de nuvem usando hello Azure Cosmos DB conta, você perderá conexões Olá se você regenerar chaves, a menos que você reverter suas chaves.</span><span class="sxs-lookup"><span data-stu-id="7e837-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="7e837-136">Olá, etapas a seguir descrevem Olá processo envolvido na substituição de suas chaves.</span><span class="sxs-lookup"><span data-stu-id="7e837-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="7e837-137">Atualize a chave de acesso de saudação na sua chave de acesso secundária do aplicativo código tooreference Olá de hello Azure Cosmos DB conta.</span><span class="sxs-lookup"><span data-stu-id="7e837-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7e837-138">Regenere a chave de acesso primária Olá para sua conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="7e837-139">Em Olá [Portal do Azure](https://portal.azure.com/), acessar sua conta do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="7e837-140">Em Olá **conta de banco de dados do Azure Cosmos** folha, clique em **chaves**.</span><span class="sxs-lookup"><span data-stu-id="7e837-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="7e837-141">Em Olá **chaves** folha, clique botão regenerar hello, clique **Okey** tooconfirm que você deseja toogenerate uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="7e837-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="7e837-142">![Regenerar chaves de acesso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="7e837-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="7e837-143">Depois de verificar a nova chave hello está disponível para uso (aproximadamente 5 minutos após a regeneração), atualizar a chave de acesso de saudação na aplicativo código tooreference Olá nova chave de acesso primária.</span><span class="sxs-lookup"><span data-stu-id="7e837-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="7e837-144">Regenere a chave de acesso secundária hello.</span><span class="sxs-lookup"><span data-stu-id="7e837-144">Regenerate hello secondary access key.</span></span>
   
    ![Regenerar chaves de acesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="7e837-146">Pode levar vários minutos antes que uma chave gerada mais recentemente pode ser usado tooaccess sua conta de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="7e837-147">Obter cadeia de caracteres de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="7e837-147">Get hello  connection string</span></span>
<span data-ttu-id="7e837-148">tooretrieve sua conexão de cadeia de caracteres, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e837-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="7e837-149">Em Olá [portal do Azure](https://portal.azure.com), acessar sua conta do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7e837-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7e837-150">No menu de recursos de saudação, clique em **chaves**.</span><span class="sxs-lookup"><span data-stu-id="7e837-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="7e837-151">Clique em Olá **cópia** toohello próximo botão **cadeia de caracteres de Conexão primária** ou **cadeia de caracteres de Conexão secundária** caixa.</span><span class="sxs-lookup"><span data-stu-id="7e837-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="7e837-152">Se você estiver usando a cadeia de caracteres de conexão de saudação em Olá [ferramenta de migração de banco de dados de banco de dados do Azure Cosmos](import-data.md), acrescente término toohello do nome de banco de dados Olá de cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e837-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="7e837-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="7e837-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="7e837-154"><a id="delete"></a> Excluir uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e837-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="7e837-155">tooremove um banco de dados do Azure Cosmos Olá Portal do Azure que você já não estiver usando nome da conta com o botão direito hello, de conta e clique em **excluir conta**.</span><span class="sxs-lookup"><span data-stu-id="7e837-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Como a conta de toodelete um banco de dados do Azure Cosmos no hello Portal do Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="7e837-157">Em Olá [portal do Azure](https://portal.azure.com/), acessar a conta de banco de dados do Azure Cosmos Olá desejar toodelete.</span><span class="sxs-lookup"><span data-stu-id="7e837-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="7e837-158">Em Olá **conta de banco de dados do Azure Cosmos** folha, clique em conta hello e, em seguida, clique em **excluir conta**.</span><span class="sxs-lookup"><span data-stu-id="7e837-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="7e837-159">Na folha de confirmação resultante Olá, digite o nome de conta do hello Azure Cosmos DB tooconfirm que você deseja toodelete Olá conta.</span><span class="sxs-lookup"><span data-stu-id="7e837-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="7e837-160">Clique em Olá **excluir** botão.</span><span class="sxs-lookup"><span data-stu-id="7e837-160">Click hello **Delete** button.</span></span>

![Como a conta de toodelete um banco de dados do Azure Cosmos no hello Portal do Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="7e837-162"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e837-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="7e837-163">Saiba como muito[começar com sua conta do banco de dados do Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="7e837-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
