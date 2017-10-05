---
title: Pontos de extremidade do Azure
description: "Descreve as configurações dos Pontos de Extremidade do Azure no Kit de ferramentas do Azure para Eclipse."
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
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="8ab2f-103">Pontos de extremidade do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab2f-103">Azure Service Endpoints</span></span>
<span data-ttu-id="8ab2f-104">Os pontos de extremidade do Azure de serviço que determinam se o aplicativo será implantado e gerenciado pela plataforma global do Azure, operado pelo Azure pela 21Vianet na China ou por uma plataforma privada do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="8ab2f-105">A caixa de diálogo **Pontos de Extremidade de Serviço** permite que você especifique quais pontos de extremidade de serviço deseja usar.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="8ab2f-106">Para abrir a caixa de diálogo **Pontos de extremidade de Serviço** no Eclipse, clique em **Janela**, clique em **Preferências**, expanda **Azure** e, em seguida, clique em **Pontos de Extremidade de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="8ab2f-107">A definição do campo **Conjunto Ativo** determina quais pontos de extremidade de serviço do Azure serão usados para os projetos do Azure no seu espaço de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="8ab2f-108">A imagem a seguir mostra a caixa de diálogo **Pontos de Extremidade de Serviço** .</span><span class="sxs-lookup"><span data-stu-id="8ab2f-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="8ab2f-109">Para definir pontos de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="8ab2f-109">To set the service endpoints</span></span>
<span data-ttu-id="8ab2f-110">Na caixa de diálogo **Pontos de Extremidade de Serviço** , execute uma das seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="8ab2f-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="8ab2f-111">Se deseja usar a plataforma global do Azure, na lista suspensa **Conjunto Ativo**, selecione **windowsazure.com** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="8ab2f-112">Se deseja usar o Azure operado pela 21Vianet na China, a partir da lista suspensa **Conjunto Ativo**, selecione **windowsazure.cn (China)** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="8ab2f-113">Se quiser usar uma plataforma privada do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ab2f-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="8ab2f-114">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="8ab2f-115">Uma caixa de diálogo será aberta, informando que a caixa de diálogo **Pontos de Extremidade de Serviço** será fechada e o arquivo de definições de preferência será aberto.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="8ab2f-116">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-116">Click **OK**.</span></span>

  3. <span data-ttu-id="8ab2f-117">No arquivo preferencesets.xml, crie um novo elemento `preferenceset` .</span><span class="sxs-lookup"><span data-stu-id="8ab2f-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="8ab2f-118">Para esse novo elemento, crie atributos `name`, `blob`, `management`, `portalURL` e `publishsettings` e adicione valores para que correspondam à sua plataforma privada do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="8ab2f-119">Você pode usar os valores fornecidos para os elementos `preferenceset` existentes como modelos.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="8ab2f-120">**Observação**: o valor usado para o atributo `blob` deve conter o texto "blob" na URL.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="8ab2f-121">Salve e feche preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="8ab2f-122">Reabra a caixa de diálogo **Pontos de Extremidade de Serviço** .</span><span class="sxs-lookup"><span data-stu-id="8ab2f-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="8ab2f-123">Na lista suspensa **Conjunto Ativo**, selecione o ativo definido que você criou e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="8ab2f-124">Depois de criar seu elemento `preferenceset` da plataforma privada do Azure, você pode alterar os valores atribuídos a ele clicando no botão **Editar** na caixa de diálogo **Ponto de Extremidade de Serviços**.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="8ab2f-125">Se desejar, você também pode criar vários elementos `preferenceset` de plataformas privadas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab2f-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="8ab2f-126">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8ab2f-126">See Also</span></span>
<span data-ttu-id="8ab2f-127">[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8ab2f-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="8ab2f-128">[Instalar o Kit de Ferramentas do Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8ab2f-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="8ab2f-129">[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8ab2f-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="8ab2f-130">Para saber mais sobre como usar o Azure com o Java, confira o [Centro de Desenvolvedores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="8ab2f-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
