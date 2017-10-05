---
title: "Guia estratégico do Azure Active Directory Identity Protection | Microsoft Docs"
description: Saiba como o Azure AD Identity Protection permite limitar a capacidade de um invasor de explorar uma identidade ou um dispositivo comprometidos ou um dispositivo que sofreu comprometimento conhecido ou suspeito anteriormente.
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="799f2-104">Guia estratégico do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="799f2-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="799f2-105">Este guia estratégico vai ajudá-lo a:</span><span class="sxs-lookup"><span data-stu-id="799f2-105">This playbook helps you to:</span></span>

* <span data-ttu-id="799f2-106">Popular dados no ambiente do Identity Protection, simulando eventos de riscos e vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="799f2-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="799f2-107">Configurar políticas de acesso condicional baseadas em risco e testar o impacto dessas políticas</span><span class="sxs-lookup"><span data-stu-id="799f2-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="799f2-108">Simulação de Eventos de Risco</span><span class="sxs-lookup"><span data-stu-id="799f2-108">Simulating Risk Events</span></span>
<span data-ttu-id="799f2-109">Esta seção fornece as etapas para simular os seguintes tipos de evento de risco:</span><span class="sxs-lookup"><span data-stu-id="799f2-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="799f2-110">Entradas de endereços IP anônimos (fácil)</span><span class="sxs-lookup"><span data-stu-id="799f2-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="799f2-111">Entradas de locais desconhecidos (moderado)</span><span class="sxs-lookup"><span data-stu-id="799f2-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="799f2-112">Viagem impossível a locais atípicos (difícil)</span><span class="sxs-lookup"><span data-stu-id="799f2-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="799f2-113">Outros eventos de risco não podem ser simulados de maneira segura.</span><span class="sxs-lookup"><span data-stu-id="799f2-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="799f2-114">Entradas de endereços IP anônimos</span><span class="sxs-lookup"><span data-stu-id="799f2-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="799f2-115">Esse tipo de evento de risco identifica os usuários que entraram com êxito de um endereço IP que foi identificado como um endereço IP de proxy anônimo.</span><span class="sxs-lookup"><span data-stu-id="799f2-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="799f2-116">Esses proxies geralmente são usados por usuários que desejam ocultar o endereço IP de seu dispositivo e podem ser usados com objetivos mal-intencionados.</span><span class="sxs-lookup"><span data-stu-id="799f2-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="799f2-117">**Para simular uma entrada de um IP anônimo, realize as seguintes etapas**:</span><span class="sxs-lookup"><span data-stu-id="799f2-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="799f2-118">Baixe o [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="799f2-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="799f2-119">Usando o Tor Browser, navegue até [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="799f2-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="799f2-120">Insira as credenciais da conta que deseja exibir no relatório **Entradas de endereços IP anônimos** .</span><span class="sxs-lookup"><span data-stu-id="799f2-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="799f2-121">A entrada será exibida no painel do Identity Protection dentro de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="799f2-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="799f2-122">Entradas de locais desconhecidos</span><span class="sxs-lookup"><span data-stu-id="799f2-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="799f2-123">O risco de locais desconhecidos é um mecanismo de avaliação de entrada em tempo real que considera locais de entrada anteriores (IP, Latitude/Longitude e ASN) para determinar os locais novos/desconhecidos.</span><span class="sxs-lookup"><span data-stu-id="799f2-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="799f2-124">O sistema armazena IPs, Latitude/Longitude e ASNs anteriores de um usuário e os considera como locais “conhecidos”.</span><span class="sxs-lookup"><span data-stu-id="799f2-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="799f2-125">Um local de entrada é considerado desconhecido se não corresponder a nenhum dos locais familiares existentes.</span><span class="sxs-lookup"><span data-stu-id="799f2-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="799f2-126">Azure Active Directory Identity Protection:</span><span class="sxs-lookup"><span data-stu-id="799f2-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="799f2-127">tem um período inicial de aprendizado de 14 dias, durante o qual ele não sinaliza nenhum local novo como desconhecido.</span><span class="sxs-lookup"><span data-stu-id="799f2-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="799f2-128">ignora entradas de dispositivos conhecidos e locais que estão geograficamente próximos de um local conhecido existente.</span><span class="sxs-lookup"><span data-stu-id="799f2-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="799f2-129">Para simular locais desconhecidos, você precisa entrar de um local e um dispositivo nunca utilizados para entrada na conta.</span><span class="sxs-lookup"><span data-stu-id="799f2-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="799f2-130">**Para simular uma entrada de um local desconhecido, realize as seguintes etapas**:</span><span class="sxs-lookup"><span data-stu-id="799f2-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="799f2-131">Escolha uma conta com um histórico de entrada de, pelo menos, 14 dias.</span><span class="sxs-lookup"><span data-stu-id="799f2-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="799f2-132">Realize uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="799f2-132">Do either:</span></span>
   
   <span data-ttu-id="799f2-133">a.</span><span class="sxs-lookup"><span data-stu-id="799f2-133">a.</span></span> <span data-ttu-id="799f2-134">Usando uma VPN, navegue até [https://myapps.microsoft.com](https://myapps.microsoft.com) e insira as credenciais da conta para a qual deseja simular o evento de risco.</span><span class="sxs-lookup"><span data-stu-id="799f2-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="799f2-135">b.</span><span class="sxs-lookup"><span data-stu-id="799f2-135">b.</span></span> <span data-ttu-id="799f2-136">Peça que um colega de um local diferente entre usando as credenciais da conta (não recomendado).</span><span class="sxs-lookup"><span data-stu-id="799f2-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="799f2-137">A entrada será exibida no painel do Identity Protection dentro de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="799f2-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="799f2-138">Viagem impossível a um local atípico</span><span class="sxs-lookup"><span data-stu-id="799f2-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="799f2-139">É difícil simular a condição de viagem impossível porque o algoritmo usa o aprendizado de máquina para eliminar falsos positivos, tais como viagens impossíveis de dispositivos conhecidos ou entradas de VPNs usadas por outros usuários no diretório.</span><span class="sxs-lookup"><span data-stu-id="799f2-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="799f2-140">Além disso, o algoritmo exige um histórico de entrada de três a 14 dias para o usuário antes de começar a gerar eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="799f2-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="799f2-141">**Para simular uma viagem impossível para um local atípico, realize as seguintes etapas**:</span><span class="sxs-lookup"><span data-stu-id="799f2-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="799f2-142">Usando seu navegador padrão, navegue até [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="799f2-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="799f2-143">Insira as credenciais da conta para a qual deseja gerar um evento de risco de viagem impossível.</span><span class="sxs-lookup"><span data-stu-id="799f2-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="799f2-144">Altere o agente do usuário.</span><span class="sxs-lookup"><span data-stu-id="799f2-144">Change your user agent.</span></span> <span data-ttu-id="799f2-145">É possível alterar o agente do usuário no Internet Explorer nas Ferramentas de Desenvolvedor ou então no Firefox ou Chrome usando um complemento de alternador de agente do usuário.</span><span class="sxs-lookup"><span data-stu-id="799f2-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="799f2-146">Altere seu endereço IP.</span><span class="sxs-lookup"><span data-stu-id="799f2-146">Change your IP address.</span></span> <span data-ttu-id="799f2-147">É possível alterar seu endereço IP usando uma VPN, um complemento do Tor ou criando um novo computador no Azure em um diferente.</span><span class="sxs-lookup"><span data-stu-id="799f2-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="799f2-148">Entre em [https://myapps.microsoft.com](https://myapps.microsoft.com) usando as mesmas credenciais de antes, alguns minutos após a entrada anterior.</span><span class="sxs-lookup"><span data-stu-id="799f2-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="799f2-149">A entrada será exibida no painel do Identity Protection dentro de 2 a 4 horas.</span><span class="sxs-lookup"><span data-stu-id="799f2-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="799f2-150">Devido aos complexos modelos de aprendizado de máquina envolvidos, há uma chance de que isso não seja captado.</span><span class="sxs-lookup"><span data-stu-id="799f2-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="799f2-151">É conveniente replicar essas etapas para várias contas do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="799f2-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="799f2-152">Simulação de vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="799f2-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="799f2-153">Vulnerabilidades são pontos fracos no seu ambiente do Azure AD que podem ser explorados por um ator maligno.</span><span class="sxs-lookup"><span data-stu-id="799f2-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="799f2-154">Atualmente, três tipos de vulnerabilidades são exibidas no Azure AD Identity Protection que aproveitam os outros recursos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="799f2-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="799f2-155">Essas vulnerabilidades serão exibidas no painel do Identity Protection automaticamente depois que esses recursos forem configurados.</span><span class="sxs-lookup"><span data-stu-id="799f2-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="799f2-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="799f2-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="799f2-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="799f2-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="799f2-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="799f2-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="799f2-159">Risco de comprometimento do usuário</span><span class="sxs-lookup"><span data-stu-id="799f2-159">User compromise risk</span></span>
<span data-ttu-id="799f2-160">**Para testar o Risco de comprometimento do usuário, realize as seguintes etapas**:</span><span class="sxs-lookup"><span data-stu-id="799f2-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="799f2-161">Entre em [https://portal.azure.com](https://portal.azure.com) com as credenciais de administrador global para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="799f2-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="799f2-162">Navegue até **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="799f2-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="799f2-163">Na folha principal de **Azure AD Identity Protection**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="799f2-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="799f2-164">Na folha **Configurações do Portal**, em **Regras de segurança**, clique em **Risco de comprometimento do usuário**.</span><span class="sxs-lookup"><span data-stu-id="799f2-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="799f2-165">Na folha **Risco de Entrada**, desative **Habilitar regra** e clique em **Salvar** configurações.</span><span class="sxs-lookup"><span data-stu-id="799f2-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="799f2-166">Para uma determinada conta de usuário, simule um evento de risco de locais desconhecidos ou IP anônimo.</span><span class="sxs-lookup"><span data-stu-id="799f2-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="799f2-167">Isso elevará o nível de risco do usuário para **Médio**.</span><span class="sxs-lookup"><span data-stu-id="799f2-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="799f2-168">Aguarde alguns minutos e verifique se o nível do usuário é **Médio**.</span><span class="sxs-lookup"><span data-stu-id="799f2-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="799f2-169">Vá para a folha **Configurações do Portal** .</span><span class="sxs-lookup"><span data-stu-id="799f2-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="799f2-170">Na folha **Risco de Comprometimento do Usuário**, em **Habilitar regra**, selecione **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="799f2-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="799f2-171">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="799f2-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="799f2-172">a.</span><span class="sxs-lookup"><span data-stu-id="799f2-172">a.</span></span> <span data-ttu-id="799f2-173">Para bloquear, selecione **Médio** em **Bloquear entrada**.</span><span class="sxs-lookup"><span data-stu-id="799f2-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="799f2-174">b.</span><span class="sxs-lookup"><span data-stu-id="799f2-174">b.</span></span> <span data-ttu-id="799f2-175">Para impor a alteração de senha de segurança, selecione **Médio** em **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="799f2-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="799f2-176">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="799f2-176">Click **Save**.</span></span>
12. <span data-ttu-id="799f2-177">Agora você pode testar o acesso condicional baseado em risco ao entrar usando um usuário com um nível de risco elevado.</span><span class="sxs-lookup"><span data-stu-id="799f2-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="799f2-178">Se o risco do usuário for Médio, dependendo da configuração da política, sua entrada será bloqueada ou você será forçado a alterar a senha.</span><span class="sxs-lookup"><span data-stu-id="799f2-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="799f2-179">
    ![Guia estratégico](./media/active-directory-identityprotection-playbook/201.png "manual")
    </span><span class="sxs-lookup"><span data-stu-id="799f2-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="799f2-180">Risco de entrada</span><span class="sxs-lookup"><span data-stu-id="799f2-180">Sign-in risk</span></span>
<span data-ttu-id="799f2-181">**Para testar um risco de entrada, realize as seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="799f2-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="799f2-182">Entre em [https://portal.azure.com ](https://portal.azure.com) com as credenciais de administrador global para seu locatário.</span><span class="sxs-lookup"><span data-stu-id="799f2-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="799f2-183">Navegue até **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="799f2-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="799f2-184">Na folha principal de **Azure AD Identity Protection**, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="799f2-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="799f2-185">Na folha **Configurações do Portal**, em **Regras de segurança**, clique em **Risco de entrada**.</span><span class="sxs-lookup"><span data-stu-id="799f2-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="799f2-186">Sobre o * * entrar risco * * folha, selecione **em** em **Habilitar regra**.</span><span class="sxs-lookup"><span data-stu-id="799f2-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="799f2-187">Selecione uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="799f2-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="799f2-188">a.</span><span class="sxs-lookup"><span data-stu-id="799f2-188">a.</span></span> <span data-ttu-id="799f2-189">Para bloquear, selecione **Médio** em **Bloquear entrada**</span><span class="sxs-lookup"><span data-stu-id="799f2-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="799f2-190">b.</span><span class="sxs-lookup"><span data-stu-id="799f2-190">b.</span></span> <span data-ttu-id="799f2-191">Para impor a alteração de senha de segurança, selecione **Médio** em **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="799f2-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="799f2-192">Para bloquear, selecione Médio em Bloquear entrada.</span><span class="sxs-lookup"><span data-stu-id="799f2-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="799f2-193">Para impor a autenticação multifator, selecione **Médio** em **Exigir autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="799f2-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="799f2-194">Clique em **Save**.</span><span class="sxs-lookup"><span data-stu-id="799f2-194">Click on **Save**.</span></span>
10. <span data-ttu-id="799f2-195">Agora é possível testar o acesso condicional baseado em risco simulando eventos de risco de locais desconhecidos ou IP anônimo, pois são considerados eventos de risco **Médio** .</span><span class="sxs-lookup"><span data-stu-id="799f2-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="799f2-196">![Guia estratégico](./media/active-directory-identityprotection-playbook/200.png "Guia estratégico")</span><span class="sxs-lookup"><span data-stu-id="799f2-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="799f2-197">Consulte também</span><span class="sxs-lookup"><span data-stu-id="799f2-197">See also</span></span>
* [<span data-ttu-id="799f2-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="799f2-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

