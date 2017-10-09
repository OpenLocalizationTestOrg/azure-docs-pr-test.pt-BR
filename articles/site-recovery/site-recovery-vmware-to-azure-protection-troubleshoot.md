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
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Solução de problemas de replicação de servidor local VMware/Físico
Você pode receber uma mensagem de erro específica ao proteger suas máquinas virtuais VMware ou servidores físicos usando o Azure Site Recovery. Este artigo detalha algumas das Olá encontradas, junto com tooresolve de etapas de solução de problemas de mensagens de erro mais comuns-los.


## <a name="initial-replication-is-stuck-at-0"></a>A replicação inicial está parada em 0%
A maioria das falhas de replicação inicial de saudação que encontramos no site de suporte são devido a problemas de tooconnectivity entre o servidor de processo do servidor de origem ou o processo de servidor para Azure.
Na maioria dos casos, você pode self solucionar esses problemas seguindo as etapas Olá listadas abaixo.

###<a name="check-hello-following-on-source-machine"></a>Verifique a seguinte Olá na máquina de origem
* Na linha de comando de máquina do servidor de origem, use o Telnet tooping saudação do servidor em processo com a porta https (padrão 9443), como mostrado abaixo toosee se há problemas de conectividade de rede ou problemas de bloqueio de porta de firewall.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Usar o Telnet, não use a conectividade de tootest de PING.  Se o Telnet não estiver instalado, siga a lista de etapas de saudação [aqui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Se não é possível tooconnect, permitir que a porta de entrada 9443 em saudação do servidor em processo e verifique se hello problema ainda será fechado. Houve alguns casos em que o servidor de processo estava atrás da DMZ, e isso estava causando o problema.

* Verificar status de saudação do serviço `InMage Scout VX Agent – Sentinel/OutpostStart` se não for em execução e verifique se o problema de saudação ainda existe.   
 
###<a name="check-hello-following-on-process-server"></a>Verifique a seguinte Olá no servidor de processo

* **Verifique se o servidor de processo está fazendo ativamente tooAzure de dados** 

Da máquina do servidor de processo, abra hello (pressione Ctrl-Shift-Esc) do Gerenciador de tarefas. Acesse a guia de desempenho de toohello e clique em link 'Abrir o Monitor de recursos'. No Gerenciador de recursos, vá tooNetwork guia. Verifique se cbengine.exe em 'Processos com atividade de rede' está enviando ativamente um grande volume (em Mbs) de dados.

![Habilitar a replicação](./media/site-recovery-protection-common-errors/cbengine.png)

Caso não siga etapas Olá listadas abaixo:

* **Verifique se o servidor de processo é tooconnect capaz de BLOBs do Azure**: selecione e marque cbengine.exe tooview Olá 'Conexões de TCP' toosee se há conectividade com a URL de blob do armazenamento do servidor de processo tooAzure.

![Habilitar a replicação](./media/site-recovery-protection-common-errors/rmonitor.png)

Se não vá tooControl painel > serviços, verifique se Olá serviços a seguir está em execução:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Iniciar qualquer serviço que não está em execução e verifique se o problema de saudação ainda existe.

* **Verifique se o servidor de processo é o endereço de IP público tooAzure tooconnect capaz de usar a porta 443**

Abra Olá CBEngineCurr.errlog mais recente do `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e procure: 443 e a conexão falha na tentativa.

![Habilitar a replicação](./media/site-recovery-protection-common-errors/logdetails1.png)

Se houver problemas, na linha de comando do servidor de processo, use telnet tooping seu endereço IP público do Azure (mascarado acima imagem) encontrado no hello CBEngineCurr.currLog usando a porta 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Se você não é possível tooconnect, verifique se o problema de acesso Olá for devido toofirewall ou Proxy, conforme descrito na próxima etapa.


* **Verifique se o firewall baseado em endereço IP no servidor de processo não estão bloqueando o acesso**: se você estiver usando um regras de firewall baseado em endereço IP no servidor de saudação, baixe a lista completa de saudação do Microsoft Azure Datacenter intervalos de IP de [aqui ](https://www.microsoft.com/download/details.aspx?id=41653) e adicioná-las tooyour tooensure de configuração de firewall permitem comunicação tooAzure (e Olá porta HTTPS (443)).  Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).

* **Verifique se o firewall baseado em URL no servidor de processo não está bloqueando o acesso**: se você estiver usando regras de firewall de URL com base no servidor de saudação, certifique-se de saudação URLs a seguir é adicionada toofirewall configuração. 
     
  `*.accesscontrol.windows.net:` Usado para controle de acesso e gerenciamento de identidades

  `*.backup.windowsazure.com:` Usado para transferência de dados de replicação e orquestração

  `*.blob.core.windows.net:`Usado para acesso toohello conta de armazenamento que armazena dados replicados

  `*.hypervrecoverymanager.windowsazure.com:` Usado para operações de gerenciamento de replicação e orquestração

  `time.nist.gov`e `time.windows.com`: usado toocheck a sincronização de horário entre o sistema e o tempo global.

URLs para a **Nuvem do Azure Governamental**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Verifique se as Configurações de Proxy no Servidor de Processo não estão bloqueando o acesso**.  Se você estiver usando um servidor Proxy, certifique-se de nome do servidor proxy hello está resolvendo pelo servidor DNS hello.
toocheck o que você forneceu no tempo de saudação do programa de instalação do servidor de configuração. Vá tooregistry chave

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Agora, verifique se que Olá mesmas configurações estão sendo usadas pelos dados de toosend do agente de recuperação de Site do Azure.
Procure o Backup do Microsoft Azure 

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mab.png)

Abra-o e clique em Ação > Alterar as Propriedades. Na guia de configuração de Proxy, você deve ver o endereço de proxy hello, que deve ser idênticos, conforme mostrado pelas configurações de registro de saudação. Se não estiver, altere-o toohello mesmo endereço.

![Habilitar a replicação](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Verifique se a limitação de largura de banda não é restrito no servidor de processo**: aumente a largura de banda hello e verifique se o problema de saudação ainda existe.

##<a name="next-steps"></a>Próximas etapas
Se você precisar de mais ajuda, em seguida, poste sua consulta muito[fórum ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Temos uma comunidade ativa e um dos nossos engenheiros será capaz de tooassist você.
