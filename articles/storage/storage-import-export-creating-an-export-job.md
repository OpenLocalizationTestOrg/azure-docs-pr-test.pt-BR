---
title: "aaaCreate uma exportação de trabalho de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocreate uma exportação de trabalho para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a><span data-ttu-id="b3cd9-103">Criar um trabalho de exportação para Olá serviço de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="b3cd9-103">Creating an export job for hello Azure Import/Export service</span></span>
<span data-ttu-id="b3cd9-104">Criar um trabalho de exportação para o serviço de importação/exportação do Microsoft Azure hello usando Olá API REST envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3cd9-104">Creating an export job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="b3cd9-105">Selecionar Olá blobs tooexport.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-105">Selecting hello blobs tooexport.</span></span>

-   <span data-ttu-id="b3cd9-106">Obter uma localização de envio.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="b3cd9-107">Criar trabalho de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-107">Creating hello export job.</span></span>

-   <span data-ttu-id="b3cd9-108">Envio tooMicrosoft suas unidades vazias por meio de um serviço de transporte com suporte.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-108">Shipping your empty drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="b3cd9-109">Atualizar o trabalho de exportação de saudação com informações do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-109">Updating hello export job with hello package information.</span></span>

-   <span data-ttu-id="b3cd9-110">Receber Olá unidades da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-110">Receiving hello drives back from Microsoft.</span></span>

 <span data-ttu-id="b3cd9-111">Consulte [usando Olá importação/exportação do Windows Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como Olá toouse [portal do Azure](https://portal.azure.com/) toocreate gerenciar importar e exportar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-111">See [Using hello Windows Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="selecting-blobs-tooexport"></a><span data-ttu-id="b3cd9-112">Selecionar blobs tooexport</span><span class="sxs-lookup"><span data-stu-id="b3cd9-112">Selecting blobs tooexport</span></span>
 <span data-ttu-id="b3cd9-113">toocreate um trabalho de exportação, você precisará tooprovide uma lista de blobs que você deseja tooexport da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-113">toocreate an export job, you will need tooprovide a list of blobs that you want tooexport from your storage account.</span></span> <span data-ttu-id="b3cd9-114">Há algumas maneiras tooselect blobs toobe exportado:</span><span class="sxs-lookup"><span data-stu-id="b3cd9-114">There are a few ways tooselect blobs toobe exported:</span></span>

-   <span data-ttu-id="b3cd9-115">Você pode usar um tooselect de caminho de blob relativo de um único blob e todos os seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-115">You can use a relative blob path tooselect a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="b3cd9-116">Você pode usar um tooselect de caminho de blob relativo um único blob, excluindo seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-116">You can use a relative blob path tooselect a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="b3cd9-117">Você pode usar um caminho de blob relativo e um tempo de instantâneo tooselect um único instantâneo.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-117">You can use a relative blob path and a snapshot time tooselect a single snapshot.</span></span>

-   <span data-ttu-id="b3cd9-118">Você pode usar um tooselect de prefixo de blob todos os blobs e instantâneos com hello fornecido prefixo.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-118">You can use a blob prefix tooselect all blobs and snapshots with hello given prefix.</span></span>

-   <span data-ttu-id="b3cd9-119">Você pode exportar todos os blobs e instantâneos na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-119">You can export all blobs and snapshots in hello storage account.</span></span>

 <span data-ttu-id="b3cd9-120">Para obter mais informações sobre como especificar blobs tooexport, consulte Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-120">For more information about specifying blobs tooexport, see hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="b3cd9-121">Obtendo o local de envio</span><span class="sxs-lookup"><span data-stu-id="b3cd9-121">Obtaining your shipping location</span></span>
<span data-ttu-id="b3cd9-122">Antes de criar um trabalho de exportação, você precisa tooobtain um nome de local de envio e o endereço por chamada hello [obter local](https://portal.azure.com) ou [listar locais](/rest/api/storageimportexport/listlocations) operação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-122">Before creating an export job, you need tooobtain a shipping location name and address by calling hello [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="b3cd9-123">`List Locations` retorna uma lista de locais e seus endereços de correspondência.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="b3cd9-124">Você pode selecionar um local da saudação retornada lista e seu endereço de toothat de unidades de disco rígido de destino.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-124">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="b3cd9-125">Você também pode usar o hello `Get Location` Olá tooobtain de operação envio diretamente o endereço para um local específico.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-125">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

<span data-ttu-id="b3cd9-126">Siga as próximas etapas, Olá local de envio de saudação do tooobtain:</span><span class="sxs-lookup"><span data-stu-id="b3cd9-126">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="b3cd9-127">Identificar o nome de saudação do local de saudação de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-127">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="b3cd9-128">Esse valor pode ser encontrado em Olá **local** campo da conta de armazenamento Olá **painel** em clássico Olá portal ou consultado por meio de operação da API de gerenciamento de serviços de saudação [obter Propriedades da conta de armazenamento](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="b3cd9-128">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello classic portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="b3cd9-129">Recuperar o local de saudação que estão disponíveis tooprocess esta conta de armazenamento por chamada hello `Get Location` operação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-129">Retrieve hello location that are available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="b3cd9-130">Se hello `AlternateLocations` propriedade de local de saudação contém o local de saudação em si, então é toouse okey neste local.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-130">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="b3cd9-131">Caso contrário, chamar hello `Get Location` operação novamente com um dos locais alternativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-131">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="b3cd9-132">local original Olá pode estar fechada temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-132">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-export-job"></a><span data-ttu-id="b3cd9-133">Criar trabalho de exportação de saudação</span><span class="sxs-lookup"><span data-stu-id="b3cd9-133">Creating hello export job</span></span>
 <span data-ttu-id="b3cd9-134">trabalho de exportação toocreate hello, chamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-134">toocreate hello export job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="b3cd9-135">Você precisará Olá tooprovide informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3cd9-135">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="b3cd9-136">Um nome para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-136">A name for hello job.</span></span>

-   <span data-ttu-id="b3cd9-137">nome de conta de armazenamento Hello.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-137">hello storage account name.</span></span>

-   <span data-ttu-id="b3cd9-138">saudação de envio de nome local, obtido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-138">hello shipping location name, obtained in hello previous step.</span></span>

-   <span data-ttu-id="b3cd9-139">Um tipo de trabalho (Exportação).</span><span class="sxs-lookup"><span data-stu-id="b3cd9-139">A job type (Export).</span></span>

-   <span data-ttu-id="b3cd9-140">endereço de devolução Olá onde Olá unidades devem ser enviadas após a conclusão do trabalho de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-140">hello return address where hello drives should be sent after hello export job has completed.</span></span>

-   <span data-ttu-id="b3cd9-141">Olá toobe de lista de blobs (ou prefixos de blob) exportado.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-141">hello list of blobs (or blob prefixes) toobe exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="b3cd9-142">Enviando suas unidades</span><span class="sxs-lookup"><span data-stu-id="b3cd9-142">Shipping your drives</span></span>
 <span data-ttu-id="b3cd9-143">Em seguida, usar Olá ferramenta de importação/exportação do Azure toodetermine Olá número de unidades que precisar toosend, com base em blobs Olá selecionado toobe exportado e Olá tamanho da unidade.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-143">Next, use hello Azure Import/Export Tool toodetermine hello number of drives you need toosend, based on hello blobs you have selected toobe exported and hello drive size.</span></span> <span data-ttu-id="b3cd9-144">Consulte Olá [referência da ferramenta de importação/exportação do Azure](storage-import-export-tool-how-to-v1.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-144">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="b3cd9-145">Unidades de saudação do pacote em um único pacote e enviá-las toohello endereço obtido na Olá etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-145">Package hello drives in a single package and ship them toohello address obtained in hello earlier step.</span></span> <span data-ttu-id="b3cd9-146">Observe Olá número do seu pacote para a próxima etapa de saudação de controle.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-146">Note hello tracking number of your package for hello next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="b3cd9-147">Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-export-job-with-your-package-information"></a><span data-ttu-id="b3cd9-148">Atualizar o trabalho de exportação de saudação com as informações do pacote</span><span class="sxs-lookup"><span data-stu-id="b3cd9-148">Updating hello export job with your package information</span></span>
 <span data-ttu-id="b3cd9-149">Depois que você tem o número de controle, chame Olá [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) nome da operadora operação tooupdated hello e número de controle para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-149">After you have your tracking number, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation tooupdated hello carrier name and tracking number for hello job.</span></span> <span data-ttu-id="b3cd9-150">Opcionalmente, você pode especificar número de saudação de unidades, o endereço de retorno hello e data de envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-150">You can optionally specify hello number of drives, hello return address, and hello shipping date as well.</span></span>

## <a name="receiving-hello-package"></a><span data-ttu-id="b3cd9-151">Pacote de saudação de recebimento</span><span class="sxs-lookup"><span data-stu-id="b3cd9-151">Receiving hello package</span></span>
 <span data-ttu-id="b3cd9-152">Depois que o trabalho de exportação tiver sido processado, as unidades serão retornadas tooyou com os dados criptografados.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-152">After your export job has been processed, your drives will be returned tooyou with your encrypted data.</span></span> <span data-ttu-id="b3cd9-153">Você pode recuperar a chave do BitLocker Olá para cada uma das unidades de saudação pela chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-153">You can retrieve hello BitLocker key for each of hello drives by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="b3cd9-154">Você pode então desbloquear unidade hello usando Olá chave.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-154">You can then unlock hello drive using hello key.</span></span> <span data-ttu-id="b3cd9-155">arquivo de manifesto Olá unidade em cada unidade contém a lista de saudação dos arquivos na unidade hello, bem como o endereço original de blob Olá para cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="b3cd9-155">hello drive manifest file on each drive contains hello list of files on hello drive, as well as hello original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3cd9-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3cd9-156">Next steps</span></span>

* [<span data-ttu-id="b3cd9-157">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="b3cd9-157">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
