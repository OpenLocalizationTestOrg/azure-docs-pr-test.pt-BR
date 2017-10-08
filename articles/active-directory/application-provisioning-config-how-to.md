---
title: "aaaHow tooconfigure usuário Provisionando o aplicativo de galeria tooan AD do Azure | Microsoft Docs"
description: "Como você pode rapidamente configurar conta de usuário avançado, provisionamento e desprovisionamento tooapplications já está listado no hello Galeria de aplicativos do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a><span data-ttu-id="88505-103">Como usuário tooconfigure Provisionando o aplicativo de galeria tooan AD do Azure</span><span class="sxs-lookup"><span data-stu-id="88505-103">How tooconfigure user provisioning tooan Azure AD Gallery application</span></span>

<span data-ttu-id="88505-104">*Provisionamento de conta de usuário* é Olá ato de criar, atualizar e/ou desabilitando os registros de conta de usuário no repositório de perfil de usuário local do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88505-104">*User account provisioning* is hello act of creating, updating, and/or disabling user account records in an application’s local user profile store.</span></span> <span data-ttu-id="88505-105">A maioria dos aplicativos SaaS e nuvem armazenam a função hello usuários e permissões em seu próprio armazenamento de perfil de usuário local e a presença de um registro de usuário em seu repositório local é *necessária* para toowork única de logon e acesso.</span><span class="sxs-lookup"><span data-stu-id="88505-105">Most cloud and SaaS applications store hello users role and permissions in their own local user profile store, and presence of such a user record in their local store is *required* for single sign-on and access toowork.</span></span>

<span data-ttu-id="88505-106">No portal do Azure de Olá, Olá **provisionamento** guia no painel de navegação à esquerda de saudação de um aplicativo Empresarial exibe quais modos de provisionamento têm suporte para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88505-106">In hello Azure portal, hello **Provisioning** tab in hello left navigation pane for an Enterprise App displays what provisioning modes are supported for that app.</span></span> <span data-ttu-id="88505-107">Existem dois valores válidos:</span><span class="sxs-lookup"><span data-stu-id="88505-107">This can be one of two values:</span></span>

## <a name="configuring-an-application-for-manual-provisioning"></a><span data-ttu-id="88505-108">Configurar um aplicativo para o provisionamento manual</span><span class="sxs-lookup"><span data-stu-id="88505-108">Configuring an application for Manual Provisioning</span></span>

<span data-ttu-id="88505-109">*Manual* provisionamento significa que as contas de usuário devem ser criadas manualmente usando os métodos Olá fornecidos por esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88505-109">*Manual* provisioning means that user accounts must be created manually using hello methods provided by that app.</span></span> <span data-ttu-id="88505-110">Isso pode significar fazendo logon em um portal administrativo para que o aplicativo e adicionar usuários usando uma interface do usuário baseada na web.</span><span class="sxs-lookup"><span data-stu-id="88505-110">This could mean logging into an administrative portal for that app and adding users using a web-based user interface.</span></span> <span data-ttu-id="88505-111">Ou ele pode carregar uma planilha com detalhes da conta de usuário, usando um mecanismo fornecido pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88505-111">Or it could be uploading a spreadsheet with user account detail, using a mechanism provided by that application.</span></span> <span data-ttu-id="88505-112">Consulte a documentação de saudação fornecido pelo app hello, ou contato Olá mecanismos do desenvolvedor toodetermine wat estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="88505-112">Consult hello documentation provided by hello app, or contact hello app developer toodetermine wat mechanisms are available.</span></span>

<span data-ttu-id="88505-113">Se Manual é modo somente Olá mostrado para um determinado aplicativo, isso significa que nenhum conector de provisionamento do AD do Azure automática foi criado para o aplicativo hello ainda.</span><span class="sxs-lookup"><span data-stu-id="88505-113">If Manual is hello only mode shown for a given application, it means that no automatic Azure AD provisioning connector has been created for hello app yet.</span></span> <span data-ttu-id="88505-114">Ou, isso significa que aplicativo de saudação não não suporte Olá usuário pré-requisito API de gerenciamento ao qual toobuild um conector de provisionamento automatizado.</span><span class="sxs-lookup"><span data-stu-id="88505-114">Or it means hello app does not support hello pre-requisite user management API upon which toobuild an automated provisioning connector.</span></span>

