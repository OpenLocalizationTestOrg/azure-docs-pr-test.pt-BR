---
title: "aaaTroubleshoot criando coleções do RemoteApp híbrido | Microsoft Docs"
description: "Saiba como falhas na criação de coleção híbrida tootroubleshoot RemoteApp"
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
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a><span data-ttu-id="4ab71-103">Solucionar problemas na criação de coleções híbridas do RemoteApp do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab71-103">Troubleshoot creating Azure RemoteApp hybrid collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4ab71-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="4ab71-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4ab71-105">Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="4ab71-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4ab71-106">Uma coleção híbrida é hospedada no e armazena dados em Olá nuvem do Azure, mas também permite que usuários acessem dados e recursos armazenados em sua rede local.</span><span class="sxs-lookup"><span data-stu-id="4ab71-106">A hybrid collection is hosted in and stores data in hello Azure cloud but also lets users access data and resources stored on your local network.</span></span> <span data-ttu-id="4ab71-107">Os usuários podem acessar aplicativos ao efetuar logon com suas credenciais corporativas sincronizadas ou federadas com o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab71-107">Users can access apps by logging in with their corporate credentials synchronized or federated with Azure Active Directory.</span></span> <span data-ttu-id="4ab71-108">Você pode implantar uma coleção híbrida que usa uma Rede Virtual existente do Azure, ou você pode criar uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4ab71-108">You can deploy a hybrid collection that uses an existing Azure Virtual Network, or you can create a new virtual network.</span></span> <span data-ttu-id="4ab71-109">Recomendamos que você crie ou use uma sub-rede da rede virtual com uma variedade CIDR grande o suficiente para futuro crescimento estimado para o RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab71-109">We recommend that you create or use a virtual network subnet with a CIDR range large enough for expected future growth for Azure RemoteApp.</span></span>

<span data-ttu-id="4ab71-110">Ainda não criou sua coleção?</span><span class="sxs-lookup"><span data-stu-id="4ab71-110">Haven't created your collection yet?</span></span> <span data-ttu-id="4ab71-111">Consulte [criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md) para etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab71-111">See [Create a hybrid collection](remoteapp-create-hybrid-deployment.md) for hello steps.</span></span>

