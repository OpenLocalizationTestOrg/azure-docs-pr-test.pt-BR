---
title: "Criar um trabalho de importação para a Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como criar uma importação para o serviço de Importação/Exportação do Microsoft Azure."
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
ms.openlocfilehash: d373d2a0e601f2796719fc5efb8761f276ab24d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-import-job-for-the-azure-importexport-service"></a><span data-ttu-id="9665a-103">Criando um trabalho de importação para o serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="9665a-103">Creating an import job for the Azure Import/Export service</span></span>

<span data-ttu-id="9665a-104">Criar um trabalho de importação para o serviço de importação/exportação do Microsoft Azure usando a API REST envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9665a-104">Creating an import job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="9665a-105">Preparar unidades com a Ferramenta de Importação/Exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9665a-105">Preparing drives with the Azure Import/Export Tool.</span></span>

-   <span data-ttu-id="9665a-106">Obter o local para o qual enviar a unidade.</span><span class="sxs-lookup"><span data-stu-id="9665a-106">Obtaining the location to which to ship the drive.</span></span>

-   <span data-ttu-id="9665a-107">Criar o trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="9665a-107">Creating the import job.</span></span>

-   <span data-ttu-id="9665a-108">Enviar as unidades à Microsoft por meio de um serviço de transporte compatível.</span><span class="sxs-lookup"><span data-stu-id="9665a-108">Shipping the drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="9665a-109">Atualizar o trabalho de importação com os detalhes do envio.</span><span class="sxs-lookup"><span data-stu-id="9665a-109">Updating the import job with the shipping details.</span></span>

 <span data-ttu-id="9665a-110">Veja [Usar o serviço de importação/exportação do Microsoft Azure para transferir dados ao armazenamento de blobs](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação e um tutorial que demonstra como usar o [Portal do Azure](https://portal.azure.com/) para criar e gerenciar tarefas de importação e exportação.</span><span class="sxs-lookup"><span data-stu-id="9665a-110">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure  portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="preparing-drives-with-the-azure-importexport-tool"></a><span data-ttu-id="9665a-111">Preparar unidades com a ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="9665a-111">Preparing drives with the Azure Import/Export Tool</span></span>

<span data-ttu-id="9665a-112">As etapas para preparar unidades para um trabalho de importação são as mesmas se você cria o trabalho pelo portal ou pela API REST.</span><span class="sxs-lookup"><span data-stu-id="9665a-112">The steps to prepare drives for an import job are the same whether you create the jobvia the portal or via the REST API.</span></span>

<span data-ttu-id="9665a-113">Abaixo apresentamos uma breve visão geral da preparação de unidades.</span><span class="sxs-lookup"><span data-stu-id="9665a-113">Below is a brief overview of drive preparation.</span></span> <span data-ttu-id="9665a-114">Veja a [Referência de Import-ExportTool do Azure](storage-import-export-tool-how-to-v1.md) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="9665a-114">Refer to the [Azure Import-ExportTool Reference](storage-import-export-tool-how-to-v1.md) for complete instructions.</span></span> <span data-ttu-id="9665a-115">Você pode baixar a Ferramenta de Importação/Exportação do Azure [aqui](http://go.microsoft.com/fwlink/?LinkID=301900).</span><span class="sxs-lookup"><span data-stu-id="9665a-115">You can download the Azure Import/Export Tool [here](http://go.microsoft.com/fwlink/?LinkID=301900).</span></span>

<span data-ttu-id="9665a-116">Para preparar a unidade:</span><span class="sxs-lookup"><span data-stu-id="9665a-116">Preparing your drive involves:</span></span>

-   <span data-ttu-id="9665a-117">Identifique os dados a importar.</span><span class="sxs-lookup"><span data-stu-id="9665a-117">Identifying the data to be imported.</span></span>

-   <span data-ttu-id="9665a-118">Identifique os blobs de destino no armazenamento do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="9665a-118">Identifying the destination blobs in Windows Azure Storage.</span></span>

-   <span data-ttu-id="9665a-119">Use a Ferramenta de Importação/Exportação do Azure para copiar seus dados para um ou mais discos rígidos.</span><span class="sxs-lookup"><span data-stu-id="9665a-119">Using the Azure Import/Export Tool to copy your data to one or more hard drives.</span></span>

 <span data-ttu-id="9665a-120">A Ferramenta de Importação/Exportação do Azure também gerará um arquivo de manifesto para cada unidade assim que for preparada.</span><span class="sxs-lookup"><span data-stu-id="9665a-120">The Azure Import/Export Tool will also generate a manifest file for each of the drives as it is prepared.</span></span> <span data-ttu-id="9665a-121">Um arquivo de manifesto contém:</span><span class="sxs-lookup"><span data-stu-id="9665a-121">A manifest file contains:</span></span>

-   <span data-ttu-id="9665a-122">Uma enumeração de todos os arquivos a carregar e os mapeamentos desses arquivos para blobs.</span><span class="sxs-lookup"><span data-stu-id="9665a-122">An enumeration of all the files intended for upload and the mappings from these files to blobs.</span></span>

-   <span data-ttu-id="9665a-123">Somas de verificação dos segmentos de cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="9665a-123">Checksums of the segments of each file.</span></span>

-   <span data-ttu-id="9665a-124">Informações sobre metadados e propriedades para associar a cada blob.</span><span class="sxs-lookup"><span data-stu-id="9665a-124">Information about the metadata and properties to associate with each blob.</span></span>

-   <span data-ttu-id="9665a-125">Lista de ação a ser tomada se um blob que está sendo carregado tem o mesmo nome de um blob existente no contêiner.</span><span class="sxs-lookup"><span data-stu-id="9665a-125">A listing of the action to take if a blob that is being uploaded has the same name as an existing blob in the container.</span></span> <span data-ttu-id="9665a-126">As opções possíveis são: a) substituir o blob com o arquivo, b) manter o blob existente e ignorar o carregamento do arquivo, c) acrescentar um sufixo ao nome para que não haja conflito com outros arquivos.</span><span class="sxs-lookup"><span data-stu-id="9665a-126">Possible options are: a) overwrite the blob with the file, b) keep the existing blob and skip uploading the file, c) append a suffix to the name so that it does not conflict with other files.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="9665a-127">Obtendo o local de envio</span><span class="sxs-lookup"><span data-stu-id="9665a-127">Obtaining your shipping location</span></span>

