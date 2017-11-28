---
title: Conectar computadores Windows ao Azure Log Analytics | Microsoft Docs
description: "Este artigo mostra as etapas para conectar os computadores Windows em sua infraestrutura local ao serviço do Log Analytics usando uma versão personalizada do MMA (Microsoft Monitoring Agent)."
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="9ccd6-103">Conectar computadores Windows ao serviço do Log Analytics no Azure</span><span class="sxs-lookup"><span data-stu-id="9ccd6-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="9ccd6-104">Este artigo mostra as etapas para conectar os computadores Windows em sua infraestrutura local aos espaços de trabalho OMS usando uma versão personalizada do MMA (Microsoft Monitoring Agent).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="9ccd6-105">Você precisa instalar e conectar agentes para todos os computadores que deseja integrar de modo que eles enviem dados ao serviço do Log Analytics, bem como para exibir e agir com base nesses dados.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="9ccd6-106">Cada agente pode relatar a vários espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="9ccd6-107">Você pode instalar agentes usando a Instalação, a linha de comando ou com o DSC (Configuração de Estado Desejado) na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="9ccd6-108">Para máquinas virtuais em execução no Azure, você poderá simplificar a instalação usando a [extensão da máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="9ccd6-109">Em computadores com conectividade com a Internet, o agente usa a conexão com a Internet para enviar dados ao OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="9ccd6-110">Para computadores que não têm conectividade com a Internet, você pode usar um proxy ou o [Gateway OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="9ccd6-111">É muito simples conectar seus computadores Windows ao OMS usando três etapas simples:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="9ccd6-112">Baixar o arquivo de instalação do agente no Portal do OMS</span><span class="sxs-lookup"><span data-stu-id="9ccd6-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="9ccd6-113">Instalar o agente usando o método que você preferir</span><span class="sxs-lookup"><span data-stu-id="9ccd6-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="9ccd6-114">Configurar o agente ou adicionar outros espaços de trabalho, se necessário</span><span class="sxs-lookup"><span data-stu-id="9ccd6-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="9ccd6-115">O diagrama a seguir mostra a relação entre seus computadores Windows e o OMS depois de ter instalado e configurado os agentes.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="9ccd6-117">Se suas políticas de segurança de TI não permitirem que os computadores em sua rede se conectem à Internet, você poderá configurá-los para conectarem-se ao Gateway do OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="9ccd6-118">Para obter mais informações e etapas sobre como configurar seus servidores para comunicarem-se por meio de um Gateway do OMS com o serviço do OMS, consulte [Conectar computadores ao OMS usando o Gateway do OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="9ccd6-119">Requisitos do sistema e a configuração necessária</span><span class="sxs-lookup"><span data-stu-id="9ccd6-119">System requirements and required configuration</span></span>
<span data-ttu-id="9ccd6-120">Antes de instalar ou implantar agentes, examine os detalhes a seguir para verificar se você atende aos requisitos.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="9ccd6-121">Só é possível instalar o MMA do OMS em computadores que executam o Windows Server 2008 SP 1 ou posterior ou o Windows 7 SP1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="9ccd6-122">É necessária uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-122">You need an Azure subscription.</span></span>  <span data-ttu-id="9ccd6-123">Para saber mais, confira [Introdução ao Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="9ccd6-124">Todo computador do Windows deve ser capaz de se conectar à Internet usando HTTPS ou ao Gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="9ccd6-125">Essa conexão pode ser direta, por meio de um proxy ou pelo Gateway OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="9ccd6-126">Você pode instalar o MMA do OMS em computadores autônomos, servidores e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="9ccd6-127">Se você deseja se conectar a máquinas virtuais hospedadas no Azure ao OMS, consulte [Conectar as Máquinas Virtuais do Azure ao Log Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="9ccd6-128">O agente deve usar a porta TCP 443 para vários recursos.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="9ccd6-129">Rede</span><span class="sxs-lookup"><span data-stu-id="9ccd6-129">Network</span></span>

<span data-ttu-id="9ccd6-130">Para agentes do Windows conectarem-se e registrarem-se no serviço OMS, eles devem ter acesso aos recursos de rede, incluindo os números de porta e as URLs de domínio.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="9ccd6-131">Para servidores proxy, você precisa garantir que os recursos do servidor proxy apropriados estejam configurados nas configurações do agente.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="9ccd6-132">Para firewalls que restringem o acesso à Internet, você ou seus engenheiros de rede precisam configurar o firewall para permitir acesso ao OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="9ccd6-133">Nenhuma ação é necessária nas configurações do agente.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="9ccd6-134">A tabela a seguir mostra os recursos necessários para comunicação.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="9ccd6-135">Alguns dos recursos a seguir mencionam os Insights Operacionais, que era o nome anterior do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="9ccd6-136">Recurso de agente</span><span class="sxs-lookup"><span data-stu-id="9ccd6-136">Agent Resource</span></span> | <span data-ttu-id="9ccd6-137">Portas</span><span class="sxs-lookup"><span data-stu-id="9ccd6-137">Ports</span></span> | <span data-ttu-id="9ccd6-138">Ignorar a inspeção de HTTPS</span><span class="sxs-lookup"><span data-stu-id="9ccd6-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="9ccd6-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9ccd6-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="9ccd6-140">443</span><span class="sxs-lookup"><span data-stu-id="9ccd6-140">443</span></span> | <span data-ttu-id="9ccd6-141">Sim</span><span class="sxs-lookup"><span data-stu-id="9ccd6-141">Yes</span></span> |
| <span data-ttu-id="9ccd6-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="9ccd6-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="9ccd6-143">443</span><span class="sxs-lookup"><span data-stu-id="9ccd6-143">443</span></span> | <span data-ttu-id="9ccd6-144">Sim</span><span class="sxs-lookup"><span data-stu-id="9ccd6-144">Yes</span></span> |
| <span data-ttu-id="9ccd6-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9ccd6-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="9ccd6-146">443</span><span class="sxs-lookup"><span data-stu-id="9ccd6-146">443</span></span> | <span data-ttu-id="9ccd6-147">Sim</span><span class="sxs-lookup"><span data-stu-id="9ccd6-147">Yes</span></span> |
| <span data-ttu-id="9ccd6-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="9ccd6-148">*.azure-automation.net</span></span> | <span data-ttu-id="9ccd6-149">443</span><span class="sxs-lookup"><span data-stu-id="9ccd6-149">443</span></span> | <span data-ttu-id="9ccd6-150">Sim</span><span class="sxs-lookup"><span data-stu-id="9ccd6-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="9ccd6-151">Baixar o arquivo de instalação do agente do OMS</span><span class="sxs-lookup"><span data-stu-id="9ccd6-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="9ccd6-152">No portal do OMS, na página **Visão Geral**, clique no bloco **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="9ccd6-153">Clique na guia **Fontes Conectadas** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="9ccd6-154">![Guia Fontes Conectadas](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="9ccd6-155">Clique em **Servidores Windows** e clique em **Baixar Agente do Windows** aplicável seu tipo de processador do computador para baixar o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="9ccd6-156">À direita da **ID do Espaço de Trabalho**, clique no ícone para copiar e cole-a no Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="9ccd6-157">À direita da **Chave Primária**, clique no ícone para copiar e cole-a Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="9ccd6-158">Instalar o agente usando a instalação</span><span class="sxs-lookup"><span data-stu-id="9ccd6-158">Install the agent using setup</span></span>
1. <span data-ttu-id="9ccd6-159">Execute Instalação para instalar o agente em um computador que você deseje gerenciar.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="9ccd6-160">Na página de Boas-vindas, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="9ccd6-161">Na página Termos de Licença, leia a licença e clique em **Aceito**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="9ccd6-162">Na página Pasta de Destino, altere ou mantenha a pasta de instalação padrão e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="9ccd6-163">Na página Opções de Instalação do Agente, você pode optar por conectar o agente ao OMS (Azure Log Analytics), ao Operations Manager ou você pode deixar as escolhas em branco se quiser configurar o agente mais tarde.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="9ccd6-164">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-164">Click **Next**.</span></span>   
    - <span data-ttu-id="9ccd6-165">Se você optar por conectar-se ao OMS (Azure Log Analytics), cole a **ID do Espaço de Trabalho** e a **Chave do Espaço de Trabalho (Chave Primária)** que você copiou para o Bloco de Notas no procedimento anterior e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="9ccd6-166">![colar ID de Espaço de Trabalho e a Chave Primária](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="9ccd6-167">Se você optar por conectar-se ao Operations Manager, digite o **Nome do Grupo de Gerenciamento**, nome do **Servidor de Gerenciamento** e **Porta do Servidor de Gerenciamento**, e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="9ccd6-168">Na página Conta de Ação de Agente, escolha a conta Sistema Local ou uma conta de domínio local e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="9ccd6-169">![configuração do grupo de gerenciamento ](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![conta de ação de agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="9ccd6-170">Na página Pronto para Instalar, reveja suas escolhas e clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="9ccd6-171">Na página Configuração concluída com êxito, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="9ccd6-172">Após concluir, o **Microsoft Monitoring Agent** aparecerá no **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="9ccd6-173">Você pode examinar sua configuração e verificar se o agente está conectado ao OMS (Operational Insights).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="9ccd6-174">Quando conectado ao OMS, o agente exibe uma mensagem dizendo: **o Microsoft Monitoring Agent conectou-se com êxito ao serviço Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="9ccd6-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="9ccd6-175">Definir configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="9ccd6-175">Configure proxy settings</span></span>

<span data-ttu-id="9ccd6-176">Você pode usar o procedimento a seguir para definir configurações de proxy para o Microsoft Monitoring Agent usando o painel de controle.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="9ccd6-177">Você precisa usar esse procedimento para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="9ccd6-178">Se você tiver vários servidores que precisa configurar, talvez seja mais fácil usar um script para automatizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="9ccd6-179">Nesse caso, consulte o próximo procedimento [Definir configurações de proxy para o Microsoft Monitoring Agent usando um script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="9ccd6-180">Para definir configurações de proxy para o Microsoft Monitoring Agent usando o painel de controle</span><span class="sxs-lookup"><span data-stu-id="9ccd6-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="9ccd6-181">Abra o **Painel de controle**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="9ccd6-182">Abra o **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="9ccd6-183">Clique na guia **Configurações de Proxy** .</span><span class="sxs-lookup"><span data-stu-id="9ccd6-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="9ccd6-184">![guia Configurações de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="9ccd6-185">Selecione **Usar um servidor proxy** e digite a URL e o número da porta, se for necessário, semelhante ao exemplo mostrado.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="9ccd6-186">Se o servidor proxy requer autenticação, digite o nome de usuário e senha para acessar o servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="9ccd6-187">Verifique a conectividade do agente com o OMS</span><span class="sxs-lookup"><span data-stu-id="9ccd6-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="9ccd6-188">Você pode facilmente verificar se os agentes estão se comunicando com o OMS usando o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="9ccd6-189">No computador com o agente do Windows, abra o Painel de Controle.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="9ccd6-190">Abra o Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="9ccd6-191">Clique na guia Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="9ccd6-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="9ccd6-192">Na coluna de Status, você verá que o agente se conectou com êxito ao serviço Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="9ccd6-194">Definir configurações de proxy para o Microsoft Monitoring Agent usando um script</span><span class="sxs-lookup"><span data-stu-id="9ccd6-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="9ccd6-195">Copie o exemplo a seguir, atualize-o com informações específicas para seu ambiente, salve-o com uma extensão de nome de arquivo PS1 e então execute o script em cada computador que se conecte diretamente ao serviço do OMS.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="9ccd6-196">Instalar o agente usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="9ccd6-196">Install the agent using the command line</span></span>
- <span data-ttu-id="9ccd6-197">Modifique e, em seguida, use o exemplo a seguir para instalar o agente usando a linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="9ccd6-198">O exemplo executa uma instalação completamente silenciosa.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="9ccd6-199">Se você quiser atualizar um agente, precisará usar a API de script do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="9ccd6-200">Consulte a próxima seção para atualizar um agente.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="9ccd6-201">O agente usa o IExpress como seu autoextrator usando o comando `/c`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="9ccd6-202">É possível ver as opções de linha de comando em [Opções de linha de comando do IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e, em seguida, atualizar o exemplo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="9ccd6-203">Opções específicas do MMA</span><span class="sxs-lookup"><span data-stu-id="9ccd6-203">MMA-specific options</span></span>                   |<span data-ttu-id="9ccd6-204">Observações</span><span class="sxs-lookup"><span data-stu-id="9ccd6-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="9ccd6-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="9ccd6-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="9ccd6-206">1 = configurar o agente para reportar a um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="9ccd6-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="9ccd6-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="9ccd6-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="9ccd6-208">ID do espaço de trabalho (guid) para o espaço de trabalho a ser adicionado</span><span class="sxs-lookup"><span data-stu-id="9ccd6-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="9ccd6-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="9ccd6-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="9ccd6-210">Chave do espaço de trabalho usada para autenticar inicialmente com o espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="9ccd6-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="9ccd6-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="9ccd6-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="9ccd6-212">Especifique o ambiente de nuvem no qual o espaço de trabalho está</span><span class="sxs-lookup"><span data-stu-id="9ccd6-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="9ccd6-213">0 = nuvem comercial do Azure (padrão)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="9ccd6-214">1 = Azure Governamental</span><span class="sxs-lookup"><span data-stu-id="9ccd6-214">1 = Azure Government</span></span> |
|<span data-ttu-id="9ccd6-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="9ccd6-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="9ccd6-216">URI do proxy a ser usado</span><span class="sxs-lookup"><span data-stu-id="9ccd6-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="9ccd6-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="9ccd6-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="9ccd6-218">Nome de usuário para acessar um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="9ccd6-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="9ccd6-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="9ccd6-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="9ccd6-220">Senha para acessar um proxy autenticado</span><span class="sxs-lookup"><span data-stu-id="9ccd6-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="9ccd6-221">Para evitar atingir o limite de comprimento da linha de comando do IExpress, instale o agente sem nenhum espaço de trabalho configurado e, em seguida, use um script para definir a configuração do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="9ccd6-222">Se você receber um `Command line option syntax error.` ao usar o parâmetro `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`, poderá usar a solução a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="9ccd6-223">Adicionar um espaço de trabalho usando um script</span><span class="sxs-lookup"><span data-stu-id="9ccd6-223">Add a workspace using a script</span></span>
<span data-ttu-id="9ccd6-224">Adicione um espaço de trabalho usando a API de script de agente do Log Analytics com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="9ccd6-225">Para adicionar um espaço de trabalho no Azure para o governo dos EUA, use o exemplo de script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="9ccd6-226">Se você já usou a linha de comando ou o script anteriormente para instalar ou configurar o agente, `EnableAzureOperationalInsights` foi substituído por `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="9ccd6-227">Instalar o agente usando o DSC na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="9ccd6-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="9ccd6-228">É possível usar o exemplo de script a seguir para instalar o agente usando o DSC na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="9ccd6-229">O exemplo instala o agente de 64 bits, identificado pelo valor `URI`.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="9ccd6-230">Também é possível usar a versão de 32 bits, substituindo o valor do URI.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="9ccd6-231">Os URIs para ambas as versões são:</span><span class="sxs-lookup"><span data-stu-id="9ccd6-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="9ccd6-232">Agente do Windows de 64 bits – https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="9ccd6-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="9ccd6-233">Agente do Windows de 32 bits – https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="9ccd6-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="9ccd6-234">Este exemplo de procedimento e de script não atualizará um agente existente.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="9ccd6-235">Importe o Módulo xPSDesiredStateConfiguration do DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) para a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="9ccd6-236">Crie ativos de variável da Automação do Azure para *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="9ccd6-237">Defina *OPSINSIGHTS_WS_ID* para sua ID do espaço de trabalho do Log Analytics do OMS e defina *OPSINSIGHTS_WS_KEY* para a chave primária do seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="9ccd6-238">Use o seguinte script e salve-o como MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="9ccd6-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="9ccd6-239">Modifique e use o exemplo a seguir para instalar o agente usando o DSC na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="9ccd6-240">Importe o MMAgent.ps1 para Automação do Azure usando a interface ou o cmdlet da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="9ccd6-241">Atribua um nó à configuração.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-241">Assign a node to the configuration.</span></span> <span data-ttu-id="9ccd6-242">Dentro de 15 minutos, o nó verifica sua configuração e o MMA é enviado para o nó.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="9ccd6-243">Obter o último valor de ProductId</span><span class="sxs-lookup"><span data-stu-id="9ccd6-243">Get the latest ProductId value</span></span>

<span data-ttu-id="9ccd6-244">O `ProductId value` no script MMAgent.ps1 é exclusivo para cada versão do agente.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="9ccd6-245">Quando uma versão atualizada de cada agente é publicada, o valor de ProductId é alterado.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="9ccd6-246">Portanto, quando o ProductId muda no futuro, é possível encontrar a versão do agente usando um script simples.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="9ccd6-247">Depois de ter a versão mais recente do agente instalada em um servidor de teste, você pode usar o script a seguir para obter o valor de ProductId instalado.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="9ccd6-248">Usando o valor de ProductId mais recente, é possível atualizar o valor no script MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="9ccd6-249">Configurar um agente manualmente ou adicionar outros espaços de trabalho</span><span class="sxs-lookup"><span data-stu-id="9ccd6-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="9ccd6-250">Se você tiver instalado os agentes, mas não os configurou, ou se quiser que o agente relate a vários espaços de trabalho, poderá usar as informações a seguir para habilitar um agente ou para reconfigurá-lo.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="9ccd6-251">Depois que você tiver configurado o agente, ele será registrado com o serviço do agente e obterá as informações de configuração necessárias e os pacotes de gerenciamento contendo informações da solução.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="9ccd6-252">Depois de instalar o Microsoft Monitoring Agent, abra o **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="9ccd6-253">Abra o **Microsoft Monitoring Agent** e clique na guia **OMS (Azure Log Analytics)**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="9ccd6-254">Clique em **Adicionar** para abrir a caixa **Adicionar um Espaço de Trabalho do Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="9ccd6-255">Cole a **ID do Espaço de Trabalho** e a **Chave do Espaço de Trabalho (Chave Primária)** que você copiou no procedimento anterior para o espaço de trabalho que você deseja adicionar e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="9ccd6-256">![configurar o Azure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="9ccd6-257">Depois que dados forem coletados de computadores monitorados por agente, o número de computadores monitorados pelo OMS aparecerá no portal do OMS na guia **Fontes Conectadas** em **Configurações** como **Servidores Conectados**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="9ccd6-258">Para desabilitar um agente</span><span class="sxs-lookup"><span data-stu-id="9ccd6-258">To disable an agent</span></span>
1. <span data-ttu-id="9ccd6-259">Depois de instalar o agente, abra o **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="9ccd6-260">Abra o Microsoft Monitoring Agent e clique na guia **OMS (Azure Log Analytics)** .</span><span class="sxs-lookup"><span data-stu-id="9ccd6-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="9ccd6-261">Selecione um espaço de trabalho e clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="9ccd6-262">Repita essa etapa para todos os outros espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="9ccd6-263">Outra opção é configurar os agentes para relatar a um grupo de gerenciamento do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9ccd6-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="9ccd6-264">Se você usar o Operations Manager em sua infraestrutura de TI, também poderá usar o agente de MMA como um agente do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="9ccd6-265">Para configurar os agentes do MMA para relatar a um grupo de gerenciamento do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9ccd6-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="9ccd6-266">No computador no qual o agente está instalado, abra o **Painel de Controle**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="9ccd6-267">Abra o **Microsoft Monitoring Agent** e clique na guia **Operations Manager**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="9ccd6-268">![Guia Microsoft Monitoring Agent Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="9ccd6-269">Se seus servidores do Operations Manager tiverem integração com o Active Directory, clique em **Atualizar automaticamente as atribuições de grupo de gerenciamento do AD DS**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="9ccd6-270">Clique em **Adicionar** para abrir a caixa de diálogo **Adicionar um Grupo de Gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="9ccd6-271">![Adicionar um Grupo de Gerenciamento do Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="9ccd6-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="9ccd6-272">Na caixa **Nome do grupo de gerenciamento** , digite o nome do grupo de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="9ccd6-273">Na caixa **Servidor de gerenciamento primário** , digite o nome do computador do servidor de gerenciamento primário.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="9ccd6-274">Na caixa **Porta do servidor de gerenciamento** , digite o número da porta TCP.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="9ccd6-275">Na página **Conta de Ação de Agente**, escolha a conta Sistema Local ou uma conta de domínio local.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="9ccd6-276">Clique em **OK** para fechar a caixa de diálogo **Adicionar um Grupo de Gerenciamento** e clique em **OK** para fechar a caixa de diálogo **Propriedades do Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9ccd6-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ccd6-277">Next steps</span></span>

- <span data-ttu-id="9ccd6-278">[Adicionar soluções do Log Analytics da Galeria de Soluções](log-analytics-add-solutions.md) para adicionar funcionalidade e obter dados.</span><span class="sxs-lookup"><span data-stu-id="9ccd6-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