<span data-ttu-id="88505-115">Se você quiser toorequest suporte para o provisionamento automático para um determinado aplicativo, você pode preencher uma solicitação em <http://aka.ms/aadapprequest>.</span><span class="sxs-lookup"><span data-stu-id="88505-115">If you would like toorequest support for automatic provisioning for a given app, you can fill out a request at <http://aka.ms/aadapprequest>.</span></span>

## <a name="configuring-an-application-for-automatic-provisioning"></a><span data-ttu-id="88505-116">Configurar um aplicativo para o provisionamento automático</span><span class="sxs-lookup"><span data-stu-id="88505-116">Configuring an application for Automatic Provisioning</span></span>

<span data-ttu-id="88505-117">*Automático* significa que o conector de provisionamento do Azure AD foi desenvolvido para este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="88505-117">*Automatic* means that an Azure AD provisioning connector has been developed for this application.</span></span> <span data-ttu-id="88505-118">Para obter mais informações sobre Olá AD do Azure, o provisionamento de serviço e como ele funciona, consulte [tooSaaS automatizar o provisionamento de usuário e desprovisionamento aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span><span class="sxs-lookup"><span data-stu-id="88505-118">For more information on hello Azure AD provisioning service and how it works, see [Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).</span></span>

<span data-ttu-id="88505-119">Para obter mais informações sobre como tooprovision determinados usuários e aplicativos de tooan de grupos, consulte [Gerenciando o provisionamento de conta de usuário para aplicativos corporativos](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span><span class="sxs-lookup"><span data-stu-id="88505-119">For more information on how tooprovision specific users and groups tooan application, see [Managing user account provisioning for enterprise apps](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).</span></span>

<span data-ttu-id="88505-120">Olá tooenable necessárias etapas reais e configurar o provisionamento automático variam de acordo com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="88505-120">hello actual steps required tooenable and configure automatic provisioning vary depending on hello application.</span></span>

>[!NOTE]
><span data-ttu-id="88505-121">Você deve começar encontrando Olá toosetting tutorial específicas de instalação o provisionamento para seu aplicativo e seguir essas etapas tooconfigure aplicativo hello e toocreate do AD do Azure Olá provisionamento de conexão.</span><span class="sxs-lookup"><span data-stu-id="88505-121">You should start by finding hello setup tutorial specific toosetting up provisioning for your application, and following those steps tooconfigure both hello app and Azure AD toocreate hello provisioning connection.</span></span> 
>
>

<span data-ttu-id="88505-122">Tutoriais de aplicativo podem ser encontrados em [lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span><span class="sxs-lookup"><span data-stu-id="88505-122">App tutorials can be found at [List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).</span></span>

<span data-ttu-id="88505-123">Tooconsider uma coisa importante quando a configuração de provisionamento ser tooreview e configurar mapeamentos de atributo hello e fluxos de trabalho que definem quais fluxo de propriedades de usuário (ou grupo) do aplicativo de toohello do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="88505-123">An important thing tooconsider when setting up provisioning be tooreview and configure hello attribute mappings and workflows that define which user (or group) properties flow from Azure AD toohello application.</span></span> <span data-ttu-id="88505-124">Isso inclui a configuração hello "correspondência da propriedade" ser toouniquely usada identificar e corresponder usuários/grupos entre sistemas Olá dois.</span><span class="sxs-lookup"><span data-stu-id="88505-124">This includes setting hello “matching property” that be used toouniquely identify and match users/groups between hello two systems.</span></span> <span data-ttu-id="88505-125">Para obter mais informações sobre esse processo importante.</span><span class="sxs-lookup"><span data-stu-id="88505-125">For more information on this important process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88505-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88505-126">Next steps</span></span>
[<span data-ttu-id="88505-127">Personalizar os mapeamentos de atributos de provisionamento de usuário para aplicativos SaaS no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88505-127">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

