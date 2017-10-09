---
title: "aaaCreate um trabalho de importação para importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocreate uma importação para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a><span data-ttu-id="a611d-103">Criar um trabalho de importação para Olá serviço de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="a611d-103">Creating an import job for hello Azure Import/Export service</span></span>

<span data-ttu-id="a611d-104">Criar um trabalho de importação para o serviço de importação/exportação do Microsoft Azure hello usando Olá API REST envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a611d-104">Creating an import job for hello Microsoft Azure Import/Export service using hello REST API involves hello following steps:</span></span>

-   <span data-ttu-id="a611d-105">Preparando unidades com Olá, ferramenta de importação/exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a611d-105">Preparing drives with hello Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="a611d-106">Obter Olá local toowhich tooship Olá unidade.</span><span class="sxs-lookup"><span data-stu-id="a611d-106">Obtaining hello location toowhich tooship hello drive.</span></span>

-   <span data-ttu-id="a611d-107">Criar trabalho de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-107">Creating hello import job.</span></span>

-   <span data-ttu-id="a611d-108">Saudação de envio unidades tooMicrosoft através de um serviço de transporte com suporte.</span><span class="sxs-lookup"><span data-stu-id="a611d-108">Shipping hello drives tooMicrosoft via a supported carrier service.</span></span>

