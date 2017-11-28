---
title: aaaAzure lista de contas de armazenamento
description: "Gerenciar as configurações de conta de armazenamento usando Olá Kit de ferramentas do Azure para Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="be7de-103">Lista de contas do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="be7de-103">Azure Storage Account List</span></span>
<span data-ttu-id="be7de-104">Habilitar contas de armazenamento do Azure baixar toobe locais usado para o seu JDK, servidor de aplicativos e componentes arbitrários, bem como para armazenar o estado ao usar o cache.</span><span class="sxs-lookup"><span data-stu-id="be7de-104">Azure storage accounts enable download locations toobe used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="be7de-105">O Eclipse mantém uma lista de contas de armazenamento conhecidas que são projetos tooyour disponíveis no seu espaço de trabalho do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="be7de-105">Eclipse maintains a list of known storage accounts that are available tooyour projects in your Eclipse workspace.</span></span> <span data-ttu-id="be7de-106">Olá tooopen **contas de armazenamento** caixa de diálogo, que é usado toomanage que listam no Eclipse, clique em **janela**, clique em **preferências**, expanda **Azure** e, em seguida, clique em **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="be7de-106">tooopen hello **Storage Accounts** dialog, which is used toomanage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="be7de-107">Veja a seguir de Olá Olá **contas de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-107">hello following shows hello **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="be7de-108">Essa caixa de diálogo também pode ser aberta em uma **contas** em caixas de diálogo que usam contas de armazenamento, como a seguir Olá link:</span><span class="sxs-lookup"><span data-stu-id="be7de-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as hello following:</span></span>

* <span data-ttu-id="be7de-109">Olá **JDK** guia da saudação **configuração do servidor** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-109">hello **JDK** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="be7de-110">Olá **servidor** guia da saudação **configuração do servidor** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-110">hello **Server** tab of hello **Server Configuration** dialog.</span></span>
* <span data-ttu-id="be7de-111">Olá **adicionar componente** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-111">hello **Add Component** dialog.</span></span>
* <span data-ttu-id="be7de-112">Olá **cache** caixa de diálogo Propriedades.</span><span class="sxs-lookup"><span data-stu-id="be7de-112">hello **Caching** properties dialog.</span></span>

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="be7de-113">tooimport contas de armazenamento usando um arquivo de configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="be7de-113">tooimport your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="be7de-114">Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **importar do arquivo de configurações de publicação**.</span><span class="sxs-lookup"><span data-stu-id="be7de-114">Within hello **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="be7de-115">(Ignore esta etapa se você já tiver salvo uma máquina local tooyour de arquivo publicar configurações). Em Olá **importar informações de assinatura** caixa de diálogo, clique em **baixar o arquivo de configurações de publicação**.</span><span class="sxs-lookup"><span data-stu-id="be7de-115">(Skip this step if you have already saved a publish settings file tooyour local machine.) In hello **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="be7de-116">Se você ainda não está conectados à sua conta do Azure, será solicitado toolog no.</span><span class="sxs-lookup"><span data-stu-id="be7de-116">If you are not yet logged into your Azure account, you will be prompted toolog in.</span></span> <span data-ttu-id="be7de-117">Em seguida, será solicitado que você toosave do Azure publica o arquivo de configurações.</span><span class="sxs-lookup"><span data-stu-id="be7de-117">Then you'll be prompted toosave an Azure publish settings file.</span></span> <span data-ttu-id="be7de-118">(Você pode ignorar Olá resultante instruções nas páginas de logon Olá - eles são fornecidos pelo Olá portal do Azure e são destinados a usuários do Visual Studio.) Salve-o computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="be7de-118">(You can ignore hello resulting instructions shown on hello logon pages - they are provided by hello Azure portal and are intended for Visual Studio users.) Save it tooyour local machine.</span></span>

3. <span data-ttu-id="be7de-119">Ainda no hello **importar informações de assinatura** caixa de diálogo, clique em Olá **procurar** botão, selecione Olá Publicar arquivo de configurações que você salvou anteriormente e, em seguida, clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="be7de-119">Still in hello **Import Subscription Information** dialog, click hello **Browse** button, select hello publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="be7de-120">Clique em **Okey** tooclose Olá **importar informações de assinatura** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-120">Click **OK** tooclose hello **Import Subscription Information** dialog.</span></span>

## <a name="toocreate-a-new-storage-account"></a><span data-ttu-id="be7de-121">toocreate uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="be7de-121">toocreate a new storage account</span></span>
1. <span data-ttu-id="be7de-122">Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="be7de-122">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="be7de-123">Dentro de saudação **adicionar conta de armazenamento** caixa de diálogo, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="be7de-123">Within hello **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="be7de-124">Dentro de saudação **nova conta de armazenamento** caixa de diálogo, especifique valores para seguir hello:</span><span class="sxs-lookup"><span data-stu-id="be7de-124">Within hello **New Storage Account** dialog, specify values for hello following:</span></span>

   * <span data-ttu-id="be7de-125">Nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be7de-125">Storage account name.</span></span>

   * <span data-ttu-id="be7de-126">Local da conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="be7de-126">Location of hello storage account.</span></span>

   * <span data-ttu-id="be7de-127">Descrição da conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="be7de-127">Description of hello storage account.</span></span>

   * <span data-ttu-id="be7de-128">conta de armazenamento Olá assinatura toowhich Olá pertence.</span><span class="sxs-lookup"><span data-stu-id="be7de-128">hello subscription toowhich hello storage account belongs.</span></span>

