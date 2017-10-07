---
title: "aaaGet iniciado com o Gerenciador de armazenamento (visualização) | Microsoft Docs"
description: "Gerenciar os recursos de armazenamento do Azure com o Gerenciador de Armazenamento (Visualização)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="e3c58-103">Introdução ao Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="e3c58-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="e3c58-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e3c58-104">Overview</span></span>
<span data-ttu-id="e3c58-105">Gerenciador de armazenamento do Azure (visualização) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="e3c58-105">Azure Storage Explorer (Preview) is a standalone app that enables you tooeasily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="e3c58-106">Neste artigo, você aprenderá Olá várias maneiras de se conectar tooand gerenciar suas contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-106">In this article, you learn hello various ways of connecting tooand managing your Azure storage accounts.</span></span>

![Gerenciador de Armazenamento do Microsoft Azure (Preview)][15]

## <a name="prerequisites"></a><span data-ttu-id="e3c58-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3c58-108">Prerequisites</span></span>
* [<span data-ttu-id="e3c58-109">Baixe e instale o Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="e3c58-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a><span data-ttu-id="e3c58-110">Conecte-se a conta de armazenamento tooa ou serviço</span><span class="sxs-lookup"><span data-stu-id="e3c58-110">Connect tooa storage account or service</span></span>
<span data-ttu-id="e3c58-111">O Gerenciador de armazenamento (visualização) fornece várias maneiras tooconnect toostorage contas.</span><span class="sxs-lookup"><span data-stu-id="e3c58-111">Storage Explorer (Preview) provides several ways tooconnect toostorage accounts.</span></span> <span data-ttu-id="e3c58-112">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="e3c58-112">For example, you can:</span></span>
* <span data-ttu-id="e3c58-113">Conecte-se toostorage contas associadas às suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-113">Connect toostorage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="e3c58-114">Conecte-se toostorage contas e serviços compartilhados de outras assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-114">Connect toostorage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="e3c58-115">Conecte-se tooand gerenciar armazenamento local usando Olá emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-115">Connect tooand manage local storage by using hello Azure Storage Emulator.</span></span> 

<span data-ttu-id="e3c58-116">Além disso, você pode trabalhar com contas nacionais e internacionais de armazenamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="e3c58-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="e3c58-117">[Conectar-se a assinatura do Azure do tooan](#connect-to-an-azure-subscription): gerenciar recursos de armazenamento que pertencem a tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-117">[Connect tooan Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong tooyour Azure subscription.</span></span>
* <span data-ttu-id="e3c58-118">[Trabalhar com o armazenamento de desenvolvimento local](#work-with-local-development-storage): gerenciar o armazenamento local usando Olá emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using hello Azure Storage Emulator.</span></span>
* <span data-ttu-id="e3c58-119">[Anexar armazenamento tooexternal](#attach-or-detach-an-external-storage-account): gerenciar recursos de armazenamento que pertencem a tooanother assinatura do Azure ou que estão sob national nuvens do Azure usando o nome da conta de armazenamento hello, chave e pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e3c58-119">[Attach tooexternal storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong tooanother Azure subscription or that are under national Azure clouds by using hello storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="e3c58-120">[Anexar uma conta de armazenamento usando uma SAS](#attach-storage-account-using-sas): gerenciar recursos de armazenamento que pertencem tooanother assinatura do Azure usando uma assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="e3c58-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong tooanother Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="e3c58-121">[Anexe um serviço usando uma SAS](#attach-service-using-sas): gerenciar um serviço de armazenamento específico (contêiner de blob, fila ou tabela) que pertence a tooanother assinatura do Azure usando uma SAS.</span><span class="sxs-lookup"><span data-stu-id="e3c58-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs tooanother Azure subscription by using an SAS.</span></span>

## <a name="connect-tooan-azure-subscription"></a><span data-ttu-id="e3c58-122">Conecte-se tooan assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="e3c58-122">Connect tooan Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="e3c58-123">Se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e3c58-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="e3c58-124">No Gerenciador de Armazenamento (Visualização), selecione **Configurações de conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Configurações de conta do Azure][0]

2. <span data-ttu-id="e3c58-126">painel esquerdo Olá exibe todas as contas da Microsoft hello em que você entrou.</span><span class="sxs-lookup"><span data-stu-id="e3c58-126">hello left pane displays all hello Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="e3c58-127">conta de tooanother tooconnect, selecione **adicionar uma conta**e, em seguida, siga Olá instruções toosign com uma conta da Microsoft que está associada a pelo menos uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-127">tooconnect tooanother account, select **Add an account**, and then follow hello instructions toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e3c58-128">Conectar toonational Azure (como o Azure Alemanha, governo do Azure e do Azure na China por meio de entrada) não é suportado atualmente.</span><span class="sxs-lookup"><span data-stu-id="e3c58-128">Connecting toonational Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="e3c58-129">Consulte hello "anexar ou desanexar uma conta de armazenamento externo" seção para saber como contas de armazenamento do Azure toonational tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e3c58-129">See hello "Attach or detach an external storage account" section for how tooconnect toonational Azure storage accounts.</span></span>

3. <span data-ttu-id="e3c58-130">Depois que você entrar com êxito com uma conta da Microsoft, Olá esquerda painel é populado com hello assinaturas do Azure associadas a essa conta.</span><span class="sxs-lookup"><span data-stu-id="e3c58-130">After you successfully sign in with a Microsoft account, hello left pane is populated with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="e3c58-131">Selecione Olá assinaturas do Azure que você deseja toowork com e, em seguida, selecione **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-131">Select hello Azure subscriptions that you want toowork with, and then select **Apply**.</span></span> <span data-ttu-id="e3c58-132">(Selecionar **todas as assinaturas** alterna selecionando todos ou nenhum Olá listados assinaturas do Azure.)</span><span class="sxs-lookup"><span data-stu-id="e3c58-132">(Selecting **All subscriptions** toggles selecting all or none of hello listed Azure subscriptions.)</span></span>

    ![Selecionar assinaturas do Azure][3]  
    <span data-ttu-id="e3c58-134">painel esquerdo Olá exibe as contas de armazenamento Olá associadas a assinaturas do Azure Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="e3c58-134">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>

    ![Assinaturas do Azure selecionadas][4]

## <a name="connect-tooan-azure-stack-subscription"></a><span data-ttu-id="e3c58-136">Conecte-se a assinatura do Azure pilha tooan</span><span class="sxs-lookup"><span data-stu-id="e3c58-136">Connect tooan Azure Stack subscription</span></span>

<span data-ttu-id="e3c58-137">Para obter informações sobre assinatura de pilha do Azure tooan conexão, consulte [conectar o Gerenciador de armazenamento tooan assinatura do Azure pilha](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="e3c58-137">For information about connecting tooan Azure Stack subscription, see [Connect Storage Explorer tooan Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="e3c58-138">Trabalhar com o armazenamento de desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="e3c58-138">Work with local development storage</span></span>
<span data-ttu-id="e3c58-139">Com o Gerenciador de armazenamento (visualização), você pode trabalhar no armazenamento local usando Olá emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-139">With Storage Explorer (Preview), you can work against local storage by using hello Azure Storage Emulator.</span></span> <span data-ttu-id="e3c58-140">Essa abordagem permite que você escreva o código e teste de armazenamento sem necessariamente ter uma conta de armazenamento implantada no Azure, porque a conta de armazenamento hello está sendo emulada pelo Olá emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because hello storage account is being emulated by hello Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="e3c58-141">Olá emulador de armazenamento do Azure é suportada atualmente apenas para Windows.</span><span class="sxs-lookup"><span data-stu-id="e3c58-141">hello Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="e3c58-142">No painel esquerdo de saudação do Gerenciador de armazenamento (visualização), expanda Olá **(Local e conectado)** > **contas de armazenamento** > **(desenvolvimento)** nó.</span><span class="sxs-lookup"><span data-stu-id="e3c58-142">In hello left pane of Storage Explorer (Preview), expand hello **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nó de desenvolvimento local][21]

2. <span data-ttu-id="e3c58-144">Se você ainda não tiver instalado Olá emulador de armazenamento do Azure, é solicitada toodo caso por meio de uma barra de informações.</span><span class="sxs-lookup"><span data-stu-id="e3c58-144">If you have not yet installed hello Azure Storage Emulator, you are prompted toodo so via an infobar.</span></span> <span data-ttu-id="e3c58-145">Se a barra de informações Olá for exibida, selecione **Baixe a versão mais recente Olá**e, em seguida, instale o emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3c58-145">If hello infobar is displayed, select **Download hello latest version**, and then install hello emulator.</span></span>

    ![Baixar o prompt do Emulador de Armazenamento do Azure][22]

3. <span data-ttu-id="e3c58-147">Depois de instalar o emulador hello, você pode criar e trabalhar com locais blobs, filas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="e3c58-147">After hello emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="e3c58-148">toolearn como tipo toowork com cada conta de armazenamento, consulte um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e3c58-148">toolearn how toowork with each storage account type, see one of hello following:</span></span>

    * [<span data-ttu-id="e3c58-149">Gerenciar recursos de Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="e3c58-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="e3c58-150">Gerenciar recursos de armazenamento de compartilhamento de arquivos do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="e3c58-151">Gerenciar recursos de armazenamento de filas do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="e3c58-152">Gerenciar recursos de armazenamento de tabelas do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="e3c58-153">Conexão ou desconexão de uma conta de armazenamento externo</span><span class="sxs-lookup"><span data-stu-id="e3c58-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="e3c58-154">Com o Gerenciador de armazenamento (visualização), você pode anexar tooexternal contas de armazenamento para que as contas de armazenamento podem ser facilmente compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="e3c58-154">With Storage Explorer (Preview), you can attach tooexternal storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="e3c58-155">Esta seção explica como tooattach too(and detach from) contas de armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="e3c58-155">This section explains how tooattach too(and detach from) external storage accounts.</span></span>

### <a name="get-hello-storage-account-credentials"></a><span data-ttu-id="e3c58-156">Obter credenciais de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="e3c58-156">Get hello storage account credentials</span></span>
<span data-ttu-id="e3c58-157">tooshare uma conta de armazenamento externo, o proprietário de saudação dessa conta deve primeiro obter credenciais de saudação (nome da conta e chave) para a conta de saudação e, em seguida, compartilhar essas informações com hello quem quer tooattach toothat (externos) conta.</span><span class="sxs-lookup"><span data-stu-id="e3c58-157">tooshare an external storage account, hello owner of that account must first get hello credentials (account name and key) for hello account and then share that information with hello person who wants tooattach toothat (external) account.</span></span> <span data-ttu-id="e3c58-158">Você pode obter credenciais de conta de armazenamento Olá via Olá portal do Azure fazendo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="e3c58-158">You can obtain hello storage account credentials via hello Azure portal by doing hello following:</span></span>

1. <span data-ttu-id="e3c58-159">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e3c58-159">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e3c58-160">Selecione **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-160">Select **Browse**.</span></span>

3. <span data-ttu-id="e3c58-161">Selecione **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="e3c58-162">Em Olá **contas de armazenamento** folha, selecione Olá desejado conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3c58-162">On hello **Storage Accounts** blade, select hello desired storage account.</span></span>

5. <span data-ttu-id="e3c58-163">Em Olá **configurações** folha para Olá selecionada a conta de armazenamento, selecione **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-163">On hello **Settings** blade for hello selected storage account, select **Access keys**.</span></span>

    ![Opção Chaves de Acesso][5]

6. <span data-ttu-id="e3c58-165">Em Olá **chaves de acesso** folha, Olá cópia **nome da conta de armazenamento** e **key1** valores para uso ao anexar toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3c58-165">On hello **Access keys** blade, copy hello **Storage account name** and **key1** values for use when attaching toohello storage account.</span></span>

    ![Chaves de acesso][6]

### <a name="attach-tooan-external-storage-account"></a><span data-ttu-id="e3c58-167">Anexar a conta de armazenamento externo de tooan</span><span class="sxs-lookup"><span data-stu-id="e3c58-167">Attach tooan external storage account</span></span>
<span data-ttu-id="e3c58-168">conta de armazenamento externo de tooan tooattach, é necessário nome e a chave da conta hello.</span><span class="sxs-lookup"><span data-stu-id="e3c58-168">tooattach tooan external storage account, you need hello account's name and key.</span></span> <span data-ttu-id="e3c58-169">Olá "Credenciais de conta de armazenamento do Get hello" seção explica como tooobtain esses valores de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-169">hello "Get hello storage account credentials" section explains how tooobtain these values from hello Azure portal.</span></span> <span data-ttu-id="e3c58-170">No entanto, no portal de Olá Olá conta chave é chamada de **key1**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-170">However, in hello portal, hello account key is called **key1**.</span></span> <span data-ttu-id="e3c58-171">Portanto em que o Gerenciador de armazenamento (visualização) solicita uma chave de conta, digite Olá **key1** valor.</span><span class="sxs-lookup"><span data-stu-id="e3c58-171">So where Storage Explorer (Preview) asks for an account key, you enter hello **key1** value.</span></span>

1. <span data-ttu-id="e3c58-172">No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-172">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. <span data-ttu-id="e3c58-174">Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique a chave de conta hello (Olá **key1** valor da saudação portal do Azure) e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-174">In hello **Connect tooAzure Storage** dialog box, specify hello account key (hello **key1** value from hello Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3c58-175">Você pode inserir a cadeia de caracteres de conexão de armazenamento Olá de uma conta de armazenamento no Azure nacional.</span><span class="sxs-lookup"><span data-stu-id="e3c58-175">You can enter hello storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="e3c58-176">Por exemplo, contas de armazenamento do tooconnect tooAzure Alemanha, insira o seguinte de toohello conexão cadeias de caracteres semelhante:</span><span class="sxs-lookup"><span data-stu-id="e3c58-176">For example, tooconnect tooAzure Germany storage accounts, enter connection strings similar toohello following:</span></span> 
    >
    >* <span data-ttu-id="e3c58-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="e3c58-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="e3c58-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="e3c58-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="e3c58-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="e3c58-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="e3c58-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="e3c58-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="e3c58-181">Você pode obter a cadeia de caracteres de conexão de saudação do hello Azure portal em Olá mesmo maneira conforme descrito em Olá seção "Obter credenciais de conta de armazenamento Olá".</span><span class="sxs-lookup"><span data-stu-id="e3c58-181">You can get hello connection string from hello Azure portal in hello same way as described in hello "Get hello storage account credentials" section.</span></span>

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. <span data-ttu-id="e3c58-183">Em Olá **anexar armazenamento externo** caixa de diálogo Olá **nome da conta** caixa, digite o nome de conta de armazenamento hello, especifique outras configurações desejadas e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-183">In hello **Attach External Storage** dialog box, in hello **Account name** box, enter hello storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Caixa de diálogo Anexar Armazenamento Externo][8]

4. <span data-ttu-id="e3c58-185">Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3c58-185">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="e3c58-186">Se você desejar toochange qualquer coisa, selecione **novamente** e redigitar as definições de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="e3c58-186">If you want toochange anything, select **Back** and reenter hello desired settings.</span></span> 

5. <span data-ttu-id="e3c58-187">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-187">Select **Connect**.</span></span>

6. <span data-ttu-id="e3c58-188">Depois que ele está conectado com êxito, a conta de armazenamento externo de saudação é exibida com **(externo)** acrescentado toohello nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3c58-188">After it is successfully connected, hello external storage account is displayed with **(External)** appended toohello storage account name.</span></span>

    ![Resultado de conectar-se a conta de armazenamento externo de tooan][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="e3c58-190">Desconexão de uma conta de armazenamento externo</span><span class="sxs-lookup"><span data-stu-id="e3c58-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="e3c58-191">Clique em Olá conta de armazenamento externo que você deseja toodetach e, em seguida, selecione **desanexar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-191">Right-click hello external storage account that you want toodetach, and then select **Detach**.</span></span>

    ![Opção Desanexar do armazenamento][10]

2. <span data-ttu-id="e3c58-193">Na mensagem de confirmação de saudação, selecione **Sim** tooconfirm desconexão de saudação da conta de armazenamento externo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3c58-193">In hello confirmation message, select **Yes** tooconfirm hello detachment from hello external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="e3c58-194">Como anexar uma conta de armazenamento usando uma SAS</span><span class="sxs-lookup"><span data-stu-id="e3c58-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="e3c58-195">Um [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite Olá administrador de uma assinatura do Azure conceder a conta de armazenamento temporário acesso tooa sem ter que tooprovide credenciais de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3c58-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets hello admin of an Azure subscription grant temporary access tooa storage account without having tooprovide Azure subscription credentials.</span></span>

<span data-ttu-id="e3c58-196">tooillustrate neste cenário, vamos dizer que UserA é um administrador de uma assinatura do Azure e UserA quer tooallow UserB tooaccess conta de armazenamento por um período limitado com determinadas permissões:</span><span class="sxs-lookup"><span data-stu-id="e3c58-196">tooillustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants tooallow UserB tooaccess a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="e3c58-197">UserA gera uma SAS (consistindo de cadeia de caracteres de conexão de Olá Olá conta de armazenamento) para um momento específico período e com permissões de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="e3c58-197">UserA generates an SAS (consisting of hello connection string for hello storage account) for a specific time period and with hello desired permissions.</span></span>

2. <span data-ttu-id="e3c58-198">Compartilhamentos de UserA Olá SAS com pessoa de saudação (UserB, em nosso exemplo) que deseja conta de armazenamento toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3c58-198">UserA shares hello SAS with hello person (UserB, in our example) who wants access toohello storage account.</span></span>  

3. <span data-ttu-id="e3c58-199">UserB usa a conta de toohello de tooattach do Gerenciador de armazenamento (visualização) que pertence a tooUserA usando Olá fornecido SAS.</span><span class="sxs-lookup"><span data-stu-id="e3c58-199">UserB uses Storage Explorer (Preview) tooattach toohello account that belongs tooUserA by using hello supplied SAS.</span></span>

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a><span data-ttu-id="e3c58-200">Obter um SAS para a conta de saudação desejado tooshare</span><span class="sxs-lookup"><span data-stu-id="e3c58-200">Get an SAS for hello account you want tooshare</span></span>
1. <span data-ttu-id="e3c58-201">No Gerenciador de armazenamento (visualização), clique na conta de armazenamento Olá você deseja compartilhar e, em seguida, selecione **obter assinatura de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-201">In Storage Explorer (Preview), right-click hello storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opção do menu de contexto Obter SAS][13]

2. <span data-ttu-id="e3c58-203">Em Olá **assinatura de acesso compartilhado** caixa de diálogo, especifique o período de tempo de saudação e as permissões que você deseja para a conta de saudação e, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-203">In hello **Shared Access Signature** dialog box, specify hello time frame and permissions that you want for hello account, and then select **Create**.</span></span>

    <span data-ttu-id="e3c58-204">![Caixa de diálogo Obter SAS][14]</span><span class="sxs-lookup"><span data-stu-id="e3c58-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="e3c58-205">Olá **assinatura de acesso compartilhado** caixa de diálogo é aberta e exibe o saudação SAS.</span><span class="sxs-lookup"><span data-stu-id="e3c58-205">hello **Shared Access Signature** dialog box opens and displays hello SAS.</span></span>

3. <span data-ttu-id="e3c58-206">Próxima toohello **cadeia de caracteres de Conexão**, selecione **cópia** toocopy-toohello área de transferência e, em seguida, selecione **fechar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-206">Next toohello **Connection String**, select **Copy** toocopy it toohello clipboard, and then select **Close**.</span></span>

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a><span data-ttu-id="e3c58-207">Anexar conta toohello compartilhado usando Olá SAS</span><span class="sxs-lookup"><span data-stu-id="e3c58-207">Attach toohello shared account by using hello SAS</span></span>
1. <span data-ttu-id="e3c58-208">No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-208">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. <span data-ttu-id="e3c58-210">Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique a cadeia de caracteres de conexão hello e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-210">In hello **Connect tooAzure Storage** dialog box, specify hello connection string, and then select **Next**.</span></span>

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. <span data-ttu-id="e3c58-212">Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3c58-212">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="e3c58-213">alterações de toomake, selecione **novamente**e então insira configurações de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="e3c58-213">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="e3c58-214">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-214">Select **Connect**.</span></span>

5. <span data-ttu-id="e3c58-215">Depois que ele é anexado, conta de armazenamento Olá é exibida com **(SAS)** acrescentado toohello nome da conta que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="e3c58-215">After it is attached, hello storage account is displayed with **(SAS)** appended toohello account name that you supplied.</span></span>

    ![Resultado da conta tooan anexados usando SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="e3c58-217">Como anexar um serviço usando uma SAS</span><span class="sxs-lookup"><span data-stu-id="e3c58-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="e3c58-218">seção de "Anexar a uma conta de armazenamento usando uma SAS" Hello explica como um administrador de assinatura do Azure pode conceder a conta de armazenamento temporário acesso tooa gerando e compartilhando um SAS para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="e3c58-218">hello "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access tooa storage account by generating and sharing an SAS for hello storage account.</span></span> <span data-ttu-id="e3c58-219">Da mesma forma, uma SAS pode ser gerada para um serviço específico (contêiner de blobs, fila ou tabela) em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e3c58-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a><span data-ttu-id="e3c58-220">Gerar um SAS para o serviço de saudação que você deseja tooshare</span><span class="sxs-lookup"><span data-stu-id="e3c58-220">Generate an SAS for hello service that you want tooshare</span></span>
<span data-ttu-id="e3c58-221">Nesse contexto, um serviço pode ser um contêiner de blob, fila ou tabela.</span><span class="sxs-lookup"><span data-stu-id="e3c58-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="e3c58-222">Olá toogenerate SAS para um serviço listado, consulte:</span><span class="sxs-lookup"><span data-stu-id="e3c58-222">toogenerate hello SAS for a listed service, see:</span></span>

* [<span data-ttu-id="e3c58-223">Obter Olá SAS para um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="e3c58-223">Get hello SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="e3c58-224">Obter Olá SAS para um compartilhamento de arquivos: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-224">Get hello SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="e3c58-225">Obter Olá SAS para uma fila: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-225">Get hello SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="e3c58-226">Obter Olá SAS para uma tabela: *em breve*</span><span class="sxs-lookup"><span data-stu-id="e3c58-226">Get hello SAS for a table: *Coming soon*</span></span>

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a><span data-ttu-id="e3c58-227">Anexar toohello compartilhado conta serviço usando Olá SAS</span><span class="sxs-lookup"><span data-stu-id="e3c58-227">Attach toohello shared account service by using hello SAS</span></span>
1. <span data-ttu-id="e3c58-228">No Gerenciador de armazenamento (visualização), selecione **conectar o armazenamento de tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-228">In Storage Explorer (Preview), select **Connect tooAzure storage**.</span></span>

    ![Conecte-se a opção de armazenamento tooAzure][23]

2. <span data-ttu-id="e3c58-230">Em Olá **conectar tooAzure armazenamento** caixa de diálogo, especifique Olá URI SAS e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-230">In hello **Connect tooAzure Storage** dialog box, specify hello SAS URI, and then select **Next**.</span></span>

    ![Conecte-se a caixa de diálogo de armazenamento tooAzure][24]

3. <span data-ttu-id="e3c58-232">Em Olá **Conexão resumo** caixa de diálogo caixa, verifique as informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3c58-232">In hello **Connection Summary** dialog box, verify hello information.</span></span> <span data-ttu-id="e3c58-233">alterações de toomake, selecione **novamente**e então insira configurações de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="e3c58-233">toomake changes, select **Back**, and then enter hello settings you want.</span></span> 

4. <span data-ttu-id="e3c58-234">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="e3c58-234">Select **Connect**.</span></span>

5. <span data-ttu-id="e3c58-235">Depois que ele é anexado, hello serviço recentemente anexado é exibido em Olá **(serviço SAS)** nó.</span><span class="sxs-lookup"><span data-stu-id="e3c58-235">After it is attached, hello newly attached service is displayed under hello **(Service SAS)** node.</span></span>

    ![Resultado da anexação de serviço tooa compartilhado usando uma SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="e3c58-237">Pesquisar nas contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e3c58-237">Search for storage accounts</span></span>
<span data-ttu-id="e3c58-238">Se você tiver uma longa lista de contas de armazenamento, uma maneira rápida de toolocate uma determinada conta de armazenamento é toouse caixa de pesquisa de saudação na parte superior de saudação do painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="e3c58-238">If you have a long list of storage accounts, a quick way toolocate a particular storage account is toouse hello search box at hello top of hello left pane.</span></span>

<span data-ttu-id="e3c58-239">Conforme você digita na caixa de pesquisa hello, Olá painel esquerdo exibe contas de armazenamento de saudação que correspondam ao valor de pesquisa de saudação que você inseriu toothat ponto.</span><span class="sxs-lookup"><span data-stu-id="e3c58-239">As you type in hello search box, hello left pane displays hello storage accounts that match hello search value you've entered up toothat point.</span></span> <span data-ttu-id="e3c58-240">Por exemplo, uma pesquisa para armazenamento de todas as contas cujo nome contém **tarcher** é mostrado no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3c58-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in hello following screenshot:</span></span>

![Pesquisa na conta de armazenamento][11]

## <a name="next-steps"></a><span data-ttu-id="e3c58-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3c58-242">Next steps</span></span>
* [<span data-ttu-id="e3c58-243">Como gerenciar os recursos de armazenamento de Blobs do Azure com o Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="e3c58-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
