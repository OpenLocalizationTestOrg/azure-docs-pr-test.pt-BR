---
title: Lista de contas do Armazenamento do Azure
description: "Gerenciar as configurações de conta de armazenamento usando o Kit de Ferramentas do Azure para o Eclipse"
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a><span data-ttu-id="34a8f-103">Lista de contas do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="34a8f-103">Azure Storage Account List</span></span>
<span data-ttu-id="34a8f-104">As contas de armazenamento do Azure permitem que os locais de download sejam usados para o seu JDK, servidor de aplicativos e componentes arbitrários, bem como para armazenar o estado ao usar o caching.</span><span class="sxs-lookup"><span data-stu-id="34a8f-104">Azure storage accounts enable download locations to be used for your JDK, application server, and arbitrary components, as well as for storing state when using caching.</span></span> <span data-ttu-id="34a8f-105">O Eclipse mantém uma lista de contas de armazenamento conhecidas que estão disponíveis para seus projetos no espaço de trabalho do Eclipse.</span><span class="sxs-lookup"><span data-stu-id="34a8f-105">Eclipse maintains a list of known storage accounts that are available to your projects in your Eclipse workspace.</span></span> <span data-ttu-id="34a8f-106">Para abrir a caixa de diálogo **Contas de Armazenamento**, que é usada para gerenciar essa lista, no Eclipse, clique em **Janela**, **Preferências**, expanda o **Azure**, em seguida, clique em **Contas de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-106">To open the **Storage Accounts** dialog, which is used to manage that list, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Storage Accounts**.</span></span>

<span data-ttu-id="34a8f-107">Veja a seguir o diálogo **Contas de Armazenamento** .</span><span class="sxs-lookup"><span data-stu-id="34a8f-107">The following shows the **Storage Accounts** dialog.</span></span>

![][ic719496]

<span data-ttu-id="34a8f-108">Essa caixa de diálogo também pode ser aberta a partir de um link **Contas** nas caixas de diálogo que usam contas de armazenamento, como as seguintes:</span><span class="sxs-lookup"><span data-stu-id="34a8f-108">This dialog can also be opened from an **Accounts** link on dialog boxes that use storage accounts, such as the following:</span></span>

* <span data-ttu-id="34a8f-109">Guia **JDK** da caixa de diálogo **Configuração do Servidor**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-109">The **JDK** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="34a8f-110">Guia **Servidor** da caixa de diálogo **Configuração do Servidor**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-110">The **Server** tab of the **Server Configuration** dialog.</span></span>
* <span data-ttu-id="34a8f-111">O diálogo **Adicionar Componente** .</span><span class="sxs-lookup"><span data-stu-id="34a8f-111">The **Add Component** dialog.</span></span>
* <span data-ttu-id="34a8f-112">O diálogo de propriedades **Caching** .</span><span class="sxs-lookup"><span data-stu-id="34a8f-112">The **Caching** properties dialog.</span></span>

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a><span data-ttu-id="34a8f-113">Para importar suas contas de armazenamento usando um arquivo de configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="34a8f-113">To import your storage accounts using a publish settings file</span></span>
1. <span data-ttu-id="34a8f-114">Na caixa de diálogo **Contas de Armazenamento**, clique em **Importar do arquivo PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-114">Within the **Storage Accounts** dialog, click **Import from PUBLISH-SETTINGS file**.</span></span>

2. <span data-ttu-id="34a8f-115">(Ignore esta etapa se você já tiver salvo um arquivo de configurações de publicação em seu computador local.) Na caixa de diálogo **Importar Informações da Assinatura**, clique em **Baixar Arquivo PUBLISH-SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-115">(Skip this step if you have already saved a publish settings file to your local machine.) In the **Import Subscription Information** dialog, click **Download PUBLISH-SETTINGS File**.</span></span> <span data-ttu-id="34a8f-116">Se você ainda não estiver conectado à sua conta do Azure, receberá uma solicitação para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="34a8f-116">If you are not yet logged into your Azure account, you will be prompted to log in.</span></span> <span data-ttu-id="34a8f-117">Em seguida, você receberá uma solicitação para salvar um arquivo de configurações de publicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="34a8f-117">Then you'll be prompted to save an Azure publish settings file.</span></span> <span data-ttu-id="34a8f-118">(Você pode ignorar as instruções resultantes mostradas nas páginas de logon - elas são fornecidas pelo portal do Azure e são destinadas aos usuários do Visual Studio.) Salve-o em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="34a8f-118">(You can ignore the resulting instructions shown on the logon pages - they are provided by the Azure portal and are intended for Visual Studio users.) Save it to your local machine.</span></span>

