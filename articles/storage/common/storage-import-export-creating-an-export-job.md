---
title: "Criar um Trabalho de exportação para a Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como criar um trabalho de exportação para o serviço de Importação/Exportação do Microsoft Azure."
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
ms.openlocfilehash: bdeac373aa8270bd9de8f135ec7166d744fd83ae
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-export-job-for-the-azure-importexport-service"></a><span data-ttu-id="75d5f-103">Criando um trabalho de exportação para o serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="75d5f-103">Creating an export job for the Azure Import/Export service</span></span>
<span data-ttu-id="75d5f-104">A criação de um trabalho de exportação do serviço de Importação/Exportação do Microsoft Azure usando a API REST envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75d5f-104">Creating an export job for the Microsoft Azure Import/Export service using the REST API involves the following steps:</span></span>

-   <span data-ttu-id="75d5f-105">Selecionar os blobs a serem exportados.</span><span class="sxs-lookup"><span data-stu-id="75d5f-105">Selecting the blobs to export.</span></span>

-   <span data-ttu-id="75d5f-106">Obter uma localização de envio.</span><span class="sxs-lookup"><span data-stu-id="75d5f-106">Obtaining a shipping location.</span></span>

-   <span data-ttu-id="75d5f-107">Criar o trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="75d5f-107">Creating the export job.</span></span>

-   <span data-ttu-id="75d5f-108">Enviar as unidades vazias para a Microsoft por meio de um serviço de carrier com suporte.</span><span class="sxs-lookup"><span data-stu-id="75d5f-108">Shipping your empty drives to Microsoft via a supported carrier service.</span></span>

-   <span data-ttu-id="75d5f-109">Atualizar o trabalho de exportação com as informações do pacote.</span><span class="sxs-lookup"><span data-stu-id="75d5f-109">Updating the export job with the package information.</span></span>

