---
title: "aaaAzure pontos de extremidade de serviço"
description: "Descreve as configurações de ponto de extremidade de serviço do Azure Olá no hello Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="db7a5-103">Pontos de extremidade do Azure</span><span class="sxs-lookup"><span data-stu-id="db7a5-103">Azure Service Endpoints</span></span>
<span data-ttu-id="db7a5-104">Pontos de extremidade de serviço do Azure determinam que se o aplicativo é implantado tooand gerenciado pela plataforma global do Azure da saudação, Azure operado pela 21Vianet na China ou uma particular plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="db7a5-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="db7a5-105">Olá **pontos de extremidade de serviço** caixa de diálogo permite toospecify que você deseja toouse de pontos de extremidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="db7a5-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="db7a5-106">Olá tooopen **pontos de extremidade de serviço** caixa de diálogo, no Eclipse, clique em **janela**, clique em **preferências**, expanda **Azure**e, em seguida, clique em **Pontos de extremidade de serviço**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="db7a5-107">Saudação de configuração **conjunto ativo** campo determina qual serviço do Azure, pontos de extremidade serão usados para hello Azure projetos no seu espaço de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="db7a5-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="db7a5-108">Veja a seguir de Olá Olá **pontos de extremidade de serviço** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db7a5-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="db7a5-109">pontos de extremidade do serviço tooset Olá</span><span class="sxs-lookup"><span data-stu-id="db7a5-109">tooset hello service endpoints</span></span>
<span data-ttu-id="db7a5-110">Em Olá **pontos de extremidade de serviço** caixa de diálogo, execute uma das seguintes ações de saudação:</span><span class="sxs-lookup"><span data-stu-id="db7a5-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="db7a5-111">Se você quiser toouse Olá plataforma global do Azure, de saudação **conjunto ativo** lista suspensa, selecione **windowsazure.com** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="db7a5-112">Se você quiser que o Azure operado pela 21Vianet na China, de saudação do toouse **conjunto ativo** lista suspensa, selecione **windowsazure.cn (China)** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="db7a5-113">Se você desejar toouse uma plataforma privada do Azure:</span><span class="sxs-lookup"><span data-stu-id="db7a5-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="db7a5-114">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="db7a5-115">Abre uma caixa de diálogo, informando que Olá **pontos de extremidade de serviço** caixa de diálogo será fechada e o arquivo de definições de preferência Olá será aberto.</span><span class="sxs-lookup"><span data-stu-id="db7a5-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="db7a5-116">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-116">Click **OK**.</span></span>

  3. <span data-ttu-id="db7a5-117">No arquivo do hello preferencesets.xml, crie um novo `preferenceset` elemento.</span><span class="sxs-lookup"><span data-stu-id="db7a5-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="db7a5-118">Para esse novo elemento, criar `name`, `blob`, `management`, `portalURL` e `publishsettings` atributos e adicionar valores para eles que correspondam a plataforma do tooyour privada do Azure.</span><span class="sxs-lookup"><span data-stu-id="db7a5-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="db7a5-119">Você pode usar valores hello fornecidos Olá existentes `preferenceset` elementos como modelos.</span><span class="sxs-lookup"><span data-stu-id="db7a5-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="db7a5-120">**Observação**: Olá valor usado para Olá `blob` atributo deve conter o texto de saudação "blob" na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="db7a5-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="db7a5-121">Salve e feche preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="db7a5-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="db7a5-122">Reabra Olá **pontos de extremidade de serviço** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db7a5-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="db7a5-123">De saudação **conjunto ativo** lista suspensa, selecione Olá ativo definido que você criou e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="db7a5-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="db7a5-124">Depois de criar sua plataforma privada do Azure `preferenceset` elemento, você pode alterar Olá valores atribuídos tooit clicando Olá **editar** botão Olá **ponto de extremidade de serviços** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="db7a5-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="db7a5-125">Se desejar, você também pode criar vários elementos `preferenceset` de plataformas privadas do Azure.</span><span class="sxs-lookup"><span data-stu-id="db7a5-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="db7a5-126">Consulte também</span><span class="sxs-lookup"><span data-stu-id="db7a5-126">See Also</span></span>
<span data-ttu-id="db7a5-127">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="db7a5-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="db7a5-128">[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="db7a5-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="db7a5-129">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="db7a5-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="db7a5-130">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="db7a5-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