3. <span data-ttu-id="34a8f-119">Ainda na caixa de diálogo **Importar Informações da Assinatura**, clique no botão **Procurar**, selecione o arquivo de configurações da publicação salvo anteriormente, em seguida, clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-119">Still in the **Import Subscription Information** dialog, click the **Browse** button, select the publish settings file that you saved locally previously, and then click **Open**.</span></span>

4. <span data-ttu-id="34a8f-120">Clique em **OK** para fechar a caixa de diálogo **Importar Informações da Assinatura**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-120">Click **OK** to close the **Import Subscription Information** dialog.</span></span>

## <a name="to-create-a-new-storage-account"></a><span data-ttu-id="34a8f-121">Para criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="34a8f-121">To create a new storage account</span></span>
1. <span data-ttu-id="34a8f-122">Na caixa de diálogo **Contas de Armazenamento**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-122">Within the **Storage Accounts** dialog, click **Add**.</span></span>

2. <span data-ttu-id="34a8f-123">Na caixa de diálogo **Adicionar Conta de Armazenamento**, clique em **Nova**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-123">Within the **Add Storage Account** dialog, click **New**.</span></span>

3. <span data-ttu-id="34a8f-124">No diálogo **Nova Conta de Armazenamento** , especifique valores para os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="34a8f-124">Within the **New Storage Account** dialog, specify values for the following:</span></span>

   * <span data-ttu-id="34a8f-125">Nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-125">Storage account name.</span></span>

   * <span data-ttu-id="34a8f-126">Local da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-126">Location of the storage account.</span></span>

   * <span data-ttu-id="34a8f-127">Descrição da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-127">Description of the storage account.</span></span>

   * <span data-ttu-id="34a8f-128">A assinatura à qual pertence a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-128">The subscription to which the storage account belongs.</span></span>

4. <span data-ttu-id="34a8f-129">Clique em **OK** para fechar a caixa de diálogo **Nova Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-129">Click **OK** to close the **New Storage Account** dialog.</span></span>

<span data-ttu-id="34a8f-130">Pode levar vários minutos para que a sua conta de armazenamento seja criada.</span><span class="sxs-lookup"><span data-stu-id="34a8f-130">It may take several minutes for your storage account to be created.</span></span> <span data-ttu-id="34a8f-131">Depois de criada, clique em **OK** para fechar a caixa de diálogo **Adicionar Conta de Armazenamento** e sua nova conta de armazenamento será adicionado à lista de contas de armazenamento disponíveis.</span><span class="sxs-lookup"><span data-stu-id="34a8f-131">After it is created, click **OK** to close the **Add Storage Account** dialog, and your new storage account will be added to the list of available storage accounts.</span></span>

## <a name="to-add-an-existing-storage-account-to-the-list"></a><span data-ttu-id="34a8f-132">Para adicionar uma conta de armazenamento existente à lista</span><span class="sxs-lookup"><span data-stu-id="34a8f-132">To add an existing storage account to the list</span></span>
1. <span data-ttu-id="34a8f-133">Se você ainda não tem uma conta de armazenamento do Azure, crie uma seguindo as etapas listadas na seção **Para criar uma nova conta de armazenamento** acima.</span><span class="sxs-lookup"><span data-stu-id="34a8f-133">If you do not already have a Azure storage account, create one by following the steps listed in the **To create a new storage account section** above.</span></span> <span data-ttu-id="34a8f-134">(Como alternativa, você pode criar uma nova conta de armazenamento no [Portal de Gerenciamento do Azure][Azure Management Portal].)</span><span class="sxs-lookup"><span data-stu-id="34a8f-134">(Alternatively, you can create a new storage account at the [Azure Management Portal][Azure Management Portal].)</span></span>

