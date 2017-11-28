---
title: "aaaWindows autenticação e o servidor Azure MFA | Microsoft Docs"
description: "Isso é a página de autenticação do Azure multi-factor Olá ajudará na implantação de autenticação do Windows e o servidor Azure multi-Factor Authentication."
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
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="9e1cf-103">Autenticação do Windows e Servidor Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9e1cf-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="9e1cf-104">Use a seção de autenticação do Windows hello de saudação servidor Azure multi-Factor Authentication tooenable e configurar a autenticação do Windows para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="9e1cf-105">Antes de configurar a autenticação do Windows, lembre-Olá lista em mente a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e1cf-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="9e1cf-106">Após a instalação, reinicialize hello Azure multi-Factor Authentication para efeito de tootake de serviços de Terminal.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="9e1cf-107">Se 'Correspondência de usuários exigir Azure multi-Factor Authentication' está marcada e você não estiver na lista de saudação do usuário, não será capaz de toolog na máquina de saudação após a reinicialização.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="9e1cf-108">IPs confiáveis que é depende se o aplicativo hello pode fornecer Olá IP do cliente com a autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="9e1cf-109">Atualmente, apenas os Serviços de Terminal têm suporte.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="9e1cf-110">Este recurso não está toosecure com suporte dos serviços de Terminal no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="9e1cf-111">toosecure um aplicativo com autenticação do Windows, use Olá procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="9e1cf-112">No servidor Azure multi-Factor Authentication de saudação Clique ícone de autenticação do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="9e1cf-113">![Autenticação do Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="9e1cf-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="9e1cf-114">Verificar Olá **habilitar autenticação do Windows** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="9e1cf-115">Por padrão, essa caixa está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="9e1cf-116">Guia de aplicativos Olá permite Olá administrador tooconfigure um ou mais aplicativos para autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="9e1cf-117">Selecione um servidor ou aplicativo – especifique se o servidor/aplicativo hello está habilitado.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="9e1cf-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-118">Click **OK**.</span></span>
5. <span data-ttu-id="9e1cf-119">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="9e1cf-119">Click **Add…**</span></span>
6. <span data-ttu-id="9e1cf-120">Guia do Hello IPs confiáveis permite que você tooskip Azure multi-Factor Authentication para sessões do Windows provenientes de IPs específicos.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="9e1cf-121">Por exemplo, se os funcionários usarem o aplicativo hello no office hello e em casa, você pode decidir que você não quer seus telefones liguem para o Azure multi-Factor Authentication e ao office hello.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="9e1cf-122">Para isso, você deve especificar a sub-rede de escritório hello como entrada de IPs confiáveis.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="9e1cf-123">Clique em **Adicionar...**</span><span class="sxs-lookup"><span data-stu-id="9e1cf-123">Click **Add…**</span></span>
8. <span data-ttu-id="9e1cf-124">Selecione **IP único** se você gostaria que tooskip um único endereço IP.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="9e1cf-125">Selecione **intervalo IP** se você gostaria que tooskip todo um intervalo IP.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="9e1cf-126">Exemplo 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="9e1cf-127">Selecione **sub-rede** se você gostaria que toospecify um intervalo de IPs usando a notação de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="9e1cf-128">Insira o IP inicial da sub-rede hello e escolha a máscara de rede apropriada da lista suspensa de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="9e1cf-129">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e1cf-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e1cf-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e1cf-130">Next steps</span></span>

- [<span data-ttu-id="9e1cf-131">Configure os dispositivos de VPN de terceiros para servidor Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9e1cf-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="9e1cf-132">Aumentar sua infraestrutura de autenticação existente com hello extensão NPS para o Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9e1cf-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
