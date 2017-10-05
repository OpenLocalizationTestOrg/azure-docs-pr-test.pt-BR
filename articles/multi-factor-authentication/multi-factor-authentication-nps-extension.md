---
title: Usar servidores NPS existentes para fornecer recursos ao Azure MFA| Microsoft Docs
description: "A extensão do Servidor de Políticas de Rede para a Autenticação Multifator do Azure é uma solução simples para adicionar recursos de verificação em duas etapas baseados em nuvem à sua infraestrutura de autenticação existente."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: fa125292ee85bd9b5329cffeff7f076d3002cbf3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a><span data-ttu-id="2bff9-103">Integrar sua infraestrutura do NPS existente à Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="2bff9-103">Integrate your existing NPS infrastructure with Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="2bff9-104">A extensão do Servidor de Políticas de Rede (NPS) para o Azure MFA adiciona recursos MFA baseados em nuvem à sua infraestrutura de autenticação usando os seus servidores existentes.</span><span class="sxs-lookup"><span data-stu-id="2bff9-104">The Network Policy Server (NPS) extension for Azure MFA adds cloud-based MFA capabilities to your authentication infrastructure using your existing servers.</span></span> <span data-ttu-id="2bff9-105">Com a extensão do NPS, você pode adicionar verificação por chamada telefônica, mensagem de texto ou aplicativo ao fluxo de autenticação existente sem a necessidade de instalar, configurar e manter novos servidores.</span><span class="sxs-lookup"><span data-stu-id="2bff9-105">With the NPS extension, you can add phone call, text message, or phone app verification to your existing authentication flow without having to install, configure, and maintain new servers.</span></span> 

<span data-ttu-id="2bff9-106">Esta extensão foi criada para organizações que desejam proteger conexões VPN sem implantar o Servidor do Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-106">This extension was created for organizations that want to protect VPN connections without deploying the Azure MFA Server.</span></span> <span data-ttu-id="2bff9-107">A extensão NPS atua como um adaptador entre RADIUS e Azure MFA baseado em nuvem para fornecer um segundo fator de autenticação para usuários federados ou sincronizados.</span><span class="sxs-lookup"><span data-stu-id="2bff9-107">The NPS extension acts as an adapter between RADIUS and cloud-based Azure MFA to provide a second factor of authentication for federated or synced users.</span></span>

<span data-ttu-id="2bff9-108">Ao usar a extensão do NPS para o Azure MFA, o fluxo de autenticação inclui os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="2bff9-108">When using the NPS extension for Azure MFA, the authentication flow includes the following components:</span></span> 

1. <span data-ttu-id="2bff9-109">**Servidor VPN/NAS** recebe solicitações de clientes VPN e converte-os em solicitações RADIUS para servidores NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-109">**NAS/VPN Server** receives requests from VPN clients and converts them into RADIUS requests to NPS servers.</span></span> 
2. <span data-ttu-id="2bff9-110">**Servidor NPS** conecta-se ao Active Directory para executar a autenticação primária das solicitações RADIUS e, ao obter êxito, passa a solicitação para quaisquer extensões instaladas.</span><span class="sxs-lookup"><span data-stu-id="2bff9-110">**NPS Server** connects to Active Directory to perform the primary authentication for the RADIUS requests and, upon success, passes the request to any installed extensions.</span></span>  
3. <span data-ttu-id="2bff9-111">**Extensão do NPS** dispara uma solicitação ao Azure MFA para a autenticação secundária.</span><span class="sxs-lookup"><span data-stu-id="2bff9-111">**NPS Extension** triggers a request to Azure MFA for the secondary authentication.</span></span> <span data-ttu-id="2bff9-112">Quando a extensão receber a resposta, e se o desafio de MFA for bem-sucedido, ela concluirá a solicitação de autenticação, fornecendo ao servidor NPS os tokens de segurança que incluem uma declaração MFA, emitida pelo STS do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bff9-112">Once the extension receives the response, and if the MFA challenge succeeds, it completes the authentication request by providing the NPS server with security tokens that include an MFA claim, issued by Azure STS.</span></span>  
4. <span data-ttu-id="2bff9-113">O **Azure MFA** comunica-se com o Azure Active Directory para recuperar os detalhes do usuário e executa a autenticação secundária usando um método de verificação configurado para o usuário.</span><span class="sxs-lookup"><span data-stu-id="2bff9-113">**Azure MFA** communicates with Azure Active Directory to retrieve the user’s details and performs the secondary authentication using a verification method configured to the user.</span></span>

<span data-ttu-id="2bff9-114">O diagrama a seguir ilustra esse fluxo de solicitação de autenticação de alto nível:</span><span class="sxs-lookup"><span data-stu-id="2bff9-114">The following diagram illustrates this high-level authentication request flow:</span></span> 