2. <span data-ttu-id="34a8f-135">Na caixa de diálogo **Contas de Armazenamento**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-135">Within the **Storage Accounts** dialog, click **Add**.</span></span>

3. <span data-ttu-id="34a8f-136">Na caixa de diálogo **Adicionar Conta de Armazenamento**, insira valores para o **Nome** e a **Chave de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-136">Within the **Add Storage Account** dialog, enter values for **Name** and **Access Key**.</span></span> <span data-ttu-id="34a8f-137">O nome da conta e a chave de acesso devem ser de uma conta existente do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="34a8f-137">The account name and access key must be for an existing Azure storage account.</span></span> <span data-ttu-id="34a8f-138">Use a seção **Armazenamento** do [Portal de Gerenciamento do Azure][Azure Management Portal] para exibir seus nomes e chaves de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-138">Use the **Storage** section of the [Azure Management Portal][Azure Management Portal] to view your storage account names and keys.</span></span> <span data-ttu-id="34a8f-139">O diálogo **Adicionar Conta de Armazenamento** será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="34a8f-139">Your **Add Storage Account** dialog will look similar to the following.</span></span>
   
   ![][ic719497]

4. <span data-ttu-id="34a8f-140">Clique em **OK** para fechar a caixa de diálogo **Adicionar Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-140">Click **OK** to close the **Add Storage Account** dialog.</span></span>

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a><span data-ttu-id="34a8f-141">Para modificar uma conta de armazenamento para usar uma nova chave de acesso</span><span class="sxs-lookup"><span data-stu-id="34a8f-141">To modify a storage account to use a new access key</span></span>
1. <span data-ttu-id="34a8f-142">Na caixa de diálogo **Contas de Armazenamento**, clique na conta de armazenamento que você deseja editar e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-142">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Edit**.</span></span>

2. <span data-ttu-id="34a8f-143">Na caixa de diálogo **Editar Chave de Acesso da Conta do Armazenamento**, modifique o valor **Chave de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-143">Within the **Edit Storage Account Access Key** dialog, modify the **Access Key** value.</span></span>

3. <span data-ttu-id="34a8f-144">Clique em **OK** para fechar a caixa de diálogo **Editar Chave de Acesso da Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-144">Click **OK** to close the **Edit Storage Account Access Key** dialog.</span></span>

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a><span data-ttu-id="34a8f-145">Para remover uma conta de armazenamento da lista mantida no Eclipse</span><span class="sxs-lookup"><span data-stu-id="34a8f-145">To remove a storage account from the list maintained in Eclipse</span></span>
1. <span data-ttu-id="34a8f-146">Na caixa de diálogo **Contas de Armazenamento**, clique na conta de armazenamento que você deseja editar e clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="34a8f-146">Within the **Storage Accounts** dialog, click the storage account that you want to edit and then click **Remove**.</span></span>

2. <span data-ttu-id="34a8f-147">Clique em **OK** quando for solicitado a remover a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="34a8f-147">Click **OK** when prompted to remove the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="34a8f-148">A remoção da conta de armazenamento por meio do diálogo **Contas de Armazenamento** apenas a remove da lista de contas de armazenamento que podem ser exibidas no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="34a8f-148">Removing the storage account through the **Storage Accounts** dialog only removes it from the list of storage accounts viewable within Eclipse.</span></span> <span data-ttu-id="34a8f-149">Ela não remove a conta de armazenamento de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="34a8f-149">It does not remove the storage account from your Azure subscription.</span></span> <span data-ttu-id="34a8f-150">Além disso, a conta de armazenamento pode reaparecer em sua lista, depois que o Eclipse carregar novamente os detalhes de sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="34a8f-150">Additionally, the storage account could appear again in your list after Eclipse reloads the details of your subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="34a8f-151">Consulte também</span><span class="sxs-lookup"><span data-stu-id="34a8f-151">See Also</span></span>
<span data-ttu-id="34a8f-152">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="34a8f-152">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="34a8f-153">[Instalar o Kit de Ferramentas do Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="34a8f-153">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="34a8f-154">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="34a8f-154">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="34a8f-155">Para saber mais sobre como usar o Azure com o Java, confira o [Centro de Desenvolvedores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="34a8f-155">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
