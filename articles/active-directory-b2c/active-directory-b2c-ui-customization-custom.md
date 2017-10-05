---
title: "Personalizar uma interface do usuário usando políticas personalizadas – Azure AD B2C | Microsoft Docs"
description: "Saiba mais sobre como personalizar uma interface do usuário (UI) ao usar políticas personalizadas no Azure AD B2C."
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 658c597e-3787-465e-b377-26aebc94e46d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: d5a3c0a323b31696d39e3d2b36317dec3a2337d7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-configure-ui-customization-in-a-custom-policy"></a><span data-ttu-id="d2818-103">Azure Active Directory B2C: Configurar a personalização da interface do usuário em uma política personalizada</span><span class="sxs-lookup"><span data-stu-id="d2818-103">Azure Active Directory B2C: Configure UI customization in a custom policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="d2818-104">Depois de concluir este artigo, você terá uma política personalizada de inscrição e entrada com sua marca e aparência.</span><span class="sxs-lookup"><span data-stu-id="d2818-104">After you complete this article, you will have a sign-up and sign-in custom policy with your brand and appearance.</span></span> <span data-ttu-id="d2818-105">Com o Azure Active Directory B2C (Azure AD B2C), você obtém controle quase total do conteúdo HTML e CSS apresentado aos usuários.</span><span class="sxs-lookup"><span data-stu-id="d2818-105">With Azure Active Directory B2C (Azure AD B2C), you get nearly full control of the HTML and CSS content that's presented to users.</span></span> <span data-ttu-id="d2818-106">Ao usar uma política personalizada, a personalização da interface do usuário é configurada em XML em vez de usar controles no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2818-106">When you use a custom policy, you configure UI customization in XML instead of using controls in the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d2818-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2818-107">Prerequisites</span></span>

