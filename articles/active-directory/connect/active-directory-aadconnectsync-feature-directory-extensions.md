---
title: "Sincronização do Azure AD Connect: extensões do Directory | Microsoft Docs"
description: "Este tópico descreve o recurso de extensões de diretório no Azure AD Connect."
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
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="f2f45-103">Sincronização do Azure AD Connect: extensões do Directory</span><span class="sxs-lookup"><span data-stu-id="f2f45-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="f2f45-104">Extensões de diretório permite que você estenda o esquema no Azure AD com seus próprios atributos do Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="f2f45-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="f2f45-105">Esse recurso permite criar aplicativos de LOB que consumem atributos que você continua gerenciando localmente.</span><span class="sxs-lookup"><span data-stu-id="f2f45-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="f2f45-106">Esses atributos podem ser consumidos por meio de [extensões de diretório do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) ou [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="f2f45-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="f2f45-107">Você pode ver os atributos disponíveis usando [gerenciador do Azure AD Graph](https://graphexplorer.cloudapp.net) e o [gerenciador do Microsoft Graph](https://graphexplorer2.azurewebsites.net/), respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f2f45-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="f2f45-108">No momento, nenhuma carga de trabalho do Office 365 consome esses atributos.</span><span class="sxs-lookup"><span data-stu-id="f2f45-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="f2f45-109">Configure quais atributos adicionais você deseja sincronizar no caminho de configurações personalizadas no assistente de instalação.</span><span class="sxs-lookup"><span data-stu-id="f2f45-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="f2f45-110">![Assistente de Extensão do Esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="f2f45-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="f2f45-111">A instalação mostra os seguintes atributos, que são candidatos válidos:</span><span class="sxs-lookup"><span data-stu-id="f2f45-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="f2f45-112">Tipos de objeto de Usuário e de Grupo</span><span class="sxs-lookup"><span data-stu-id="f2f45-112">User and Group object types</span></span>
* <span data-ttu-id="f2f45-113">Atributos de valor único: String, Boolean, Integer, Binary</span><span class="sxs-lookup"><span data-stu-id="f2f45-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="f2f45-114">Atributos de vários valores: String, Binary</span><span class="sxs-lookup"><span data-stu-id="f2f45-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="f2f45-115">A lista de atributos é lida do cache de esquema criado durante a instalação do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="f2f45-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="f2f45-116">Se você estendeu o esquema do Active Directory com atributos adicionais, o [esquema deve ser atualizado](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) para que esses novos atributos fiquem visíveis.</span><span class="sxs-lookup"><span data-stu-id="f2f45-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="f2f45-117">Um objeto no Azure AD pode ter até 100 atributos de extensões de diretório.</span><span class="sxs-lookup"><span data-stu-id="f2f45-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="f2f45-118">O comprimento máximo é de 250 caracteres.</span><span class="sxs-lookup"><span data-stu-id="f2f45-118">The max length is 250 characters.</span></span> <span data-ttu-id="f2f45-119">Se um valor de atributo for mais longo, ele será truncado pelo mecanismo de sincronização.</span><span class="sxs-lookup"><span data-stu-id="f2f45-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="f2f45-120">Durante a instalação do Azure AD Connect, é registrado um aplicativo no qual esses atributos estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f2f45-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="f2f45-121">Você pode ver esse aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2f45-121">You can see this application in the Azure portal.</span></span>  
![Aplicativo de extensão do esquema](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="f2f45-123">Esses atributos agora estão disponíveis por meio do Graph: </span><span class="sxs-lookup"><span data-stu-id="f2f45-123">These attributes are now available through Graph:</span></span>  
![Gráfico](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="f2f45-125">Os atributos são prefixados com extension\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="f2f45-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="f2f45-126">O AppClientId tem o mesmo valor para todos os atributos em seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2f45-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2f45-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2f45-127">Next steps</span></span>
<span data-ttu-id="f2f45-128">Saiba mais sobre a configuração de [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="f2f45-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="f2f45-129">Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="f2f45-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
