---
title: "Serviços de mídia aaaUpdate depois de implantar o armazenamento de chaves de acesso | Microsoft Docs"
description: "Este artigo oferece orientação sobre como tooupdate Media Services depois de implantar o armazenamento de chaves de acesso."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="24b92-103">Atualizar os Serviços de Mídia após implantar chaves de acesso de armazenamento</span><span class="sxs-lookup"><span data-stu-id="24b92-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="24b92-104">Quando você cria uma nova conta de serviços de mídia do Azure (AMS), você será solicitado tooselect um armazenamento do Azure da conta que é usada toostore seu conteúdo de mídia.</span><span class="sxs-lookup"><span data-stu-id="24b92-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="24b92-105">Você pode adicionar tooyour de contas de armazenamento mais de uma conta de serviços de mídia.</span><span class="sxs-lookup"><span data-stu-id="24b92-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="24b92-106">Este tópico mostra como toorotate chaves de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24b92-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="24b92-107">Ele também mostra como as contas de armazenamento tooadd tooa conta de mídia.</span><span class="sxs-lookup"><span data-stu-id="24b92-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="24b92-108">ações de saudação tooperform descritas neste tópico, você deve usar [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) e [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="24b92-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="24b92-109">Para obter mais informações, consulte [como toomanage Azure recursos com o PowerShell e o Gerenciador de recursos](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="24b92-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="24b92-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="24b92-110">Overview</span></span>

<span data-ttu-id="24b92-111">Quando uma nova conta de armazenamento é criada, o Azure gera duas chaves de acesso de armazenamento de 512 bits, que são usado tooauthenticate acessar tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24b92-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="24b92-112">tookeep suas conexões de armazenamento mais seguros, é recomendável tooperiodically regenerar e girar sua chave de acesso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24b92-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="24b92-113">Duas chaves de acesso (primárias e secundárias) são fornecidos na ordem tooenable você toomaintain conexões toohello conta de armazenamento usando um acesso chave enquanto você regenera Olá outra chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="24b92-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="24b92-114">Esse procedimento também é chamado de "implantação de chaves de acesso".</span><span class="sxs-lookup"><span data-stu-id="24b92-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="24b92-115">Serviços de mídia depende de uma chave de armazenamento fornecida tooit.</span><span class="sxs-lookup"><span data-stu-id="24b92-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="24b92-116">Especificamente, localizadores Olá toostream usado ou baixar seus ativos dependem de chave de acesso de armazenamento especificado hello.</span><span class="sxs-lookup"><span data-stu-id="24b92-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="24b92-117">Quando uma conta de AMS é criada que leva uma dependência na chave de acesso de armazenamento primário Olá por padrão, mas como um usuário, você pode atualizar a chave de armazenamento de saudação AMS tem.</span><span class="sxs-lookup"><span data-stu-id="24b92-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="24b92-118">Você deve se certificar de que os serviços de mídia toolet saber quais toouse chave seguindo as etapas descritas neste tópico.</span><span class="sxs-lookup"><span data-stu-id="24b92-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="24b92-119">Se tiver várias contas de armazenamento, você deverá executar esse procedimento com cada conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24b92-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="24b92-120">ordem de saudação na qual você rotação de chaves de armazenamento não é fixo.</span><span class="sxs-lookup"><span data-stu-id="24b92-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="24b92-121">Você pode girar a chave secundária Olá primeiro e, em seguida, Olá primário chave ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="24b92-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="24b92-122">Antes de executar as etapas descritas neste tópico em uma conta de produção, tootest se torná-los em uma conta de pré-produção.</span><span class="sxs-lookup"><span data-stu-id="24b92-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="24b92-123">Chaves de armazenamento toorotate etapas</span><span class="sxs-lookup"><span data-stu-id="24b92-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="24b92-124">Alteração Olá armazenamento chave primária da conta por meio do cmdlet do powershell hello ou [Azure](https://portal.azure.com/) portal.</span><span class="sxs-lookup"><span data-stu-id="24b92-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="24b92-125">Chamar o cmdlet de sincronização AzureRmMediaServiceStorageKeys com os parâmetros apropriados tooforce mídia conta toopick backup das chaves de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="24b92-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="24b92-126">saudação de exemplo a seguir mostra como toosync chaves toostorage contas.</span><span class="sxs-lookup"><span data-stu-id="24b92-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="24b92-127">Aguarde uma hora mais ou menos.</span><span class="sxs-lookup"><span data-stu-id="24b92-127">Wait an hour or so.</span></span> <span data-ttu-id="24b92-128">Verificar os cenários de streaming Olá estão funcionando.</span><span class="sxs-lookup"><span data-stu-id="24b92-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="24b92-129">Alterar a chave secundária de conta de armazenamento por meio do cmdlet do powershell hello ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="24b92-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="24b92-130">Chame powershell AzureRmMediaServiceStorageKeys de sincronização com os parâmetros apropriados tooforce mídia conta toopick backup novas chaves de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="24b92-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="24b92-131">Aguarde uma hora mais ou menos.</span><span class="sxs-lookup"><span data-stu-id="24b92-131">Wait an hour or so.</span></span> <span data-ttu-id="24b92-132">Verificar os cenários de streaming Olá estão funcionando.</span><span class="sxs-lookup"><span data-stu-id="24b92-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="24b92-133">Um exemplo de cmdlet do powershell</span><span class="sxs-lookup"><span data-stu-id="24b92-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="24b92-134">Olá exemplo a seguir demonstra como tooget Olá conta de armazenamento e sincronizá-lo com conta Olá AMS.</span><span class="sxs-lookup"><span data-stu-id="24b92-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="24b92-135">Contas de armazenamento de tooadd etapas tooyour AMS conta</span><span class="sxs-lookup"><span data-stu-id="24b92-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="24b92-136">Olá tópico a seguir mostra como as contas de armazenamento tooadd tooyour AMS conta: [anexar várias tooa de contas de armazenamento conta do Media Services](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="24b92-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="24b92-137">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="24b92-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24b92-138">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="24b92-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="24b92-139">Agradecimentos</span><span class="sxs-lookup"><span data-stu-id="24b92-139">Acknowledgments</span></span>
<span data-ttu-id="24b92-140">Gostaríamos Olá tooacknowledge pessoas que contribuíram para a criação deste documento a seguir: Cenk Dingiloglu, Gada Milão, Seva Titov.</span><span class="sxs-lookup"><span data-stu-id="24b92-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
