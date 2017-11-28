---
title: aaaAccess aplicativos de Proxy de aplicativo do Azure AD em equipes | Microsoft Docs
description: Use Proxy de aplicativo do Azure AD tooaccess seu aplicativo local por meio de Teams da Microsoft.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="e46e2-103">Acessar seus aplicativos locais por meio do Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e46e2-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="e46e2-104">Azure Active Directory Application Proxy fornece single sign-on tooon aplicativos locais, independentemente de onde você está e Teams Microsoft simplifica seus esforços de colaboração em um único local.</span><span class="sxs-lookup"><span data-stu-id="e46e2-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="e46e2-105">Integrando Olá dois juntos significa que os usuários podem ser produtivos com seus colegas em qualquer situação.</span><span class="sxs-lookup"><span data-stu-id="e46e2-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="e46e2-106">Os usuários poderão adicionar canais de equipes de tootheir de aplicativos de nuvem [usando guias](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), mas o que acontece se esse site do SharePoint ou a ferramenta de planejamento, todos eles usarão é hospedado no local?</span><span class="sxs-lookup"><span data-stu-id="e46e2-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="e46e2-107">Proxy de aplicativo é a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="e46e2-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="e46e2-108">Eles podem adicionar aplicativos publicados pelo Proxy de aplicativo tootheir canais usando Olá URLs externas mesmo que eles sempre usam tooaccess seus aplicativos remotamente.</span><span class="sxs-lookup"><span data-stu-id="e46e2-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="e46e2-109">E porque o Proxy de aplicativo autentica por meio do Active Directory do Azure, Olá ocorre mesmo única experiência de logon.</span><span class="sxs-lookup"><span data-stu-id="e46e2-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="e46e2-110">Instalar o conector de Proxy de aplicativo hello e publicar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e46e2-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="e46e2-111">Se você ainda não o fez, [configurar o Proxy de aplicativo para seu locatário e instalar o conector Olá](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="e46e2-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="e46e2-112">Em seguida, [publique seu aplicativo local](application-proxy-publish-azure-portal.md) para acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="e46e2-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="e46e2-113">Quando você estiver publicando um aplicativo hello, tome nota da URL externa Olá porque os usuários finais precisam essas informações quando adicionarem Olá tooTeams de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e46e2-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="e46e2-114">Se já tiver seus aplicativos publicados, mas não se lembra de suas URLs externas, consultá-los em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e46e2-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e46e2-115">Entrar e navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos** > Selecionar seu aplicativo > **Proxy de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e46e2-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="e46e2-116">Adicionar tooTeams seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e46e2-116">Add your app tooTeams</span></span>

<span data-ttu-id="e46e2-117">Depois de publicar o aplicativo hello por meio do Proxy de aplicativo, informe aos usuários que eles podem adicioná-lo como uma guia diretamente em seus canais de equipes.</span><span class="sxs-lookup"><span data-stu-id="e46e2-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="e46e2-118">Faça com que eles sigam estas três etapas:</span><span class="sxs-lookup"><span data-stu-id="e46e2-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="e46e2-119">Navegue toohello equipes de canal onde você deseja tooadd este aplicativo e selecionem  **+**  tooadd uma guia.</span><span class="sxs-lookup"><span data-stu-id="e46e2-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Selecione Adicionar uma guia](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="e46e2-121">Selecione **site** de opções da guia hello.</span><span class="sxs-lookup"><span data-stu-id="e46e2-121">Select **Website** from hello tab options.</span></span>

   ![Adicionar um site](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="e46e2-123">Dê um nome de guia hello e definir a URL externa do Proxy de aplicativo hello URL toohello.</span><span class="sxs-lookup"><span data-stu-id="e46e2-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Configurar a URL e o nome da guia](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="e46e2-125">Depois que um membro de uma equipe adiciona guia hello, ele mostra todos no canal de saudação.</span><span class="sxs-lookup"><span data-stu-id="e46e2-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="e46e2-126">Todos os usuários que têm acesso toohello aplicativo obtém acesso de logon único com credenciais Olá usam para Teams da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e46e2-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="e46e2-127">Todos os usuários que não têm acesso toohello aplicativo verão a guia Olá em equipes, mas são bloqueados até que você conceder a eles permissões toohello local aplicativo e Olá versão publicada portal do Azure do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e46e2-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e46e2-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e46e2-128">Next steps</span></span>

- <span data-ttu-id="e46e2-129">Saiba como muito[publicar sites do SharePoint local](application-proxy-enable-remote-access-sharepoint.md) com Proxy de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e46e2-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="e46e2-130">Configurar seu aplicativos toouse [domínios personalizados](active-directory-application-proxy-custom-domains.md) para sua URL externa.</span><span class="sxs-lookup"><span data-stu-id="e46e2-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
