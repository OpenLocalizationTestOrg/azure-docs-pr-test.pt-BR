---
title: "aaaVMware solução de monitoramento na análise de Log | Microsoft Docs"
description: "Saiba mais sobre como Olá solução de monitoramento da VMware pode ajudar a gerenciar logs e monitorar hosts ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Solução de Monitoramento de VMware (visualização) no Log Analytics

![Símbolo de VMware](./media/log-analytics-vmware/vmware-symbol.png)

Olá solução de monitoramento da VMware em análise de Log é uma solução que ajuda você a criar uma abordagem de monitoramento para grandes logs de VMware e o log centralizado. Este artigo descreve como você pode solucionar, capturar e gerenciar hosts de ESXi Olá em um único local usando a solução de saudação. Com a solução Olá, você pode ver os dados detalhados para todos os hosts de ESXi em um único local. Você pode ver os principais eventos contagens, status e tendências de VM e hosts ESXi fornecidos por meio de registros de host de ESXi hello. Você pode solucionar problemas exibindo e pesquisando logs de host ESXi centralizados. Além disso, você pode criar alertas com base em consultas de pesquisa de log.

solução de saudação usa a funcionalidade de syslog nativo de saudação ESXi host toopush dados tooa VM de destino, que tem o agente do OMS. No entanto, solução de saudação não gravar arquivos no syslog em VM de destino hello. agente do OMS Olá abre a porta 1514 e escuta toothis. Depois que ele recebe dados hello, agente do OMS Olá Olá enviar dados por push ao OMS.

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação.

