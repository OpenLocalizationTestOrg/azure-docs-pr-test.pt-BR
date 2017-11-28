---
title: "Azure Active Directory B2C: configuração da Amazon | Microsoft Docs"
description: "Fornece tooconsumers Inscreva-se e entrar com contas do Amazon em seus aplicativos que são protegidos pelo Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="74f48-103">B2C de diretório ativo do Azure: Fornecer tooconsumers se inscrever e fazer logon com contas do Amazon</span><span class="sxs-lookup"><span data-stu-id="74f48-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="74f48-104">Criar um aplicativo da Amazon</span><span class="sxs-lookup"><span data-stu-id="74f48-104">Create an Amazon application</span></span>
<span data-ttu-id="74f48-105">toouse Amazon como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um aplicativo Amazon e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="74f48-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="74f48-106">É necessário um toodo de conta do Amazon isso.</span><span class="sxs-lookup"><span data-stu-id="74f48-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="74f48-107">Se você não tiver uma, poderá obtê-la em [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="74f48-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="74f48-108">Vá toohello [Amazon Developer Center](https://login.amazon.com/) e entre com suas credenciais de conta do Amazon.</span><span class="sxs-lookup"><span data-stu-id="74f48-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="74f48-109">Se você ainda não tiver feito isso, clique em **inscrever-se**, execute as etapas de registro de desenvolvedor hello e aceitar a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f48-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="74f48-110">Clique em **Registrar novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="74f48-110">Click **Register new application**.</span></span>
   
    ![Registrar um novo aplicativo no site da Amazon Olá](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="74f48-112">Forneça as informações do aplicativo (**Nome**, **Descrição** e **URL do Aviso de Privacidade**) e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="74f48-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Fornecendo informações de aplicativo para registrar um novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="74f48-114">Em Olá **configurações Web** seção valores de saudação de cópia de **ID do cliente** e **segredo do cliente**.</span><span class="sxs-lookup"><span data-stu-id="74f48-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="74f48-115">(É necessário tooclick Olá **Mostrar segredo** botão toosee isso.) Você precisará de ambos deles tooconfigure Amazon como um provedor de identidade em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="74f48-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="74f48-116">Clique em **editar** na parte inferior da saudação da seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f48-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="74f48-117">**Segredo do Cliente** é uma credencial de segurança importante.</span><span class="sxs-lookup"><span data-stu-id="74f48-117">**Client Secret** is an important security credential.</span></span>
   
    ![Fornecendo a ID e o Segredo do Cliente para seu novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="74f48-119">Digite `https://login.microsoftonline.com` em Olá **permitido origens do JavaScript** campo e `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` em Olá **permitidas URLs de retorno** campo.</span><span class="sxs-lookup"><span data-stu-id="74f48-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="74f48-120">Substitua **{tenant}** pelo nome do locatário (por exemplo, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="74f48-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="74f48-121">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="74f48-121">Click **Save**.</span></span> <span data-ttu-id="74f48-122">Olá **{locatário}** valor diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="74f48-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Fornecendo JavaScript Origins e URLs de Retorno para o novo aplicativo na Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="74f48-124">Configurar a Amazon como um provedor de identidade em seu locatário</span><span class="sxs-lookup"><span data-stu-id="74f48-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="74f48-125">Siga estas etapas muito[navegue folha de recursos toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="74f48-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="74f48-126">Na folha de recursos Olá B2C, clique em **provedores de identidade**.</span><span class="sxs-lookup"><span data-stu-id="74f48-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="74f48-127">Clique em **+ adicionar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="74f48-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="74f48-128">Forneça um amigável **nome** para configuração do provedor de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="74f48-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="74f48-129">Por exemplo, insira “Amzn”.</span><span class="sxs-lookup"><span data-stu-id="74f48-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="74f48-130">Clique em **Tipo de provedor de identidade**, selecione **Amazon** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="74f48-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="74f48-131">Clique em **configurar esse provedor de identidade** e digite Olá ID e o cliente segredo do cliente do hello aplicativo Amazon que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74f48-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="74f48-132">Clique em **Okey** e, em seguida, clique em **criar** toosave sua configuração da Amazon.</span><span class="sxs-lookup"><span data-stu-id="74f48-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