-   <span data-ttu-id="75d5f-110">Receber as unidades de volta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="75d5f-110">Receiving the drives back from Microsoft.</span></span>

 <span data-ttu-id="75d5f-111">Consulte [Usar o serviço de Importação/Exportação do Microsoft Azure para transferir dados para o Armazenamento de Blobs](storage-import-export-service.md) para obter uma visão geral do serviço de Importação/Exportação e um tutorial que demonstra como usar o [portal do Azure](https://portal.azure.com/) para criar e gerenciar trabalhos de importação e exportação.</span><span class="sxs-lookup"><span data-stu-id="75d5f-111">See [Using the Windows Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the [Azure portal](https://portal.azure.com/) to create and manage import and export jobs.</span></span>

## <a name="selecting-blobs-to-export"></a><span data-ttu-id="75d5f-112">Selecionando os blobs a serem exportados</span><span class="sxs-lookup"><span data-stu-id="75d5f-112">Selecting blobs to export</span></span>
 <span data-ttu-id="75d5f-113">Para criar um trabalho de exportação, você precisará fornecer uma lista de blobs que deseja exportar de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="75d5f-113">To create an export job, you will need to provide a list of blobs that you want to export from your storage account.</span></span> <span data-ttu-id="75d5f-114">Há algumas maneiras para selecionar os blobs a serem exportados:</span><span class="sxs-lookup"><span data-stu-id="75d5f-114">There are a few ways to select blobs to be exported:</span></span>

-   <span data-ttu-id="75d5f-115">É possível usar um caminho de blob relativo para selecionar um único blob e todos os seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="75d5f-115">You can use a relative blob path to select a single blob and all of its snapshots.</span></span>

-   <span data-ttu-id="75d5f-116">É possível usar um caminho de blob relativo para selecionar um único blob, excluindo seus instantâneos.</span><span class="sxs-lookup"><span data-stu-id="75d5f-116">You can use a relative blob path to select a single blob excluding its snapshots.</span></span>

-   <span data-ttu-id="75d5f-117">É possível usar um caminho de blob relativo e um tempo de instantâneo para selecionar um único instantâneo.</span><span class="sxs-lookup"><span data-stu-id="75d5f-117">You can use a relative blob path and a snapshot time to select a single snapshot.</span></span>

-   <span data-ttu-id="75d5f-118">É possível usar um prefixo de blob para selecionar todos os blobs e instantâneos com o prefixo especificado.</span><span class="sxs-lookup"><span data-stu-id="75d5f-118">You can use a blob prefix to select all blobs and snapshots with the given prefix.</span></span>

-   <span data-ttu-id="75d5f-119">É possível exportar todos os blobs e instantâneos na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="75d5f-119">You can export all blobs and snapshots in the storage account.</span></span>

 <span data-ttu-id="75d5f-120">Para obter mais informações sobre como especificar os blobs a serem exportados, consulte a operação [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="75d5f-120">For more information about specifying blobs to export, see the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span>

## <a name="obtaining-your-shipping-location"></a><span data-ttu-id="75d5f-121">Obtendo o local de envio</span><span class="sxs-lookup"><span data-stu-id="75d5f-121">Obtaining your shipping location</span></span>
<span data-ttu-id="75d5f-122">Antes de criar um trabalho de exportação, você precisa obter um nome e o endereço de uma localização de envio chamando a operação [Get Location](https://portal.azure.com) ou [List Locations](/rest/api/storageimportexport/listlocations).</span><span class="sxs-lookup"><span data-stu-id="75d5f-122">Before creating an export job, you need to obtain a shipping location name and address by calling the [Get Location](https://portal.azure.com) or [List Locations](/rest/api/storageimportexport/listlocations) operation.</span></span> <span data-ttu-id="75d5f-123">`List Locations` retornará uma lista de localizações e seus endereços para correspondência.</span><span class="sxs-lookup"><span data-stu-id="75d5f-123">`List Locations` will return a list of locations and their mailing addresses.</span></span> <span data-ttu-id="75d5f-124">É possível selecionar uma localização na lista retornada e enviar os discos rígidos para esse endereço.</span><span class="sxs-lookup"><span data-stu-id="75d5f-124">You can select a location from the returned list and ship your hard drives to that address.</span></span> <span data-ttu-id="75d5f-125">Você também pode usar a operação `Get Location` para obter o endereço para entrega de uma localização específica diretamente.</span><span class="sxs-lookup"><span data-stu-id="75d5f-125">You can also use the `Get Location` operation to obtain the shipping address for a specific location directly.</span></span>

<span data-ttu-id="75d5f-126">Siga as etapas abaixo para obter a localização de envio:</span><span class="sxs-lookup"><span data-stu-id="75d5f-126">Follow the steps below to obtain the shipping location:</span></span>

-   <span data-ttu-id="75d5f-127">Identifique o nome da localização de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="75d5f-127">Identify the name of the location of your storage account.</span></span> <span data-ttu-id="75d5f-128">Esse valor pode ser encontrado no campo **Local** do **Painel** da conta de armazenamento no portal clássico ou consultado usando a operação [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties) da API de gerenciamento de serviços.</span><span class="sxs-lookup"><span data-stu-id="75d5f-128">This value can be found under the **Location** field on the storage account's **Dashboard** in the classic portal or queried for by using the service management API operation [Get Storage Account Properties](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).</span></span>

-   <span data-ttu-id="75d5f-129">Recupere a localização que está disponível para processar essa conta de armazenamento chamando a operação `Get Location`.</span><span class="sxs-lookup"><span data-stu-id="75d5f-129">Retrieve the location that are available to process this storage account by calling the `Get Location` operation.</span></span>

-   <span data-ttu-id="75d5f-130">Se a propriedade `AlternateLocations` da localização contiver a própria localização, será seguro usá-la.</span><span class="sxs-lookup"><span data-stu-id="75d5f-130">If the `AlternateLocations` property of the location contains the location itself, then it is okay to use this location.</span></span> <span data-ttu-id="75d5f-131">Caso contrário, chame a operação `Get Location` novamente com uma das localizações alternativas.</span><span class="sxs-lookup"><span data-stu-id="75d5f-131">Otherwise, call the `Get Location` operation again with one of the alternate locations.</span></span> <span data-ttu-id="75d5f-132">O local original pode estar fechado temporariamente para manutenção.</span><span class="sxs-lookup"><span data-stu-id="75d5f-132">The original location might be temporarily closed for maintenance.</span></span>

## <a name="creating-the-export-job"></a><span data-ttu-id="75d5f-133">Criando o trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="75d5f-133">Creating the export job</span></span>
 <span data-ttu-id="75d5f-134">Para criar o trabalho de exportação, chame a operação [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="75d5f-134">To create the export job, call the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="75d5f-135">Você precisará fornecer as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="75d5f-135">You will need to provide the following information:</span></span>

-   <span data-ttu-id="75d5f-136">Um nome para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="75d5f-136">A name for the job.</span></span>

-   <span data-ttu-id="75d5f-137">O nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="75d5f-137">The storage account name.</span></span>

-   <span data-ttu-id="75d5f-138">O nome da localização de envio, obtido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="75d5f-138">The shipping location name, obtained in the previous step.</span></span>

-   <span data-ttu-id="75d5f-139">Um tipo de trabalho (Exportação).</span><span class="sxs-lookup"><span data-stu-id="75d5f-139">A job type (Export).</span></span>

-   <span data-ttu-id="75d5f-140">O endereço do remetente para o qual as unidades deverão ser enviadas após a conclusão do trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="75d5f-140">The return address where the drives should be sent after the export job has completed.</span></span>

-   <span data-ttu-id="75d5f-141">A lista de blobs (ou os prefixos de blob) a ser exportada.</span><span class="sxs-lookup"><span data-stu-id="75d5f-141">The list of blobs (or blob prefixes) to be exported.</span></span>

## <a name="shipping-your-drives"></a><span data-ttu-id="75d5f-142">Enviando suas unidades</span><span class="sxs-lookup"><span data-stu-id="75d5f-142">Shipping your drives</span></span>
 <span data-ttu-id="75d5f-143">Em seguida, use a Ferramenta de Importação/Exportação do Azure para determinar o número de unidades que precisam ser enviadas, com base nos blobs selecionados para serem exportados e no tamanho da unidade.</span><span class="sxs-lookup"><span data-stu-id="75d5f-143">Next, use the Azure Import/Export Tool to determine the number of drives you need to send, based on the blobs you have selected to be exported and the drive size.</span></span> <span data-ttu-id="75d5f-144">Consulte [Referência da Ferramenta de Importação/Exportação do Azure](storage-import-export-tool-how-to-v1.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="75d5f-144">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) for details.</span></span>

 <span data-ttu-id="75d5f-145">Empacote as unidades em um único pacote e envie-as para o endereço obtido na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="75d5f-145">Package the drives in a single package and ship them to the address obtained in the earlier step.</span></span> <span data-ttu-id="75d5f-146">Anote o número de acompanhamento do pacote para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="75d5f-146">Note the tracking number of your package for the next step.</span></span>

> [!NOTE]
>  <span data-ttu-id="75d5f-147">Você deve enviar suas unidades por meio de um serviço de transporte compatível, que fornecerá um número de rastreamento para seu pacote.</span><span class="sxs-lookup"><span data-stu-id="75d5f-147">You must ship your drives via a supported carrier service, which will provide a tracking number for your package.</span></span>

## <a name="updating-the-export-job-with-your-package-information"></a><span data-ttu-id="75d5f-148">Atualizando o trabalho de exportação com as informações do pacote</span><span class="sxs-lookup"><span data-stu-id="75d5f-148">Updating the export job with your package information</span></span>
 <span data-ttu-id="75d5f-149">Depois que tiver o número de acompanhamento, chame a operação [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) para atualizar o nome da carrier e o número de acompanhamento do trabalho.</span><span class="sxs-lookup"><span data-stu-id="75d5f-149">After you have your tracking number, call the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation to updated the carrier name and tracking number for the job.</span></span> <span data-ttu-id="75d5f-150">Opcionalmente, você pode especificar o número de unidades, o endereço do remetente, bem como a data de remessa.</span><span class="sxs-lookup"><span data-stu-id="75d5f-150">You can optionally specify the number of drives, the return address, and the shipping date as well.</span></span>

## <a name="receiving-the-package"></a><span data-ttu-id="75d5f-151">Recebendo o pacote</span><span class="sxs-lookup"><span data-stu-id="75d5f-151">Receiving the package</span></span>
 <span data-ttu-id="75d5f-152">Após o processamento do trabalho de exportação, as unidades serão retornadas para você com os dados criptografados.</span><span class="sxs-lookup"><span data-stu-id="75d5f-152">After your export job has been processed, your drives will be returned to you with your encrypted data.</span></span> <span data-ttu-id="75d5f-153">É possível recuperar a chave do BitLocker para cada uma das unidades chamando a operação [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="75d5f-153">You can retrieve the BitLocker key for each of the drives by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="75d5f-154">Em seguida, você poderá desbloquear a unidade usando a chave.</span><span class="sxs-lookup"><span data-stu-id="75d5f-154">You can then unlock the drive using the key.</span></span> <span data-ttu-id="75d5f-155">O arquivo de manifesto da unidade em cada unidade contém a lista de arquivos na unidade, bem como o endereço original do blob para cada arquivo.</span><span class="sxs-lookup"><span data-stu-id="75d5f-155">The drive manifest file on each drive contains the list of files on the drive, as well as the original blob address for each file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75d5f-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75d5f-156">Next steps</span></span>

* [<span data-ttu-id="75d5f-157">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="75d5f-157">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
