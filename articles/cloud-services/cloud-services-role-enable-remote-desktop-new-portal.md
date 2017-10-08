---
title: "aaaEnable Conexão de área de trabalho remota para uma função nos serviços de nuvem do Azure | Microsoft Docs"
description: "Como tooconfigure do azure nuvem conexões de área de trabalho remota de tooallow aplicativo de serviço"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="21418-103">Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="21418-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21418-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="21418-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="21418-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="21418-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="21418-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21418-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="21418-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21418-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="21418-108">Área de trabalho remota permite que você tooaccess área de trabalho de saudação de uma função em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="21418-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="21418-109">Você pode usar um tootroubleshoot de conexão de área de trabalho remota e diagnosticar problemas com seu aplicativo enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="21418-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="21418-110">Você pode habilitar uma conexão de área de trabalho remota na sua função durante o desenvolvimento, incluindo módulos de área de trabalho remota de saudação em sua definição de serviço ou você pode escolher tooenable área de trabalho remota por meio de saudação extensão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="21418-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="21418-111">Olá abordagem preferencial é toouse Olá área de trabalho remota extensão como você pode habilitar área de trabalho remota, mesmo após a implantação do aplicativo hello sem ter que tooredeploy seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="21418-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="21418-112">Configurar área de trabalho remota a partir do hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="21418-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="21418-113">Olá portal do Azure usa o método de extensão da área de trabalho remota de saudação para que você possa habilitar a área de trabalho remota mesmo após a implantação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="21418-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="21418-114">Olá **área de trabalho remota** folha para seu serviço de nuvem permite que você tooenable área de trabalho remota, Olá alterar conta do administrador local usado tooconnect toohello VMs, certificado Olá usado na autenticação e defina Olá Data de expiração.</span><span class="sxs-lookup"><span data-stu-id="21418-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="21418-115">Clique em **serviços de nuvem**, clique em nome de Olá Olá do serviço de nuvem e, em seguida, clique em **área de trabalho remota**.</span><span class="sxs-lookup"><span data-stu-id="21418-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="21418-117">Escolha se você deseja tooenable área de trabalho remota para uma função individual ou para todas as funções e altere o valor de saudação do alternador Olá muito**habilitado**.</span><span class="sxs-lookup"><span data-stu-id="21418-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="21418-118">Preencha os campos de saudação necessárias para o nome de usuário, senha, expiração e certificado.</span><span class="sxs-lookup"><span data-stu-id="21418-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="21418-120">Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="21418-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="21418-121">tooprevent uma reinicialização, a senha de Olá Olá certificado tooencrypt usado deve ser instalado na função hello.</span><span class="sxs-lookup"><span data-stu-id="21418-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="21418-122">tooprevent uma reinicialização, [carregar um certificado para o serviço de nuvem Olá](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e, em seguida, retornar toothis caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="21418-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="21418-123">Em **funções**, selecione função hello desejado tooupdate ou selecione **todos os** para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="21418-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="21418-124">Ao concluir as atualizações da configuração, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="21418-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="21418-125">Levará alguns minutos antes que suas instâncias de função são conexões tooreceive pronto.</span><span class="sxs-lookup"><span data-stu-id="21418-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="21418-126">Remoto em instâncias de função</span><span class="sxs-lookup"><span data-stu-id="21418-126">Remote into role instances</span></span>
<span data-ttu-id="21418-127">Depois que a área de trabalho remota está habilitada em funções hello, você pode iniciar uma conexão diretamente da saudação Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="21418-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="21418-128">Clique em **instâncias** tooopen Olá **instâncias** folha.</span><span class="sxs-lookup"><span data-stu-id="21418-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="21418-129">Selecione uma instância de função com a área de trabalho remota configurada.</span><span class="sxs-lookup"><span data-stu-id="21418-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="21418-130">Clique em **conectar** toodownload uma RDP de arquivo para a instância de função hello.</span><span class="sxs-lookup"><span data-stu-id="21418-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="21418-132">Clique em **abrir** e **conectar** toostart Olá conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="21418-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="21418-133">Se seu serviço de nuvem estiver atrás de um NSG, talvez seja necessário toocreate regras que permitam o tráfego em portas **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="21418-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="21418-134">A Área de Trabalho Remota usa a porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="21418-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="21418-135">Instâncias de serviço de nuvem têm a carga balanceada, portanto diretamente, você não pode controlar quais tooconnect de instância para.</span><span class="sxs-lookup"><span data-stu-id="21418-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="21418-136">Olá *RemoteForwarder* e *RemoteAccess* agentes gerenciar o tráfego RDP e permitir Olá cliente toosend um cookie RDP e especifique um tooconnect instância individual para.</span><span class="sxs-lookup"><span data-stu-id="21418-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="21418-137">Olá *RemoteForwarder* e *RemoteAccess* agentes exigem essa porta **20000*** aberto, que pode ser bloqueado se você tiver um NSG.</span><span class="sxs-lookup"><span data-stu-id="21418-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="21418-138">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="21418-138">Additional resources</span></span>

<span data-ttu-id="21418-139">[Como tooConfigure serviços de nuvem](cloud-services-how-to-configure.md)
[serviços em nuvem perguntas Frequentes – área de trabalho remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="21418-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
