---
title: Habilitando o Azure Active Directory Identity Protection | Microsoft Docs
description: Saiba como habilitar o Azure Active Directory Identity Protection.
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="aeeb1-104">Habilitando o Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="aeeb1-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="aeeb1-105">O Azure Active Directory Identity Protection é um novo recurso que fornece uma exibição consolidada de atividades de entrada suspeitas e possíveis vulnerabilidades e, com notificações, recomendações de correção e políticas baseadas em risco, ajuda você a proteger sua empresa.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="aeeb1-106">O serviço detecta atividades suspeitas para identidades de usuário final e com privilégios (administrador) com base em sinais como ataques de força bruta, vazamento de credenciais, entradas de locais desconhecidos, dispositivos infectados, de modo a proteger essas atividades em tempo real.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="aeeb1-107">E o que é mais importante, com base nessas atividades suspeitas, uma severidade de risco de usuário é calculada e as políticas baseadas em risco podem ser configuradas e proteger automaticamente as identidades de sua organização.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="aeeb1-108">Para obter mais detalhes, confira [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="aeeb1-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="aeeb1-109">Este tópico mostra como habilitar o Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="aeeb1-110">Etapas para habilitar o Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="aeeb1-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="aeeb1-111">[Entre](https://ms.portal.azure.com/) no portal do Azure como administrador global.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="aeeb1-112">No Portal do Azure, clique em **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="aeeb1-113">![Criar](./media/active-directory-identityprotection-enable/01.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="aeeb1-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="aeeb1-114">Na lista de aplicativos, escolha **Segurança + Identidade**.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="aeeb1-115">![Criar](./media/active-directory-identityprotection-enable/02.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="aeeb1-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="aeeb1-116">Clique em **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="aeeb1-117">![Criar](./media/active-directory-identityprotection-enable/03.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="aeeb1-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="aeeb1-118">Na folha **Azure AD Identity Protection**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aeeb1-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="aeeb1-119">![Criar](./media/active-directory-identityprotection-enable/04.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="aeeb1-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="aeeb1-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aeeb1-120">Next Steps</span></span>
* [<span data-ttu-id="aeeb1-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="aeeb1-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

