---
title: "Notas de versão do Gerenciador de armazenamento do Azure (visualização) aaaMicrosoft | Microsoft Docs"
description: "Notas de versão do Gerenciador de Armazenamento do Microsoft Azure (Visualização)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a><span data-ttu-id="10157-103">Notas de versão do Gerenciador de Armazenamento do Microsoft Azure (Visualização)</span><span class="sxs-lookup"><span data-stu-id="10157-103">Microsoft Azure Storage Explorer (Preview) release notes</span></span>

<span data-ttu-id="10157-104">Este artigo contém a versão de hello anotações para o Azure Storage Explorer 0.8.16 (visualização) da versão, bem como notas de versão para versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="10157-104">This article contains hello release notes for Azure Storage Explorer 0.8.16 (Preview) release, as well as release notes for previous versions.</span></span>

<span data-ttu-id="10157-105">[Gerenciador de armazenamento do Microsoft Azure (visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="10157-105">[Microsoft Azure Storage Explorer (Preview)](./vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span>

## <a name="version-0816-preview"></a><span data-ttu-id="10157-106">Versão 0.8.16 (Versão Prévia)</span><span class="sxs-lookup"><span data-stu-id="10157-106">Version 0.8.16 (Preview)</span></span>
<span data-ttu-id="10157-107">8/21/2017</span><span class="sxs-lookup"><span data-stu-id="10157-107">8/21/2017</span></span>

### <a name="download-azure-storage-explorer-0816-preview"></a><span data-ttu-id="10157-108">Baixar o Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia)</span><span class="sxs-lookup"><span data-stu-id="10157-108">Download Azure Storage Explorer 0.8.16 (Preview)</span></span>
- [<span data-ttu-id="10157-109">Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Windows</span><span class="sxs-lookup"><span data-stu-id="10157-109">Azure Storage Explorer 0.8.16 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=708343)
- [<span data-ttu-id="10157-110">Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Mac</span><span class="sxs-lookup"><span data-stu-id="10157-110">Azure Storage Explorer 0.8.16 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=708342)
- [<span data-ttu-id="10157-111">Gerenciador de Armazenamento do Azure 0.8.16 (Versão Prévia) para Linux</span><span class="sxs-lookup"><span data-stu-id="10157-111">Azure Storage Explorer 0.8.16 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a><span data-ttu-id="10157-112">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-112">New</span></span>
* <span data-ttu-id="10157-113">Quando você abre um blob, Gerenciador de armazenamento solicitará que você tooupload Olá baixado arquivos se uma mudança for detectada</span><span class="sxs-lookup"><span data-stu-id="10157-113">When you open a blob, Storage Explorer will prompt you tooupload hello downloaded file if a change is detected</span></span>
* <span data-ttu-id="10157-114">Experiência de aprimorada de conexão no Azure Stack</span><span class="sxs-lookup"><span data-stu-id="10157-114">Enhanced Azure Stack sign-in experience</span></span>
* <span data-ttu-id="10157-115">Desempenho aprimorado de saudação do upload/download de muitas empresas de pequeno arquivos no hello mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="10157-115">Improved hello performance of uploading/downloading many small files at hello same time</span></span>


### <a name="fixes"></a><span data-ttu-id="10157-116">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-116">Fixes</span></span>
* <span data-ttu-id="10157-117">Para alguns tipos de blob, escolher "substituir" muito durante um conflito de carregamento, às vezes, resultaria em carregamento hello está sendo reiniciado.</span><span class="sxs-lookup"><span data-stu-id="10157-117">For some blob types, choosing too"replace" during an upload conflict would sometimes result in hello upload being restarted.</span></span> 
* <span data-ttu-id="10157-118">Na versão 0.8.15, os uploads às vezes paralisavam em 99%.</span><span class="sxs-lookup"><span data-stu-id="10157-118">In version 0.8.15, uploads would sometimes stall at 99%.</span></span>
* <span data-ttu-id="10157-119">Ao carregar o compartilhamento de arquivos de tooa de arquivos, se você escolher o diretório de tooa tooupload que ainda não existe, o carregamento falhará.</span><span class="sxs-lookup"><span data-stu-id="10157-119">When uploading files tooa file share, if you chose tooupload tooa directory which did not yet exist, your upload would fail.</span></span>
* <span data-ttu-id="10157-120">O Gerenciador de Armazenamento estava gerando incorretamente os carimbos de data/hora para assinaturas de acesso compartilhadas e consultas de tabela.</span><span class="sxs-lookup"><span data-stu-id="10157-120">Storage Explorer was incorrectly generating time stamps for shared access signatures and table queries.</span></span>


<span data-ttu-id="10157-121">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-121">Known Issues</span></span>
* <span data-ttu-id="10157-122">Usar uma cadeia de conexão de nome e chave não funciona atualmente.</span><span class="sxs-lookup"><span data-stu-id="10157-122">Using a name and key connection string does not currently work.</span></span> <span data-ttu-id="10157-123">Ele será corrigido na próxima versão do hello.</span><span class="sxs-lookup"><span data-stu-id="10157-123">It will be fixed in hello next release.</span></span> <span data-ttu-id="10157-124">Até lá, você pode usar anexar com o nome e chave.</span><span class="sxs-lookup"><span data-stu-id="10157-124">Until then you can use attach with name and key.</span></span>
* <span data-ttu-id="10157-125">Se você tentar tooopen um arquivo com um nome de arquivo inválido do Windows, o download Olá resultará em um arquivo não encontrado o erro.</span><span class="sxs-lookup"><span data-stu-id="10157-125">If you try tooopen a file with an invalid Windows file name, hello download will result in a file not found error.</span></span>
* <span data-ttu-id="10157-126">Depois de clicar em "Cancelar" em uma tarefa, pode demorar um pouco para toocancel essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="10157-126">After clicking "Cancel" on a task, it may take a while for that task toocancel.</span></span> <span data-ttu-id="10157-127">Essa é uma limitação da biblioteca de nó de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10157-127">This is a limitation of hello Azure Storage Node library.</span></span>
* <span data-ttu-id="10157-128">Depois de concluir o carregamento de um blob, guia Olá que iniciou o carregamento de saudação é atualizado.</span><span class="sxs-lookup"><span data-stu-id="10157-128">After completing a blob upload, hello tab which initiated hello upload is refreshed.</span></span> <span data-ttu-id="10157-129">Isso é uma alteração de comportamento anterior e também causará toobe novamente executada toohello raiz do contêiner Olá em que estão.</span><span class="sxs-lookup"><span data-stu-id="10157-129">This is a change from previous behavior, and will also cause you toobe taken back toohello root of hello container you are in.</span></span>
* <span data-ttu-id="10157-130">Se você escolher Olá certificado incorreto do PIN/cartão inteligente, em seguida, você precisará toorestart em ordem toohave Gerenciador de armazenamento, esquecer essa decisão.</span><span class="sxs-lookup"><span data-stu-id="10157-130">If you choose hello wrong PIN/Smartcard certificate, then you will need toorestart in order toohave Storage Explorer forget that decision.</span></span>
* <span data-ttu-id="10157-131">Painel de configurações de conta Olá pode mostrar que você precisa de assinaturas de toofilter tooreenter credenciais.</span><span class="sxs-lookup"><span data-stu-id="10157-131">hello account settings panel may show that you need tooreenter credentials toofilter subscriptions.</span></span>
* <span data-ttu-id="10157-132">Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="10157-132">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="10157-133">Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.</span><span class="sxs-lookup"><span data-stu-id="10157-133">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="10157-134">Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada.</span><span class="sxs-lookup"><span data-stu-id="10157-134">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span>
* <span data-ttu-id="10157-135">Para usuários no Ubuntu 14.04, será necessário tooensure GCC está ativo toodate – isso pode ser feito executando Olá comandos a seguir e, em seguida, reinicie seu computador:</span><span class="sxs-lookup"><span data-stu-id="10157-135">For users on Ubuntu 14.04, you will need tooensure GCC is up toodate - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* <span data-ttu-id="10157-136">Para usuários no Ubuntu 17.04, será necessário tooinstall GConf - isso pode ser feito executando Olá comandos a seguir e, em seguida, reinicie seu computador:</span><span class="sxs-lookup"><span data-stu-id="10157-136">For users on Ubuntu 17.04, you will need tooinstall GConf - this can be done by running hello following commands, and then restarting your machine:</span></span>

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a><span data-ttu-id="10157-137">Versão 0.8.14 (Visualização)</span><span class="sxs-lookup"><span data-stu-id="10157-137">Version 0.8.14 (Preview)</span></span>
<span data-ttu-id="10157-138">06/22/2017</span><span class="sxs-lookup"><span data-stu-id="10157-138">06/22/2017</span></span>

### <a name="download-azure-storage-explorer-0814-preview"></a><span data-ttu-id="10157-139">Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização)</span><span class="sxs-lookup"><span data-stu-id="10157-139">Download Azure Storage Explorer 0.8.14 (Preview)</span></span>
* [<span data-ttu-id="10157-140">Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Windows</span><span class="sxs-lookup"><span data-stu-id="10157-140">Download Azure Storage Explorer 0.8.14 (Preview) for Windows</span></span>](https://go.microsoft.com/fwlink/?LinkId=809306)
* [<span data-ttu-id="10157-141">Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Mac</span><span class="sxs-lookup"><span data-stu-id="10157-141">Download Azure Storage Explorer 0.8.14 (Preview) for Mac</span></span>](https://go.microsoft.com/fwlink/?LinkId=809307)
* [<span data-ttu-id="10157-142">Baixar o Gerenciador de Armazenamento do Azure 0.8.14 (Visualização) para Linux</span><span class="sxs-lookup"><span data-stu-id="10157-142">Download Azure Storage Explorer 0.8.14 (Preview) for Linux</span></span>](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a><span data-ttu-id="10157-143">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-143">New</span></span>

* <span data-ttu-id="10157-144">Too1.7.2 de versão elétrons atualizado em vantagem de tootake de ordem de várias atualizações críticas de segurança</span><span class="sxs-lookup"><span data-stu-id="10157-144">Updated Electron version too1.7.2 in order tootake advantage of several critical security updates</span></span>
* <span data-ttu-id="10157-145">Você agora pode acessar rapidamente o guia de solução de problemas online Olá no menu de ajuda Olá</span><span class="sxs-lookup"><span data-stu-id="10157-145">You can now quickly access hello online troubleshooting guide from hello help menu</span></span>
* <span data-ttu-id="10157-146">[Guia][2] de solução de problemas do Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="10157-146">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="10157-147">[Instruções] [ 3] sobre conexão de assinatura do Azure pilha tooan</span><span class="sxs-lookup"><span data-stu-id="10157-147">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

### <a name="known-issues"></a><span data-ttu-id="10157-148">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-148">Known Issues</span></span>

* <span data-ttu-id="10157-149">Botões da caixa de diálogo de confirmação do hello excluir pasta não se registrar com hello cliques do mouse no Linux.</span><span class="sxs-lookup"><span data-stu-id="10157-149">Buttons on hello delete folder confirmation dialog don't register with hello mouse clicks on Linux.</span></span> <span data-ttu-id="10157-150">Solução alternativa é a chave do toouse Olá Enter</span><span class="sxs-lookup"><span data-stu-id="10157-150">Workaround is toouse hello Enter key</span></span>
* <span data-ttu-id="10157-151">Se você escolher Olá certificado PIN/cartão inteligente errado, será necessário toorestart em ordem toohave Gerenciador de armazenamento se esqueça de decisão Olá</span><span class="sxs-lookup"><span data-stu-id="10157-151">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="10157-152">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros</span><span class="sxs-lookup"><span data-stu-id="10157-152">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="10157-153">Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem</span><span class="sxs-lookup"><span data-stu-id="10157-153">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="10157-154">Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="10157-154">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="10157-155">Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.</span><span class="sxs-lookup"><span data-stu-id="10157-155">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="10157-156">Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada.</span><span class="sxs-lookup"><span data-stu-id="10157-156">Although Azure Stack doesn't currently support File Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="10157-157">Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="10157-157">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a><span data-ttu-id="10157-158">Versões anteriores</span><span class="sxs-lookup"><span data-stu-id="10157-158">Previous releases</span></span>

* [<span data-ttu-id="10157-159">Versão 0.8.13</span><span class="sxs-lookup"><span data-stu-id="10157-159">Version 0.8.13</span></span>](#version-0813)
* [<span data-ttu-id="10157-160">Versão 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="10157-160">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>](#version-0812--0811--0810)
* [<span data-ttu-id="10157-161">Versão 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="10157-161">Version 0.8.9 / 0.8.8</span></span>](#version-089--088)
* [<span data-ttu-id="10157-162">Versão 0.8.7</span><span class="sxs-lookup"><span data-stu-id="10157-162">Version 0.8.7</span></span>](#version-087)
* [<span data-ttu-id="10157-163">Versão 0.8.6</span><span class="sxs-lookup"><span data-stu-id="10157-163">Version 0.8.6</span></span>](#version-086)
* [<span data-ttu-id="10157-164">Versão 0.8.5</span><span class="sxs-lookup"><span data-stu-id="10157-164">Version 0.8.5</span></span>](#version-085)
* [<span data-ttu-id="10157-165">Versão 0.8.4</span><span class="sxs-lookup"><span data-stu-id="10157-165">Version 0.8.4</span></span>](#version-084)
* [<span data-ttu-id="10157-166">Versão 0.8.3</span><span class="sxs-lookup"><span data-stu-id="10157-166">Version 0.8.3</span></span>](#version-083)
* [<span data-ttu-id="10157-167">Versão 0.8.2</span><span class="sxs-lookup"><span data-stu-id="10157-167">Version 0.8.2</span></span>](#version-082)
* [<span data-ttu-id="10157-168">Versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="10157-168">Version 0.8.0</span></span>](#version-080)
* [<span data-ttu-id="10157-169">Versão 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="10157-169">Version 0.7.20160509.0</span></span>](#version-07201605090)
* [<span data-ttu-id="10157-170">Versão 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="10157-170">Version 0.7.20160325.0</span></span>](#version-07201603250)
* [<span data-ttu-id="10157-171">Versão 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="10157-171">Version 0.7.20160129.1</span></span>](#version-07201601291)
* [<span data-ttu-id="10157-172">Versão 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="10157-172">Version 0.7.20160105.0</span></span>](#version-07201601050)
* [<span data-ttu-id="10157-173">Versão 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="10157-173">Version 0.7.20151116.0</span></span>](#version-07201511160)


### <a name="version-0813"></a><span data-ttu-id="10157-174">Versão 0.8.13</span><span class="sxs-lookup"><span data-stu-id="10157-174">Version 0.8.13</span></span>
<span data-ttu-id="10157-175">05/12/2017</span><span class="sxs-lookup"><span data-stu-id="10157-175">05/12/2017</span></span>

#### <a name="new"></a><span data-ttu-id="10157-176">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-176">New</span></span>

* <span data-ttu-id="10157-177">[Guia][2] de solução de problemas do Gerenciador de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="10157-177">Storage Explorer Troubleshooting [Guide][2]</span></span>
* <span data-ttu-id="10157-178">[Instruções] [ 3] sobre conexão de assinatura do Azure pilha tooan</span><span class="sxs-lookup"><span data-stu-id="10157-178">[Instructions][3] on connecting tooan Azure Stack subscription</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-179">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-179">Fixes</span></span>

* <span data-ttu-id="10157-180">Corrigido: o carregamento do arquivo tinha uma chance maior de causar um erro de falta de memória</span><span class="sxs-lookup"><span data-stu-id="10157-180">Fixed: File upload had a high chance of causing an out of memory error</span></span>
* <span data-ttu-id="10157-181">Corrigido: agora você pode entrar com PIN/Cartão inteligente</span><span class="sxs-lookup"><span data-stu-id="10157-181">Fixed: You can now sign in with PIN/Smartcard</span></span>
* <span data-ttu-id="10157-182">Corrigido: a opção Abrir no Portal agora funciona com o Azure China, Azure Alemanha, Azure US Government e Azure Stack</span><span class="sxs-lookup"><span data-stu-id="10157-182">Fixed: Open in Portal now works with Azure China, Azure Germany, Azure US Government, and Azure Stack</span></span>
* <span data-ttu-id="10157-183">Correção: Durante o carregamento de um contêiner de blob de tooa de pasta, um erro de "Operação ilegal" às vezes, ocorreria</span><span class="sxs-lookup"><span data-stu-id="10157-183">Fixed: While uploading a folder tooa blob container, an "Illegal operation" error would sometimes occur</span></span>
* <span data-ttu-id="10157-184">Corrigido: selecionar tudo foi desabilitado ao gerenciar instantâneos</span><span class="sxs-lookup"><span data-stu-id="10157-184">Fixed: Select all was disabled while managing snapshots</span></span>
* <span data-ttu-id="10157-185">Correção: Olá metadados de blob de base Olá podem obter substituídos após exibir propriedades de saudação de seus instantâneos</span><span class="sxs-lookup"><span data-stu-id="10157-185">Fixed: hello metadata of hello base blob might get overwritten after viewing hello properties of its snapshots</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-186">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-186">Known Issues</span></span>

* <span data-ttu-id="10157-187">Se você escolher Olá certificado PIN/cartão inteligente errado, será necessário toorestart em ordem toohave Gerenciador de armazenamento se esqueça de decisão Olá</span><span class="sxs-lookup"><span data-stu-id="10157-187">If you choose hello wrong PIN/Smartcard certificate then you will need toorestart in order toohave Storage Explorer forget hello decision</span></span>
* <span data-ttu-id="10157-188">Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello</span><span class="sxs-lookup"><span data-stu-id="10157-188">While zoomed in or out, hello zoom level may momentarily reset toohello default level</span></span>
* <span data-ttu-id="10157-189">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros</span><span class="sxs-lookup"><span data-stu-id="10157-189">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="10157-190">Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem</span><span class="sxs-lookup"><span data-stu-id="10157-190">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="10157-191">Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="10157-191">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="10157-192">Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.</span><span class="sxs-lookup"><span data-stu-id="10157-192">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="10157-193">Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada.</span><span class="sxs-lookup"><span data-stu-id="10157-193">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="10157-194">Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="10157-194">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a><span data-ttu-id="10157-195">Versão 0.8.12 / 0.8.11 / 0.8.10</span><span class="sxs-lookup"><span data-stu-id="10157-195">Version 0.8.12 / 0.8.11 / 0.8.10</span></span>
<span data-ttu-id="10157-196">04/07/2017</span><span class="sxs-lookup"><span data-stu-id="10157-196">04/07/2017</span></span>

#### <a name="new"></a><span data-ttu-id="10157-197">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-197">New</span></span>

* <span data-ttu-id="10157-198">Gerenciador de armazenamento agora será fechada automaticamente quando você instala uma atualização de notificação de atualização de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-198">Storage Explorer will now automatically close when you install an update from hello update notification</span></span>
* <span data-ttu-id="10157-199">O acesso rápido in-loco fornece uma experiência aprimorada para trabalhar com seus recursos acessados com frequência</span><span class="sxs-lookup"><span data-stu-id="10157-199">In-place quick access provides an enhanced experience for working with your frequently accessed resources</span></span>
* <span data-ttu-id="10157-200">No editor de contêiner de Blob hello, agora você pode ver um blob concedido pertence à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="10157-200">In hello Blob Container editor, you can now see which virtual machine a leased blob belongs to</span></span>
* <span data-ttu-id="10157-201">Agora você pode recolher painel do lado esquerdo de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-201">You can now collapse hello left side panel</span></span>
* <span data-ttu-id="10157-202">Descoberta agora é executado no Olá a mesma hora como download</span><span class="sxs-lookup"><span data-stu-id="10157-202">Discovery now runs at hello same time as download</span></span>
* <span data-ttu-id="10157-203">Usar estatísticas no contêiner de Blob, o compartilhamento de arquivos e a tabela editores toosee Olá tamanho do recurso ou seleção de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-203">Use Statistics in hello Blob Container, File Share, and Table editors toosee hello size of your resource or selection</span></span>
* <span data-ttu-id="10157-204">Você pode agora entrar tooAzure AAD (Active Directory) com base em contas de pilha do Azure.</span><span class="sxs-lookup"><span data-stu-id="10157-204">You can now sign-in tooAzure Active Directory (AAD) based Azure Stack accounts.</span></span> 
* <span data-ttu-id="10157-205">Você pode agora carregar arquivos em 32 MB as contas de armazenamento tooPremium</span><span class="sxs-lookup"><span data-stu-id="10157-205">You can now upload archive files over 32MB tooPremium storage accounts</span></span>
* <span data-ttu-id="10157-206">Suporte a acessibilidade aprimorado</span><span class="sxs-lookup"><span data-stu-id="10157-206">Improved accessibility support</span></span>
* <span data-ttu-id="10157-207">Agora você pode adicionar confiável Base 64 codificados certificados x. 509 SSL pelo vai tooEdit -&gt; certificados SSL -&gt; importar certificados</span><span class="sxs-lookup"><span data-stu-id="10157-207">You can now add trusted Base-64 encoded X.509 SSL certificates by going tooEdit -&gt; SSL Certificates -&gt; Import Certificates</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-208">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-208">Fixes</span></span>

* <span data-ttu-id="10157-209">Correção: depois de atualizar as credenciais da conta, modo de exibição de árvore de saudação seria, às vezes, não atualizar automaticamente</span><span class="sxs-lookup"><span data-stu-id="10157-209">Fixed: after refreshing an account's credentials, hello tree view would sometimes not automatically refresh</span></span>
* <span data-ttu-id="10157-210">Corrigido: a geração de um SAS para tabelas e filas do emulador poderia resultar em uma URL inválida</span><span class="sxs-lookup"><span data-stu-id="10157-210">Fixed: generating a SAS for emulator queues and tables would result in an invalid URL</span></span>
* <span data-ttu-id="10157-211">Corrigido: agora, as contas de armazenamento Premium podem ser expandidas enquanto um proxy está habilitado</span><span class="sxs-lookup"><span data-stu-id="10157-211">Fixed: premium storage accounts can now be expanded while a proxy is enabled</span></span>
* <span data-ttu-id="10157-212">Correção: Olá botão Aplicar em contas Olá página de gerenciamento não funcionará se você tivesse 1 ou 0 contas selecionadas</span><span class="sxs-lookup"><span data-stu-id="10157-212">Fixed: hello apply button on hello accounts management page would not work if you had 1 or 0 accounts selected</span></span>
* <span data-ttu-id="10157-213">Corrigido: o carregamento de blobs que exigem resoluções de conflitos pode falhar – corrigido no 0.8.11</span><span class="sxs-lookup"><span data-stu-id="10157-213">Fixed: uploading blobs that require conflict resolutions may fail - fixed in 0.8.11</span></span> 
* <span data-ttu-id="10157-214">Corrigido: o envio de comentários foi interrompido no 0.8.11 – corrigido no 0.8.12</span><span class="sxs-lookup"><span data-stu-id="10157-214">Fixed: sending feedback was broken in 0.8.11 - fixed in 0.8.12</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="10157-215">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-215">Known Issues</span></span>

* <span data-ttu-id="10157-216">Após a atualização too0.8.10, será necessário toorefresh todas as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="10157-216">After upgrading too0.8.10, you will need toorefresh all of your credentials.</span></span>
* <span data-ttu-id="10157-217">Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello.</span><span class="sxs-lookup"><span data-stu-id="10157-217">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="10157-218">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros.</span><span class="sxs-lookup"><span data-stu-id="10157-218">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>
* <span data-ttu-id="10157-219">Painel de configurações de conta Olá pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter de ordem.</span><span class="sxs-lookup"><span data-stu-id="10157-219">hello account settings panel may show that you need tooreenter credentials in order toofilter subscriptions.</span></span>
* <span data-ttu-id="10157-220">Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="10157-220">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="10157-221">Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação.</span><span class="sxs-lookup"><span data-stu-id="10157-221">All other properties and metadata for blobs, files and entities are preserved during a rename.</span></span>
* <span data-ttu-id="10157-222">Embora o Azure Stack não dê suporte no momento a Compartilhamentos de Arquivos, um nó de Compartilhamentos de Arquivos ainda aparece em uma conta de armazenamento do Azure Stack anexada.</span><span class="sxs-lookup"><span data-stu-id="10157-222">Although Azure Stack doesn't currently support Files Shares, a File Shares node still appears under an attached Azure Stack storage account.</span></span> 
* <span data-ttu-id="10157-223">Ubuntu 14.04 instalação necessidades gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="10157-223">Ubuntu 14.04 install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span>

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a><span data-ttu-id="10157-224">Versão 0.8.9 / 0.8.8</span><span class="sxs-lookup"><span data-stu-id="10157-224">Version 0.8.9 / 0.8.8</span></span>
<span data-ttu-id="10157-225">02/23/2017</span><span class="sxs-lookup"><span data-stu-id="10157-225">02/23/2017</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="10157-226">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-226">New</span></span>

* <span data-ttu-id="10157-227">O Gerenciador de armazenamento 0.8.9 baixará automaticamente a versão mais recente Olá para atualizações.</span><span class="sxs-lookup"><span data-stu-id="10157-227">Storage Explorer 0.8.9 will automatically download hello latest version for updates.</span></span>
* <span data-ttu-id="10157-228">Hotfix: usando um portal gerado URI SAS tooattach que uma conta de armazenamento pode resultar em um erro.</span><span class="sxs-lookup"><span data-stu-id="10157-228">Hotfix: using a portal generated SAS URI tooattach a storage account would result in an error.</span></span>
* <span data-ttu-id="10157-229">Agora você pode criar, gerenciar e promover os instantâneos de blob.</span><span class="sxs-lookup"><span data-stu-id="10157-229">You can now create, manage, and promote blob snapshots.</span></span>
* <span data-ttu-id="10157-230">Agora você pode entrar em contas da China, o Azure Alemanha e o Azure US Government tooAzure.</span><span class="sxs-lookup"><span data-stu-id="10157-230">You can now sign in tooAzure China, Azure Germany, and Azure US Government accounts.</span></span>
* <span data-ttu-id="10157-231">Agora você pode alterar o nível de zoom de saudação.</span><span class="sxs-lookup"><span data-stu-id="10157-231">You can now change hello zoom level.</span></span> <span data-ttu-id="10157-232">Use as opções de Olá Olá Exibir menu tooZoom no zoom e redefinição de Zoom.</span><span class="sxs-lookup"><span data-stu-id="10157-232">Use hello options in hello View menu tooZoom In, Zoom Out, and Reset Zoom.</span></span>
* <span data-ttu-id="10157-233">Agora há suporte para caracteres Unicode nos metadados do usuário para blobs e arquivos.</span><span class="sxs-lookup"><span data-stu-id="10157-233">Unicode characters are now supported in user metadata for blobs and files.</span></span>
* <span data-ttu-id="10157-234">Aprimoramentos de acessibilidade.</span><span class="sxs-lookup"><span data-stu-id="10157-234">Accessibility improvements.</span></span>
* <span data-ttu-id="10157-235">Notas de versão do Hello próxima versão podem ser exibidas de notificação de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="10157-235">hello next version's release notes can be viewed from hello update notification.</span></span> <span data-ttu-id="10157-236">Você também pode exibir as notas de versão atuais Olá no menu de ajuda de saudação.</span><span class="sxs-lookup"><span data-stu-id="10157-236">You can also view hello current release notes from hello Help menu.</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-237">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-237">Fixes</span></span>

* <span data-ttu-id="10157-238">Correção: o número de versão Olá é agora exibido corretamente no painel de controle no Windows</span><span class="sxs-lookup"><span data-stu-id="10157-238">Fixed: hello version number is now correctly displayed in Control Panel on Windows</span></span>
* <span data-ttu-id="10157-239">Foram corrigidos: pesquisa não está mais limitado too50, nós 000</span><span class="sxs-lookup"><span data-stu-id="10157-239">Fixed: search is no longer limited too50,000 nodes</span></span>
* <span data-ttu-id="10157-240">Correção: compartilhamento de arquivos do carregamento tooa girado para sempre se o diretório de destino Olá ainda não existia</span><span class="sxs-lookup"><span data-stu-id="10157-240">Fixed: upload tooa file share spun forever if hello destination directory did not already exist</span></span>
* <span data-ttu-id="10157-241">Corrigido: mais estabilidade para downloads e uploads longos</span><span class="sxs-lookup"><span data-stu-id="10157-241">Fixed: improved stability for long uploads and downloads</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-242">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-242">Known Issues</span></span>

* <span data-ttu-id="10157-243">Enquanto aumentados in ou out, nível de zoom Olá momentaneamente pode redefinir o nível padrão de toohello.</span><span class="sxs-lookup"><span data-stu-id="10157-243">While zoomed in or out, hello zoom level may momentarily reset toohello default level.</span></span>
* <span data-ttu-id="10157-244">O Acesso Rápido só funciona com itens baseados em assinatura.</span><span class="sxs-lookup"><span data-stu-id="10157-244">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="10157-245">Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão.</span><span class="sxs-lookup"><span data-stu-id="10157-245">Local resources or resources attached via key or SAS token are not supported in this release.</span></span>
* <span data-ttu-id="10157-246">Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos que você tem.</span><span class="sxs-lookup"><span data-stu-id="10157-246">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have.</span></span>
* <span data-ttu-id="10157-247">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros.</span><span class="sxs-lookup"><span data-stu-id="10157-247">Having more than 3 groups of blobs or files uploading at hello same time may cause errors.</span></span>

<span data-ttu-id="10157-248">12/16/2016</span><span class="sxs-lookup"><span data-stu-id="10157-248">12/16/2016</span></span>
### <a name="version-087"></a><span data-ttu-id="10157-249">Versão 0.8.7</span><span class="sxs-lookup"><span data-stu-id="10157-249">Version 0.8.7</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="10157-250">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-250">New</span></span>

* <span data-ttu-id="10157-251">Você pode escolher como conflitos tooresolve no início de saudação de uma atualização, baixar ou copiar a sessão na janela de atividades de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-251">You can choose how tooresolve conflicts at hello beginning of an update, download or copy session in hello Activities window</span></span>
* <span data-ttu-id="10157-252">Passe o mouse sobre um caminho guia toosee Olá completo saudação do recurso de armazenamento</span><span class="sxs-lookup"><span data-stu-id="10157-252">Hover over a tab toosee hello full path of hello storage resource</span></span>
* <span data-ttu-id="10157-253">Quando você clica em uma guia, sincronizar com seu local no painel de navegação do lado esquerdo de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-253">When you click on a tab, it synchronizes with its location in hello left side navigation pane</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-254">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-254">Fixes</span></span>

* <span data-ttu-id="10157-255">Corrigido: agora, o Gerenciador de Armazenamento é um aplicativo confiável no Mac</span><span class="sxs-lookup"><span data-stu-id="10157-255">Fixed: Storage Explorer is now a trusted app on Mac</span></span>
* <span data-ttu-id="10157-256">Corrigido: o Ubuntu 14.04 tem suporte novamente</span><span class="sxs-lookup"><span data-stu-id="10157-256">Fixed: Ubuntu 14.04 is again supported</span></span>
* <span data-ttu-id="10157-257">Correção: Às vezes Olá adicionar conta pisca de interface do usuário durante o carregamento de assinaturas</span><span class="sxs-lookup"><span data-stu-id="10157-257">Fixed: Sometimes hello add account UI flashes when loading subscriptions</span></span>
* <span data-ttu-id="10157-258">Correção: Às vezes, nem todos os recursos de armazenamento foram listados no painel de navegação do lado esquerdo de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-258">Fixed: Sometimes not all storage resources were listed in hello left side navigation pane</span></span>
* <span data-ttu-id="10157-259">Correção: Olá ação painel, às vezes, exibido ações vazias</span><span class="sxs-lookup"><span data-stu-id="10157-259">Fixed: hello action pane sometimes displayed empty actions</span></span>
* <span data-ttu-id="10157-260">Correção: tamanho da janela Olá da sessão Olá fechado pela última vez é agora retido</span><span class="sxs-lookup"><span data-stu-id="10157-260">Fixed: hello window size from hello last closed session is now retained</span></span>
* <span data-ttu-id="10157-261">Correção: Você pode abrir várias guias para Olá mesmo recurso usando o menu de contexto de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-261">Fixed: You can open multiple tabs for hello same resource using hello context menu</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-262">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-262">Known Issues</span></span>

* <span data-ttu-id="10157-263">O Acesso Rápido só funciona com itens baseados em assinatura.</span><span class="sxs-lookup"><span data-stu-id="10157-263">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="10157-264">Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão</span><span class="sxs-lookup"><span data-stu-id="10157-264">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="10157-265">Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos</span><span class="sxs-lookup"><span data-stu-id="10157-265">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="10157-266">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros</span><span class="sxs-lookup"><span data-stu-id="10157-266">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="10157-267">Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado ou pode causar exceções sem tratamento</span><span class="sxs-lookup"><span data-stu-id="10157-267">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>
* <span data-ttu-id="10157-268">Para Olá pela primeira vez usando Olá Gerenciador de armazenamento em macOS, você verá vários prompts pedindo o conjunto de chaves de tooaccess de permissão do usuário.</span><span class="sxs-lookup"><span data-stu-id="10157-268">For hello first time using hello Storage Explorer on macOS, you might see multiple prompts asking for user's permission tooaccess keychain.</span></span> <span data-ttu-id="10157-269">Sugerimos que você selecionar sempre permitir modo prompt Olá não mostra novamente</span><span class="sxs-lookup"><span data-stu-id="10157-269">We suggest you select Always Allow so hello prompt won't show up again</span></span>

<span data-ttu-id="10157-270">11/18/2016</span><span class="sxs-lookup"><span data-stu-id="10157-270">11/18/2016</span></span>
### <a name="version-086"></a><span data-ttu-id="10157-271">Versão 0.8.6</span><span class="sxs-lookup"><span data-stu-id="10157-271">Version 0.8.6</span></span>

#### <a name="new"></a><span data-ttu-id="10157-272">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-272">New</span></span>

* <span data-ttu-id="10157-273">Você pode agora fixar usados com mais frequência serviços toohello acesso rápido para facilitar a navegação</span><span class="sxs-lookup"><span data-stu-id="10157-273">You can now pin most frequently used services toohello Quick Access for easy navigation</span></span>
* <span data-ttu-id="10157-274">Agora você pode abrir vários editores em guias diferentes.</span><span class="sxs-lookup"><span data-stu-id="10157-274">You can now open multiple editors in different tabs.</span></span> <span data-ttu-id="10157-275">Clique tooopen uma guia temporária; Clique duas vezes em tooopen uma guia permanente. Você também pode clicar em Olá guia temporário toomake-uma guia permanente</span><span class="sxs-lookup"><span data-stu-id="10157-275">Single click tooopen a temporary tab; double click tooopen a permanent tab. You can also click on hello temporary tab toomake it a permanent tab</span></span>
* <span data-ttu-id="10157-276">Fizemos aperfeiçoamentos de desempenho e estabilidade para carregamentos e downloads, especialmente para grandes arquivos em máquinas rápidas</span><span class="sxs-lookup"><span data-stu-id="10157-276">We have made noticeable performance and stability improvements for uploads and downloads, especially for large files on fast machines</span></span>
* <span data-ttu-id="10157-277">Pastas "virtuais" vazias agora podem ser criadas em contêineres de blob</span><span class="sxs-lookup"><span data-stu-id="10157-277">Empty "virtual" folders can now be created in blob containers</span></span>
* <span data-ttu-id="10157-278">Introduzimos novamente a pesquisa com escopo com nossa nova pesquisa avançada de subcadeia de caracteres, e agora você tem duas opções de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="10157-278">We have re-introduced scoped search with our new enhanced substring search, so you now have two options for searching:</span></span> 
    * <span data-ttu-id="10157-279">Global pesquisa - insira apenas um termo de pesquisa na caixa de texto de pesquisa de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-279">Global search - just enter a search term into hello search textbox</span></span>
    * <span data-ttu-id="10157-280">Pesquisa com escopo definido - clique Olá Lupa ícone próximo tooa nó, em seguida, adicionar um final de toohello do termo de pesquisa do caminho de hello, ou com o botão direito e selecione "Pesquisa de aqui"</span><span class="sxs-lookup"><span data-stu-id="10157-280">Scoped search - click hello magnifying glass icon next tooa node, then add a search term toohello end of hello path, or right-click and select "Search from Here"</span></span>
* <span data-ttu-id="10157-281">Adicionamos vários temas: luz (padrão), escuro, preto em alto contraste e branco em alto contraste.</span><span class="sxs-lookup"><span data-stu-id="10157-281">We have added various themes: Light (default), Dark, High Contrast Black, and High Contrast White.</span></span> <span data-ttu-id="10157-282">Vá tooEdit -&gt; toochange temas sua preferência de temas</span><span class="sxs-lookup"><span data-stu-id="10157-282">Go tooEdit -&gt; Themes toochange your theming preference</span></span>
* <span data-ttu-id="10157-283">Você pode modificar as propriedades do Blob e do arquivo</span><span class="sxs-lookup"><span data-stu-id="10157-283">You can modify Blob and file properties</span></span>
* <span data-ttu-id="10157-284">Agora, damos suporte mensagens em fila codificadas (base64) e não codificadas</span><span class="sxs-lookup"><span data-stu-id="10157-284">We now support encoded (base64) and unencoded queue messages</span></span>
* <span data-ttu-id="10157-285">No Linux, um sistema operacional de 64 bits agora é necessário.</span><span class="sxs-lookup"><span data-stu-id="10157-285">On Linux, a 64-bit OS is now required.</span></span> <span data-ttu-id="10157-286">Para esta versão, só há suporte para Ubuntu 16.04.1 LTS de 64 bits</span><span class="sxs-lookup"><span data-stu-id="10157-286">For this release we only support 64-bit Ubuntu 16.04.1 LTS</span></span>
* <span data-ttu-id="10157-287">Atualizamos nosso logotipo!</span><span class="sxs-lookup"><span data-stu-id="10157-287">We have updated our logo!</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-288">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-288">Fixes</span></span>

* <span data-ttu-id="10157-289">Corrigido: Tela problemas congelamento</span><span class="sxs-lookup"><span data-stu-id="10157-289">Fixed: Screen freezing problems</span></span>
* <span data-ttu-id="10157-290">Corrigido: Segurança aprimorada</span><span class="sxs-lookup"><span data-stu-id="10157-290">Fixed: Enhanced security</span></span>
* <span data-ttu-id="10157-291">Corrigido: às vezes, contas anexadas duplicadas apareciam</span><span class="sxs-lookup"><span data-stu-id="10157-291">Fixed: Sometimes duplicate attached accounts could appear</span></span>
* <span data-ttu-id="10157-292">Corrigido: um blob com um tipo de conteúdo indefinido pode gerar uma exceção</span><span class="sxs-lookup"><span data-stu-id="10157-292">Fixed: A blob with an undefined content type could generate an exception</span></span>
* <span data-ttu-id="10157-293">Correção: Olá abrindo o painel de consulta em uma tabela vazia não foi possível</span><span class="sxs-lookup"><span data-stu-id="10157-293">Fixed: Opening hello Query Panel on an empty table was not possible</span></span>
* <span data-ttu-id="10157-294">Corrigido: vários bugs na Pesquisa</span><span class="sxs-lookup"><span data-stu-id="10157-294">Fixed: Varies bugs in Search</span></span>
* <span data-ttu-id="10157-295">Correção: Maior número de saudação de recursos carregados do too100 50 quando clicar em "Mais carga"</span><span class="sxs-lookup"><span data-stu-id="10157-295">Fixed: Increased hello number of resources loaded from 50 too100 when clicking "Load More"</span></span>
* <span data-ttu-id="10157-296">Corrigido: agora, na primeira execução, se uma conta for conectada, selecionamos todas as assinaturas para essa conta por padrão</span><span class="sxs-lookup"><span data-stu-id="10157-296">Fixed: On first run, if an account is signed into, we now select all subscriptions for that account by default</span></span> 

#### <a name="known-issues"></a><span data-ttu-id="10157-297">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-297">Known Issues</span></span>

* <span data-ttu-id="10157-298">Esta versão do hello Gerenciador de armazenamento não é executado no Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="10157-298">This release of hello Storage Explorer does not run on Ubuntu 14.04</span></span>
* <span data-ttu-id="10157-299">tooopen várias guias para Olá mesmo recurso, não é continuamente clique em Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="10157-299">tooopen multiple tabs for hello same resource, do not continuously click on hello same resource.</span></span> <span data-ttu-id="10157-300">Clique em outro recurso e, em seguida, volte e clique no hello original recurso tooopen-lo novamente em outra guia</span><span class="sxs-lookup"><span data-stu-id="10157-300">Click on another resource and then go back and then click on hello original resource tooopen it again in another tab</span></span> 
* <span data-ttu-id="10157-301">O Acesso Rápido só funciona com itens baseados em assinatura.</span><span class="sxs-lookup"><span data-stu-id="10157-301">Quick Access only works with subscription based items.</span></span> <span data-ttu-id="10157-302">Recursos locais ou conectados por meio de chave ou o token SAS de recursos não têm suporte nesta versão</span><span class="sxs-lookup"><span data-stu-id="10157-302">Local resources or resources attached via key or SAS token are not supported in this release</span></span>
* <span data-ttu-id="10157-303">Acesso rápido pode levar alguns segundos toonavigate toohello recurso de destino, dependendo de quantos recursos</span><span class="sxs-lookup"><span data-stu-id="10157-303">It may take Quick Access a few seconds toonavigate toohello target resource, depending on how many resources you have</span></span>
* <span data-ttu-id="10157-304">Com mais de 3 grupos de blobs ou arquivos fazer upload de saudação mesmo tempo pode causar erros</span><span class="sxs-lookup"><span data-stu-id="10157-304">Having more than 3 groups of blobs or files uploading at hello same time may cause errors</span></span>
* <span data-ttu-id="10157-305">Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado ou pode causar exceções sem tratamento</span><span class="sxs-lookup"><span data-stu-id="10157-305">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted or may cause unhandled exception</span></span>

<span data-ttu-id="10157-306">10/03/2016</span><span class="sxs-lookup"><span data-stu-id="10157-306">10/03/2016</span></span>
### <a name="version-085"></a><span data-ttu-id="10157-307">Versão 0.8.5</span><span class="sxs-lookup"><span data-stu-id="10157-307">Version 0.8.5</span></span>

#### <a name="new"></a><span data-ttu-id="10157-308">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-308">New</span></span>

* <span data-ttu-id="10157-309">Pode agora usar SAS gerado pelo Portal chaves tooattach tooStorage contas e recursos</span><span class="sxs-lookup"><span data-stu-id="10157-309">Can now use Portal-generated SAS keys tooattach tooStorage Accounts and resources</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-310">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-310">Fixes</span></span>

* <span data-ttu-id="10157-311">Foram corrigidos: condição de corrida durante a pesquisa às vezes causado nós toobecome não expansível</span><span class="sxs-lookup"><span data-stu-id="10157-311">Fixed: race condition during search sometimes caused nodes toobecome non-expandable</span></span>
* <span data-ttu-id="10157-312">Correção: "Usar HTTP" não funciona ao conectar-se tooStorage contas com chave e o nome da conta</span><span class="sxs-lookup"><span data-stu-id="10157-312">Fixed: "Use HTTP" doesn't work when connecting tooStorage Accounts with account name and key</span></span>
* <span data-ttu-id="10157-313">Corrigido: chaves SAS (especialmente as geradas pelo Portal) retornam um erro de "barra à direita"</span><span class="sxs-lookup"><span data-stu-id="10157-313">Fixed: SAS keys (specially Portal-generated ones) return a "trailing slash" error</span></span>
* <span data-ttu-id="10157-314">Corrigido: problemas de importação de tabela</span><span class="sxs-lookup"><span data-stu-id="10157-314">Fixed: table import issues</span></span>
    * <span data-ttu-id="10157-315">Às vezes, a chave de partição e chave de linha eram invertidas</span><span class="sxs-lookup"><span data-stu-id="10157-315">Sometimes partition key and row key were reversed</span></span>
    * <span data-ttu-id="10157-316">Não é possível tooread "null" chaves de partição</span><span class="sxs-lookup"><span data-stu-id="10157-316">Unable tooread "null" Partition Keys</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-317">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-317">Known Issues</span></span>

* <span data-ttu-id="10157-318">Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado</span><span class="sxs-lookup"><span data-stu-id="10157-318">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>
* <span data-ttu-id="10157-319">Pilha do Azure atualmente não oferece suporte a arquivos, para que tentar tooexpand arquivos mostrará um erro</span><span class="sxs-lookup"><span data-stu-id="10157-319">Azure Stack doesn't currently support Files, so trying tooexpand Files will show an error</span></span>

<span data-ttu-id="10157-320">09/12/2016</span><span class="sxs-lookup"><span data-stu-id="10157-320">09/12/2016</span></span>
### <a name="version-084"></a><span data-ttu-id="10157-321">Versão 0.8.4</span><span class="sxs-lookup"><span data-stu-id="10157-321">Version 0.8.4</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="10157-322">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-322">New</span></span>

* <span data-ttu-id="10157-323">Gerar contas de toostorage links diretos, contêineres, filas, tabelas ou compartilhamentos de arquivos para compartilhamento e fácil acessam os recursos de tooyour - Windows e o suporte do Mac OS</span><span class="sxs-lookup"><span data-stu-id="10157-323">Generate direct links toostorage accounts, containers, queues, tables, or file shares for sharing and easy access tooyour resources - Windows and Mac OS support</span></span>
* <span data-ttu-id="10157-324">Pesquisar para contêineres de blob, tabelas, filas, compartilhamentos de arquivos ou contas de armazenamento de caixa de pesquisa Olá</span><span class="sxs-lookup"><span data-stu-id="10157-324">Search for your blob containers, tables, queues, file shares, or storage accounts from hello search box</span></span>
* <span data-ttu-id="10157-325">Agora você pode agrupar cláusulas no construtor de consultas de tabela Olá</span><span class="sxs-lookup"><span data-stu-id="10157-325">You can now group clauses in hello table query builder</span></span>
* <span data-ttu-id="10157-326">Renomear e copiar/colar contêineres de blob, compartilhamentos de arquivos, tabelas, blobs, pastas de blob, arquivos e diretórios de contas e contêineres anexadas a SAS</span><span class="sxs-lookup"><span data-stu-id="10157-326">Rename and copy/paste blob containers, file shares, tables, blobs, blob folders, files and directories from within SAS-attached accounts and containers</span></span>
* <span data-ttu-id="10157-327">Agora, ao renomear e copiar contêineres de blob e compartilhamentos de arquivos, as propriedades e metadados são preservados</span><span class="sxs-lookup"><span data-stu-id="10157-327">Renaming and copying blob containers and file shares now preserve properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-328">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-328">Fixes</span></span>

* <span data-ttu-id="10157-329">Corrigido: não é possível editar entidades de tabela se elas contiverem propriedades boolianas ou binárias</span><span class="sxs-lookup"><span data-stu-id="10157-329">Fixed: cannot edit table entities if they contain boolean or binary properties</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-330">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-330">Known Issues</span></span>

* <span data-ttu-id="10157-331">Identificadores de pesquisa pesquisar em nós aproximadamente 50.000 – depois disso, o desempenho pode ser afetado</span><span class="sxs-lookup"><span data-stu-id="10157-331">Search handles searching across roughly 50,000 nodes - after this, performance may be impacted</span></span>

<span data-ttu-id="10157-332">08/03/2016</span><span class="sxs-lookup"><span data-stu-id="10157-332">08/03/2016</span></span>
### <a name="version-083"></a><span data-ttu-id="10157-333">Versão 0.8.3</span><span class="sxs-lookup"><span data-stu-id="10157-333">Version 0.8.3</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="10157-334">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-334">New</span></span>

* <span data-ttu-id="10157-335">Renomear os contêineres, tabelas, compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="10157-335">Rename containers, tables, file shares</span></span>
* <span data-ttu-id="10157-336">Experiência aprimorada do Construtor de consulta</span><span class="sxs-lookup"><span data-stu-id="10157-336">Improved Query builder experience</span></span>
* <span data-ttu-id="10157-337">Consultas de toosave e carga de capacidade</span><span class="sxs-lookup"><span data-stu-id="10157-337">Ability toosave and load queries</span></span>
* <span data-ttu-id="10157-338">Direcionar links toostorage contas ou contêineres, filas, tabelas ou arquivos compartilhados para compartilhar e acessar facilmente os recursos (somente Windows - macOS suporte em breve!)</span><span class="sxs-lookup"><span data-stu-id="10157-338">Direct links toostorage accounts or containers, queues, tables, or file shares for sharing and easily accessing your resources (Windows-only - macOS support coming soon!)</span></span>
* <span data-ttu-id="10157-339">Capacidade toomanage e configure as regras CORS</span><span class="sxs-lookup"><span data-stu-id="10157-339">Ability toomanage and configure CORS rules</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-340">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-340">Fixes</span></span>

* <span data-ttu-id="10157-341">Corrigido: as Contas da Microsoft exigem reautenticação a cada 8 a 12 horas</span><span class="sxs-lookup"><span data-stu-id="10157-341">Fixed: Microsoft Accounts require re-authentication every 8-12 hours</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-342">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-342">Known Issues</span></span>

* <span data-ttu-id="10157-343">Às vezes, hello interface do usuário pode parecer congelada - maximizando a janela Olá ajuda a resolver esse problema</span><span class="sxs-lookup"><span data-stu-id="10157-343">Sometimes hello UI might appear frozen - maximizing hello window helps resolve this issue</span></span>
* <span data-ttu-id="10157-344">A instalação do macOS pode exigir permissões elevadas</span><span class="sxs-lookup"><span data-stu-id="10157-344">macOS install may require elevated permissions</span></span>
* <span data-ttu-id="10157-345">Painel de configurações de conta pode mostrar que você precisa ter credenciais de tooreenter em assinaturas de toofilter ordem</span><span class="sxs-lookup"><span data-stu-id="10157-345">Account settings panel may show that you need tooreenter credentials in order toofilter subscriptions</span></span>
* <span data-ttu-id="10157-346">Renomeação de compartilhamentos de arquivos, contêineres de blob e tabelas não preserva metadados ou outras propriedades no contêiner de saudação, como a cota de compartilhamento de arquivo, o nível de acesso público ou políticas de acesso</span><span class="sxs-lookup"><span data-stu-id="10157-346">Renaming file shares, blob containers, and tables does not preserve metadata or other properties on hello container, such as file share quota, public access level or access policies</span></span>
* <span data-ttu-id="10157-347">Renomear blobs (individualmente ou dentro de um contêiner de blob renomeado) não preserva os instantâneos.</span><span class="sxs-lookup"><span data-stu-id="10157-347">Renaming blobs (individually or inside a renamed blob container) does not preserve snapshots.</span></span> <span data-ttu-id="10157-348">Todas as outras propriedades e metadados de blobs, arquivos e entidades são preservadas durante uma renomeação</span><span class="sxs-lookup"><span data-stu-id="10157-348">All other properties and metadata for blobs, files and entities are preserved during a rename</span></span>
* <span data-ttu-id="10157-349">A cópia ou a renomeação de recursos não funciona em contas anexadas a SAS</span><span class="sxs-lookup"><span data-stu-id="10157-349">Copying or renaming resources does not work within SAS-attached accounts</span></span>

<span data-ttu-id="10157-350">07/07/2016</span><span class="sxs-lookup"><span data-stu-id="10157-350">07/07/2016</span></span>
### <a name="version-082"></a><span data-ttu-id="10157-351">Versão 0.8.2</span><span class="sxs-lookup"><span data-stu-id="10157-351">Version 0.8.2</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="10157-352">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-352">New</span></span>

* <span data-ttu-id="10157-353">As Contas de Armazenamento são agrupadas por assinaturas; armazenamento de desenvolvimento e recursos anexados via chave ou SAS são mostrados sob o nó (Local e Anexado)</span><span class="sxs-lookup"><span data-stu-id="10157-353">Storage Accounts are grouped by subscriptions; development storage and resources attached via key or SAS are shown under (Local and Attached) node</span></span>
* <span data-ttu-id="10157-354">Saia das contas no painel "Configurações de Conta do Azure"</span><span class="sxs-lookup"><span data-stu-id="10157-354">Sign off from accounts in "Azure Account Settings" panel</span></span>
* <span data-ttu-id="10157-355">Configurar tooenable de configurações de proxy e gerenciar entrar</span><span class="sxs-lookup"><span data-stu-id="10157-355">Configure proxy settings tooenable and manage sign-in</span></span>
* <span data-ttu-id="10157-356">Criar e quebrar concessões de blob</span><span class="sxs-lookup"><span data-stu-id="10157-356">Create and break blob leases</span></span>
* <span data-ttu-id="10157-357">Abrir contêineres de blob, filas, tabelas e arquivos com um único clique</span><span class="sxs-lookup"><span data-stu-id="10157-357">Open blob containers, queues, tables, and files with single-click</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-358">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-358">Fixes</span></span>

* <span data-ttu-id="10157-359">Corrigido: mensagens em fila inseridas com bibliotecas .NET ou Java não são corretamente decodificadas com base64</span><span class="sxs-lookup"><span data-stu-id="10157-359">Fixed: queue messages inserted with .NET or Java libraries are not properly decoded from base64</span></span>
* <span data-ttu-id="10157-360">Corrigido: tabelas $metrics não são exibidas para contas de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="10157-360">Fixed: $metrics tables are not shown for Blob Storage accounts</span></span>
* <span data-ttu-id="10157-361">Corrigido: o nó tabelas não funciona para o armazenamento local (Desenvolvimento)</span><span class="sxs-lookup"><span data-stu-id="10157-361">Fixed: tables node does not work for local (Development) storage</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-362">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-362">Known Issues</span></span>

* <span data-ttu-id="10157-363">A instalação do macOS pode exigir permissões elevadas</span><span class="sxs-lookup"><span data-stu-id="10157-363">macOS install may require elevated permissions</span></span>

<span data-ttu-id="10157-364">06/15/2016</span><span class="sxs-lookup"><span data-stu-id="10157-364">06/15/2016</span></span>
### <a name="version-080"></a><span data-ttu-id="10157-365">Versão 0.8.0</span><span class="sxs-lookup"><span data-stu-id="10157-365">Version 0.8.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a><span data-ttu-id="10157-366">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-366">New</span></span>

* <span data-ttu-id="10157-367">Suporte para compartilhamento de arquivos: exibição, upload, download, cópia de arquivos e diretórios, URIs SAS (criar e conectar)</span><span class="sxs-lookup"><span data-stu-id="10157-367">File share support: viewing, uploading, downloading, copying files and directories, SAS URIs (create and connect)</span></span>
* <span data-ttu-id="10157-368">Melhor experiência do usuário para conectar-se tooStorage com URIs de SAS ou chaves de conta</span><span class="sxs-lookup"><span data-stu-id="10157-368">Improved user experience for connecting tooStorage with SAS URIs or account keys</span></span>
* <span data-ttu-id="10157-369">Exportar resultados da consulta de tabela</span><span class="sxs-lookup"><span data-stu-id="10157-369">Export table query results</span></span>
* <span data-ttu-id="10157-370">Personalização e reordenação da coluna Tabela</span><span class="sxs-lookup"><span data-stu-id="10157-370">Table column reordering and customization</span></span>
* <span data-ttu-id="10157-371">Exibição de contêineres de blob $logs e tabelas $metrics para Contas de Armazenamento com métricas habilitadas</span><span class="sxs-lookup"><span data-stu-id="10157-371">Viewing $logs blob containers and $metrics tables for Storage Accounts with enabled metrics</span></span>
* <span data-ttu-id="10157-372">Comportamento de exportação e importação aprimorado, agora inclui o tipo de valor da propriedade</span><span class="sxs-lookup"><span data-stu-id="10157-372">Improved export and import behavior, now includes property value type</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-373">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-373">Fixes</span></span>

* <span data-ttu-id="10157-374">Corrigido: o upload ou download de blobs grandes pode resultar em uploads/downloads incompletos</span><span class="sxs-lookup"><span data-stu-id="10157-374">Fixed: uploading or downloading large blobs can result in incomplete uploads/downloads</span></span>
* <span data-ttu-id="10157-375">Correção: a edição, adicionando ou importando uma entidade com um valor de cadeia de caracteres numéricos ("1") converterá toodouble</span><span class="sxs-lookup"><span data-stu-id="10157-375">Fixed: editing, adding, or importing an entity with a numeric string value ("1") will convert it toodouble</span></span>
* <span data-ttu-id="10157-376">Correção: Nó de tabela Olá tooexpand não é possível no ambiente de desenvolvimento local Olá</span><span class="sxs-lookup"><span data-stu-id="10157-376">Fixed: Unable tooexpand hello table node in hello local development environment</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-377">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-377">Known Issues</span></span>

* <span data-ttu-id="10157-378">As tabelas $metrics não são visíveis para contas de Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="10157-378">$metrics tables are not visible for Blob Storage accounts</span></span>
* <span data-ttu-id="10157-379">Adicionado por meio de programação de fila de mensagens não pode ser exibida corretamente se mensagens de saudação são codificadas usando a codificação Base64</span><span class="sxs-lookup"><span data-stu-id="10157-379">Queue messages added programmatically may not be displayed correctly if hello messages are encoded using Base64 encoding</span></span>

<span data-ttu-id="10157-380">05/17/2016</span><span class="sxs-lookup"><span data-stu-id="10157-380">05/17/2016</span></span>
### <a name="version-07201605090"></a><span data-ttu-id="10157-381">Versão 0.7.20160509.0</span><span class="sxs-lookup"><span data-stu-id="10157-381">Version 0.7.20160509.0</span></span>

#### <a name="new"></a><span data-ttu-id="10157-382">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-382">New</span></span>

* <span data-ttu-id="10157-383">Melhor tratamento de erros para falhas de aplicativo</span><span class="sxs-lookup"><span data-stu-id="10157-383">Better error handling for app crashes</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-384">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-384">Fixes</span></span>

* <span data-ttu-id="10157-385">Correção de bug no qual as mensagens da Barra de Informações às vezes não apareciam quando as credenciais de entrada eram exigidas</span><span class="sxs-lookup"><span data-stu-id="10157-385">Fixed bug where InfoBar messages sometimes don't show up when sign-in credentials were required</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-386">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-386">Known Issues</span></span>

* <span data-ttu-id="10157-387">Tabelas: Adicionando, editando, ou importar uma entidade que tem uma propriedade com um valor numérico de maneira ambígua, como "1" ou "1.0", e Olá toosend de tentativas de usuário como um `Edm.String`, valor Olá voltará por meio do cliente Olá API como um EDM</span><span class="sxs-lookup"><span data-stu-id="10157-387">Tables: Adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>

<span data-ttu-id="10157-388">03/31/2016</span><span class="sxs-lookup"><span data-stu-id="10157-388">03/31/2016</span></span>

### <a name="version-07201603250"></a><span data-ttu-id="10157-389">Versão 0.7.20160325.0</span><span class="sxs-lookup"><span data-stu-id="10157-389">Version 0.7.20160325.0</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a><span data-ttu-id="10157-390">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-390">New</span></span>

* <span data-ttu-id="10157-391">Suporte à tabela: exibição, consulta, exportação, importação e operações CRUD para entidades</span><span class="sxs-lookup"><span data-stu-id="10157-391">Table support: viewing, querying, export, import, and CRUD operations for entities</span></span>
* <span data-ttu-id="10157-392">Suporte à fila: exibição, adição, remoção de mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="10157-392">Queue support: viewing, adding, dequeueing messages</span></span>
* <span data-ttu-id="10157-393">Gerar URIs SAS para Contas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="10157-393">Generating SAS URIs for Storage Accounts</span></span>
* <span data-ttu-id="10157-394">Conectando tooStorage contas com URIs de SAS</span><span class="sxs-lookup"><span data-stu-id="10157-394">Connecting tooStorage Accounts with SAS URIs</span></span>
* <span data-ttu-id="10157-395">Atualize notificações para atualizações futuras tooStorage Explorer</span><span class="sxs-lookup"><span data-stu-id="10157-395">Update notifications for future updates tooStorage Explorer</span></span>
* <span data-ttu-id="10157-396">Aparência atualizada</span><span class="sxs-lookup"><span data-stu-id="10157-396">Updated look and feel</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-397">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-397">Fixes</span></span>

* <span data-ttu-id="10157-398">Aprimoramento de desempenho e confiabilidade</span><span class="sxs-lookup"><span data-stu-id="10157-398">Performance and reliability improvements</span></span>

### <a name="known-issues-amp-mitigations"></a><span data-ttu-id="10157-399">Problemas &amp; mitigações conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-399">Known Issues &amp; Mitigations</span></span>

* <span data-ttu-id="10157-400">O download de arquivos de blob grandes não funciona corretamente – recomendamos usar AzCopy enquanto resolvemos esse problema</span><span class="sxs-lookup"><span data-stu-id="10157-400">Download of large blob files does not work correctly - we recommend using AzCopy while we address this issue</span></span> 
* <span data-ttu-id="10157-401">As credenciais de conta não serão recuperadas nem armazenadas em cache se a pasta base Olá não foi encontrada ou não pode ser gravada</span><span class="sxs-lookup"><span data-stu-id="10157-401">Account credentials will not be retrieved nor cached if hello home folder cannot be found or cannot be written to</span></span>
* <span data-ttu-id="10157-402">Se estamos adicionando, editando ou importando uma entidade que tem uma propriedade com um valor numérico de maneira ambígua, como "1" ou "1.0", e o usuário Olá tenta toosend-lo como um `Edm.String`, valor Olá voltará por meio do cliente Olá API como um EDM</span><span class="sxs-lookup"><span data-stu-id="10157-402">If we are adding, editing, or importing an entity that has a property with an ambiguously numeric value, such as "1" or "1.0", and hello user tries toosend it as an `Edm.String`, hello value will come back through hello client API as an Edm.Double</span></span>
* <span data-ttu-id="10157-403">Ao importar arquivos CSV com registros de várias linhas, os dados de saudação podem obter embaralhados ou embaralhados</span><span class="sxs-lookup"><span data-stu-id="10157-403">When importing CSV files with multiline records, hello data may get chopped or scrambled</span></span>

<span data-ttu-id="10157-404">02/03/2016</span><span class="sxs-lookup"><span data-stu-id="10157-404">02/03/2016</span></span>

### <a name="version-07201601291"></a><span data-ttu-id="10157-405">Versão 0.7.20160129.1</span><span class="sxs-lookup"><span data-stu-id="10157-405">Version 0.7.20160129.1</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-406">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-406">Fixes</span></span>

* <span data-ttu-id="10157-407">Desempenho geral aprimorado ao carregar, baixar e copiar blobs</span><span class="sxs-lookup"><span data-stu-id="10157-407">Improved overall performance when uploading, downloading and copying blobs</span></span>

<span data-ttu-id="10157-408">01/14/2016</span><span class="sxs-lookup"><span data-stu-id="10157-408">01/14/2016</span></span>

### <a name="version-07201601050"></a><span data-ttu-id="10157-409">Versão 0.7.20160105.0</span><span class="sxs-lookup"><span data-stu-id="10157-409">Version 0.7.20160105.0</span></span>

#### <a name="new"></a><span data-ttu-id="10157-410">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-410">New</span></span>

* <span data-ttu-id="10157-411">Suporte a Linux (paridade recursos tooOSX)</span><span class="sxs-lookup"><span data-stu-id="10157-411">Linux support (parity features tooOSX)</span></span>
* <span data-ttu-id="10157-412">Adicionar contêineres de blob com chave SAS (Assinaturas de Acesso Compartilhado)</span><span class="sxs-lookup"><span data-stu-id="10157-412">Add blob containers with Shared Access Signatures (SAS) key</span></span>
* <span data-ttu-id="10157-413">Adicionar Contas de Armazenamento para o Azure China</span><span class="sxs-lookup"><span data-stu-id="10157-413">Add Storage Accounts for Azure China</span></span>
* <span data-ttu-id="10157-414">Adicionar Contas de Armazenamento com pontos de extremidade personalizados</span><span class="sxs-lookup"><span data-stu-id="10157-414">Add Storage Accounts with custom endpoints</span></span>
* <span data-ttu-id="10157-415">Abrir e exibir os blobs de texto e imagem de conteúdo Olá</span><span class="sxs-lookup"><span data-stu-id="10157-415">Open and view hello contents text and picture blobs</span></span>
* <span data-ttu-id="10157-416">Exibir e editar propriedades e metadados de blob</span><span class="sxs-lookup"><span data-stu-id="10157-416">View and edit blob properties and metadata</span></span>

#### <a name="fixes"></a><span data-ttu-id="10157-417">Correções</span><span class="sxs-lookup"><span data-stu-id="10157-417">Fixes</span></span>

* <span data-ttu-id="10157-418">Foram corrigidos: carregar ou baixar um grande número de blobs (500) pode às vezes causar Olá aplicativo toohave uma tela em branca</span><span class="sxs-lookup"><span data-stu-id="10157-418">Fixed: uploading or download a large number of blobs (500+) may sometimes cause hello app toohave a white screen</span></span> 
* <span data-ttu-id="10157-419">Correção: ao definir o nível de acesso público de contêiner de blob, Olá novo valor não é atualizado até que você defina o foco Olá no contêiner Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="10157-419">Fixed: when setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container.</span></span> <span data-ttu-id="10157-420">Além disso, caixa de diálogo Olá sempre padroniza muito "não acessar nenhum public" e não Olá atual valor real.</span><span class="sxs-lookup"><span data-stu-id="10157-420">Also, hello dialog always defaults too"No public access", and not hello actual current value.</span></span>
* <span data-ttu-id="10157-421">Suporte geral aprimorado de teclado/acessibilidade e interface do usuário</span><span class="sxs-lookup"><span data-stu-id="10157-421">Better overall keyboard/accessibility and UI support</span></span>
* <span data-ttu-id="10157-422">A disposição do texto do histórico de trilha quebra automaticamente quando o texto é longo com espaços em branco</span><span class="sxs-lookup"><span data-stu-id="10157-422">Breadcrumbs history text wraps when it's long with white space</span></span>
* <span data-ttu-id="10157-423">A caixa de diálogo SAS dá suporte à validação de entrada</span><span class="sxs-lookup"><span data-stu-id="10157-423">SAS dialog supports input validation</span></span>
* <span data-ttu-id="10157-424">Armazenamento local continua toobe disponível mesmo se as credenciais do usuário tem expirado</span><span class="sxs-lookup"><span data-stu-id="10157-424">Local storage continues toobe available even if user credentials have expired</span></span>
* <span data-ttu-id="10157-425">Quando um contêiner de blob aberto é excluído, explorer de blob Olá Olá direita é fechado</span><span class="sxs-lookup"><span data-stu-id="10157-425">When an opened blob container is deleted, hello blob explorer on hello right side is closed</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-426">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-426">Known Issues</span></span>

* <span data-ttu-id="10157-427">Necessidades de instalação Linux gcc versão atualizada ou atualizado – tooupgrade etapas estão abaixo:</span><span class="sxs-lookup"><span data-stu-id="10157-427">Linux install needs gcc version updated or upgraded – steps tooupgrade are below:</span></span> 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

<span data-ttu-id="10157-428">11/18/2015</span><span class="sxs-lookup"><span data-stu-id="10157-428">11/18/2015</span></span>
### <a name="version-07201511160"></a><span data-ttu-id="10157-429">Versão 0.7.20151116.0</span><span class="sxs-lookup"><span data-stu-id="10157-429">Version 0.7.20151116.0</span></span>

#### <a name="new"></a><span data-ttu-id="10157-430">Novo</span><span class="sxs-lookup"><span data-stu-id="10157-430">New</span></span>

* <span data-ttu-id="10157-431">Versões para macOS e Windows</span><span class="sxs-lookup"><span data-stu-id="10157-431">macOS, and Windows versions</span></span>
* <span data-ttu-id="10157-432">Entrar tooview suas contas de armazenamento – use sua conta institucional Microsoft Account, 2FA, etc.</span><span class="sxs-lookup"><span data-stu-id="10157-432">Sign in tooview your Storage Accounts – use your Org Account, Microsoft Account, 2FA, etc.</span></span>
* <span data-ttu-id="10157-433">Armazenamento de desenvolvimento local (use o emulador de armazenamento, somente para Windows)</span><span class="sxs-lookup"><span data-stu-id="10157-433">Local development storage (use storage emulator, Windows-only)</span></span>
* <span data-ttu-id="10157-434">Suporte ao Azure Resource Manager e ao recurso Clássico</span><span class="sxs-lookup"><span data-stu-id="10157-434">Azure Resource Manager and Classic resource support</span></span>
* <span data-ttu-id="10157-435">Criar e excluir blobs, filas ou tabelas</span><span class="sxs-lookup"><span data-stu-id="10157-435">Create and delete blobs, queues, or tables</span></span>
* <span data-ttu-id="10157-436">Procurar blobs, filas ou tabelas específicas</span><span class="sxs-lookup"><span data-stu-id="10157-436">Search for specific blobs, queues, or tables</span></span>
* <span data-ttu-id="10157-437">Explore o conteúdo de saudação de contêineres de blob</span><span class="sxs-lookup"><span data-stu-id="10157-437">Explore hello contents of blob containers</span></span>
* <span data-ttu-id="10157-438">Exibir e navegar pelos diretórios</span><span class="sxs-lookup"><span data-stu-id="10157-438">View and navigate through directories</span></span>
* <span data-ttu-id="10157-439">Carregar, baixar e excluir blobs e pastas</span><span class="sxs-lookup"><span data-stu-id="10157-439">Upload, download, and delete blobs and folders</span></span>
* <span data-ttu-id="10157-440">Exibir e editar propriedades e metadados de blob</span><span class="sxs-lookup"><span data-stu-id="10157-440">View and edit blob properties and metadata</span></span>
* <span data-ttu-id="10157-441">Gerar as chaves SAS</span><span class="sxs-lookup"><span data-stu-id="10157-441">Generate SAS keys</span></span>
* <span data-ttu-id="10157-442">Gerenciar e criar SAP (Políticas de Acesso armazenado)</span><span class="sxs-lookup"><span data-stu-id="10157-442">Manage and create Stored Access Policies (SAP)</span></span>
* <span data-ttu-id="10157-443">Procure blobs pelo prefixo</span><span class="sxs-lookup"><span data-stu-id="10157-443">Search for blobs by prefix</span></span>
* <span data-ttu-id="10157-444">Arraste ' drop n tooupload de arquivos ou de download</span><span class="sxs-lookup"><span data-stu-id="10157-444">Drag 'n drop files tooupload or download</span></span>

#### <a name="known-issues"></a><span data-ttu-id="10157-445">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="10157-445">Known Issues</span></span>

* <span data-ttu-id="10157-446">Ao definir o nível de acesso público de contêiner de blob, valor novo Olá não é atualizado até que você defina o foco Olá no contêiner Olá novamente</span><span class="sxs-lookup"><span data-stu-id="10157-446">When setting blob container public access level, hello new value is not updated until you re-set hello focus on hello container</span></span>
* <span data-ttu-id="10157-447">Quando você abre o nível de acesso público do hello diálogo tooset Olá, ele sempre não mostra "Nenhum acesso público" como Olá, valor padrão e não Olá real atual</span><span class="sxs-lookup"><span data-stu-id="10157-447">When you open hello dialog tooset hello public access level, it always shows "No public access" as hello default, and not hello actual current value</span></span>
* <span data-ttu-id="10157-448">Não é possível renomear blobs baixados</span><span class="sxs-lookup"><span data-stu-id="10157-448">Cannot rename downloaded blobs</span></span>
* <span data-ttu-id="10157-449">Estado de entradas de log de atividade será às vezes "preso" em uma em andamento quando ocorre um erro e erro Olá não é exibido</span><span class="sxs-lookup"><span data-stu-id="10157-449">Activity log entries will sometimes get "stuck" in an in progress state when an error occurs, and hello error is not displayed</span></span>
* <span data-ttu-id="10157-450">Às vezes, falhas ou ativa completamente durante a tentativa de tooupload em branco ou baixar um grande número de blobs</span><span class="sxs-lookup"><span data-stu-id="10157-450">Sometimes crashes or turns completely white when trying tooupload or download a large number of blobs</span></span>
* <span data-ttu-id="10157-451">Às vezes, cancelar uma operação de cópia não funciona</span><span class="sxs-lookup"><span data-stu-id="10157-451">Sometimes canceling a copy operation does not work</span></span>
* <span data-ttu-id="10157-452">Durante a criação de um contêiner (tabela/fila/blob), se um nome inválido de entrada e continuar toocreate outro em um tipo de contêiner diferentes você não pode definir foco no novo tipo de saudação</span><span class="sxs-lookup"><span data-stu-id="10157-452">During creating a container (blob/queue/table), if you input an invalid name and proceed toocreate another under a different container type you cannot set focus on hello new type</span></span>
* <span data-ttu-id="10157-453">Não é possível criar uma nova pasta ou renomear a pasta</span><span class="sxs-lookup"><span data-stu-id="10157-453">Can't create new folder or rename folder</span></span>




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md