---
title: Proteger recursos de nuvem com o Azure MFA e o AD FS | Microsoft Docs
description: "Esta é a página do Azure Multi-Factor Authentication que descreve como começar a usar o Azure MFA e o AD FS na nuvem."
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
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="0daf0-103">Protegendo os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS</span><span class="sxs-lookup"><span data-stu-id="0daf0-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="0daf0-104">Se sua organização for federada com o Azure Active Directory, use a Autenticação Multifator do Azure ou os Serviços de Federação do Active Directory (AD FS) para proteger os recursos que são acessados pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0daf0-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="0daf0-105">Use os procedimentos a seguir para proteger os recursos do Azure Active Directory com Autenticação Multifator do Azure ou os Serviços de Federação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0daf0-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="0daf0-106">Proteger recursos do Azure AD usando o AD FS</span><span class="sxs-lookup"><span data-stu-id="0daf0-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="0daf0-107">Para proteger seus recursos de nuvem, configure uma regra de declaração para que os Serviços de Federação do Active Directory emitem a declaração multipleauthn quando um usuário executa a verificação em duas etapas com êxito.</span><span class="sxs-lookup"><span data-stu-id="0daf0-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="0daf0-108">Essa declaração é passada para o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0daf0-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="0daf0-109">Siga este procedimento para percorrer as etapas:</span><span class="sxs-lookup"><span data-stu-id="0daf0-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="0daf0-110">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="0daf0-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="0daf0-111">À esquerda, selecione **Relações de Confiança com Terceira Parte Confiável**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0daf0-112">Clique com o botão direito do mouse na **Plataforma de Identidade do Microsoft Office 365** e selecione **Editar Regras de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="0daf0-114">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="0daf0-116">No Assistente Adicionar Regra de Declaração de Transformação, selecione **Passar ou filtrar uma Declaração de Entrada** na lista e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="0daf0-118">Dê um nome para a regra.</span><span class="sxs-lookup"><span data-stu-id="0daf0-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="0daf0-119">Selecione **Referências de Métodos de Autenticação** como o tipo de declaração Entrada.</span><span class="sxs-lookup"><span data-stu-id="0daf0-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="0daf0-120">Selecione **Passar todos os valores de declaração**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="0daf0-121">![Assistente para Adicionar Regra de Declaração de Transformação](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="0daf0-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="0daf0-122">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-122">Click **Finish**.</span></span> <span data-ttu-id="0daf0-123">Feche o Console de gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="0daf0-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="0daf0-124">IPs confiáveis para usuários federados</span><span class="sxs-lookup"><span data-stu-id="0daf0-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="0daf0-125">IPs confiáveis permitem aos administradores ignorar a verificação em duas etapas para endereços IP específicos ou para usuários federados que têm as solicitações originadas em seu próprios intranet.</span><span class="sxs-lookup"><span data-stu-id="0daf0-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="0daf0-126">As seções a seguir descrevem como configurar IPs confiáveis da Autenticação Multifator do Azure com usuários federados e desviar a verificação em duas etapas quando uma solicitação se originar de dentro de uma intranet de usuários federados.</span><span class="sxs-lookup"><span data-stu-id="0daf0-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="0daf0-127">Isso é conseguido por meio da configuração do AD FS para usar uma passagem ou filtrar um modelo de declaração de entrada com o tipo de declaração Dentro da rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="0daf0-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="0daf0-128">Este exemplo usa o Office 365 para a relação de confiança com terceira parte confiável.</span><span class="sxs-lookup"><span data-stu-id="0daf0-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="0daf0-129">Configurar as regras de declarações do AD FS</span><span class="sxs-lookup"><span data-stu-id="0daf0-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="0daf0-130">A primeira coisa que precisamos fazer é configurar as declarações do AD FS.</span><span class="sxs-lookup"><span data-stu-id="0daf0-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="0daf0-131">Criamos duas regras declarações: uma para o tipo de declaração Dentro da rede corporativa e um adicional para manter nossos usuários conectados.</span><span class="sxs-lookup"><span data-stu-id="0daf0-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="0daf0-132">Abra o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="0daf0-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="0daf0-133">À esquerda, selecione **Relações de Confiança com Terceira Parte Confiável**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0daf0-134">Clique com o botão direito do mouse na **Plataforma de Identidade Microsoft Office 365** e selecione **Editar Regras de Declaração...**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="0daf0-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="0daf0-135">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**
   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="0daf0-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="0daf0-136">No Assistente Adicionar Regra de Declaração de Transformação, selecione **Passar ou filtrar uma Declaração de Entrada** na lista e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="0daf0-137">![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="0daf0-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="0daf0-138">Na caixa ao lado do nome da regra de declaração, nomeie a regra.</span><span class="sxs-lookup"><span data-stu-id="0daf0-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="0daf0-139">Por exemplo: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="0daf0-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="0daf0-140">Na lista suspensa, ao lado do tipo de declaração de entrada, selecione **Dentro da rede corporativa**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="0daf0-141">![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="0daf0-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="0daf0-142">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-142">Click **Finish**.</span></span>
9. <span data-ttu-id="0daf0-143">Em Regras de Transformação de Emissão, clique em **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="0daf0-144">No Assistente Adicionar Regra de Declaração de Transformação, selecione **Enviar Declarações Usando uma Regra Personalizada** da lista suspensa e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="0daf0-145">Na caixa abaixo do nome da regra de declaração: insira *Manter Usuários Conectados*.</span><span class="sxs-lookup"><span data-stu-id="0daf0-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="0daf0-146">Na caixa de regra Personalizada, digite:</span><span class="sxs-lookup"><span data-stu-id="0daf0-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="0daf0-148">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-148">Click **Finish**.</span></span>
14. <span data-ttu-id="0daf0-149">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-149">Click **Apply**.</span></span>
15. <span data-ttu-id="0daf0-150">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-150">Click **Ok**.</span></span>
16. <span data-ttu-id="0daf0-151">Feche o gerenciamento do AD FS.</span><span class="sxs-lookup"><span data-stu-id="0daf0-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="0daf0-152">Configurar IPs confiáveis do Azure Multi-Factor Authentication com usuários federados</span><span class="sxs-lookup"><span data-stu-id="0daf0-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="0daf0-153">Agora que as declarações estão prontas, podemos configurar IPs confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0daf0-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="0daf0-154">Entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0daf0-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0daf0-155">À esquerda, clique em **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="0daf0-156">Em Diretório, selecione o diretório onde você deseja configurar IPs confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0daf0-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="0daf0-157">No Diretório que você selecionou, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="0daf0-158">Na seção autenticação multifator, clique em **Gerenciar configurações de serviço**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="0daf0-159">Na página Configurações de Serviço, em IPs confiáveis, selecione **Ignorar autenticação multifator para solicitações de usuários federados na minha intranet**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Nuvem](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="0daf0-161">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-161">Click **save**.</span></span>
8. <span data-ttu-id="0daf0-162">Depois que as atualizações forem aplicadas, clique em **fechar**.</span><span class="sxs-lookup"><span data-stu-id="0daf0-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="0daf0-163">É isso!</span><span class="sxs-lookup"><span data-stu-id="0daf0-163">That’s it!</span></span> <span data-ttu-id="0daf0-164">Neste ponto, os usuários federados do Office 365 devem somente ter que usar MFA quando uma declaração for originada fora da intranet corporativa.</span><span class="sxs-lookup"><span data-stu-id="0daf0-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
