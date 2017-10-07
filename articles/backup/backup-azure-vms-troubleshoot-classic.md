---
title: "aaaTroubleshoot Azure backup erros no portal clássico | Microsoft Docs"
description: "Solucionar problemas de Backup e restauração de máquinas virtuais do Azure no portal clássico do hello Azure."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
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

## <a name="discovery"></a>Descoberta
| Operação de backup | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Descoberta |Falha ao toodiscover novos itens - erro interno e Backup do Microsoft Azure encontrou. Aguarde alguns minutos e tente novamente a operação de saudação. |Repita o processo de descoberta de saudação após 15 minutos. |
| Descoberta |Falha ao toodiscover novos itens – descoberta outra operação já está em andamento. Aguarde até que a operação de descoberta atual Olá foi concluída. |Nenhum |

## <a name="register"></a>Registrar
| Operação de backup | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Registrar |Número de discos de dados anexados limite de saudação com suporte de máquina virtual excedida toohello - Desanexe alguns discos de dados nesta operação de saudação de máquina virtual e tente novamente. Azure oferece suporte a backup os discos de dados too16 anexado tooan máquina virtual do Azure para backup |Nenhum |
| Registrar |Backup do Microsoft Azure encontrou um erro interno - Aguarde alguns minutos e tente novamente a operação de saudação. Se Olá problema persistir, entre em contato com o Microsoft Support. |Você pode obter esse erro devido a configuração de tooone de saudação a seguir sem suporte de VM em LRS Premium. <br>  pode ser feito usando o cofre de serviços de recuperação. [Saiba mais](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Registrar |Falha no registro com o tempo limite da operação Instalar agente |Verifique se há suporte para a versão de sistema operacional de saudação da máquina virtual de saudação. |
| Registrar |A execução do comando falhou - há outra operação em andamento neste item. Aguarde a conclusão da operação anterior Olá |Nenhum |
| Registrar |Não há suporte para máquinas virtuais com discos rígidos virtuais no armazenamento Premium para backup |Nenhum |
| Registrar |Agente da máquina virtual não está presente na máquina virtual de saudação - instale Olá necessário pré-requisitos, agente de VM e reinicie a operação hello. |[Leia mais](#vm-agent) sobre a instalação do agente VM e como toovalidate Olá a instalação do agente VM. |

## <a name="backup"></a>Backup
| Operação de backup | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Backup |Não foi possível se comunicar com o agente de VM Olá para status do snapshot. Subtarefa de VM do instantâneo atingiu o tempo limite. -Consulte solução de problemas de saudação guia em como tooresolve isso. |Esse erro é gerado se há um problema com hello agente de VM ou toohello de acesso de rede infraestrutura do Azure é bloqueado de alguma forma. Saiba mais sobre [depuração de problemas de instantâneo de VM](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Se o agente de VM Olá não está causando problemas, reinicie Olá VM. Às vezes um estado VM incorreto pode causar problemas e reiniciar Olá VM redefine essa "estado inválido" |
| Backup |Falha no backup com um erro interno - tente novamente realizar a operação Olá em poucos minutos. Se Olá problema persistir, entre em contato com o Microsoft Support |Verifique se há um problema temporário ao acessar o armazenamento de VM. Verifique [Status do Azure](https://azure.microsoft.com/en-us/status/) toosee se houver qualquer emitir relacionado toocompute / / rede de armazenamento na região de saudação em andamento. Por favor, repetição Olá post backup problema é reduzido. |
| Backup |Não foi possível executar a operação de saudação como VM não existe mais. |Backup não pode ser executado porque hello VM configurada para o backup foi excluído. Parar outros backups pela exibição de itens tooProtected vai, selecione o item protegido e clique em Parar proteção. Você pode manter dados selecionando a opção de dados Reter Backup. Posteriormente, você poderá retomar a proteção para essa máquina virtual clicando em configurar proteção no modo de exibição Itens Registrados |
| Backup |Olá tooinstall Falha na extensão de serviços de recuperação do Azure no item de saudação selecionada - agente de VM é um pré-requisito para a extensão de serviços de recuperação do Azure. Instale o agente de VM do Azure hello e reinicie a operação de registro de saudação |<ol> <li>Verifique se o agente de VM Olá foi instalado corretamente. <li>Certifique-se de que Olá sinalizador na configuração VM hello está definida corretamente.</ol> [Leia mais](#validating-vm-agent-installation) sobre a instalação do agente VM e como toovalidate Olá a instalação do agente VM. |
| Backup |A execução do comando falhou - outra operação está em andamento neste item. Aguarde a conclusão da operação de saudação anterior e, em seguida, tente novamente |Um trabalho de backup ou restauração existente para Olá VM está em execução, e um novo trabalho não pode ser iniciado enquanto o trabalho existente hello está sendo executado. |
| Backup |A instalação da extensão falhou com erro de hello "COM+ foi tootalk não é possível toohello Microsoft Distributed Transaction Coordinator |Isso geralmente significa que o serviço COM+ Olá não está em execução. Entre em contato com o suporte da Microsoft para obter ajuda sobre como corrigir esse problema. |
| Backup |Operação de instantâneo falhou com hello erro de operação VSS "essa unidade está bloqueada pela criptografia de unidade de disco BitLocker. Você deve desbloquear esta unidade no Painel de Controle. |Desativar o BitLocker para todas as unidades no hello VM e observe se Olá VSS problema foi resolvido |
| Backup |Não há suporte para máquinas virtuais com discos rígidos virtuais no armazenamento Premium para backup |Nenhum |
| Backup |Máquina Virtual do Azure não encontrada. |Isso acontece quando hello VM primária é excluído, mas política de backup Olá continua toolook para um backup de tooperform VM. toofix este erro: <ol><li>Recriar a máquina virtual Olá Olá mesmo nome e o mesmo nome do grupo de recursos [nome do serviço de nuvem,] <br>(OU) <li>  Desabilite a proteção para esta VM para que os trabalhos de backup subsequentes não sejam disparados. </ol> |
| Backup |Agente da máquina virtual não está presente na máquina virtual de saudação - instale Olá necessário pré-requisitos, agente de VM e reinicie a operação hello. |[Leia mais](#vm-agent) sobre a instalação do agente VM e como toovalidate Olá a instalação do agente VM. |

## <a name="jobs"></a>Trabalhos
| Operação | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Cancelar trabalho |Não há suporte para cancelamento para este tipo de trabalho - Aguarde a conclusão do trabalho de saudação. |Nenhum |
| Cancelar trabalho |Olá trabalho não está em um estado cancelável - Aguarde a conclusão do trabalho de saudação. <br>OU<br> trabalho de saudação selecionado não está em um estado cancelável - Aguarde Olá toocomplete de trabalho. |Provavelmente, Olá quase conclusão do trabalho; Aguarde a conclusão do trabalho de saudação |
| Cancelar trabalho |Não é possível cancelar o trabalho de saudação porque ele não está em andamento - cancelamento só tem suporte para trabalhos que estão em andamento. Tente cancelar um trabalho em andamento. |Isso ocorre devido a estado transitório tooa. Aguarde um minuto e tente novamente a operação de cancelamento Olá |
| Cancelar trabalho |Olá toocancel falha trabalho - Aguarde até que o trabalho seja concluído. |Nenhum |

## <a name="restore"></a>Restaurar
| Operação | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Restaurar |A restauração falhou com erro interno de nuvem |<ol><li>Toowhich de serviço de nuvem, você está tentando toorestore é configurado com as configurações de DNS. Você pode verificar  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Se houver um endereço configurado, isso significa que as configurações de DNS estão definidas.<br> <li>Tentativa de nuvem serviço toowhich tooyou toorestore está configurado com ReservedIP e VMs existentes no serviço de nuvem estão no estado interrompido.<br>Você pode verificar se um serviço de nuvem tem IP reservado usando os seguintes cmdlets do Powershell:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Você está tentando toorestore uma máquina virtual com as seguintes configurações de rede especiais em toosame serviço de nuvem. <br>– Máquinas virtuais sob configuração do balanceador de carga (interno e externo)<br>– Máquinas virtuais com vários IPs reservados<br>– Máquinas virtuais com várias NICs<br>Selecione um novo serviço de nuvem na saudação da interface do usuário ou consulte muito[considerações sobre restauração](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) para VMs com configurações de rede especiais</ol> |
| Restaurar |nome DNS de saudação selecionada já está em uso -. Especifique um nome DNS diferente e tente novamente. |Olá nome DNS aqui refere-se o nome de serviço de nuvem toohello (geralmente terminam com. n e t). Isso deve toobe exclusivo. Se você encontrar esse erro, será necessário toochoose um nome VM diferente durante a restauração. <br><br> Esse erro é mostrado apenas toousers de saudação portal do Azure. Olá a operação de restauração por meio do PowerShell tem sucesso porque somente restaura discos hello e não cria Olá VM. Erro de saudação enfrentarão quando Olá VM for explicitamente criado por você após a operação de restauração de disco hello. |
| Restaurar |Olá configuração de rede virtual especificado não está correta - especifique uma configuração de rede virtual diferente e tente novamente. |Nenhum |
| Restaurar |Olá especificado serviço de nuvem está usando um IP reservado, o que não corresponde à configuração de saudação da máquina virtual de hello está sendo restaurada - especifique um serviço de nuvem diferente que não está usando o IP reservado ou escolha outro toorestore de ponto de recuperação do. |Nenhum |
| Restaurar |Serviço de nuvem atingiu o limite do número de pontos de extremidade de entrada - operação de saudação de repetição com a especificação de um serviço de nuvem diferente ou usando um ponto de extremidade existente. |Nenhum |
| Restaurar |Backup conta de armazenamento de cofre e de destino estão em duas regiões diferentes - Certifique-se de que a conta de armazenamento Olá especificada na operação de restauração está em Olá mesma região do Azure como um cofre de backup hello. |Nenhum |
| Restaurar |Conta de armazenamento especificada para operação de restauração Olá não é suportada - contas de armazenamento apenas Basic/Standard com redundância local ou há suporte para configurações de replicação com redundância geográfica. Selecione uma conta de armazenamento com suporte |Nenhum |
| Restaurar |Tipo de conta de armazenamento especificado para a operação de restauração não está on-line - Certifique-se de que a conta de armazenamento Olá especificada na operação de restauração está online |Isso pode acontecer devido a um erro transitório no armazenamento do Azure, seja devido à interrupção tooan. Escolha outra conta de armazenamento. |
| Restaurar |Você atingiu a cota do grupo de recursos - exclua alguns grupos de recursos do portal do Azure ou entre em contato com o suporte do Azure tooincrease Olá limites. |Nenhum |
| Restaurar |A subrede selecionada não existe - selecione uma subrede que exista |Nenhum |

## <a name="policy"></a>Política
| Operação | Detalhes do erro | Solução alternativa |
| --- | --- | --- |
| Criar política |Falha na diretiva de saudação toocreate - reduza Olá toocontinue de escolhas de retenção com a configuração de política. |Nenhum |

## <a name="vm-agent"></a>Agente de VM
### <a name="setting-up-hello-vm-agent"></a>Configurando Olá agente de VM
Normalmente, Olá VM Agent já está presente em máquinas virtuais que são criados a partir Olá Galeria do Azure. No entanto, máquinas virtuais que são migradas de datacenters locais não teria Olá agente de VM instalado. Para essas VMs, Olá agente de VM precisa toobe instalado explicitamente. Leia mais sobre [Instalando agente VM de saudação em uma VM existente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Para VMs do Windows:

* Baixe e instale Olá [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Você precisará de instalação de saudação do toocomplete de privilégios de administrador.
* [Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado.

Para VMs do Linux:

* Instale o [agente Linux](https://github.com/Azure/WALinuxAgent) mais recente do github.
* [Atualizar a propriedade VM Olá](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Olá agente está instalado.

### <a name="updating-hello-vm-agent"></a>Atualizando Olá agente de VM
Para VMs do Windows:

* Olá atualizar agente de VM é tão simple quanto a reinstalação Olá [binários de agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). No entanto, é necessário tooensure nenhuma operação de backup está em execução durante a saudação que VM Agent está sendo atualizado.

Para VMs do Linux:

* Siga as instruções de saudação [atualizar agente de VM do Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Validando a instalação do Agente de VM
Como toocheck para Olá versão do agente VM em VMs do Windows:

1. Faça logon no toohello máquina virtual do Azure e navegue toohello pasta *C:\WindowsAzure\Packages*. Você deve encontrar o arquivo de WaAppAgent.exe de saudação presente.
2. Clique duas vezes o arquivo hello, ir muito**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão do produto de saudação de guia deve ser 2.6.1198.718 ou superior
