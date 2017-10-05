---
title: "Azure Active Directory B2C: configuração do Twitter | Microsoft Docs"
description: "Forneça inscrição e credenciais para consumidores com contas do Twitter em seus aplicativos protegidos pelo Azure Active Directory B2C."
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
ms.openlocfilehash: 82a001dd53cdddcf3b360090f3250af593c96fbb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-twitter-accounts"></a><span data-ttu-id="244b4-103">Azure Active Directory B2C: fornecer inscrição e credenciais para consumidores com contas do Twitter</span><span class="sxs-lookup"><span data-stu-id="244b4-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="244b4-104">Essa funcionalidade está em visualização.</span><span class="sxs-lookup"><span data-stu-id="244b4-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="244b4-105">Criar um aplicativo do Twitter</span><span class="sxs-lookup"><span data-stu-id="244b4-105">Create a Twitter application</span></span>
<span data-ttu-id="244b4-106">Para usar o Twitter como um provedor de identidade no Azure AD (Azure Active Directory) B2C, você precisa criar um aplicativo Twitter e fornecer a ele os parâmetros certos.</span><span class="sxs-lookup"><span data-stu-id="244b4-106">To use Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Twitter application and supply it with the right parameters.</span></span> <span data-ttu-id="244b4-107">Você precisa de uma conta de desenvolvedor do Twitter para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="244b4-107">You need a Twitter developer account to do this.</span></span> <span data-ttu-id="244b4-108">Se não tiver uma, você poderá obtê-la em [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="244b4-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="244b4-109">Vá para o [site do desenvolvedor do Twitter](https://dev.twitter.com/) e entre com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="244b4-109">Go to the [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="244b4-110">Clique em **Meus aplicativos** em **Ferramentas e Suporte** e, em seguida, clique em **Criar Novo Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="244b4-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="244b4-111">No formulário, forneça um valor para o **Nome**, **Descrição**, e **Site**.</span><span class="sxs-lookup"><span data-stu-id="244b4-111">In the form, provide a value for the **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="244b4-112">Insira `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` como o valor da **URL de Retorno de Chamada**.</span><span class="sxs-lookup"><span data-stu-id="244b4-112">For the **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="244b4-113">Certifique-se de substituir **{tenant}** pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="244b4-113">Make sure to replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="244b4-114">Marque a caixa para concordar com o **Contrato de Desenvolvedor** e clique em **Criar seu aplicativo do Twitter**.</span><span class="sxs-lookup"><span data-stu-id="244b4-114">Check the box to agree to the **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="244b4-115">Quando o aplicativo for criado, clique na guia **Chaves e Tokens de acesso**.</span><span class="sxs-lookup"><span data-stu-id="244b4-115">Once the app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="244b4-116">Copie o valor de **Chave do consumidor** e **Segredo do consumidor**.</span><span class="sxs-lookup"><span data-stu-id="244b4-116">Copy the value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="244b4-117">Você precisará de ambos para configurar o Twitter como um provedor de identidade no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="244b4-117">You will need both of them to configure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="244b4-118">Configurar o Twitter como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="244b4-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="244b4-119">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="244b4-119">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="244b4-120">Na folha de recursos do B2C, clique em **Provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="244b4-120">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="244b4-121">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="244b4-121">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="244b4-122">Forneça um **Nome** amigável para a configuração do provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="244b4-122">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="244b4-123">Por exemplo, insira "Twitter".</span><span class="sxs-lookup"><span data-stu-id="244b4-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="244b4-124">Clique em **Tipo de provedor de identidade**, selecione **Twitter** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="244b4-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="244b4-125">Clique em **Configurar esse provedor de identidade** e insira a **Chave do Consumidor** do Twitter para a **ID do cliente** e o **Segredo do Consumidor** do Twitter para o **Segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="244b4-125">Click **Set up this identity provider** and enter the Twitter **Consumer Key** for the **Client id** and the Twitter **Consumer Secret** for the **Client secret**.</span></span>
7. <span data-ttu-id="244b4-126">Clique em **OK** e em **Criar** para salvar sua configuração do Twitter.</span><span class="sxs-lookup"><span data-stu-id="244b4-126">Click **OK**, and then click **Create** to save your Twitter configuration.</span></span>

