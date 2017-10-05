---
title: "Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas"
description: "Um artigo de instruções sobre como configurar o ADFS 2016 usando o protocolo SAML e políticas personalizadas"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="5f590-103">Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="5f590-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5f590-104">Este artigo mostra como habilitar a entrada para usuários da conta ADFS por meio de [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5f590-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f590-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5f590-105">Prerequisites</span></span>

<span data-ttu-id="5f590-106">Conclua as etapas no artigo [Introdução às políticas personalizadas](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="5f590-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="5f590-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="5f590-107">These steps include:</span></span>

1.  <span data-ttu-id="5f590-108">Criar um objeto de confiança de terceira parte confiável do ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f590-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="5f590-109">Adicionar o certificado do objeto de confiança de terceira parte confiável do ADFS ao Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5f590-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="5f590-110">Adicionar provedor de declarações a uma política.</span><span class="sxs-lookup"><span data-stu-id="5f590-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="5f590-111">Registrar o provedor de declarações da conta do ADFS a um percurso do usuário.</span><span class="sxs-lookup"><span data-stu-id="5f590-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="5f590-112">Carregar a política para um locatário do Azure AD B2C e testá-la.</span><span class="sxs-lookup"><span data-stu-id="5f590-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="5f590-113">Para criar um objeto de confiança de terceira parte confiável com reconhecimento de declarações</span><span class="sxs-lookup"><span data-stu-id="5f590-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="5f590-114">Para usar o ADFS como um provedor de identidade no Azure AD (Azure Active Directory) B2C, é necessário criar um objeto de confiança de terceira parte confiável do ADFS e fornecê-lo com os parâmetros corretos.</span><span class="sxs-lookup"><span data-stu-id="5f590-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="5f590-115">Para adicionar um novo objeto de confiança de terceira parte confiável usando o snap-in de Gerenciamento do AD FS e definir manualmente as configurações, execute o seguinte procedimento em um servidor de Federação.</span><span class="sxs-lookup"><span data-stu-id="5f590-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="5f590-116">A associação em **Administradores**, ou equivalente, no computador local é o mínimo necessário para concluir este procedimento.</span><span class="sxs-lookup"><span data-stu-id="5f590-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="5f590-117">Examine os detalhes sobre como usar as contas apropriadas e associações de grupos em [Grupos Padrão Locais e de Domínio](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="5f590-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="5f590-118">Em Gerenciador do Servidor, clique em **Ferramentas** e depois selecione **Gerenciamento do ADFS**.</span><span class="sxs-lookup"><span data-stu-id="5f590-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="5f590-119">Clique em **Adicionar Objeto de Confiança de Terceira Parte Confiável**.</span><span class="sxs-lookup"><span data-stu-id="5f590-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="5f590-120">![Adicionar Objeto de Confiança de Terceira Parte Confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="5f590-121">Na página **Boas-vindas**, escolha **Reconhecimento de declaração** e clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="5f590-122">![Na página Boas-vindas, escolha Reconhecimento de declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="5f590-123">Na página **Selecionar Fonte de Dados**, clique em **Inserir dados sobre a terceira parte confiável manualmente** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="5f590-124">![Inserir dados sobre a terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="5f590-125">Na página **Especificar Nome de Exibição**, digite um nome em **Nome de exibição**, em **Notas** digite uma descrição para essa terceira parte confiável e, em seguida, clique em **Avançar** .</span><span class="sxs-lookup"><span data-stu-id="5f590-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="5f590-126">![Especifique o Nome de Exibição e notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="5f590-127">Opcional.</span><span class="sxs-lookup"><span data-stu-id="5f590-127">Optional.</span></span> <span data-ttu-id="5f590-128">Se você tiver um certificado de criptografia de token opcional, na página **Configurar Certificado**, clique em **Procurar** para localizar o arquivo de certificado e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="5f590-129">![Configurar Certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="5f590-130">Na página **Configurar URL**, marque a caixa de seleção **Habilitar o suporte para o protocolo WebSSO de SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5f590-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="5f590-131">Em **URL do serviço de SSO do SAML 2.0 da terceira parte confiável**, digite a URL do ponto de extremidade do serviço SAML (Security Assertion Markup Language) para essa terceira parte confiável e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="5f590-132">Para a **URL do serviço de SSO do SAML 2.0 da terceira parte confiável**, cole a `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="5f590-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="5f590-133">Substitua {tenant} pelo nome do locatário (por exemplo, contosob2c.onmicrosoft.com) e substitua {policy} pelo nome da política de extensões (por exemplo, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="5f590-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="5f590-134">O nome da política é aquele da qual a política de signup_or_signin herda, nesse caso é: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="5f590-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="5f590-135">Por exemplo, a URL pode ser: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="5f590-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![URL do serviço de SSO do SAML 2.0 da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="5f590-137">Na página **Configurar Identificadores**, especifique a mesma URL da etapa anterior, clique em **Adicionar** para adicioná-la à lista e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="5f590-138">![Identificadores de objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="5f590-139">Em **Escolher Política de Controle de Acesso**, escolha uma política e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="5f590-140">![Escolher a Política de Controle de Acesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="5f590-141">Na página **Pronto para Adicionar Objeto de Confiança**, examine as configurações e, em seguida, clique em **Avançar** para salvar as informações de seu objeto de confiança de terceira parte confiável.</span><span class="sxs-lookup"><span data-stu-id="5f590-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="5f590-142">![Salvar as informações de seu objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="5f590-143">Na página **Concluir**, clique em **Fechar**, essa ação exibe automaticamente a caixa de diálogo **Editar Regras de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="5f590-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="5f590-144">![Editar Regras de Declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="5f590-145">Clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="5f590-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="5f590-146">![Adicionar nova regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="5f590-147">Em **Modelo de regra de declaração**, selecione **Enviar atributos do LDAP como declarações**.</span><span class="sxs-lookup"><span data-stu-id="5f590-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="5f590-148">![Selecione Enviar atributos do LDAP como regra de modelo de declarações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="5f590-149">Forneça o **Nome da regra de declaração**.</span><span class="sxs-lookup"><span data-stu-id="5f590-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="5f590-150">Para o **Repositório de atributos**, selecione **Selecionar Active Directory** Adicione as seguintes declarações e clique em **Concluir** e em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f590-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="5f590-151">![Definir propriedades de regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="5f590-152">No Gerenciador do Servidor, selecione **Objetos de Confiança de Terceira Parte Confiável**, depois, selecione o objeto de confiança de terceira parte confiável que você criou e clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="5f590-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="5f590-153">![Editar propriedades da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="5f590-154">na janela de propriedades do objeto de confiança de terceira parte (Demonstração de B2C), clique na guia **Assinatura** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="5f590-155">![Definir assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="5f590-156">Adicione o certificado de assinatura (arquivo .cert, sem a chave privada).</span><span class="sxs-lookup"><span data-stu-id="5f590-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Adicionar seu certificado de assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="5f590-158">Na janela de propriedades do objeto de confiança da terceira parte confiável (Demonstração de B2C), clique na guia **Avançado** e altere o **Algoritmo de hash seguro** para **SHA-1**, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f590-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="5f590-159">![Definir o algoritmo de hash seguro como SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="5f590-160">Adicionar a chave de aplicativo da conta do ADFS ao Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5f590-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="5f590-161">A federação com contas do ADFS exige um segredo do cliente para a conta do ADFS para confiar no Azure AD B2C em nome do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5f590-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="5f590-162">Você precisa armazenar o certificado ADFS em seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="5f590-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="5f590-163">Vá até seu locatário do Azure AD B2C e selecione **Configurações de B2C** > **Identity Experience Framework**</span><span class="sxs-lookup"><span data-stu-id="5f590-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="5f590-164">Selecione **Chaves de Política** para exibir as chaves disponíveis no seu locatário.</span><span class="sxs-lookup"><span data-stu-id="5f590-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="5f590-165">Clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5f590-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="5f590-166">Para as **Opções**, use **Upload**.</span><span class="sxs-lookup"><span data-stu-id="5f590-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="5f590-167">Para o **Nome**, use `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5f590-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="5f590-168">O prefixo `B2C_1A_` pode ser adicionado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5f590-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="5f590-169">No Carregamento do arquivo, ** selecione seu arquivo de certificado .pfx com chave privada.</span><span class="sxs-lookup"><span data-stu-id="5f590-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="5f590-170">Observação: esse certificado (com a chave privada) deve ser o mesmo que foi emitido e usado para a terceira parte confiável do ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f590-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="5f590-171">![Carregar chave de política](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="5f590-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="5f590-172">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="5f590-172">Click **Create**</span></span>
8.  <span data-ttu-id="5f590-173">Confirme que você criou a chave `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="5f590-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="5f590-174">Adicionar um provedor de declarações à política de extensão</span><span class="sxs-lookup"><span data-stu-id="5f590-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="5f590-175">Se quiser que os usuários entrem usando a conta do ADFS, você precisará definir a conta do ADFS como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="5f590-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="5f590-176">Em outras palavras, você precisa especificar um ponto de extremidade com o qual o Azure AD B2C se comunica.</span><span class="sxs-lookup"><span data-stu-id="5f590-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="5f590-177">O ponto de extremidade fornece um conjunto de declarações que são usadas pelo Azure AD B2C para verificar se um usuário específico foi autenticado.</span><span class="sxs-lookup"><span data-stu-id="5f590-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="5f590-178">Defina o ADFS como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:</span><span class="sxs-lookup"><span data-stu-id="5f590-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="5f590-179">Abra o arquivo de política de extensão (TrustFrameworkExtensions.xml) de seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5f590-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="5f590-180">Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.</span><span class="sxs-lookup"><span data-stu-id="5f590-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="5f590-181">Localize a seção `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="5f590-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="5f590-182">Adicione o seguinte trecho XML sob o elemento `ClaimsProviders` e substitua `identityProvider` pelo DNS (valor arbitrário que indica o seu domínio) e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="5f590-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="5f590-183">Registrar o provedor de declarações da conta do ADFS a um percurso do usuário de Inscrição ou Entrada</span><span class="sxs-lookup"><span data-stu-id="5f590-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="5f590-184">Neste ponto, o provedor de identidade foi configurado.</span><span class="sxs-lookup"><span data-stu-id="5f590-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="5f590-185">No entanto, ele não está disponível em qualquer uma das telas de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="5f590-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="5f590-186">Agora você precisa adicionar o provedor de identidade da conta do ADFS ao percurso de usuário `SignUpOrSignIn` do usuário.</span><span class="sxs-lookup"><span data-stu-id="5f590-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="5f590-187">Para disponibilizá-lo, criamos uma duplicata de um percurso de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="5f590-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="5f590-188">Em seguida, nós o modificamos para inclua o provedor de identidade do ADFS:</span><span class="sxs-lookup"><span data-stu-id="5f590-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="5f590-189">Abra o arquivo base da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="5f590-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="5f590-190">Localize o elemento `<UserJourneys>` e copie todo o conteúdo do nó `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="5f590-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="5f590-191">Abra o arquivo de extensão (por exemplo, TrustFrameworkExtensions.xml) e localize o elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="5f590-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="5f590-192">Se o elemento não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="5f590-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="5f590-193">Cole todo o conteúdo do nó `<UserJournesy>` copiado como um filho do elemento `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="5f590-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="5f590-194">Exibir o botão</span><span class="sxs-lookup"><span data-stu-id="5f590-194">Display the button</span></span>
<span data-ttu-id="5f590-195">O elemento `<ClaimsProviderSelections>` define a lista de opções de seleção de provedor de declarações e sua ordem.</span><span class="sxs-lookup"><span data-stu-id="5f590-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="5f590-196">O elemento `<ClaimsProviderSelection>` é análogo a um botão de provedor de identidade em uma página de inscrição/entrada.</span><span class="sxs-lookup"><span data-stu-id="5f590-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="5f590-197">Se você adicionar um elemento `<ClaimsProviderSelection>` para a conta do ADFS, um novo botão será exibido quando um usuário chegar à página.</span><span class="sxs-lookup"><span data-stu-id="5f590-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="5f590-198">Para adicionar este elemento:</span><span class="sxs-lookup"><span data-stu-id="5f590-198">To add this element:</span></span>

1.  <span data-ttu-id="5f590-199">Localize o nó `<UserJourney>` que inclui `Id="SignUpOrSignIn"` no percurso do usuário que você acabou de copiar.</span><span class="sxs-lookup"><span data-stu-id="5f590-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="5f590-200">Localize o nó `<OrchestrationStep>` que inclui `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5f590-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="5f590-201">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="5f590-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="5f590-202">Vincular o botão a uma ação</span><span class="sxs-lookup"><span data-stu-id="5f590-202">Link the button to an action</span></span>

<span data-ttu-id="5f590-203">Agora que implementou um botão, você precisará vinculá-lo a uma ação.</span><span class="sxs-lookup"><span data-stu-id="5f590-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="5f590-204">Nesse caso, a ação destina-se a que o Azure AD B2C se comunique com a conta do ADFS para receber um token.</span><span class="sxs-lookup"><span data-stu-id="5f590-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="5f590-205">Vincule o botão a uma ação vinculando o perfil técnico ao provedor de declarações da conta do ADFS:</span><span class="sxs-lookup"><span data-stu-id="5f590-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="5f590-206">Localize o `<OrchestrationStep>` que inclui `Order="2"` no nó `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="5f590-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5f590-207">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="5f590-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="5f590-208">Certifique-se de que o `Id` tenha o mesmo valor de `TargetClaimsExchangeId` na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="5f590-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="5f590-209">Certifique-se de que `TechnicalProfileReferenceId` esteja definido como o perfil técnico criado anteriormente (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="5f590-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="5f590-210">Carregar a política ao seu locatário</span><span class="sxs-lookup"><span data-stu-id="5f590-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="5f590-211">No [Portal do Azure](https://portal.azure.com), alterne para o [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) e abra a folha do **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="5f590-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="5f590-212">Selecione **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="5f590-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="5f590-213">Abra a folha **Todas as Políticas**.</span><span class="sxs-lookup"><span data-stu-id="5f590-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="5f590-214">Selecione **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="5f590-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="5f590-215">Marque a caixa **Substituir a política caso ela exista**.</span><span class="sxs-lookup"><span data-stu-id="5f590-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="5f590-216">**Carregue** TrustFrameworkExtensions.xml e verifique se ele não falhou na validação</span><span class="sxs-lookup"><span data-stu-id="5f590-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="5f590-217">Testar a política personalizada usando a opção Executar Agora</span><span class="sxs-lookup"><span data-stu-id="5f590-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="5f590-218">Abra as **Configurações do Azure AD B2C** e acesse a **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="5f590-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5f590-219">Abra a **B2C_1A_signup_signin**, a política personalizada da RP (terceira parte confiável) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="5f590-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5f590-220">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="5f590-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="5f590-221">Você deve conseguir entrar usando a conta do ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f590-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="5f590-222">[Opcional] Registrar o provedor de declarações da conta do ADFS ao percurso de usuário de Edição de Perfil</span><span class="sxs-lookup"><span data-stu-id="5f590-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="5f590-223">Convém adicionar também o provedor de identidade da conta do ADFS ao percurso de usuário `ProfileEdit` do usuário.</span><span class="sxs-lookup"><span data-stu-id="5f590-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="5f590-224">Para disponibilizá-lo, repetimos as duas últimas etapas:</span><span class="sxs-lookup"><span data-stu-id="5f590-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="5f590-225">Exibir o botão</span><span class="sxs-lookup"><span data-stu-id="5f590-225">Display the button</span></span>
1.  <span data-ttu-id="5f590-226">Abra o arquivo de extensão de sua política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="5f590-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="5f590-227">Localize o nó `<UserJourney>` que inclui `Id="ProfileEdit"` no percurso do usuário que você acabou de copiar.</span><span class="sxs-lookup"><span data-stu-id="5f590-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="5f590-228">Localize o nó `<OrchestrationStep>` que inclui `Order="1"`</span><span class="sxs-lookup"><span data-stu-id="5f590-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="5f590-229">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="5f590-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="5f590-230">Vincular o botão a uma ação</span><span class="sxs-lookup"><span data-stu-id="5f590-230">Link the button to an action</span></span>
1.  <span data-ttu-id="5f590-231">Localize o `<OrchestrationStep>` que inclui `Order="2"` no nó `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="5f590-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="5f590-232">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="5f590-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="5f590-233">Testar a política personalizada de Edição de Perfil usando Executar Agora</span><span class="sxs-lookup"><span data-stu-id="5f590-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="5f590-234">Abra as **Configurações do Azure AD B2C** e acesse a **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="5f590-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="5f590-235">Abra **B2C_1A_signup_signin**, a política personalizada da RP (terceira parte confiável) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="5f590-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="5f590-236">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="5f590-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="5f590-237">Você deve conseguir entrar usando a conta do ADFS.</span><span class="sxs-lookup"><span data-stu-id="5f590-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="5f590-238">Baixar os arquivos da política completa</span><span class="sxs-lookup"><span data-stu-id="5f590-238">Download the complete policy files</span></span>
<span data-ttu-id="5f590-239">Opcional: recomendamos a criação de seu cenário usando seus próprios arquivos de política personalizada após a conclusão do passo a passo Introdução às políticas personalizadas.</span><span class="sxs-lookup"><span data-stu-id="5f590-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="5f590-240">Arquivos de exemplo de política apenas para referência</span><span class="sxs-lookup"><span data-stu-id="5f590-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
