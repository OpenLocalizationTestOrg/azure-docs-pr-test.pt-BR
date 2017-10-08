---
title: "Solucionar problemas de falha de Backup do Azure: indisponível no status de agente convidado | Microsoft Docs"
description: "Sintomas, causas e resoluções de tooerror relacionado de falhas de Backup do Azure: não pôde se comunicar com o agente de VM Olá"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: Backup do Azure; agente da VM; conectividade de rede;
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: genli;markgal;
ms.openlocfilehash: 724c61ba80d0a9ef91a5f8543ae72bb86968881b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Solucionar problemas de falha de Backup do Azure: problemas com o agente e/ou extensão

Este artigo fornece toohelp de etapas para solução de problemas resolver falhas de Backup relacionados tooproblems na comunicação com o agente de VM e a extensão.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-toocommunicate-with-azure-backup"></a>Agente de VM de toocommunicate não é possível com o Backup do Azure
Depois de registrar e agendar uma VM para Olá serviço Backup do Azure, o Backup inicia o trabalho de saudação comunicando-se com hello VM agent tootake um instantâneo point-in-time. Qualquer uma das seguintes condições de saudação pode impedir que o instantâneo de saudação do que está sendo disparado, que por sua vez, pode levar tooBackup falha. Seguem abaixo Olá considerando a ordem de etapas de solução de problemas e repita a operação.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Olá VM tem sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [agente hello está instalado no hello VM, mas não está respondendo (para máquinas virtuais do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente Olá instalado na VM de saudação está desatualizado (para VMs do Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [não é possível recuperar o status de saudação do instantâneo ou um instantâneo não pode ser realizado](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [falha de extensão de backup Olá tooupdate ou carga](#the-backup-extension-fails-to-update-or-load)

## <a name="snapshot-operation-failed-due-toono-network-connectivity-on-hello-virtual-machine"></a>Falha na operação de instantâneo devido toono conectividade de rede na máquina virtual de saudação
Depois de registrar e agendar uma VM para Olá serviço Backup do Azure, o Backup inicia o trabalho de saudação comunicando-se com o instantâneo de tootake um point-in-time de extensão de backup de VM hello. Qualquer uma das seguintes condições de saudação pode impedir que o instantâneo de saudação do que está sendo disparado, que por sua vez, pode levar tooBackup falha. Seguem abaixo Olá considerando a ordem de etapas de solução de problemas e repita a operação.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Olá VM tem sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 2: [não é possível recuperar o status de saudação do instantâneo ou um instantâneo não pode ser realizado](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 3: [falha de extensão de backup Olá tooupdate ou carga](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Falha na operação da extensão de VMSnapshot

Depois de registrar e agendar uma VM para Olá serviço Backup do Azure, o Backup inicia o trabalho de saudação comunicando-se com o instantâneo de tootake um point-in-time de extensão de backup de VM hello. Qualquer uma das seguintes condições de saudação pode impedir que o instantâneo de saudação do que está sendo disparado, que por sua vez, pode levar tooBackup falha. Seguem abaixo Olá considerando a ordem de etapas de solução de problemas e repita a operação.
##### <a name="cause-1-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 1: [não é possível recuperar o status de saudação do instantâneo ou um instantâneo não pode ser realizado](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 2: [falha de extensão de backup Olá tooupdate ou carga](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [Olá VM tem sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 4: [agente hello está instalado no hello VM, mas não está respondendo (para máquinas virtuais do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 5: [agente Olá instalado na VM de saudação está desatualizado (para VMs do Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-tooperform-hello-operation-as-hello-vm-agent-is-not-responsive"></a>Operação tooperform não é possível Olá Olá agente de VM não está respondendo

Depois de registrar e agendar uma VM para Olá serviço Backup do Azure, o Backup inicia o trabalho de saudação comunicando-se com o instantâneo de tootake um point-in-time de extensão de backup de VM hello. Qualquer uma das seguintes condições de saudação pode impedir que o instantâneo de saudação do que está sendo disparado, que por sua vez, pode levar tooBackup falha. Seguem abaixo Olá considerando a ordem de etapas de solução de problemas e repita a operação.
##### <a name="cause-1-hello-agent-is-installed-in-hello-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 1: [agente hello está instalado no hello VM, mas não está respondendo (para máquinas virtuais do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 2: [agente Olá instalado na VM de saudação está desatualizado (para VMs do Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [Olá VM tem sem acesso à Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-hello-operation-in-a-few-minutes"></a>Falha no backup com um erro interno - tente novamente realizar a operação Olá em poucos minutos

Depois de registrar e agendar uma VM para Olá serviço Backup do Azure, o Backup inicia o trabalho de saudação comunicando-se com o instantâneo de tootake um point-in-time de extensão de backup de VM hello. Qualquer uma das seguintes condições de saudação pode impedir que o instantâneo de saudação do que está sendo disparado, que por sua vez, pode levar tooBackup falha. Seguem abaixo Olá considerando a ordem de etapas de solução de problemas e repita a operação.
##### <a name="cause-1-hello-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [Olá VM tem sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [agente de saudação instalado no hello VM, mas sem resposta (para máquinas virtuais do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [agente Olá instalado na VM de saudação está desatualizado (para VMs do Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [não é possível recuperar o status de saudação do instantâneo ou um instantâneo não pode ser realizado](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-hello-backup-extension-fails-tooupdate-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [falha de extensão de backup Olá tooupdate ou carga](#the-backup-extension-fails-to-update-or-load)


## <a name="causes-and-solutions"></a>Causas e soluções

### <a name="hello-vm-has-no-internet-access"></a>Olá VM tem sem acesso à Internet
Por exigência de implantação de Olá Olá VM tem sem acesso à Internet ou tem restrições que impedem o acesso toohello infraestrutura do Azure.

toofunction corretamente, Olá backup extensão requer conectividade toohello endereços de IP público do Azure. extensão de saudação envia comandos instantâneos de saudação de toomanage tooan armazenamento do Azure (URL de HTTP) do ponto de extremidade de saudação VM. Se a extensão de saudação estiver sem toohello acesso que Internet pública, Backup poderá falha.

####  <a name="solution"></a>Solução
problema de saudação tooresolve, tente um dos métodos de saudação listados aqui.
##### <a name="allow-access-toohello-azure-datacenter-ip-ranges"></a>Permitir acesso toohello intervalos IP de datacenter do Azure

1. Obter Olá [lista de IPs do datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) tooallow acessem.
2. Desbloquear Olá IPs executando Olá **New-NetRoute** cmdlet Olá VM do Azure em uma janela elevada do PowerShell. Execute o cmdlet do hello como um administrador.
3. tooallow acesso toohello IPs, adicione o grupo de segurança de rede de toohello de regras, se você tiver um.

##### <a name="create-a-path-for-http-traffic-tooflow"></a>Criar um caminho para tooflow de tráfego HTTP

1. Se você tiver restrições de rede no local (por exemplo, um grupo de segurança de rede), implante um tráfego de saudação de tooroute do servidor de proxy HTTP.
2. tooallow acesso toohello da Internet do servidor de proxy HTTP hello, adicionar grupo de segurança de rede de toohello de regras, se você tiver um.

toolearn como tooset um proxy HTTP para backups VM, consulte [preparar seu tooback ambiente backup de máquinas virtuais do Azure](backup-azure-vms-prepare.md#using-an-http-proxy-for-vm-backups).

Caso você esteja usando discos gerenciados, talvez seja necessário uma porta adicional (8443) abrindo nos firewalls hello.

### <a name="hello-agent-installed-in-hello-vm-but-unresponsive-for-windows-vms"></a>Agente de saudação instalado no hello VM, mas sem resposta (para máquinas virtuais do Windows)

#### <a name="solution"></a>Solução
Olá agente de VM pode ter sido corrompido ou serviço Olá deve ter sido interrompido. Agente VM Olá reinstalar ajudaria obter versão mais recente do hello e reinicie a comunicação de saudação.

1. Verifique se o serviço de agente de convidado do Windows está em execução nos serviços (services.msc) do hello Máquina Virtual. Tente reiniciar o serviço de agente de convidado do Windows hello e iniciar Olá Backup<br>
2. Se não estiver visível em serviços, verifique em Programas e Recursos se o serviço de agente Convidado do Windows está instalado.
4. Se você é capaz de tooview em programas e recursos Olá desinstalar o agente de convidado do Windows.
5. Baixe e instale Olá [versão mais recente do agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisa de instalação de saudação do toocomplete de privilégios de administrador.
6. Em seguida, você deve ser capaz de tooview serviços de agente de convidado do Windows nos serviços de
7. Tente executar um backup na demanda/adhoc clicando em "Fazer Backup agora" no portal de saudação.

Verifique também se sua máquina Virtual possui  **[.NET 4.5 instalado no sistema de saudação](https://docs.microsoft.com/en-us/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. Ele é necessário para Olá toocommunicate de agente VM com o serviço de saudação

### <a name="hello-agent-installed-in-hello-vm-is-out-of-date-for-linux-vms"></a>Agente de Olá instalado na VM de saudação está desatualizado (para VMs do Linux)

#### <a name="solution"></a>Solução
A maioria das falhas relacionadas ao agente ou relacionadas à extensão para VMs do Linux é causada por problemas que afetam um agente de VM desatualizado. tootroubleshoot esse problema, siga estas diretrizes gerais:

1. Siga as instruções de saudação de [atualização Olá agente de VM do Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Estamos *altamente recomendável* que você atualize o agente Olá somente por meio de um repositório de distribuição. Não é recomendável baixar o código de saudação do agente diretamente do GitHub e atualizá-lo. Se o agente mais recente Olá não está disponível para a sua distribuição, contate o suporte de distribuição para obter instruções sobre como tooinstall-lo. toocheck hello mais recente do agente do, vá toohello [agente Linux do Windows Azure](https://github.com/Azure/WALinuxAgent/releases) página no repositório do GitHub hello.

2. Certifique-se de que Olá agente do Azure está em execução no hello VM executando Olá comando a seguir:`ps -e`

 Se o processo de saudação não está em execução, reinicie-o usando Olá comandos a seguir:

 * Para o Ubuntu: `service walinuxagent start`
 * Para outras distribuições: `service waagent start`

3. [Configurar o agente de reinicialização automática Olá](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Execute um novo backup de teste. Se Olá falha persistir, reúna Olá seguintes logs de VM do cliente hello:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Se precisarmos do registro detalhado para waagent, siga estas etapas:

1. No arquivo de /etc/waagent.conf de hello, localize a seguinte linha de saudação: **Habilitar log detalhado (y | n)**
2. Saudação de alteração **Logs.Verbose** valor  *n*  muito*y*.
3. Salvar alterações de saudação e reinicie waagent seguindo as etapas anteriores Olá nesta seção.

### <a name="hello-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>não é possível recuperar o status de saudação do instantâneo ou um instantâneo não pode ser realizado
backup de VM Olá se baseia na emissão de uma conta de armazenamento subjacente do instantâneo comando toohello. Backup poderá falhar porque ele tem nenhuma conta de armazenamento toohello acesso ou execução de saudação da tarefa de instantâneo hello está atrasada.

#### <a name="solution"></a>Solução
Olá seguintes condições pode causar a falha de tarefa de instantâneo:

| Causa | Solução |
| --- | --- |
| Olá VM tenha configurado o backup do SQL Server. | Por padrão, o backup de VM Olá executa um backup completo de VSS em VMs do Windows. Em VMs que executam servidores baseados no SQL Server e em que o backup do SQL Server está configurado, podem ocorrer atrasos na execução do instantâneo.<br><br>Se houver uma falha de Backup devido a um problema instantâneo, defina Olá chave do registro a seguir:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| Olá status da VM é informada incorretamente como Olá VM for desligada no RDP. | Se você desligar Olá VM no protocolo de área de trabalho remota (RDP), verifique toodetermine portal Olá se Olá status da VM está correto. Se não estiver correto, desligue o hello VM no portal de saudação usando Olá **desligamento** opção no painel VM hello. |
| Muitas máquinas virtuais de saudação são do mesmo serviço de nuvem configurado tooback backup no hello simultaneamente. | É um toospread de prática recomendada out agendas de backup Olá para VMs de saudação mesmo serviço de nuvem. |
| Olá VM está em execução com alto uso de CPU ou memória. | Se Olá VM estiver em execução no uso intenso da CPU (mais de 90 por cento) ou alto uso da memória, Olá instantâneo tarefa em fila e atrasada, e finalmente o tempo limite. Nessa situação, tente um backup sob demanda. |
| Olá VM não é possível obter o endereço de host de malha de saudação do DHCP. | DHCP deve ser habilitado no convidado Olá Olá toowork backup de VM de IaaS.  Se hello VM não é possível obter endereço de host de malha de saudação da resposta DHCP 245, ele não pode baixar ou executar as extensões. Se você precisar de um endereço IP privado estático, você deve configurá-lo por meio da plataforma hello. Olá opção DHCP dentro Olá VM deve ser deixada habilitado. Para saber mais, veja [Definição de um IP interno estático privado](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="hello-backup-extension-fails-tooupdate-or-load"></a>Olá tooupdate de falha de extensão de backup ou de carga
Se as extensões não puderem ser carregadas, o Backup falhará porque não é possível obter um instantâneo.

#### <a name="solution"></a>Solução

**Para convidados do Windows:** Verifique se o hello iaasvmprovider está habilitado e tem um tipo de inicialização *automática*. Se o serviço de saudação não está configurado dessa forma, habilite toodetermine se o próximo backup de saudação for bem-sucedida.

**Para convidados do Linux:** verificar Olá versão mais recente VMSnapshot para Linux (extensão de saudação usada pelo Backup) é 1.0.91.0.<br>


Se extensão backup Olá não tooupdate ou carga, você pode forçar Olá VMSnapshot extensão toobe recarregado Desinstalando extensão hello. próxima tentativa de backup Olá recarregará extensão hello.

toouninstall Olá extensão, Olá a seguir:

1. Vá toohello [portal do Azure](https://portal.azure.com/).
2. Localize Olá VM que tem problemas de backup.
3. Clique em **Configurações**.
4. Clique em **Extensões**.
5. Clique em **Extensão Vmsnapshot**.
6. Clique em **Desinstalar**.

Este procedimento faz com que Olá extensão toobe reinstalado durante o próximo backup de saudação.

