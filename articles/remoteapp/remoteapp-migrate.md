---
title: "Migrar dados de usuário do Azure RemoteApp | Microsoft Docs"
description: "Saiba como migrar seus dados de usuário para dentro e fora do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ba3cf4c6834279bbd7f94d666fd8abbb7ac05bf0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-migrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="1f213-103">Como migrar dados para dentro e fora do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="1f213-103">How to migrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f213-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="1f213-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1f213-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="1f213-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1f213-106">Você pode usar várias ferramentas e métodos diferentes para transferir [dados de usuário](remoteapp-upd.md) para dentro e fora do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1f213-106">You can use many different tools and methods to transfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="1f213-107">Veja alguns métodos:</span><span class="sxs-lookup"><span data-stu-id="1f213-107">Here are a few methods:</span></span>

* <span data-ttu-id="1f213-108">Copiar e colar usando o compartilhamento da área de transferência</span><span class="sxs-lookup"><span data-stu-id="1f213-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="1f213-109">Copiar arquivos e dados para um servidor de arquivos</span><span class="sxs-lookup"><span data-stu-id="1f213-109">Copy files and data to a file server</span></span>
* <span data-ttu-id="1f213-110">Copiar arquivos para o OneDrive for Business por meio de um navegador</span><span class="sxs-lookup"><span data-stu-id="1f213-110">Copy files to OneDrive for Business through a browser</span></span>
* <span data-ttu-id="1f213-111">Copiar os arquivos usando o redirecionamento</span><span class="sxs-lookup"><span data-stu-id="1f213-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="1f213-112">Não é possível habilitar os agentes de sincronização do OneDrive for Business ou para Consumidor - eles [não têm suporte](remoteapp-onedrive.md) no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1f213-112">You cannot enable the OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="1f213-113">Usar copiar e colar no Explorador de Arquivos</span><span class="sxs-lookup"><span data-stu-id="1f213-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="1f213-114">Copiar e colar usando a área de transferência está habilitado nas implantações do RemoteApp [por padrão](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="1f213-114">Copy and paste using the clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="1f213-115">Isso permite que os usuários copiem arquivos entre seus PCs locais e aplicativos do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1f213-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="1f213-116">Muitas vezes, durante o curso normal de utilização de aplicativos no RemoteApp, os usuários salvam arquivos em seus UPDs – e é fácil mover dados para fora do RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="1f213-116">Often, through the normal course of using apps in RemoteApp, users have saved files to their UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="1f213-117">[Publicar o Explorador de Arquivos como um aplicativo](remoteapp-publish.md) em uma coleção de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1f213-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="1f213-118">(Observe que se trata de uma tarefa administrativa).</span><span class="sxs-lookup"><span data-stu-id="1f213-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="1f213-119">Direcione os usuários para iniciar o aplicativo do Explorador de Arquivos que você publicou e usá-lo para copiar e colar arquivos em seu UPD e para fora dele.</span><span class="sxs-lookup"><span data-stu-id="1f213-119">Direct your users to launch the File Explorer app you published and to use that to copy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-to-a-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="1f213-120">Carregar arquivos e dados em um servidor de arquivos usando a cópia de arquivos de rede padrão</span><span class="sxs-lookup"><span data-stu-id="1f213-120">Upload files and data to a file server by using standard network file copy</span></span>
<span data-ttu-id="1f213-121">Normalmente, as organizações usam servidores de arquivos para armazenar dados gerais.</span><span class="sxs-lookup"><span data-stu-id="1f213-121">Often organizations use file servers to store general data.</span></span> <span data-ttu-id="1f213-122">Se você souber o nome ou o local do servidor, os usuários poderão procurá-lo na rede local e copiar seus arquivos, assim como fizeram acima.</span><span class="sxs-lookup"><span data-stu-id="1f213-122">If you know the server name or location, your users can browse the local network for the server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="1f213-123">Novamente, convém publicar o Explorador de Arquivos no RemoteApp e compartilhá-lo com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="1f213-123">Again you'll want to publish File Explorer to RemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="1f213-124">O servidor de arquivos deve estar na rede roteável na qual o RemoteApp foi implantado.</span><span class="sxs-lookup"><span data-stu-id="1f213-124">The file server must be on the routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-to-onedrive-for-business"></a><span data-ttu-id="1f213-125">Copiar um arquivo no OneDrive for Business</span><span class="sxs-lookup"><span data-stu-id="1f213-125">Copy files to OneDrive for Business</span></span>
<span data-ttu-id="1f213-126">Embora não seja possível habilitar o agente de sincronização do OneDrive for Business no RemoteApp, você ainda pode copiar arquivos de seu UPD para o OneDrive for Business por meio de um navegador.</span><span class="sxs-lookup"><span data-stu-id="1f213-126">Although you cannot enable the OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD to OneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="1f213-127">Publique o Explorador de Arquivos no RemoteApp e, depois, peça aos usuários para acessarem os arquivos por meio desse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f213-127">Publish File Explorer to RemoteApp and then tell users to access the files through that app.</span></span> 
2. <span data-ttu-id="1f213-128">É mais fácil transferir arquivos se eles estiverem compactados. Portanto, os usuários devem criar um arquivo .zip contendo todos os arquivos a fim de movê-lo para o OneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="1f213-128">It's easiest to transfer files if they are compressed, so users should create a .zip file that contains all of the files to move to OneDrive for Business.</span></span>
3. <span data-ttu-id="1f213-129">Peça aos usuários para acessarem o Portal do Office 365 e, em seguida, acesse o OneDrive e carregue o arquivo .zip.</span><span class="sxs-lookup"><span data-stu-id="1f213-129">Ask users to go to the Office 365 portal, and then go to OneDrive and upload the .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="1f213-130">Copiar arquivos usando o redirecionamento de unidade</span><span class="sxs-lookup"><span data-stu-id="1f213-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="1f213-131">Se tiver habilitado o [redirecionamento de unidade](remoteapp-redirection.md), você já terá criado uma unidade mapeada para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="1f213-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="1f213-132">Nesse caso, eles poderão compactar seus arquivos na unidade redirecionada e salvá-los em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="1f213-132">In this case, they can zip their files on the redirected drive and then save them to their local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="1f213-133">Como os administradores podem exportar dados</span><span class="sxs-lookup"><span data-stu-id="1f213-133">How administrators can export data</span></span>

