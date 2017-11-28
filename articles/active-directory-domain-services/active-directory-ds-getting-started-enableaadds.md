---
title: 'Azure Active Directory Domain Services: habilitar Azure Active Directory Domain Services | Microsoft Docs'
description: "Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="fc952-103">Habilitar o Azure Active Directory Domain Services usando Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="fc952-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>

## <a name="task-3-enable-azure-active-directory-domain-services"></a><span data-ttu-id="fc952-104">Tarefa 3: habilitar o Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="fc952-104">Task 3: enable Azure Active Directory Domain Services</span></span>
<span data-ttu-id="fc952-105">Nesta tarefa, você habilitar serviços de domínio de diretório ativo do Azure (Azure AD DS) para seu diretório fazendo Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fc952-105">In this task, you enable Azure Active Directory Domain Services (Azure AD DS) for your directory by doing hello following steps:</span></span>

1. <span data-ttu-id="fc952-106">Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fc952-106">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fc952-107">No painel esquerdo do hello, selecione Olá **do Active Directory** botão.</span><span class="sxs-lookup"><span data-stu-id="fc952-107">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="fc952-108">Selecione o locatário do Azure Active Directory (AD do Azure) de saudação (diretório) para o qual você deseja tooenable do Azure AD DS.</span><span class="sxs-lookup"><span data-stu-id="fc952-108">Select hello Azure Active Directory (Azure AD) tenant (directory) for which you want tooenable Azure AD DS.</span></span>

    ![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="fc952-110">Em Olá **directory visualização** , clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="fc952-110">On hello **preview directory** page, click hello **Configure** tab.</span></span>

    ![Guia Configurar do diretório](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="fc952-112">Em **dos serviços de domínio**, alterar Olá **habilitar serviços de domínio para este diretório** opção muito**Sim**.</span><span class="sxs-lookup"><span data-stu-id="fc952-112">Under **domain services**, change hello **Enable domain services for this directory** option too**Yes**.</span></span>  
    <span data-ttu-id="fc952-113">Opções adicionais de configuração do Azure Active Directory Domain Services aparecem na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc952-113">Additional Azure Active Directory Domain Services configuration options appear on hello page.</span></span>

    ![Habilitar Serviços de Domínio](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > <span data-ttu-id="fc952-115">Quando você habilita o Azure Active Directory Domain Services para seu locatário, o AD do Azure gera e armazena Olá Kerberos e NTLM hashes de credenciais que são necessários para autenticar usuários.</span><span class="sxs-lookup"><span data-stu-id="fc952-115">When you enable Azure Active Directory Domain Services for your tenant, Azure AD generates and stores hello Kerberos and NTLM credential hashes that are required for authenticating users.</span></span>
   >
   >
6. <span data-ttu-id="fc952-116">Especifique a saudação **nome de domínio DNS dos serviços de domínio**.</span><span class="sxs-lookup"><span data-stu-id="fc952-116">Specify hello **DNS domain name of domain services**.</span></span>

   * <span data-ttu-id="fc952-117">nome de domínio saudação padrão do diretório de saudação (com um **. c o m** sufixo) é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="fc952-117">hello default domain name of hello directory (with a **.onmicrosoft.com** suffix) is selected by default.</span></span>

   * <span data-ttu-id="fc952-118">Olá lista contém todos os domínios que foram configurados para seu diretório do AD do Azure, inclusive verificado e não verificadas domínios que você configura no hello **domínios** guia.</span><span class="sxs-lookup"><span data-stu-id="fc952-118">hello list contains all domains that have been configured for your Azure AD directory, including both verified and unverified domains that you configure on hello **Domains** tab.</span></span>

   * <span data-ttu-id="fc952-119">Você também pode inserir um nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="fc952-119">You can also enter a custom domain name.</span></span> <span data-ttu-id="fc952-120">Neste exemplo, é o nome de domínio personalizado Olá *contoso100.com*.</span><span class="sxs-lookup"><span data-stu-id="fc952-120">In this example, hello custom domain name is *contoso100.com*.</span></span>

     > [!WARNING]
     > <span data-ttu-id="fc952-121">prefixo de saudação do seu nome de domínio especificado (por exemplo, *contoso100* em Olá *contoso100.com* nome de domínio) deve conter a 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fc952-121">hello prefix of your specified domain name (for example, *contoso100* in hello *contoso100.com* domain name) must contain 15 or fewer characters.</span></span> <span data-ttu-id="fc952-122">Você não pode criar um domínio do Azure Active Directory Domain Services com um prefixo que contenha mais de 15 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fc952-122">You cannot create an Azure Active Directory Domain Services domain with a prefix containing more than 15 characters.</span></span>
     >
     >
7. <span data-ttu-id="fc952-123">Verifique se esse nome de domínio DNS Olá escolhido para Olá gerenciado domínio ainda não existir na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fc952-123">Ensure that hello DNS domain name you have chosen for hello managed domain does not already exist in hello virtual network.</span></span> <span data-ttu-id="fc952-124">Especificamente, verifique se toosee:</span><span class="sxs-lookup"><span data-stu-id="fc952-124">Specifically, check toosee whether:</span></span>

   * <span data-ttu-id="fc952-125">Você já tiver um domínio com hello mesmo nome de domínio DNS na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fc952-125">You already have a domain with hello same DNS domain name on hello virtual network.</span></span>

   * <span data-ttu-id="fc952-126">rede virtual que você selecionou Hello tem uma conexão VPN com a sua rede local, e você tiver um domínio com hello mesmo nome de domínio DNS na rede local.</span><span class="sxs-lookup"><span data-stu-id="fc952-126">hello virtual network you've selected has a VPN connection with your on-premises network, and you have a domain with hello same DNS domain name on your on-premises network.</span></span>

   * <span data-ttu-id="fc952-127">Você tem um serviço de nuvem existente com esse nome na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="fc952-127">You have an existing cloud service with that name on hello virtual network.</span></span>
8. <span data-ttu-id="fc952-128">Selecione uma rede virtual no qual você deseja que o Azure Active Directory Domain Services toobe disponível.</span><span class="sxs-lookup"><span data-stu-id="fc952-128">Select a virtual network on which you want Azure Active Directory Domain Services toobe available.</span></span> <span data-ttu-id="fc952-129">Selecione Olá uma rede virtual e sub-rede dedicada que você criou no hello **domínio conectar serviços de rede virtual toothis** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="fc952-129">Select hello virtual network and dedicated subnet you created in hello **Connect domain services toothis virtual network** drop-down list.</span></span> <span data-ttu-id="fc952-130">Considere também Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="fc952-130">Also consider hello following:</span></span>

   * <span data-ttu-id="fc952-131">Certifique-se de que essa rede virtual Olá especificado pertence tooan região do Azure que é compatível com o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fc952-131">Ensure that hello virtual network that you have specified belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="fc952-132">tooascertain Olá regiões do Azure, onde o Azure Active Directory Domain Services está disponível, consulte [os serviços do Azure por região](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="fc952-132">tooascertain hello Azure regions where Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>

   * <span data-ttu-id="fc952-133">Redes virtuais que pertencem a região tooa onde não há suporte para Azure Active Directory Domain Services não aparecem na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc952-133">Virtual networks that belong tooa region where Azure Active Directory Domain Services is not supported do not show up in hello drop-down list.</span></span>

   * <span data-ttu-id="fc952-134">Use uma sub-rede dedicada em rede virtual Olá para o Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fc952-134">Use a dedicated subnet within hello virtual network for Azure Active Directory Domain Services.</span></span> <span data-ttu-id="fc952-135">Fazer *não* selecione Olá sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="fc952-135">Do *not* select hello gateway subnet.</span></span> <span data-ttu-id="fc952-136">Confira [Considerações de rede](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="fc952-136">See [networking considerations](active-directory-ds-networking.md).</span></span>

   * <span data-ttu-id="fc952-137">Da mesma forma, redes virtuais que foram criadas usando o Gerenciador de recursos do Azure não aparecem na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc952-137">Similarly, virtual networks that were created by using Azure Resource Manager do not appear in hello drop-down list.</span></span> <span data-ttu-id="fc952-138">No momento, as redes virtuais baseadas no Resource Manager não têm suporte dos Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="fc952-138">Resource Manager-based virtual networks are not currently supported by Azure Active Directory Domain Services.</span></span>
9. <span data-ttu-id="fc952-139">tooenable do Azure Active Directory Domain Services, no painel de tarefas Olá final Olá Olá página, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="fc952-139">tooenable Azure Active Directory Domain Services, in hello task pane at hello bottom of hello page, click **Save**.</span></span>
    * <span data-ttu-id="fc952-140">Enquanto o Azure Active Directory Domain Services está sendo habilitada para seu diretório, página Olá exibe um status de *pendente*.</span><span class="sxs-lookup"><span data-stu-id="fc952-140">While Azure Active Directory Domain Services is being enabled for your directory, hello page displays a status of *Pending*.</span></span>

        ![Habilitar janela de serviços de domínio](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > <span data-ttu-id="fc952-142">O Azure Active Directory Domain Services fornece alta disponibilidade para seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="fc952-142">Azure Active Directory Domain Services provides high availability for your managed domain.</span></span> <span data-ttu-id="fc952-143">Depois de habilitar o Azure Active Directory Domain Services, endereços IP de saudação em qual domínio os serviços estão disponíveis na rede virtual Olá são exibidos um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="fc952-143">After you enable Azure Active Directory Domain Services, hello IP addresses at which domain services are available on hello virtual network are displayed one at a time.</span></span> <span data-ttu-id="fc952-144">segundo endereço IP Hello é exibido pela primeira vez, logo após hello como assim serviço Olá habilita a alta disponibilidade para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="fc952-144">hello second IP address is displayed shortly after hello first, as soon hello service enables high availability for your domain.</span></span> <span data-ttu-id="fc952-145">Quando a alta disponibilidade está configurada e ativo para o seu domínio, você deverá ver dois endereços IP em hello **dos serviços de domínio** seção Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="fc952-145">When high availability is configured and active for your domain, you should see two IP addresses in hello **domain services** section of hello **Configure** tab.</span></span>
        >
        >
    * <span data-ttu-id="fc952-146">Depois de cerca de 20 minutos de too30, Olá primeiro endereço IP no qual domínio os serviços estão disponíveis em sua rede virtual na Olá **endereço IP** campo Olá **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="fc952-146">After about 20 too30 minutes, hello first IP address at which domain services are available on your virtual network in hello **IP address** field on hello **Configure** page.</span></span>

        ![Janela de serviços de domínio exibindo o primeiro IP provisionado](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * <span data-ttu-id="fc952-148">Quando a alta disponibilidade é operacional para seu domínio, dois endereços IP são exibidos na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc952-148">When high availability is operational for your domain, two IP addresses are displayed on hello page.</span></span> <span data-ttu-id="fc952-149">O domínio gerenciado está disponível em sua rede virtual selecionada nesses dois endereços IP.</span><span class="sxs-lookup"><span data-stu-id="fc952-149">Your managed domain is available on your selected virtual network at these two IP addresses.</span></span>

10. <span data-ttu-id="fc952-150">Observe os dois endereços IP Olá para que você possa atualizar as configurações de DNS Olá para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="fc952-150">Note hello two IP addresses so that you can update hello DNS settings for your virtual network.</span></span> <span data-ttu-id="fc952-151">Isso permite que máquinas virtuais no domínio do hello rede virtual tooconnect toohello para operações como ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="fc952-151">Doing so enables virtual machines on hello virtual network tooconnect toohello domain for operations such as domain join.</span></span>

    ![Janela de serviços de domínio mostrando ambos os IPs provisionados](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> <span data-ttu-id="fc952-153">Dependendo do tamanho de saudação do seu locatário do AD do Azure (por exemplo, o número de saudação de usuários ou grupos), o domínio gerenciado do tooyour sincronização leva algum tempo.</span><span class="sxs-lookup"><span data-stu-id="fc952-153">Depending on hello size of your Azure AD tenant (for example, hello number of users or groups), synchronization tooyour managed domain takes a while.</span></span> <span data-ttu-id="fc952-154">Esse processo de sincronização ocorre no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fc952-154">This synchronization process happens in hello background.</span></span> <span data-ttu-id="fc952-155">Para locatários grandes com dezenas de milhares de objetos, pode levar um ou dois dias para todos os usuários, associações de grupo e as credenciais toobe sincronizados.</span><span class="sxs-lookup"><span data-stu-id="fc952-155">For large tenants with tens of thousands of objects, it might take a day or two for all users, group memberships, and credentials toobe synchronized.</span></span>
>
>

## <a name="next-step"></a><span data-ttu-id="fc952-156">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="fc952-156">Next step</span></span>
[<span data-ttu-id="fc952-157">Tarefa 4: atualizar configurações de DNS Olá Olá rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="fc952-157">Task 4: update hello DNS settings for hello Azure virtual network</span></span>](active-directory-ds-getting-started-update-dns.md)
