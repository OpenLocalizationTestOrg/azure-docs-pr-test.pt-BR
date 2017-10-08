---
title: aaaUpload um certificado de API de gerenciamento do Azure | Microsoft Docs
description: "Saiba como tooupload athe API de gerenciamento de certificado para Olá Portal clássico do Azure."
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
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="0f2a4-103">Carregar um Certificado de Gerenciamento de API do Gerenciamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0f2a4-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="0f2a4-104">Permitir certificados de gerenciamento que você tooauthenticate com o modelo de implantação clássico Olá fornecida pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="0f2a4-105">Muitos programas e ferramentas (como o Visual Studio ou saudação do SDK do Azure) usam esses configuração tooautomate de certificados e a implantação de vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="0f2a4-106">Portanto, tenha cuidado!</span><span class="sxs-lookup"><span data-stu-id="0f2a4-106">Be careful!</span></span> <span data-ttu-id="0f2a4-107">Esses tipos de certificados que qualquer pessoa que se autentica com eles toomanage assinatura de saudação que estão associados.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="0f2a4-108">Se você quiser obter mais informações sobre certificados do Azure (incluindo a criação de um certificado autoassinado), veja [Visão geral de certificados para Serviços de Nuvem do Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="0f2a4-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="0f2a4-109">Você também pode usar [Active Directory do Azure](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-código do cliente para fins de automação.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="0f2a4-110">Carregar um certificado de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f2a4-110">Upload a management certificate</span></span>
<span data-ttu-id="0f2a4-111">Depois que você tiver um certificado de gerenciamento criado, (arquivo. cer com a chave pública só Olá) você pode carregá-lo no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="0f2a4-112">Quando o certificado hello está disponível no portal de Olá, qualquer pessoa com um certificado correspondente (chave privada) pode se conectar por meio de recursos de saudação API de gerenciamento e acesso de saudação para assinatura Olá associado.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="0f2a4-113">Faça logon no toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f2a4-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="0f2a4-114">Clique em **mais serviços** na lista de serviço do Azure do hello inferior, em seguida, selecione **assinaturas** em Olá _geral_ grupo do serviço.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Menu de assinatura](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="0f2a4-116">Certifique-se de tooselect Olá assinatura correta que você deseja tooassociate com certificado hello.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="0f2a4-117">Depois que você selecionou a assinatura correta hello, pressione **certificados de gerenciamento** em Olá _configurações_ grupo.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Configurações](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="0f2a4-119">Olá pressione **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-119">Press hello **Upload** button.</span></span>

    ![Carregar na página de certificados](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="0f2a4-121">Preencha as informações da caixa de diálogo de saudação e pressione **carregar**.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Configurações](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="0f2a4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f2a4-123">Next steps</span></span>
<span data-ttu-id="0f2a4-124">Agora que você tem um certificado de gerenciamento associado a uma assinatura, você pode (depois de ter instalado o hello correspondência certificado localmente) programaticamente conectar toohello [API REST do modelo de implantação clássico](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizar Olá vários recursos do Azure que também estão associados essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="0f2a4-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
