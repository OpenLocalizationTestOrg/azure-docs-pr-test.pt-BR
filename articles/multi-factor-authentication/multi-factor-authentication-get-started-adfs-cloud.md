---
title: recursos de nuvem aaaSecure com o Azure MFA e AD FS | Microsoft Docs
description: "Esta é hello Azure multi-Factor authentication página que descreve como tooget iniciada com o Azure MFA e AD FS na nuvem hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="c4f4a-103">Protegendo os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS</span><span class="sxs-lookup"><span data-stu-id="c4f4a-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="c4f4a-104">Se sua organização for federada com o Active Directory do Azure, use o Azure multi-Factor Authentication ou os recursos de toosecure os serviços de Federação do Active Directory (AD FS) que são acessados pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="c4f4a-105">Saudação de usar recursos do Active Directory do Azure procedimentos toosecure com autenticação multifator do Azure ou os serviços de Federação do Active Directory a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="c4f4a-106">Proteger recursos do Azure AD usando o AD FS</span><span class="sxs-lookup"><span data-stu-id="c4f4a-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="c4f4a-107">toosecure seu recurso de nuvem, configurar uma regra de declarações para que os serviços de Federação do Active Directory emite a declaração de multipleauthn hello quando um usuário executa a verificação em duas etapas com êxito.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="c4f4a-108">Esta declaração é passada no tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="c4f4a-109">Siga este toowalk procedimento etapas hello:</span><span class="sxs-lookup"><span data-stu-id="c4f4a-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="c4f4a-110">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="c4f4a-111">Olá esquerda, selecione **terceira parte confiável**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="c4f4a-112">Clique com o botão direito do mouse na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="c4f4a-114">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="c4f4a-116">Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **passar ou filtrar uma declaração de entrada** de Olá suspensa e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="c4f4a-118">Dê um nome para a regra.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="c4f4a-119">Selecione **referências de métodos de autenticação** como Olá entrada o tipo de declaração.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="c4f4a-120">Selecione **Passar todos os valores de declaração**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="c4f4a-121">![Assistente para Adicionar Regra de Declaração de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="c4f4a-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="c4f4a-122">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-122">Click **Finish**.</span></span> <span data-ttu-id="c4f4a-123">Feche o console de gerenciamento FS Olá AD.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="c4f4a-124">IPs confiáveis para usuários federados</span><span class="sxs-lookup"><span data-stu-id="c4f4a-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="c4f4a-125">IPs confiáveis permitem que os administradores tooby passagem verificação de duas etapas para endereços IP específicos, ou para usuários federados que têm as solicitações originadas dentro de sua própria intranet.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="c4f4a-126">Olá seções a seguir descrevem como tooconfigure autenticação multifator do Azure confiável IPs com usuários federados e verificação em duas etapas de desviar quando uma solicitação se origina de dentro de uma intranet de usuários federados.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="c4f4a-127">Isso é conseguido por meio da configuração do AD FS toouse passagem ou filtro de um modelo de declaração de entrada com hello tipo de declaração de dentro da rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="c4f4a-128">Este exemplo usa o Office 365 para a relação de confiança com terceira parte confiável.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="c4f4a-129">Configurar regras de declarações de saudação do AD FS</span><span class="sxs-lookup"><span data-stu-id="c4f4a-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="c4f4a-130">Olá primeira coisa a toodo é tooconfigure declarações de saudação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="c4f4a-131">Crie duas regras de declarações, um para hello dentro da rede corporativa de declaração de tipo e um adicional para manter nossos usuários conectados.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="c4f4a-132">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="c4f4a-133">Olá esquerda, selecione **terceira parte confiável**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="c4f4a-134">Clique com o botão direito do mouse na **Plataforma de Identidade Microsoft Office 365** e selecione **Editar Regras de Declaração...**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="c4f4a-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="c4f4a-135">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="c4f4a-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="c4f4a-136">Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **passar ou filtrar uma declaração de entrada** de Olá suspensa e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="c4f4a-137">![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="c4f4a-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="c4f4a-138">Em Olá caixa próxima tooClaim nome da regra, nomeie a regra.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="c4f4a-139">Por exemplo: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="c4f4a-140">No hello suspenso, tooIncoming próximo tipo de declaração, selecione **dentro da rede corporativa**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="c4f4a-141">![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="c4f4a-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="c4f4a-142">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-142">Click **Finish**.</span></span>
9. <span data-ttu-id="c4f4a-143">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="c4f4a-144">Em Olá Adicionar Assistente de regra de declaração de transformação, selecione **enviar declarações usando uma regra personalizada** de Olá suspensa e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="c4f4a-145">Na caixa Nome da regra de declaração Olá: insira *manter usuários assinado em*.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="c4f4a-146">Na caixa de regra personalizada hello, digite:</span><span class="sxs-lookup"><span data-stu-id="c4f4a-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="c4f4a-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-148">Click **Finish**.</span></span>
14. <span data-ttu-id="c4f4a-149">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-149">Click **Apply**.</span></span>
15. <span data-ttu-id="c4f4a-150">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-150">Click **Ok**.</span></span>
16. <span data-ttu-id="c4f4a-151">Feche o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="c4f4a-152">Configurar IPs confiáveis do Azure Multi-Factor Authentication com usuários federados</span><span class="sxs-lookup"><span data-stu-id="c4f4a-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="c4f4a-153">Agora que as declarações de saudação entram em vigor, é possível configurar IPs confiáveis.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="c4f4a-154">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c4f4a-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c4f4a-155">Olá esquerda, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="c4f4a-156">Em diretório, selecione o diretório de saudação onde você deseja tooset backup IPs confiáveis.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="c4f4a-157">No hello diretório que você selecionou, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="c4f4a-158">Na seção de autenticação multifator hello, clique em **gerenciar configurações de serviço**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="c4f4a-159">Na página de configurações do serviço de hello, em IPs confiáveis, selecione **ignorar o multi-factor-autenticação de solicitações de usuários federados na minha intranet**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="c4f4a-161">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-161">Click **save**.</span></span>
8. <span data-ttu-id="c4f4a-162">Depois de saudação atualizações foram aplicadas, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="c4f4a-163">É isso!</span><span class="sxs-lookup"><span data-stu-id="c4f4a-163">That’s it!</span></span> <span data-ttu-id="c4f4a-164">Neste ponto, os usuários federados do Office 365 devem ter somente toouse MFA quando uma reivindicação tem origem fora da intranet corporativa hello.</span><span class="sxs-lookup"><span data-stu-id="c4f4a-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
