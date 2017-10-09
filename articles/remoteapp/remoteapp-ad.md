---
title: aaaAzure AD + requisitos do Active Directory do Azure RemoteApp | Microsoft Docs
description: Saiba como tooset backup toowork do Active Directory com o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="e39f6-103">Requisitos do AD do Azure + Active Directory para o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e39f6-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e39f6-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="e39f6-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e39f6-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="e39f6-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e39f6-106">Para sua coleção do RemoteApp híbrida ou para uma coleção de nuvem que você deseja toofederate usando AD Connect, é necessário a seguir Olá toodo.</span><span class="sxs-lookup"><span data-stu-id="e39f6-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want toofederate using AD Connect, you need toodo hello following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="e39f6-107">Conecte o AD do Azure e o Active Directory</span><span class="sxs-lookup"><span data-stu-id="e39f6-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="e39f6-108">Se você quiser tooconnect seu locatário do AD do Azure e seus ambientes do Active Directory local, use AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e39f6-108">If you want tooconnect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="e39f6-109">Levará apenas [4 cliques](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Olá dois diretórios.</span><span class="sxs-lookup"><span data-stu-id="e39f6-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect hello two directories.</span></span>

<span data-ttu-id="e39f6-110">Observação - a sincronização de diretórios é necessária para coleções híbridas.</span><span class="sxs-lookup"><span data-stu-id="e39f6-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="e39f6-111">Certifique-se de que o "@domain.com" corresponda</span><span class="sxs-lookup"><span data-stu-id="e39f6-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="e39f6-112">Antes de começar, certifique-se que hello UPN para o sufixo de saudação do local floresta correspondências de seu domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e39f6-112">Before you get started, make sure that hello UPN for your on-premises forest matches hello suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="e39f6-113">Depois de configurar o sufixo de domínio do UPN Olá no AD do Azure, todos os usuários que fizerem logon no Azure RemoteApp fará logon como "usuário @<hello suffix you set up>."</span><span class="sxs-lookup"><span data-stu-id="e39f6-113">After you set up hello UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<hello suffix you set up>."</span></span> <span data-ttu-id="e39f6-114">Certifique-se de que os usuários podem também fazer logon com hello mesmo user@suffix no domínio local de saudação.</span><span class="sxs-lookup"><span data-stu-id="e39f6-114">Make sure that users can also log in with hello same user@suffix into hello on-premises domain.</span></span> <span data-ttu-id="e39f6-115">Em alguns casos você pode configurar um nome de domínio no AD do Azure ao especificar um sufixo de domínio diferente para Olá usuário-local.</span><span class="sxs-lookup"><span data-stu-id="e39f6-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for hello user on-prem.</span></span> <span data-ttu-id="e39f6-116">Nesse caso, os usuários não será capaz de tooconnect tooany computadores do domínio ou os recursos por meio do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e39f6-116">In this case, your users won't be able tooconnect tooany domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="e39f6-117">Por exemplo, se você configurar o sufixo de domínio do UPN no AAD como contoso.com, mas alguns usuários no local/AD toolog configurado com @contoso.uk, em seguida, os usuários não será capaz de toocorrectly log em Olá coleção ARA.</span><span class="sxs-lookup"><span data-stu-id="e39f6-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured toolog in with @contoso.uk, then those users will not be able toocorrectly log into hello ARA collection.</span></span> <span data-ttu-id="e39f6-118">Os usuários que deve ser UPN no AAD e AD hello mesmo para possíveis de toobe logon hello"</span><span class="sxs-lookup"><span data-stu-id="e39f6-118">Users UPN in AAD and AD must be hello same for hello login toobe possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="e39f6-119">Criar objetos para o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e39f6-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="e39f6-120">Você também precisa Olá toocreate objetos do Active Directory no local a seguir:</span><span class="sxs-lookup"><span data-stu-id="e39f6-120">You also need toocreate hello following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="e39f6-121">Uma conta de serviço tooprovide acesso toodomain recursos para os programas RemoteApp unindo o domínio de local de toohello RDSH pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e39f6-121">A service account tooprovide access toodomain resources for RemoteApp programs by joining RDSH end points toohello on-premises domain.</span></span>
* <span data-ttu-id="e39f6-122">Objetos de computador uma UO (unidade organizacional) toocontain RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e39f6-122">An Organizational Unit (OU) toocontain RemoteApp machine objects.</span></span> <span data-ttu-id="e39f6-123">Uso de saudação UO é recomendado (mas não obrigatório) tooisolate Olá contas e políticas que você usará com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e39f6-123">Use of hello OU is recommended (but not required) tooisolate hello accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="e39f6-124">Você precisará de ambos esses objetos ao criar sua coleção do RemoteApp, portanto, ser toodo-se de que essas etapas primeiro.</span><span class="sxs-lookup"><span data-stu-id="e39f6-124">You need both of these objects when you create your RemoteApp collection, so be sure toodo these steps first.</span></span>

