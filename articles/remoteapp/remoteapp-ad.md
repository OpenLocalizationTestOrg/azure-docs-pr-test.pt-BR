---
title: Requisitos do Azure AD + Active Directory para o Azure RemoteApp | Microsoft Docs
description: Saiba como configurar o Active Directory para trabalhar com o Azure RemoteApp.
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
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a><span data-ttu-id="b2042-103">Requisitos do AD do Azure + Active Directory para o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b2042-103">Azure AD + Active Directory requirements for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b2042-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="b2042-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b2042-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b2042-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b2042-106">Para a coleção híbrida do Azure RemoteApp ou para uma coleção na nuvem que você deseja federar usando o AD Connect, você precisa fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b2042-106">For your Azure RemoteApp hybrid collection or for a cloud collection that you want to federate using AD Connect, you need to do the following.</span></span>

### <a name="connect-azure-ad-and-active-directory"></a><span data-ttu-id="b2042-107">Conecte o AD do Azure e o Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2042-107">Connect Azure AD and Active Directory</span></span>
<span data-ttu-id="b2042-108">Se desejar conectar seu locatário do AD do Azure e seus ambientes locais do Active Directory, use o AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b2042-108">If you want to connect your Azure AD tenant and your on-premises Active Directory environments, use AD Connect.</span></span> <span data-ttu-id="b2042-109">Levará apenas [quatro cliques](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) para conectar os dois diretórios.</span><span class="sxs-lookup"><span data-stu-id="b2042-109">It will take you only [4 clicks](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) to connect the two directories.</span></span>

<span data-ttu-id="b2042-110">Observação - a sincronização de diretórios é necessária para coleções híbridas.</span><span class="sxs-lookup"><span data-stu-id="b2042-110">Note - Directory synchronization is required for hybrid collections.</span></span>

### <a name="make-sure-your-domaincom-match"></a><span data-ttu-id="b2042-111">Certifique-se de que o "@domain.com" corresponda</span><span class="sxs-lookup"><span data-stu-id="b2042-111">Make sure your "@domain.com" match</span></span>
<span data-ttu-id="b2042-112">Antes de começar, lembre-se de que o UPN da floresta local corresponde ao sufixo do seu domínio do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2042-112">Before you get started, make sure that the UPN for your on-premises forest matches the suffix of your Azure AD domain.</span></span> 

<span data-ttu-id="b2042-113">Depois de configurar o sufixo de domínio UPN no Azure AD, todos os usuários que fizerem logon no Azure RemoteApp farão logon como "user@<the suffix you set up>".</span><span class="sxs-lookup"><span data-stu-id="b2042-113">After you set up the UPN domain suffix in Azure AD, all users logging into Azure RemoteApp will log in as "user@<the suffix you set up>."</span></span> <span data-ttu-id="b2042-114">Certifique-se de que os usuários também podem fazer logon com o mesmo user@suffix no domínio local.</span><span class="sxs-lookup"><span data-stu-id="b2042-114">Make sure that users can also log in with the same user@suffix into the on-premises domain.</span></span> <span data-ttu-id="b2042-115">Em alguns casos, é possível configurar um nome de domínio no AD do Azure, ao mesmo tempo que você especifica um sufixo de domínio diferente para o usuário local.</span><span class="sxs-lookup"><span data-stu-id="b2042-115">In certain cases you can set up one domain name in Azure AD while specifying a different domain suffix for the user on-prem.</span></span> <span data-ttu-id="b2042-116">Nesse caso, seus usuários não poderão se conectar a nenhum computador ou recurso ingressado no domínio por meio do Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b2042-116">In this case, your users won't be able to connect to any domain-joined computers or resources through Azure RemoteApp.</span></span>

<span data-ttu-id="b2042-117">Por exemplo, se você configurar o sufixo de domínio UPN no AAD como contoso.com mas alguns usuários locais/no AD estiverem configurados para fazer logon em @contoso.uk, esses usuários não poderão fazer logon corretamente na coleção ARA.</span><span class="sxs-lookup"><span data-stu-id="b2042-117">For example, if you set up your UPN domain suffix in AAD as contoso.com, but some users on premises/AD are configured to log in with @contoso.uk, then those users will not be able to correctly log into the ARA collection.</span></span> <span data-ttu-id="b2042-118">Os UPNs dos usuários no AAD e no AD devem ser iguais para que o logon seja possível.</span><span class="sxs-lookup"><span data-stu-id="b2042-118">Users UPN in AAD and AD must be the same for the login to be possible”</span></span>

### <a name="create-objects-for-azure-remoteapp"></a><span data-ttu-id="b2042-119">Criar objetos para o Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b2042-119">Create objects for Azure RemoteApp</span></span>
<span data-ttu-id="b2042-120">Você também precisará criar os seguintes objetos locais do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="b2042-120">You also need to create the following on-premises Active Directory objects:</span></span>

* <span data-ttu-id="b2042-121">Uma conta de serviço para fornecer acesso aos recursos do domínio para programas RemoteApp unindo os pontos de extremidade RDSH ao domínio local.</span><span class="sxs-lookup"><span data-stu-id="b2042-121">A service account to provide access to domain resources for RemoteApp programs by joining RDSH end points to the on-premises domain.</span></span>
* <span data-ttu-id="b2042-122">Uma OU (unidade organizacional) para conter objetos de computador do RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b2042-122">An Organizational Unit (OU) to contain RemoteApp machine objects.</span></span> <span data-ttu-id="b2042-123">Uso da OU é recomendável (mas não obrigatório) para isolar as contas e as políticas que você usará com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b2042-123">Use of the OU is recommended (but not required) to isolate the accounts and policies you will use with RemoteApp.</span></span>

<span data-ttu-id="b2042-124">Você precisa desses dois objetos ao criar sua coleção do RemoteApp, portanto lembre-se de realizar essas etapas primeiro.</span><span class="sxs-lookup"><span data-stu-id="b2042-124">You need both of these objects when you create your RemoteApp collection, so be sure to do these steps first.</span></span>