<span data-ttu-id="d2818-108">Antes de começar, conclua as etapas em [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d2818-108">Before you begin, complete [Getting started with custom policies](active-directory-b2c-get-started-custom.md).</span></span> <span data-ttu-id="d2818-109">Você deve ter uma política personalizada funcional para inscrição e conexão com contas locais.</span><span class="sxs-lookup"><span data-stu-id="d2818-109">You should have a working custom policy for sign-up and sign-in with local accounts.</span></span>

## <a name="page-ui-customization"></a><span data-ttu-id="d2818-110">Personalização da interface do usuário da página</span><span class="sxs-lookup"><span data-stu-id="d2818-110">Page UI customization</span></span>

<span data-ttu-id="d2818-111">Usando o recurso de personalização da interface do usuário da página, você pode personalizar a aparência de qualquer política personalizada.</span><span class="sxs-lookup"><span data-stu-id="d2818-111">By using the page UI customization feature, you can customize the look and feel of any custom policy.</span></span> <span data-ttu-id="d2818-112">Também pode manter a consistência visual e da marca entre seu aplicativo e o Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d2818-112">You can also maintain brand and visual consistency between your application and Azure AD B2C.</span></span>

<span data-ttu-id="d2818-113">É assim que ela funciona: o Azure AD B2C executa o código no navegador do cliente e usa uma abordagem moderna chamada [CORS (Compartilhamento de Recursos entre Origens)](http://www.w3.org/TR/cors/).</span><span class="sxs-lookup"><span data-stu-id="d2818-113">Here's how it works: Azure AD B2C runs code in your customer's browser and uses a modern approach called [Cross-Origin Resource Sharing (CORS)](http://www.w3.org/TR/cors/).</span></span> <span data-ttu-id="d2818-114">Primeiro, especifique uma URL na política personalizada com um conteúdo personalizado em HTML.</span><span class="sxs-lookup"><span data-stu-id="d2818-114">First, you specify a URL in the custom policy with customized HTML content.</span></span> <span data-ttu-id="d2818-115">O Azure AD B2C mescla os elementos de interface do usuário com o conteúdo HTML carregado da URL e exibe a página para o cliente.</span><span class="sxs-lookup"><span data-stu-id="d2818-115">Azure AD B2C merges UI elements with the HTML content that's loaded from your URL and then displays the page to the customer.</span></span>

## <a name="create-your-html5-content"></a><span data-ttu-id="d2818-116">Crie seu conteúdo em HTML5</span><span class="sxs-lookup"><span data-stu-id="d2818-116">Create your HTML5 content</span></span>

<span data-ttu-id="d2818-117">Crie conteúdo em HTML com o nome da marca de seu produto no título.</span><span class="sxs-lookup"><span data-stu-id="d2818-117">Create HTML content with your product's brand name in the title.</span></span>

1. <span data-ttu-id="d2818-118">Copie o trecho de HTML a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2818-118">Copy the following HTML snippet.</span></span> <span data-ttu-id="d2818-119">É um HTML5 bem formado com um elemento vazio chamado *\<div id = "api"\>\</div\>* localizado dentro das marcas *\<body\>*.</span><span class="sxs-lookup"><span data-stu-id="d2818-119">It is well-formed HTML5 with an empty element called *\<div id="api"\>\</div\>* located within the *\<body\>* tags.</span></span> <span data-ttu-id="d2818-120">Esse elemento marca o local em que o conteúdo do Azure AD B2C será inserido.</span><span class="sxs-lookup"><span data-stu-id="d2818-120">This element indicates where Azure AD B2C content is to be inserted.</span></span>

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <title>My Product Brand Name</title>
   </head>
   <body>
       <div id="api"></div>
   </body>
   </html>
   ```

   >[!NOTE]
   ><span data-ttu-id="d2818-121">Por motivos de segurança, bloqueamos a personalização do uso do JavaScript no momento.</span><span class="sxs-lookup"><span data-stu-id="d2818-121">For security reasons, the use of JavaScript is currently blocked for customization.</span></span>

2. <span data-ttu-id="d2818-122">Cole o trecho copiado em um editor de texto e salve o arquivo como *customize-ui.html*.</span><span class="sxs-lookup"><span data-stu-id="d2818-122">Paste the copied snippet in a text editor, and then save the file as *customize-ui.html*.</span></span>

## <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="d2818-123">Criar uma conta de Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="d2818-123">Create an Azure Blob storage account</span></span>

>[!NOTE]
> <span data-ttu-id="d2818-124">Neste artigo, usamos o Armazenamento de Blobs do Azure para hospedar nosso conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d2818-124">In this article, we use Azure Blob storage to host our content.</span></span> <span data-ttu-id="d2818-125">Você pode optar por hospedar seu conteúdo em um servidor Web, mas deve [habilitar CORS em seu servidor Web](https://enable-cors.org/server.html).</span><span class="sxs-lookup"><span data-stu-id="d2818-125">You can choose to host your content on a web server, but you must [enable CORS on your web server](https://enable-cors.org/server.html).</span></span>

<span data-ttu-id="d2818-126">Para hospedar esse conteúdo HTML no Armazenamento de Blobs, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2818-126">To host this HTML content in Blob storage, do the following:</span></span>

1. <span data-ttu-id="d2818-127">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2818-127">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d2818-128">No menu **Hub**, selecione **Novo** > **Armazenamento** > **Conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="d2818-128">On the **Hub** menu, select **New** > **Storage** > **Storage account**.</span></span>
3. <span data-ttu-id="d2818-129">Insira um **Nome** exclusivo para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2818-129">Enter a unique **Name** for your storage account.</span></span>
4. <span data-ttu-id="d2818-130">O **Modelo de implantação** pode permanecer **Gerenciador de Recursos**.</span><span class="sxs-lookup"><span data-stu-id="d2818-130">**Deployment model** can remain **Resource Manager**.</span></span>
5. <span data-ttu-id="d2818-131">Altere **Tipo de Conta** para **Armazenamento de blobs**.</span><span class="sxs-lookup"><span data-stu-id="d2818-131">Change **Account Kind** to **Blob storage**.</span></span>
6. <span data-ttu-id="d2818-132">O **Desempenho** pode permanecer **Padrão**.</span><span class="sxs-lookup"><span data-stu-id="d2818-132">**Performance** can remain **Standard**.</span></span>
7. <span data-ttu-id="d2818-133">A **Replicação** pode permanecer **RA-GRS**.</span><span class="sxs-lookup"><span data-stu-id="d2818-133">**Replication** can remain **RA-GRS**.</span></span>
8. <span data-ttu-id="d2818-134">A **Camada de acesso** pode permanecer **Dinâmica**.</span><span class="sxs-lookup"><span data-stu-id="d2818-134">**Access tier** can remain **Hot**.</span></span>
9. <span data-ttu-id="d2818-135">A **Criptografia do serviço de armazenamento** pode permanecer **Desabilitada**.</span><span class="sxs-lookup"><span data-stu-id="d2818-135">**Storage service encryption** can remain **Disabled**.</span></span>
10. <span data-ttu-id="d2818-136">Selecione uma **Assinatura** para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2818-136">Select a **Subscription** for your storage account.</span></span>
11. <span data-ttu-id="d2818-137">Crie um **Grupo de recursos** ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="d2818-137">Create a **Resource group** or select an existing one.</span></span>
12. <span data-ttu-id="d2818-138">Selecione a **Localização geográfica** para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2818-138">Select the **Geographic location** for your storage account.</span></span>
13. <span data-ttu-id="d2818-139">Clique em **Criar** para criar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2818-139">Click **Create** to create the storage account.</span></span>  
    <span data-ttu-id="d2818-140">Após a conclusão da implantação, a folha **Conta de armazenamento** será aberta automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d2818-140">After the deployment is completed, the **Storage account** blade opens automatically.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d2818-141">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="d2818-141">Create a container</span></span>

<span data-ttu-id="d2818-142">Para criar um contêiner público no armazenamento de Blobs, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2818-142">To create a public container in Blob storage, do the following:</span></span>

1. <span data-ttu-id="d2818-143">Clique na guia **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="d2818-143">Click the **Overview** tab.</span></span>
2. <span data-ttu-id="d2818-144">Clique em **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="d2818-144">Click **Container**.</span></span>
3. <span data-ttu-id="d2818-145">Em **Nome**, digite **$root**.</span><span class="sxs-lookup"><span data-stu-id="d2818-145">For **Name**, type **$root**.</span></span>
4. <span data-ttu-id="d2818-146">Defina **Tipo de acesso** como **Blob**.</span><span class="sxs-lookup"><span data-stu-id="d2818-146">Set **Access type** to **Blob**.</span></span>
5. <span data-ttu-id="d2818-147">Clique em **$root** para abrir o novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="d2818-147">Click **$root** to open the new container.</span></span>
6. <span data-ttu-id="d2818-148">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="d2818-148">Click **Upload**.</span></span>
7. <span data-ttu-id="d2818-149">Clique no ícone de pasta ao lado de **Selecionar um arquivo**.</span><span class="sxs-lookup"><span data-stu-id="d2818-149">Click the folder icon next to **Select a file**.</span></span>
8. <span data-ttu-id="d2818-150">Acesse **customize-ui.html**, que você criou anteriormente na seção [Personalização da interface do usuário da página](#the-page-ui-customization-feature).</span><span class="sxs-lookup"><span data-stu-id="d2818-150">Go to **customize-ui.html**, which you created earlier in the [Page UI customization](#the-page-ui-customization-feature) section.</span></span>
9. <span data-ttu-id="d2818-151">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="d2818-151">Click **Upload**.</span></span>
10. <span data-ttu-id="d2818-152">Selecione o blob customize-ui.html que você carregou.</span><span class="sxs-lookup"><span data-stu-id="d2818-152">Select the customize-ui.html blob that you uploaded.</span></span>
11. <span data-ttu-id="d2818-153">Ao lado de **URL**, clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="d2818-153">Next to **URL**, click **Copy**.</span></span>
12. <span data-ttu-id="d2818-154">Em um navegador, cole a URL copiada e acesse o site.</span><span class="sxs-lookup"><span data-stu-id="d2818-154">In a browser, paste the copied URL, and go to the site.</span></span> <span data-ttu-id="d2818-155">Se o site não estiver acessível, verifique se o tipo de acesso do contêiner está definido como **blob**.</span><span class="sxs-lookup"><span data-stu-id="d2818-155">If the site is inaccessible, make sure the container access type is set to **blob**.</span></span>

## <a name="configure-cors"></a><span data-ttu-id="d2818-156">Configurar o CORS</span><span class="sxs-lookup"><span data-stu-id="d2818-156">Configure CORS</span></span>

<span data-ttu-id="d2818-157">Configure o Armazenamento de nlobs para o Compartilhamento de Recursos entre Origens do Azure fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2818-157">Configure Blob storage for Cross-Origin Resource Sharing by doing the following:</span></span>

>[!NOTE]
><span data-ttu-id="d2818-158">Quer experimentar o recurso de personalização da interface do usuário usando nosso conteúdo de HTML e CSS de exemplo?</span><span class="sxs-lookup"><span data-stu-id="d2818-158">Want to try out the UI customization feature by using our sample HTML and CSS content?</span></span> <span data-ttu-id="d2818-159">Fornecemos [uma ferramenta auxiliar simples](active-directory-b2c-reference-ui-customization-helper-tool.md) que carrega e configura nosso conteúdo de exemplo em sua conta de armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="d2818-159">We've provided [a simple helper tool](active-directory-b2c-reference-ui-customization-helper-tool.md) that uploads and configures our sample content on your Blob storage account.</span></span> <span data-ttu-id="d2818-160">Se você usar a ferramenta, pule para [Modificar a política personalizada de inscrição ou entrada](#modify-your-sign-up-or-sign-in-custom-policy).</span><span class="sxs-lookup"><span data-stu-id="d2818-160">If you use the tool, skip ahead to [Modify your sign-up or sign-in custom policy](#modify-your-sign-up-or-sign-in-custom-policy).</span></span>

1. <span data-ttu-id="d2818-161">Na folha **Armazenamento**, em **Configurações**, abra **CORS**.</span><span class="sxs-lookup"><span data-stu-id="d2818-161">On the **Storage** blade, under **Settings**, open **CORS**.</span></span>
2. <span data-ttu-id="d2818-162">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d2818-162">Click **Add**.</span></span>
3. <span data-ttu-id="d2818-163">Para **Origens permitidas**, digite um asterisco (\*).</span><span class="sxs-lookup"><span data-stu-id="d2818-163">For **Allowed origins**, type an asterisk (\*).</span></span>
4. <span data-ttu-id="d2818-164">Na lista suspensa **Verbos permitidos**, selecione **OBTER** e **OPÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="d2818-164">In the **Allowed verbs** drop-down list, select both **GET** and **OPTIONS**.</span></span>
5. <span data-ttu-id="d2818-165">Para **Cabeçalhos permitidos**, digite um asterisco (\*).</span><span class="sxs-lookup"><span data-stu-id="d2818-165">For **Allowed headers**, type an asterisk (\*).</span></span>
6. <span data-ttu-id="d2818-166">Para **Cabeçalhos expostos**, digite um asterisco (\*).</span><span class="sxs-lookup"><span data-stu-id="d2818-166">For **Exposed headers**, type an asterisk (\*).</span></span>
7. <span data-ttu-id="d2818-167">Para **Idade máxima (segundos)**, digite **200**.</span><span class="sxs-lookup"><span data-stu-id="d2818-167">For **Maximum age (seconds)**, type **200**.</span></span>
8. <span data-ttu-id="d2818-168">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d2818-168">Click **Add**.</span></span>

## <a name="test-cors"></a><span data-ttu-id="d2818-169">Testar o CORS</span><span class="sxs-lookup"><span data-stu-id="d2818-169">Test CORS</span></span>

<span data-ttu-id="d2818-170">Verifique se você está pronto fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2818-170">Validate that you're ready by doing the following:</span></span>

1. <span data-ttu-id="d2818-171">Acesse o site [teste-cors.org](http://test-cors.org/) e cole a URL na caixa **URL Remota**.</span><span class="sxs-lookup"><span data-stu-id="d2818-171">Go to the [test-cors.org](http://test-cors.org/) website, and then paste the URL in the **Remote URL** box.</span></span>
2. <span data-ttu-id="d2818-172">Clique em **Enviar Solicitação**.</span><span class="sxs-lookup"><span data-stu-id="d2818-172">Click **Send Request**.</span></span>  
    <span data-ttu-id="d2818-173">Se você receber um erro, verifique se as [Configurações do CORS](#configure-cors) estão corretas.</span><span class="sxs-lookup"><span data-stu-id="d2818-173">If you receive an error, make sure that your [CORS settings](#configure-cors) are correct.</span></span> <span data-ttu-id="d2818-174">Você também pode precisar limpar o cache do navegador ou abrir uma sessão de navegação particular pressionando Ctrl+Shift+P.</span><span class="sxs-lookup"><span data-stu-id="d2818-174">You might also need to clear your browser cache or open an in-private browsing session by pressing Ctrl+Shift+P.</span></span>

## <a name="modify-your-sign-up-or-sign-in-custom-policy"></a><span data-ttu-id="d2818-175">Modificar a política personalizada de inscrição ou conexão</span><span class="sxs-lookup"><span data-stu-id="d2818-175">Modify your sign-up or sign-in custom policy</span></span>

<span data-ttu-id="d2818-176">Na marca de nível superior *\<TrustFrameworkPolicy\>*, você deve encontrar a marca *\<BuildingBlocks\>*.</span><span class="sxs-lookup"><span data-stu-id="d2818-176">Under the top-level *\<TrustFrameworkPolicy\>* tag, you should find *\<BuildingBlocks\>* tag.</span></span> <span data-ttu-id="d2818-177">Dentro das marcas *\<BuildingBlocks\>*, adicione uma marca *\<ContentDefinitions\>* copiando o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2818-177">Within the *\<BuildingBlocks\>* tags, add a *\<ContentDefinitions\>* tag by copying the following example.</span></span> <span data-ttu-id="d2818-178">Substitua *your_storage_account* pelo nome de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2818-178">Replace *your_storage_account* with the name of your storage account.</span></span>

  ```xml
  <BuildingBlocks>
    <ContentDefinitions>
      <ContentDefinition Id="api.idpselections">
        <LoadUri>https://{your_storage_account}.blob.core.windows.net/customize-ui.html</LoadUri>
      </ContentDefinition>
    </ContentDefinitions>
  </BuildingBlocks>
  ```

## <a name="upload-your-updated-custom-policy"></a><span data-ttu-id="d2818-179">Carregar a política personalizada atualizada</span><span class="sxs-lookup"><span data-stu-id="d2818-179">Upload your updated custom policy</span></span>

1. <span data-ttu-id="d2818-180">No [Portal do Azure](https://portal.azure.com), [alterne para o contexto do locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e abra a folha **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="d2818-180">In the [Azure portal](https://portal.azure.com), [switch into the context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open the **Azure AD B2C** blade.</span></span>
2. <span data-ttu-id="d2818-181">Clique em **Todas as Políticas**.</span><span class="sxs-lookup"><span data-stu-id="d2818-181">Click **All Policies**.</span></span>
3. <span data-ttu-id="d2818-182">Clique em **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="d2818-182">Click **Upload Policy**.</span></span>
4. <span data-ttu-id="d2818-183">Carregue `SignUpOrSignin.xml` com a marca *\<ContentDefinitions\>* adicionada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d2818-183">Upload `SignUpOrSignin.xml` with the *\<ContentDefinitions\>* tag that you added previously.</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="d2818-184">Teste a política personalizada usando a opção **Executar Agora**</span><span class="sxs-lookup"><span data-stu-id="d2818-184">Test the custom policy by using **Run now**</span></span>

1. <span data-ttu-id="d2818-185">Abra a folha **Azure AD B2C**, acesse **Todas as políticas**.</span><span class="sxs-lookup"><span data-stu-id="d2818-185">On the **Azure AD B2C** blade, go to **All polices**.</span></span>
2. <span data-ttu-id="d2818-186">Selecione a política personalizada carregada e clique no botão **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="d2818-186">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="d2818-187">Você deverá conseguir se inscrever usando um endereço de email.</span><span class="sxs-lookup"><span data-stu-id="d2818-187">You should be able to sign up by using an email address.</span></span>

## <a name="reference"></a><span data-ttu-id="d2818-188">Referência</span><span class="sxs-lookup"><span data-stu-id="d2818-188">Reference</span></span>

<span data-ttu-id="d2818-189">Encontre modelos de exemplo para personalização da interface do usuário aqui:</span><span class="sxs-lookup"><span data-stu-id="d2818-189">You can find sample templates for UI customization here:</span></span>

```
git clone https://github.com/azureadquickstarts/b2c-azureblobstorage-client
```

<span data-ttu-id="d2818-190">A pasta sample_templates/wingtip contém os seguintes arquivos HTML:</span><span class="sxs-lookup"><span data-stu-id="d2818-190">The sample_templates/wingtip folder contains the following HTML files:</span></span>

| <span data-ttu-id="d2818-191">Modelo do HTML5</span><span class="sxs-lookup"><span data-stu-id="d2818-191">HTML5 template</span></span> | <span data-ttu-id="d2818-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2818-192">Description</span></span> |
|----------------|-------------|
| <span data-ttu-id="d2818-193">*phonefactor.html*</span><span class="sxs-lookup"><span data-stu-id="d2818-193">*phonefactor.html*</span></span> | <span data-ttu-id="d2818-194">Use esse arquivo como modelo para uma página de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d2818-194">Use this file as a template for a multi-factor authentication page.</span></span> |
| <span data-ttu-id="d2818-195">*resetpassword.html*</span><span class="sxs-lookup"><span data-stu-id="d2818-195">*resetpassword.html*</span></span> | <span data-ttu-id="d2818-196">Use esse arquivo como modelo para uma página de esquecimento de senha.</span><span class="sxs-lookup"><span data-stu-id="d2818-196">Use this file as a template for a forgot password page.</span></span> |
| <span data-ttu-id="d2818-197">*selfasserted.html*</span><span class="sxs-lookup"><span data-stu-id="d2818-197">*selfasserted.html*</span></span> | <span data-ttu-id="d2818-198">Use esse arquivo como modelo para uma página de inscrição de conta social ou uma página de inscrição de conta local.</span><span class="sxs-lookup"><span data-stu-id="d2818-198">Use this file as a template for a social account sign-up page, a local account sign-up page, or a local account sign-in page.</span></span> |
| <span data-ttu-id="d2818-199">*unified.html*</span><span class="sxs-lookup"><span data-stu-id="d2818-199">*unified.html*</span></span> | <span data-ttu-id="d2818-200">Use esse arquivo como modelo para uma página de inscrição ou entrada unificada.</span><span class="sxs-lookup"><span data-stu-id="d2818-200">Use this file as a template for a unified sign-up or sign-in page.</span></span> |
| <span data-ttu-id="d2818-201">*updateprofile.html*</span><span class="sxs-lookup"><span data-stu-id="d2818-201">*updateprofile.html*</span></span> | <span data-ttu-id="d2818-202">Use esse arquivo como modelo para uma página de atualização de perfil.</span><span class="sxs-lookup"><span data-stu-id="d2818-202">Use this file as a template for a profile update page.</span></span> |

<span data-ttu-id="d2818-203">Na seção [Modificar sua política personalizada de inscrição ou entrada](#modify-your-sign-up-or-sign-in-custom-policy), você configurou a definição de conteúdo para `api.idpselections`.</span><span class="sxs-lookup"><span data-stu-id="d2818-203">In the [Modify your sign-up or sign-in custom policy section](#modify-your-sign-up-or-sign-in-custom-policy), you configured the content definition for `api.idpselections`.</span></span> <span data-ttu-id="d2818-204">O conjunto completo de IDs de definição de conteúdo reconhecidas pelo framework de experiência de identidade do Azure AD B2C e suas descrições estão na tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2818-204">The full set of content definition IDs that are recognized by the Azure AD B2C identity experience framework and their descriptions are in the following table:</span></span>

| <span data-ttu-id="d2818-205">ID de definição de conteúdo</span><span class="sxs-lookup"><span data-stu-id="d2818-205">Content definition ID</span></span> | <span data-ttu-id="d2818-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2818-206">Description</span></span> | 
|-----------------------|-------------|
| <span data-ttu-id="d2818-207">*api.error*</span><span class="sxs-lookup"><span data-stu-id="d2818-207">*api.error*</span></span> | <span data-ttu-id="d2818-208">**Página de erro**.</span><span class="sxs-lookup"><span data-stu-id="d2818-208">**Error page**.</span></span> <span data-ttu-id="d2818-209">Essa página é exibida quando uma exceção ou um erro é encontrado.</span><span class="sxs-lookup"><span data-stu-id="d2818-209">This page is displayed when an exception or an error is encountered.</span></span> |
| <span data-ttu-id="d2818-210">*api.idpselections*</span><span class="sxs-lookup"><span data-stu-id="d2818-210">*api.idpselections*</span></span> | <span data-ttu-id="d2818-211">**Página de seleção de provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="d2818-211">**Identity provider selection page**.</span></span> <span data-ttu-id="d2818-212">Esta página contém uma lista de provedores de identidade que o usuário pode escolher durante a inscrição.</span><span class="sxs-lookup"><span data-stu-id="d2818-212">This page contains a list of identity providers that the user can choose from during sign-in.</span></span> <span data-ttu-id="d2818-213">Essas opções são os provedores de identidade empresarial, provedores de identidade social, como Facebook e Google+, ou contas locais.</span><span class="sxs-lookup"><span data-stu-id="d2818-213">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="d2818-214">*api.idpselections.signup*</span><span class="sxs-lookup"><span data-stu-id="d2818-214">*api.idpselections.signup*</span></span> | <span data-ttu-id="d2818-215">**Seleção de provedor de identidade para inscrição**.</span><span class="sxs-lookup"><span data-stu-id="d2818-215">**Identity provider selection for sign-up**.</span></span> <span data-ttu-id="d2818-216">Esta página contém uma lista de provedores de identidade que o usuário pode escolher durante a inscrição.</span><span class="sxs-lookup"><span data-stu-id="d2818-216">This page contains a list of identity providers that the user can choose from during sign-up.</span></span> <span data-ttu-id="d2818-217">Essas opções são os provedores de identidade empresarial, provedores de identidade social, como Facebook e Google+, ou contas locais.</span><span class="sxs-lookup"><span data-stu-id="d2818-217">These options are either enterprise identity providers, social identity providers such as Facebook and Google+, or local accounts.</span></span> |
| <span data-ttu-id="d2818-218">*api.localaccountpasswordreset*</span><span class="sxs-lookup"><span data-stu-id="d2818-218">*api.localaccountpasswordreset*</span></span> | <span data-ttu-id="d2818-219">**Página de esquecimento de senha**.</span><span class="sxs-lookup"><span data-stu-id="d2818-219">**Forgot password page**.</span></span> <span data-ttu-id="d2818-220">Esta página contém um formulário que o usuário precisa preencher para iniciar sua redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="d2818-220">This page contains a form that the user must complete to initiate a password reset.</span></span>  |
| <span data-ttu-id="d2818-221">*api.localaccountsignin*</span><span class="sxs-lookup"><span data-stu-id="d2818-221">*api.localaccountsignin*</span></span> | <span data-ttu-id="d2818-222">**Página de entrada da conta local**.</span><span class="sxs-lookup"><span data-stu-id="d2818-222">**Local account sign-in page**.</span></span> <span data-ttu-id="d2818-223">Esta página contém um formulário de entrada para entradas com uma conta local baseada em endereço de email ou nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="d2818-223">This page contains a sign-in form for signing in with a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="d2818-224">O formulário pode conter uma caixa de entrada de texto e caixa de entrada de senha.</span><span class="sxs-lookup"><span data-stu-id="d2818-224">The form can contain a text input box and password entry box.</span></span> |
| <span data-ttu-id="d2818-225">*api.localaccountsignup*</span><span class="sxs-lookup"><span data-stu-id="d2818-225">*api.localaccountsignup*</span></span> | <span data-ttu-id="d2818-226">**Página de inscrição da conta local**.</span><span class="sxs-lookup"><span data-stu-id="d2818-226">**Local account sign-up page**.</span></span> <span data-ttu-id="d2818-227">Esta página contém um formulário de inscrição para inscrições com uma conta local baseada em endereço de email ou nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="d2818-227">This page contains a sign-up form for signing up for a local account that is based on an email address or a user name.</span></span> <span data-ttu-id="d2818-228">O formulário pode conter diferentes controles de entrada como caixa de entrada de texto, caixa de entrada de senha, botão de opção, caixas de lista suspensa de seleção única e caixas de seleção múltipla.</span><span class="sxs-lookup"><span data-stu-id="d2818-228">The form can contain various input controls, such as a text input box, a password entry box, a radio button, single-select drop-down boxes, and multi-select check boxes.</span></span> |
| <span data-ttu-id="d2818-229">*api.phonefactor*</span><span class="sxs-lookup"><span data-stu-id="d2818-229">*api.phonefactor*</span></span> | <span data-ttu-id="d2818-230">**Página de autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="d2818-230">**Multi-factor authentication page**.</span></span> <span data-ttu-id="d2818-231">Nesta página, os usuários podem verificar seus números de telefone (usando mensagem de texto ou por voz) durante a inscrição ou entrada.</span><span class="sxs-lookup"><span data-stu-id="d2818-231">On this page, users can verify their phone numbers (by using text or voice) during sign-up or sign-in.</span></span> |
| <span data-ttu-id="d2818-232">*api.selfasserted*</span><span class="sxs-lookup"><span data-stu-id="d2818-232">*api.selfasserted*</span></span> | <span data-ttu-id="d2818-233">**Página de inscrição de conta social**.</span><span class="sxs-lookup"><span data-stu-id="d2818-233">**Social account sign-up page**.</span></span> <span data-ttu-id="d2818-234">Esta página contém um formulário de inscrição que deve ser preenchido pelos usuários ao se inscreverem usando uma conta existente de um provedor de identidade social, como o Facebook ou Google+.</span><span class="sxs-lookup"><span data-stu-id="d2818-234">This page contains a sign-up form that users must complete when they sign up by using an existing account from a social identity provider such as Facebook or Google+.</span></span> <span data-ttu-id="d2818-235">Esta página é semelhante à página de inscrição de conta social anterior, exceto os campos de entrada de senha.</span><span class="sxs-lookup"><span data-stu-id="d2818-235">This page is similar to the preceding social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="d2818-236">*api.selfasserted.profileupdate*</span><span class="sxs-lookup"><span data-stu-id="d2818-236">*api.selfasserted.profileupdate*</span></span> | <span data-ttu-id="d2818-237">**Página de atualização de perfil**.</span><span class="sxs-lookup"><span data-stu-id="d2818-237">**Profile update page**.</span></span> <span data-ttu-id="d2818-238">Esta página contém um formulário que os usuários podem usar para atualizar o perfil.</span><span class="sxs-lookup"><span data-stu-id="d2818-238">This page contains a form that users can use to update their profile.</span></span> <span data-ttu-id="d2818-239">Esta página é semelhante à página de inscrição de conta social, exceto os campos de entrada de senha.</span><span class="sxs-lookup"><span data-stu-id="d2818-239">This page is similar to the social account sign-up page, except for the password entry fields.</span></span> |
| <span data-ttu-id="d2818-240">*api.signuporsignin*</span><span class="sxs-lookup"><span data-stu-id="d2818-240">*api.signuporsignin*</span></span> | <span data-ttu-id="d2818-241">**Página de inscrição ou entrada unificada**.</span><span class="sxs-lookup"><span data-stu-id="d2818-241">**Unified sign-up or sign-in page**.</span></span> <span data-ttu-id="d2818-242">Esta página controla tanto a inscrição quanto a entrada de usuários que podem usar provedores de identidade empresarial ou provedores de identidade social, como Facebook, Google+ ou contas locais.</span><span class="sxs-lookup"><span data-stu-id="d2818-242">This page handles both the sign-up and sign-in of users, who can use enterprise identity providers, social identity providers such as Facebook or Google+, or local accounts.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d2818-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2818-243">Next steps</span></span>

<span data-ttu-id="d2818-244">Para saber mais sobre quais elementos de interface do usuário podem ser personalizados, confira [Guia de referência para personalização da interface do usuário para políticas internas](active-directory-b2c-reference-ui-customization.md) .</span><span class="sxs-lookup"><span data-stu-id="d2818-244">For additional information about UI elements that can be customized, see [reference guide for UI customization for built-in policies](active-directory-b2c-reference-ui-customization.md).</span></span>
