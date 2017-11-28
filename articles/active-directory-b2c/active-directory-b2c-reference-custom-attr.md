---
title: 'Azure Active Directory B2C: atributos personalizados | Microsoft Docs'
description: "Como os atributos de toouse personalizado no Azure Active Directory B2C toocollect informações sobre seus consumidores"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 055ffb0a-197b-4716-8dad-1fd8a01e174f
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: fb1bff77ad54c246c6d2f69f39c03eafb76fe6bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-toocollect-information-about-your-consumers"></a><span data-ttu-id="c5257-103">B2C de diretório ativo do Azure: Use informações de toocollect de atributos personalizados sobre seus consumidores</span><span class="sxs-lookup"><span data-stu-id="c5257-103">Azure Active Directory B2C: Use custom attributes toocollect information about your consumers</span></span>
<span data-ttu-id="c5257-104">O diretório do Azure AD (Azure Active Directory) B2C é fornecido com um conjunto interno de informações (atributos): Nome, Sobrenome, Cidade e CEP, entre outros atributos.</span><span class="sxs-lookup"><span data-stu-id="c5257-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="c5257-105">No entanto, todos os aplicativos voltados para o consumidor tem requisitos exclusivos em toogather quais atributos de consumidores.</span><span class="sxs-lookup"><span data-stu-id="c5257-105">However, every consumer-facing application has unique requirements on what attributes toogather from consumers.</span></span> <span data-ttu-id="c5257-106">Com o Azure AD B2C, você pode estender o conjunto de saudação de atributos armazenados em cada conta de consumidor.</span><span class="sxs-lookup"><span data-stu-id="c5257-106">With Azure AD B2C, you can extend hello set of attributes stored on each consumer account.</span></span> <span data-ttu-id="c5257-107">Você pode criar atributos personalizados em Olá [portal do Azure](https://portal.azure.com/) e usá-lo em suas políticas de inscrição, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c5257-107">You can create custom attributes on hello [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="c5257-108">Você também pode ler e gravar esses atributos usando Olá [do Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c5257-108">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c5257-109">Os atributos personalizados usam as [Extensões de Esquema de Diretório da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5257-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="c5257-110">Como criar um atributo personalizado</span><span class="sxs-lookup"><span data-stu-id="c5257-110">Create a custom attribute</span></span>
1. <span data-ttu-id="c5257-111">[Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="c5257-111">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="c5257-112">Clique em **Atributos de usuário**.</span><span class="sxs-lookup"><span data-stu-id="c5257-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="c5257-113">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5257-113">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="c5257-114">Forneça um **nome** para atributo personalizado de saudação (por exemplo, "ShoeSize") e, opcionalmente, um **descrição**.</span><span class="sxs-lookup"><span data-stu-id="c5257-114">Provide a **Name** for hello custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="c5257-115">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c5257-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c5257-116">Somente hello "Cadeia de caracteres" **tipo de dados** está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="c5257-116">Only hello "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="c5257-117">atributo personalizado Olá agora está disponível na lista de saudação do **atributos de usuário**e para uso em suas políticas de inscrição.</span><span class="sxs-lookup"><span data-stu-id="c5257-117">hello custom attribute is now available in hello list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="c5257-118">Usar um atributo personalizado na sua política de inscrição</span><span class="sxs-lookup"><span data-stu-id="c5257-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="c5257-119">[Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="c5257-119">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="c5257-120">Clique em **Políticas de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="c5257-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="c5257-121">Clique em sua política de inscrição (por exemplo, "B2C_1_SiUp") tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="c5257-121">Click your sign-up policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="c5257-122">Clique em **editar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5257-122">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="c5257-123">Clique em **inscrição atributos** e selecione Olá personalizada (por exemplo, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="c5257-123">Click **Sign-up attributes** and select hello custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="c5257-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5257-124">Click **OK**.</span></span>
5. <span data-ttu-id="c5257-125">Clique em **declarações de aplicativo** e atributo personalizado Olá select.</span><span class="sxs-lookup"><span data-stu-id="c5257-125">Click **Application claims** and select hello custom attribute.</span></span> <span data-ttu-id="c5257-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5257-126">Click **OK**.</span></span>
6. <span data-ttu-id="c5257-127">Clique em **salvar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5257-127">Click **Save** at hello top of hello blade.</span></span>

<span data-ttu-id="c5257-128">Você pode usar o recurso de "Executar agora" hello na experiência do consumidor Olá política tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="c5257-128">You can use hello "Run now" feature on hello policy tooverify hello consumer experience.</span></span> <span data-ttu-id="c5257-129">Agora você deve vê "ShoeSize" hello lista de atributos coletados durante a inscrição do consumidor e vê-lo no aplicativo de token tooyour back enviados hello.</span><span class="sxs-lookup"><span data-stu-id="c5257-129">You should now see "ShoeSize" in hello list of attributes collected during consumer sign-up, and see it in hello token sent back tooyour application.</span></span>

## <a name="notes"></a><span data-ttu-id="c5257-130">Observações</span><span class="sxs-lookup"><span data-stu-id="c5257-130">Notes</span></span>
* <span data-ttu-id="c5257-131">Juntamente com as políticas de inscrição, os atributos personalizados também podem ser usados nas políticas de inscrição ou de entrada e também nas políticas de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="c5257-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="c5257-132">Há uma limitação conhecida de atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="c5257-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="c5257-133">É somente criado Olá primeira vez que ele é usado em qualquer política e não quando você adicionar lista de toohello de **atributos de usuário**.</span><span class="sxs-lookup"><span data-stu-id="c5257-133">It is only created hello first time it is used in any policy, and not when you add it toohello list of **User attributes**.</span></span>

