---
title: "Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor | Microsoft Docs"
description: "Um tópico que demonstra como desabilitar a verificação de email durante a inscrição do consumidor no Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="42f5a-103">Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor</span><span class="sxs-lookup"><span data-stu-id="42f5a-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="42f5a-104">Quando está habilitado, o Azure Active Directory (Azure AD) B2C fornece a um consumidor a capacidade de se inscrever em aplicativos fornecendo um endereço de email e criando uma conta local.</span><span class="sxs-lookup"><span data-stu-id="42f5a-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="42f5a-105">O Azure AD B2C verifica os endereços de email válidos exigindo que os consumidores os confirmem durante o processo de inscrição.</span><span class="sxs-lookup"><span data-stu-id="42f5a-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="42f5a-106">Ele também impede que um processo automatizado mal-intencionado gere contas falsas para os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="42f5a-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="42f5a-107">Alguns desenvolvedores de aplicativo preferem ignorar a verificação de email durante o processo de inscrição e, em vez disso, pedem para os consumidores verificarem o endereço de email mais tarde.</span><span class="sxs-lookup"><span data-stu-id="42f5a-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="42f5a-108">Para dar suporte a isso, o Azure AD B2C pode ser configurado para desabilitar a verificação de email.</span><span class="sxs-lookup"><span data-stu-id="42f5a-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="42f5a-109">Isso cria um processo de inscrição mais tranquilo e oferece aos desenvolvedores a flexibilidade para diferenciar os consumidores que confirmaram seu endereço de email daqueles que não o fizeram.</span><span class="sxs-lookup"><span data-stu-id="42f5a-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="42f5a-110">Por padrão, as políticas de inscrição têm a verificação de email ativada.</span><span class="sxs-lookup"><span data-stu-id="42f5a-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="42f5a-111">Use as etapas a seguir para desativá-la:</span><span class="sxs-lookup"><span data-stu-id="42f5a-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="42f5a-112">Siga estas etapas para [navegar até a folha de recursos do B2C no Portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="42f5a-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="42f5a-113">Clique em **Políticas de inscrição** ou em **Políticas de inscrição ou entrada** dependendo do que você configurou para inscrição.</span><span class="sxs-lookup"><span data-stu-id="42f5a-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="42f5a-114">Clique em sua política (por exemplo, "B2C_1_SiUp") para abri-la.</span><span class="sxs-lookup"><span data-stu-id="42f5a-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="42f5a-115">Clique em **Editar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="42f5a-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="42f5a-116">Clique em **Personalização da interface do usuário da página**.</span><span class="sxs-lookup"><span data-stu-id="42f5a-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="42f5a-117">Clique em **Página de inscrição da conta local**.</span><span class="sxs-lookup"><span data-stu-id="42f5a-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="42f5a-118">Clique em **Endereço de Email** na coluna **Nome** na seção **Atributos de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="42f5a-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="42f5a-119">Alterne a opção **Exigir verificação** para **Não**.</span><span class="sxs-lookup"><span data-stu-id="42f5a-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="42f5a-120">Clique em **OK** na parte inferior até chegar à folha **Editar política**.</span><span class="sxs-lookup"><span data-stu-id="42f5a-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="42f5a-121">Clique em **Salvar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="42f5a-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="42f5a-122">Pronto!</span><span class="sxs-lookup"><span data-stu-id="42f5a-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="42f5a-123">Desabilitar a verificação de email no processo de inscrição pode gerar spam.</span><span class="sxs-lookup"><span data-stu-id="42f5a-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="42f5a-124">Se você desabilitar o padrão, recomendamos adicionar seu próprio sistema de verificação.</span><span class="sxs-lookup"><span data-stu-id="42f5a-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="42f5a-125">Estamos sempre abertos a comentários e sugestões!</span><span class="sxs-lookup"><span data-stu-id="42f5a-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="42f5a-126">Caso você tenha alguma dúvida sobre este tópico ou recomendações para melhorar o conteúdo, agradecemos seus comentários na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="42f5a-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="42f5a-127">Para solicitações de recursos, adicione-os ao [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="42f5a-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>