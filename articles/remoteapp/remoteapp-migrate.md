---
title: "dados de usuário aaaMigrate do Azure RemoteApp | Microsoft Docs"
description: "Saiba como toomigrate seus dados de usuário dentro e fora do Azure RemoteApp."
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
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a><span data-ttu-id="62634-103">Como toomigrate dados dentro e fora do Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="62634-103">How toomigrate data into and out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="62634-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="62634-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="62634-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="62634-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="62634-106">Você pode usar várias ferramentas diferentes e métodos tootransfer [dados de usuário](remoteapp-upd.md) dentro e fora do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="62634-106">You can use many different tools and methods tootransfer [user data](remoteapp-upd.md) into and out of Azure RemoteApp.</span></span> <span data-ttu-id="62634-107">Veja alguns métodos:</span><span class="sxs-lookup"><span data-stu-id="62634-107">Here are a few methods:</span></span>

* <span data-ttu-id="62634-108">Copiar e colar usando o compartilhamento da área de transferência</span><span class="sxs-lookup"><span data-stu-id="62634-108">Copy and paste using clipboard sharing</span></span>
* <span data-ttu-id="62634-109">Copiar arquivos e dados do servidor de arquivos tooa</span><span class="sxs-lookup"><span data-stu-id="62634-109">Copy files and data tooa file server</span></span>
* <span data-ttu-id="62634-110">Copiar arquivos tooOneDrive para os negócios por meio de um navegador</span><span class="sxs-lookup"><span data-stu-id="62634-110">Copy files tooOneDrive for Business through a browser</span></span>
* <span data-ttu-id="62634-111">Copiar os arquivos usando o redirecionamento</span><span class="sxs-lookup"><span data-stu-id="62634-111">Copy files using redirection</span></span>

> [!NOTE]
> <span data-ttu-id="62634-112">Não é possível habilitar Olá OneDrive para agentes de sincronização de consumidor ou de negócios - eles [não há suporte para](remoteapp-onedrive.md) no Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="62634-112">You cannot enable hello OneDrive for Business or Consumer sync agents - they [are not supported](remoteapp-onedrive.md) in Azure RemoteApp.</span></span>
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a><span data-ttu-id="62634-113">Usar copiar e colar no Explorador de Arquivos</span><span class="sxs-lookup"><span data-stu-id="62634-113">Use copy and paste in File Explorer</span></span>
<span data-ttu-id="62634-114">Copiar e colar usando a área de transferência hello está habilitado em implantações de RemoteApp [por padrão](remoteapp-redirection.md).</span><span class="sxs-lookup"><span data-stu-id="62634-114">Copy and paste using hello clipboard is enabled in RemoteApp deployments [by default](remoteapp-redirection.md).</span></span> <span data-ttu-id="62634-115">Isso permite que os usuários copiem arquivos entre seus PCs locais e aplicativos do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="62634-115">This lets users copy files between their local PC and RemoteApp apps.</span></span> <span data-ttu-id="62634-116">Em geral, por meio de curso normal de saudação do uso de aplicativos no RemoteApp, os usuários salvou os arquivos tootheir UPDs - movendo que os dados do RemoteApp são fácil:</span><span class="sxs-lookup"><span data-stu-id="62634-116">Often, through hello normal course of using apps in RemoteApp, users have saved files tootheir UPDs - moving that data out of RemoteApp is easy:</span></span>

1. <span data-ttu-id="62634-117">[Publicar o Explorador de Arquivos como um aplicativo](remoteapp-publish.md) em uma coleção de RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="62634-117">[Publish File Explorer as an app](remoteapp-publish.md) in a RemoteApp collection.</span></span> <span data-ttu-id="62634-118">(Observe que se trata de uma tarefa administrativa).</span><span class="sxs-lookup"><span data-stu-id="62634-118">(Note that this is an administrative task.)</span></span>
2. <span data-ttu-id="62634-119">Direcione seus usuários toolaunch Olá Explorador de arquivos aplicativo publicado e toouse que toocopy e colar arquivos em sua UPD e fora dele.</span><span class="sxs-lookup"><span data-stu-id="62634-119">Direct your users toolaunch hello File Explorer app you published and toouse that toocopy and paste files both into their UPD and out of it.</span></span>

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a><span data-ttu-id="62634-120">Upload de arquivos e o servidor de arquivos tooa dados usando a cópia de arquivos de rede padrão</span><span class="sxs-lookup"><span data-stu-id="62634-120">Upload files and data tooa file server by using standard network file copy</span></span>
<span data-ttu-id="62634-121">As organizações usam dados gerais de toostore de servidores de arquivos.</span><span class="sxs-lookup"><span data-stu-id="62634-121">Often organizations use file servers toostore general data.</span></span> <span data-ttu-id="62634-122">Se você souber o nome do servidor de saudação ou local, os usuários podem procurar na rede local para o servidor de saudação hello e copie seus arquivos, bem como acima.</span><span class="sxs-lookup"><span data-stu-id="62634-122">If you know hello server name or location, your users can browse hello local network for hello server and then copy their files there, much like they did above.</span></span> <span data-ttu-id="62634-123">Novamente você deseja toopublish tooRemoteApp de Explorador de arquivos e compartilhá-lo com seus usuários.</span><span class="sxs-lookup"><span data-stu-id="62634-123">Again you'll want toopublish File Explorer tooRemoteApp and then share it with your users.</span></span>

