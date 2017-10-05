---
title: "Persistir arquivos no Azure Cloud Shell (versão prévia) | Microsoft Docs"
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
ms.openlocfilehash: 61a8bfcf3704f361432400771d8fcc8b81927b53
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="555a7-103">Persistir arquivos no Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="555a7-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="555a7-104">O Cloud Shell faz uso do Armazenamento de Arquivos do Azure para persistir os arquivos entre as sessões.</span><span class="sxs-lookup"><span data-stu-id="555a7-104">Cloud Shell takes advantage of Azure File storage to persist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="555a7-105">Configurar um compartilhamento de arquivos `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="555a7-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="555a7-106">No primeiro início, o Cloud Shell solicita a associação de um compartilhamento de arquivos novo ou existente para persistir arquivos entre as sessões.</span><span class="sxs-lookup"><span data-stu-id="555a7-106">On initial start, Cloud Shell prompts you to associate a new or existing file share to persist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="555a7-107">Criar novo armazenamento</span><span class="sxs-lookup"><span data-stu-id="555a7-107">Create new storage</span></span>

<span data-ttu-id="555a7-108">Ao usar as configurações básicas e seleciona apenas uma assinatura, o Cloud Shell criará três recursos em seu nome na região com suporte mais próxima de você:</span><span class="sxs-lookup"><span data-stu-id="555a7-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in the supported region that's nearest to you:</span></span>
* <span data-ttu-id="555a7-109">Grupo de recursos: `cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="555a7-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="555a7-110">Conta de armazenamento: `cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="555a7-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="555a7-111">Compartilhamento de arquivos:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="555a7-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![A configuração da assinatura](media/basic-storage.png)

<span data-ttu-id="555a7-113">O compartilhamento de arquivos é montado como `clouddrive` no seu diretório `$Home`.</span><span class="sxs-lookup"><span data-stu-id="555a7-113">The file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="555a7-114">O compartilhamento de arquivos também é usado para armazenar uma imagem de 5 GB criada para você que atualiza e persiste automaticamente seu diretório `$Home`.</span><span class="sxs-lookup"><span data-stu-id="555a7-114">The file share is also used to store a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="555a7-115">Isso é uma ação única e o compartilhamento de arquivos será montado automaticamente nas sessões subsequentes.</span><span class="sxs-lookup"><span data-stu-id="555a7-115">This is a one-time action, and the file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="555a7-116">Usar recursos existentes</span><span class="sxs-lookup"><span data-stu-id="555a7-116">Use existing resources</span></span>

