---
title: "Sincronização do Azure AD Connect: extensões do Directory | Microsoft Docs"
description: "Este tópico descreve o recurso de extensões de diretório Olá no Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="b04e4-103">Sincronização do Azure AD Connect: extensões do Directory</span><span class="sxs-lookup"><span data-stu-id="b04e4-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="b04e4-104">Extensões de diretório permite que você tooextend esquema de saudação no Azure AD com seus próprios atributos do Active Directory no local.</span><span class="sxs-lookup"><span data-stu-id="b04e4-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="b04e4-105">Esse recurso permite que aplicativos LOB toobuild consumindo atributos continuar toomanage local.</span><span class="sxs-lookup"><span data-stu-id="b04e4-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="b04e4-106">Esses atributos podem ser consumidos por meio de [extensões de diretório do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="b04e4-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="b04e4-107">Você pode ver Olá atributos disponíveis usando [explorer do Azure AD Graph](https://graphexplorer.cloudapp.net) e [explorer Microsoft Graph](https://graphexplorer2.azurewebsites.net/) respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b04e4-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="b04e4-108">No momento, nenhuma carga de trabalho do Office 365 consome esses atributos.</span><span class="sxs-lookup"><span data-stu-id="b04e4-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="b04e4-109">Configurar quais atributos adicionais você deseja toosynchronize no caminho de configurações personalizadas de saudação no Assistente de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04e4-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="b04e4-110">![Assistente de Extensão do Esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="b04e4-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="b04e4-111">instalação de saudação mostra Olá atributos, que são candidatas válidas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b04e4-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="b04e4-112">Tipos de objeto de Usuário e de Grupo</span><span class="sxs-lookup"><span data-stu-id="b04e4-112">User and Group object types</span></span>
* <span data-ttu-id="b04e4-113">Atributos de valor único: String, Boolean, Integer, Binary</span><span class="sxs-lookup"><span data-stu-id="b04e4-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="b04e4-114">Atributos de vários valores: String, Binary</span><span class="sxs-lookup"><span data-stu-id="b04e4-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="b04e4-115">lista de saudação de atributos é lido no cache de esquema de saudação criado durante a instalação do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b04e4-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="b04e4-116">Se você tiver estendido o esquema do Active Directory Olá com atributos adicionais, Olá [esquema deve ser atualizado](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) antes que esses novos atributos são visíveis.</span><span class="sxs-lookup"><span data-stu-id="b04e4-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="b04e4-117">Um objeto no AD do Azure pode ter atributos de extensões de diretório too100.</span><span class="sxs-lookup"><span data-stu-id="b04e4-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="b04e4-118">comprimento máximo de saudação é de 250 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b04e4-118">hello max length is 250 characters.</span></span> <span data-ttu-id="b04e4-119">Se um valor de atributo for maior, em seguida, ele será truncado pelo mecanismo de sincronização de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04e4-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="b04e4-120">Durante a instalação do Azure AD Connect, é registrado um aplicativo no qual esses atributos estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b04e4-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="b04e4-121">Você pode ver este aplicativo no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="b04e4-121">You can see this application in hello Azure portal.</span></span>  
![Aplicativo de extensão do esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="b04e4-123">Esses atributos agora estão disponíveis por meio do Graph: </span><span class="sxs-lookup"><span data-stu-id="b04e4-123">These attributes are now available through Graph:</span></span>  
![Gráfico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="b04e4-125">atributos de saudação são prefixados com extensão\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="b04e4-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="b04e4-126">Olá AppClientId tem Olá mesmo valor para todos os atributos no seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b04e4-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b04e4-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b04e4-127">Next steps</span></span>
<span data-ttu-id="b04e4-128">Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.</span><span class="sxs-lookup"><span data-stu-id="b04e4-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="b04e4-129">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b04e4-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