-   <span data-ttu-id="a611d-109">Atualizar o trabalho de importação de saudação com hello detalhes de envio.</span><span class="sxs-lookup"><span data-stu-id="a611d-109">Updating hello import job with hello shipping details.</span></span>

 <span data-ttu-id="a611d-110">Consulte [usando Olá importação/exportação do Microsoft Azure serviço tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como Olá toouse [portal do Azure](https://portal.azure.com/) toocreate gerenciar importar e exportar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a611d-110">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello [Azure  portal](https://portal.azure.com/) toocreate and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a><span data-ttu-id="a611d-111">Preparando unidades com Olá, ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="a611d-111">Preparing drives with hello Azure Import/Export Tool</span></span>

<span data-ttu-id="a611d-112">Olá etapas tooprepare unidades para um trabalho de importação são Olá mesmo se você criar hello portal de saudação jobvia ou via Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="a611d-112">hello steps tooprepare drives for an import job are hello same whether you create hello jobvia hello portal or via hello REST API.</span></span>

<span data-ttu-id="a611d-113">Abaixo apresentamos uma breve visão geral da preparação de unidades.</span><span class="sxs-lookup"><span data-stu-id="a611d-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="a611d-114">Consulte toohello [Azure importação ExportTool referência](storage-import-export-tool-how-to-v1.md) para obter instruções completas.</span><span class="sxs-lookup"><span data-stu-id="a611d-114">Refer toohello [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="a611d-115">Você pode baixar Olá, ferramenta de importação/exportação do Azure [aqui](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="a611d-115">You can download hello Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="a611d-116">Para preparar a unidade:</span><span class="sxs-lookup"><span data-stu-id="a611d-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="a611d-117">Identificando Olá toobe de dados importado.</span><span class="sxs-lookup"><span data-stu-id="a611d-117">Identifying hello data toobe imported.</span></span>

-   <span data-ttu-id="a611d-118">Identificando os blobs de destino de saudação no armazenamento do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="a611d-118">Identifying hello destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="a611d-119">Usando Olá ferramenta de importação/exportação do Azure toocopy tooone seus dados ou mais discos rígidos.</span><span class="sxs-lookup"><span data-stu-id="a611d-119">Using hello Azure Import/Export Tool toocopy your data tooone or more hard drives.</span></span>

 <span data-ttu-id="a611d-120">Olá, ferramenta de importação/exportação do Azure também irá gerar um arquivo de manifesto para cada uma das unidades de saudação assim que for preparada.</span><span class="sxs-lookup"><span data-stu-id="a611d-120">hello Azure Import/Export Tool will also generate a manifest file for each of hello drives as it is prepared.</span></span> <span data-ttu-id="a611d-121">Um arquivo de manifesto contém:</span><span class="sxs-lookup"><span data-stu-id="a611d-121">A manifest file contains:</span></span>

-   <span data-ttu-id="a611d-122">Uma enumeração de todos os arquivos de saudação destinados para carregamento e mapeamentos de saudação do tooblobs arquivos.</span><span class="sxs-lookup"><span data-stu-id="a611d-122">An enumeration of all hello files intended for upload and hello mappings from these files tooblobs.</span></span>

-   <span data-ttu-id="a611d-123">Somas de verificação dos segmentos de saudação de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="a611d-123">Checksums of hello segments of each file.</span></span>

-   <span data-ttu-id="a611d-124">Informações sobre tooassociate de metadados e propriedades de saudação com cada blob.</span><span class="sxs-lookup"><span data-stu-id="a611d-124">Information about hello metadata and properties tooassociate with each blob.</span></span>

-   <span data-ttu-id="a611d-125">Uma listagem de saudação ação tootake se um blob que está sendo carregado tem Olá mesmo nome como um blob existente no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-125">A listing of hello action tootake if a blob that is being uploaded has hello same name as an existing blob in hello container.</span></span> <span data-ttu-id="a611d-126">Opções possíveis são: a) substituir o blob de saudação pelo arquivo hello, b) manter o blob existente hello e ignorar o carregamento de arquivo hello, c) acrescentar um nome de sufixo toohello para que ele não está em conflito com outros arquivos.</span><span class="sxs-lookup"><span data-stu-id="a611d-126">Possible options are: a) overwrite hello blob with hello file, b) keep hello existing blob and skip uploading hello file, c) append a suffix toohello name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="a611d-127">Obtendo o local de envio</span><span class="sxs-lookup"><span data-stu-id="a611d-127">Obtaining your shipping location</span></span>

<span data-ttu-id="a611d-128">Antes de criar um trabalho de importação, você precisa tooobtain um nome de local de envio e o endereço por chamada hello [listar locais](/rest/api/storageimportexport/listlocations) operação.</span><span class="sxs-lookup"><span data-stu-id="a611d-128">Before creating an import job, you need tooobtain a shipping location name and address by calling hello [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="a611d-129">`List Locations` retorna uma lista de locais e seus endereços de correspondência.</span><span class="sxs-lookup"><span data-stu-id="a611d-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="a611d-130">Você pode selecionar um local da saudação retornada lista e seu endereço de toothat de unidades de disco rígido de destino.</span><span class="sxs-lookup"><span data-stu-id="a611d-130">You can select a location from hello returned list and ship your hard drives toothat address.</span></span> <span data-ttu-id="a611d-131">Você também pode usar o hello `Get Location` Olá tooobtain de operação envio diretamente o endereço para um local específico.</span><span class="sxs-lookup"><span data-stu-id="a611d-131">You can also use hello `Get Location` operation tooobtain hello shipping address for a specific location directly.</span></span>

 <span data-ttu-id="a611d-132">Siga as próximas etapas, Olá local de envio de saudação do tooobtain:</span><span class="sxs-lookup"><span data-stu-id="a611d-132">Follow hello steps below tooobtain hello shipping location:</span></span>

-   <span data-ttu-id="a611d-133">Identificar o nome de saudação do local de saudação de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a611d-133">Identify hello name of hello location of your storage account.</span></span> <span data-ttu-id="a611d-134">Esse valor pode ser encontrado em Olá **local** campo da conta de armazenamento Olá **painel** no portal do Azure ou consultado por meio de operação da API de gerenciamento de serviços de saudação do hello [obter armazenamento Propriedades de conta](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span><span class="sxs-lookup"><span data-stu-id="a611d-134">This value can be found under hello **Location** field on hello storage account's **Dashboard** in hello Azure portal or queried for by using hello service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="a611d-135">Recuperar o local Olá tooprocess disponível esta conta de armazenamento por chamada hello `Get Location` operação.</span><span class="sxs-lookup"><span data-stu-id="a611d-135">Retrieve hello location that is available tooprocess this storage account by calling hello `Get Location` operation.</span></span>

-   <span data-ttu-id="a611d-136">Se hello `AlternateLocations` propriedade de local de saudação contém o local de saudação em si, então é toouse okey neste local.</span><span class="sxs-lookup"><span data-stu-id="a611d-136">If hello `AlternateLocations` property of hello location contains hello location itself, then it is okay toouse this location.</span></span> <span data-ttu-id="a611d-137">Caso contrário, chamar hello `Get Location` operação novamente com um dos locais alternativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-137">Otherwise, call hello `Get Location` operation again with one of hello alternate locations.</span></span> <span data-ttu-id="a611d-138">local original Olá pode estar fechada temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="a611d-138">hello original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-hello-import-job"></a><span data-ttu-id="a611d-139">Criar trabalho de importação de saudação</span><span class="sxs-lookup"><span data-stu-id="a611d-139">Creating hello import job</span></span>
<span data-ttu-id="a611d-140">trabalho de importação toocreate hello, chamada hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="a611d-140">toocreate hello import job, call hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="a611d-141">Você precisará Olá tooprovide informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a611d-141">You will need tooprovide hello following information:</span></span>

-   <span data-ttu-id="a611d-142">Um nome para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-142">A name for hello job.</span></span>

-   <span data-ttu-id="a611d-143">nome de conta de armazenamento Hello.</span><span class="sxs-lookup"><span data-stu-id="a611d-143">hello storage account name.</span></span>

-   <span data-ttu-id="a611d-144">saudação de envio de nome local, obtida na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="a611d-144">hello shipping location name, obtained from hello previous step.</span></span>

-   <span data-ttu-id="a611d-145">Um tipo de trabalho (importação).</span><span class="sxs-lookup"><span data-stu-id="a611d-145">A job type (Import).</span></span>

-   <span data-ttu-id="a611d-146">endereço de devolução Olá onde Olá unidades devem ser enviadas após a conclusão do trabalho de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-146">hello return address where hello drives should be sent after hello import job has completed.</span></span>

-   <span data-ttu-id="a611d-147">lista de saudação de unidades de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-147">hello list of drives in hello job.</span></span> <span data-ttu-id="a611d-148">Para cada unidade, você deve incluir Olá informações que foram obtidas na etapa de preparação de unidade Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a611d-148">For each drive, you must include hello following information that was obtained during hello drive preparation step:</span></span>

    -   <span data-ttu-id="a611d-149">Id da unidade Olá</span><span class="sxs-lookup"><span data-stu-id="a611d-149">hello drive Id</span></span>

    -   <span data-ttu-id="a611d-150">chave do BitLocker Olá</span><span class="sxs-lookup"><span data-stu-id="a611d-150">hello BitLocker key</span></span>

    -   <span data-ttu-id="a611d-151">caminho relativo do arquivo de manifesto Olá no disco rígido Olá</span><span class="sxs-lookup"><span data-stu-id="a611d-151">hello manifest file relative path on hello hard drive</span></span>

    -   <span data-ttu-id="a611d-152">Olá Base16 codificado hash de MD5 do arquivo de manifesto</span><span class="sxs-lookup"><span data-stu-id="a611d-152">hello Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="a611d-153">Enviando suas unidades</span><span class="sxs-lookup"><span data-stu-id="a611d-153">Shipping your drives</span></span>
<span data-ttu-id="a611d-154">Você deve enviar seu endereço de toohello de unidades que você obteve na etapa anterior Olá, e você deve fornecer Olá serviço de importação/exportação com hello controle o número de pacotes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a611d-154">You must ship your drives toohello address that you obtained from hello previous step, and you must provide hello Import/Export service with hello tracking number of hello package.</span></span>

> [!NOTE]
>  <span data-ttu-id="a611d-155">Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.</span><span class="sxs-lookup"><span data-stu-id="a611d-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-hello-import-job-with-your-shipping-information"></a><span data-ttu-id="a611d-156">Atualizar o trabalho de importação de saudação com as informações de envio</span><span class="sxs-lookup"><span data-stu-id="a611d-156">Updating hello import job with your shipping information</span></span>
<span data-ttu-id="a611d-157">Depois que você tem o número de controle, chame Olá [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) Olá tooupdate de operação de envio nome da operadora, número de controle de saudação para trabalho hello e número de conta da operadora Olá para envio de retorno.</span><span class="sxs-lookup"><span data-stu-id="a611d-157">After you have your tracking number, call hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation tooupdate hello shipping carrier name, hello tracking number for hello job, and hello carrier account number for return shipping.</span></span> <span data-ttu-id="a611d-158">Opcionalmente, você pode especificar número Olá de unidades e Olá também a data de envio.</span><span class="sxs-lookup"><span data-stu-id="a611d-158">You can optionally specify hello number of drives and hello shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a611d-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a611d-159">Next steps</span></span>

* [<span data-ttu-id="a611d-160">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="a611d-160">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