> [!NOTE]
> <span data-ttu-id="62634-124">servidor de arquivo Hello deve estar na rede roteável de saudação RemoteApp implantado em.</span><span class="sxs-lookup"><span data-stu-id="62634-124">hello file server must be on hello routable network that RemoteApp was deployed into.</span></span>
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a><span data-ttu-id="62634-125">Copiar arquivos tooOneDrive para empresas</span><span class="sxs-lookup"><span data-stu-id="62634-125">Copy files tooOneDrive for Business</span></span>
<span data-ttu-id="62634-126">Embora você não pode habilitar hello OneDrive para o agente de sincronização de negócios no RemoteApp, você ainda pode copiar arquivos de seu tooOneDrive UDP para os negócios por meio de um navegador.</span><span class="sxs-lookup"><span data-stu-id="62634-126">Although you cannot enable hello OneDrive for Business sync agent in RemoteApp, you can still copy files from your UPD tooOneDrive for Business through a browser.</span></span> 

1. <span data-ttu-id="62634-127">Publicar tooRemoteApp Explorador de arquivos e, em seguida, informe a usuários tooaccess Olá arquivos por meio desse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="62634-127">Publish File Explorer tooRemoteApp and then tell users tooaccess hello files through that app.</span></span> 
2. <span data-ttu-id="62634-128">É mais fácil arquivos de tootransfer se eles são compactados, para que os usuários devem criar um arquivo. zip que contém todos os tooOneDrive de toomove arquivos hello para empresas.</span><span class="sxs-lookup"><span data-stu-id="62634-128">It's easiest tootransfer files if they are compressed, so users should create a .zip file that contains all of hello files toomove tooOneDrive for Business.</span></span>
3. <span data-ttu-id="62634-129">Peça ao portal de toohello Office 365 toogo dos usuários e, em seguida, vá tooOneDrive e carregar o arquivo. zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="62634-129">Ask users toogo toohello Office 365 portal, and then go tooOneDrive and upload hello .zip file.</span></span>

## <a name="copy-files-by-using-drive-redirection"></a><span data-ttu-id="62634-130">Copiar arquivos usando o redirecionamento de unidade</span><span class="sxs-lookup"><span data-stu-id="62634-130">Copy files by using drive redirection</span></span>
<span data-ttu-id="62634-131">Se tiver habilitado o [redirecionamento de unidade](remoteapp-redirection.md), você já terá criado uma unidade mapeada para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="62634-131">If you have enabled [drive redirection](remoteapp-redirection.md), you have already created a mapped drive for your users.</span></span> <span data-ttu-id="62634-132">Nesse caso, pode seus arquivos na unidade de saudação redirecionada zip e, em seguida, salvá-los tootheir PC local.</span><span class="sxs-lookup"><span data-stu-id="62634-132">In this case, they can zip their files on hello redirected drive and then save them tootheir local PC.</span></span>

## <a name="how-administrators-can-export-data"></a><span data-ttu-id="62634-133">Como os administradores podem exportar dados</span><span class="sxs-lookup"><span data-stu-id="62634-133">How administrators can export data</span></span>

<span data-ttu-id="62634-134">Administra para o Azure RemoteApp pode exportar todos os discos de perfil de usuário (UDP) para todas as coleções dentro de uma assinatura de tooAzure armazenamento usando o Azure PowerShell cmdlet Export-AzureRemoteAppUserDisk.</span><span class="sxs-lookup"><span data-stu-id="62634-134">Administers for Azure RemoteApp can export all user profile disks (UPD) for all collections within a subscription tooAzure Storage using Azure PowerShell cmdlet, Export-AzureRemoteAppUserDisk.</span></span>  <span data-ttu-id="62634-135">Não há nenhuma capacidade tooselect individuais UPD.</span><span class="sxs-lookup"><span data-stu-id="62634-135">There is no ability tooselect individual UPD's.</span></span>  <span data-ttu-id="62634-136">Quando Olá comando do PowerShell é executado, cada disco de usuário será um 50gb de tamanho de disco fixo e ser armazenamento tooAzure exportado.</span><span class="sxs-lookup"><span data-stu-id="62634-136">When hello PowerShell command is executed, each user disk will be a 50gb in fixed disk size and be exported tooAzure storage.</span></span>  <span data-ttu-id="62634-137">Os custos de armazenamento do Azure incorrerão imediatamente para esse armazenamento.</span><span class="sxs-lookup"><span data-stu-id="62634-137">Costs of Azure storage will incur immediately for this storage.</span></span>  <span data-ttu-id="62634-138">Quando a execução desse comando Certifique-se de não existem sessões exportação de saudação caso contrário, falhará.</span><span class="sxs-lookup"><span data-stu-id="62634-138">When running this command ensure there are no sessions otherwise hello export will fail.</span></span>

<span data-ttu-id="62634-139">UPDs para implantações do Azure RemoteApp ingressadas no domínio só podem ser usados novamente em uma implantação do RDS; implantações ingressadas fora do domínio não podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="62634-139">UPD's for domain joined Azure RemoteApp deployments can only be used again in an RDS deployment, non-domain joined deployments cannot be used.</span></span>  <span data-ttu-id="62634-140">Se esses discos serão usados em uma implantação de RDS é recomendável toouse nosso [automatizada scripts](https://github.com/arcadiahlyy/aramigration) que será exportar, converter e importar saudação do UDP para uma implantação de RDS.</span><span class="sxs-lookup"><span data-stu-id="62634-140">If these disks will be used in an RDS deployment we recommend toouse our [automated scripts](https://github.com/arcadiahlyy/aramigration) that will export, convert, and import hello UPD's into an RDS deployment.</span></span>

