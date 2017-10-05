---
title: "Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure | Microsoft Docs"
description: "Como configurar seu aplicativo de serviço de nuvem do Azure para permitir conexões de área de trabalho remota"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="0bb48-103">Habilitar a conexão de Área de Trabalho Remota para uma função nos Serviços de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb48-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bb48-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb48-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="0bb48-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb48-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="0bb48-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bb48-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="0bb48-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0bb48-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="0bb48-108">A área de trabalho remota permite que você acesse a área de trabalho de uma função em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb48-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="0bb48-109">Você pode usar a conexão da área de trabalho remota para solucionar e diagnosticar problemas com seu aplicativo durante a execução.</span><span class="sxs-lookup"><span data-stu-id="0bb48-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="0bb48-110">Você pode habilitar uma conexão de Área de Trabalho Remota em sua função durante o desenvolvimento, incluindo os módulos de Área de Trabalho Remota em sua definição de serviço, ou você pode optar por habilitar a Área de Trabalho Remota por meio da Extensão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="0bb48-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="0bb48-111">A abordagem preferida é usar a extensão de Área de Trabalho Remota, pois você poderá habilitar a Área de Trabalho Remota mesmo depois que o aplicativo for implantado, sem precisar reimplantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0bb48-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="0bb48-112">Configurar a Área de Trabalho Remota do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0bb48-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="0bb48-113">O Portal do Azure usa a abordagem de Extensão da Área de Trabalho Remota para que você possa habilitar a Área de Trabalho Remota, mesmo depois que o aplicativo for implantado.</span><span class="sxs-lookup"><span data-stu-id="0bb48-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="0bb48-114">A folha **Área de Trabalho Remota** de seu Serviço de Nuvem permite habilitar a Área de Trabalho Remota, alterar a conta do administrador local usada para conexão às máquinas virtuais, o certificado usado na autenticação e definir a data de validade.</span><span class="sxs-lookup"><span data-stu-id="0bb48-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="0bb48-115">Clique em **Serviços de Nuvem**, no nome do serviço de nuvem e depois em **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="0bb48-117">Escolha se você quer habilitar a Área de Trabalho Remota para uma função individual ou para todas as funções, e altere o valor do alternador para **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="0bb48-118">Preencha os campos obrigatórios de nome de usuário, senha, expiração e certificado.</span><span class="sxs-lookup"><span data-stu-id="0bb48-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="0bb48-120">Todas as instâncias de função serão reiniciadas quando você ativa área de trabalho remota pela primeira vez e clica em OK (marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="0bb48-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="0bb48-121">Para evitar a reinicialização, o certificado usado para criptografar a senha deve estar instalado na função.</span><span class="sxs-lookup"><span data-stu-id="0bb48-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="0bb48-122">Para evitar uma reinicialização, [carregue um certificado para o serviço de nuvem](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) e retorne a esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0bb48-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="0bb48-123">Em **Funções**, selecione a função que você deseja atualizar ou selecione **Tudo** para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="0bb48-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="0bb48-124">Ao concluir as atualizações da configuração, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="0bb48-125">Levará alguns minutos para que as instâncias da função estejam prontas para receber conexões.</span><span class="sxs-lookup"><span data-stu-id="0bb48-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="0bb48-126">Remoto em instâncias de função</span><span class="sxs-lookup"><span data-stu-id="0bb48-126">Remote into role instances</span></span>
<span data-ttu-id="0bb48-127">Após a habilitação da Área de Trabalho Remota nas funções, você poderá iniciar uma conexão diretamente do Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="0bb48-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="0bb48-128">Clique em **Instâncias** para abrir a folha **Instâncias**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="0bb48-129">Selecione uma instância de função com a área de trabalho remota configurada.</span><span class="sxs-lookup"><span data-stu-id="0bb48-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="0bb48-130">Clique em **Conectar** para baixar um arquivo RDP para a instância da função.</span><span class="sxs-lookup"><span data-stu-id="0bb48-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Área de trabalho remota dos serviços de nuvem](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="0bb48-132">Clique em **Abrir** e em **Conectar** para iniciar a conexão de Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="0bb48-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="0bb48-133">Se o serviço de nuvem estiver atrás de um NSG, talvez você precisará criar regras que permitam tráfego nas portas **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="0bb48-134">A Área de Trabalho Remota usa a porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="0bb48-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="0bb48-135">Instâncias de serviço de nuvem têm a carga balanceada, de modo que você não pode controlar diretamente a escolha da instância à qual se conectar.</span><span class="sxs-lookup"><span data-stu-id="0bb48-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="0bb48-136">Os agentes *RemoteForwarder* e *RemoteAccess* gerenciam o tráfego RDP e permitem que o cliente envie um cookie RDP e especifique uma instância individual à qual se conectar.</span><span class="sxs-lookup"><span data-stu-id="0bb48-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="0bb48-137">Os agentes *RemoteForwarder* e *RemoteAccess* exigem que essa porta **20000*** esteja aberta, a qual poderá ser bloqueada se você tiver um NSG.</span><span class="sxs-lookup"><span data-stu-id="0bb48-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0bb48-138">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0bb48-138">Additional resources</span></span>

<span data-ttu-id="0bb48-139">[Como configurar os Serviços de Nuvem](cloud-services-how-to-configure.md)
[Perguntas frequentes sobre os serviços de nuvem — Área de Trabalho Remota](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0bb48-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
