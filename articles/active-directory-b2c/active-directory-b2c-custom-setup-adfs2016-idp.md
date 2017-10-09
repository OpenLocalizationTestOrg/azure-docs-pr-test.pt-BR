---
title: "Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas"
description: "Um como-tooarticle sobre como configurar o ADFS 2016 usando o protocolo SAML e políticas personalizadas"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="d7fb6-103">Azure Active Directory B2C: Adicionar ADFS como um provedor de identidade SAML usando políticas personalizadas</span><span class="sxs-lookup"><span data-stu-id="d7fb6-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="d7fb6-104">Este artigo mostra como tooenable entrar para usuários de conta do AD FS através do uso de saudação do [políticas personalizadas](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-104">This article shows you how tooenable sign-in for users from ADFS account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7fb6-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d7fb6-105">Prerequisites</span></span>

<span data-ttu-id="d7fb6-106">Olá concluir as etapas em Olá [guia de Introdução com políticas personalizadas](active-directory-b2c-get-started-custom.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="d7fb6-107">As etapas incluem:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-107">These steps include:</span></span>

1.  <span data-ttu-id="d7fb6-108">Criar um objeto de confiança de terceira parte confiável do ADFS.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="d7fb6-109">Adicionando Olá ADFS terceira parte confiável certificado tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-109">Adding hello ADFS Relying Party Trust certificate tooAzure AD B2C.</span></span>
3.  <span data-ttu-id="d7fb6-110">Adicionar política de tooa do provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-110">Adding claims provider tooa policy.</span></span>
4.  <span data-ttu-id="d7fb6-111">Conta ADFS Olá registrar declarações jornada de usuário do provedor tooa.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-111">Registering hello ADFS account claims provider tooa user journey.</span></span>
5.  <span data-ttu-id="d7fb6-112">Carregando tooan de política de saudação do Azure AD B2C locatário e testá-lo.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-112">Uploading hello policy tooan Azure AD B2C tenant and test it.</span></span>

## <a name="toocreate-a-claims-aware-relying-party-trust"></a><span data-ttu-id="d7fb6-113">toocreate uma terceira parte confiável com reconhecimento de declarações</span><span class="sxs-lookup"><span data-stu-id="d7fb6-113">toocreate a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="d7fb6-114">toouse ADFS como um provedor de identidade em B2C do Azure Active Directory (AD do Azure), você precisa toocreate um ADFS terceira parte confiável e fornecê-lo com os parâmetros de saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-114">toouse ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an ADFS Relying Party Trust and supply it with hello right parameters.</span></span>

<span data-ttu-id="d7fb6-115">tooadd uma terceira parte confiável nova confiança usando o snap-in de gerenciamento de TI de saudação AD e configurar manualmente as definições de hello, executar Olá procedimento a seguir em um servidor de Federação.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-115">tooadd a new relying party trust by using hello AD FS Management snap-in and manually configure hello settings, perform hello following procedure on a federation server.</span></span>

<span data-ttu-id="d7fb6-116">Associação **administradores**, ou equivalente, no computador local Olá toocomplete necessária mínima de saudação esse procedimento.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-116">Membership in **Administrators**, or equivalent, on hello local computer is hello minimum required toocomplete this procedure.</span></span> <span data-ttu-id="d7fb6-117">Examine os detalhes sobre como usar as contas apropriadas hello e associações dos grupos em [locais e grupos do domínio padrão](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-117">Review details about using hello appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="d7fb6-118">Em Gerenciador do Servidor, clique em **Ferramentas** e depois selecione **Gerenciamento do ADFS**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="d7fb6-119">Clique em **Adicionar Objeto de Confiança de Terceira Parte Confiável**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="d7fb6-120">![Adicionar Objeto de Confiança de Terceira Parte Confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="d7fb6-121">Em Olá **bem-vindo** escolha **reconhecimento de declaração** e clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-121">On hello **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="d7fb6-122">![Na página de boas-vindas hello, escolha o reconhecimento de declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-122">![On hello Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="d7fb6-123">Em Olá **Selecionar fonte de dados** , clique em **inserir manualmente dados sobre a terceira parte confiável Olá**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-123">On hello **Select Data Source** page, click **Enter data about hello relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="d7fb6-124">![Inserir dados sobre a terceira parte confiável Olá](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-124">![Enter data about hello relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="d7fb6-125">Em Olá **especificar nome para exibição** página, digite um nome na **nome de exibição**, em **notas** digite uma descrição para essa terceira parte confiável e, em seguida, clique em **Avançar** .</span><span class="sxs-lookup"><span data-stu-id="d7fb6-125">On hello **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="d7fb6-126">![Especifique o Nome de Exibição e notas](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="d7fb6-127">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-127">Optional.</span></span> <span data-ttu-id="d7fb6-128">Se você tem um certificado de criptografia de token opcional, em seguida, em Olá **configurar certificado** , clique em **procurar** toolocate o arquivo de certificado e clique **próximo** .</span><span class="sxs-lookup"><span data-stu-id="d7fb6-128">If you have an optional token encryption certificate, then on hello **Configure Certificate** page, click **Browse** toolocate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="d7fb6-129">![Configurar Certificado](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="d7fb6-130">Em Olá **configurar URL** página, selecione Olá **habilitar o suporte para o protocolo WebSSO do SAML 2.0 de saudação** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-130">On hello **Configure URL** page, select hello **Enable support for hello SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="d7fb6-131">Em **URL do serviço de SSO do SAML 2.0 terceira parte confiável**, digite a URL do ponto de extremidade de serviço do hello SAML Security Assertion Markup Language () para essa terceira parte confiável e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-131">Under **Relying party SAML 2.0 SSO service URL**, type hello Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="d7fb6-132">Para Olá **URL do serviço de SSO do SAML 2.0 terceira parte confiável**, cole Olá `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-132">For hello **Relying party SAML 2.0 SSO service URL**, paste hello `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="d7fb6-133">Substitua {Locatário} com o nome do locatário (por exemplo, contosob2c.onmicrosoft.com) e Olá {política} com o nome da política extensões (por exemplo, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace hello {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="d7fb6-134">nome da política Olá é Olá uma política signup_or_signin herda, nesse caso é: `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-134">hello policy name  is hello one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="d7fb6-135">Por exemplo hello URL pode ser: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-135">For example hello URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![URL do serviço de SSO do SAML 2.0 da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="d7fb6-137">Em Olá **configurar identificadores** especifique Olá mesma URL da etapa anterior de saudação, clique em **adicionar** tooadd-los toohello lista e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-137">On hello **Configure Identifiers** page, specify hello same URL as hello previous step, click **Add** tooadd them toohello list, and then click **Next**.</span></span>
    <span data-ttu-id="d7fb6-138">![Identificadores de objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="d7fb6-139">Em Olá **escolha política de controle de acesso** selecione uma política e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-139">On hello **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="d7fb6-140">![Escolher a Política de Controle de Acesso](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="d7fb6-141">Em Olá **pronto tooAdd confiança** página, examine as configurações de saudação e, em seguida, clique em **próximo** toosave informações de confiança de sua terceira parte confiável.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-141">On hello **Ready tooAdd Trust** page, review hello settings, and then click **Next** toosave your relying party trust information.</span></span>
    <span data-ttu-id="d7fb6-142">![Salvar as informações de seu objeto de confiança de terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="d7fb6-143">Em Olá **concluir** , clique em **fechar**, essa ação exibe automaticamente Olá **editar regras de declaração** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-143">On hello **Finish** page, click **Close**, this action automatically displays hello **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="d7fb6-144">![Editar Regras de Declaração](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="d7fb6-145">Clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="d7fb6-146">![Adicionar nova regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="d7fb6-147">Em **Modelo de regra de declaração**, selecione **Enviar atributos do LDAP como declarações**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="d7fb6-148">![Selecione Enviar atributos do LDAP como regra de modelo de declarações](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="d7fb6-149">Forneça o **Nome da regra de declaração**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="d7fb6-150">Para Olá **repositório de atributos** selecione **selecione Active Directory** adicionar Olá declarações a seguir e clique em **concluir** e **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-150">For hello **Attribute store** select **Select Active Directory** Add hello following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="d7fb6-151">![Definir propriedades de regra](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="d7fb6-152">No Gerenciador do servidor, selecione **terceira parte confiável** , em seguida, selecione Olá terceira parte confiável é criado e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-152">In Server Manager, select **Relying Party Trusts** then select hello relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="d7fb6-153">![Editar propriedades da terceira parte confiável](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="d7fb6-154">Uma terceira parte confiáveis (B2C demonstração) propriedades janela clique de Olá **assinatura** guia e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-154">One hello relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="d7fb6-155">![Definir assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="d7fb6-156">Adicione o certificado de assinatura (arquivo .cert, sem a chave privada).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Adicionar seu certificado de assinatura](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="d7fb6-158">Na janela de propriedades do hello terceira parte confiáveis (B2C demonstração) clique em **avançado** guia e alterar Olá **algoritmo de hash seguro** muito**SHA-1**, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-158">On hello relying party trust (B2C Demo) properties window click **Advanced** tab and change hello **Secure hash algorithm** too**SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="d7fb6-159">![Definir o algoritmo de hash seguro tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-159">![Set secure hash algorithm tooSHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="d7fb6-160">Adicionar tooAzure de chave aplicativo AD B2C de conta ADFS Olá</span><span class="sxs-lookup"><span data-stu-id="d7fb6-160">Add hello ADFS account application key tooAzure AD B2C</span></span>
<span data-ttu-id="d7fb6-161">Federação com contas do AD FS requer um segredo do cliente para ADFS tootrust de conta do Azure AD B2C em nome do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-161">Federation with ADFS accounts requires a client secret for ADFS account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="d7fb6-162">Você precisa toostore seu certificado do AD FS no seu locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-162">You need toostore your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="d7fb6-163">Vá locatário tooyour B2C do Azure AD e selecione **B2C configurações** > **Framework de experiência de identidade**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-163">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="d7fb6-164">Selecione **chaves política** tooview chaves de saudação disponíveis em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-164">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="d7fb6-165">Clique em **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="d7fb6-166">Para as **Opções**, use **Upload**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="d7fb6-167">Para o **Nome**, use `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="d7fb6-168">prefixo de saudação `B2C_1A_` podem ser adicionadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-168">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="d7fb6-169">No carregamento do arquivo hello, * * selecione o arquivo. pfx de certificado com chave privada.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-169">In hello File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="d7fb6-170">Observação: este certificado (com a chave privada de saudação) deve ser Olá aquele mesmo que emitidos e usados para a terceira parte confiável Olá ADFS.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-170">Note: this certificate (with hello private key) should be hello same one that issued and used for hello ADFS relying party.</span></span>
<span data-ttu-id="d7fb6-171">![Carregar chave de política](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="d7fb6-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="d7fb6-172">Clique em **Criar**</span><span class="sxs-lookup"><span data-stu-id="d7fb6-172">Click **Create**</span></span>
8.  <span data-ttu-id="d7fb6-173">Confirme que você criou a chave Olá `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-173">Confirm that you've created hello key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="d7fb6-174">Adicionar um provedor de declarações à política de extensão</span><span class="sxs-lookup"><span data-stu-id="d7fb6-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="d7fb6-175">Se você quiser usuários toosign no usando a conta do AD FS, você precisa de conta ADFS toodefine como um provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-175">If you want users toosign in by using ADFS account, you need toodefine ADFS account as a claims provider.</span></span> <span data-ttu-id="d7fb6-176">Em outras palavras, você precisa toospecify do Azure AD B2C se comunica com um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-176">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="d7fb6-177">ponto de extremidade Olá fornece um conjunto de declarações que são usados pelo Azure AD B2C tooverify que um usuário específico autenticado.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-177">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="d7fb6-178">Defina o ADFS como um provedor de declarações adicionando o nó `<ClaimsProvider>` em seu arquivo de política da extensão:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="d7fb6-179">Abra o arquivo de política de extensão de saudação (TrustFrameworkExtensions.xml) do seu diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-179">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="d7fb6-180">Se você precisar de um editor de XML, [experimente o Visual Studio Code](https://code.visualstudio.com/download), um editor de plataforma cruzada leve.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="d7fb6-181">Localize Olá `<ClaimsProviders>` seção</span><span class="sxs-lookup"><span data-stu-id="d7fb6-181">Find hello `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="d7fb6-182">Adicionar Olá seguindo o trecho XML em Olá `ClaimsProviders` elemento e substituir `identityProvider` com o DNS (valor arbitrário que indica o seu domínio) e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-182">Add hello following XML snippet under hello `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save hello file.</span></span> 

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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="d7fb6-183">Registrar tooSign de provedor de declarações do hello ADFS conta se ou entrar a jornada de usuário</span><span class="sxs-lookup"><span data-stu-id="d7fb6-183">Register hello ADFS account claims provider tooSign up or Sign in user journey</span></span>
<span data-ttu-id="d7fb6-184">Neste ponto, o provedor de identidade Olá configurado.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-184">At this point, hello identity provider has been set up.</span></span>  <span data-ttu-id="d7fb6-185">No entanto, não está disponível em qualquer uma das telas de entrada-o/entrada hello.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-185">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="d7fb6-186">Agora você precisa tooadd Olá ADFS conta identidade tooyour de usuário do provedor `SignUpOrSignIn` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-186">Now you need tooadd hello ADFS account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="d7fb6-187">toomake-lo, podemos criar uma duplicata de uma jornada de usuário do modelo existente.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-187">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="d7fb6-188">Em seguida, podemos modificá-la para que ela inclua o provedor de identidade ADFS hello:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-188">Then, we modify it so it includes hello ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="d7fb6-189">Abra o arquivo de base de saudação da política (por exemplo, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-189">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="d7fb6-190">Localize Olá `<UserJourneys>` elemento e cópia Olá todo conteúdo do `<UserJourneys>` nó.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-190">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="d7fb6-191">Abra o arquivo de extensão da saudação (por exemplo, TrustFrameworkExtensions.xml) e localize Olá `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-191">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="d7fb6-192">Se o elemento de saudação não existir, adicione um.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-192">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="d7fb6-193">Cole a todo o conteúdo de saudação `<UserJournesy>` nó que você copiou como um filho do hello `<UserJourneys>` elemento.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-193">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="d7fb6-194">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="d7fb6-194">Display hello button</span></span>
<span data-ttu-id="d7fb6-195">Olá `<ClaimsProviderSelections>` elemento define a lista de saudação das opções de seleção de provedor de declarações e sua ordem.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-195">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="d7fb6-196">`<ClaimsProviderSelection>`elemento é análogo tooan botão de provedor de identidade em uma página de entrada-o/entrar.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-196">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="d7fb6-197">Se você adicionar um `<ClaimsProviderSelection>` elemento para a conta do AD FS, um novo botão aparece quando um usuário chega na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="d7fb6-198">tooadd este elemento:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-198">tooadd this element:</span></span>

1.  <span data-ttu-id="d7fb6-199">Localize Olá `<UserJourney>` nó inclui `Id="SignUpOrSignIn"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-199">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="d7fb6-200">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="d7fb6-200">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="d7fb6-201">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="d7fb6-202">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="d7fb6-202">Link hello button tooan action</span></span>

<span data-ttu-id="d7fb6-203">Agora que você tem um botão em vigor, é necessário toolink-tooan ação.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-203">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="d7fb6-204">ação de Olá, nesse caso, é para o Azure AD B2C toocommunicate com ADFS conta tooreceive um token.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-204">hello action, in this case, is for Azure AD B2C toocommunicate with ADFS account tooreceive a token.</span></span> <span data-ttu-id="d7fb6-205">Ação de link Olá botão tooan vinculando perfil técnico Olá para o seu provedor de declarações do ADFS conta:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-205">Link hello button tooan action by linking hello technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="d7fb6-206">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-206">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="d7fb6-207">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="d7fb6-208">Certifique-se de saudação `Id` tem Olá mesmo valor de `TargetClaimsExchangeId` em Olá anterior seção.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-208">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section.</span></span>
> * <span data-ttu-id="d7fb6-209">Certifique-se de `TechnicalProfileReferenceId` é definido toohello perfil técnico que você criou anteriormente (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-209">Ensure `TechnicalProfileReferenceId` is set toohello technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="d7fb6-210">Carregar o locatário de tooyour política Olá</span><span class="sxs-lookup"><span data-stu-id="d7fb6-210">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="d7fb6-211">Em Olá [portal do Azure](https://portal.azure.com), alternar para Olá [contexto do seu locatário do Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)e abra hello **do Azure AD B2C** folha.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-211">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="d7fb6-212">Selecione **Estrutura de Experiência de Identidade**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="d7fb6-213">Olá abrir **todas as políticas** folha.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-213">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="d7fb6-214">Selecione **Carregar Política**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="d7fb6-215">Verificar **substituir a política de saudação se ela existe** caixa.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-215">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="d7fb6-216">**Carregar** TrustFrameworkExtensions.xml e certifique-se de que ele não falha na validação de saudação</span><span class="sxs-lookup"><span data-stu-id="d7fb6-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="d7fb6-217">Testar a política personalizada do hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="d7fb6-217">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="d7fb6-218">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-218">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="d7fb6-219">Abra **B2C_1A_signup_signin**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-219">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="d7fb6-220">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="d7fb6-221">Você deve ser capaz de toosign usando a conta do AD FS.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-221">You should be able toosign in using ADFS account.</span></span>

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="d7fb6-222">[Opcional] Registrar a jornada do hello ADFS conta declarações provedor tooProfile Editar usuário</span><span class="sxs-lookup"><span data-stu-id="d7fb6-222">[Optional] Register hello ADFS account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="d7fb6-223">Você pode querer provedor de identidade de conta tooadd Olá ADFS também tooyour usuário `ProfileEdit` jornada de usuário.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-223">You may want tooadd hello ADFS account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="d7fb6-224">toomake disponível, podemos Repita Olá último duas etapas:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-224">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="d7fb6-225">Botão de saudação de exibição</span><span class="sxs-lookup"><span data-stu-id="d7fb6-225">Display hello button</span></span>
1.  <span data-ttu-id="d7fb6-226">Abra o arquivo de extensão de saudação da política (por exemplo, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="d7fb6-226">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="d7fb6-227">Localize Olá `<UserJourney>` nó inclui `Id="ProfileEdit"` em jornada saudação do usuário que você copiou.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-227">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="d7fb6-228">Localizar Olá `<OrchestrationStep>` nó inclui`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="d7fb6-228">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="d7fb6-229">Adicione o seguinte trecho XML ao nó `<ClaimsProviderSelections>`:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="d7fb6-230">Ação de link de saudação botão tooan</span><span class="sxs-lookup"><span data-stu-id="d7fb6-230">Link hello button tooan action</span></span>
1.  <span data-ttu-id="d7fb6-231">Localize Olá `<OrchestrationStep>` que inclui `Order="2"` em Olá `<UserJourney>` nó.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-231">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="d7fb6-232">Adicione o seguinte trecho XML ao nó `<ClaimsExchanges>`:</span><span class="sxs-lookup"><span data-stu-id="d7fb6-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="d7fb6-233">Testar a política personalizada de perfil Editar hello usando Executar agora</span><span class="sxs-lookup"><span data-stu-id="d7fb6-233">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="d7fb6-234">Abra **configurações do Azure AD B2C** e vá muito**identidade experiência Framework**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-234">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="d7fb6-235">Abra **B2C_1A_ProfileEdit**, Olá política personalizada do terceira parte confiável (RP) que você carregou.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-235">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="d7fb6-236">Selecione **Executar Agora**.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="d7fb6-237">Você deve ser capaz de toosign usando a conta do AD FS.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-237">You should be able toosign in using ADFS account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="d7fb6-238">Baixar arquivos de política completa Olá</span><span class="sxs-lookup"><span data-stu-id="d7fb6-238">Download hello complete policy files</span></span>
<span data-ttu-id="d7fb6-239">Opcional: É recomendável que criar o seu cenário usando seus próprios arquivos de política personalizada após a conclusão Olá guia de Introdução com as políticas personalizadas percorrer.</span><span class="sxs-lookup"><span data-stu-id="d7fb6-239">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="d7fb6-240">Arquivos de exemplo de política apenas para referência</span><span class="sxs-lookup"><span data-stu-id="d7fb6-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
