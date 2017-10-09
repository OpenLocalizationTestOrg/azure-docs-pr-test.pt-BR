---
title: "aaaTroubleshoot proteção contra falhas VMware/físicos tooAzure | Microsoft Docs"
description: "Este artigo descreve falhas de replicação de máquina do hello comuns VMware e como tootroubleshoot-los"
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
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="e003c-103">Solução de problemas de replicação de servidor local VMware/Físico</span><span class="sxs-lookup"><span data-stu-id="e003c-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="e003c-104">Você pode receber uma mensagem de erro específica ao proteger suas máquinas virtuais VMware ou servidores físicos usando o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e003c-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="e003c-105">Este artigo detalha algumas das Olá encontradas, junto com tooresolve de etapas de solução de problemas de mensagens de erro mais comuns-los.</span><span class="sxs-lookup"><span data-stu-id="e003c-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="e003c-106">A replicação inicial está parada em 0%</span><span class="sxs-lookup"><span data-stu-id="e003c-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="e003c-107">A maioria das falhas de replicação inicial de saudação que encontramos no site de suporte são devido a problemas de tooconnectivity entre o servidor de processo do servidor de origem ou o processo de servidor para Azure.</span><span class="sxs-lookup"><span data-stu-id="e003c-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="e003c-108">Na maioria dos casos, você pode self solucionar esses problemas seguindo as etapas Olá listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="e003c-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="e003c-109">Verifique a seguinte Olá na máquina de origem</span><span class="sxs-lookup"><span data-stu-id="e003c-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="e003c-110">Na linha de comando de máquina do servidor de origem, use o Telnet tooping saudação do servidor em processo com a porta https (padrão 9443), como mostrado abaixo toosee se há problemas de conectividade de rede ou problemas de bloqueio de porta de firewall.</span><span class="sxs-lookup"><span data-stu-id="e003c-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="e003c-111">Usar o Telnet, não use a conectividade de tootest de PING.</span><span class="sxs-lookup"><span data-stu-id="e003c-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="e003c-112">Se o Telnet não estiver instalado, siga a lista de etapas de saudação [aqui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="e003c-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="e003c-113">Se não é possível tooconnect, permitir que a porta de entrada 9443 em saudação do servidor em processo e verifique se hello problema ainda será fechado.</span><span class="sxs-lookup"><span data-stu-id="e003c-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="e003c-114">Houve alguns casos em que o servidor de processo estava atrás da DMZ, e isso estava causando o problema.</span><span class="sxs-lookup"><span data-stu-id="e003c-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="e003c-115">Verificar status de saudação do serviço `InMage Scout VX Agent – Sentinel/OutpostStart` se não for em execução e verifique se o problema de saudação ainda existe.</span><span class="sxs-lookup"><span data-stu-id="e003c-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="e003c-116">Verifique a seguinte Olá no servidor de processo</span><span class="sxs-lookup"><span data-stu-id="e003c-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="e003c-117">**Verifique se o servidor de processo está fazendo ativamente tooAzure de dados**</span><span class="sxs-lookup"><span data-stu-id="e003c-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="e003c-118">Da máquina do servidor de processo, abra hello (pressione Ctrl-Shift-Esc) do Gerenciador de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e003c-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="e003c-119">Acesse a guia de desempenho de toohello e clique em link 'Abrir o Monitor de recursos'.</span><span class="sxs-lookup"><span data-stu-id="e003c-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="e003c-120">No Gerenciador de recursos, vá tooNetwork guia. Verifique se cbengine.exe em 'Processos com atividade de rede' está enviando ativamente um grande volume (em Mbs) de dados.</span><span class="sxs-lookup"><span data-stu-id="e003c-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="e003c-122">Caso não siga etapas Olá listadas abaixo:</span><span class="sxs-lookup"><span data-stu-id="e003c-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="e003c-123">**Verifique se o servidor de processo é tooconnect capaz de BLOBs do Azure**: selecione e marque cbengine.exe tooview Olá 'Conexões de TCP' toosee se há conectividade com a URL de blob do armazenamento do servidor de processo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e003c-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="e003c-125">Se não vá tooControl painel > serviços, verifique se Olá serviços a seguir está em execução:</span><span class="sxs-lookup"><span data-stu-id="e003c-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="e003c-126">(Re) Iniciar qualquer serviço que não está em execução e verifique se o problema de saudação ainda existe.</span><span class="sxs-lookup"><span data-stu-id="e003c-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="e003c-127">**Verifique se o servidor de processo é o endereço de IP público tooAzure tooconnect capaz de usar a porta 443**</span><span class="sxs-lookup"><span data-stu-id="e003c-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="e003c-128">Abra Olá CBEngineCurr.errlog mais recente do `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e procure: 443 e a conexão falha na tentativa.</span><span class="sxs-lookup"><span data-stu-id="e003c-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="e003c-130">Se houver problemas, na linha de comando do servidor de processo, use telnet tooping seu endereço IP público do Azure (mascarado acima imagem) encontrado no hello CBEngineCurr.currLog usando a porta 443.</span><span class="sxs-lookup"><span data-stu-id="e003c-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="e003c-131">Se você não é possível tooconnect, verifique se o problema de acesso Olá for devido toofirewall ou Proxy, conforme descrito na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="e003c-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="e003c-132">**Verifique se o firewall baseado em endereço IP no servidor de processo não estão bloqueando o acesso**: se você estiver usando um regras de firewall baseado em endereço IP no servidor de saudação, baixe a lista completa de saudação do Microsoft Azure Datacenter intervalos de IP de [aqui ](https://www.microsoft.com/download/details.aspx?id=41653) e adicioná-las tooyour tooensure de configuração de firewall permitem comunicação tooAzure (e Olá porta HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="e003c-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="e003c-133">Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).</span><span class="sxs-lookup"><span data-stu-id="e003c-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="e003c-134">**Verifique se o firewall baseado em URL no servidor de processo não está bloqueando o acesso**: se você estiver usando regras de firewall de URL com base no servidor de saudação, certifique-se de saudação URLs a seguir é adicionada toofirewall configuração.</span><span class="sxs-lookup"><span data-stu-id="e003c-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="e003c-135">`*.accesscontrol.windows.net:` Usado para controle de acesso e gerenciamento de identidades</span><span class="sxs-lookup"><span data-stu-id="e003c-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="e003c-136">`*.backup.windowsazure.com:` Usado para transferência de dados de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="e003c-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="e003c-137">`*.blob.core.windows.net:`Usado para acesso toohello conta de armazenamento que armazena dados replicados</span><span class="sxs-lookup"><span data-stu-id="e003c-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="e003c-138">`*.hypervrecoverymanager.windowsazure.com:` Usado para operações de gerenciamento de replicação e orquestração</span><span class="sxs-lookup"><span data-stu-id="e003c-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="e003c-139">`time.nist.gov`e `time.windows.com`: usado toocheck a sincronização de horário entre o sistema e o tempo global.</span><span class="sxs-lookup"><span data-stu-id="e003c-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="e003c-140">URLs para a **Nuvem do Azure Governamental**:</span><span class="sxs-lookup"><span data-stu-id="e003c-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="e003c-141">**Verifique se as Configurações de Proxy no Servidor de Processo não estão bloqueando o acesso**.</span><span class="sxs-lookup"><span data-stu-id="e003c-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="e003c-142">Se você estiver usando um servidor Proxy, certifique-se de nome do servidor proxy hello está resolvendo pelo servidor DNS hello.</span><span class="sxs-lookup"><span data-stu-id="e003c-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="e003c-143">toocheck o que você forneceu no tempo de saudação do programa de instalação do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e003c-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="e003c-144">Vá tooregistry chave</span><span class="sxs-lookup"><span data-stu-id="e003c-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="e003c-145">Agora, verifique se que Olá mesmas configurações estão sendo usadas pelos dados de toosend do agente de recuperação de Site do Azure.</span><span class="sxs-lookup"><span data-stu-id="e003c-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="e003c-146">Procure o Backup do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e003c-146">Search Microsoft Azure  Backup</span></span> 

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="e003c-148">Abra-o e clique em Ação > Alterar as Propriedades.</span><span class="sxs-lookup"><span data-stu-id="e003c-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="e003c-149">Na guia de configuração de Proxy, você deve ver o endereço de proxy hello, que deve ser idênticos, conforme mostrado pelas configurações de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e003c-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="e003c-150">Se não estiver, altere-o toohello mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="e003c-150">If not, please change it toohello same address.</span></span>

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="e003c-152">**Verifique se a limitação de largura de banda não é restrito no servidor de processo**: aumente a largura de banda hello e verifique se o problema de saudação ainda existe.</span><span class="sxs-lookup"><span data-stu-id="e003c-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="e003c-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e003c-153">Next steps</span></span>
<span data-ttu-id="e003c-154">Se você precisar de mais ajuda, em seguida, poste sua consulta muito[fórum ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e003c-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="e003c-155">Temos uma comunidade ativa e um dos nossos engenheiros será capaz de tooassist você.</span><span class="sxs-lookup"><span data-stu-id="e003c-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
