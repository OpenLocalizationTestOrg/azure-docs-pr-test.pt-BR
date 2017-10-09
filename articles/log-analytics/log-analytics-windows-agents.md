---
title: "aaaConnect Windows computadores tooAzure análise de Log | Microsoft Docs"
description: "Este artigo mostra computadores com Windows hello etapas tooconnect Olá no seu toohello de infraestrutura no local de serviço de análise de Log usando uma versão personalizada do hello agente de monitoramento da Microsoft (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="f37ad-103">Conecte-se o serviço de análise de logs do Windows computadores toohello no Azure</span><span class="sxs-lookup"><span data-stu-id="f37ad-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="f37ad-104">Este artigo mostra etapas Olá tooconnect computadores com Windows em seus espaços de trabalho de tooOMS de infraestrutura local usando uma versão personalizada do hello agente de monitoramento da Microsoft (MMA).</span><span class="sxs-lookup"><span data-stu-id="f37ad-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="f37ad-105">Você precisa tooinstall e conectar agentes para todos os computadores de saudação que você deseja tooonboard para poderem serviço de análise de Log toosend dados toohello e tooview e agir sobre dados.</span><span class="sxs-lookup"><span data-stu-id="f37ad-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="f37ad-106">Cada agente pode relatar toomultiple espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f37ad-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="f37ad-107">Você pode instalar agentes usando a Instalação, a linha de comando ou com o DSC (Configuração de Estado Desejado) na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f37ad-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="f37ad-108">Para máquinas virtuais em execução no Azure, você poderá simplificar a instalação usando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f37ad-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="f37ad-109">Em computadores com conectividade com a Internet, o agente de saudação usa Olá conexão toohello Internet toosend dados tooOMS.</span><span class="sxs-lookup"><span data-stu-id="f37ad-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="f37ad-110">Para computadores que não tem conectividade com a Internet, você pode usar um proxy ou Olá [OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f37ad-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="f37ad-111">Conectar-se a sua tooOMS de computadores do Windows é simples em três etapas simples:</span><span class="sxs-lookup"><span data-stu-id="f37ad-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="f37ad-112">Baixar o arquivo de configuração do agente de saudação do portal do OMS Olá</span><span class="sxs-lookup"><span data-stu-id="f37ad-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="f37ad-113">Instalar o agente de saudação usando o método hello escolhido</span><span class="sxs-lookup"><span data-stu-id="f37ad-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="f37ad-114">Configurar o agente de saudação ou adicionar espaços de trabalho adicionais, se necessário</span><span class="sxs-lookup"><span data-stu-id="f37ad-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="f37ad-115">Hello diagrama a seguir mostra a relação Olá entre computadores com Windows e o OMS depois que você instalou e configurou os agentes.</span><span class="sxs-lookup"><span data-stu-id="f37ad-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="f37ad-117">Se suas políticas de segurança de TI não permitir que os computadores em sua toohello tooconnect de rede da Internet, você pode configurar seu toohello de tooconnect computadores Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="f37ad-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="f37ad-118">Para obter mais informações e etapas sobre como tooconfigure toocommunicate seus servidores através de um serviço OMS do Gateway do OMS toohello, consulte [conectar computadores tooOMS usando Olá OMS Gateway](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f37ad-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="f37ad-119">Requisitos do sistema e a configuração necessária</span><span class="sxs-lookup"><span data-stu-id="f37ad-119">System requirements and required configuration</span></span>
<span data-ttu-id="f37ad-120">Antes de instalar ou implantar agentes, examine Olá tooensure detalhes que você atende aos requisitos de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="f37ad-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="f37ad-121">Você só pode instalar Olá OMS MMA em computadores que executam o Windows Server 2008 SP 1 ou posterior ou Windows 7 SP1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f37ad-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="f37ad-122">É necessária uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f37ad-122">You need an Azure subscription.</span></span>  <span data-ttu-id="f37ad-123">Para saber mais, confira [Introdução ao Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f37ad-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="f37ad-124">Cada computador do Windows deve ser capaz de tooconnect toohello Internet usando HTTPS ou toohello Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="f37ad-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="f37ad-125">Essa conexão pode ser direta por meio de um proxy, ou Olá Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="f37ad-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="f37ad-126">Você pode instalar Olá OMS MMA em máquinas virtuais, servidores e computadores autônomos.</span><span class="sxs-lookup"><span data-stu-id="f37ad-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="f37ad-127">Se você quiser tooconnect tooOMS de máquinas virtuais hospedadas pelo Azure, consulte [tooLog de máquinas virtuais do Azure conectar análise](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f37ad-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="f37ad-128">Agente de saudação precisa toouse a porta TCP 443 para vários recursos.</span><span class="sxs-lookup"><span data-stu-id="f37ad-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="f37ad-129">Rede</span><span class="sxs-lookup"><span data-stu-id="f37ad-129">Network</span></span>

<span data-ttu-id="f37ad-130">Para Windows agentes tooconnect tooand registrar no serviço do OMS hello, eles devem ter acesso de recursos toonetwork, incluindo URLs de domínio e os números de porta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="f37ad-131">Para servidores proxy, você precisa tooensure que Olá recursos configurados nas configurações do agente de servidor de proxy apropriados.</span><span class="sxs-lookup"><span data-stu-id="f37ad-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="f37ad-132">Para firewalls que restringem o acesso toohello da Internet, você ou sua rede engenheiros necessário tooconfigure tooOMS de acesso de toopermit seu firewall.</span><span class="sxs-lookup"><span data-stu-id="f37ad-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="f37ad-133">Nenhuma ação é necessária nas configurações do agente.</span><span class="sxs-lookup"><span data-stu-id="f37ad-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="f37ad-134">Olá, a tabela a seguir mostra os recursos necessários para comunicação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="f37ad-135">Alguns dos Olá recursos a seguir mencionam Insights operacionais, que era o nome anterior para análise de Log.</span><span class="sxs-lookup"><span data-stu-id="f37ad-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="f37ad-136">Recurso de agente</span><span class="sxs-lookup"><span data-stu-id="f37ad-136">Agent Resource</span></span> | <span data-ttu-id="f37ad-137">Portas</span><span class="sxs-lookup"><span data-stu-id="f37ad-137">Ports</span></span> | <span data-ttu-id="f37ad-138">Ignorar a inspeção de HTTPS</span><span class="sxs-lookup"><span data-stu-id="f37ad-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="f37ad-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f37ad-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="f37ad-140">443</span><span class="sxs-lookup"><span data-stu-id="f37ad-140">443</span></span> | <span data-ttu-id="f37ad-141">Sim</span><span class="sxs-lookup"><span data-stu-id="f37ad-141">Yes</span></span> |
| <span data-ttu-id="f37ad-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f37ad-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="f37ad-143">443</span><span class="sxs-lookup"><span data-stu-id="f37ad-143">443</span></span> | <span data-ttu-id="f37ad-144">Sim</span><span class="sxs-lookup"><span data-stu-id="f37ad-144">Yes</span></span> |
| <span data-ttu-id="f37ad-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f37ad-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="f37ad-146">443</span><span class="sxs-lookup"><span data-stu-id="f37ad-146">443</span></span> | <span data-ttu-id="f37ad-147">Sim</span><span class="sxs-lookup"><span data-stu-id="f37ad-147">Yes</span></span> |
| <span data-ttu-id="f37ad-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="f37ad-148">*.azure-automation.net</span></span> | <span data-ttu-id="f37ad-149">443</span><span class="sxs-lookup"><span data-stu-id="f37ad-149">443</span></span> | <span data-ttu-id="f37ad-150">Sim</span><span class="sxs-lookup"><span data-stu-id="f37ad-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="f37ad-151">Baixar o arquivo de configuração do agente de saudação do OMS</span><span class="sxs-lookup"><span data-stu-id="f37ad-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="f37ad-152">No portal do OMS hello, em Olá **visão geral** , clique em Olá **configurações** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="f37ad-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="f37ad-153">Clique em Olá **fontes conectadas** guia na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="f37ad-154">![Guia Fontes Conectadas](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="f37ad-155">Clique em **servidores Windows** e, em seguida, clique em **baixar o agente do Windows** arquivo de instalação aplicável tooyour computador processador tipo toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="f37ad-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="f37ad-156">Em saudação à direita do **ID do espaço de trabalho**, clique Olá ícone para copiar e colar Olá ID no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="f37ad-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="f37ad-157">Em saudação à direita do **chave primária**, clique Olá ícone para copiar e colar chave Olá no bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="f37ad-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="f37ad-158">Instalar agente hello usando a instalação</span><span class="sxs-lookup"><span data-stu-id="f37ad-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="f37ad-159">Execute o agente de saudação de tooinstall de instalação em um computador que você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="f37ad-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="f37ad-160">Na página de boas-vindas hello, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="f37ad-161">Na página de termos de licença hello, leia Olá da licença e, em seguida, clique em **concordo**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="f37ad-162">Na página de pasta de destino hello, alterar ou mantenha a pasta de instalação padrão hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="f37ad-163">Na página de opções de instalação do agente Olá, você pode escolher tooconnect Olá agente tooAzure análise de Log (OMS), Operations Manager, ou você pode deixar as escolhas de saudação em branco se desejar usar o agente de saudação tooconfigure mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f37ad-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="f37ad-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-164">Click **Next**.</span></span>   
    - <span data-ttu-id="f37ad-165">Se você escolheu tooconnect tooAzure Log Analytics (OMS), cole Olá **ID do espaço de trabalho** e **chave do espaço de trabalho (chave primária)** que você copiou no bloco de notas no procedimento anterior do hello e, em seguida, clique em  **Próxima**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="f37ad-166">![colar ID de Espaço de Trabalho e a Chave Primária](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="f37ad-167">Se você escolheu tooconnect tooOperations Manager, digite Olá **nome do grupo de gerenciamento**, **Management Server** nome, e **porta do servidor de gerenciamento**e, em seguida, clique em **Próxima**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="f37ad-168">Na página de conta de Ação agente hello, escolha a conta do sistema Local hello ou uma conta de domínio local e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="f37ad-169">![configuração do grupo de gerenciamento ](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![conta de ação de agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="f37ad-170">Na página de tooInstall pronto do hello, revise suas escolhas e clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="f37ad-171">Em Olá configuração concluída com êxito, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="f37ad-172">Ao concluir, Olá **Microsoft Monitoring Agent** aparece na **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="f37ad-173">Você pode examinar sua configuração existe e verificar que o agente de saudação é conectado tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="f37ad-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="f37ad-174">Quando conectados tooOMS, Olá agent exibirá uma mensagem dizendo: **Olá Microsoft Monitoring Agent tiver conectado com êxito o serviço do Microsoft Operations Management Suite toohello.**</span><span class="sxs-lookup"><span data-stu-id="f37ad-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="f37ad-175">Definir configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="f37ad-175">Configure proxy settings</span></span>

<span data-ttu-id="f37ad-176">Você pode usar o hello seguindo as configurações de proxy do procedimento tooconfigure para Olá Microsoft Monitoring Agent usando o painel de controle.</span><span class="sxs-lookup"><span data-stu-id="f37ad-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="f37ad-177">Você precisa toouse este procedimento para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="f37ad-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="f37ad-178">Se você tiver vários servidores que você precisa tooconfigure, talvez seja mais fácil toouse tooautomate um script esse processo.</span><span class="sxs-lookup"><span data-stu-id="f37ad-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="f37ad-179">Nesse caso, consulte o procedimento a seguir Olá [tooconfigure as configurações de proxy para Olá Microsoft Monitoring Agent usando um script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="f37ad-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="f37ad-180">configurações de proxy de tooconfigure para Olá Microsoft Monitoring Agent usando o painel de controle</span><span class="sxs-lookup"><span data-stu-id="f37ad-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="f37ad-181">Abra o **Painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="f37ad-182">Abra o **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="f37ad-183">Clique em Olá **as configurações de Proxy** guia.</span><span class="sxs-lookup"><span data-stu-id="f37ad-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="f37ad-184">![guia Configurações de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="f37ad-185">Selecione **usar um servidor proxy** e digite a URL de saudação e número da porta, se necessário, semelhante toohello exemplo mostrado.</span><span class="sxs-lookup"><span data-stu-id="f37ad-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="f37ad-186">Se o servidor proxy requer autenticação, digite Olá username e password tooaccess Olá servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="f37ad-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="f37ad-187">Verifique se tooOMS de conectividade do agente</span><span class="sxs-lookup"><span data-stu-id="f37ad-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="f37ad-188">Você pode facilmente verificar se os agentes estão se comunicando com o OMS usando Olá procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="f37ad-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="f37ad-189">No computador de saudação com o agente do Windows hello, abra o painel de controle.</span><span class="sxs-lookup"><span data-stu-id="f37ad-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="f37ad-190">Abra o Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="f37ad-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="f37ad-191">Clique em Guia do hello Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="f37ad-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="f37ad-192">Na coluna de Status hello, você verá que o agente Olá conectado com êxito de serviço do Operations Management Suite toohello.</span><span class="sxs-lookup"><span data-stu-id="f37ad-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="f37ad-194">configurações de proxy de tooconfigure para Olá Microsoft Monitoring Agent usando um script</span><span class="sxs-lookup"><span data-stu-id="f37ad-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="f37ad-195">Copie Olá seguinte exemplo, atualizá-lo com o ambiente de tooyour específicas de informações, salve-o com uma extensão de nome de arquivo PS1 e, em seguida, execute o script de saudação em cada computador que se conecta diretamente de serviço do OMS toohello.</span><span class="sxs-lookup"><span data-stu-id="f37ad-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="f37ad-196">Instalar o agente de Olá usando a linha de comando de saudação</span><span class="sxs-lookup"><span data-stu-id="f37ad-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="f37ad-197">Modifique e, em seguida, use Olá após o agente de saudação tooinstall de exemplo usando a linha de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="f37ad-198">exemplo Hello executa uma instalação completamente silenciosa.</span><span class="sxs-lookup"><span data-stu-id="f37ad-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="f37ad-199">Se você quiser tooupgrade um agente, você precisa toouse Olá análise de Log do API de script.</span><span class="sxs-lookup"><span data-stu-id="f37ad-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="f37ad-200">Consulte Olá tooupgrade próximo da seção um agente.</span><span class="sxs-lookup"><span data-stu-id="f37ad-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="f37ad-201">Agente de saudação usa IExpress como seu Self-extractor usando Olá `/c` comando.</span><span class="sxs-lookup"><span data-stu-id="f37ad-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="f37ad-202">Você pode ver as opções de linha de comando de saudação em [de linha de comando para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e, em seguida, atualização Olá exemplo toosuit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f37ad-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="f37ad-203">Opções específicas do MMA</span><span class="sxs-lookup"><span data-stu-id="f37ad-203">MMA-specific options</span></span>                   |<span data-ttu-id="f37ad-204">Observações</span><span class="sxs-lookup"><span data-stu-id="f37ad-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="f37ad-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="f37ad-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="f37ad-206">1 = Configurar Olá agente tooreport tooa área de trabalho</span><span class="sxs-lookup"><span data-stu-id="f37ad-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="f37ad-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="f37ad-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="f37ad-208">Id do espaço de trabalho (guid) para Olá tooadd de espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="f37ad-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="f37ad-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="f37ad-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="f37ad-210">Tooinitially usado chave do espaço de trabalho autenticar com o espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="f37ad-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="f37ad-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="f37ad-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="f37ad-212">Especifique o ambiente de nuvem Olá onde se encontra o espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="f37ad-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="f37ad-213">0 = nuvem comercial do Azure (padrão)</span><span class="sxs-lookup"><span data-stu-id="f37ad-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="f37ad-214">1 = Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="f37ad-214">1 = Azure Government</span></span> |
|<span data-ttu-id="f37ad-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="f37ad-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="f37ad-216">URI para Olá proxy toouse</span><span class="sxs-lookup"><span data-stu-id="f37ad-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="f37ad-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="f37ad-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="f37ad-218">Nome de usuário tooaccess um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="f37ad-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="f37ad-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="f37ad-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="f37ad-220">Senha tooaccess um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="f37ad-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="f37ad-221">limite de tamanho de linha de comando de saudação de atingir do tooavoid de IExpress, instalar o agente de saudação com nenhum espaço de trabalho configurado e, em seguida, usar uma configuração de tooset de script para o espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="f37ad-222">Se você receber um `Command line option syntax error.` ao usar o hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parâmetro, você pode usar o hello solução alternativa a seguir:</span><span class="sxs-lookup"><span data-stu-id="f37ad-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="f37ad-223">Adicionar um espaço de trabalho usando um script</span><span class="sxs-lookup"><span data-stu-id="f37ad-223">Add a workspace using a script</span></span>
<span data-ttu-id="f37ad-224">Adicione um espaço de trabalho com API de script do agente de análise de Log de Olá Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f37ad-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="f37ad-225">tooadd um espaço de trabalho no Azure do governo dos EUA, use Olá exemplo de script a seguir:</span><span class="sxs-lookup"><span data-stu-id="f37ad-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="f37ad-226">Se você usou Olá linha de comando ou script anteriormente tooinstall ou configurar o agente Olá, `EnableAzureOperationalInsights` foi substituído pelo `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="f37ad-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="f37ad-227">Instalar o agente de saudação usando DSC na automação do Azure</span><span class="sxs-lookup"><span data-stu-id="f37ad-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="f37ad-228">Você pode usar o hello após o agente de saudação do script exemplo tooinstall usando DSC na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f37ad-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f37ad-229">exemplo Hello instala Olá agente de 64 bits, identificado por Olá `URI` valor.</span><span class="sxs-lookup"><span data-stu-id="f37ad-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="f37ad-230">Você também pode usar a versão de 32 bits hello, substituindo o valor URI de saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="f37ad-231">Olá URIs para ambas as versões são:</span><span class="sxs-lookup"><span data-stu-id="f37ad-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="f37ad-232">Agente do Windows de 64 bits – https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="f37ad-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="f37ad-233">Agente do Windows de 32 bits – https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="f37ad-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="f37ad-234">Este exemplo de procedimento e de script não atualizará um agente existente.</span><span class="sxs-lookup"><span data-stu-id="f37ad-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="f37ad-235">Importar Olá xPSDesiredStateConfiguration módulo de DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f37ad-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="f37ad-236">Crie ativos de variável da Automação do Azure para *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="f37ad-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="f37ad-237">Definir *OPSINSIGHTS_WS_ID* tooyour ID de espaço de trabalho de análise de logs do OMS e defina *OPSINSIGHTS_WS_KEY* toohello a chave primária de seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f37ad-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="f37ad-238">Use Olá seguinte script e salve-o como MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="f37ad-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="f37ad-239">Modifique e, em seguida, use Olá após o agente de saudação tooinstall de exemplo usando a DSC na automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f37ad-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f37ad-240">Importe MMAgent.ps1 para automação do Azure usando a interface de automação do Azure hello ou cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f37ad-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="f37ad-241">Atribua uma configuração de toohello do nó.</span><span class="sxs-lookup"><span data-stu-id="f37ad-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="f37ad-242">Dentro de 15 minutos, nó Olá verifica sua configuração e Olá MMA é enviada por push toohello nó.</span><span class="sxs-lookup"><span data-stu-id="f37ad-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="f37ad-243">Obter o valor de ProductId mais recente Olá</span><span class="sxs-lookup"><span data-stu-id="f37ad-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="f37ad-244">Olá `ProductId value` Olá MMAgent.ps1 script é exclusivo tooeach versão do agente.</span><span class="sxs-lookup"><span data-stu-id="f37ad-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="f37ad-245">Quando uma versão atualizada de cada agente é publicada, Olá ProductId valor é alterado.</span><span class="sxs-lookup"><span data-stu-id="f37ad-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="f37ad-246">Portanto, quando Olá ProductId alterado de saudação futura, você pode descobrir a versão do agente de hello usando um script simples.</span><span class="sxs-lookup"><span data-stu-id="f37ad-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="f37ad-247">Depois que você tiver Olá versão do agente mais recente instalado em um servidor de teste, você pode usar o hello seguinte valor de ProductId do script tooget Olá instalado.</span><span class="sxs-lookup"><span data-stu-id="f37ad-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="f37ad-248">Usando o valor de ProductId hello mais recente, você pode atualizar o valor de saudação em Olá MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="f37ad-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="f37ad-249">Configurar um agente manualmente ou adicionar outros espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="f37ad-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="f37ad-250">Se você instalou agentes, mas não os configurou ou se desejar que os espaços de trabalho do agente tooreport toomultiple hello, você pode usar o hello informações tooenable um agente a segui-lo ou reconfigurá-lo.</span><span class="sxs-lookup"><span data-stu-id="f37ad-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="f37ad-251">Depois que você tiver configurado o agente de hello, ele registrará o serviço do agente hello e obterá informações de configuração necessárias e os pacotes de gerenciamento que contêm informações de solução.</span><span class="sxs-lookup"><span data-stu-id="f37ad-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="f37ad-252">Depois de instalar Olá Microsoft Monitoring Agent, abra **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f37ad-253">Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **Azure Log Analytics (OMS)** guia.</span><span class="sxs-lookup"><span data-stu-id="f37ad-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="f37ad-254">Clique em **adicionar** tooopen Olá **adicionar um espaço de trabalho de análise de Log** caixa.</span><span class="sxs-lookup"><span data-stu-id="f37ad-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="f37ad-255">Saudação de colar **ID do espaço de trabalho** e **chave do espaço de trabalho (chave primária)** que você copiou no bloco de notas no procedimento anterior para espaço de trabalho de saudação que você deseja tooadd e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="f37ad-256">![configurar o Azure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="f37ad-257">Depois que dados são coletados de computadores monitorados por agente Olá, número de saudação dos computadores monitorados pelo OMS será exibido no portal do OMS Olá em Olá **fontes conectadas** guia **configurações** como  **Servidores conectados**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="f37ad-258">toodisable um agente</span><span class="sxs-lookup"><span data-stu-id="f37ad-258">toodisable an agent</span></span>
1. <span data-ttu-id="f37ad-259">Depois de instalar o agente hello, abra **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f37ad-260">Abra o Microsoft Monitoring Agent e clique em Olá **Azure Log Analytics (OMS)** guia.</span><span class="sxs-lookup"><span data-stu-id="f37ad-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="f37ad-261">Selecione um espaço de trabalho e clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="f37ad-262">Repita essa etapa para todos os outros espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f37ad-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f37ad-263">Opcionalmente, configure o grupo de gerenciamento do agentes tooreport tooan do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f37ad-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="f37ad-264">Se você usar o Operations Manager em sua infraestrutura de TI, você também pode usar o agente MMA hello como um agente do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f37ad-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f37ad-265">grupo de gerenciamento tooconfigure MMA agentes tooreport tooan do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f37ad-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="f37ad-266">No computador de saudação onde Olá é instalado, abra **painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="f37ad-267">Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **Operations Manager** guia.</span><span class="sxs-lookup"><span data-stu-id="f37ad-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="f37ad-268">![Guia Microsoft Monitoring Agent Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="f37ad-269">Se seus servidores do Operations Manager tiverem integração com o Active Directory, clique em **Atualizar automaticamente as atribuições de grupo de gerenciamento do AD DS**.</span><span class="sxs-lookup"><span data-stu-id="f37ad-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="f37ad-270">Clique em **adicionar** tooopen Olá **adicionar um grupo de gerenciamento** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f37ad-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="f37ad-271">![Adicionar um Grupo de Gerenciamento do Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="f37ad-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="f37ad-272">Em **nome do grupo de gerenciamento** caixa, digite o nome de saudação do seu grupo de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f37ad-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="f37ad-273">Em Olá **servidor de gerenciamento primário** caixa, digite o nome de computador de saudação do servidor de gerenciamento primário de saudação.</span><span class="sxs-lookup"><span data-stu-id="f37ad-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="f37ad-274">Em Olá **porta do servidor de gerenciamento** caixa tipo hello número da porta TCP.</span><span class="sxs-lookup"><span data-stu-id="f37ad-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="f37ad-275">Em **conta de Ação agente**, escolha a conta do sistema Local hello ou uma conta de domínio local.</span><span class="sxs-lookup"><span data-stu-id="f37ad-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="f37ad-276">Clique em **Okey** tooclose Olá **adicionar um grupo de gerenciamento** caixa de diálogo e clique **Okey** tooclose Olá **propriedades do agente de monitoramento Microsoft**caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f37ad-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f37ad-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f37ad-277">Next steps</span></span>

- <span data-ttu-id="f37ad-278">[Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.</span><span class="sxs-lookup"><span data-stu-id="f37ad-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
