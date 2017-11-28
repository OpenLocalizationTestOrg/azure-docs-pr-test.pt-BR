---
title: "arquivos de aaaPersist no Shell de nuvem do Azure (visualização) | Microsoft Docs"
description: Passo a passo de como o Azure Cloud Shell persiste arquivos.
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="b0c3f-103">Persistir arquivos no Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0c3f-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="b0c3f-104">Shell de nuvem tira proveito dos arquivos de toopersist de armazenamento de arquivo do Azure entre sessões.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="b0c3f-105">Configurar um compartilhamento de arquivos `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="b0c3f-106">Na inicialização inicial, o Shell de nuvem solicita tooassociate um arquivo novo ou existente compartilhar arquivos toopersist entre sessões.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="b0c3f-107">Criar novo armazenamento</span><span class="sxs-lookup"><span data-stu-id="b0c3f-107">Create new storage</span></span>

<span data-ttu-id="b0c3f-108">Quando você usa as configurações básicas e seleciona apenas uma assinatura, o Shell de nuvem cria três recursos em seu nome na região Olá suportada mais próximo tooyou:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="b0c3f-109">Grupo de recursos: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="b0c3f-110">Conta de armazenamento: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="b0c3f-111">Compartilhamento de arquivos:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![configuração de assinatura de saudação](media/basic-storage.png)

<span data-ttu-id="b0c3f-113">compartilhamento de arquivo Hello monta como `clouddrive` no seu `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="b0c3f-114">Olá compartilhamento de arquivos é também usado toostore uma imagem de 5 GB é criada para você e que automaticamente atualiza e persiste o `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="b0c3f-115">Isso é uma ação única e compartilhamento de arquivo hello monta automaticamente nas sessões subsequentes.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="b0c3f-116">Usar recursos existentes</span><span class="sxs-lookup"><span data-stu-id="b0c3f-116">Use existing resources</span></span>

<span data-ttu-id="b0c3f-117">Usando Olá opções avançadas, você pode associar recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="b0c3f-118">Quando aparece o prompt de configuração de armazenamento hello, selecione **Mostrar configurações avançadas** tooview as opções adicionais.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="b0c3f-119">Compartilhamentos de arquivos existentes recebem um toopersist de imagem de usuário de 5 GB a `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="b0c3f-120">menus suspensos de saudação são filtrados para a sua região do Shell de nuvem e para contas de armazenamento com redundância local & com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![configuração de grupo de recursos de saudação](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="b0c3f-122">Restringir a criação de recursos com uma política de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="b0c3f-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="b0c3f-123">As contas de armazenamento criadas no Cloud Shell são marcadas com `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="b0c3f-124">Toodisallow usuários criando contas de armazenamento em nuvem Shell, crie um [política de recurso do Azure para marcas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que são disparadas por essa marca específica.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="b0c3f-125">Como funciona o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0c3f-125">How Cloud Shell works</span></span>
<span data-ttu-id="b0c3f-126">Shell de nuvem persiste arquivos por meio de saudação métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="b0c3f-127">Criar uma imagem de disco do seu `$Home` directory toopersist todos os conteúdo no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="b0c3f-128">imagem de disco de saudação é salvo em seu compartilhamento de arquivo especificado como `acc_<User>.img` em `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, e sincronizará as alterações.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="b0c3f-129">Montagem do compartilhamento de arquivos especificado como `clouddrive` no diretório `$Home` para que haja interação direta com o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="b0c3f-130">`/Home/<User>/clouddrive`está mapeada muito`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="b0c3f-131">Todos os arquivos em seu diretório `$Home` como chaves SSH são persistidos em sua imagem de disco do usuário, que é armazenada no compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="b0c3f-132">Aplique as práticas recomendadas ao persistir informações em seu diretório `$Home` e no compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="b0c3f-133">Saudação de uso `clouddrive` comando</span><span class="sxs-lookup"><span data-stu-id="b0c3f-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="b0c3f-134">Com o Shell de nuvem, você pode executar um comando denominado `clouddrive`, que permite que você toomanually atualização Olá compartilhamento de arquivos que tooCloud montado Shell.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="b0c3f-135">![Executando o comando "clouddrive" hello](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="b0c3f-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="b0c3f-136">Montar um novo`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="b0c3f-137">Pré-requisitos para montagem manual</span><span class="sxs-lookup"><span data-stu-id="b0c3f-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="b0c3f-138">Você pode atualizar o compartilhamento de arquivo hello associada com o Shell de nuvem usando Olá `clouddrive mount` comando.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="b0c3f-139">Se você monta um compartilhamento de arquivo, contas de armazenamento Olá devem ser:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="b0c3f-140">O armazenamento redundante localmente ou compartilhamentos de arquivos do armazenamento com redundância geográfica toosupport.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="b0c3f-141">Localizadas na região atribuída a você.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-141">Located in your assigned region.</span></span> <span data-ttu-id="b0c3f-142">Quando a integração, região Olá você recebem toois listados no nome do grupo de recursos de saudação `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="b0c3f-143">Regiões de armazenamento com suporte</span><span class="sxs-lookup"><span data-stu-id="b0c3f-143">Supported storage regions</span></span>
<span data-ttu-id="b0c3f-144">Hello arquivos do Azure devem residir no hello mesma região que Olá nuvem Shell máquina que estiver montando sejam.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="b0c3f-145">Clusters de Shell de nuvem existem atualmente no hello regiões a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="b0c3f-146">Área</span><span class="sxs-lookup"><span data-stu-id="b0c3f-146">Area</span></span>|<span data-ttu-id="b0c3f-147">Região</span><span class="sxs-lookup"><span data-stu-id="b0c3f-147">Region</span></span>|
|---|---|
|<span data-ttu-id="b0c3f-148">Américas</span><span class="sxs-lookup"><span data-stu-id="b0c3f-148">Americas</span></span>|<span data-ttu-id="b0c3f-149">Leste dos EUA, Centro-Sul dos EUA, Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="b0c3f-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="b0c3f-150">Europa</span><span class="sxs-lookup"><span data-stu-id="b0c3f-150">Europe</span></span>|<span data-ttu-id="b0c3f-151">Norte da Europa, Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="b0c3f-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="b0c3f-152">Pacífico Asiático</span><span class="sxs-lookup"><span data-stu-id="b0c3f-152">Asia Pacific</span></span>|<span data-ttu-id="b0c3f-153">Índia Central, Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="b0c3f-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="b0c3f-154">Olá `clouddrive mount` comando</span><span class="sxs-lookup"><span data-stu-id="b0c3f-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="b0c3f-155">Se você estiver montando um novo compartilhamento de arquivo, uma nova imagem de usuário é criada para sua `$Home` diretório, porque seu anterior `$Home` imagem é mantida no compartilhamento de arquivo hello anterior.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="b0c3f-156">Executar Olá `clouddrive mount` com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="b0c3f-157">tooview obter mais detalhes, execute `clouddrive mount -h`, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Olá em execução ' clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="b0c3f-159">Desmontar o `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="b0c3f-160">Você pode desmontar um compartilhamento de arquivos que tooCloud montado Shell a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="b0c3f-161">Depois que o compartilhamento de arquivos é desmontado, será solicitado toomount um novo tooyour anterior de compartilhamento de arquivo próxima sessão.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="b0c3f-162">tooremove um arquivo de compartilhamento do Shell de nuvem:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="b0c3f-163">Execute `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="b0c3f-164">Confirmar e confirmar Olá prompts.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="b0c3f-165">O compartilhamento de arquivos continuará tooexist, a menos que você exclua-o manualmente.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="b0c3f-166">O Cloud Shell deixará de procurar por esse compartilhamento de arquivos em sessões subsequentes.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="b0c3f-167">tooview obter mais detalhes, execute `clouddrive unmount -h`, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="b0c3f-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Olá em execução ' clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="b0c3f-169">A execução desse comando não excluirá qualquer recurso.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="b0c3f-170">Excluir manualmente um grupo de recursos, a conta de armazenamento ou o compartilhamento de arquivos que é mapeado tooCloud Shell excluirá permanentemente seu `$Home` imagem de diretório e outros arquivos em seu compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="b0c3f-171">Essa ação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="b0c3f-172">Listar compartilhamentos de arquivos do `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="b0c3f-173">toodiscover o compartilhamento de arquivos está montado como `clouddrive`, execute o seguinte Olá `df` comando.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="b0c3f-174">tooclouddrive de caminho de arquivo Hello mostra que o nome da conta de armazenamento e compartilhamento de arquivos na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="b0c3f-175">Por exemplo, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="b0c3f-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="b0c3f-176">Transferência de arquivos locais tooCloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0c3f-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="b0c3f-177">Olá `clouddrive` diretório for sincronizado com folha de armazenamento do portal do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="b0c3f-178">Use este tooor de arquivos local tootransfer folha do seu compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="b0c3f-179">Atualizar os arquivos a partir do Shell de nuvem é refletido no armazenamento de arquivo hello GUI quando você atualiza a folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="b0c3f-180">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="b0c3f-180">Download files</span></span>

![Lista de arquivos locais](media/download.png)
1. <span data-ttu-id="b0c3f-182">No Olá portal do Azure, acesse o compartilhamento de arquivos montados toohello.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="b0c3f-183">Selecione o arquivo de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-183">Select hello target file.</span></span>
3. <span data-ttu-id="b0c3f-184">Selecione Olá **baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="b0c3f-185">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="b0c3f-185">Upload files</span></span>

![Arquivos locais toobe carregado](media/upload.png)
1. <span data-ttu-id="b0c3f-187">Acesse o compartilhamento de arquivos montados tooyour.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="b0c3f-188">Selecione Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="b0c3f-189">Selecione o arquivo de saudação ou arquivos que você deseja tooupload.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="b0c3f-190">Confirme o carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-190">Confirm hello upload.</span></span>

<span data-ttu-id="b0c3f-191">Agora você deve ver arquivos Olá acessíveis em sua `clouddrive` diretório no Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b0c3f-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0c3f-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0c3f-192">Next steps</span></span>
[<span data-ttu-id="b0c3f-193">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="b0c3f-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="b0c3f-194">
[Saiba mais sobre o armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="b0c3f-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="b0c3f-195">
[Saiba mais sobre marcas de armazenamento](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="b0c3f-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