<span data-ttu-id="9665a-128">Antes de criar um trabalho de importação, você precisa obter um nome e o endereço de um local de envio chamando a operação [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="9665a-128">Before creating an import job, you need to obtain a shipping location name and address by calling the [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="9665a-129">`List Locations` retorna uma lista de locais e seus endereços de correspondência.</span><span class="sxs-lookup"><span data-stu-id="9665a-129">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="9665a-130">É possível selecionar uma localização na lista retornada e enviar os discos rígidos para esse endereço.</span><span class="sxs-lookup"><span data-stu-id="9665a-130">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="9665a-131">Você também pode usar a operação `Get Location` para obter o endereço para entrega de uma localização específica diretamente.</span><span class="sxs-lookup"><span data-stu-id="9665a-131">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

 <span data-ttu-id="9665a-132">Siga as etapas abaixo para obter a localização de envio:</span><span class="sxs-lookup"><span data-stu-id="9665a-132">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="9665a-133">Identifique o nome da localização de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9665a-133">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="9665a-134">Esse valor pode ser encontrado no campo **Local** do **Painel** da conta de armazenamento no portal do Azure ou consultado usando a operação [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) da API de gerenciamento de serviços.</span><span class="sxs-lookup"><span data-stu-id="9665a-134">This value can be found under the **Location** field on the storage account's **Dashboard** in the Azure portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="9665a-135">Recupere o local que está disponível para processar esta conta de armazenamento chamando a operação `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="9665a-135">Retrieve the location that is available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="9665a-136">Se a propriedade `AlternateLocations` do local contiver o próprio local, então é seguro usar este local.</span><span class="sxs-lookup"><span data-stu-id="9665a-136">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="9665a-137">Caso contrário, chame a operação `Get Location` novamente com uma das localizações alternativas.</span><span class="sxs-lookup"><span data-stu-id="9665a-137">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="9665a-138">O local original pode estar fechado temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="9665a-138">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-import-job"></a><span data-ttu-id="9665a-139">Criando o trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="9665a-139">Creating the import job</span></span>
<span data-ttu-id="9665a-140">Para criar o trabalho de importação, chame a operação [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="9665a-140">To create the import job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="9665a-141">Primeiro, forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="9665a-141">You will need to provide the following information:</span></span>

-   <span data-ttu-id="9665a-142">Um nome para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="9665a-142">A name for the job.</span></span>

-   <span data-ttu-id="9665a-143">O nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9665a-143">The storage account name.</span></span>

-   <span data-ttu-id="9665a-144">O nome do local de envio, obtido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="9665a-144">The shipping location name, obtained from the previous step.</span></span>

-   <span data-ttu-id="9665a-145">Um tipo de trabalho (importação).</span><span class="sxs-lookup"><span data-stu-id="9665a-145">A job type (Import).</span></span>

-   <span data-ttu-id="9665a-146">O endereço de retorno para o qual as unidades devem ser enviadas depois que o trabalho de importação for concluído.</span><span class="sxs-lookup"><span data-stu-id="9665a-146">The return address where the drives should be sent after the import job has completed.</span></span>

-   <span data-ttu-id="9665a-147">A lista de unidades no trabalho.</span><span class="sxs-lookup"><span data-stu-id="9665a-147">The list of drives in the job.</span></span> <span data-ttu-id="9665a-148">Para cada unidade, você deve incluir as seguintes informações que foram obtidas durante a etapa de preparação de unidade:</span><span class="sxs-lookup"><span data-stu-id="9665a-148">For each drive, you must include the following information that was obtained during the drive preparation step:</span></span>

    -   <span data-ttu-id="9665a-149">A Id da unidade</span><span class="sxs-lookup"><span data-stu-id="9665a-149">The drive Id</span></span>

    -   <span data-ttu-id="9665a-150">A chave do BitLocker</span><span class="sxs-lookup"><span data-stu-id="9665a-150">The BitLocker key</span></span>

    -   <span data-ttu-id="9665a-151">O caminho relativo do arquivo de manifesto no disco rígido</span><span class="sxs-lookup"><span data-stu-id="9665a-151">The manifest file relative path on the hard drive</span></span>

    -   <span data-ttu-id="9665a-152">O hash MD5 do arquivo de manifesto codificado para Base16</span><span class="sxs-lookup"><span data-stu-id="9665a-152">The Base16 encoded manifest file MD5 hash</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="9665a-153">Enviando suas unidades</span><span class="sxs-lookup"><span data-stu-id="9665a-153">Shipping your drives</span></span>
<span data-ttu-id="9665a-154">Você deve enviar suas unidades para o endereço obtido na etapa anterior, e deve fornecer ao serviço de importação/exportação o número de rastreamento do pacote.</span><span class="sxs-lookup"><span data-stu-id="9665a-154">You must ship your drives to the address that you obtained from the previous step, and you must provide the Import/Export service with the tracking number of the package.</span></span>

> [!NOTE]
>  <span data-ttu-id="9665a-155">Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.</span><span class="sxs-lookup"><span data-stu-id="9665a-155">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-import-job-with-your-shipping-information"></a><span data-ttu-id="9665a-156">Atualizando o trabalho de importação com as informações do envio</span><span class="sxs-lookup"><span data-stu-id="9665a-156">Updating the import job with your shipping information</span></span>
<span data-ttu-id="9665a-157">Depois que tiver o número de rastreamento, chame a operação [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) para atualizar o nome da operadora, o número de rastreamento do trabalho e o número da conta da operadora para retorno.</span><span class="sxs-lookup"><span data-stu-id="9665a-157">After you have your tracking number, call the [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) operation to update the shipping carrier name, the tracking number for the job, and the carrier account number for return shipping.</span></span> <span data-ttu-id="9665a-158">Opcionalmente, você também pode especificar a quantidade de unidades e a data de envio.</span><span class="sxs-lookup"><span data-stu-id="9665a-158">You can optionally specify the number of drives and the shipping date as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9665a-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9665a-159">Next steps</span></span>

* [<span data-ttu-id="9665a-160">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="9665a-160">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
