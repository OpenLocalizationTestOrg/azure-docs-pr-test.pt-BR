---
title: "Azure AD Connect: autenticação de passagem – bloqueio inteligente | Microsoft Docs"
description: "Este artigo descreve como a autenticação de passagem do Azure AD (Azure Active Directory) protege suas contas locais contra ataques de senha de força bruta na nuvem."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="7b934-104">Autenticação de passagem do Azure Active Directory: bloqueio inteligente</span><span class="sxs-lookup"><span data-stu-id="7b934-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="7b934-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7b934-105">Overview</span></span>

<span data-ttu-id="7b934-106">O Azure AD protege contra ataques de senha de força bruta e impede que usuários reais sejam impedidos de acessar seus aplicativos de SaaS e do Office 365.</span><span class="sxs-lookup"><span data-stu-id="7b934-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="7b934-107">Essa capacidade, chamada **Bloqueio Inteligente**, tem suporte quando você usa a Autenticação de Passagem como seu método de entrada.</span><span class="sxs-lookup"><span data-stu-id="7b934-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="7b934-108">O Bloqueio Inteligente fica habilitado por padrão para todos os locatários e protege suas contas de usuário o tempo todo; não é necessário ativá-lo.</span><span class="sxs-lookup"><span data-stu-id="7b934-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="7b934-109">O Bloqueio Inteligente funciona controlando tentativas de logon com falha e, depois de um determinado **Limite de bloqueio**, iniciando uma **Duração de bloqueio**.</span><span class="sxs-lookup"><span data-stu-id="7b934-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="7b934-110">Qualquer tentativa de logon do invasor durante a Duração de bloqueio é rejeitada.</span><span class="sxs-lookup"><span data-stu-id="7b934-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="7b934-111">Se o ataque persistir, tentativas posteriores de logon com falha, após o final da Duração de bloqueio, levarão a Durações de bloqueio mais longas.</span><span class="sxs-lookup"><span data-stu-id="7b934-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="7b934-112">O Limite de bloqueio padrão é de 10 tentativas com falha e a Duração de bloqueio padrão é de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="7b934-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="7b934-113">O Bloqueio Inteligente também faz a distinção entre entradas de usuários reais e de invasores e bloqueia somente os invasores na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="7b934-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="7b934-114">Essa funcionalidade impede que invasores bloqueiem usuários reais de forma mal-intencionada.</span><span class="sxs-lookup"><span data-stu-id="7b934-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="7b934-115">Usamos o comportamento de entrada anterior, os dispositivos e navegadores dos usuários, entre outros sinais, para distinguir entre invasores e usuários originais.</span><span class="sxs-lookup"><span data-stu-id="7b934-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="7b934-116">Estamos aperfeiçoando constantemente nossos algoritmos.</span><span class="sxs-lookup"><span data-stu-id="7b934-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="7b934-117">Como a Autenticação de Passagem encaminha solicitações de validação de senha para o AD (Active Directory) local, você precisa impedir que invasores bloqueiem contas de usuários do AD.</span><span class="sxs-lookup"><span data-stu-id="7b934-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="7b934-118">Como tem suas próprias políticas de Bloqueio de conta do AD (especificamente, as políticas de [**Limite de bloqueio de conta**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) e [**Redefinir contador de bloqueios de conta após**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), você precisa configurar os valores de Limite de bloqueio e de Duração de bloqueio do Azure AD adequadamente para filtrar os ataques na nuvem antes que eles alcancem seu AD local.</span><span class="sxs-lookup"><span data-stu-id="7b934-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="7b934-119">O recurso de Bloqueio inteligente é gratuito e está _ativado_ por padrão para todos os clientes.</span><span class="sxs-lookup"><span data-stu-id="7b934-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="7b934-120">Entretanto, modificar os valores de Limite de Bloqueio e de Duração de Bloqueio do Azure AD usando a API do Graph precisa que seu locatário tenha pelo menos uma licença Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="7b934-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="7b934-121">Você não precisa de uma licença do Azure AD Premium P2 _por usuário_ para obter o recurso de bloqueio inteligente com Autenticação de Passagem.</span><span class="sxs-lookup"><span data-stu-id="7b934-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="7b934-122">Para garantir que as contas do AD locais dos seus usuários também sejam protegidas, você precisa garantir que:</span><span class="sxs-lookup"><span data-stu-id="7b934-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="7b934-123">O Limite de bloqueio do Azure AD seja _menor_ que o Limite de bloqueio da Conta do AD.</span><span class="sxs-lookup"><span data-stu-id="7b934-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="7b934-124">É recomendável que você defina os valores de forma que o Limite de bloqueio da Conta do AD seja pelo menos duas ou três vezes o Limite de bloqueio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b934-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="7b934-125">A Duração de bloqueio do Azure AD (representada em segundos) seja _maior_ que o valor de Redefinir contador de bloqueios de conta após do AD (representado em minutos).</span><span class="sxs-lookup"><span data-stu-id="7b934-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="7b934-126">Verifique as políticas de bloqueio de conta do AD</span><span class="sxs-lookup"><span data-stu-id="7b934-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="7b934-127">Use as instruções a seguir para verificar suas políticas de bloqueio de conta do AD:</span><span class="sxs-lookup"><span data-stu-id="7b934-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="7b934-128">Abra a ferramenta de Gerenciamento de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="7b934-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="7b934-129">Edite a política de grupo aplicada a todos os usuários, por exemplo, a Política de Domínio Padrão.</span><span class="sxs-lookup"><span data-stu-id="7b934-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="7b934-130">Navegue até Configuração do Computador\Políticas\Configurações do Windows\Configurações de Conta\Políticas de Conta\Política de Bloqueio da Conta.</span><span class="sxs-lookup"><span data-stu-id="7b934-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="7b934-131">Verifique os valores de Limite de bloqueio de conta e Redefinir contador de bloqueios de conta após.</span><span class="sxs-lookup"><span data-stu-id="7b934-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![Políticas de bloqueio de conta do AD](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="7b934-133">Use a API do Graph para gerenciar os valores do Bloqueio Inteligente de seu locatário</span><span class="sxs-lookup"><span data-stu-id="7b934-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="7b934-134">Modificar os valores de Limite de bloqueio e de Duração de bloqueio do Azure AD usando a API do Graph é um recurso do Azure AD Premium P2.</span><span class="sxs-lookup"><span data-stu-id="7b934-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="7b934-135">Também é necessário que você seja um Administrador Global em seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="7b934-136">Você pode usar o [Explorador do Graph](https://developer.microsoft.com/graph/graph-explorer) para ler, definir e atualizar os valores do Bloqueio Inteligente do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b934-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="7b934-137">Mas você também pode fazer essas operações de forma programática.</span><span class="sxs-lookup"><span data-stu-id="7b934-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="7b934-138">Ler valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="7b934-138">Read Smart Lockout values</span></span>

<span data-ttu-id="7b934-139">Siga estas etapas para ler os valores do Bloqueio Inteligente de seu locatário:</span><span class="sxs-lookup"><span data-stu-id="7b934-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="7b934-140">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="7b934-141">Se solicitado, conceda acesso para as permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="7b934-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="7b934-142">Clique em "Modificar permissões" e selecione a permissão "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="7b934-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="7b934-143">Configure a solicitação da API do Graph da seguinte maneira: defina a versão como "BETA", o tipo de solicitação como "GET" e a URL como `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="7b934-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="7b934-144">Clique em "Executar Consulta" para ver os valores do Bloqueio Inteligente de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="7b934-145">Se não tiver configurado os valores de seu locatário antes, você verá um conjunto vazio.</span><span class="sxs-lookup"><span data-stu-id="7b934-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="7b934-146">Definir valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="7b934-146">Set Smart Lockout values</span></span>

<span data-ttu-id="7b934-147">Siga estas etapas para definir os valores de do Bloqueio Inteligente de seu locatário (somente pela primeira vez):</span><span class="sxs-lookup"><span data-stu-id="7b934-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="7b934-148">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="7b934-149">Se solicitado, conceda acesso para as permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="7b934-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="7b934-150">Clique em "Modificar permissões" e selecione a permissão "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="7b934-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="7b934-151">Configure a solicitação da API do Graph da seguinte maneira: defina a versão como "BETA", o tipo de solicitação como "POST" e a URL como `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="7b934-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="7b934-152">Copie e cole a seguinte solicitação JSON no campo "Corpo da Solicitação".</span><span class="sxs-lookup"><span data-stu-id="7b934-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="7b934-153">Altere os valores do Bloqueio Inteligente conforme apropriado e use um GUID aleatório para `templateId`.</span><span class="sxs-lookup"><span data-stu-id="7b934-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="7b934-154">Clique em "Executar Consulta" para ver os valores do Bloqueio Inteligente de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="7b934-155">Se não estiver usando os valores de **BannedPasswordList** e **EnableBannedPasswordCheck**, você poderá deixá-los como vazio ("") e "false", respectivamente.</span><span class="sxs-lookup"><span data-stu-id="7b934-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="7b934-156">Verifique se você definiu os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="7b934-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="7b934-157">Atualizar valores de Bloqueio Inteligente</span><span class="sxs-lookup"><span data-stu-id="7b934-157">Update Smart Lockout values</span></span>

<span data-ttu-id="7b934-158">Siga estas etapas para atualizar os valores do Bloqueio Inteligente de seu locatário (se já tiver configurado esses valores antes):</span><span class="sxs-lookup"><span data-stu-id="7b934-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="7b934-159">Entre no Explorador do Graph como um Administrador Global de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="7b934-160">Se solicitado, conceda acesso para as permissões solicitadas.</span><span class="sxs-lookup"><span data-stu-id="7b934-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="7b934-161">Clique em "Modificar permissões" e selecione a permissão "Directory.ReadWrite.All".</span><span class="sxs-lookup"><span data-stu-id="7b934-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="7b934-162">[Siga estas etapas para ler os valores do Bloqueio Inteligente de seu locatário](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="7b934-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="7b934-163">Copie o valor de `id` (um GUID) do item com "displayName" como "PasswordRuleSettings".</span><span class="sxs-lookup"><span data-stu-id="7b934-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="7b934-164">Configure a solicitação da API do Graph da seguinte maneira: defina a versão como "BETA", o tipo de solicitação como "PATCH" e a URL como `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` – use o GUID da Etapa 3 para `<id>`.</span><span class="sxs-lookup"><span data-stu-id="7b934-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="7b934-165">Copie e cole a seguinte solicitação JSON no campo "Corpo da Solicitação".</span><span class="sxs-lookup"><span data-stu-id="7b934-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="7b934-166">Altere os valores do Bloqueio Inteligente conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="7b934-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="7b934-167">Clique em "Executar Consulta" para atualizar os valores do Bloqueio Inteligente de seu locatário.</span><span class="sxs-lookup"><span data-stu-id="7b934-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="7b934-168">Verifique se você atualizou os valores do Bloqueio Inteligente de seu locatário corretamente usando [estas etapas](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="7b934-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b934-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b934-169">Next steps</span></span>
- <span data-ttu-id="7b934-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.</span><span class="sxs-lookup"><span data-stu-id="7b934-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
