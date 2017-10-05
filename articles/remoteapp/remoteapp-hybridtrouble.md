---
title: "Solucionar problemas na criação de coleções híbridas do RemoteApp | Microsoft Docs"
description: "Saiba como solucionar problemas de falhas de criação de coleção híbrida do RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: a486dcb3f994cd78311ee86521a6792a4d57438e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="14b9f-103">Solucionar problemas na criação de coleções híbridas do RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="14b9f-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="14b9f-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="14b9f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="14b9f-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="14b9f-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="14b9f-106">Uma coleção híbrida é hospedada e armazena os dados na nuvem do Azure, mas também permite aos usuários acessarem dados e recursos armazenados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="14b9f-106">A hybrid collection is hosted in and stores data in the Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="14b9f-107">Os usuários podem acessar aplicativos ao efetuar logon com suas credenciais corporativas sincronizadas ou federadas com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="14b9f-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="14b9f-108">Você pode implantar uma coleção híbrida que usa uma Rede Virtual existente do Azure, ou você pode criar uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="14b9f-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="14b9f-109">Recomendamos que você crie ou use uma sub-rede da rede virtual com uma variedade CIDR grande o suficiente para futuro crescimento estimado para o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="14b9f-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="14b9f-110">Ainda não criou sua coleção?</span><span class="sxs-lookup"><span data-stu-id="14b9f-110">Haven't created your collection yet?</span></span> <span data-ttu-id="14b9f-111">Confira [Criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="14b9f-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for the steps.</span></span>

<span data-ttu-id="14b9f-112">Se estiver enfrentando problemas para criar sua coleção, ou se a coleção não está funcionando como você acha que deveria, verifique as informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="14b9f-112">If you are having trouble creating your collection, or if the collection isn't working the way you think it should, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="14b9f-113">A imagem é inválida</span><span class="sxs-lookup"><span data-stu-id="14b9f-113">Your image is invalid</span></span>
<span data-ttu-id="14b9f-114">Se você receber uma mensagem como “GoldImageInvalid” quando estiver aguardando enquanto o Azure provisiona sua coleção, isso significa que a sua imagem de modelo não atende aos [requisitos de imagem definidos](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="14b9f-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="14b9f-115">Portanto, leia esses [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente criar novamente sua coleção.</span><span class="sxs-lookup"><span data-stu-id="14b9f-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="14b9f-116">A sua VNET tem grupos de segurança de rede definidos?</span><span class="sxs-lookup"><span data-stu-id="14b9f-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="14b9f-117">Se você tiver grupos de segurança de rede definidos na sub-rede que você está usando para sua coleção, verifique se essas [URLs e portas](remoteapp-ports.md) estão acessíveis de dentro da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="14b9f-117">If you have network security groups defined on the subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="14b9f-118">Você pode adicionar grupos de segurança de rede adicionais às máquinas virtuais implantadas por você na sub-rede para um controle mais rigoroso.</span><span class="sxs-lookup"><span data-stu-id="14b9f-118">You can add additional network security groups to the VMs deployed by you in the subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="14b9f-119">Você está usando seus próprios servidores DNS?</span><span class="sxs-lookup"><span data-stu-id="14b9f-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="14b9f-120">Eles são acessíveis da sua sub-rede VNET?</span><span class="sxs-lookup"><span data-stu-id="14b9f-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="14b9f-121">Você precisa verificar se os servidores DNS na sua rede virtual estão sempre ativados e sempre capazes de resolver os problemas das máquinas virtuais hospedadas na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="14b9f-121">You have to make sure the DNS servers in your VNET are always up and always able to resolve the virtual machines hosted in the VNET.</span></span> <span data-ttu-id="14b9f-122">Não use o DNS do Google para isso.</span><span class="sxs-lookup"><span data-stu-id="14b9f-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="14b9f-123">Para coleções híbridas, use seus próprios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="14b9f-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="14b9f-124">Você os especifica no seu esquema de configuração de rede ou por meio do portal de gerenciamento ao criar a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="14b9f-124">You specify them in your network configuration schema or through the management portal when you create your virtual network.</span></span> <span data-ttu-id="14b9f-125">Os servidores DNS são usados na ordem em que eles forem especificados em uma forma de failover (em vez de round robin).</span><span class="sxs-lookup"><span data-stu-id="14b9f-125">DNS servers are used in the order that they are specified in a failover manner (as opposed to round robin).</span></span>  
<span data-ttu-id="14b9f-126">Confira [Resolução de nomes de VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) para verificar se os servidores DNS estão configurados corretamente.</span><span class="sxs-lookup"><span data-stu-id="14b9f-126">Please refer to [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) to make sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="14b9f-127">Verifique se os servidores DNS de sua coleção estão acessíveis e disponíveis da sub-rede VNET especificada para essa coleção.</span><span class="sxs-lookup"><span data-stu-id="14b9f-127">Make sure the DNS servers for your collection are accessible and available from the VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="14b9f-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="14b9f-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir o DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="14b9f-130">Você está usando um controlador de domínio do Active Directory em sua coleção?</span><span class="sxs-lookup"><span data-stu-id="14b9f-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="14b9f-131">No momento, somente um domínio do Active Directory pode ser associado ao RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="14b9f-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="14b9f-132">A coleção híbrida dá suporte somente às contas do Active Directory do Azure que foram sincronizadas usando a ferramenta DirSync de uma implantação do Active Directory do Windows Server. Mais especificamente, sincronizado com a opção de Sincronização de Senha ou com federação dos Serviços de Federação do Active Directory (AD FS) configurada.</span><span class="sxs-lookup"><span data-stu-id="14b9f-132">The hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with the Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="14b9f-133">Você precisa criar um domínio personalizado que coincide com o sufixo de domínio para seu domínio local e configurar a integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="14b9f-133">You need to create a custom domain that matches the UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="14b9f-134">Confira [Configurando o Active Directory para o RemoteApp do Azure](remoteapp-ad.md) para obter informações de planejamento.</span><span class="sxs-lookup"><span data-stu-id="14b9f-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="14b9f-135">Verifique se os detalhes do domínio fornecidos são válidos e se o controlador de domínio está acessível da VM criada na sub-rede usada para o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="14b9f-135">Make sure the domain details provided are valid and the domain controller is reachable from the VM created in the subnet used for Azure Remote App.</span></span> <span data-ttu-id="14b9f-136">Verifique também se as credenciais da conta de serviço fornecidas têm permissões para adicionar computadores ao domínio fornecido e se o nome do AD fornecido pode ser resolvido a partir do DNS fornecido na VNET.</span><span class="sxs-lookup"><span data-stu-id="14b9f-136">Also make sure the service account credentials supplied have permissions to add computers to the provided domain and that the AD name provided can be resolved from the DNS provided in the VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="14b9f-137">Que nome de domínio você especificou quando criou a sua coleção?</span><span class="sxs-lookup"><span data-stu-id="14b9f-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="14b9f-138">O nome de domínio criado ou adicionado deve ser um nome de domínio interno (não o seu nome de domínio do Azure AD) e deve estar no formato DNS resolvível (contoso. local).</span><span class="sxs-lookup"><span data-stu-id="14b9f-138">The domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="14b9f-139">Por exemplo, você tem um nome interno do Active Directory (Contoso) e um UPN do Active Directory (contoso.com): deve, então, usar o nome interno ao criar sua coleção.</span><span class="sxs-lookup"><span data-stu-id="14b9f-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have to use the internal name when you create your collection.</span></span>

