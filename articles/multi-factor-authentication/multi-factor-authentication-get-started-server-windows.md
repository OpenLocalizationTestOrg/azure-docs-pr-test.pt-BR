---
title: "Autenticação do Windows e servidor Azure MFA | Microsoft Docs"
description: "Esta é a página do Azure Multi-Factor Authentication que auxiliará na implantação da Autenticação do Windows e do Servidor Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7e6384ea8fea686b5cad1a3bc3007252b9cfcd65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="35254-103">Autenticação do Windows e Servidor Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="35254-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="35254-104">Use a seção de autenticação do Windows do servidor de Autenticação Multifator do Azure para habilitar e configurar a autenticação do Windows para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="35254-104">Use the Windows Authentication section of the Azure Multi-Factor Authentication Server to enable and configure Windows authentication for applications.</span></span> <span data-ttu-id="35254-105">Antes de configurar a autenticação do Windows, lembre-se a lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="35254-105">Before you set up Windows Authentication, keep the following list in mind:</span></span>

* <span data-ttu-id="35254-106">Após a instalação, reinicie a Autenticação Multifator do Azure para que os serviços de Terminal entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="35254-106">After setup, reboot the Azure Multi-Factor Authentication for Terminal Services to take effect.</span></span>
* <span data-ttu-id="35254-107">Se a opção 'Exigir correspondência de usuário do Azure Multi-Factor Authentication' for marcada e você não estiver na lista de usuários, não será possível fazer logon no computador após a reinicialização.</span><span class="sxs-lookup"><span data-stu-id="35254-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in the user list, you will not be able to log into the machine after reboot.</span></span>
* <span data-ttu-id="35254-108">IPs confiáveis dependem de o aplicativo poder fornecer o IP do cliente com a autenticação.</span><span class="sxs-lookup"><span data-stu-id="35254-108">Trusted IPs is dependent on whether the application can provide the client IP with the authentication.</span></span> <span data-ttu-id="35254-109">Atualmente, apenas os Serviços de Terminal têm suporte.</span><span class="sxs-lookup"><span data-stu-id="35254-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="35254-110">Esse recurso não tem suporte para proteger os Serviços de Terminal no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="35254-110">This feature is not supported to secure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a><span data-ttu-id="35254-111">Para proteger um aplicativo com a Autenticação do Windows, use o procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="35254-111">To secure an application with Windows Authentication, use the following procedure.</span></span>
1. <span data-ttu-id="35254-112">No Servidor Azure Multi-Factor Authentication, clique no ícone de Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="35254-112">In the Azure Multi-Factor Authentication Server click the Windows Authentication icon.</span></span>
   <span data-ttu-id="35254-113">![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="35254-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="35254-114">Marque a caixa de seleção **Habilitar Autenticação do Windows**.</span><span class="sxs-lookup"><span data-stu-id="35254-114">Check the **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="35254-115">Por padrão, essa caixa está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="35254-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="35254-116">A guia Aplicativos permite que o administrador configure um ou mais aplicativos para Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="35254-116">The Applications tab allows the administrator to configure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="35254-117">Selecione um servidor ou aplicativo — especifique se o servidor/aplicativo está habilitado.</span><span class="sxs-lookup"><span data-stu-id="35254-117">Select a server or application – specify whether the server/application is enabled.</span></span> <span data-ttu-id="35254-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35254-118">Click **OK**.</span></span>
5. <span data-ttu-id="35254-119">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="35254-119">Click **Add…**</span></span>
6. <span data-ttu-id="35254-120">A guia IPs Confiáveis permite que você ignore as sessões do Azure Multi-Factor Authentication para Windows originadas de IPs específicos.</span><span class="sxs-lookup"><span data-stu-id="35254-120">The Trusted IPs tab allows you to skip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="35254-121">Por exemplo, se os funcionários usarem o aplicativo no escritório e em casa, você pode decidir que não deseja que seus telefones toquem para o Azure Multi-Factor Authentication enquanto estiverem no escritório.</span><span class="sxs-lookup"><span data-stu-id="35254-121">For example, if employees use the application from the office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at the office.</span></span> <span data-ttu-id="35254-122">Para isso, você especifica a sub-rede do escritório como entrada de IPs Confiáveis.</span><span class="sxs-lookup"><span data-stu-id="35254-122">For this, you would specify the office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="35254-123">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="35254-123">Click **Add…**</span></span>
8. <span data-ttu-id="35254-124">Selecione **IP Único** se desejar ignorar um único endereço IP.</span><span class="sxs-lookup"><span data-stu-id="35254-124">Select **Single IP** if you would like to skip a single IP address.</span></span>
9. <span data-ttu-id="35254-125">Selecione o **Intervalo de IP** se desejar ignorar um intervalo inteiro de IP.</span><span class="sxs-lookup"><span data-stu-id="35254-125">Select **IP Range** if you would like to skip an entire IP range.</span></span> <span data-ttu-id="35254-126">Exemplo 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="35254-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="35254-127">Selecione **Sub-rede** se desejar especificar um intervalo de IPs usando a notação de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="35254-127">Select **Subnet** if you would like to specify a range of IPs using subnet notation.</span></span> <span data-ttu-id="35254-128">Insira o IP inicial da sub-rede e escolha a máscara de rede adequada na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="35254-128">Enter the subnet's starting IP and pick the appropriate netmask from the drop-down list.</span></span>
11. <span data-ttu-id="35254-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="35254-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35254-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="35254-130">Next steps</span></span>

- [<span data-ttu-id="35254-131">Configure os dispositivos de VPN de terceiros para servidor Azure MFA</span><span class="sxs-lookup"><span data-stu-id="35254-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="35254-132">Aumentar sua infraestrutura de autenticação atual com a extensão do NPS para o Azure MFA</span><span class="sxs-lookup"><span data-stu-id="35254-132">Augment your existing authentication infrastructure with the NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