<span data-ttu-id="1f213-134">Os administradores do Azure RemoteApp podem exportar todos os UPDs (discos de perfil do usuário) de todas as coleções de uma assinatura para o Armazenamento do Azure usando o cmdlet Export-AzureRemoteAppUserDisk do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f213-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription to Azure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="1f213-135">Não é possível selecionar UPDs individuais.</span><span class="sxs-lookup"><span data-stu-id="1f213-135">There is no ability to select individual UPD's.</span></span>  <span data-ttu-id="1f213-136">Quando o comando do PowerShell for executado, cada disco de usuário terá 50 GB de disco fixo e será exportado para o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f213-136">When the PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported to Azure storage.</span></span>  <span data-ttu-id="1f213-137">Os custos de armazenamento do Azure incorrerão imediatamente para esse armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1f213-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="1f213-138">Ao executar esse comando, verifique se não existem sessões; caso contrário, a exportação falhará.</span><span class="sxs-lookup"><span data-stu-id="1f213-138">When running this command ensure there are no sessions otherwise the export will fail.</span></span>

<span data-ttu-id="1f213-139">UPDs para implantações do Azure RemoteApp ingressadas no domínio só podem ser usados novamente em uma implantação do RDS; implantações ingressadas fora do domínio não podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="1f213-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="1f213-140">Se esses discos forem ser usados em uma implantação do RDS, recomendamos o uso de nossos [scripts automatizados](https://github.com/arcadiahlyy/aramigration), que exportarão, converterão e importarão os UDPs para uma implantação do RDS.</span><span class="sxs-lookup"><span data-stu-id="1f213-140">If these disks will be used in an RDS deployment we recommend to use our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import the UPD's into an RDS deployment.</span></span>

