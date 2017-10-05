---
title: Integrar uma conta de armazenamento do Azure com a CDN do Azure | Microsoft Docs
description: "Saiba como usar a CDN (Rede de Distribuição de Conteúdo) do Azure para fornecer um conteúdo com alta largura de banda armazenando em cache os blobs a partir do Armazenamento do Azure."
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
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="e02e4-103">Integrar uma conta de armazenamento do Azure com a CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="e02e4-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="e02e4-104">CDN pode ser habilitada em cache o conteúdo do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e02e4-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="e02e4-105">Ela oferece aos desenvolvedores uma solução global para entrega de conteúdo de largura de banda armazenando em cache blobs e conteúdo estático de instâncias de computação em nós físicos nos Estados Unidos, Europa, Ásia, Austrália e América do Sul.</span><span class="sxs-lookup"><span data-stu-id="e02e4-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="e02e4-106">Etapa 1: Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e02e4-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="e02e4-107">Use o procedimento a seguir para criar uma nova conta de armazenamento para uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e02e4-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="e02e4-108">A conta de armazenamento dá acesso aos serviços de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e02e4-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="e02e4-109">A conta de armazenamento representa o mais alto nível do namespace para acessar cada um dos componentes do serviço de armazenamento do Azure: serviços Blob, serviços Fila e serviços Tabela.</span><span class="sxs-lookup"><span data-stu-id="e02e4-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="e02e4-110">Para obter mais informações, veja [Introdução ao Armazenamento do Microsoft Azure](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e02e4-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="e02e4-111">Para criar uma conta de armazenamento, você deve ser o administrador de serviços ou um coadministrador da assinatura associada.</span><span class="sxs-lookup"><span data-stu-id="e02e4-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e02e4-112">Há vários métodos que você pode usar para criar uma conta de armazenamento, incluindo o Portal do Azure e o Powershell.</span><span class="sxs-lookup"><span data-stu-id="e02e4-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="e02e4-113">Para este tutorial, usaremos o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e02e4-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="e02e4-114">**Para criar uma conta de armazenamento para uma assinatura do Azure**</span><span class="sxs-lookup"><span data-stu-id="e02e4-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="e02e4-115">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e02e4-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e02e4-116">No canto superior esquerdo, selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="e02e4-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="e02e4-117">No Diálogo **Novo**, selecione **Dados + Armazenamento** e clique em **Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e02e4-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="e02e4-118">A folha **Criar conta de armazenamento** aparece.</span><span class="sxs-lookup"><span data-stu-id="e02e4-118">The **Create storage account** blade appears.</span></span>   

    ![Criar conta de armazenamento][create-new-storage-account]  

3. <span data-ttu-id="e02e4-120">No campo **Nome** , digite um nome do subdomínio.</span><span class="sxs-lookup"><span data-stu-id="e02e4-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="e02e4-121">Essa entrada pode conter de 3 a 24 letras minúsculas e números.</span><span class="sxs-lookup"><span data-stu-id="e02e4-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="e02e4-122">Esse valor torna-se o nome de host no URI que é usado para lidar com os recursos de Blob, Fila ou Tabela da assinatura em questão.</span><span class="sxs-lookup"><span data-stu-id="e02e4-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="e02e4-123">Para atender a um recurso de contêiner no serviço Blob, você usaria um URI no seguinte formato, onde *&lt;StorageAccountLabel&gt;* refere-se ao valor digitado em **Inserir uma URL**:</span><span class="sxs-lookup"><span data-stu-id="e02e4-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="e02e4-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="e02e4-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="e02e4-125">**Importante:** o rótulo da URL forma o subdomínio do URI da conta de armazenamento e deve ser exclusivo entre todos os serviços hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="e02e4-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="e02e4-126">Esse valor também é usado como o nome dessa conta de armazenamento no portal ou ao acessar essa conta programaticamente.</span><span class="sxs-lookup"><span data-stu-id="e02e4-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="e02e4-127">Mantenha os padrões para **Modelo de implantação**, **Tipo de conta**, **Desempenho** e **Replicação**.</span><span class="sxs-lookup"><span data-stu-id="e02e4-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="e02e4-128">Selecione a **assinatura** que será usada com a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e02e4-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="e02e4-129">Selecione ou crie um **Grupo de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="e02e4-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="e02e4-130">Para saber mais sobre Grupos de Recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="e02e4-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="e02e4-131">Selecione um local para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e02e4-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="e02e4-132">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e02e4-132">Click **Create**.</span></span> <span data-ttu-id="e02e4-133">O processo de criação da conta de armazenamento pode levar vários minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="e02e4-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="e02e4-134">Etapa 2: Habilitar a CDN para a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e02e4-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="e02e4-135">Com a integração mais recente, agora você pode habilitar a CDN para sua conta de armazenamento sem sair de sua extensão do portal de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e02e4-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="e02e4-136">Selecione a conta de armazenamento, pesquise por "CDN" ou role para baixo no menu de navegação à esquerda e clique em "CDN do Azure".</span><span class="sxs-lookup"><span data-stu-id="e02e4-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="e02e4-137">A folha **CDN do Azure** é exibida.</span><span class="sxs-lookup"><span data-stu-id="e02e4-137">The **Azure CDN** blade appears.</span></span>

    ![navegação habilitada para cdn][cdn-enable-navigation]
    
