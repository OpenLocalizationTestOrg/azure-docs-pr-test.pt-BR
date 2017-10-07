---
title: "erros de backup aaaTroubleshoot com a máquina virtual do Azure | Microsoft Docs"
description: "Solucionar problemas de backup e restauração de máquinas virtuais do Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 73214212-57a4-4b57-a2e2-eaf9d7fde67f
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: trinadhk;markgal;jpallavi;
ms.openlocfilehash: 9224c47e02b52688adcba5876c674c88502557c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Solucionar problemas de backup de máquinas virtuais do Azure
> [!div class="op_single_selector"]
> * [Cofre dos serviços de recuperação](backup-azure-vms-troubleshoot.md)
> * [Cofre de backup](backup-azure-vms-troubleshoot-classic.md)
>
>

Você pode solucionar problemas de erros encontrados ao usar o Backup do Azure com informações listadas na tabela de saudação abaixo.

## <a name="backup"></a>Backup
| Detalhes do erro | Solução alternativa |
| --- | --- |
| Não foi possível executar a operação de saudação como VM não existe mais. - Pare a proteção da máquina virtual sem excluir os dados de backup. Mais detalhes em http://go.microsoft.com/fwlink/?LinkId=808124 |Isso acontece quando hello VM primária é excluído, mas a política de backup Olá continua procurando tooback uma VM para cima. toofix este erro: <ol><li> Recriar a máquina virtual Olá Olá mesmo nome e o mesmo nome do grupo de recursos [nome do serviço de nuvem,]<br>(OU)</li><li> Interrompa a proteção de máquina virtual com ou sem excluir os dados de backup hello. [Mais detalhes:](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Operação de instantâneo falhou devido a conectividade de rede toono na máquina de virtual Olá - Certifique-se de que a VM tem acesso à rede. Para instantâneo toosucceed, ou lista branca de IPS do datacenter Azure intervalos ou configurar um servidor proxy para acesso à rede. Para obter mais detalhes, consulte muito http://go.microsoft.com/fwlink/?LinkId=800034. Se já estiver usando um servidor proxy, verifique se as configurações dele foram definidas corretamente | Esse erro é gerado quando você negar Olá saída conectividade com a internet na máquina virtual de saudação. Conectividade com a Internet é necessária para a VM instantâneo extensão tootake um instantâneo dos discos subjacentes da máquina virtual de saudação. [Saiba mais](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine) em como toofix instantâneo falhas devido tooblocked acesso à rede. |
| Agente de VM é toocommunicate não é possível com hello Azure Backup Service. -Verifique Olá VM tem conectividade de rede e o agente de VM Olá está em execução e mais recentes. Para obter mais informações, consulte muito http://go.microsoft.com/fwlink/?LinkId=800034 |Esse erro é gerado se há um problema com hello agente de VM ou toohello de acesso de rede infraestrutura do Azure é bloqueado de alguma forma. [Saiba mais](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vm-agent-unable-to-communicate-with-azure-backup) sobre depuração de problemas de instantâneo de VM.<br> Se o agente de VM Olá não está causando problemas, reinicie Olá VM. Às vezes um estado VM incorreto pode causar problemas, e reiniciar Olá VM redefine essa "estado inválido". |
| VM está em estado de provisionamento de falha - reinicie Olá VM e certifique-se de que Olá que VM está em estado de execução ou desligado para backup | Isso ocorre quando uma das falhas de extensão Olá leva toobe de estado da máquina virtual em estado de provisionamento com falha. Vá tooextensions lista e ver se há uma extensão com falha, removê-lo e tente reiniciar a máquina virtual de saudação. Se todas as extensões estiverem em estado de execução, verifique se o serviço de agente da VM está em execução. Caso contrário, reinicie o serviço de agente VM hello. | 
| Operação de extensão VMSnapshot falha para discos gerenciados - operação de backup de saudação de repetição. Se o problema de saudação se repetir, siga as instruções de saudação em 'http://go.microsoft.com/fwlink/?LinkId=800034'. Se ocorrer uma nova falha, entre em contato com o suporte da Microsoft | Esse erro quando o serviço de Backup do Azure não tootrigger um instantâneo. [Saiba mais](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#vmsnapshot-extension-operation-failed) sobre como depurar problemas de instantâneo de VM. |
| Pode não instantâneo de saudação cópia da máquina virtual do hello, devido a espaço livre de tooinsufficient na conta de armazenamento Olá - Certifique-se de que a conta de armazenamento tem espaço livre equivalente toohello dados presentes nos discos de armazenamento premium Olá anexado toohello virtual machine | No caso de VMs premium, podemos copiar conta de toostorage Olá instantâneo. Isso é toomake-se de que o tráfego de gerenciamento de backup, que funciona em instantâneo, não limita o número de Olá IOPS toohello disponíveis do aplicativo de usando discos premium. A Microsoft recomenda que você alocar apenas 50% do espaço de conta de armazenamento total Olá para que Olá serviço Backup do Azure possa copiar Olá toostorage conta e a transferência de dados do instantâneo deste local copiado no cofre de toohello de conta de armazenamento. | 
| Operação de Olá tooperform não é possível como agente de VM Olá não está respondendo |Esse erro é gerado se há um problema com hello agente de VM ou toohello de acesso de rede infraestrutura do Azure é bloqueado de alguma forma. Para VMs do Windows, verificar o status do serviço de agente do hello VM em serviços e se o agente de saudação aparece em programas, no painel de controle. Tente remover o programa saudação do controle de painel e reinstalá Olá agente conforme mencionado [abaixo](#vm-agent). Após a reinstalação agente hello, disparar uma tooverify de backup ad hoc. |
| Falha na operação de extensão dos serviços de recuperação. -Verifique se o agente mais recente da máquina virtual está presente na máquina virtual de saudação e agent está em execução. Tente novamente a operação de backup e, se ele falhar, entre em contato com o suporte da Microsoft. |Esse erro é disparado quando o agente da VM está desatualizado. Consulte a seção "Atualizando Olá agente de VM" agente de VM tooupdate hello. |
| A máquina virtual não existe. - Certifique-se de que a máquina virtual exista ou selecione uma máquina virtual diferente. |Isso acontece quando hello VM primária é excluído, mas política de backup Olá continua toolook para um backup de tooperform VM. toofix este erro: <ol><li> Recriar a máquina virtual Olá Olá mesmo nome e o mesmo nome do grupo de recursos [nome do serviço de nuvem,]<br>(OU)<br></li><li>Interrompa a proteção de máquina virtual de saudação sem excluir os dados de backup hello. [Mais detalhes:](http://go.microsoft.com/fwlink/?LinkId=808124)</li></ol> |
| Falha na execução do comando. - Outra operação está em andamento neste item. Aguarde a conclusão da operação de saudação anterior e, em seguida, tente novamente |Um backup existente em Olá VM está em execução, e um novo trabalho não pode ser iniciado enquanto o trabalho existente hello está sendo executado. |
| Copiar VHDs do Cofre de backup Olá atingiu o tempo limite - tente novamente realizar a operação Olá em poucos minutos. Se Olá problema persistir, entre em contato com o Microsoft Support. | Isso ocorre se houver um erro transitório no lado de armazenamento ou se o serviço de backup não estiver obtendo IOPS suficientes de hospedagem Olá VM dados de pedidos tootransfer em toovault de período de tempo limite de conta de armazenamento. Verifique se você seguiu [Práticas recomendadas](backup-azure-vms-introduction.md#best-practices) ao configurar o backup. Tente mover VM tooa outra conta de armazenamento que não está carregada e repita o backup.|
| Falha no backup com um erro interno - tente novamente realizar a operação Olá em poucos minutos. Se Olá problema persistir, entre em contato com o Microsoft Support |Você pode obter esse erro por 2 motivos:  <ol><li> Há um problema temporário ao acessar o armazenamento de saudação de VM. Verifique [Status do Azure](https://azure.microsoft.com/en-us/status/) toosee se houver qualquer problema contínuo relacionadas toocompute, armazenamento ou rede na região de saudação. Repita o trabalho de backup hello quando Olá problema for resolvido. <li>Olá VM original foi excluído e, portanto, o ponto de recuperação de saudação não puder ser obtido. tookeep hello dados de backup para uma VM excluída, mas remova os erros de backup Olá: Desproteger Olá VM e escolha Olá opção tookeep Olá dados. Essa ação interrompe o trabalho de backup agendado hello e mensagens de erro Olá recorrente. |
| Falha na extensão de serviços de recuperação do Azure Olá tooinstall no item de saudação selecionada - Olá, agente de VM é um pré-requisito para Olá extensão de serviços de recuperação do Azure. Instalar o agente de VM do Azure hello e reinicie a operação de registro de saudação |<ol> <li>Verifique se o agente de VM Olá foi instalado corretamente. <li>Certifique-se de sinalizador Olá Olá VM configuração está definida corretamente.</ol> [Leia mais](#validating-vm-agent-installation) sobre a instalação do agente de VM hello e como toovalidate Olá a instalação do agente VM. |
| A instalação da extensão falhou com erro de hello "COM+ foi tootalk não é possível toohello Microsoft Distributed Transaction Coordinator |Isso geralmente significa que o serviço COM+ Olá não está em execução. Entre em contato com o suporte da Microsoft para obter ajuda sobre como corrigir esse problema. |
| Operação de instantâneo falhou com hello erro de operação VSS "essa unidade está bloqueada pela criptografia de unidade de disco BitLocker. Você deve desbloquear essa unidade de saudação painel de controle. |Desativar o BitLocker para todas as unidades no hello VM e observe se Olá VSS problema foi resolvido |
| A VM não está em um estado que permite que os backups. |<ul><li>Verifique se a máquina virtual está em um estado transitório entre execução e desligar, para baixo. Se for, aguarde Olá VM estado toobe um deles e disparar backup novamente. <li> Se Olá VM é uma VM do Linux e o módulo de kernel usa [segurança reforçada Linux], é necessário tooexclude Olá caminho do agente do Linux (_/var/lib/waagent_) de segurança se backup extensão de diretiva de toomake é instalado.  |
| Máquina Virtual do Azure não encontrada. |Isso acontece quando hello VM primária é excluído, mas política de backup Olá continua toolook para uma VM tooperform fazer backup. toofix este erro: <ol><li>Recriar a máquina virtual Olá Olá mesmo nome e o mesmo nome do grupo de recursos [nome do serviço de nuvem,] <br>(OU) <li> Desabilite a proteção para esta VM para que trabalhos de backup Olá não serão criados. </ol> |
| Agente da máquina virtual não está presente na máquina virtual de saudação - instale todos os pré-requisitos e Olá agente de VM e, em seguida, reinicie a operação de saudação. |[Leia mais](#vm-agent) sobre a instalação do agente VM e como toovalidate Olá a instalação do agente VM. |
| Falha na operação de instantâneo devido gravadores tooVSS em estado inválido |Você precisa de gravadores VSS (serviço de cópia de sombra de Volume) de toorestart que estão em estado inválido. tooachieve isso, em um prompt de comando elevado, execute _vssadmin gravadores de lista_. A saída contém todos os gravadores VSS e seus estados. Para cada gravador VSS cujo estado não for "[1] estável", reinicie o gravador VSS executando os comandos a seguir em um prompt de comandos com privilégios elevados:<br> _net stop serviceName_ <br> _net start serviceName_|
| Falha na operação de instantâneo devido a falha de análise de tooa da configuração de saudação |Isso ocorre devido a permissões toochanged no diretório de MachineKeys Olá: _%systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br>Execute o comando abaixo e verifique se as permissões no diretório MachineKeys são as permissões padrão:<br>_icacls %systemdrive%\programdata\microsoft\crypto\rsa\machinekeys_ <br><br> As permissões padrão são:<br>Everyone:(R,W) <br>BUILTIN\Administrators:(F)<br><br>Se você ver as permissões no diretório MachineKeys diferente do padrão, siga abaixo as etapas toocorrect permissões, excluir certificado hello e disparar o backup de saudação.<ol><li>Corrigir as permissões no diretório MachineKeys.<br>Usando propriedades de segurança do Pesquisador de objetos e configurações de segurança avançadas no diretório hello, redefinir permissões fazer toohello os valores padrão, remova qualquer objeto de usuário adicionais (diferente do padrão) do diretório de saudação e certifique-se de que Olá 'Todos' permissões tinham especiais acesso para:<br>– Listar pastas / ler dados <br>– Atributos de leitura <br>– Atributos de leitura estendidos <br>– Criar arquivos / gravar dados <br>– Criar pastas / acrescentar dados<br>– Atributos de gravação<br>– Atributos de gravação estendidos<br>– Permissões de leitura<br><br><li>Exclua todos os certificados com o campo “Emitido Para” = “Gerenciamento de Serviços do Microsoft Azure para Extensões” ou “Gerador de Certificados CRP do Microsoft Azure”.<ul><li>[Abra o console de certificados (computador Local)](https://msdn.microsoft.com/library/ms788967(v=vs.110).aspx)<li>Exclua todos os certificados (em Pessoal -> Certificados) com o campo “Emitido Para” = “Gerenciamento de Serviços do Microsoft Azure para Extensões” ou “Gerador de Certificados CRP do Microsoft Azure”.</ul><li>Disparar Backup de VM. </ol>|
| Falha na validação pois a máquina virtual é criptografada somente com BEK. Os backups podem ser habilitados somente para máquinas virtuais criptografadas com BEK e KEK. |A máquina virtual deve ser criptografado usando a Chave de Criptografia BitLocker e a Chave de Criptografia. Depois disso, o backup deve ser habilitado. |
| Serviço de Backup do Azure não tem suficientes permissões tooKey cofre para Backup de criptografado máquinas virtuais. |Essas permissões podem ser fornecidas pelo serviço de backup no PowerShell usando as etapas mencionadas na seção **Habilitar Backup** da [documentação do PowerShell](backup-azure-vms-automation.md). |
|Instalação do instantâneo falhou com erro de extensão - COM+ não é possível tootalk toohello coordenador de transações distribuídas da Microsoft | Tente toostart windows conserte "aplicativo de sistema COM+" (em um prompt de comando elevado - _net start-COMSysApp_). <br>Se ele falhar ao iniciar, siga etapas a seguir:<ol><li> Verifique se a conta de Logon de saudação do serviço "Coordenador de transações distribuídas" é "Serviço de rede". Se não estiver, altere-o muito "Serviço de rede", reiniciar o serviço e, em seguida, tente toostart serviço "aplicativo de sistema COM+".'<li>Se ele ainda falhar toostart, desinstalar/instalar service "Coordenador de transações distribuídas" seguindo etapas a seguir:<br> -Parar o serviço MSDTC Olá<br> – Abra um prompt de comando (cmd) <br> – Execute o comando “msdtc -uninstall” <br> – Execute o comando “msdtc -install” <br> -Iniciar o serviço MSDTC Olá<li>Inicie o serviço Windows "Aplicativo de Sistema COM+" e, depois de iniciado, dispare o backup do portal.</ol> |
|  Falha na operação de instantâneo devido a erro tooCOM + | Olá recomendado de ação é um serviço do windows toorestart "aplicativo de sistema COM+" (em um prompt de comando elevado - _net start-COMSysApp_). Se Olá problema persistir, reinicie o hello VM. Se a reinicialização Olá VM não ajuda, tente [removendo Olá extensão VMSnapshot](https://docs.microsoft.com/en-us/azure/backup/backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout#cause-3-the-backup-extension-fails-to-update-or-load) e disparar o backup Olá manualmente. |
| Falha de toofreeze um ou mais pontos de montagem de Olá VM tootake um instantâneo consistente do sistema de arquivos | Olá Use as etapas a seguir: <ol><li>Verificar estado do sistema de arquivos Olá todos os dispositivos montados usando _'tune2fs'_ comando.<br> Por exemplo: tune2fs -l /dev/sdb1 \| grep "Filesystem state" <li>Desmontar Olá dispositivos para os quais filesystem estado não é limpa usando _'umount'_ comando <li> Execute a verificação de FileSystemConsistency nesses dispositivos usando o comando _'fsck'_ <li> Montar dispositivos Olá novamente e repita o backup.</ol> |
| Falha na conclusão de operação do instantâneo toofailure na criação de canal de comunicação de rede segura | <ol><Li> Abra o Editor do Registro executando regedit.exe no modo elevado. <li> Identifique todas as versões do .NetFramework presentes no sistema. Eles estão presentes na hierarquia de saudação da chave do Registro "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft" <li> Para cada .NetFramework presente na chave do Registro, adicione a seguinte chave: <br> "SchUseStrongCrypto"=dword:00000001 </ol>|
| Falha na conclusão de operação do instantâneo toofailure na instalação do Visual C++ redistribuível para Visual Studio 2012 | Navegue tooC:\Packages\Plugins\Microsoft.Azure.RecoveryServices.VMSnapshot\agentVersion e instalar vcredist2012_x64. Certifique-se de que o valor de chave do registro para permitir que a instalação do serviço estiver definido como o valor de toocorrect ou seja, o valor da chave do registro _HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Msiserver_ é definir too3 e não 4. Se você ainda estiver enfrentando problemas com a instalação, reinicie o serviço de instalação executando _MSIEXEC /UNREGISTER_ seguido de _MSIEXEC /REGISTER_ em um prompt de comandos com privilégios elevados.  |


## <a name="jobs"></a>Trabalhos
| Detalhes do erro | Solução alternativa |
| --- | --- |
| Não há suporte para cancelamento para este tipo de trabalho - Aguarde a conclusão do trabalho de saudação. |Nenhum |
| Olá trabalho não está em um estado cancelável - Aguarde a conclusão do trabalho de saudação. <br>OU<br> trabalho de saudação selecionado não está em um estado cancelável - Aguarde Olá toocomplete de trabalho. |Provavelmente, trabalho hello está quase concluído. Aguarde até que o trabalho Olá seja concluído.|
| Não é possível cancelar o trabalho de saudação porque ele não está em andamento - cancelamento só tem suporte para trabalhos que estão em andamento. Tente cancelar um trabalho em andamento. |Isso ocorre devido a estado transitório tooa. Aguarde um minuto e tente novamente a operação de cancelamento de saudação. |
| Olá toocancel falha trabalho - Aguarde até que o trabalho seja concluído. |Nenhum |

## <a name="restore"></a>Restaurar
| Detalhes do erro | Solução alternativa |
| --- | --- |
| A restauração falhou com erro interno de nuvem |<ol><li>Toowhich de serviço de nuvem, você está tentando toorestore é configurado com as configurações de DNS. Você pode verificar  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Se houver um endereço configurado, isso significa que as configurações de DNS estão definidas.<br> <li>Tentativa de nuvem serviço toowhich tooyou toorestore está configurado com ReservedIP e VMs existentes no serviço de nuvem estão no estado interrompido.<br>Você pode verificar se um serviço de nuvem tem IP reservado usando os seguintes cmdlets do Powershell:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Você está tentando toorestore uma máquina virtual com as seguintes configurações de rede especiais em toosame serviço de nuvem. <br>– Máquinas virtuais sob configuração do balanceador de carga (interno e externo)<br>– Máquinas virtuais com vários IPs reservados<br>– Máquinas virtuais com várias NICs<br>Selecione um novo serviço de nuvem na saudação da interface do usuário ou consulte muito[considerações sobre restauração](backup-azure-arm-restore-vms.md#restoring-vms-with-special-network-configurations) para VMs com configurações de rede especiais.</ol> |
| nome DNS de saudação selecionada já está em uso -. Especifique um nome DNS diferente e tente novamente. |Olá nome DNS aqui refere-se o nome de serviço de nuvem toohello (geralmente terminam com. n e t). Isso deve toobe exclusivo. Se você encontrar esse erro, será necessário toochoose um nome VM diferente durante a restauração. <br><br> Esse erro é mostrado apenas toousers de saudação portal do Azure. operação de restauração por meio do PowerShell Hello terá êxito porque apenas restaura discos hello e não cria Olá VM. Erro de saudação enfrentarão quando Olá VM for explicitamente criado por você após a operação de restauração de disco hello. |
| Olá configuração de rede virtual especificado não está correta - especifique uma configuração de rede virtual diferente e tente novamente. |Nenhum |
| Olá especificado serviço de nuvem está usando um IP reservado, o que não corresponde à configuração de saudação da máquina virtual de hello está sendo restaurada - especifique um serviço de nuvem diferente, que não está usando o IP reservado, ou escolha outro toorestore de ponto de recuperação do. |Nenhum |
| Serviço de nuvem atingiu o limite do número de pontos de extremidade de entrada - operação de saudação de repetição com a especificação de um serviço de nuvem diferente ou usando um ponto de extremidade existente. |Nenhum |
| Backup conta de armazenamento de cofre e de destino estão em duas regiões diferentes - Certifique-se de que a conta de armazenamento Olá especificada na operação de restauração está em Olá mesma região do Azure como um cofre de backup hello. |Nenhum |
| Conta de armazenamento especificada para operação de restauração Olá não é suportada - contas de armazenamento apenas Basic/Standard com redundância local ou há suporte para configurações de replicação com redundância geográfica. Selecione uma conta de armazenamento com suporte |Nenhum |
| Tipo de conta de armazenamento especificado para a operação de restauração não está on-line - Certifique-se de que a conta de armazenamento Olá especificada na operação de restauração está online |Isso pode acontecer devido a um erro transitório no armazenamento do Azure, seja devido à interrupção tooan. Escolha outra conta de armazenamento. |
| Você atingiu a cota do grupo de recursos - exclua alguns grupos de recursos do portal do Azure ou entre em contato com o suporte do Azure tooincrease Olá limites. |Nenhum |
| A subrede selecionada não existe - selecione uma subrede que exista |Nenhum |
| Serviço de backup não tem recursos de tooaccess de autorização em sua assinatura. |tooresolve isso, primeiro discos restaurar usando as etapas mencionadas na seção **restauração do backup discos** na [a configuração de VM escolhendo restauração](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Depois disso, use as etapas do PowerShell mencionadas [criar uma VM de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate completo VM de discos restaurados. |

## <a name="backup-or-restore-taking-time"></a>Backup ou restauração demorando
Se você observar que o backup (>12 horas) ou a restauração (>6 horas) está demorando:
* Entender [fatores contribuintes tempo toobackup](backup-azure-vms-introduction.md#total-vm-backup-time) e [fatores contribuintes tempo toorestore](backup-azure-vms-introduction.md#total-restore-time).
* Siga as [melhores práticas de Backup](backup-azure-vms-introduction.md#best-practices). 

## <a name="vm-agent"></a>Agente de VM
### <a name="setting-up-hello-vm-agent"></a>Configurando Olá agente de VM
Normalmente, Olá VM Agent já está presente em máquinas virtuais que são criados a partir Olá Galeria do Azure. No entanto, máquinas virtuais que são migradas de datacenters locais não teria Olá agente de VM instalado. Para essas VMs, Olá agente de VM precisa toobe instalado explicitamente.

Para VMs do Windows:

* Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisa de instalação de saudação do toocomplete de privilégios de administrador.
* Para máquinas virtuais de clássico, [atualizar Olá VM propriedade](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. Essa etapa não é necessária para máquinas virtuais do Resource Manager.

Para VMs do Linux:

* Instale o mais recente do repositório de distribuição. É **altamente recomendável** a instalação do agente somente por meio do repositório de distribuição. Para obter detalhes sobre o nome do pacote, consulte muito[repositório de agente do Linux](https://github.com/Azure/WALinuxAgent) 
* Para VMs clássicas, [atualizar Olá VM propriedade](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado. Essa etapa não é necessária para máquinas virtuais do Resource Manager.

### <a name="updating-hello-vm-agent"></a>Atualizando Olá agente de VM
Para VMs do Windows:

* Olá atualizar agente de VM é tão simple quanto a reinstalação Olá [binários de agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). No entanto, é necessário tooensure nenhuma operação de backup está em execução durante a saudação que VM Agent está sendo atualizado.

Para VMs do Linux:

* Siga as instruções de saudação [atualizar agente de VM do Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
É **altamente recomendável** a atualização do agente somente por meio do repositório de distribuição. Não é recomendável baixar o código do agente de saudação do github diretamente e atualizá-lo. Se o agente mais recente não está disponível para a sua distribuição, entre em contato toodistribution suporte para obter instruções sobre como agente mais recente tooinstall. Você pode verificar as informações mais recentes do [agente do Linux do Microsoft Azure](https://github.com/Azure/WALinuxAgent/releases) no repositório GitHub.

### <a name="validating-vm-agent-installation"></a>Validando a instalação do Agente de VM
Como toocheck para Olá versão do agente VM em VMs do Windows:

1. Faça logon no toohello máquina virtual do Azure e navegue toohello pasta *C:\WindowsAzure\Packages*. Você deve encontrar o arquivo de WaAppAgent.exe de saudação presente.
2. Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão do produto de saudação de guia deve ser 2.6.1198.718 ou superior

## <a name="troubleshoot-vm-snapshot-issues"></a>Solucionar Problemas de Instantâneo de VM
Backup de VM se baseia em emitir comandos de instantâneo toounderlying armazenamento. Não tem acesso toostorage ou atrasos na execução da tarefa instantâneo pode causar Olá toofail de trabalho de backup. a seguir Olá pode causar a falha de tarefa de instantâneo.

1. TooStorage de acesso de rede está bloqueado usando NSG<br>
    Saiba mais sobre como muito[habilitar acesso à rede](backup-azure-vms-prepare.md#network-connectivity) tooStorage usando a lista branca de IPs ou por meio do servidor proxy.
2. Máquinas virtuais com o backup do SQL Server configurado podem causar atraso na tarefa do instantâneo  <br>
    Por padrão, o backup de VM emite backup completo de VSS em VMs do Windows. Em VMs que estão executando SQL Servers, se o backup do SQL Server estiver configurado, isso poderá causar atraso na execução do instantâneo. Defina a chave do Registro a seguir se houver falhas de backup devido a problemas de instantâneo.

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
   "USEVSSCOPYBACKUP"="TRUE"
   ```
3. Status da VM informado incorretamente porque a VM está desligada no RDP.  <br>
   Se desligar máquina virtual Olá RDP, verifique no portal de saudação que o status da VM é refletido corretamente. Caso contrário, desligue Olá VM no portal usando a opção 'Desligamento' no painel da máquina virtual.
4. Se o compartilhamento de mais de quatro VMs Olá mesmo serviço de nuvem, configure a saudação de toostage várias políticas de backup backup vezes, portanto, não há mais de quatro backups VM são iniciados em Olá simultaneamente. Tente toospread Olá backup horas de início de uma hora a distância entre as políticas.
5. A VM está executando com alta utilização de CPU/memória.<br>
   Se Olá VM estiver em execução no alto da CPU usage(>90%) ou tarefa de instantâneo de memória, é enfileirado, atrasado e será eventualmente obtém atingiu o tempo limite. Tente o backup sob demanda em tais situações.

<br>

## <a name="networking"></a>Rede
Como todas as extensões, extensão de Backup necessário acessar toohello toowork de internet pública. Não tem acesso toohello internet pública pode se manifestar de várias maneiras:

* a instalação da extensão Olá pode falhar
* as operações de backup Hello (como instantâneos de disco) podem falhar
* Exibir o status de Olá Olá da operação de backup pode falhar

Olá necessidade para resolver endereços da internet pública foi articulada [aqui](http://blogs.msdn.com/b/mast/archive/2014/06/18/azure-vm-provisioning-stuck-on-quot-installing-extensions-on-virtual-machine-quot.aspx). Você precisa de configurações de DNS de saudação do toocheck para Olá VNET e certifique-se que Olá que URIs do Azure pode ser resolvido.

Depois de resolução de nomes de saudação corretamente, acesse toohello que IPS do Azure também precisa toobe fornecido. toounblock acesso toohello infraestrutura do Azure, siga uma destas etapas:

1. Intervalos de IP do datacenter do Azure do hello lista branca.
   * Obter lista de saudação do [IPs do datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) toobe na lista de permissões.
   * Desbloquear Olá IPs usando Olá [New-NetRoute](https://technet.microsoft.com/library/hh826148.aspx) cmdlet. Execute este cmdlet dentro Olá VM do Azure, em uma janela do PowerShell com privilégios elevados (Executar como administrador).
   * Adicionar regras toohello NSG (se você tiver uma) tooallow acesso toohello IPs.
2. Criar um caminho para tooflow de tráfego HTTP
   * Se você tiver alguma restrição de rede no local (uma rede grupo de segurança, por exemplo) implantar um tráfego de saudação de tooroute do servidor de proxy HTTP. Etapas toodeploy pode encontrar um servidor de HTTP Proxy [aqui](backup-azure-vms-prepare.md#network-connectivity).
   * Adicionar regras toohello NSG (se você tiver uma) tooallow acesso toohello INTERNET da saudação HTTP Proxy.

> [!NOTE]
> DHCP deve ser habilitado no convidado Olá para Backup de VM de IaaS toowork.  Se você precisar de um endereço IP privado estático, você deve configurá-lo por meio da plataforma hello. Olá opção DHCP dentro Olá VM deve ser deixada habilitado.
> Exiba mais informações sobre [Como definir um IP interno estático privado](../virtual-network/virtual-networks-reserved-private-ip.md).
>
>
