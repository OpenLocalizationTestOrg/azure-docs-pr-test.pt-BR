---
title: "Monitorar hubs de superfície com o Azure Log Analytics | Microsoft Docs"
description: "Use a solução Surface Hubs para controlar a integridade dos seus Hubs de superfície e compreender como eles estão sendo usados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="a6cf2-103">Monitorar Surface Hubs com o Log Analytics para acompanhar sua integridade</span><span class="sxs-lookup"><span data-stu-id="a6cf2-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Símbolo do Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="a6cf2-105">Este artigo descreve como você pode usar a solução Surface Hub no Log Analytics para monitorar dispositivos do Microsoft Surface Hubs com o Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="a6cf2-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="a6cf2-106">O Log Analytics o ajuda a controlar a integridade dos seus Surface Hubs além de compreender como eles estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="a6cf2-107">Cada Surface Hub tem o Microsoft Monitoring Agent instalado.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="a6cf2-108">É por meio do agente que você pode enviar dados do seu Surface Hub para o OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="a6cf2-109">Os arquivos de log são lidos a partir de seus Surface Hubs e são, em seguida, enviados para o serviço OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="a6cf2-110">Problemas como servidores offline, o calendário não está sincronizando, ou se a conta do dispositivo não puder fazer logon no Skype são mostrados no OMS no painel do Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="a6cf2-111">Ao usar os dados no painel, você pode identificar os dispositivos que não estão em execução ou que têm outros problemas e, potencialmente, aplicar correções para os problemas detectados.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="a6cf2-112">Instalando e configurando a solução</span><span class="sxs-lookup"><span data-stu-id="a6cf2-112">Installing and configuring the solution</span></span>
<span data-ttu-id="a6cf2-113">Use as informações a seguir para instalar e configurar a solução.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="a6cf2-114">Para gerenciar os Surface Hubs do Microsoft Operations Management Suite (OMS), você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a6cf2-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="a6cf2-115">Uma assinatura válida para o [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="a6cf2-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="a6cf2-116">Um nível de [assinatura do OMS](https://azure.microsoft.com/pricing/details/log-analytics/) que dará suporte ao número de dispositivos que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="a6cf2-117">Os preços do OMS variam dependendo de quantos dispositivos estão registrados e a quantidade de dados que ele processa.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="a6cf2-118">Convém levar isso em consideração ao planejar a distribuição do Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="a6cf2-119">Em seguida, você adicionará uma assinatura do OMS à sua assinatura do Microsoft Azure existente ou criará um novo espaço de trabalho diretamente através do portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="a6cf2-120">Instruções detalhadas para usar o método podem ser encontradas em [Introdução ao Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6cf2-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="a6cf2-121">Depois que a assinatura do OMS estiver configurada, há duas maneiras de registrar seus dispositivos do Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="a6cf2-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="a6cf2-122">Automaticamente por meio do Intune</span><span class="sxs-lookup"><span data-stu-id="a6cf2-122">Automatically through Intune</span></span>
* <span data-ttu-id="a6cf2-123">Manualmente por meio das **configurações** em seu dispositivo do Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="a6cf2-124">Configurar monitoramento</span><span class="sxs-lookup"><span data-stu-id="a6cf2-124">Set up monitoring</span></span>
<span data-ttu-id="a6cf2-125">Você pode monitorar a integridade e a atividade do seu Surface Hub usando o Log Analytics no OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="a6cf2-126">Você pode registrar o Surface Hub no OMS usando o Intune ou localmente usando as **Configurações** no Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="a6cf2-127">Conectar Surface Hubs ao OMS através do Intune</span><span class="sxs-lookup"><span data-stu-id="a6cf2-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="a6cf2-128">Será necessário o ID do espaço de trabalho e a chave do espaço de trabalho para o espaço de trabalho do OMS que gerenciará os Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="a6cf2-129">Você pode obtê-los no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="a6cf2-130">O Intune é um produto da Microsoft que permite que você gerencie centralmente as definições de configuração do OMS que são aplicadas a um ou mais dos seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="a6cf2-131">Siga estas etapas para configurar seus dispositivos por meio do Intune:</span><span class="sxs-lookup"><span data-stu-id="a6cf2-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="a6cf2-132">Entre no Intune.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="a6cf2-133">Navegue até **configurações** > **Fontes conectadas**.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="a6cf2-134">Criar ou editar uma política com base no modelo de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="a6cf2-135">Navegue até a seção OMS (Insights operacionais do Azure) da política e adicione o *ID do espaço de trabalho* e a *Chave do espaço de trabalho* à política.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="a6cf2-136">Salve a política.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-136">Save the policy.</span></span>
6. <span data-ttu-id="a6cf2-137">Associe a política ao grupo de dispositivos apropriado.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Política do Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="a6cf2-139">O Intune então sincroniza as configurações do OMS com os dispositivos no grupo de destino, registrando-os em seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="a6cf2-140">Conectar Surface Hubs ao OMS usando o aplicativo de configurações</span><span class="sxs-lookup"><span data-stu-id="a6cf2-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="a6cf2-141">Será necessário o ID do espaço de trabalho e a chave do espaço de trabalho para o espaço de trabalho do OMS que gerenciará os Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="a6cf2-142">Você pode obtê-los no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="a6cf2-143">Se você não usar o Intune para gerenciar seu ambiente, poderá registrar dispositivos manualmente por meio das **Configurações** em cada Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="a6cf2-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="a6cf2-144">No seu Surface Hub, abra **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="a6cf2-145">Insira as credenciais de administrador do dispositivo quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="a6cf2-146">Clique em **Este dispositivo** e, em **Monitoramento**, clique em **Configurar definições do OMS**.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="a6cf2-147">Selecione **Habilitar monitoramento**.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="a6cf2-148">Na caixa de diálogo Configurações do OMS, digite o **ID do espaço de trabalho** e digite a **Chave do espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="a6cf2-149">![configurações](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="a6cf2-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="a6cf2-150">Clique em **OK** para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="a6cf2-151">Uma confirmação será exibida informando se a configuração do OMS foi aplicada ou não com êxito ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="a6cf2-152">Se foi, uma mensagem será exibida informando que o agente foi conectado com êxito ao serviço do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="a6cf2-153">O dispositivo começará a enviar dados ao OMS, onde você pode exibi-lo e trabalhar com ele.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="a6cf2-154">Monitorar Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="a6cf2-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="a6cf2-155">Monitorar os Surface Hubs usando o OMS é muito parecido com o monitoramento de todos os outros dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="a6cf2-156">Entrar no portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="a6cf2-157">Navegue até o painel do pacote de solução do Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="a6cf2-158">A integridade do dispositivo é exibida.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-158">Your device's health is displayed.</span></span>

   ![Painel do Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="a6cf2-160">Você pode criar [alertas](log-analytics-alerts.md) com base em pesquisas de log existentes ou personalizadas.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="a6cf2-161">Ao usar os dados que o OMS coleta de seu Surface Hubs, você pode procurar problemas e alertar sobre as condições que definir para seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6cf2-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6cf2-162">Next steps</span></span>
* <span data-ttu-id="a6cf2-163">Use [Pesquisas de Log no Log Analytics](log-analytics-log-searches.md) para exibir dados detalhados do Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="a6cf2-164">Crie [alertas](log-analytics-alerts.md) para notificá-lo quando ocorrerem problemas com seus Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="a6cf2-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