4. <span data-ttu-id="be7de-129">Clique em **Okey** tooclose Olá **nova conta de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-129">Click **OK** tooclose hello **New Storage Account** dialog.</span></span>

<span data-ttu-id="be7de-130">Ele pode levar vários minutos para que seu toobe de conta de armazenamento criada.</span><span class="sxs-lookup"><span data-stu-id="be7de-130">It may take several minutes for your storage account toobe created.</span></span> <span data-ttu-id="be7de-131">Depois de criado, clique em **Okey** tooclose Olá **adicionar conta de armazenamento** caixa de diálogo e sua nova conta de armazenamento serão adicionado toohello lista de contas de armazenamento disponível.</span><span class="sxs-lookup"><span data-stu-id="be7de-131">After it is created, click **OK** tooclose hello **Add Storage Account** dialog, and your new storage account will be added toohello list of available storage accounts.</span></span>

## <a name="tooadd-an-existing-storage-account-toohello-list"></a><span data-ttu-id="be7de-132">tooadd uma lista de toohello de conta de armazenamento existente</span><span class="sxs-lookup"><span data-stu-id="be7de-132">tooadd an existing storage account toohello list</span></span>
1. <span data-ttu-id="be7de-133">Se você ainda não tiver um armazenamento do Azure da conta, crie uma saudação etapas listadas na Olá **toocreate uma nova seção de conta de armazenamento** acima.</span><span class="sxs-lookup"><span data-stu-id="be7de-133">If you do not already have a Azure storage account, create one by following hello steps listed in hello **toocreate a new storage account section** above.</span></span> <span data-ttu-id="be7de-134">(Como alternativa, você pode criar uma nova conta de armazenamento no hello [Portal de gerenciamento][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="be7de-134">(Alternatively, you can create a new storage account at hello [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="be7de-135">Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="be7de-135">Within hello **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="be7de-136">Dentro de saudação **adicionar conta de armazenamento** caixa de diálogo, insira valores para **nome** e **chave de acesso**.</span><span class="sxs-lookup"><span data-stu-id="be7de-136">Within hello **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="be7de-137">chave de acesso e nome da conta de saudação deve ser uma conta de armazenamento do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="be7de-137">hello account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="be7de-138">Saudação de uso **armazenamento** seção Olá [Portal de gerenciamento] [ Azure Management Portal] tooview nomes e as chaves de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be7de-138">Use hello **Storage** section of hello [Azure Management Portal][Azure Management Portal] tooview your storage account names and keys.</span></span> <span data-ttu-id="be7de-139">O **adicionar conta de armazenamento** caixa de diálogo será a aparência a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="be7de-139">Your **Add Storage Account** dialog will look similar toohello following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="be7de-140">Clique em **Okey** tooclose Olá **adicionar conta de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-140">Click **OK** tooclose hello **Add Storage Account** dialog.</span></span>

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a><span data-ttu-id="be7de-141">toomodify uma conta de armazenamento toouse uma nova chave de acesso</span><span class="sxs-lookup"><span data-stu-id="be7de-141">toomodify a storage account toouse a new access key</span></span>
1. <span data-ttu-id="be7de-142">Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em Olá conta de armazenamento que você deseja tooedit e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="be7de-142">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Edit**.</span></span>

2. <span data-ttu-id="be7de-143">Dentro de saudação **Editar chave de acesso de conta de armazenamento** caixa de diálogo, modificar Olá **chave de acesso** valor.</span><span class="sxs-lookup"><span data-stu-id="be7de-143">Within hello **Edit Storage Account Access Key** dialog, modify hello **Access Key** value.</span></span>

3. <span data-ttu-id="be7de-144">Clique em **Okey** tooclose Olá **Editar chave de acesso de conta de armazenamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="be7de-144">Click **OK** tooclose hello **Edit Storage Account Access Key** dialog.</span></span>

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a><span data-ttu-id="be7de-145">tooremove uma conta de armazenamento da saudação lista mantida no Eclipse</span><span class="sxs-lookup"><span data-stu-id="be7de-145">tooremove a storage account from hello list maintained in Eclipse</span></span>
1. <span data-ttu-id="be7de-146">Dentro de saudação **contas de armazenamento** caixa de diálogo, clique em Olá conta de armazenamento que você deseja tooedit e, em seguida, clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="be7de-146">Within hello **Storage Accounts** dialog, click hello storage account that you want tooedit and then click **Remove**.</span></span>

2. <span data-ttu-id="be7de-147">Clique em **Okey** quando tooremove solicitada Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="be7de-147">Click **OK** when prompted tooremove hello storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="be7de-148">Removendo Olá conta de armazenamento por meio de saudação **contas de armazenamento** diálogo apenas a remove da lista de saudação de contas de armazenamento podem ser visualizadas no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="be7de-148">Removing hello storage account through hello **Storage Accounts** dialog only removes it from hello list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="be7de-149">Ele não remove o conta de armazenamento Olá sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="be7de-149">It does not remove hello storage account from your Azure subscription.</span></span> <span data-ttu-id="be7de-150">Além disso, o conta de armazenamento Olá pode aparecer novamente na sua lista, após o Eclipse recarregar os detalhes de saudação da sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="be7de-150">Additionally, hello storage account could appear again in your list after Eclipse reloads hello details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="be7de-151">Consulte também</span><span class="sxs-lookup"><span data-stu-id="be7de-151">See Also</span></span>
<span data-ttu-id="be7de-152">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="be7de-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="be7de-153">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="be7de-153">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="be7de-154">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="be7de-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="be7de-155">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="be7de-155">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
