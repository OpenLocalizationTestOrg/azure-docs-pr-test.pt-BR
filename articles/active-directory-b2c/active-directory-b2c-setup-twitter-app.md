---
title: "Azure Active Directory B2C: configuração do Twitter | Microsoft Docs"
description: "Fornece tooconsumers se inscrever e fazer logon com contas do Twitter em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="362e7-103">B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Twitter</span><span class="sxs-lookup"><span data-stu-id="362e7-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="362e7-104">Esse recurso está em visualização.</span><span class="sxs-lookup"><span data-stu-id="362e7-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="362e7-105">Criar um aplicativo do Twitter</span><span class="sxs-lookup"><span data-stu-id="362e7-105">Create a Twitter application</span></span>
<span data-ttu-id="362e7-106">toouse do Twitter como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), precisa toocreate um aplicativo do Twitter e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="362e7-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="362e7-107">É necessário um toodo de conta de desenvolvedor do Twitter isso.</span><span class="sxs-lookup"><span data-stu-id="362e7-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="362e7-108">Se não tiver uma, você poderá obtê-la em [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="362e7-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="362e7-109">Vá toohello [site do desenvolvedor do Twitter](https://dev.twitter.com/) e entre com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="362e7-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="362e7-110">Clique em **Meus aplicativos** em **Ferramentas e Suporte** e, em seguida, clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="362e7-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="362e7-111">No formulário de hello, forneça um valor para Olá **nome**, **descrição**, e **site**.</span><span class="sxs-lookup"><span data-stu-id="362e7-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="362e7-112">Para Olá **URL de retorno de chamada**, digite `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="362e7-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="362e7-113">Certifique-se de que tooreplace **{locatário}** com o nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="362e7-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="362e7-114">Verificar Olá caixa tooagree toohello **contrato de desenvolvedor** e clique em **criar seu aplicativo Twitter**.</span><span class="sxs-lookup"><span data-stu-id="362e7-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="362e7-115">Depois que o aplicativo hello for criado, clique em **chaves e Tokens de acesso**.</span><span class="sxs-lookup"><span data-stu-id="362e7-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="362e7-116">Copie o valor de saudação do **chave do consumidor** e **segredo do consumidor**.</span><span class="sxs-lookup"><span data-stu-id="362e7-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="362e7-117">Você precisará de ambos tooconfigure Twitter como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="362e7-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="362e7-118">Configurar o Twitter como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="362e7-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="362e7-119">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="362e7-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="362e7-120">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="362e7-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="362e7-121">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="362e7-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="362e7-122">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="362e7-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="362e7-123">Por exemplo, insira "Twitter".</span><span class="sxs-lookup"><span data-stu-id="362e7-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="362e7-124">Clique em **Tipo de provedor de identidade**, selecione **Twitter** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="362e7-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="362e7-125">Clique em **configurar esse provedor de identidade** e digite Olá Twitter **chave do consumidor** para Olá **id do cliente** e Olá Twitter **segredo do consumidor**para Olá **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="362e7-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="362e7-126">Clique em **Okey**e, em seguida, clique em **criar** toosave sua configuração do Twitter.</span><span class="sxs-lookup"><span data-stu-id="362e7-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

