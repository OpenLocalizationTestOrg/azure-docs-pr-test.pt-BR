---
title: 'Azure Active Directory B2C: atributos personalizados | Microsoft Docs'
description: "Como usar atributos personalizados no Active Directory B2C do Azure para coletar informações sobre seus consumidores"
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
ms.openlocfilehash: 356aaeff3a78fc7b682d621e8e0de9312582b2fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-use-custom-attributes-to-collect-information-about-your-consumers"></a><span data-ttu-id="b1b1d-103">Azure Active Directory B2C: usar atributos personalizados para coletar informações sobre seus consumidores</span><span class="sxs-lookup"><span data-stu-id="b1b1d-103">Azure Active Directory B2C: Use custom attributes to collect information about your consumers</span></span>
<span data-ttu-id="b1b1d-104">O diretório do Azure AD (Azure Active Directory) B2C é fornecido com um conjunto interno de informações (atributos): Nome, Sobrenome, Cidade e CEP, entre outros atributos.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-104">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of information (attributes): Given Name, Surname, City, Postal Code, and other attributes.</span></span> <span data-ttu-id="b1b1d-105">No entanto, todos os aplicativos voltados para o consumidor têm requisitos exclusivos sobre quais atributos devem ser coletados dos consumidores.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-105">However, every consumer-facing application has unique requirements on what attributes to gather from consumers.</span></span> <span data-ttu-id="b1b1d-106">Com o Azure AD B2C, você pode estender o conjunto de atributos armazenados em cada conta de consumidor.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-106">With Azure AD B2C, you can extend the set of attributes stored on each consumer account.</span></span> <span data-ttu-id="b1b1d-107">Você pode criar atributos personalizados no [Portal do Azure](https://portal.azure.com/) e usá-los em suas políticas de inscrição, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-107">You can create custom attributes on the [Azure portal](https://portal.azure.com/) and use it in your sign-up policies, as shown below.</span></span> <span data-ttu-id="b1b1d-108">Você também pode ler e gravar esses atributos usando a [API do Graph do Azure AD](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="b1b1d-108">You can also read and write these attributes by using the [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b1b1d-109">Os atributos personalizados usam as [Extensões de Esquema de Diretório da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1b1d-109">Custom attributes use [Azure AD Graph API Directory Schema Extensions](https://msdn.microsoft.com/library/azure/dn720459.aspx).</span></span>
> 
> 

## <a name="create-a-custom-attribute"></a><span data-ttu-id="b1b1d-110">Como criar um atributo personalizado</span><span class="sxs-lookup"><span data-stu-id="b1b1d-110">Create a custom attribute</span></span>
1. <span data-ttu-id="b1b1d-111">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-111">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="b1b1d-112">Clique em **Atributos de usuário**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-112">Click **User attributes**.</span></span>
3. <span data-ttu-id="b1b1d-113">Clique em **+Adicionar** , na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-113">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="b1b1d-114">Forneça um **Nome** para o atributo personalizado (por exemplo, "ShoeSize") e, opcionalmente, uma **Descrição**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-114">Provide a **Name** for the custom attribute (for example, "ShoeSize") and optionally, a **Description**.</span></span> <span data-ttu-id="b1b1d-115">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-115">Click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b1b1d-116">Apenas o **Tipo de Dados** "String" está disponível no momento.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-116">Only the "String" **Data Type** is currently available.</span></span>
   > 
   > 

<span data-ttu-id="b1b1d-117">O atributo personalizado agora está disponível na lista de **Atributos do usuário**e para uso em suas políticas de inscrição.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-117">The custom attribute is now available in the list of **User attributes**, and for use in your sign-up policies.</span></span>

## <a name="use-a-custom-attribute-in-your-sign-up-policy"></a><span data-ttu-id="b1b1d-118">Usar um atributo personalizado na sua política de inscrição</span><span class="sxs-lookup"><span data-stu-id="b1b1d-118">Use a custom attribute in your sign-up policy</span></span>
1. <span data-ttu-id="b1b1d-119">Siga estas etapas para [navegar até a folha de recursos do B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-119">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="b1b1d-120">Clique em **Políticas de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-120">Click **Sign-up policies**.</span></span>
3. <span data-ttu-id="b1b1d-121">Clique na sua política de inscrição (por exemplo, "B2C_1_SiUp") para abri-la.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-121">Click your sign-up policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="b1b1d-122">Clique em **Editar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-122">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="b1b1d-123">Clique em **Atributos de inscrição** e selecione o atributo personalizado (por exemplo, "ShoeSize").</span><span class="sxs-lookup"><span data-stu-id="b1b1d-123">Click **Sign-up attributes** and select the custom attribute (for example, "ShoeSize").</span></span> <span data-ttu-id="b1b1d-124">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-124">Click **OK**.</span></span>
5. <span data-ttu-id="b1b1d-125">Clique em **Declarações de aplicativo** e selecione o atributo personalizado.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-125">Click **Application claims** and select the custom attribute.</span></span> <span data-ttu-id="b1b1d-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-126">Click **OK**.</span></span>
6. <span data-ttu-id="b1b1d-127">Clique em **Salvar** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-127">Click **Save** at the top of the blade.</span></span>

<span data-ttu-id="b1b1d-128">Você pode usar o recurso "Executar agora" da política para verificar a experiência do consumidor.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-128">You can use the "Run now" feature on the policy to verify the consumer experience.</span></span> <span data-ttu-id="b1b1d-129">Agora você deve ver "ShoeSize" na lista de atributos que são coletados durante a inscrição do consumidor e vê-lo no token enviado de volta ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-129">You should now see "ShoeSize" in the list of attributes collected during consumer sign-up, and see it in the token sent back to your application.</span></span>

## <a name="notes"></a><span data-ttu-id="b1b1d-130">Observações</span><span class="sxs-lookup"><span data-stu-id="b1b1d-130">Notes</span></span>
* <span data-ttu-id="b1b1d-131">Juntamente com as políticas de inscrição, os atributos personalizados também podem ser usados nas políticas de inscrição ou de entrada e também nas políticas de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-131">Along with sign-up policies, custom attributes can also be used in sign-up or sign-in policies and profile editing policies.</span></span>
* <span data-ttu-id="b1b1d-132">Há uma limitação conhecida de atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-132">There is a known limitation of custom attributes.</span></span> <span data-ttu-id="b1b1d-133">Esse tipo de atributo só é criado na primeira vez que é usado em qualquer política, e não quando você o adiciona à lista de **Atributos de usuário**.</span><span class="sxs-lookup"><span data-stu-id="b1b1d-133">It is only created the first time it is used in any policy, and not when you add it to the list of **User attributes**.</span></span>