* Adicionar VMware monitoramento da saudação solução tooyour espaço de trabalho do OMS usando Olá processo descrito na [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Hosts VMware ESXi com suporte
Host vSphere ESXi 5.5 e 6.0

#### <a name="prepare-a-linux-server"></a>Preparar um servidor Linux
Crie um tooreceive VM do sistema operacional Linux todos os dados de syslog de hosts de ESXi hello. Olá [agente do OMS Linux](log-analytics-linux-agents.md) é o ponto de coleta Olá para todos os dados de syslog de host de ESXi. Você pode usar vários ESXi hosts tooforward logs tooa único servidor Linux, como no exemplo a seguir de saudação.  

   ![fluxo syslog](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Configurar coleção syslog
1. Configure o encaminhamento syslog para VSphere. Para obter informações detalhadas toohelp de configurar o encaminhamento de syslog, consulte [configuração syslog em ESXi 5. x e 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Vá muito**configuração do Host de ESXi** > **Software** > **configurações avançadas** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. Em Olá *Syslog.global.logHost* campo, adicione o número de porta de servidor e hello Linux *1514*. Por exemplo, `tcp://hostname:1514` ou `tcp://123.456.789.101:1514`
3. Abra o firewall do host de ESXi Olá para syslog. **Configuração do Host ESXi** > **Software** > **Perfil de Segurança** > **Firewall** e abra **Propriedades**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Verifique tooverify de Console do vSphere Olá que syslog está configurado corretamente. Confirmar a saudação essa porta de host de ESXI **1514** está configurado.
5. Baixe e instale a saudação do agente do OMS para Linux no servidor Linux de saudação. Para obter mais informações, consulte Olá [documentação do agente do OMS para Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Depois de saudação do agente do OMS para Linux for instalada, vá toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d diretório e cópia Olá vmware_esxi.conf arquivo toohello /etc/opt/microsoft/omsagent/conf/omsagent.d e Olá Olá de alteração de proprietário/grupo e as permissões de arquivo hello. Por exemplo:

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Reinicie Olá agente do OMS para Linux executando `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Testar a conectividade de saudação entre o servidor Linux de saudação e host de ESXi hello usando Olá `nc` comando Olá ESXi Host. Por exemplo:

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Olá Portal do OMS, executar uma pesquisa de log para `Type=VMware_CL`. Quando o OMS coleta dados de syslog hello, ele retém o formato de syslog hello. No portal de hello, alguns campos específicos são capturados como *Hostname* e *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Se seus resultados de pesquisa de log de exibição são semelhantes imagem toohello acima, você está configurado toouse Olá OMS VMware monitoramento solução painel de controle.  

## <a name="vmware-data-collection-details"></a>Detalhes da coleta de dados do VMware
Olá solução de monitoramento da VMware coleta vários dados de log e métricas de desempenho de hosts de ESXi usando Olá agentes do OMS para Linux que você tiver habilitado.

Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados.

| plataforma | Agente do OMS para Linux | Agente SCOM | Armazenamento do Azure | SCOM necessário? | Os dados do agente SCOM enviados por meio do grupo de gerenciamento | frequência de coleta |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |a cada 3 minutos |

Olá, a tabela a seguir mostra exemplos de campos de dados coletados pelo Olá solução de monitoramento do VMware:

| nome do campo | Descrição |
| --- | --- |
| Device_s |dispositivos de armazenamento do VMware |
| ESXIFailure_s |tipos de falha |
| EventTime_t |horário em que o evento ocorreu |
| HostName_s |nome de host ESXi |
| Operation_s |criar VM ou excluir VM |
| ProcessName_s |nome do evento |
| ResourceId_s |nome do host do VMware Olá |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |Status de SCSI do VMware |
| SyslogMessage_s |Dados syslog |
| UserName_s |usuário que criou ou excluiu a VM |
| VMName_s |Nome da VM |
| Computador |computador host |
| TimeGenerated |dados de saudação do tempo foi gerados |
| DataCenter_s |Datacenter do VMware |
| StorageLatency_s |latência de armazenamento (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Visão geral da solução de Monitoramento de VMware
bloco de VMware Olá aparece no hello portal do OMS. Ele fornece uma visão ampla de eventuais falhas. Quando você clica em bloco hello, ir para uma exibição de painel.

![bloco](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Navegue de exibição de painel Olá
Em Olá **VMware** de exibição de painel, blades são organizados por:

* Contagem de Status de Falha
* Contagens de hosts principais por evento
* Contagens de eventos principais
* Atividades da Máquina Virtual
* Eventos de Disco do Host ESXi

![solução1](./media/log-analytics-vmware/solutionview1-1.png)

![solução2](./media/log-analytics-vmware/solutionview1-2.png)

Clique em qualquer folha de tooopen painel de pesquisa de análise de Log que mostra informações detalhadas específicas para a folha de saudação.

A partir daqui, você pode editar Olá toomodify de consulta de pesquisa para algo específico. Para obter um tutorial sobre noções básicas de saudação de pesquisa do OMS, check-out Olá [tutorial de pesquisa de log do OMS.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Encontrar eventos do host ESXi
Um único host ESXi gera vários logs, com base em seus processos. Olá solução de monitoramento da VMware centraliza-los e resume Olá contagens dos eventos. Essa exibição centralizada ajuda a entender qual host ESXi tem um alto volume de eventos e quais eventos ocorrem com mais frequência em seu ambiente.

![evento](./media/log-analytics-vmware/events.png)

Você pode aprofundar-se ainda mais, clicando em um host ESXi ou um tipo de evento.

Quando você clica em um nome de host ESXi, as informações desse host são exibidas. Se você deseja que os resultados de toonarrow com o tipo de evento hello, adicione `“ProcessName_s=EVENT TYPE”` na consulta de pesquisa. Você pode selecionar **ProcessName** no filtro de pesquisa de saudação. Que restringe informações Olá para você.

![aprofundar-se](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Localizar atividades altas de VM
Uma máquina virtual pode ser criada em e excluída de qualquer host ESXi. É útil para um administrador tooidentify quantas máquinas virtuais que cria um host de ESXi. Que por sua vez, ajuda a toounderstand desempenho e planejamento de capacidade. Manter o controle dos eventos de atividade de VM é essencial ao gerenciar seu ambiente.

![aprofundar-se](./media/log-analytics-vmware/vmactivities1.png)

Se desejar que o host de ESXi adicional toosee data de criação de VM, clique em um nome de host de ESXi.

![aprofundar-se](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Consultas de pesquisa comuns
solução de saudação inclui outras consultas úteis que podem ajudá-lo a gerenciar seus hosts de ESXi, como espaço de armazenamento de alta latência de armazenamento e falha de caminho.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![consultas](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Salvar consultas
Salvar consultas de pesquisa é um recurso padrão do OMS e pode lhe ajudar a manter todas as consultas que você considerar úteis. Depois de criar uma consulta que sejam úteis, salve-o clicando Olá **Favoritos**. Uma consulta salva permite que você facilmente reutilizá-la posteriormente da saudação [meu painel](log-analytics-dashboards.md) página onde você pode criar seus próprios painéis personalizados.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Criar alertas com base em consultas
Depois que você criou suas consultas, convém toouse Olá consultas tooalert quando eventos específicos ocorrem. Consulte [alertas na análise de Log](log-analytics-alerts.md) para obter informações sobre como toocreate alertas. Para obter exemplos de consultas e outros exemplos de consulta de alertas, consulte Olá [VMware Monitor usando a análise de Log do OMS](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) postagem de blog.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>O que é necessário toodo na configuração do host de ESXi Olá? Que impacto terá no meu ambiente atual?
Olá solução usa o mecanismo de encaminhamento de Syslog do Host de ESXi nativo hello. Não é necessário software adicional Microsoft hello Host ESXi toocapture Olá logs. Ele deve ter um ambiente existente do tooyour de baixo impacto. No entanto, é necessário o encaminhamento de syslog tooset, que é a funcionalidade ESXI.

### <a name="do-i-need-toorestart-my-esxi-host"></a>É necessário toorestart meu host de ESXi?
Não. Esse processo não requer uma reinicialização. Às vezes, vSphere não atualizar corretamente Olá syslog. Nesse caso, faça logon no host de ESXi toohello e recarregue Olá syslog. Novamente, host de saudação toorestart, não é necessário para que esse processo não é o ambiente tooyour interrupções.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>Pode aumentar ou diminuir volume Olá dos dados de log enviados tooOMS?
Sim, pode. Você pode usar as configurações de nível de Log do Host de ESXi Olá no vSphere. Coleção de log é baseada em Olá *informações* nível. Portanto, se você quiser tooaudit VM criação ou exclusão, você precisa Olá tookeep *informações* nível em Hostd. Para obter mais informações, consulte Olá [da Base de dados de Conhecimento VMware](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Por que Hostd não está fornecendo dados tooOMS? Minha configuração de log é definida tooinfo.
Houve um bug de host de ESXi para Olá syslog timestamp. Para obter mais informações, consulte Olá [da Base de dados de Conhecimento VMware](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Depois de aplicar a solução alternativa de hello, Hostd devem funcionar normalmente.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Posso ter ESXi vários hosts encaminhamento syslog dados tooa única VM com omsagent?
Sim. Você pode ter vários ESXi hosts encaminhamento tooa única VM com omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Por que não vejo dados que fluem para OMS?
Pode haver vários motivos:

* host de ESXi Olá é não enviar dados toohello VM em execução omsagent corretamente. tootest, executar Olá etapas a seguir:

  1. tooconfirm, faça logon no host de ESXi toohello usando ssh e execute Olá comando a seguir:`nc -z ipaddressofVM 1514`

      Se não for bem-sucedida, as configurações do vSphere no hello configuração avançada são provavelmente não corrigir. Consulte [configurar coleta de syslog](#configure-syslog-collection) para obter informações sobre como tooset a saudação ESXi hospedar para encaminhamento de syslog.
  2. Se a conectividade da porta de syslog foi bem-sucedida, mas os dados ainda não aparecem, recarregue Olá syslog no host de ESXi hello usando ssh Olá toorun comando a seguir:` esxcli system syslog reload`
* Olá VM com o agente do OMS não está definido corretamente. tootest isso, execute Olá etapas a seguir:

  1. OMS escuta a porta toohello 1514 e envia dados ao OMS. tooverify que ele é aberto e execute Olá comando a seguir:`netstat -a | grep 1514`
  2. Você deve ver a porta `1514/tcp` abrir. Se você não fizer isso, verifique se que omsagent hello está instalado corretamente. Se você não vir as informações de porta hello, porta de syslog Olá não é aberta no hello VM.

     1. Verifique se esse Olá executando o agente do OMS usando `ps -ef | grep oms`. Se não estiver em execução, iniciar o processo de saudação executando o comando Olá` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Olá abrir `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` arquivo.

         Verificar se o usuário apropriado hello e configuração de grupo é válido, semelhante a:`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Se o arquivo hello não existe ou Olá usuário e a configuração de grupo está incorreta, execute ações corretivas por [Preparando um servidor Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log](log-analytics-log-searches.md) na análise de Log tooview obter dados de host do VMware.
* [Criar seus próprios painéis](log-analytics-dashboards.md) mostrando os dados de host do VMware.
* [Criar alertas](log-analytics-alerts.md) quando ocorrem eventos específicos de host do VMware.
