---
title: Carregar um Certificado de API de Gerenciamento do Azure | Microsoft Docs
description: "Saiba como carregar o certificado de API de Gerenciamento para o Portal Clássico do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="af2f4-103">Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="af2f4-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="af2f4-104">Os certificados de gerenciamento permitem que você autentique com o modelo de implantação clássico fornecido pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="af2f4-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="af2f4-105">Muitos programas e ferramentas (como o Visual Studio ou o SDK do Azure) usam esses certificados para automatizar a configuração e a implantação de diversos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="af2f4-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="af2f4-106">Portanto, tenha cuidado!</span><span class="sxs-lookup"><span data-stu-id="af2f4-106">Be careful!</span></span> <span data-ttu-id="af2f4-107">Esses tipos de certificados permitem que qualquer pessoa que os utilize para autenticação gerencie a assinatura à qual eles estão associados.</span><span class="sxs-lookup"><span data-stu-id="af2f4-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="af2f4-108">Se você quiser obter mais informações sobre certificados do Azure (incluindo a criação de um certificado autoassinado), veja [Visão geral de certificados para Serviços de Nuvem do Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="af2f4-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="af2f4-109">Você também pode usar o [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) para autenticar o código cliente, para fins de automação.</span><span class="sxs-lookup"><span data-stu-id="af2f4-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="af2f4-110">Carregar um certificado de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="af2f4-110">Upload a management certificate</span></span>
<span data-ttu-id="af2f4-111">Após criar um certificado de gerenciamento (arquivo .cer somente com a chave pública), você poderá carregá-lo no portal.</span><span class="sxs-lookup"><span data-stu-id="af2f4-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="af2f4-112">Quando o certificado estiver disponível no portal, qualquer pessoa com um certificado correspondente (chave privada) pode conectar-se por meio da API de Gerenciamento e acessar os recursos para a assinatura associada.</span><span class="sxs-lookup"><span data-stu-id="af2f4-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="af2f4-113">Faça logon no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af2f4-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="af2f4-114">Clique em **Mais serviços** na lista de serviços inferior do Azure e selecione **Assinaturas** no grupo de serviços _Geral_.</span><span class="sxs-lookup"><span data-stu-id="af2f4-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Menu de assinatura](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="af2f4-116">Selecione a assinatura correta à qual você deseja associar um certificado.</span><span class="sxs-lookup"><span data-stu-id="af2f4-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="af2f4-117">Depois que você tiver selecionado a assinatura correta, pressione **Certificados de gerenciamento** no grupo _Configurações_.</span><span class="sxs-lookup"><span data-stu-id="af2f4-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![Configurações](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="af2f4-119">Pressione o botão **Carregar** .</span><span class="sxs-lookup"><span data-stu-id="af2f4-119">Press the **Upload** button.</span></span>

    ![Carregar na página de certificados](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="af2f4-121">Preencha as informações de caixa de diálogo e pressione **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="af2f4-121">Fill out the dialog information and press **Upload**.</span></span>

    ![Configurações](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="af2f4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="af2f4-123">Next steps</span></span>
<span data-ttu-id="af2f4-124">Agora que você tem um certificado de gerenciamento associado a uma assinatura, você pode (depois de ter instalado localmente o certificado correspondente) conectar-se programaticamente à [API REST do modelo de implantação clássico](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizar os diversos recursos do Azure que também estão associados à assinatura.</span><span class="sxs-lookup"><span data-stu-id="af2f4-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