<span data-ttu-id="555a7-117">Usando a opção avançada, você pode associar recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="555a7-117">By using the advanced option, you can associate existing resources.</span></span> <span data-ttu-id="555a7-118">Quando aparecer o prompt de instalação de armazenamento, selecione **Mostrar configurações avançadas** para exibir opções adicionais.</span><span class="sxs-lookup"><span data-stu-id="555a7-118">When the storage setup prompt appears, select **Show advanced settings** to view additional options.</span></span> <span data-ttu-id="555a7-119">Compartilhamentos de arquivos existentes recebem uma imagem do usuário de 5 GB para persistir seu diretório `$Home`.</span><span class="sxs-lookup"><span data-stu-id="555a7-119">Existing file shares receive a 5-GB user image to persist your `$Home` directory.</span></span> <span data-ttu-id="555a7-120">Os menus suspensos são filtrados para sua região do Cloud Shell e para contas de armazenamento com redundância local e geográfica.</span><span class="sxs-lookup"><span data-stu-id="555a7-120">The drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![A configuração do grupo de recursos](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="555a7-122">Restringir a criação de recursos com uma política de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="555a7-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="555a7-123">As contas de armazenamento criadas no Cloud Shell são marcadas com `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="555a7-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="555a7-124">Se você deseja impedir que os usuários criem contas de armazenamento no Cloud Shell, crie uma [Política de recursos do Azure para marcas](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) que seja disparada por essa marca específica.</span><span class="sxs-lookup"><span data-stu-id="555a7-124">If you want to disallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="555a7-125">Como funciona o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="555a7-125">How Cloud Shell works</span></span>
<span data-ttu-id="555a7-126">O Cloud Shell persiste arquivos usando os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="555a7-126">Cloud Shell persists files through both of the following methods:</span></span>
* <span data-ttu-id="555a7-127">Criando uma imagem de disco do seu diretório `$Home` para persistir todo o conteúdo do diretório.</span><span class="sxs-lookup"><span data-stu-id="555a7-127">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="555a7-128">A imagem de disco é salva no compartilhamento de arquivos especificado como `acc_<User>.img` em `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img` e sincroniza as alterações automaticamente.</span><span class="sxs-lookup"><span data-stu-id="555a7-128">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="555a7-129">Montagem do compartilhamento de arquivos especificado como `clouddrive` no diretório `$Home` para que haja interação direta com o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="555a7-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="555a7-130">`/Home/<User>/clouddrive` é mapeado para `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="555a7-130">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="555a7-131">Todos os arquivos em seu diretório `$Home` como chaves SSH são persistidos em sua imagem de disco do usuário, que é armazenada no compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="555a7-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="555a7-132">Aplique as práticas recomendadas ao persistir informações em seu diretório `$Home` e no compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="555a7-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-the-clouddrive-command"></a><span data-ttu-id="555a7-133">Use o comando `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="555a7-133">Use the `clouddrive` command</span></span>
<span data-ttu-id="555a7-134">Com o Cloud Shell, você pode executar um comando denominado `clouddrive`, que permite a atualização manual do compartilhamento de arquivos que está montado no Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="555a7-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that's mounted to Cloud Shell.</span></span>
<span data-ttu-id="555a7-135">![Usando o comando “clouddrive”](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="555a7-135">![Running the "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="555a7-136">Montar um novo`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="555a7-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="555a7-137">Pré-requisitos para montagem manual</span><span class="sxs-lookup"><span data-stu-id="555a7-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="555a7-138">Você pode atualizar o compartilhamento de arquivos associado ao Cloud Shell usando o comando `clouddrive mount`.</span><span class="sxs-lookup"><span data-stu-id="555a7-138">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="555a7-139">Se estiver montando um compartilhamento de arquivos existente, as contas de armazenamento deverão atender ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="555a7-139">If you mount an existing file share, the storage accounts must be:</span></span>
* <span data-ttu-id="555a7-140">Armazenamento redundante localmente ou armazenamento com redundância geográfica para dar suporte a compartilhamentos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="555a7-140">Locally-redundant storage or geo-redundant storage to support file shares.</span></span>
* <span data-ttu-id="555a7-141">Localizadas na região atribuída a você.</span><span class="sxs-lookup"><span data-stu-id="555a7-141">Located in your assigned region.</span></span> <span data-ttu-id="555a7-142">Ao fazer a integração, a região atribuída a você será listada no nome do grupo de recursos `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="555a7-142">When you are onboarding, the region you are assigned to is listed in the resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="555a7-143">Regiões de armazenamento com suporte</span><span class="sxs-lookup"><span data-stu-id="555a7-143">Supported storage regions</span></span>
<span data-ttu-id="555a7-144">Os arquivos do Azure devem residir na mesma região que o computador do Cloud Shell em que você estiver montando.</span><span class="sxs-lookup"><span data-stu-id="555a7-144">The Azure files must reside in the same region as the Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="555a7-145">Há clusters do Cloud Shell nas regiões a seguir:</span><span class="sxs-lookup"><span data-stu-id="555a7-145">Cloud Shell clusters currently exist in the following regions:</span></span>
|<span data-ttu-id="555a7-146">Área</span><span class="sxs-lookup"><span data-stu-id="555a7-146">Area</span></span>|<span data-ttu-id="555a7-147">Região</span><span class="sxs-lookup"><span data-stu-id="555a7-147">Region</span></span>|
|---|---|
|<span data-ttu-id="555a7-148">Américas</span><span class="sxs-lookup"><span data-stu-id="555a7-148">Americas</span></span>|<span data-ttu-id="555a7-149">Leste dos EUA, Centro-Sul dos EUA, Oeste dos EUA</span><span class="sxs-lookup"><span data-stu-id="555a7-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="555a7-150">Europa</span><span class="sxs-lookup"><span data-stu-id="555a7-150">Europe</span></span>|<span data-ttu-id="555a7-151">Norte da Europa, Europa Ocidental</span><span class="sxs-lookup"><span data-stu-id="555a7-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="555a7-152">Pacífico Asiático</span><span class="sxs-lookup"><span data-stu-id="555a7-152">Asia Pacific</span></span>|<span data-ttu-id="555a7-153">Índia Central, Sudeste Asiático</span><span class="sxs-lookup"><span data-stu-id="555a7-153">India Central, Southeast Asia</span></span>|

### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="555a7-154">O comando `clouddrive mount`</span><span class="sxs-lookup"><span data-stu-id="555a7-154">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="555a7-155">Se você estiver montando um novo compartilhamento de arquivos, uma nova imagem de usuário será criada para o diretório `$Home`, pois a imagem de `$Home` anterior é mantida no compartilhamento de arquivos anterior.</span><span class="sxs-lookup"><span data-stu-id="555a7-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in the previous file share.</span></span>

<span data-ttu-id="555a7-156">Execute o comando `clouddrive mount` com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="555a7-156">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="555a7-157">Para exibir mais detalhes, execute `clouddrive mount -h` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="555a7-157">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Executando o comando ' clouddrive mount'](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="555a7-159">Desmontar o `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="555a7-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="555a7-160">Você pode desmontar um compartilhamento de arquivos que esteja montado no Cloud Shell a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="555a7-160">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="555a7-161">Após desmontar o compartilhamento de arquivos, você receberá uma solicitação para montar um novo compartilhamento de arquivo antes de sua próxima sessão.</span><span class="sxs-lookup"><span data-stu-id="555a7-161">Once your file share is unmounted, you will be prompted to mount a new file share prior to your next session.</span></span>

<span data-ttu-id="555a7-162">Para remover um compartilhamento de arquivos do Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="555a7-162">To remove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="555a7-163">Execute `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="555a7-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="555a7-164">Reconheça e confirme os prompts.</span><span class="sxs-lookup"><span data-stu-id="555a7-164">Acknowledge and confirm the prompts.</span></span>

<span data-ttu-id="555a7-165">Seu compartilhamento de arquivos continuará existindo se você não o excluir manualmente.</span><span class="sxs-lookup"><span data-stu-id="555a7-165">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="555a7-166">O Cloud Shell deixará de procurar por esse compartilhamento de arquivos em sessões subsequentes.</span><span class="sxs-lookup"><span data-stu-id="555a7-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="555a7-167">Para exibir mais detalhes, execute `clouddrive unmount -h` conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="555a7-167">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Executando o comando ' clouddrive unmount'](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="555a7-169">A execução desse comando não excluirá qualquer recurso.</span><span class="sxs-lookup"><span data-stu-id="555a7-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="555a7-170">A exclusão manual de um grupo de recursos, conta de armazenamento ou compartilhamento de arquivos mapeado para o Cloud Shell apagará permanentemente sua imagem de diretório `$Home` e todos os arquivos no compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="555a7-170">Manually deleting a resource group, storage account, or file share that is mapped to Cloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="555a7-171">Essa ação não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="555a7-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="555a7-172">Listar compartilhamentos de arquivos do `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="555a7-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="555a7-173">Para descobrir qual compartilhamento de arquivos está montado como `clouddrive`, execute o comando `df` a seguir.</span><span class="sxs-lookup"><span data-stu-id="555a7-173">To discover which file share is mounted as `clouddrive`, run the following `df` command.</span></span> 

<span data-ttu-id="555a7-174">O caminho de arquivo para a unidade de nuvem mostra o nome da conta de armazenamento e o compartilhamento de arquivos na URL.</span><span class="sxs-lookup"><span data-stu-id="555a7-174">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="555a7-175">Por exemplo, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="555a7-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

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

## <a name="transfer-local-files-to-cloud-shell"></a><span data-ttu-id="555a7-176">Transferir arquivos locais para o Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="555a7-176">Transfer local files to Cloud Shell</span></span>
<span data-ttu-id="555a7-177">O diretório `clouddrive` é sincronizado com a folha de armazenamento do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="555a7-177">The `clouddrive` directory syncs with the Azure portal storage blade.</span></span> <span data-ttu-id="555a7-178">Use essa folha para transferir arquivos locais de ou para o compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="555a7-178">Use this blade to transfer local files to or from your file share.</span></span> <span data-ttu-id="555a7-179">A atualização dos arquivos a partir do Cloud Shell é refletida na GUI do armazenamento de arquivos quando você atualiza a folha.</span><span class="sxs-lookup"><span data-stu-id="555a7-179">Updating files from within Cloud Shell is reflected in the file storage GUI when you refresh the blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="555a7-180">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="555a7-180">Download files</span></span>

![Lista de arquivos locais](media/download.png)
1. <span data-ttu-id="555a7-182">No portal do Azure, vá para o compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="555a7-182">In the Azure portal, go to the mounted file share.</span></span>
2. <span data-ttu-id="555a7-183">Selecione o arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="555a7-183">Select the target file.</span></span>
3. <span data-ttu-id="555a7-184">Selecione o botão **Baixar** .</span><span class="sxs-lookup"><span data-stu-id="555a7-184">Select the **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="555a7-185">Carregar arquivos</span><span class="sxs-lookup"><span data-stu-id="555a7-185">Upload files</span></span>

![Arquivos locais a serem carregados](media/upload.png)
1. <span data-ttu-id="555a7-187">Vá para o compartilhamento de arquivos montado.</span><span class="sxs-lookup"><span data-stu-id="555a7-187">Go to your mounted file share.</span></span>
2. <span data-ttu-id="555a7-188">Selecione o botão **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="555a7-188">Select the **Upload** button.</span></span>
3. <span data-ttu-id="555a7-189">Selecione os arquivos que você deseja carregar.</span><span class="sxs-lookup"><span data-stu-id="555a7-189">Select the file or files that you want to upload.</span></span>
4. <span data-ttu-id="555a7-190">Confirme o upload.</span><span class="sxs-lookup"><span data-stu-id="555a7-190">Confirm the upload.</span></span>

<span data-ttu-id="555a7-191">Agora você deve ver os arquivos que estão acessíveis em seu diretório do `clouddrive` no Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="555a7-191">You should now see the files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="555a7-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="555a7-192">Next steps</span></span>
[<span data-ttu-id="555a7-193">Início rápido do Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="555a7-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="555a7-194">
[Saiba mais sobre o armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="555a7-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="555a7-195">
[Saiba mais sobre marcas de armazenamento](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="555a7-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