2. <span data-ttu-id="e02e4-139">Crie um novo ponto de extremidade inserindo as informações necessárias</span><span class="sxs-lookup"><span data-stu-id="e02e4-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="e02e4-140">**Perfil CDN**: você pode criar um novo perfil ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="e02e4-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="e02e4-141">**Tipo de preço**: você precisa selecionar um tipo de preço apenas se criar um novo perfil CDN.</span><span class="sxs-lookup"><span data-stu-id="e02e4-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="e02e4-142">**Nome do ponto de extremidade da CDN**: insira um nome de ponto de extremidade de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="e02e4-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="e02e4-143">O ponto de extremidade da CDN criado usa o nome do host de sua conta de armazenamento como origem por padrão.</span><span class="sxs-lookup"><span data-stu-id="e02e4-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="e02e4-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span><span class="sxs-lookup"><span data-stu-id="e02e4-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="e02e4-145">Após a criação, o novo ponto de extremidade aparecerá na lista de pontos de extremidade acima.</span><span class="sxs-lookup"><span data-stu-id="e02e4-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![novo ponto de extremidade do armazenamento da cdn][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="e02e4-147">Você também pode ir para a extensão da CDN do Azure para habilitar o CDN.[Tutorial](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="e02e4-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="e02e4-148">Etapa 3: Habilitar recursos adicionais da CDN</span><span class="sxs-lookup"><span data-stu-id="e02e4-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="e02e4-149">Na folha de "CDN do Azure" da conta de armazenamento, clique no ponto de extremidade da CDN na lista para abrir a folha de configuração da CDN.</span><span class="sxs-lookup"><span data-stu-id="e02e4-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="e02e4-150">Você pode habilitar recursos adicionais da CDN para o fornecimento, como compactação, cadeia de caracteres de consulta e filtragem de área geográfica.</span><span class="sxs-lookup"><span data-stu-id="e02e4-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="e02e4-151">Você também pode adicionar o mapeamento de domínio personalizado ao seu ponto de extremidade da CDN e habilitar HTTPS do domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="e02e4-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![configuração da cdn do armazenamento da CDN][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="e02e4-153">Etapa 4: acessar conteúdo da CDN</span><span class="sxs-lookup"><span data-stu-id="e02e4-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="e02e4-154">Para acessar o conteúdo armazenado em cache na CDN, utilize a URL da CDN fornecida no portal.</span><span class="sxs-lookup"><span data-stu-id="e02e4-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="e02e4-155">O endereço de um blob armazenado em cache será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="e02e4-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="e02e4-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="e02e4-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="e02e4-157">Depois que você habilitar o acesso à CDN para uma conta de armazenamento, todos os objetos disponíveis publicamente estarão qualificados para armazenamento em cache de borda da CDN.</span><span class="sxs-lookup"><span data-stu-id="e02e4-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="e02e4-158">Se você modificar um objeto que está armazenado em cache na CDN atualmente, o novo conteúdo não estará disponível por meio da CDN até que a CDN atualize seu conteúdo quando o período de vida do conteúdo em cache expirar.</span><span class="sxs-lookup"><span data-stu-id="e02e4-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="e02e4-159">Etapa 5: remover conteúdo da CDN</span><span class="sxs-lookup"><span data-stu-id="e02e4-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="e02e4-160">Se não desejar mais armazenar em cache um objeto na CDN (Rede de Distribuição de Conteúdo) do Azure, você poderá executar uma das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e02e4-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="e02e4-161">Você pode tornar o contêiner particular em vez de público.</span><span class="sxs-lookup"><span data-stu-id="e02e4-161">You can make the container private instead of public.</span></span> <span data-ttu-id="e02e4-162">Veja [Gerenciar acesso anônimo de leitura aos contêineres e blobs](../storage/blobs/storage-manage-access-to-resources.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="e02e4-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="e02e4-163">Você pode desabilitar ou excluir o ponto de extremidade CDN usando o Portal de Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="e02e4-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="e02e4-164">Você pode modificar seu serviço hospedado para não responder a solicitações do objeto.</span><span class="sxs-lookup"><span data-stu-id="e02e4-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="e02e4-165">Um objeto que já está armazenado em cache na CDN permanecerá em cache até que o período de vida útil do objeto expire ou até que o ponto de extremidade seja limpo.</span><span class="sxs-lookup"><span data-stu-id="e02e4-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="e02e4-166">Quando o período de vida expira, a CDN verifica se o ponto de extremidade CDN ainda é válido, e se o objeto ainda pode ser acessado anonimamente.</span><span class="sxs-lookup"><span data-stu-id="e02e4-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="e02e4-167">Se não for, o objeto não estará mais armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="e02e4-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e02e4-168">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e02e4-168">Additional resources</span></span>
* [<span data-ttu-id="e02e4-169">Como mapear o conteúdo da CDN para um domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="e02e4-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="e02e4-170">Habilitar o HTTPS para seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="e02e4-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