![Diagrama de fluxo de autenticação](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a><span data-ttu-id="2bff9-116">Planejar sua implantação</span><span class="sxs-lookup"><span data-stu-id="2bff9-116">Plan your deployment</span></span>

<span data-ttu-id="2bff9-117">A extensão NPS controla automaticamente a redundância, de maneira que você não precisa de uma configuração especial.</span><span class="sxs-lookup"><span data-stu-id="2bff9-117">The NPS extension automatically handles redundancy, so you don't need a special configuration.</span></span>

<span data-ttu-id="2bff9-118">Você pode criar quantos servidores NPS habilitados para o Azure MFA conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="2bff9-118">You can create as many Azure MFA-enabled NPS servers as you need.</span></span> <span data-ttu-id="2bff9-119">Se você instalar vários servidores, use um certificado de cliente diferente para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="2bff9-119">If you do install multiple servers, you should use a difference client certificate for each one of them.</span></span> <span data-ttu-id="2bff9-120">Ao criar um certificado para cada servidor, você pode atualizar cada certificado individualmente e não se preocupar com tempo de inatividade em todos eles.</span><span class="sxs-lookup"><span data-stu-id="2bff9-120">Creating a cert for each server means that you can update each cert individually, and not worry about downtime across all your servers.</span></span>

<span data-ttu-id="2bff9-121">Os servidores VPN encaminham as solicitações de autenticação, portanto precisam estar cientes dos novos servidores NPS habilitados para a MFA do Azure.</span><span class="sxs-lookup"><span data-stu-id="2bff9-121">VPN servers route authentication requests, so they need to be aware of the new Azure MFA-enabled NPS servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bff9-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2bff9-122">Prerequisites</span></span>

<span data-ttu-id="2bff9-123">A extensão do NPS deve trabalhar com sua infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="2bff9-123">The NPS extension is meant to work with your existing infrastructure.</span></span> <span data-ttu-id="2bff9-124">Verifique se você cumpre os seguintes pré-requisitos antes de iniciar.</span><span class="sxs-lookup"><span data-stu-id="2bff9-124">Make sure you have the following prerequisites before you begin.</span></span>

### <a name="licenses"></a><span data-ttu-id="2bff9-125">Licenças</span><span class="sxs-lookup"><span data-stu-id="2bff9-125">Licenses</span></span>

<span data-ttu-id="2bff9-126">A extensão do NPS para o Azure MFA está disponível para clientes com [licenças para Autenticação Multifator do Azure](multi-factor-authentication.md) (incluído no Azure AD Premium, EMS ou uma assinatura de MFA).</span><span class="sxs-lookup"><span data-stu-id="2bff9-126">The NPS Extension for Azure MFA is available to customers with [licenses for Azure Multi-Factor Authentication](multi-factor-authentication.md) (included with Azure AD Premium, EMS, or an MFA subscription).</span></span>

### <a name="software"></a><span data-ttu-id="2bff9-127">Software</span><span class="sxs-lookup"><span data-stu-id="2bff9-127">Software</span></span>

<span data-ttu-id="2bff9-128">Windows Server 2008 R2 SP1 ou superior.</span><span class="sxs-lookup"><span data-stu-id="2bff9-128">Windows Server 2008 R2 SP1 or above.</span></span>

### <a name="libraries"></a><span data-ttu-id="2bff9-129">Bibliotecas</span><span class="sxs-lookup"><span data-stu-id="2bff9-129">Libraries</span></span>

<span data-ttu-id="2bff9-130">Essas bibliotecas são instaladas automaticamente com a extensão.</span><span class="sxs-lookup"><span data-stu-id="2bff9-130">These libraries are installed automatically with the extension.</span></span>
-   [<span data-ttu-id="2bff9-131">Pacotes redistribuíveis do Visual C++ para Visual Studio 2013 (X64)</span><span class="sxs-lookup"><span data-stu-id="2bff9-131">Visual C++ Redistributable Packages for Visual Studio 2013 (X64)</span></span>](https://www.microsoft.com/download/details.aspx?id=40784)
-   [<span data-ttu-id="2bff9-132">Módulo Microsoft Azure Active Directory para Windows PowerShell versão 1.1.166.0</span><span class="sxs-lookup"><span data-stu-id="2bff9-132">Microsoft Azure Active Directory Module for Windows PowerShell version 1.1.166.0</span></span>](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a><span data-ttu-id="2bff9-133">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bff9-133">Azure Active Directory</span></span>

<span data-ttu-id="2bff9-134">Todos que usam a extensão do NPS devem estar sincronizados com o Azure Active Directory usando o Azure AD Connect e devem estar registrados para MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-134">Everyone using the NPS extension must be synced to Azure Active Directory using Azure AD Connect, and must be registered for MFA.</span></span>

<span data-ttu-id="2bff9-135">Ao instalar a extensão, você precisa das credenciais de administrador e a ID de diretório para seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bff9-135">When you install the extension, you need the directory ID and admin credentials for your Azure AD tenant.</span></span> <span data-ttu-id="2bff9-136">Você pode encontrar a ID de diretório no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2bff9-136">You can find your directory ID in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2bff9-137">Entre como administrador, selecione o ícone **Azure Active Directory** à esquerda e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="2bff9-137">Sign in as an administrator, select the **Azure Active Directory** icon on the left, then select **Properties**.</span></span> <span data-ttu-id="2bff9-138">Copie o GUID na caixa **ID do diretório** e salve-o.</span><span class="sxs-lookup"><span data-stu-id="2bff9-138">Copy the GUID in the **Directory ID** box and save it.</span></span> <span data-ttu-id="2bff9-139">Você usará esse GUID como a ID de locatário ao instalar a extensão NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-139">You use this GUID as the tenant ID when you install the NPS extension.</span></span>

![Localize sua ID de diretório em Propriedades do Azure Active Directory](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a><span data-ttu-id="2bff9-141">Prepare o seu ambiente</span><span class="sxs-lookup"><span data-stu-id="2bff9-141">Prepare your environment</span></span>

<span data-ttu-id="2bff9-142">Antes de instalar a extensão NPS, convém preparar o ambiente para manipular o tráfego de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-142">Before you install the NPS extension, you want to prepare you environment to handle the authentication traffic.</span></span>

### <a name="enable-the-nps-role-on-a-domain-joined-server"></a><span data-ttu-id="2bff9-143">Habilitar a função NPS em um servidor ingressado no domínio</span><span class="sxs-lookup"><span data-stu-id="2bff9-143">Enable the NPS role on a domain-joined server</span></span>

<span data-ttu-id="2bff9-144">O servidor NPS se conecta ao Azure Active Directory e autentica as solicitações da MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-144">The NPS server connects to Azure Active Directory and authenticates the MFA requests.</span></span> <span data-ttu-id="2bff9-145">Escolha um servidor para essa função.</span><span class="sxs-lookup"><span data-stu-id="2bff9-145">Choose one server for this role.</span></span> <span data-ttu-id="2bff9-146">É recomendável escolher um servidor que não manipule solicitações de outros serviços, porque a extensão NPS gerará erros para solicitações que não sejam RADIUS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-146">We recommend choosing a server that doesn't handle requests from other services, because the NPS extension throws errors for any requests that aren't RADIUS.</span></span>

1. <span data-ttu-id="2bff9-147">No servidor, abra o **Assistente de Adição de Funções e Recursos** no menu de Início rápido do Gerenciador do Servidor.</span><span class="sxs-lookup"><span data-stu-id="2bff9-147">On your server, open the **Add Roles and Features Wizard** from the Server Manager Quickstart menu.</span></span>
2. <span data-ttu-id="2bff9-148">Escolha **Instalação baseada em função ou recurso** para o tipo de instalação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-148">Choose **Role-based or feature-based installation** for your installation type.</span></span>
3. <span data-ttu-id="2bff9-149">Selecione a função de servidor **Serviços de Acesso e Política de Rede**.</span><span class="sxs-lookup"><span data-stu-id="2bff9-149">Select the **Network Policy and Access Services** server role.</span></span> <span data-ttu-id="2bff9-150">Uma janela poderá ser exibida para informá-lo dos recursos necessários para executar essa função.</span><span class="sxs-lookup"><span data-stu-id="2bff9-150">A window may pop up to inform you of required features to run this role.</span></span>
4. <span data-ttu-id="2bff9-151">Siga as etapas do assistente até a página de Confirmação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-151">Continue through the wizard until the Confirmation page.</span></span> <span data-ttu-id="2bff9-152">Selecione **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="2bff9-152">Select **Install**.</span></span>

<span data-ttu-id="2bff9-153">Agora que você tem um servidor designado para o NPS, você também deve configurar esse servidor para manipular as solicitações RADIUS de entrada da solução VPN.</span><span class="sxs-lookup"><span data-stu-id="2bff9-153">Now that you have a server designated for NPS, you should also configure this server to handle incoming RADIUS requests from the VPN solution.</span></span>

### <a name="configure-your-vpn-solution-to-communicate-with-the-nps-server"></a><span data-ttu-id="2bff9-154">Configurar a solução VPN para se comunicar com o servidor NPS</span><span class="sxs-lookup"><span data-stu-id="2bff9-154">Configure your VPN solution to communicate with the NPS server</span></span>

<span data-ttu-id="2bff9-155">Dependendo da solução VPN que você usa, as etapas para configurar a política de autenticação RADIUS variam.</span><span class="sxs-lookup"><span data-stu-id="2bff9-155">Depending on which VPN solution you use, the steps to configure your RADIUS authentication policy vary.</span></span> <span data-ttu-id="2bff9-156">Configure essa política para apontar para o servidor NPS de RADIUS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-156">Configure this policy to point to your RADIUS NPS server.</span></span>

### <a name="sync-domain-users-to-the-cloud"></a><span data-ttu-id="2bff9-157">Sincronizar usuários de domínio com a nuvem</span><span class="sxs-lookup"><span data-stu-id="2bff9-157">Sync domain users to the cloud</span></span>

<span data-ttu-id="2bff9-158">Esta etapa pode já estar concluída no seu locatário, mas é bom verificar se Azure AD Connect sincronizou recentemente os seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="2bff9-158">This step may already be complete on your tenant, but it's good to double-check that Azure AD Connect has synchronized your databases recently.</span></span>

1. <span data-ttu-id="2bff9-159">Entre no [Portal do Azure](https://portal.azure.com) como administrador.</span><span class="sxs-lookup"><span data-stu-id="2bff9-159">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="2bff9-160">Selecione **Azure Active Directory** > **Azure AD Connect**</span><span class="sxs-lookup"><span data-stu-id="2bff9-160">Select **Azure Active Directory** > **Azure AD Connect**</span></span>
3. <span data-ttu-id="2bff9-161">Verifique se o status de sincronização está **Habilitado** e se a última sincronização foi há menos de uma hora.</span><span class="sxs-lookup"><span data-stu-id="2bff9-161">Verify that your sync status is **Enabled** and that your last sync was less than an hour ago.</span></span>

<span data-ttu-id="2bff9-162">Se você precisar disparar uma nova rodada de sincronização, use as instruções em [Sincronização do Azure AD Connect: agendador](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span><span class="sxs-lookup"><span data-stu-id="2bff9-162">If you need to kick off a new round of synchronization, us the instructions in [Azure AD Connect sync: Scheduler](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).</span></span>

### <a name="determine-which-authentication-methods-your-users-can-use"></a><span data-ttu-id="2bff9-163">Determinar quais métodos de autenticação os usuários podem usar</span><span class="sxs-lookup"><span data-stu-id="2bff9-163">Determine which authentication methods your users can use</span></span>

<span data-ttu-id="2bff9-164">Há dois fatores que afetam quais métodos de autenticação estão disponíveis com uma implantação de extensão do NPS:</span><span class="sxs-lookup"><span data-stu-id="2bff9-164">There are two factors that affect which authentication methods are available with an NPS extension deployment:</span></span>

1. <span data-ttu-id="2bff9-165">O algoritmo de criptografia de senha usado entre o cliente RADIUS (VPN, servidor Netscaler ou outros) e os servidores NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-165">The password encryption algorithm used between the RADIUS client (VPN, Netscaler server, or other) and the NPS servers.</span></span>
   - <span data-ttu-id="2bff9-166">O **PAP** dá suporte a todos os métodos de autenticação do Azure MFA na nuvem: chamada telefônica, mensagem de texto unidirecional, notificação de aplicativo móvel e código de verificação de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="2bff9-166">**PAP** supports all the authentication methods of Azure MFA in the cloud: phone call, one-way text message, mobile app notification, and mobile app verification code.</span></span>
   - <span data-ttu-id="2bff9-167">**CHAPV2** e **EAP** dão suporte a chamada telefônica e notificação de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="2bff9-167">**CHAPV2** and **EAP** support phone call and mobile app notification.</span></span>
2. <span data-ttu-id="2bff9-168">Os métodos de entrada que o aplicativo cliente (VPN, servidor Netscaler ou outros) pode manipular.</span><span class="sxs-lookup"><span data-stu-id="2bff9-168">The input methods that the client application (VPN, Netscaler server, or other) can handle.</span></span> <span data-ttu-id="2bff9-169">Por exemplo, o cliente VPN tem algum meio de permitir que o usuário digite um código de verificação de um texto ou aplicativo móvel?</span><span class="sxs-lookup"><span data-stu-id="2bff9-169">For example, does the VPN client have some means to allow the user to type in a verification code from a text or mobile app?</span></span>

<span data-ttu-id="2bff9-170">Quando você implanta a extensão do NPS, use esses fatores para avaliar quais métodos estão disponíveis para os usuários.</span><span class="sxs-lookup"><span data-stu-id="2bff9-170">When you deploy the NPS extension, use these factors to evaluate which methods are available for your users.</span></span> <span data-ttu-id="2bff9-171">Se o cliente RADIUS dá suporte a PAP, mas a experiência do cliente não tem campos de entrada para um código de verificação, chamada telefônica e notificação do aplicativo móvel são as duas opções com suporte.</span><span class="sxs-lookup"><span data-stu-id="2bff9-171">If your RADIUS client supports PAP, but the client UX doesn't have input fields for a verification code, then phone call and mobile app notification are the two supported options.</span></span>

<span data-ttu-id="2bff9-172">Você pode [desabilitar métodos de autenticação sem suporte](multi-factor-authentication-whats-next.md#selectable-verification-methods) no Azure.</span><span class="sxs-lookup"><span data-stu-id="2bff9-172">You can [disable unsupported authentication methods](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.</span></span>

### <a name="enable-users-for-mfa"></a><span data-ttu-id="2bff9-173">Habilitar usuários para a MFA</span><span class="sxs-lookup"><span data-stu-id="2bff9-173">Enable users for MFA</span></span>

<span data-ttu-id="2bff9-174">Antes de implantar a extensão NPS completa, você precisa habilitar a MFA para os usuários que você deseja que executem a verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="2bff9-174">Before you deploy the full NPS extension, you need to enable MFA for the users that you want to perform two-step verification.</span></span> <span data-ttu-id="2bff9-175">Mas antes disso, a fim de testar a extensão ao implantá-la, você precisa de pelo menos uma conta de teste que seja totalmente registrada para a Autenticação Multifator.</span><span class="sxs-lookup"><span data-stu-id="2bff9-175">More immediately, to test the extension as you deploy it, you need at least one test account that is fully registered for Multi-Factor Authentication.</span></span>

<span data-ttu-id="2bff9-176">Use estas etapas para iniciar uma conta de teste:</span><span class="sxs-lookup"><span data-stu-id="2bff9-176">Use these steps to get a test account started:</span></span>
1. <span data-ttu-id="2bff9-177">Entre em [https://aka.ms/mfasetup](https://aka.ms/mfasetup) com uma conta de teste.</span><span class="sxs-lookup"><span data-stu-id="2bff9-177">Sign in to [https://aka.ms/mfasetup](https://aka.ms/mfasetup) with a test account.</span></span> 
2. <span data-ttu-id="2bff9-178">Siga os prompts para configurar um método de verificação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-178">Follow the prompts to set up a verification method.</span></span>
3. <span data-ttu-id="2bff9-179">Crie uma política de acesso condicional ou [altere o estado do usuário](multi-factor-authentication-get-started-user-states.md) para exigir verificação em duas etapas para a conta de teste.</span><span class="sxs-lookup"><span data-stu-id="2bff9-179">Either create a conditional access policy or [change the user state](multi-factor-authentication-get-started-user-states.md) to require two-step verification for the test account.</span></span> 

<span data-ttu-id="2bff9-180">Os usuários também precisam seguir estas etapas para se autenticar com a extensão NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-180">Your users also need to follow these steps to enroll before they can authenticate with the NPS extension.</span></span>

## <a name="install-the-nps-extension"></a><span data-ttu-id="2bff9-181">Instalar a extensão NPS</span><span class="sxs-lookup"><span data-stu-id="2bff9-181">Install the NPS extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2bff9-182">Instale a extensão do NPS em um servidor diferente do ponto de acesso VPN.</span><span class="sxs-lookup"><span data-stu-id="2bff9-182">Install the NPS extension on a different server than the VPN access point.</span></span>

### <a name="download-and-install-the-nps-extension-for-azure-mfa"></a><span data-ttu-id="2bff9-183">Baixar e instalar a extensão NPS para a MFA do Azure</span><span class="sxs-lookup"><span data-stu-id="2bff9-183">Download and install the NPS extension for Azure MFA</span></span>

1.  <span data-ttu-id="2bff9-184">[Baixe a extensão NPS](https://aka.ms/npsmfa) do Centro de Download da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2bff9-184">[Download the NPS Extension](https://aka.ms/npsmfa) from the Microsoft Download Center.</span></span>
2.  <span data-ttu-id="2bff9-185">Copie o binário para o Servidor de Políticas de Rede que você deseja configurar.</span><span class="sxs-lookup"><span data-stu-id="2bff9-185">Copy the binary to the Network Policy Server you want to configure.</span></span>
3.  <span data-ttu-id="2bff9-186">Execute o arquivo *setup.exe* e siga as instruções de instalação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-186">Run *setup.exe* and follow the installation instructions.</span></span> <span data-ttu-id="2bff9-187">Se você encontrar erros, verifique se as duas bibliotecas, da seção de pré-requisitos, foram instaladas com êxito.</span><span class="sxs-lookup"><span data-stu-id="2bff9-187">If you encounter errors, double-check that the two libraries from the prerequisite section were successfully installed.</span></span>

### <a name="run-the-powershell-script"></a><span data-ttu-id="2bff9-188">Executar o script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bff9-188">Run the PowerShell script</span></span>

<span data-ttu-id="2bff9-189">O instalador cria um script do PowerShell neste local: `C:\Program Files\Microsoft\AzureMfa\Config` (em que C:\ é a sua unidade de instalação).</span><span class="sxs-lookup"><span data-stu-id="2bff9-189">The installer creates a PowerShell script in this location: `C:\Program Files\Microsoft\AzureMfa\Config` (where C:\ is your installation drive).</span></span> <span data-ttu-id="2bff9-190">O script do PowerShell executa as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="2bff9-190">This PowerShell script performs the following actions:</span></span>

-   <span data-ttu-id="2bff9-191">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="2bff9-191">Create a self-signed certificate.</span></span>
-   <span data-ttu-id="2bff9-192">Associa a chave pública do certificado à entidade de serviço no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bff9-192">Associate the public key of the certificate to the service principal on Azure AD.</span></span>
-   <span data-ttu-id="2bff9-193">Armazena o certificado no repositório de certificados do computador local.</span><span class="sxs-lookup"><span data-stu-id="2bff9-193">Store the cert in the local machine cert store.</span></span>
-   <span data-ttu-id="2bff9-194">Concede acesso à chave privada do certificado ao usuário de rede.</span><span class="sxs-lookup"><span data-stu-id="2bff9-194">Grant access to the certificate’s private key to Network User.</span></span>
-   <span data-ttu-id="2bff9-195">Reinicia o NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-195">Restart the NPS.</span></span>

<span data-ttu-id="2bff9-196">A menos que você deseje usar seus próprios certificados (em vez dos certificados autoassinados gerados pelo script do PowerShell), execute o Script do PowerShell para concluir a instalação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-196">Unless you want to use your own certificates (instead of the self-signed certificates that the PowerShell script generates), run the PowerShell Script to complete the installation.</span></span> <span data-ttu-id="2bff9-197">Se você instalar a extensão em vários servidores, cada um deverá ter seu próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="2bff9-197">If you install the extension on multiple servers, each one should have its own certificate.</span></span>

1. <span data-ttu-id="2bff9-198">Execute o Windows PowerShell como um administrador.</span><span class="sxs-lookup"><span data-stu-id="2bff9-198">Run Windows PowerShell as an administrator.</span></span>
2. <span data-ttu-id="2bff9-199">Altere os diretórios.</span><span class="sxs-lookup"><span data-stu-id="2bff9-199">Change directories.</span></span>

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. <span data-ttu-id="2bff9-200">Execute o script do PowerShell criado pelo instalador.</span><span class="sxs-lookup"><span data-stu-id="2bff9-200">Run the PowerShell script created by the installer.</span></span>

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. <span data-ttu-id="2bff9-201">O PowerShell solicitará a sua ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="2bff9-201">PowerShell prompts for your tenant ID.</span></span> <span data-ttu-id="2bff9-202">Use o GUID da ID de diretório que você copiou do Portal do Azure na seção de pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="2bff9-202">Use the Directory ID GUID that you copied from the Azure portal in the prerequisites section.</span></span>
5. <span data-ttu-id="2bff9-203">Entre no Azure AD como administrador.</span><span class="sxs-lookup"><span data-stu-id="2bff9-203">Sign in to Azure AD as an administrator.</span></span>
6. <span data-ttu-id="2bff9-204">O PowerShell mostra uma mensagem de êxito quando o script é concluído.</span><span class="sxs-lookup"><span data-stu-id="2bff9-204">PowerShell shows a success message when the script is finished.</span></span>  

<span data-ttu-id="2bff9-205">Repita essas etapas em quaisquer servidores NPS adicionais em que você deseja configurar o balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="2bff9-205">Repeat these steps on any additional NPS servers that you want to set up for load balancing.</span></span>

>[!NOTE]
><span data-ttu-id="2bff9-206">Se você usar seus próprios certificados em vez de gerar certificados com o script do PowerShell, certifique-se de que eles estejam alinhados com a convenção de nomenclatura do NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-206">If you use your own certificates instead of generating certificates with the PowerShell script, make sure that they align to the NPS naming convention.</span></span> <span data-ttu-id="2bff9-207">O nome da entidade deve ser **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span><span class="sxs-lookup"><span data-stu-id="2bff9-207">The subject name must be **CN=\<TenantID\>,OU=Microsoft NPS Extension**.</span></span> 

## <a name="configure-your-nps-extension"></a><span data-ttu-id="2bff9-208">Configurar sua extensão do NPS</span><span class="sxs-lookup"><span data-stu-id="2bff9-208">Configure your NPS extension</span></span>

<span data-ttu-id="2bff9-209">Esta seção inclui considerações sobre o design e sugestões para implantações bem-sucedidas da extensão do NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-209">This section includes design considerations and suggestions for successful NPS extension deployments.</span></span>

### <a name="configuration-limitations"></a><span data-ttu-id="2bff9-210">Limitações de configuração</span><span class="sxs-lookup"><span data-stu-id="2bff9-210">Configuration limitations</span></span>

- <span data-ttu-id="2bff9-211">A extensão NPS para a MFA do Azure não inclui ferramentas para migrar usuários e configurações do Servidor MFA para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="2bff9-211">The NPS extension for Azure MFA does not include tools to migrate users and settings from MFA Server to the cloud.</span></span> <span data-ttu-id="2bff9-212">Por esse motivo, é aconselhável usar a extensão para novas implantações, em vez da implantação existente.</span><span class="sxs-lookup"><span data-stu-id="2bff9-212">For this reason, we suggest using the extension for new deployments, rather than existing deployment.</span></span> <span data-ttu-id="2bff9-213">Se você usar a extensão em uma implantação existente, os usuários terão que executar a verificação novamente para preencher os detalhes de MFA na nuvem.</span><span class="sxs-lookup"><span data-stu-id="2bff9-213">If you use the extension on an existing deployment, your users have to perform proof-up again to populate their MFA details in the cloud.</span></span>  
- <span data-ttu-id="2bff9-214">A extensão do NPS usa o UPN do Active Directory local para identificar o usuário no Azure MFA para realizar a autenticação secundária. A extensão pode ser configurada para usar um identificador diferente, como a ID de logon alternativa ou um campo personalizado do Active Directory que não seja o UPN.</span><span class="sxs-lookup"><span data-stu-id="2bff9-214">The NPS extension uses the UPN from the on-premises Active directory to identify the user on Azure MFA for performing the Secondary Auth. The extension can be configured to use a different identifier like alternate login ID or custom Active Directory field other than UPN.</span></span> <span data-ttu-id="2bff9-215">Consulte [Opções de configuração avançadas da extensão NPS para a Autenticação Multifator](multi-factor-authentication-advanced-vpn-configurations.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="2bff9-215">See [Advanced configuration options for the NPS extension for Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for more information.</span></span>
- <span data-ttu-id="2bff9-216">Nem todos os protocolos de criptografia dão suporte a todos os métodos de verificação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-216">Not all encryption protocols support all verification methods.</span></span>
   - <span data-ttu-id="2bff9-217">O **PAP** dá suporte a chamadas telefônicas, mensagens de texto unidirecionais, notificações de aplicativo móvel e códigos de verificação de aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="2bff9-217">**PAP** supports phone call, one-way text message, mobile app notification, and mobile app verification code</span></span>
   - <span data-ttu-id="2bff9-218">**CHAPV2** e **EAP** dão suporte a chamada telefônica e notificação do aplicativo móvel</span><span class="sxs-lookup"><span data-stu-id="2bff9-218">**CHAPV2** and **EAP** support phone call and mobile app notification</span></span>

### <a name="control-radius-clients-that-require-mfa"></a><span data-ttu-id="2bff9-219">Clientes RADIUS de controle que exigem MFA</span><span class="sxs-lookup"><span data-stu-id="2bff9-219">Control RADIUS clients that require MFA</span></span>

<span data-ttu-id="2bff9-220">Depois que você habilita a MFA para um cliente RADIUS usando a extensão do NPS, todas as autenticações desse cliente são necessárias para executar a MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-220">Once you enable MFA for a RADIUS client using the NPS Extension, all authentications for this client are required to perform MFA.</span></span> <span data-ttu-id="2bff9-221">Se você deseja habilitar a MFA para alguns clientes RADIUS, mas outros não, você pode configurar dois servidores NPS e instalar a extensão em apenas um deles.</span><span class="sxs-lookup"><span data-stu-id="2bff9-221">If you want to enable MFA for some RADIUS clients but not others, you can configure two NPS servers and install the extension on only one of them.</span></span> <span data-ttu-id="2bff9-222">Configure clientes RADIUS para os quais você deseja que a MFA envie solicitações ao servidor NPS configurado com a extensão e outros clientes RADIUS para o servidor NPS não configurado com a extensão.</span><span class="sxs-lookup"><span data-stu-id="2bff9-222">Configure RADIUS clients that you want to require MFA to send requests to the NPS server configured with the extension, and other RADIUS clients to the NPS server not configured with the extension.</span></span>

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a><span data-ttu-id="2bff9-223">Preparar usuários que não são registrados na MFA</span><span class="sxs-lookup"><span data-stu-id="2bff9-223">Prepare for users that aren't enrolled for MFA</span></span>

<span data-ttu-id="2bff9-224">Se você tiver usuários que não são registrados na MFA, determine o que acontece quando eles tentam fazer a autenticação.</span><span class="sxs-lookup"><span data-stu-id="2bff9-224">If you have users that aren't enrolled for MFA, you can determine what happens when they try to authenticate.</span></span> <span data-ttu-id="2bff9-225">Use a configuração de Registro *REQUIRE_USER_MATCH* no caminho do Registro *HKLM\Software\Microsoft\AzureMFA* para controlar o comportamento do recurso.</span><span class="sxs-lookup"><span data-stu-id="2bff9-225">Use the registry setting *REQUIRE_USER_MATCH* in the registry path *HKLM\Software\Microsoft\AzureMFA* to control the feature behavior.</span></span> <span data-ttu-id="2bff9-226">Essa configuração tem uma opção de configuração única:</span><span class="sxs-lookup"><span data-stu-id="2bff9-226">This setting has a single configuration option:</span></span>

| <span data-ttu-id="2bff9-227">Chave</span><span class="sxs-lookup"><span data-stu-id="2bff9-227">Key</span></span> | <span data-ttu-id="2bff9-228">Valor</span><span class="sxs-lookup"><span data-stu-id="2bff9-228">Value</span></span> | <span data-ttu-id="2bff9-229">Padrão</span><span class="sxs-lookup"><span data-stu-id="2bff9-229">Default</span></span> |
| --- | ----- | ------- |
| <span data-ttu-id="2bff9-230">REQUIRE_USER_MATCH</span><span class="sxs-lookup"><span data-stu-id="2bff9-230">REQUIRE_USER_MATCH</span></span> | <span data-ttu-id="2bff9-231">TRUE/FALSE</span><span class="sxs-lookup"><span data-stu-id="2bff9-231">TRUE/FALSE</span></span> | <span data-ttu-id="2bff9-232">Não definido (equivalente a TRUE)</span><span class="sxs-lookup"><span data-stu-id="2bff9-232">Not set (equivalent to TRUE)</span></span> |

<span data-ttu-id="2bff9-233">A finalidade dessa configuração é determinar o que fazer quando um usuário não estiver inscrito na MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-233">The purpose of this setting is to determine what to do when a user is not enrolled for MFA.</span></span> <span data-ttu-id="2bff9-234">Quando a chave não existir, não estiver definida ou estiver definida como TRUE e o usuário não estiver registrado, a extensão falha no desafio da MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-234">When the key does not exist, is not set, or is set to TRUE, and the user is not enrolled, then the extension fails the MFA challenge.</span></span> <span data-ttu-id="2bff9-235">Quando a chave estiver definida como FALSE e o usuário não estiver registrado, a autenticação continuará sem executar a MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-235">When the key is set to FALSE and the user is not enrolled, authentication proceeds without performing MFA.</span></span>

<span data-ttu-id="2bff9-236">Você pode optar por criar essa chave e defini-la como FALSE, e os usuários estão carregando e ainda não podem se inscrever no Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="2bff9-236">You can choose to create this key and set it to FALSE while your users are onboarding, and may not all be enrolled for Azure MFA yet.</span></span> <span data-ttu-id="2bff9-237">Porém, como definir a chave permite que os usuários que não são registrados na MFA se conectem, você deve remover essa chave antes de ir para a produção.</span><span class="sxs-lookup"><span data-stu-id="2bff9-237">However, since setting the key permits users that aren't enrolled for MFA to sign in, you should remove this key before going to production.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2bff9-238">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2bff9-238">Troubleshooting</span></span>

### <a name="how-do-i-verify-that-the-client-cert-is-installed-as-expected"></a><span data-ttu-id="2bff9-239">Como verificar se o certificado do cliente está instalado conforme o esperado?</span><span class="sxs-lookup"><span data-stu-id="2bff9-239">How do I verify that the client cert is installed as expected?</span></span>

<span data-ttu-id="2bff9-240">Procure o certificado autoassinado criado pelo instalador no repositório de certificados e verifique se a chave privada tem permissões concedidas ao usuário **NETWORK SERVICE**.</span><span class="sxs-lookup"><span data-stu-id="2bff9-240">Look for the self-signed certificate created by the installer in the cert store, and check that the private key has permissions granted to user **NETWORK SERVICE**.</span></span> <span data-ttu-id="2bff9-241">O certificado tem um nome de entidade igual a **CN \<tenantid\>, OU = extensão NPS da Microsoft**</span><span class="sxs-lookup"><span data-stu-id="2bff9-241">The cert has a subject name of **CN \<tenantid\>, OU = Microsoft NPS Extension**</span></span>

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-to-my-tenant-in-azure-active-directory"></a><span data-ttu-id="2bff9-242">Como verificar se o certificado do cliente está associado ao meu locatário no Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2bff9-242">How can I verify that my client cert is associated to my tenant in Azure Active Directory?</span></span>

<span data-ttu-id="2bff9-243">Abra um prompt de comando no PowerShell e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="2bff9-243">Open PowerShell command prompt and run the following commands:</span></span>

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

<span data-ttu-id="2bff9-244">Esses comandos imprimem todos os certificados associados ao seu locatário com a instância da extensão do NPS em sua sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bff9-244">These commands print all the certificates associating your tenant with your instance of the NPS extension in your PowerShell session.</span></span> <span data-ttu-id="2bff9-245">Procure seu certificado exportando o certificado do cliente como um arquivo "codificado em Base 64 X.509(.cer)" sem a chave particular e compare-a com a lista do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bff9-245">Look for your certificate by exporting your client cert as a "Base-64 encoded X.509(.cer)" file without the private key, and compare it with the list from PowerShell.</span></span>

<span data-ttu-id="2bff9-246">Os carimbos de data/hora Válido-de e Válido-até, que estão em formato legível, poderão ser usados para filtrar desvios óbvios se o comando retornar mais de um certificado.</span><span class="sxs-lookup"><span data-stu-id="2bff9-246">Valid-From and Valid-Until timestamps, which are in human-readable form, can be used to filter out obvious misfits if the command returns more than one cert.</span></span>

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a><span data-ttu-id="2bff9-247">Por que minhas solicitações estão falhando, com erro de token ADAL?</span><span class="sxs-lookup"><span data-stu-id="2bff9-247">Why are my requests failing with ADAL token error?</span></span>

<span data-ttu-id="2bff9-248">Esse erro pode ser causado por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="2bff9-248">This error could be due to one of several reasons.</span></span> <span data-ttu-id="2bff9-249">Use estas etapas para solucionar o problema:</span><span class="sxs-lookup"><span data-stu-id="2bff9-249">Use these steps to help troubleshoot:</span></span>

1. <span data-ttu-id="2bff9-250">Reinicie o servidor NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-250">Restart your NPS server.</span></span>
2. <span data-ttu-id="2bff9-251">Verifique se o certificado do cliente está instalado conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="2bff9-251">Verify that that client cert is installed as expected.</span></span>
3. <span data-ttu-id="2bff9-252">Verifique se o certificado está associado ao seu locatário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bff9-252">Verify that the certificate is associated with your tenant on Azure AD.</span></span>
4. <span data-ttu-id="2bff9-253">Verifique se que https://login.microsoftonline.com/ está acessível do servidor que executa a extensão.</span><span class="sxs-lookup"><span data-stu-id="2bff9-253">Verify that https://login.microsoftonline.com/ is accessible from the server running the extension.</span></span>

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-the-user-is-not-found"></a><span data-ttu-id="2bff9-254">Por que a autenticação falha, com um erro nos logs de HTTP, informando que o usuário não foi encontrado?</span><span class="sxs-lookup"><span data-stu-id="2bff9-254">Why does authentication fail with an error in HTTP logs stating that the user is not found?</span></span>

<span data-ttu-id="2bff9-255">Verifique se o AD Connect está em execução e se o usuário está presente no Windows Active Directory e no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2bff9-255">Verify that AD Connect is running, and that the user is present in both Windows Active Directory and Azure Active Directory.</span></span>

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a><span data-ttu-id="2bff9-256">Por que vejo erros de conexão HTTP nos logs, com todas as minhas autenticações falhando?</span><span class="sxs-lookup"><span data-stu-id="2bff9-256">Why do I see HTTP connect errors in logs with all my authentications failing?</span></span>

<span data-ttu-id="2bff9-257">Verifique se o link https://adnotifications.windowsazure.com pode ser acessado por meio do servidor que executa a extensão do NPS.</span><span class="sxs-lookup"><span data-stu-id="2bff9-257">Verify that https://adnotifications.windowsazure.com is reachable from the server running the NPS extension.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2bff9-258">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2bff9-258">Next steps</span></span>

- <span data-ttu-id="2bff9-259">Configurar IDs alternativos para logon ou configurar uma lista de exceções para IPs que não devem executar a verificação em duas etapas nas [Opções de configuração avançadas para a extensão do NPS para autenticação multifator](nps-extension-advanced-configuration.md)</span><span class="sxs-lookup"><span data-stu-id="2bff9-259">Configure alternate IDs for login, or set up an exception list for IPs that shouldn't perform two-step verification in [Advanced configuration options for the NPS extension for Multi-Factor Authentication](nps-extension-advanced-configuration.md)</span></span>

- [<span data-ttu-id="2bff9-260">Resolver mensagens de erro da extensão NPS da Autenticação Multifator do Azure</span><span class="sxs-lookup"><span data-stu-id="2bff9-260">Resolve error messages from the NPS extension for Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-nps-errors.md)
