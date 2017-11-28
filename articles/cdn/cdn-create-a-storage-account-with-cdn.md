---
title: aaaIntegrate uma conta de armazenamento do Azure com o Azure CDN | Microsoft Docs
description: "Saiba como o conteúdo de rede de fornecimento de conteúdo (CDN) do Azure toodeliver alta largura de banda de saudação toouse armazenando em cache blobs do armazenamento do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="fc557-103">Integrar uma conta de armazenamento do Azure com a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="fc557-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="fc557-104">CDN pode ser habilitado toocache conteúdo do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc557-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="fc557-105">Ele oferece aos desenvolvedores uma solução global para distribuir o conteúdo de alta largura de banda ao armazenar em cache o conteúdo estático de instâncias de computação em nós físicos nos Estados Unidos de hello, Europa, Ásia, Austrália e América do Sul e blobs.</span><span class="sxs-lookup"><span data-stu-id="fc557-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="fc557-106">Etapa 1: Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fc557-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="fc557-107">Use Olá seguindo o procedimento toocreate uma nova conta de armazenamento para uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc557-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="fc557-108">A conta de armazenamento dá acesso aos serviços de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc557-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="fc557-109">conta de armazenamento de saudação representa o nível mais alto de Olá Olá namespace para acessar cada um dos componentes de serviço de armazenamento do Azure Olá: services, serviços de fila e tabela serviços de Blob.</span><span class="sxs-lookup"><span data-stu-id="fc557-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="fc557-110">Para obter mais informações, consulte toohello [tooMicrosoft Introdução armazenamento do Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc557-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="fc557-111">toocreate uma conta de armazenamento, você deve ser administrador de serviço hello ou um coadministrador para Olá associado assinatura.</span><span class="sxs-lookup"><span data-stu-id="fc557-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fc557-112">Há vários métodos que você pode usar toocreate uma conta de armazenamento, inclusive Olá Portal do Azure e do Powershell.</span><span class="sxs-lookup"><span data-stu-id="fc557-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="fc557-113">Para este tutorial, usaremos Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fc557-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="fc557-114">**toocreate uma conta de armazenamento para uma assinatura do Azure**</span><span class="sxs-lookup"><span data-stu-id="fc557-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="fc557-115">Entrar toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fc557-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fc557-116">No canto esquerdo superior do hello, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="fc557-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="fc557-117">Em Olá **novo** caixa de diálogo, selecione **dados + armazenamento**, em seguida, clique em **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="fc557-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="fc557-118">Olá **criar conta de armazenamento** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="fc557-118">hello **Create storage account** blade appears.</span></span>   

    ![Criar conta de armazenamento][create-new-storage-account]  

3. <span data-ttu-id="fc557-120">Em Olá **nome** , digite um nome de subdomínio.</span><span class="sxs-lookup"><span data-stu-id="fc557-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="fc557-121">Essa entrada pode conter de 3 a 24 letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="fc557-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="fc557-122">Esse valor se torna o nome do host Olá no hello URI que é usado para endereçar recursos de Blob, fila ou tabela para a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc557-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="fc557-123">Para endereçar um recurso de contêiner no serviço Blob da saudação, você usaria um URI no hello seguinte formato, onde * &lt;StorageAccountLabel&gt; * refere-se o valor de toohello que você digitou na **insira uma URL**:</span><span class="sxs-lookup"><span data-stu-id="fc557-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="fc557-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="fc557-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="fc557-125">**Importante:** Olá subdomínio do URL rótulo formulários Olá Olá da conta de armazenamento URI e deve ser exclusivo entre todos os serviços hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="fc557-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="fc557-126">Esse valor também é usado como nome de saudação dessa conta de armazenamento no portal de hello, ou ao acessar essa conta por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="fc557-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="fc557-127">Mantenha os padrões de saudação para **modelo de implantação**, **conta tipo**, **desempenho**, e **replicação**.</span><span class="sxs-lookup"><span data-stu-id="fc557-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="fc557-128">Selecione Olá **assinatura** que a conta de armazenamento hello será usada com.</span><span class="sxs-lookup"><span data-stu-id="fc557-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="fc557-129">Selecione ou crie um **Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="fc557-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="fc557-130">Para saber mais sobre Grupos de Recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="fc557-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="fc557-131">Selecione um local para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc557-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="fc557-132">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fc557-132">Click **Create**.</span></span> <span data-ttu-id="fc557-133">processo de saudação de criação de conta de armazenamento Olá pode levar várias toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="fc557-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="fc557-134">Etapa 2: Habilitar a CDN Olá conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fc557-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="fc557-135">Com a integração mais recente do hello, agora você pode habilitar CDN para sua conta de armazenamento sem sair de sua extensão de portal de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fc557-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="fc557-136">Selecione a conta de armazenamento hello, pesquisar "CDN" ou role para baixo no menu de navegação à esquerda de saudação, clique em "CDN do Azure".</span><span class="sxs-lookup"><span data-stu-id="fc557-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="fc557-137">Olá **Azure CDN** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="fc557-137">hello **Azure CDN** blade appears.</span></span>

    ![navegação habilitada para cdn][cdn-enable-navigation]
    
2. <span data-ttu-id="fc557-139">Criar um novo ponto de extremidade inserindo informações de saudação necessária</span><span class="sxs-lookup"><span data-stu-id="fc557-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="fc557-140">**Perfil CDN**: você pode criar um novo perfil ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="fc557-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="fc557-141">**Camada de preços**: você só precisa tooselect um preço se você criar um novo perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="fc557-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="fc557-142">**Nome do ponto de extremidade da CDN**: insira um nome de ponto de extremidade de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="fc557-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="fc557-143">Por padrão, o ponto de extremidade CDN Olá criado usa Olá hostname de sua conta de armazenamento como origem.</span><span class="sxs-lookup"><span data-stu-id="fc557-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="fc557-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="fc557-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="fc557-145">Após a criação, novo ponto de extremidade de saudação aparecerão na lista de ponto de extremidade de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="fc557-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![novo ponto de extremidade do armazenamento da cdn][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="fc557-147">Você também pode ir tooAzure CDN extensão tooenable CDN. [Tutorial](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="fc557-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="fc557-148">Etapa 3: Habilitar recursos adicionais da CDN</span><span class="sxs-lookup"><span data-stu-id="fc557-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="fc557-149">Na folha de "Azure CDN" da conta de armazenamento, clique em ponto de extremidade CDN de saudação da folha de configuração Olá lista tooopen CDN.</span><span class="sxs-lookup"><span data-stu-id="fc557-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="fc557-150">Você pode habilitar recursos adicionais da CDN para o fornecimento, como compactação, cadeia de caracteres de consulta e filtragem de área geográfica.</span><span class="sxs-lookup"><span data-stu-id="fc557-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="fc557-151">Você também pode adicionar o ponto de extremidade CDN tooyour de mapeamento de domínio personalizado e habilitar HTTPS do domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="fc557-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![configuração da cdn do armazenamento da CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="fc557-153">Etapa 4: acessar conteúdo da CDN</span><span class="sxs-lookup"><span data-stu-id="fc557-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="fc557-154">use Olá URL CDN tooaccess armazenado em cache o conteúdo em Olá CDN, fornecido no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc557-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="fc557-155">endereço de saudação para um blob armazenado em cache será a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="fc557-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="fc557-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="fc557-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="fc557-157">Depois de habilitar a conta de armazenamento de tooa de acesso à CDN, todos os objetos publicamente disponíveis são qualificados para o cache de borda da CDN.</span><span class="sxs-lookup"><span data-stu-id="fc557-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="fc557-158">Se você modificar um objeto que está atualmente armazenada em cache Olá CDN, novo conteúdo de saudação não estará disponível por meio de saudação CDN até Olá CDN atualize seu conteúdo quando o período de tempo de vida conteúdo Olá armazenado em cache expira.</span><span class="sxs-lookup"><span data-stu-id="fc557-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="fc557-159">Etapa 5: Remover conteúdo da saudação CDN</span><span class="sxs-lookup"><span data-stu-id="fc557-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="fc557-160">Se você não deseja mais toocache um objeto no hello Azure Content Delivery Network (CDN), você pode executar uma das Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc557-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="fc557-161">Você pode fazer Olá privado de contêiner, e não público.</span><span class="sxs-lookup"><span data-stu-id="fc557-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="fc557-162">Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../storage/blobs/storage-manage-access-to-resources.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fc557-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="fc557-163">Você pode desabilitar ou excluir o ponto de extremidade CDN hello usando Olá Portal de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="fc557-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="fc557-164">Você pode modificar seu toorequests de responder mais tempo do serviço hospedado toono para objeto hello.</span><span class="sxs-lookup"><span data-stu-id="fc557-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="fc557-165">Um objeto já armazenado em cache no hello CDN permanecerá em cache até que Olá tempo de vida do objeto Olá expirar ou ponto de extremidade de saudação é apagado.</span><span class="sxs-lookup"><span data-stu-id="fc557-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="fc557-166">Quando o período de tempo de vida de saudação expira, Olá CDN verificará toosee se o ponto de extremidade do hello CDN ainda é válido e o objeto de saudação permanece acessível anonimamente.</span><span class="sxs-lookup"><span data-stu-id="fc557-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="fc557-167">Se não for, não será armazenada em objeto hello.</span><span class="sxs-lookup"><span data-stu-id="fc557-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc557-168">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fc557-168">Additional resources</span></span>
* [<span data-ttu-id="fc557-169">Como tooMap conteúdo CDN tooa domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="fc557-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="fc557-170">Habilitar o HTTPS para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="fc557-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
