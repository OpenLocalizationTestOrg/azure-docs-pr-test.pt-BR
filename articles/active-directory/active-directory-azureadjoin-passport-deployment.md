---
title: "Habilitar o Microsoft Windows Hello for Business em sua organização |Microsoft Docs"
description: "Instruções de implantação para habilitar o Microsoft Passport na sua organização."
services: active-directory
documentationcenter: 
keywords: "configurar o Microsoft Passport, implantação do Microsoft Windows Hello for Business"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="171f0-104">Habilitar o Microsoft Windows Hello for Business em sua organização</span><span class="sxs-lookup"><span data-stu-id="171f0-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="171f0-105">Depois de [conectar os dispositivos integrados ao domínio do Windows 10 ao Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), faça o seguinte para habilitar o Microsoft Windows Hello para Empresas em sua organização:</span><span class="sxs-lookup"><span data-stu-id="171f0-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="171f0-106">Implantar o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="171f0-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="171f0-107">Definir as configurações de política</span><span class="sxs-lookup"><span data-stu-id="171f0-107">Configure policy settings</span></span>
3. <span data-ttu-id="171f0-108">Configurar o perfil de certificado</span><span class="sxs-lookup"><span data-stu-id="171f0-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="171f0-109">Implantar o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="171f0-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="171f0-110">Para implantar certificados de usuário baseados em chaves do Windows Hello for Business, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="171f0-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="171f0-111">**Ramificação atual do System Center Configuration Manager** - Você precisa instalar a versão 1606 ou superior.</span><span class="sxs-lookup"><span data-stu-id="171f0-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="171f0-112">Para saber mais, confira a [Documentação do System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) e [Blog da equipe do System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="171f0-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="171f0-113">**PKI (infraestrutura de chave pública)**: para habilitar o Microsoft Windows Hello para Empresas usando certificados de usuário, você deve ter uma PKI em vigor.</span><span class="sxs-lookup"><span data-stu-id="171f0-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="171f0-114">Caso você não tenha uma ou não queira usá-la para certificados de usuário, você pode implantar um novo controlador de domínio que tenha a build 10551 (ou superior) do Windows Server 2016 instalada.</span><span class="sxs-lookup"><span data-stu-id="171f0-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="171f0-115">Siga as etapas para [instalar um controlador de domínio de réplica em um domínio existente](https://technet.microsoft.com/library/jj574134.aspx) ou para [instalar uma nova floresta do Active Directory, caso você esteja criando um novo ambiente](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="171f0-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="171f0-116">(Os ISOs estão disponíveis para download em [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="171f0-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="171f0-117">Definir as configurações de política</span><span class="sxs-lookup"><span data-stu-id="171f0-117">Configure policy settings</span></span>
<span data-ttu-id="171f0-118">Para definir as configurações de política no Microsoft Windows Hello para Empresas, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="171f0-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="171f0-119">Política de grupo no Active Directory</span><span class="sxs-lookup"><span data-stu-id="171f0-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="171f0-120">System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="171f0-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="171f0-121">Usar a Política de grupo no Active Directory é o método recomendado para definir as configurações de política no Microsoft Windows Hello para Empresas.</span><span class="sxs-lookup"><span data-stu-id="171f0-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="171f0-122">Usar o System Center Configuration Manager é o método preferencial quando você também for usá-lo para implantar certificados.</span><span class="sxs-lookup"><span data-stu-id="171f0-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="171f0-123">Este cenário:</span><span class="sxs-lookup"><span data-stu-id="171f0-123">This scenario:</span></span>

* <span data-ttu-id="171f0-124">Garante a compatibilidade com os novos cenários de implantação</span><span class="sxs-lookup"><span data-stu-id="171f0-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="171f0-125">Exige do cliente a versão 1607 ou superior do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="171f0-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="171f0-126">Configurar o Microsoft Windows Hello para Empresas usando a Política de Grupo no Active Directory</span><span class="sxs-lookup"><span data-stu-id="171f0-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="171f0-127">**Etapas**:</span><span class="sxs-lookup"><span data-stu-id="171f0-127">**Steps**:</span></span>

1. <span data-ttu-id="171f0-128">Abra o Gerenciador do Servidor e navegue até **Ferramentas** > **Gerenciamento de Política de Grupo**.</span><span class="sxs-lookup"><span data-stu-id="171f0-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="171f0-129">No Gerenciamento de Política de Grupo, navegue até o nó de domínio que corresponde ao domínio no qual você deseja habilitar o Ingresso no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="171f0-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="171f0-130">Clique com o botão direito do mouse em **Objetos de Política de Grupo** e selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="171f0-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="171f0-131">Dê um nome ao seu Objeto de Política de Grupo, por exemplo, Habilitar o Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="171f0-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="171f0-132">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="171f0-132">Click **OK**.</span></span>
4. <span data-ttu-id="171f0-133">Clique com o botão direito do mouse em seu novo Objeto de Política de Grupo e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="171f0-134">Navegue até **Configuração do Computador** > **Políticas** > **Modelos Administrativos** > **Componentes do Windows** > **Windows Hello para Empresas**.</span><span class="sxs-lookup"><span data-stu-id="171f0-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="171f0-135">Clique com o botão direito em **Habilitar o Windows Hello para Empresas** e, em seguida, selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="171f0-136">Selecione o botão de opção **Habilitado** e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="171f0-137">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="171f0-137">Click **OK**.</span></span>
8. <span data-ttu-id="171f0-138">Agora você pode vincular o Objeto de Política de Grupo para um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="171f0-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="171f0-139">Para habilitar essa política para todos os dispositivos do Windows 10 associados ao domínio em sua organização, vincule a Política de Grupo ao domínio.</span><span class="sxs-lookup"><span data-stu-id="171f0-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="171f0-140">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="171f0-140">For example:</span></span>
   * <span data-ttu-id="171f0-141">Uma UO (unidade organizacional) específica no Active Directory onde os computadores ingressados no domínio do Windows 10 estejam localizados.</span><span class="sxs-lookup"><span data-stu-id="171f0-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="171f0-142">Um grupo de segurança específico com computadores ingressados no domínio do Windows 10 que serão registrados automaticamente no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="171f0-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="171f0-143">Configurar o Windows Hello for Business usando o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="171f0-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="171f0-144">**Etapas**:</span><span class="sxs-lookup"><span data-stu-id="171f0-144">**Steps**:</span></span>

1. <span data-ttu-id="171f0-145">Abrir o **System Center Configuration Manager** e, em seguida, navegar até **Ativos e Conformidade > Configurações de Conformidade > Acesso a Recursos da Empresa > Perfis do Windows Hello para Empresas**.</span><span class="sxs-lookup"><span data-stu-id="171f0-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="171f0-147">Na barra de ferramentas na parte superior, clique em **Criar perfil Windows Hello for Business**.</span><span class="sxs-lookup"><span data-stu-id="171f0-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="171f0-149">Na caixa de diálogo **Geral** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="171f0-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="171f0-151">a.</span><span class="sxs-lookup"><span data-stu-id="171f0-151">a.</span></span> <span data-ttu-id="171f0-152">Na caixa de diálogo **Nome**, digite um nome para seu perfil, por exemplo, **Meu Perfil WHfB**.</span><span class="sxs-lookup"><span data-stu-id="171f0-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="171f0-153">b.</span><span class="sxs-lookup"><span data-stu-id="171f0-153">b.</span></span> <span data-ttu-id="171f0-154">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-154">Click **Next**.</span></span>
4. <span data-ttu-id="171f0-155">Na caixa de diálogo **Plataformas com Suporte**, selecione as plataformas que serão provisionadas com esse perfil do Windows Hello para Empresas e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="171f0-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="171f0-157">Na caixa de diálogo **Configurações** , execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="171f0-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="171f0-159">a.</span><span class="sxs-lookup"><span data-stu-id="171f0-159">a.</span></span> <span data-ttu-id="171f0-160">Em **Configurar o Windows Hello para Empresas**, selecionar **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="171f0-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="171f0-161">b.</span><span class="sxs-lookup"><span data-stu-id="171f0-161">b.</span></span> <span data-ttu-id="171f0-162">Em **Usar um TPM (Trusted Platform Module)**, selecione **Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="171f0-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="171f0-163">c.</span><span class="sxs-lookup"><span data-stu-id="171f0-163">c.</span></span> <span data-ttu-id="171f0-164">Em **Método de autenticação**, selecione **Baseado em certificado**.</span><span class="sxs-lookup"><span data-stu-id="171f0-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="171f0-165">d.</span><span class="sxs-lookup"><span data-stu-id="171f0-165">d.</span></span> <span data-ttu-id="171f0-166">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-166">Click **Next**.</span></span>
6. <span data-ttu-id="171f0-167">Na caixa de diálogo de **Resumo**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="171f0-168">Na caixa de diálogo **Conclusão**, clique em **Fechar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="171f0-169">Na barra de ferramentas na parte superior, clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="171f0-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Configurar o Windows Hello for Business](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="171f0-171">Configurar o perfil de certificado</span><span class="sxs-lookup"><span data-stu-id="171f0-171">Configure the certificate profile</span></span>
<span data-ttu-id="171f0-172">Se você estiver usando a autenticação baseada em certificado para autenticação local, você precisará configurar e implantar um perfil de certificado.</span><span class="sxs-lookup"><span data-stu-id="171f0-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="171f0-173">Essa tarefa exige que você configure um servidor NDES e a função de site do Ponto de Registro de Certificado no System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="171f0-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="171f0-174">Para obter mais detalhes, consulte os [Pré-requisitos para perfis de Certificado no Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="171f0-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="171f0-175">Abra o **System Center Configuration Manager** e, em seguida, navegue até **Ativos e Conformidade > Configurações de Conformidade > Acesso a Recursos da Empresa > Perfis de Certificado**.</span><span class="sxs-lookup"><span data-stu-id="171f0-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="171f0-176">Selecione um modelo que tenha EKU (uso estendido da chave) para entrada com cartão inteligente.</span><span class="sxs-lookup"><span data-stu-id="171f0-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="171f0-177">Na página **Registro do SCEP** do perfil de certificado, você precisa escolher **Instalar Passport for Work se houver falha** como o **Provedor de Armazenamento de Chave**.</span><span class="sxs-lookup"><span data-stu-id="171f0-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="171f0-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="171f0-178">Next steps</span></span>
* [<span data-ttu-id="171f0-179">Windows 10 para a empresa: maneiras de usar dispositivos para o trabalho</span><span class="sxs-lookup"><span data-stu-id="171f0-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="171f0-180">Estendendo os recursos de nuvem para dispositivos Windows 10 por meio da Junção do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="171f0-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="171f0-181">Autenticando identidades sem senhas com o Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="171f0-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="171f0-182">Saiba mais sobre cenários de uso da Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="171f0-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="171f0-183">Conectar dispositivos ingressados no domínio ao AD do Azure para experiências com o Windows 10</span><span class="sxs-lookup"><span data-stu-id="171f0-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="171f0-184">Configurar a Junção do Azure AD</span><span class="sxs-lookup"><span data-stu-id="171f0-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

