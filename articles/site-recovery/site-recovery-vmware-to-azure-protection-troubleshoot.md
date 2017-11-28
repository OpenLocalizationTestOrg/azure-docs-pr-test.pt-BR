---
title: "Solução de problemas de falhas de proteção do VMware/Física para o Azure | Microsoft Docs"
description: "Este artigo descreve as falhas de replicação de máquina VMware comuns e como solucioná-los"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="c3ad8-103">Solução de problemas de replicação de servidor local VMware/Físico</span><span class="sxs-lookup"><span data-stu-id="c3ad8-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="c3ad8-104">Você pode receber uma mensagem de erro específica ao proteger suas máquinas virtuais VMware ou servidores físicos usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="c3ad8-105">Este artigo detalha algumas das mensagens de erro mais comuns encontradas, junto com as etapas para resolvê-las.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="c3ad8-106">A replicação inicial está parada em 0%</span><span class="sxs-lookup"><span data-stu-id="c3ad8-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="c3ad8-107">A maioria das falhas de replicação inicial que encontramos no site de suporte são devido a problemas de conectividade entre o servidor de origem e o servidor de processo ou entre o servidor de processo e o Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="c3ad8-108">Na maioria dos casos, você pode solucionar esses problemas por conta própria, seguindo as etapas listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="c3ad8-109">Verifique o seguinte no computador de origem</span><span class="sxs-lookup"><span data-stu-id="c3ad8-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="c3ad8-110">Na linha de comando do computador do Servidor de Origem, use o Telnet para executar um ping no Servidor de Processo com a porta https (padrão 9443), conforme mostrado abaixo para ver se há problemas de conectividade de rede ou problemas de bloqueio de porta de firewall.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="c3ad8-111">Use o Telnet, não use o PING para testar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="c3ad8-112">Se o Telnet não estiver instalado, siga a lista de etapas [aqui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="c3ad8-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="c3ad8-113">Se não conseguir se conectar, dê permissão para a porta de entrada 9443 no Servidor de Processo e verifique se o problema ainda existe.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="c3ad8-114">Houve alguns casos em que o servidor de processo estava atrás da DMZ, e isso estava causando o problema.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="c3ad8-115">Verifique o status do serviço `InMage Scout VX Agent – Sentinel/OutpostStart` e se ele não está em execução e verifique se o problema ainda existe.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="c3ad8-116">Verifique o seguinte no servidor de processo</span><span class="sxs-lookup"><span data-stu-id="c3ad8-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="c3ad8-117">**Verifique se o servidor de processo está ativamente enviando dados por push para o Azure**</span><span class="sxs-lookup"><span data-stu-id="c3ad8-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="c3ad8-118">Do computador do Servidor de Processo, abra o Gerenciador de Tarefas (pressione Ctrl-Shift-Esc).</span><span class="sxs-lookup"><span data-stu-id="c3ad8-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="c3ad8-119">Vá para a guia Desempenho e clique no link 'Abrir o Monitor de Recursos'.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="c3ad8-120">No Gerenciador de Recursos, vá para a guia Rede.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="c3ad8-121">Verifique se cbengine.exe em 'Processos com atividade de rede' está enviando ativamente um grande volume (em Mbs) de dados.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="c3ad8-123">Se isso não estiver acontecendo siga as etapas listadas abaixo:</span><span class="sxs-lookup"><span data-stu-id="c3ad8-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="c3ad8-124">**Verifique se o Servidor de Processo é capaz de se conectar de Blob do Azure**: Selecione e marque cbengine.exe para exibir as 'Conexões de TCP' para ver se há conectividade do Servidor de Processo a URL de blob do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="c3ad8-126">Se não, em seguida, vá para o Painel de Controle > Serviços, verifique se os seguintes serviços estão em execução:</span><span class="sxs-lookup"><span data-stu-id="c3ad8-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="c3ad8-127">(Re)Inicie qualquer serviço que não estiver em execução e verifique se o problema ainda existe.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="c3ad8-128">**Verifique se o Servidor de Processo é capaz de se conectar ao endereço IP público do Azure usando a porta 443**</span><span class="sxs-lookup"><span data-stu-id="c3ad8-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="c3ad8-129">Abra o CBEngineCurr.errlog mais recente do `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e procure: 443 e a tentativa de conexão com falha.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="c3ad8-131">Se houver problemas, em seguida, na linha de comando do Servidor de Processo, use o telnet para executar o ping do seu endereço IP público do Azure (mascarado na imagem acima) encontrado no CBEngineCurr.currLog usando a porta 443.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="c3ad8-132">Se não for possível conectar-se, em seguida, verifique se o problema de acesso é devido ao firewall ou Proxy, conforme descrito na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="c3ad8-133">**Verifique se o firewall baseado em endereço IP no Servidor de Processo não estão bloqueando o acesso**: Se você estiver usando regras de firewall baseadas em endereço IP no servidor, em seguida, baixe a lista completa de intervalos de IP do Microsoft Azure Datacenter [aqui](https://www.microsoft.com/download/details.aspx?id=41653) e adicione-os à sua configuração de firewall para garantir que eles permitam a comunicação com o Azure (e a porta HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="c3ad8-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="c3ad8-134">Permita os intervalos de endereços IP para a região do Azure da sua assinatura e para o Oeste dos EUA (usados para Controle de Acesso e Gerenciamento de Identidade).</span><span class="sxs-lookup"><span data-stu-id="c3ad8-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="c3ad8-135">**Verifique se o firewall baseado em URL no Servidor de Processo não está bloqueando o acesso**: Se você estiver usando regras de firewall baseada em URL no servidor, verifique se as URLs a seguir são adicionadas à configuração do firewall.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="c3ad8-136">`*.accesscontrol.windows.net:` Usado para controle de acesso e gerenciamento de identidades</span><span class="sxs-lookup"><span data-stu-id="c3ad8-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="c3ad8-137">`*.backup.windowsazure.com:` Usado para transferência de dados de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="c3ad8-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="c3ad8-138">`*.blob.core.windows.net:` Usado para acessar a conta de armazenamento que armazena os dados replicados</span><span class="sxs-lookup"><span data-stu-id="c3ad8-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="c3ad8-139">`*.hypervrecoverymanager.windowsazure.com:` Usado para operações de gerenciamento de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="c3ad8-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="c3ad8-140">`time.nist.gov` e `time.windows.com`: Usados para verificar a sincronização de horário entre a hora do sistema e a hora global.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="c3ad8-141">URLs para a **Nuvem do Azure Governamental**:</span><span class="sxs-lookup"><span data-stu-id="c3ad8-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="c3ad8-142">**Verifique se as Configurações de Proxy no Servidor de Processo não estão bloqueando o acesso**.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="c3ad8-143">Se você estiver usando um Servidor Proxy, certifique-se de que o nome do servidor proxy é resolvido pelo servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="c3ad8-144">Para verificar o que você forneceu no momento da instalação do Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="c3ad8-145">Vá para a chave do registro</span><span class="sxs-lookup"><span data-stu-id="c3ad8-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="c3ad8-146">Agora, certifique-se de que as mesmas configurações estão sendo usadas pelo agente Azure Site Recovery para enviar dados.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="c3ad8-147">Procure o Backup do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c3ad8-147">Search Microsoft Azure  Backup</span></span> 

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="c3ad8-149">Abra-o e clique em Ação > Alterar as Propriedades.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="c3ad8-150">Na guia de Configuração de Proxy, você deve ver o endereço de proxy, que deve ser igual ao mostrado pelas configurações do registro.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="c3ad8-151">Caso contrário, altere-a para o mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-151">If not, please change it to the same address.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="c3ad8-153">**Verifique se a Limitação de largura de banda não é restrita no Servidor de Processo**: Aumente a largura de banda e verifique se o problema ainda existe.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="c3ad8-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3ad8-154">Next steps</span></span>
<span data-ttu-id="c3ad8-155">Se precisar de mais ajuda, poste sua consulta no [fórum de ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c3ad8-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="c3ad8-156">Temos uma comunidade ativa e um dos nossos engenheiros poderá ajudá-lo.</span><span class="sxs-lookup"><span data-stu-id="c3ad8-156">We have an active community and one of our engineers will be able to assist you.</span></span>