<span data-ttu-id="4ab71-112">Se você estiver tendo problemas para criar sua coleção, ou se não estiver funcionando, coleção Olá maneira Olá achar que deve, confira Olá informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ab71-112">If you are having trouble creating your collection, or if hello collection isn't working hello way you think it should, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="4ab71-113">A imagem é inválida</span><span class="sxs-lookup"><span data-stu-id="4ab71-113">Your image is invalid</span></span>
<span data-ttu-id="4ab71-114">Se você vir uma mensagem como "GoldImageInvalid" quando você está esperando por Azure tooprovision sua coleção, isso significa que a imagem de modelo não atende a saudação [definido requisitos de imagem](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="4ab71-114">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="4ab71-115">Assim, vá ler os [requisitos](remoteapp-imagereqs.md), corrija sua imagem e tente toocreate sua coleção novamente.</span><span class="sxs-lookup"><span data-stu-id="4ab71-115">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="does-your-vnet-have-network-security-groups-defined"></a><span data-ttu-id="4ab71-116">A sua VNET tem grupos de segurança de rede definidos?</span><span class="sxs-lookup"><span data-stu-id="4ab71-116">Does your VNET have network security groups defined?</span></span>
<span data-ttu-id="4ab71-117">Se você tiver definidos na sub-rede Olá que você está usando para sua coleção de grupos de segurança de rede, verifique se esses [URLs e portas](remoteapp-ports.md) são acessíveis a partir de sua sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4ab71-117">If you have network security groups defined on hello subnet you are using for your collection, make sure these [URLs and ports](remoteapp-ports.md) are accessible from within your subnet.</span></span>

<span data-ttu-id="4ab71-118">Você pode adicionar rede adicional segurança grupos toohello VMs implantadas por você na sub-rede Olá para um controle.</span><span class="sxs-lookup"><span data-stu-id="4ab71-118">You can add additional network security groups toohello VMs deployed by you in hello subnet for tighter control.</span></span>

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a><span data-ttu-id="4ab71-119">Você está usando seus próprios servidores DNS?</span><span class="sxs-lookup"><span data-stu-id="4ab71-119">Are you using your own DNS servers?</span></span> <span data-ttu-id="4ab71-120">Eles são acessíveis da sua sub-rede VNET?</span><span class="sxs-lookup"><span data-stu-id="4ab71-120">And are they accessible from your VNET subnet?</span></span>
> [!NOTE]
> <span data-ttu-id="4ab71-121">Você tem toomake Olá-se de que os servidores DNS na sua rede virtual estão sempre ativados e sempre capaz tooresolve máquinas de virtuais de Olá hospedadas em redes de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab71-121">You have toomake sure hello DNS servers in your VNET are always up and always able tooresolve hello virtual machines hosted in hello VNET.</span></span> <span data-ttu-id="4ab71-122">Não use o DNS do Google para isso.</span><span class="sxs-lookup"><span data-stu-id="4ab71-122">Don't use Google DNS for this.</span></span>
> 
> 

<span data-ttu-id="4ab71-123">Para coleções híbridas, use seus próprios servidores DNS.</span><span class="sxs-lookup"><span data-stu-id="4ab71-123">For hybrid collections you use your own DNS servers.</span></span> <span data-ttu-id="4ab71-124">Você especificá-los em seu esquema de configuração de rede ou por meio do portal de gerenciamento hello quando você criar sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4ab71-124">You specify them in your network configuration schema or through hello management portal when you create your virtual network.</span></span> <span data-ttu-id="4ab71-125">Servidores DNS são usados na ordem de saudação que elas são especificadas em uma forma de failover (como tooround contrário robin).</span><span class="sxs-lookup"><span data-stu-id="4ab71-125">DNS servers are used in hello order that they are specified in a failover manner (as opposed tooround robin).</span></span>  
<span data-ttu-id="4ab71-126">Consulte também[resolução de nomes para VMs e instâncias de função](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake-se de que os servidores DNS estão correcly configurado.</span><span class="sxs-lookup"><span data-stu-id="4ab71-126">Please refer too[Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake sure your DNS servers are configured correcly.</span></span>

<span data-ttu-id="4ab71-127">Verifique se os servidores DNS Olá para sua coleção estão acessíveis e disponíveis na sub-rede da rede virtual de saudação especificado para esta coleção.</span><span class="sxs-lookup"><span data-stu-id="4ab71-127">Make sure hello DNS servers for your collection are accessible and available from hello VNET subnet you specified for this collection.</span></span>

<span data-ttu-id="4ab71-128">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="4ab71-128">For example:</span></span>

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Definir o DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a><span data-ttu-id="4ab71-130">Você está usando um controlador de domínio do Active Directory em sua coleção?</span><span class="sxs-lookup"><span data-stu-id="4ab71-130">Are you using an Active Directory domain controller in your collection?</span></span>
<span data-ttu-id="4ab71-131">No momento, somente um domínio do Active Directory pode ser associado ao RemoteApp do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab71-131">Currently only one Active Directory domain can be associated with Azure RemoteApp.</span></span> <span data-ttu-id="4ab71-132">a coleção de híbrida Olá suporta apenas as contas do Active Directory do Azure que foram sincronizadas usando a ferramenta DirSync de uma implantação do Windows Server Active Directory; Especificamente, ou sincronizados com a opção de sincronização de senha Olá sincronizado com a federação de serviços de Federação do Active Directory (AD FS) configurada.</span><span class="sxs-lookup"><span data-stu-id="4ab71-132">hello hybrid collection supports only Azure Active Directory accounts that have been synced using DirSync tool from a Windows Server Active Directory deployment; specifically, either synced with hello Password Synchronization option or synced with Active Directory Federation Services (AD FS) federation configured.</span></span> <span data-ttu-id="4ab71-133">Você precisa toocreate um domínio personalizado que coincide com o sufixo de domínio do UPN Olá para seu domínio local e configurar a integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="4ab71-133">You need toocreate a custom domain that matches hello UPN domain suffix for your on-premises domain and set up directory integration.</span></span>

<span data-ttu-id="4ab71-134">Confira [Configurando o Active Directory para o RemoteApp do Azure](remoteapp-ad.md) para obter informações de planejamento.</span><span class="sxs-lookup"><span data-stu-id="4ab71-134">See [Configuring Active Directory for Azure RemoteApp](remoteapp-ad.md) for more information.</span></span>

<span data-ttu-id="4ab71-135">Certifique-se de detalhes do domínio Olá fornecidos são válidos e o controlador de domínio Olá é acessível a partir do hello que VM criada na sub-rede Olá usado para o aplicativo remoto do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab71-135">Make sure hello domain details provided are valid and hello domain controller is reachable from hello VM created in hello subnet used for Azure Remote App.</span></span> <span data-ttu-id="4ab71-136">Verifique também se a conta de serviço Olá credenciais fornecidas têm permissões tooadd computadores toohello desde que o domínio e que Olá nome AD fornecido pode ser resolvida a partir de saudação DNS fornecido na VNET de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab71-136">Also make sure hello service account credentials supplied have permissions tooadd computers toohello provided domain and that hello AD name provided can be resolved from hello DNS provided in hello VNET.</span></span>

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a><span data-ttu-id="4ab71-137">Que nome de domínio você especificou quando criou a sua coleção?</span><span class="sxs-lookup"><span data-stu-id="4ab71-137">What domain name did you specify when you created your collection?</span></span>
<span data-ttu-id="4ab71-138">o nome de domínio Olá criado ou adicionado deve ser um nome de domínio interno (não o nome de domínio do AD do Azure) e deve estar no formato DNS resolvido (contoso. local).</span><span class="sxs-lookup"><span data-stu-id="4ab71-138">hello domain name you created or added must be an internal domain name (not your Azure AD domain name) and must be in resolvable DNS format (contoso.local).</span></span> <span data-ttu-id="4ab71-139">Por exemplo, você tem um nome interno do Active Directory (contoso. local) e um UPN de diretório ativo (contoso.com) - você tem nome interno do toouse hello quando você cria sua coleção.</span><span class="sxs-lookup"><span data-stu-id="4ab71-139">For example, you have an Active Directory internal name (contoso.local) and an Active Directory UPN (contoso.com) - you have toouse hello internal name when you create your collection.</span></span>

