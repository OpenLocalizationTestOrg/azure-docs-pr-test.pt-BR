---
title: "aaaSetting a credenciais de autenticação de chamada | Microsoft Docs"
description: "Saiba como o serviço de nuvem tootooprovide credenciais que o Visual Studio pode usar tooauthenticate solicitações tooAzure toopublish tooAzure um aplicativo do Visual Studio ou toomonitor um existente. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="30f77-103">Configurando credenciais de autenticação nomeadas</span><span class="sxs-lookup"><span data-stu-id="30f77-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="30f77-104">toopublish tooAzure um aplicativo do Visual Studio ou toomonitor um serviço de nuvem existente, você deve fornecer credenciais que o Visual Studio pode usar tooauthenticate solicitações tooAzure.</span><span class="sxs-lookup"><span data-stu-id="30f77-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="30f77-105">Há vários locais no Visual Studio, onde você pode entrar no tooprovide essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="30f77-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="30f77-106">Por exemplo, de Olá Gerenciador de servidores, você pode abrir o menu de atalho de saudação de saudação **Azure** nó e escolha **conectar tooMicrosoft assinatura do Azure...** . Quando você entrar, informações de assinatura de saudação associadas à sua conta do Azure estão disponíveis no Visual Studio, e nada mais que ter toodo.</span><span class="sxs-lookup"><span data-stu-id="30f77-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="30f77-107">Ferramentas do Azure também oferece suporte a uma maneira mais antiga de fornecer credenciais, Olá assinatura (arquivo. publishsettings).</span><span class="sxs-lookup"><span data-stu-id="30f77-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="30f77-108">Este tópico descreve esse método, que ainda tem suporte no Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="30f77-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="30f77-109">Olá itens a seguir é necessário para autenticação tooAzure:</span><span class="sxs-lookup"><span data-stu-id="30f77-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="30f77-110">Sua ID de assinatura</span><span class="sxs-lookup"><span data-stu-id="30f77-110">Your subscription ID</span></span>
* <span data-ttu-id="30f77-111">Um certificado X.509 v3 válido</span><span class="sxs-lookup"><span data-stu-id="30f77-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="30f77-112">comprimento de saudação da chave do certificado x. 509 v3 da saudação deve ser pelo menos 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="30f77-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="30f77-113">O Azure descartará qualquer certificado que não atenda a esse requisito ou que não seja válido.</span><span class="sxs-lookup"><span data-stu-id="30f77-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="30f77-114">O Visual Studio usa sua ID da assinatura junto com dados de certificado hello como credenciais.</span><span class="sxs-lookup"><span data-stu-id="30f77-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="30f77-115">credenciais apropriadas Olá são referenciadas no arquivo de assinatura de saudação (arquivo. publishsettings), que contém uma chave pública para o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="30f77-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="30f77-116">arquivo de assinatura de saudação pode conter credenciais para mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="30f77-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="30f77-117">Você pode editar as informações de assinatura de saudação da saudação **nova assinatura/editar** caixa de diálogo, conforme explicado mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="30f77-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="30f77-118">Se você quiser toocreate um certificado por conta própria, você pode consultar instruções toohello [criar e carregar um certificado de gerenciamento do Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e, em seguida, carregar manualmente Olá certificado toohello [portal clássico do Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="30f77-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="30f77-119">Essas credenciais que o Visual Studio requer toomanage que seus serviços de nuvem não são Olá mesmas credenciais que são necessária tooauthenticate uma solicitação nos serviços de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="30f77-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="30f77-120">Importar, configurar ou editar as credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30f77-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="30f77-121">Você pode importar, configurar ou modificar suas credenciais de autenticação em Olá **nova assinatura** caixa de diálogo que aparece se você executar Olá ação a seguir:</span><span class="sxs-lookup"><span data-stu-id="30f77-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="30f77-122">Em **Server Explorer**, abra menu de atalho de saudação de saudação **Azure** nó, escolha **gerenciar e assinaturas de filtro...** , escolha Olá **certificados** guia e siga um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="30f77-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="30f77-123">Escolha **importar** tooopen Olá importar assinaturas do Microsoft Azure caixa de diálogo onde você pode baixar o arquivo assinaturas Olá Olá atualmente carregados assinatura, procurar tooits local de download e, em seguida, importá-lo para uso em autenticação.</span><span class="sxs-lookup"><span data-stu-id="30f77-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="30f77-124">Escolha **novo** tooopen Olá nova caixa de diálogo onde você pode configurar uma nova assinatura para uso na autenticação.</span><span class="sxs-lookup"><span data-stu-id="30f77-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="30f77-125">Escolha **editar** (depois de escolher sua assinatura ativa) tooopen Olá Editar caixa de diálogo onde você pode editar uma assinatura existente para uso na autenticação.</span><span class="sxs-lookup"><span data-stu-id="30f77-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="30f77-126">Olá, procedimento a seguir supõe que Olá **nova assinatura** caixa de diálogo é aberta.</span><span class="sxs-lookup"><span data-stu-id="30f77-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="30f77-127">tooset as credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30f77-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="30f77-128">Em Olá **selecionar um certificado existente** para lista de autenticação, selecione um certificado.</span><span class="sxs-lookup"><span data-stu-id="30f77-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="30f77-129">Escolha Olá **Copiar caminho completo do hello** link.</span><span class="sxs-lookup"><span data-stu-id="30f77-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="30f77-130">Olá caminho certificado hello (arquivo. cer) é copiado toohello da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="30f77-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="30f77-131">toopublish seu aplicativo do Azure no Visual Studio, você deve carregar este certificado toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="30f77-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="30f77-132">tooupload Olá certificado toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="30f77-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="30f77-133">Olá abrir [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="30f77-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="30f77-134">Se solicitado, entre no portal de toohello e navegue muito**configurações**, **certificados de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="30f77-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="30f77-135">No painel de certificados de gerenciamento hello, escolha **carregar**.</span><span class="sxs-lookup"><span data-stu-id="30f77-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="30f77-136">Selecione sua assinatura do Azure, cole o caminho completo de saudação do arquivo. cer de saudação que você acabou de criado e escolha **carregar**.</span><span class="sxs-lookup"><span data-stu-id="30f77-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
