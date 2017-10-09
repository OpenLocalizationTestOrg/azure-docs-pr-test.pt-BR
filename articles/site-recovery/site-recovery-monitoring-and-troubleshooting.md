---
title: "aaaMonitor e solucionar problemas de proteção para máquinas virtuais e servidores físicos | Microsoft Docs"
description: "O Azure Site Recovery coordena a replicação hello, failover e recuperação de máquinas virtuais localizadas em tooAzure de servidores local ou em um datacenter secundário. Use este artigo toomonitor e solucionar problemas de proteção de site do Hyper-V ou o Virtual Machine Manager."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: mkjain
editor: 
ms.assetid: 0fc8e368-0c0e-4bb1-9d50-cffd5ad0853f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: d790375db5f30e98f009c8d8272558188c51934c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-troubleshoot-protection-for-virtual-machines-and-physical-servers"></a>Monitorar e solucionar problemas de proteção para máquinas virtuais e sites físicos
Este monitoramento e solução de problemas guia ajuda você a aprender como tootrack integridade da replicação e técnicas de solução de problemas para o Azure Site Recovery.

## <a name="understand-hello-components"></a>Entender os componentes de saudação
### <a name="vmware-virtual-machine-or-physical-server-site-deployment-for-replication-between-on-premises-and-azure"></a>Implantação de máquina virtual VMware ou site do servidor físico para replicação entre locais e o Azure
tooset a recuperação de banco de dados entre uma máquina virtual no local, VMware ou o servidor físico e o Azure, você precisa tooset o servidor de configuração de saudação, servidor de destino mestre e componentes de servidor de processo em sua máquina virtual ou o servidor. Ao habilitar a proteção para o servidor de origem hello, Azure Site Recovery instala o recurso de aplicativos móveis de saudação do serviço de aplicativo do Microsoft Azure. Após uma interrupção de local e a saudação source server realiza failover tooAzure, os clientes precisam tooset backup de um servidor de processo no Azure e um servidor de destino mestre no servidor de origem do local toorebuild Olá no local.

