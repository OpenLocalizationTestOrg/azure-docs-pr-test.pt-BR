---
title: "Configurando credenciais de autenticação nomeadas | Microsoft Docs"
description: "Saiba como fornecer credenciais que o Visual Studio pode usar para autenticar solicitações no Azure para publicar um aplicativo no Azure do Visual Studio ou para monitorar um serviço de nuvem existente. "
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
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="29dd3-103">Configurando credenciais de autenticação nomeadas</span><span class="sxs-lookup"><span data-stu-id="29dd3-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="29dd3-104">Para publicar um aplicativo no Azure do Visual Studio ou para monitorar um serviço de nuvem existente, você deve fornecer credenciais que o Visual Studio pode usar para autenticar solicitações no Azure.</span><span class="sxs-lookup"><span data-stu-id="29dd3-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="29dd3-105">Existem diversos lugares no Visual Studio nos quais você pode entrar para fornecer essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="29dd3-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="29dd3-106">Por exemplo, no Gerenciador de Servidores, você pode abrir o menu de atalho do nó do **Azure** e escolher **Conectar-se à Assinatura do Microsoft Azure...**. Quando você entra, as informações de assinatura associadas à sua conta do Azure estão disponíveis no Visual Studio e não é necessário fazer mais nada.</span><span class="sxs-lookup"><span data-stu-id="29dd3-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="29dd3-107">As Ferramentas do Azure também dão suporte a uma maneira mais antiga de fornecer credenciais, usando o arquivo de assinatura (arquivo .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="29dd3-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="29dd3-108">Este tópico descreve esse método, que ainda tem suporte no Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="29dd3-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="29dd3-109">Os itens a seguir são necessários para autenticação no Azure:</span><span class="sxs-lookup"><span data-stu-id="29dd3-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="29dd3-110">Sua ID de assinatura</span><span class="sxs-lookup"><span data-stu-id="29dd3-110">Your subscription ID</span></span>
* <span data-ttu-id="29dd3-111">Um certificado X.509 v3 válido</span><span class="sxs-lookup"><span data-stu-id="29dd3-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="29dd3-112">O comprimento da chave do certificado X.509 v3 deve ser pelo menos 2.048 bits.</span><span class="sxs-lookup"><span data-stu-id="29dd3-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="29dd3-113">O Azure descartará qualquer certificado que não atenda a esse requisito ou que não seja válido.</span><span class="sxs-lookup"><span data-stu-id="29dd3-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="29dd3-114">O Visual Studio usa sua ID da assinatura junto com os dados do certificado como credenciais.</span><span class="sxs-lookup"><span data-stu-id="29dd3-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="29dd3-115">As credenciais apropriadas são referenciadas no arquivo de assinatura (arquivo .publishsettings), que contém uma chave pública para o certificado.</span><span class="sxs-lookup"><span data-stu-id="29dd3-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="29dd3-116">O arquivo de assinatura pode conter credenciais para mais de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="29dd3-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="29dd3-117">Você pode editar as informações de assinatura da caixa de diálogo **Nova/Editar Assinatura** , conforme explicado posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="29dd3-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="29dd3-118">Se você deseja criar um certificado por conta própria, pode consultar as instruções em [Criar e carregar um certificado de gerenciamento do Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e carregar manualmente o certificado para o [Portal Clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="29dd3-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="29dd3-119">Essas credenciais que o Visual Studio requer para gerenciar seus serviços de nuvem não são as mesmas credenciais necessárias para autenticar uma solicitação nos serviços de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="29dd3-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="29dd3-120">Importar, configurar ou editar as credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29dd3-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="29dd3-121">Você pode importar, configurar ou modificar suas credenciais de autenticação na nova caixa de diálogo **Assinatura** que aparece se você realizar uma das seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="29dd3-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="29dd3-122">Em **Gerenciador de Servidores**, abra o menu de atalho para o nó do **Azure**, escolha **Gerenciar e Filtrar Assinaturas...**, escolha a guia **Certificados** e execute um dos procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="29dd3-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="29dd3-123">Escolha **Importar** para abrir a caixa de diálogo Importar Assinaturas do Microsoft Azure onde você pode baixar o arquivo de assinaturas da assinatura carregada atualmente, navegue até o local de download e, depois, importe-o para uso na autenticação.</span><span class="sxs-lookup"><span data-stu-id="29dd3-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="29dd3-124">Escolha **Novo** para abrir a caixa de diálogo Nova Assinatura onde você pode configurar uma nova assinatura para uso em autenticação.</span><span class="sxs-lookup"><span data-stu-id="29dd3-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="29dd3-125">Escolha **Editar** (depois de escolher sua assinatura ativa) para abrir a caixa de diálogo Editar Assinatura onde você pode editar uma assinatura existente para uso em autenticação.</span><span class="sxs-lookup"><span data-stu-id="29dd3-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="29dd3-126">O procedimento a seguir pressupõe que a caixa de diálogo **Nova Assinatura** está aberta.</span><span class="sxs-lookup"><span data-stu-id="29dd3-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="29dd3-127">Para configurar credenciais de autenticação no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="29dd3-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="29dd3-128">Na lista **Selecionar um certificado existente para autenticação** , escolha um certificado.</span><span class="sxs-lookup"><span data-stu-id="29dd3-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="29dd3-129">Escolha o link **Copiar o caminho completo**.</span><span class="sxs-lookup"><span data-stu-id="29dd3-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="29dd3-130">O caminho para o certificado (arquivo .cer) é copiado para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="29dd3-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="29dd3-131">Para publicar seu aplicativo do Azure do Visual Studio, você deve carregar esse certificado no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="29dd3-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="29dd3-132">Para carregar o certificado no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="29dd3-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="29dd3-133">Abra o [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="29dd3-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="29dd3-134">Se receber uma solicitação, entre no portal e navegue até **Configurações**, **Certificados de Gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="29dd3-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="29dd3-135">No painel Certificados de gerenciamento, escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="29dd3-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="29dd3-136">Selecione sua assinatura do Azure, cole o caminho completo do arquivo .cer que você acabou de criar e escolha **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="29dd3-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
