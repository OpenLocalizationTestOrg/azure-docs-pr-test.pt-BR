---
title: "Introdução ao Gerenciador de armazenamento (visualização) | Microsoft Docs"
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
ms.openlocfilehash: 1794a86a4185d587cf184a1f61a5720e2ab65e92
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-storage-explorer-preview"></a><span data-ttu-id="72b19-103">Introdução ao Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="72b19-103">Get started with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="72b19-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="72b19-104">Overview</span></span>
<span data-ttu-id="72b19-105">O Gerenciador de armazenamento do Azure (visualização) é um aplicativo autônomo que permite que você trabalhe facilmente com dados do Armazenamento do Azure no Windows, no macOS e no Linux.</span><span class="sxs-lookup"><span data-stu-id="72b19-105">Azure Storage Explorer (Preview) is a standalone app that enables you to easily work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="72b19-106">Neste artigo, você aprende as várias maneiras de se conectar e gerenciar suas contas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-106">In this article, you learn the various ways of connecting to and managing your Azure storage accounts.</span></span>

![Gerenciador de Armazenamento do Microsoft Azure (Preview)][15]

## <a name="prerequisites"></a><span data-ttu-id="72b19-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="72b19-108">Prerequisites</span></span>
* [<span data-ttu-id="72b19-109">Baixe e instale o Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="72b19-109">Download and install Storage Explorer (Preview)</span></span>](http://www.storageexplorer.com)

## <a name="connect-to-a-storage-account-or-service"></a><span data-ttu-id="72b19-110">Conectar-se a uma conta de armazenamento ou serviço</span><span class="sxs-lookup"><span data-stu-id="72b19-110">Connect to a storage account or service</span></span>
<span data-ttu-id="72b19-111">O Gerenciador de armazenamento (visualização) fornece várias maneiras de se conectar às contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-111">Storage Explorer (Preview) provides several ways to connect to storage accounts.</span></span> <span data-ttu-id="72b19-112">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="72b19-112">For example, you can:</span></span>
* <span data-ttu-id="72b19-113">Conecte-se às contas de armazenamento associadas às suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-113">Connect to storage accounts associated with your Azure subscriptions.</span></span>
* <span data-ttu-id="72b19-114">Conecte-se às contas de armazenamento e serviços compartilhados a partir de outras assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-114">Connect to storage accounts and services that are shared from other Azure subscriptions.</span></span>
* <span data-ttu-id="72b19-115">Conecte-se e gerencie o armazenamento local usando o Emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-115">Connect to and manage local storage by using the Azure Storage Emulator.</span></span> 

<span data-ttu-id="72b19-116">Além disso, você pode trabalhar com contas nacionais e internacionais de armazenamento no Azure:</span><span class="sxs-lookup"><span data-stu-id="72b19-116">In addition, you can work with storage accounts in global and national Azure:</span></span>

* <span data-ttu-id="72b19-117">[Como conectar-se a uma assinatura do Azure](#connect-to-an-azure-subscription) - gerencie os recursos de armazenamento que pertencem à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-117">[Connect to an Azure subscription](#connect-to-an-azure-subscription): Manage storage resources that belong to your Azure subscription.</span></span>
* <span data-ttu-id="72b19-118">[Como trabalhar com o armazenamento de desenvolvimento local](#work-with-local-development-storage) - gerencie o armazenamento local usando o Emulador de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-118">[Work with local development storage](#work-with-local-development-storage): Manage local storage by using the Azure Storage Emulator.</span></span>
* <span data-ttu-id="72b19-119">[Como anexar ao armazenamento externo](#attach-or-detach-an-external-storage-account) - Gerencie os recursos de armazenamento que pertencem a outra assinatura do Azure ou que estão sob nuvens nacionais do Azure usando o nome de conta de armazenamento, a chave e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="72b19-119">[Attach to external storage](#attach-or-detach-an-external-storage-account): Manage storage resources that belong to another Azure subscription or that are under national Azure clouds by using the storage account's name, key, and endpoints.</span></span>
* <span data-ttu-id="72b19-120">[Como anexar uma conta de armazenamento usando uma SAS](#attach-storage-account-using-sas): gerencie recursos de armazenamento que pertencem a outra assinatura do Azure usando uma assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="72b19-120">[Attach a storage account by using an SAS](#attach-storage-account-using-sas): Manage storage resources that belong to another Azure subscription by using a shared access signature (SAS).</span></span>
* <span data-ttu-id="72b19-121">[Como anexar um serviço usando uma SAS](#attach-service-using-sas): gerenciar um serviço de armazenamento específico (contêiner de blobs, fila ou tabela) que pertence a outra assinatura do Azure usando uma SAS.</span><span class="sxs-lookup"><span data-stu-id="72b19-121">[Attach a service by using an SAS](#attach-service-using-sas): Manage a specific storage service (blob container, queue, or table) that belongs to another Azure subscription by using an SAS.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="72b19-122">Conectar-se a uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="72b19-122">Connect to an Azure subscription</span></span>
> [!NOTE]
> <span data-ttu-id="72b19-123">Se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="72b19-123">If you don't have an Azure account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
>
>

1. <span data-ttu-id="72b19-124">No Gerenciador de Armazenamento (Visualização), selecione **Configurações de conta do Azure**.</span><span class="sxs-lookup"><span data-stu-id="72b19-124">In Storage Explorer (Preview), select **Azure Account settings**.</span></span>

    ![Configurações de conta do Azure][0]

2. <span data-ttu-id="72b19-126">O painel esquerdo exibe todas as contas da Microsoft em que você fez logon.</span><span class="sxs-lookup"><span data-stu-id="72b19-126">The left pane displays all the Microsoft accounts you've signed in to.</span></span> <span data-ttu-id="72b19-127">Para se conectar a outra conta, selecione **Adicionar uma conta** e siga as instruções para entrar com uma conta da Microsoft associada a pelo menos uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-127">To connect to another account, select **Add an account**, and then follow the instructions to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>

    >[!NOTE]
    ><span data-ttu-id="72b19-128">Conectar-se ao Azure nacional (como Azure Alemanha, Azure Governamental e Azure China por meio logon) não é suportado atualmente.</span><span class="sxs-lookup"><span data-stu-id="72b19-128">Connecting to national Azure (such as Azure Germany, Azure Government, and Azure China via sign-in) is currently not supported.</span></span> <span data-ttu-id="72b19-129">Confira a seção "Anexar ou desanexar uma conta de armazenamento externo" para saber como se conectar a contas de armazenamento do Azure nacional.</span><span class="sxs-lookup"><span data-stu-id="72b19-129">See the "Attach or detach an external storage account" section for how to connect to national Azure storage accounts.</span></span>

3. <span data-ttu-id="72b19-130">Depois de entrar com êxito usando uma conta da Microsoft, o painel esquerdo é preenchido com as assinaturas do Azure associadas à conta.</span><span class="sxs-lookup"><span data-stu-id="72b19-130">After you successfully sign in with a Microsoft account, the left pane is populated with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="72b19-131">Selecione as assinaturas do Azure com as quais você deseja trabalhar e selecione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-131">Select the Azure subscriptions that you want to work with, and then select **Apply**.</span></span> <span data-ttu-id="72b19-132">(A escolha dos botões **Todas as assinaturas** seleciona todas ou nenhuma das assinaturas do Azure listadas).</span><span class="sxs-lookup"><span data-stu-id="72b19-132">(Selecting **All subscriptions** toggles selecting all or none of the listed Azure subscriptions.)</span></span>

    ![Selecionar assinaturas do Azure][3]  
    <span data-ttu-id="72b19-134">O painel esquerdo exibe as contas de armazenamento associadas às assinaturas do Azure selecionadas.</span><span class="sxs-lookup"><span data-stu-id="72b19-134">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>

    ![Assinaturas do Azure selecionadas][4]

## <a name="connect-to-an-azure-stack-subscription"></a><span data-ttu-id="72b19-136">Conexão com uma assinatura do Azure Stack</span><span class="sxs-lookup"><span data-stu-id="72b19-136">Connect to an Azure Stack subscription</span></span>

<span data-ttu-id="72b19-137">Para obter informações sobre como se conectar a uma assinatura do Azure Stack, confira [Conectar o Gerenciador de Armazenamento para uma assinatura do Azure Stack](azure-stack/azure-stack-storage-connect-se.md).</span><span class="sxs-lookup"><span data-stu-id="72b19-137">For information about connecting to an Azure Stack subscription, see [Connect Storage Explorer to an Azure Stack subscription](azure-stack/azure-stack-storage-connect-se.md).</span></span>

## <a name="work-with-local-development-storage"></a><span data-ttu-id="72b19-138">Trabalhar com o armazenamento de desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="72b19-138">Work with local development storage</span></span>
<span data-ttu-id="72b19-139">O Gerenciador de armazenamento (visualização) permite que você trabalhe no armazenamento local usando o Emulador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-139">With Storage Explorer (Preview), you can work against local storage by using the Azure Storage Emulator.</span></span> <span data-ttu-id="72b19-140">Isso permite que você escreva códigos e teste o armazenamento sem necessariamente ter uma conta de armazenamento implantada no Azure, uma vez que a conta de armazenamento está sendo emulada pelo Emulador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-140">This approach lets you write code against and test storage without necessarily having a storage account deployed on Azure, because the storage account is being emulated by the Azure Storage Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="72b19-141">No momento, o Emulador de Armazenamento do Azure tem suporte somente para Windows.</span><span class="sxs-lookup"><span data-stu-id="72b19-141">The Azure Storage Emulator is currently supported only for Windows.</span></span>
>
>

1. <span data-ttu-id="72b19-142">No painel esquerdo do Gerenciador de armazenamento (visualização), expanda o nó **(Local e Anexados)** > **Contas de Armazenamento** > **(Desenvolvimento)**.</span><span class="sxs-lookup"><span data-stu-id="72b19-142">In the left pane of Storage Explorer (Preview), expand the **(Local and Attached)** > **Storage Accounts** > **(Development)** node.</span></span>

    ![Nó de desenvolvimento local][21]

2. <span data-ttu-id="72b19-144">Se você ainda não tiver instalado o Emulador de Armazenamento do Azure, receberá uma solicitação para fazer isso por meio de uma barra de informações.</span><span class="sxs-lookup"><span data-stu-id="72b19-144">If you have not yet installed the Azure Storage Emulator, you are prompted to do so via an infobar.</span></span> <span data-ttu-id="72b19-145">Se a barra de informações for exibida, escolha **Baixar a versão mais recente** e instale o emulador.</span><span class="sxs-lookup"><span data-stu-id="72b19-145">If the infobar is displayed, select **Download the latest version**, and then install the emulator.</span></span>

    ![Baixar o prompt do Emulador de Armazenamento do Azure][22]

3. <span data-ttu-id="72b19-147">Depois que o emulador está instalado, você pode criar e trabalhar com blobs, filas e tabelas locais.</span><span class="sxs-lookup"><span data-stu-id="72b19-147">After the emulator is installed, you can create and work with local blobs, queues, and tables.</span></span> <span data-ttu-id="72b19-148">Para saber como trabalhar com cada tipo de conta de armazenamento, confira um dos links a seguir:</span><span class="sxs-lookup"><span data-stu-id="72b19-148">To learn how to work with each storage account type, see one of the following:</span></span>

    * [<span data-ttu-id="72b19-149">Gerenciar recursos de Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="72b19-149">Manage Azure blob storage resources</span></span>](vs-azure-tools-storage-explorer-blobs.md)
    * <span data-ttu-id="72b19-150">Gerenciar recursos de armazenamento de compartilhamento de arquivos do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-150">Manage Azure file share storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="72b19-151">Gerenciar recursos de armazenamento de filas do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-151">Manage Azure queue storage resources: *Coming soon*</span></span>
    * <span data-ttu-id="72b19-152">Gerenciar recursos de armazenamento de tabelas do Azure: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-152">Manage Azure table storage resources: *Coming soon*</span></span>

## <a name="attach-or-detach-an-external-storage-account"></a><span data-ttu-id="72b19-153">Conexão ou desconexão de uma conta de armazenamento externo</span><span class="sxs-lookup"><span data-stu-id="72b19-153">Attach or detach an external storage account</span></span>
<span data-ttu-id="72b19-154">O Gerenciador de armazenamento (visualização) permite anexar contas de armazenamento externas para facilitar o compartilhamento das contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-154">With Storage Explorer (Preview), you can attach to external storage accounts so that storage accounts can be easily shared.</span></span> <span data-ttu-id="72b19-155">Esta seção explica como anexar e desanexar contas do armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="72b19-155">This section explains how to attach to (and detach from) external storage accounts.</span></span>

### <a name="get-the-storage-account-credentials"></a><span data-ttu-id="72b19-156">Obter as credenciais da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="72b19-156">Get the storage account credentials</span></span>
<span data-ttu-id="72b19-157">Para compartilhar uma conta de armazenamento externo, o proprietário dessa conta precisa primeiro obter as credenciais (nome e chave da conta), para depois compartilhar essas informações com a pessoa que deseja ser anexada a essa conta (externa).</span><span class="sxs-lookup"><span data-stu-id="72b19-157">To share an external storage account, the owner of that account must first get the credentials (account name and key) for the account and then share that information with the person who wants to attach to that (external) account.</span></span> <span data-ttu-id="72b19-158">Você pode obter as credenciais da conta de armazenamento por meio do portal do Azure fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="72b19-158">You can obtain the storage account credentials via the Azure portal by doing the following:</span></span>

1. <span data-ttu-id="72b19-159">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72b19-159">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="72b19-160">Selecione **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-160">Select **Browse**.</span></span>

3. <span data-ttu-id="72b19-161">Selecione **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="72b19-161">Select **Storage Accounts**.</span></span>

4. <span data-ttu-id="72b19-162">Na folha **Contas de Armazenamento** , escolha a conta de armazenamento desejada.</span><span class="sxs-lookup"><span data-stu-id="72b19-162">On the **Storage Accounts** blade, select the desired storage account.</span></span>

5. <span data-ttu-id="72b19-163">Na folha **Configurações** da conta de armazenamento selecionada, escolha **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="72b19-163">On the **Settings** blade for the selected storage account, select **Access keys**.</span></span>

    ![Opção Chaves de Acesso][5]

6. <span data-ttu-id="72b19-165">Na folha **Chaves de acesso**, copie os valores de **Nome da conta de armazenamento** e **key1** que serão usados para anexação à conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-165">On the **Access keys** blade, copy the **Storage account name** and **key1** values for use when attaching to the storage account.</span></span>

    ![Chaves de acesso][6]

### <a name="attach-to-an-external-storage-account"></a><span data-ttu-id="72b19-167">Anexação a uma conta de armazenamento externo</span><span class="sxs-lookup"><span data-stu-id="72b19-167">Attach to an external storage account</span></span>
<span data-ttu-id="72b19-168">Para anexar a uma conta de armazenamento externo, você precisará do nome da conta e da chave.</span><span class="sxs-lookup"><span data-stu-id="72b19-168">To attach to an external storage account, you need the account's name and key.</span></span> <span data-ttu-id="72b19-169">A seção "Como obter as credenciais de conta de armazenamento" explica como obter esses valores no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-169">The "Get the storage account credentials" section explains how to obtain these values from the Azure portal.</span></span> <span data-ttu-id="72b19-170">No entanto, no portal, a chave de conta é chamada **key1**.</span><span class="sxs-lookup"><span data-stu-id="72b19-170">However, in the portal, the account key is called **key1**.</span></span> <span data-ttu-id="72b19-171">Então, quando o Gerenciador de armazenamento (visualização) solicitar uma chave de conta, digite o valor **key1**.</span><span class="sxs-lookup"><span data-stu-id="72b19-171">So where Storage Explorer (Preview) asks for an account key, you enter the **key1** value.</span></span>

1. <span data-ttu-id="72b19-172">No Gerenciador de Armazenamento (Visualização), selecione **Conectar ao armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="72b19-172">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opção Conectar ao Armazenamento do Azure][23]

2. <span data-ttu-id="72b19-174">Na caixa de diálogo **Conectar ao Armazenamento do Azure**, especifique a chave de conta (o valor **key1** no portal do Azure) e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-174">In the **Connect to Azure Storage** dialog box, specify the account key (the **key1** value from the Azure portal), and then select **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72b19-175">Você pode inserir a cadeia de conexão de armazenamento de uma conta de armazenamento no Azure nacional.</span><span class="sxs-lookup"><span data-stu-id="72b19-175">You can enter the storage connection string from a storage account on national Azure.</span></span> <span data-ttu-id="72b19-176">Por exemplo, para se conectar às contas de armazenamento do Azure Alemanha, insira cadeias de conexão semelhantes à seguinte:</span><span class="sxs-lookup"><span data-stu-id="72b19-176">For example, to connect to Azure Germany storage accounts, enter connection strings similar to the following:</span></span> 
    >
    >* <span data-ttu-id="72b19-177">DefaultEndpointsProtocol=https</span><span class="sxs-lookup"><span data-stu-id="72b19-177">DefaultEndpointsProtocol=https</span></span>
    >* <span data-ttu-id="72b19-178">AccountName=cawatest03</span><span class="sxs-lookup"><span data-stu-id="72b19-178">AccountName=cawatest03</span></span>
    >* <span data-ttu-id="72b19-179">AccountKey=<storage_account_key></span><span class="sxs-lookup"><span data-stu-id="72b19-179">AccountKey=<storage_account_key></span></span>
    >* <span data-ttu-id="72b19-180">EndpointSuffix=core.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="72b19-180">EndpointSuffix=core.cloudapi.de</span></span>
    
    ><span data-ttu-id="72b19-181">Você pode obter a cadeia de conexão no portal do Azure da mesma forma que conforme descrito na seção "Como obter as credenciais da conta de armazenamento".</span><span class="sxs-lookup"><span data-stu-id="72b19-181">You can get the connection string from the Azure portal in the same way as described in the "Get the storage account credentials" section.</span></span>

    ![Caixa de diálogo Conectar ao Armazenamento do Azure][24]

3. <span data-ttu-id="72b19-183">Na caixa de diálogo **Anexar Armazenamento Externo**, insira o nome da conta de armazenamento na caixa **Nome da conta**, especifique outras configurações desejadas e, então, selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-183">In the **Attach External Storage** dialog box, in the **Account name** box, enter the storage account name, specify any other desired settings, and then select **Next**.</span></span>

    ![Caixa de diálogo Anexar Armazenamento Externo][8]

4. <span data-ttu-id="72b19-185">Na caixa de diálogo **Resumo da Conexão**, verifique as informações.</span><span class="sxs-lookup"><span data-stu-id="72b19-185">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="72b19-186">Se você quiser alterar alguma coisa, selecione **Voltar** e insira novamente as configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="72b19-186">If you want to change anything, select **Back** and reenter the desired settings.</span></span> 

5. <span data-ttu-id="72b19-187">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-187">Select **Connect**.</span></span>

6. <span data-ttu-id="72b19-188">Depois de conectada, a conta de armazenamento externo será exibida com o texto **(Externo)** anexado ao nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-188">After it is successfully connected, the external storage account is displayed with **(External)** appended to the storage account name.</span></span>

    ![Resultado da conexão a uma conta de armazenamento externo][9]

### <a name="detach-from-an-external-storage-account"></a><span data-ttu-id="72b19-190">Desconexão de uma conta de armazenamento externo</span><span class="sxs-lookup"><span data-stu-id="72b19-190">Detach from an external storage account</span></span>
1. <span data-ttu-id="72b19-191">Clique o botão direito do mouse na conta de armazenamento externo que você deseja desanexar e, em seguida, selecione **Desanexar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-191">Right-click the external storage account that you want to detach, and then select **Detach**.</span></span>

    ![Opção Desanexar do armazenamento][10]

2. <span data-ttu-id="72b19-193">Na mensagem de confirmação, escolha **Sim** para confirmar a desconexão da conta de armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="72b19-193">In the confirmation message, select **Yes** to confirm the detachment from the external storage account.</span></span>

## <a name="attach-a-storage-account-by-using-an-sas"></a><span data-ttu-id="72b19-194">Como anexar uma conta de armazenamento usando uma SAS</span><span class="sxs-lookup"><span data-stu-id="72b19-194">Attach a storage account by using an SAS</span></span>
<span data-ttu-id="72b19-195">Uma [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) permite que o administrador de uma assinatura do Azure conceda acesso temporário para uma conta de armazenamento sem ter que fornecer credenciais de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="72b19-195">An [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) lets the admin of an Azure subscription grant temporary access to a storage account without having to provide Azure subscription credentials.</span></span>

<span data-ttu-id="72b19-196">Para ilustrar isso, vamos supor que o UsuárioA é um administrador de uma assinatura do Azure, e o UsuárioA deseja permitir que o UsuárioB acesse uma conta de armazenamento por um período limitado com determinadas permissões:</span><span class="sxs-lookup"><span data-stu-id="72b19-196">To illustrate this scenario, let's say that UserA is an admin of an Azure subscription, and UserA wants to allow UserB to access a storage account for a limited time with certain permissions:</span></span>

1. <span data-ttu-id="72b19-197">O UsuárioA gera uma SAS (formada pela cadeia de conexão da conta de armazenamento) para um período específico e com as permissões desejadas.</span><span class="sxs-lookup"><span data-stu-id="72b19-197">UserA generates an SAS (consisting of the connection string for the storage account) for a specific time period and with the desired permissions.</span></span>

2. <span data-ttu-id="72b19-198">O UsuárioA compartilha a SAS com a pessoa (no exemplo, o UsuárioB) que deseja acessar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-198">UserA shares the SAS with the person (UserB, in our example) who wants access to the storage account.</span></span>  

3. <span data-ttu-id="72b19-199">O UsuárioB usa o Gerenciador de armazenamento (visualização) para se anexar à conta pertencente ao UsuárioA usando a SAS fornecida.</span><span class="sxs-lookup"><span data-stu-id="72b19-199">UserB uses Storage Explorer (Preview) to attach to the account that belongs to UserA by using the supplied SAS.</span></span>

### <a name="get-an-sas-for-the-account-you-want-to-share"></a><span data-ttu-id="72b19-200">Obter uma SAS para a conta que você deseja compartilhar</span><span class="sxs-lookup"><span data-stu-id="72b19-200">Get an SAS for the account you want to share</span></span>
1. <span data-ttu-id="72b19-201">No Gerenciador de armazenamento (visualização), clique o botão direito do mouse na conta de armazenamento que você deseja compartilhar e, então, escolha **Obter Assinatura de Acesso Compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="72b19-201">In Storage Explorer (Preview), right-click the storage account you want share, and then select **Get Shared Access Signature**.</span></span>

    ![Opção do menu de contexto Obter SAS][13]

2. <span data-ttu-id="72b19-203">Na caixa de diálogo **Assinatura de Acesso Compartilhado**, especifique o intervalo e as permissões que você deseja para a conta e, então, escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-203">In the **Shared Access Signature** dialog box, specify the time frame and permissions that you want for the account, and then select **Create**.</span></span>

    <span data-ttu-id="72b19-204">![Caixa de diálogo Obter SAS][14]</span><span class="sxs-lookup"><span data-stu-id="72b19-204">![Get SAS dialog box][14]</span></span>  
    <span data-ttu-id="72b19-205">A caixa de diálogo **Assinatura de Acesso Compartilhado** abre e exibe a SAS.</span><span class="sxs-lookup"><span data-stu-id="72b19-205">The **Shared Access Signature** dialog box opens and displays the SAS.</span></span>

3. <span data-ttu-id="72b19-206">Ao lado de **cadeia de conexão**, selecione **Copiar** para copiar para a área de transferência e, em seguida, selecione **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-206">Next to the **Connection String**, select **Copy** to copy it to the clipboard, and then select **Close**.</span></span>

### <a name="attach-to-the-shared-account-by-using-the-sas"></a><span data-ttu-id="72b19-207">Anexar à conta compartilhada usando a SAS</span><span class="sxs-lookup"><span data-stu-id="72b19-207">Attach to the shared account by using the SAS</span></span>
1. <span data-ttu-id="72b19-208">No Gerenciador de Armazenamento (Visualização), selecione **Conectar ao armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="72b19-208">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opção Conectar ao Armazenamento do Azure][23]

2. <span data-ttu-id="72b19-210">Na caixa de diálogo **Conectar ao Armazenamento do Azure**, especifique a cadeia de conexão e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-210">In the **Connect to Azure Storage** dialog box, specify the connection string, and then select **Next**.</span></span>

    ![Caixa de diálogo Conectar ao Armazenamento do Azure][24]

3. <span data-ttu-id="72b19-212">Na caixa de diálogo **Resumo da Conexão**, verifique as informações.</span><span class="sxs-lookup"><span data-stu-id="72b19-212">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="72b19-213">Para fazer alterações, selecione **Retornar** e, em seguida, insira as configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="72b19-213">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="72b19-214">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-214">Select **Connect**.</span></span>

5. <span data-ttu-id="72b19-215">Depois que estiver conectado, a conta de armazenamento é exibida com **(SAS)** acrescentado ao nome da conta que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="72b19-215">After it is attached, the storage account is displayed with **(SAS)** appended to the account name that you supplied.</span></span>

    ![O resultado da anexação a uma conta usando a SAS][17]

## <a name="attach-a-service-by-using-an-sas"></a><span data-ttu-id="72b19-217">Como anexar um serviço usando uma SAS</span><span class="sxs-lookup"><span data-stu-id="72b19-217">Attach a service by using an SAS</span></span>
<span data-ttu-id="72b19-218">A seção "Como anexar uma conta de armazenamento usando uma SAS" ilustra como um administrador de assinatura do Azure pode conceder acesso temporário a uma conta de armazenamento gerando e compartilhando uma SAS para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-218">The "Attach a storage account by using an SAS" section explains how an Azure subscription admin can grant temporary access to a storage account by generating and sharing an SAS for the storage account.</span></span> <span data-ttu-id="72b19-219">Da mesma forma, uma SAS pode ser gerada para um serviço específico (contêiner de blobs, fila ou tabela) em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="72b19-219">Similarly, an SAS can be generated for a specific service (blob container, queue, or table) within a storage account.</span></span>  

### <a name="generate-an-sas-for-the-service-that-you-want-to-share"></a><span data-ttu-id="72b19-220">Gerar uma SAS para o serviço que você deseja compartilhar</span><span class="sxs-lookup"><span data-stu-id="72b19-220">Generate an SAS for the service that you want to share</span></span>
<span data-ttu-id="72b19-221">Nesse contexto, um serviço pode ser um contêiner de blob, fila ou tabela.</span><span class="sxs-lookup"><span data-stu-id="72b19-221">In this context, a service can be a blob container, queue, or table.</span></span> <span data-ttu-id="72b19-222">Para gerar o SAS para um serviço listado, confira:</span><span class="sxs-lookup"><span data-stu-id="72b19-222">To generate the SAS for a listed service, see:</span></span>

* [<span data-ttu-id="72b19-223">Obter a SAS para um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="72b19-223">Get the SAS for a blob container</span></span>](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* <span data-ttu-id="72b19-224">Obter a SAS para um compartilhamento de arquivos: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-224">Get the SAS for a file share: *Coming soon*</span></span>
* <span data-ttu-id="72b19-225">Obter a SAS para uma fila: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-225">Get the SAS for a queue: *Coming soon*</span></span>
* <span data-ttu-id="72b19-226">Obter a SAS para uma tabela: *em breve*</span><span class="sxs-lookup"><span data-stu-id="72b19-226">Get the SAS for a table: *Coming soon*</span></span>

### <a name="attach-to-the-shared-account-service-by-using-the-sas"></a><span data-ttu-id="72b19-227">Anexar ao serviço de conta compartilhada usando a SAS</span><span class="sxs-lookup"><span data-stu-id="72b19-227">Attach to the shared account service by using the SAS</span></span>
1. <span data-ttu-id="72b19-228">No Gerenciador de Armazenamento (Visualização), selecione **Conectar ao armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="72b19-228">In Storage Explorer (Preview), select **Connect to Azure storage**.</span></span>

    ![Opção Conectar ao Armazenamento do Azure][23]

2. <span data-ttu-id="72b19-230">Na caixa de diálogo **Conectar ao Armazenamento do Azure**, especifique o URI da SAS e selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-230">In the **Connect to Azure Storage** dialog box, specify the SAS URI, and then select **Next**.</span></span>

    ![Caixa de diálogo Conectar ao Armazenamento do Azure][24]

3. <span data-ttu-id="72b19-232">Na caixa de diálogo **Resumo da Conexão**, verifique as informações.</span><span class="sxs-lookup"><span data-stu-id="72b19-232">In the **Connection Summary** dialog box, verify the information.</span></span> <span data-ttu-id="72b19-233">Para fazer alterações, selecione **Retornar** e, em seguida, insira as configurações desejadas.</span><span class="sxs-lookup"><span data-stu-id="72b19-233">To make changes, select **Back**, and then enter the settings you want.</span></span> 

4. <span data-ttu-id="72b19-234">Selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="72b19-234">Select **Connect**.</span></span>

5. <span data-ttu-id="72b19-235">Depois de anexado, o serviço recém-anexado será exibido abaixo do nó **(SAS do Serviço)** .</span><span class="sxs-lookup"><span data-stu-id="72b19-235">After it is attached, the newly attached service is displayed under the **(Service SAS)** node.</span></span>

    ![Resultado da anexação a um serviço compartilhado usando SAS][20]

## <a name="search-for-storage-accounts"></a><span data-ttu-id="72b19-237">Pesquisar nas contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="72b19-237">Search for storage accounts</span></span>
<span data-ttu-id="72b19-238">Se você tiver uma lista longa de contas de armazenamento, uma maneira rápida de localizar uma determinada conta de armazenamento é usar a caixa de pesquisa na parte superior do painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="72b19-238">If you have a long list of storage accounts, a quick way to locate a particular storage account is to use the search box at the top of the left pane.</span></span>

<span data-ttu-id="72b19-239">À medida que você digita na caixa de pesquisa, o painel esquerdo exibe somente as contas de armazenamento que correspondem ao valor de pesquisa inserido até esse ponto.</span><span class="sxs-lookup"><span data-stu-id="72b19-239">As you type in the search box, the left pane displays the storage accounts that match the search value you've entered up to that point.</span></span> <span data-ttu-id="72b19-240">Por exemplo, uma pesquisa para todas as contas de armazenamento cujo nome contém **tarcher** é mostrado na seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="72b19-240">For example, a search for all storage accounts whose name contains **tarcher** is shown in the following screenshot:</span></span>

![Pesquisa na conta de armazenamento][11]

## <a name="next-steps"></a><span data-ttu-id="72b19-242">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72b19-242">Next steps</span></span>
* [<span data-ttu-id="72b19-243">Como gerenciar os recursos de armazenamento de Blobs do Azure com o Gerenciador de armazenamento (visualização)</span><span class="sxs-lookup"><span data-stu-id="72b19-243">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>](vs-azure-tools-storage-explorer-blobs.md)

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