![Implantação de site Físico/VMware para replicação entre locais e o Azure](media/site-recovery-monitoring-and-troubleshooting/image18.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-sites"></a>Implantação de site do Virtual Machine Manager para a replicação entre sites locais
tooset a recuperação de banco de dados entre dois locais local, você precisa de provedor de Azure Site Recovery toodownload hello e instalá-lo no servidor do Virtual Machine Manager hello. provedor de saudação precisa tooensure de conectividade de Internet que todas as operações de saudação que são disparadas de saudação portal do Azure obtém operações locais tooon traduzidos.

![Implantação de site do Virtual Machine Manager para a replicação entre sites locais](media/site-recovery-monitoring-and-troubleshooting/image1.png)

### <a name="virtual-machine-manager-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Implantação de site do Virtual Machine Manager para replicação entre localizações locais e o Azure
Quando você configura a recuperação de banco de dados entre locais de local e o Azure, você precisa de provedor de Azure Site Recovery toodownload hello e instalá-lo no servidor do Virtual Machine Manager hello. Você também precisa tooinstall hello Azure Recovery Services Agent, que deve toobe instalado em cada host Hyper-V. [Saiba mais](site-recovery-hyper-v-azure-architecture.md) para obter mais informações.

![Implantação de site do Virtual Machine Manager para replicação entre localizações locais e o Azure](media/site-recovery-monitoring-and-troubleshooting/image2.png)

### <a name="hyper-v-site-deployment-for-replication-between-on-premises-locations-and-azure"></a>Implantação de site do Hyper-V para replicação entre pontos locais e o Azure
Esse processo é semelhante implantação do Gerenciador de máquina de tooVirtual. Olá única diferença é que o provedor do Azure Site Recovery hello e Azure Recovery Services Agent obtenham instalados no host do Hyper-V Olá em si. [Saiba mais](site-recovery-hyper-v-azure-architecture.md). .

## <a name="monitor-configuration-protection-and-recovery-operations"></a>Monitorar as operações de configuração, proteção e recuperação
Cada operação no Azure Site Recovery é auditada e rastreada em Olá **trabalhos** guia. Para qualquer configuração, proteção ou erro de recuperação, vá toohello **trabalhos** guia e procure falhas.

![filtro de falha de saudação na guia trabalhos da saudação](media/site-recovery-monitoring-and-troubleshooting/image3.png)

Se você encontrar falhas em Olá **trabalhos** guia, clique em trabalho hello e clique em **detalhes do erro** para esse trabalho.

![botão de detalhes do erro Olá](media/site-recovery-monitoring-and-troubleshooting/image4.png)

detalhes do erro Olá ajudará você a identificar uma possível causa e a recomendação para problema de saudação.

![Caixa de diálogo que mostra os detalhes de erro de um trabalho específico](media/site-recovery-monitoring-and-troubleshooting/image5.png)

No exemplo anterior de saudação, outra operação está em andamento parece toobe causando Olá toofail de configuração de proteção. Resolver o problema Olá com base na recomendação de saudação e, em seguida, clique em **RESART** tooinitiate a operação de saudação novamente.

![botão de reinicialização Olá na guia trabalhos da saudação](media/site-recovery-monitoring-and-troubleshooting/image6.png)

Olá **reiniciar** opção não está disponível para todas as operações. Se uma operação não tem Olá **reiniciar** opção, volte objeto toohello e refazer Olá novamente. Você pode cancelar qualquer trabalho que está em andamento usando Olá **Cancelar** botão.

![botão Cancelar Olá](media/site-recovery-monitoring-and-troubleshooting/image7.png)

## <a name="monitor-replication-health-for-virtual-machines"></a>Monitorar a integridade da replicação para máquinas virtuais
Você pode usar provedores de Azure Site Recovery de monitor do hello tooremotely portal do Azure para cada uma das entidades Olá protegido. Clique em **ITENS PROTEGIDOS** e, em seguida, clique em **NUVENS DO VMM** ou **GRUPOS DE PROTEÇÃO**. Olá **NUVENS do VMM** guia só está disponível para implantações que estão baseadas no Gerenciador de máquina Virtual. Para outros cenários, entidades Olá protegido estão sob Olá **grupos de proteção** guia.

![Opções de saudação nuvens do VMM e grupos de proteção](media/site-recovery-monitoring-and-troubleshooting/image8.png)

Clique em uma entidade protegida em Olá respectiva nuvem ou proteção grupo toosee que todas as operações disponíveis são mostradas no painel inferior de saudação.

![Opções disponíveis para uma entidade protegida selecionada](media/site-recovery-monitoring-and-troubleshooting/image9.png)

Conforme mostrado na captura de tela anterior hello, integridade da máquina virtual Olá é **crítico**. Você pode clicar em Olá **detalhes do erro** botão no erro de Olá Olá inferior toosee. Com base em Olá **possíveis causas** e **recomendação**, resolva o problema de saudação.

![botão de detalhes do erro Olá](media/site-recovery-monitoring-and-troubleshooting/image10.png)

![Erros e as recomendações na caixa de diálogo Detalhes do erro Olá](media/site-recovery-monitoring-and-troubleshooting/image11.png)

> [!NOTE]
> Se quaisquer operações ativas em andamento ou falhou, vá toohello **trabalhos** exibição como anteriores tooview Olá erro para um trabalho específico.
>
>

## <a name="troubleshoot-on-premises-hyper-v-issues"></a>Solucionar problemas do Hyper-V no local
Conectar o console do Gerenciador Hyper-V toohello local, Olá selecione máquina de virtual e consulte a integridade da replicação hello.

![Integridade da replicação tooview opção no console do Gerenciador de saudação Hyper-V](media/site-recovery-monitoring-and-troubleshooting/image12.png)

Neste caso, a **Integridade da Replicação** é **Crítica**. Clique com botão direito a máquina virtual de saudação e, em seguida, clique em **replicação** > **exibir integridade da replicação** toosee detalhes de saudação.

![Integridade da replicação para uma máquina virtual específica](media/site-recovery-monitoring-and-troubleshooting/image13.png)

Se a replicação está em pausa de máquina virtual de saudação, clique a máquina virtual de saudação e, em seguida, clique em **replicação** > **retomar replicação**.

![Opção de replicação tooresume no console do Gerenciador de saudação Hyper-V](media/site-recovery-monitoring-and-troubleshooting/image19.png)

Se uma máquina virtual migra de um novo host do Hyper-V que está dentro do cluster hello ou em um computador autônomo e o host do Hyper-V Olá tiver sido configurado por meio do Azure Site Recovery, a replicação da máquina virtual de saudação não ser afetada. Certifique-se de host Hyper-V novo Olá atende a todos os pré-requisitos de saudação e é configurada por meio do Azure Site Recovery.

### <a name="event-log"></a>Log de Eventos
| Origens de eventos | Detalhes |
| --- |:--- |
| **Applications and Service Logs/Microsoft/VirtualMachineManager/Server/Admin** (servidor do Virtual Machine Manager) |Fornece log útil tootroubleshoot muitas questões do Virtual Machine Manager. |
| **Applications and Service Logs/MicrosoftAzureRecoveryServices/Replication** (host Hyper-V) |Fornece log útil tootroubleshoot muitos problemas de agente de serviços de recuperação do Microsoft Azure. <br/> ![Local da origem do evento de replicação para o host Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer03.png) |
| **Applications and Service Logs/Microsoft/Azure Site Recovery/Provider/Operational** (host Hyper-V) |Fornece log útil tootroubleshoot muitos problemas de serviço do Microsoft Azure Site Recovery. <br/> ![Local da origem do evento operacional do host do Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer02.png) |
| **Applications and Service Logs/Microsoft/Windows/Hyper-V-VMMS/Admin** (host Hyper-V) |Fornece log útil tootroubleshoot muitos problemas de gerenciamento de máquina virtual de Hyper-V. <br/> ![Local de origem do evento do Virtual Machine Manager para o host Hyper-V](media/site-recovery-monitoring-and-troubleshooting/eventviewer01.png) |

### <a name="hyper-v-replication-logging-options"></a>Opções de registro em log de replicação do Hyper-V
Todos os eventos que pertencem a replicação tooHyper-V são registrados no hello Hyper-V-VMMS\\Admin log localizado em Applications and Services Logs\\Microsoft\\Windows. Além disso, você pode habilitar um log analítico de saudação serviço de gerenciamento de máquina Virtual do Hyper-V. tooenable logon, faça primeiro Olá analítico e depuração logs podem ser exibidos no Visualizador de eventos de saudação. Abra Visualizador de Eventos e, em seguida, clique em **Exibir** > **Mostrar Logs Analíticos e de Depuração**.

![Olá opção Mostrar Logs analíticos e de depuração](media/site-recovery-monitoring-and-troubleshooting/image14.png)

Um log Analítico está visível em **VMMS do Hyper-V**.

![Olá analítico de log na árvore de Visualizador de eventos Olá](media/site-recovery-monitoring-and-troubleshooting/image15.png)

Em Olá **ações** painel, clique em **Habilitar Log**. Depois de habilitado, ele é exibido no **Monitor de Desempenho** como uma **Sessão de Rastreamento de Evento** localizada em **Conjuntos de Coletores de Dados**.

![Sessões de rastreamento de eventos na árvore do Monitor de desempenho de saudação](media/site-recovery-monitoring-and-troubleshooting/image16.png)

tooview Olá informações coletadas, primeiro interrompa a sessão de rastreamento de saudação desabilitando o log de saudação. Salvar log de saudação e abri-lo novamente no Visualizador de eventos ou usar outra ferramentas tooconvert-lo conforme desejado.

## <a name="reach-out-for-microsoft-support"></a>Entre em contato com o Suporte da Microsoft
### <a name="log-collection"></a>Coleta de logs
Para proteção de locais do Virtual Machine Manager, consulte muito[coleta de log do Azure Site Recovery usando a ferramenta de diagnóstico de suporte à plataforma (SDP)](http://social.technet.microsoft.com/wiki/contents/articles/28198.asr-data-collection-and-analysis-using-the-vmm-support-diagnostics-platform-sdp-tool.aspx) toocollect Olá necessário logs.

Para proteção de site do Hyper-V, baixe o [ferramenta](https://dcupload.microsoft.com/tools/win7files/DIAG_ASRHyperV_global.DiagCab) e executá-lo em Olá Hyper-V host toocollect Olá logs.

Para cenários de servidor do VMware/físicos, consulte muito[coleta de log do Azure Site Recovery para VMware e proteção do local físico](http://social.technet.microsoft.com/wiki/contents/articles/30677.azure-site-recovery-log-collection-for-vmware-and-physical-site-protection.aspx) toocollect Olá necessário logs.

ferramenta de saudação coleta logs Olá localmente em uma subpasta nomeada aleatoriamente em % LocalAppData%\ElevatedDiagnostics.

![Etapas de exemplo mostradas da proteção de site do Hyper-V.](media/site-recovery-monitoring-and-troubleshooting/animate01.gif)

### <a name="open-a-support-ticket"></a>Abra um tíquete de suporte
tooraise um tíquete de suporte para o Azure Site Recovery, alcançar tooAzure suporte usando a URL em <http://aka.ms/getazuresupport>.

## <a name="kb-articles"></a>Artigos da Base de Dados de Conhecimento
* [Como a letra da unidade toopreserve Olá para protegido máquinas virtuais que fizeram failover ou migrados tooAzure](http://support.microsoft.com/kb/3031135)
* [Como toomanage local tooAzure uso de largura de banda de rede de proteção](https://support.microsoft.com/kb/3056159)
* [Erro do Azure Site Recovery: "hello cluster recurso não pôde ser encontrado" quando você tentar tooenable proteção para uma máquina virtual](http://support.microsoft.com/kb/3010979)
* [Guia para Compreender e solucionar problemas de replicação do Hyper-V](http://social.technet.microsoft.com/wiki/contents/articles/21948.hyper-v-replica-troubleshooting-guide.aspx)

## <a name="common-azure-site-recovery-errors-and-their-resolutions"></a>Erros comuns do Azure Site Recovery e suas resoluções
A seguir estão os erros comuns e suas resoluções. Cada erro é documentado em uma página separada do wiki.

### <a name="general"></a>Geral
* <span style="color:green;">NOVO</span> [Trabalhos que falham com um erro "Operação em andamento". Erros 505, 514, 532.](http://social.technet.microsoft.com/wiki/contents/articles/32190.azure-site-recovery-jobs-failing-with-error-an-operation-is-in-progress-error-505-514-532.aspx)
* <span style="color:green;">NOVO</span> [trabalhos falha com o erro "O servidor não está conectado toohello Internet". Erro 25018.](http://social.technet.microsoft.com/wiki/contents/articles/32192.azure-site-recovery-jobs-failing-with-error-server-isn-t-connected-to-the-internet-error-25018.aspx)

### <a name="setup"></a>Configuração
* [servidor do Virtual Machine Manager Olá não pode ser registrado devido a erro interno tooan. Consulte toohello o modo de exibição de trabalhos no portal de recuperação de Site Olá para obter mais detalhes sobre o erro de saudação. Execute a instalação do servidor de saudação tooregister novamente.](http://social.technet.microsoft.com/wiki/contents/articles/25570.the-vmm-server-cannot-be-registered-due-to-an-internal-error-please-refer-to-the-jobs-view-in-the-site-recovery-portal-for-more-details-on-the-error-run-setup-again-to-register-the-server.aspx)
* [Uma conexão não pode ser estabelecida toohello Hyper-V Recovery Manager cofre. Verifique se as configurações de proxy de saudação ou tente novamente mais tarde.](http://social.technet.microsoft.com/wiki/contents/articles/25571.a-connection-cant-be-established-to-the-hyper-v-recovery-manager-vault-verify-the-proxy-settings-or-try-again-later.aspx)

### <a name="configuration"></a>Configuração
* [Não é possível toocreate grupo de proteção: Ocorreu um erro ao recuperar a lista de saudação de servidores.](http://blogs.technet.com/b/somaning/archive/2015/08/12/unable-to-create-the-protection-group-in-azure-site-recovery-portal.aspx)
* [Cluster de host Hyper-V contém pelo menos um adaptador de rede estático, ou nenhum adaptador conectado está configurado toouse DHCP.](http://social.technet.microsoft.com/wiki/contents/articles/25498.hyper-v-host-cluster-contains-at-least-one-static-network-adapter-or-no-connected-adapters-are-configured-to-use-dhcp.aspx)
* [O Virtual Machine Manager não tem permissões toocomplete uma ação.](http://social.technet.microsoft.com/wiki/contents/articles/31110.vmm-does-not-have-permissions-to-complete-an-action.aspx)
* [Não é possível selecionar a conta de armazenamento de saudação em assinatura Olá ao configurar a proteção.](http://social.technet.microsoft.com/wiki/contents/articles/32027.can-t-select-the-storage-account-within-the-subscription-while-configuring-protection.aspx)

### <a name="protection"></a>Proteção
* <span style="color:green;">NOVO</span> [Habilitar proteção falha com o erro "Não foi possível configurar a proteção para a máquina virtual de Olá". Erros 60007, 40003.](http://social.technet.microsoft.com/wiki/contents/articles/32194.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-configured-for-the-virtual-machine-error-60007-40003.aspx)
* <span style="color:green;">NOVO</span> [Habilitar proteção falha com o erro "Não foi possível habilitar a proteção para a máquina virtual de hello." Erro 70094.](http://social.technet.microsoft.com/wiki/contents/articles/32195.azure-site-recovery-enable-protection-failing-with-error-protection-couldn-t-be-enabled-for-the-virtual-machine-error-70094.aspx)
* <span style="color:green;">NOVO</span> [erro de migração ao vivo 23848 - Olá VM será toobe movida usando o tipo ao vivo. Isso poderia interromper o status de proteção de recuperação de saudação da máquina virtual de saudação.](http://social.technet.microsoft.com/wiki/contents/articles/32021.live-migration-error-23848-the-virtual-machine-is-going-to-be-moved-using-type-live-this-could-break-the-recovery-protection-status-of-the-virtual-machine.aspx)
* [Falha na habilitação da proteção, pois o Agente não está instalado no computador host.](http://social.technet.microsoft.com/wiki/contents/articles/31105.enable-protection-failed-since-agent-not-installed-on-host-machine.aspx)
* [Não é possível encontrar um host adequado Olá máquina virtual de réplica - devido a recursos de computação toolow.](http://social.technet.microsoft.com/wiki/contents/articles/25501.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-low-compute-resources.aspx)
* [Não é possível encontrar um host adequado Olá máquina virtual de réplica - devido toono conectado à rede lógica.](http://social.technet.microsoft.com/wiki/contents/articles/25502.a-suitable-host-for-the-replica-virtual-machine-can-t-be-found-due-to-no-logical-network-attached.aspx)
* [Não é possível conectar o computador de host de réplica toohello - não foi possível estabelecer a conexão.](http://social.technet.microsoft.com/wiki/contents/articles/31106.cannot-connect-to-the-replica-host-machine-connection-could-not-be-established.aspx)

### <a name="recovery"></a>Recuperação
* O Virtual Machine Manager não pode concluir a operação de host de saudação:
  * [Ponto de recuperação toohello selecionado para a máquina virtual para failover: geral erro de acesso negado.](http://social.technet.microsoft.com/wiki/contents/articles/25504.fail-over-to-the-selected-recovery-point-for-virtual-machine-general-access-denied-error.aspx)
  * [Toofail com falha do Hyper-V em toohello selecionado de ponto de recuperação para a máquina virtual: operação cancelada.  Tente um ponto de recuperação mais recente. (0x80004004).](http://social.technet.microsoft.com/wiki/contents/articles/25503.hyper-v-failed-to-fail-over-to-the-selected-recovery-point-for-virtual-machine-operation-aborted-try-a-more-recent-recovery-point-0x80004004.aspx)
  * Uma conexão com o servidor de saudação não pôde ser estabelecida (0x00002EFD).
    * [Hyper-V falha tooenable a replicação inversa da máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25505.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-reverse-replication-for-virtual-machine.aspx)
    * [Replicação tooenable com falha do Hyper-V para a máquina virtual de máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25506.a-connection-with-the-server-could-not-be-established-0x00002efd-hyper-v-failed-to-enable-replication-for-virtual-machine-virtual-machine.aspx)
  * [Não foi possível confirmar o failover para a máquina virtual.](http://social.technet.microsoft.com/wiki/contents/articles/25508.could-not-commit-failover-for-virtual-machine.aspx)
* [plano de recuperação de saudação contém máquinas virtuais que não estão prontas para failover planejado.](http://social.technet.microsoft.com/wiki/contents/articles/25509.the-recovery-plan-contains-virtual-machines-which-are-not-ready-for-planned-failover.aspx)
* [máquina virtual de saudação não está pronta para failover planejado.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* [A máquina virtual não está em execução e não está desligada.](http://social.technet.microsoft.com/wiki/contents/articles/25510.virtual-machine-is-not-running-and-is-not-powered-off.aspx)
* [Ocorreu uma operação fora de banda em uma máquina virtual e não foi possível confirmar o failover.](http://social.technet.microsoft.com/wiki/contents/articles/25507.the-virtual-machine-isn-t-ready-for-planned-failover.aspx)
* Failover de Teste
  * [Não foi possível iniciar o failover, pois o failover de teste está em andamento.](http://social.technet.microsoft.com/wiki/contents/articles/31111.failover-could-not-be-initiated-since-test-failover-is-in-progress.aspx)
* <span style="color:green;">NOVO</span> Failover o tempo limite 'PreFailoverWorkflow task WaitForScriptExecutionTaskTimeout' devido a configurações de toohello no hello grupo de segurança de rede associado à saudação Máquina Virtual ou máquinas de Olá Olá sub-redes toowhich pertence. Consulte também['PreFailoverWorkflow task WaitForScriptExecutionTaskTimeout'](https://aka.ms/troubleshoot-nsg-issue-azure-site-recovery) para obter detalhes.

### <a name="configuration-server-process-server-master-target"></a>Servidor de configuração, servidor de processo, destino mestre
* [host de ESXi Olá no qual Olá PS/CS está hospedado como uma VM falhará com uma tela roxa de morte.](http://social.technet.microsoft.com/wiki/contents/articles/31107.vmware-esxi-host-experiences-a-purple-screen-of-death.aspx)

### <a name="remote-desktop-troubleshooting-after-failover"></a>Solução de problemas da área de trabalho remota após failover
* Muitos clientes enfrentam problemas tooconnect toohello failover da máquina virtual no Azure. [Saudação de uso tooRDP de documento de solução de problemas na máquina virtual de saudação](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx).

#### <a name="adding-a-public-ip-on-a-resource-manager-virtual-machine"></a>Adicionando um IP público em uma máquina virtual do Gerenciador de recursos
Se hello **conectar** botão no portal de saudação estiver esmaecido e não são tooAzure conectado por meio de uma conexão VPN Site a Site ou de rota expressa, você precisa toocreate e atribuir um endereço IP público de sua máquina virtual antes de usar remoto Shell de área de trabalho/compartilhado. Em seguida, você pode adicionar um IP público na interface de rede de saudação da máquina virtual de saudação.  

![Falha ao adicionar um IP público na interface de rede de saudação de máquina virtual com failover](media/site-recovery-monitoring-and-troubleshooting/createpublicip.gif)
