---
title: "servidores aaaRemove e desabilite a proteção | Microsoft Docs"
description: "Este artigo descreve como os servidores de toounregister de uma recuperação de Site cofre e toodisable proteção para máquinas virtuais e servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Remover os servidores e desabilitar a proteção

Olá serviço Azure Site Recovery contribui com a estratégia de recuperação (BCDR) de desastre e continuidade de negócios tooyour. serviço de saudação coordena a replicação, failover e recuperação de máquinas virtuais e servidores físicos. Computadores podem ser replicado tooAzure ou tooa local secundário data center. Para ter uma breve visão geral, leia [O que é Azure Site Recovery?](site-recovery-overview.md)

Este artigo descreve como toounregister servidores de serviços de recuperação de um cofre no portal do Azure de saudação e como toodisable proteção para máquinas protegidos pela recuperação de Site.

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Cancelar o registro de um servidor de configuração conectado

Se você replicar máquinas virtuais do VMware ou tooAzure de servidores físicos do Windows/Linux, você pode cancelar o registro de um servidor conectado de configuração de um cofre da seguinte maneira:

1. Desabilite o proteção da máquina. Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.
2. Desassocie todas as políticas. Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **políticas de replicação**, clique duas vezes em Olá diretiva associada. Servidor de configuração com o botão direito hello > **desassociar**.
3. Remova qualquer outro processo local ou servidores de destino mestre. Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de saudação com o botão direito > **Excluir**.
4. Exclua o servidor de configuração de saudação.
5. Desinstalar manualmente o serviço de mobilidade Olá em execução no servidor de destino mestre da saudação (Isso será um separado ou servidor ou em execução no servidor de configuração de saudação).
6. Desinstale quaisquer servidores de processo adicionais.
7. Desinstale o servidor de configuração de saudação.
8. No servidor de configuração de hello, desinstale a instância de saudação do MySQL que foi instalada pela recuperação de Site.
9. No registro de saudação saudação do servidor de configuração excluir chave Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Cancelar o registro de um servidor de configuração não conectado

Se você replicar máquinas virtuais do VMware ou tooAzure de servidores físicos do Windows/Linux, você pode cancelar o registro de um servidor de configuração desconectado de um cofre da seguinte maneira:

1. Desabilite o proteção da máquina. Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**. Selecione **parar de gerenciar a máquina Olá**.
2. Remova qualquer outro processo local ou servidores de destino mestre. Em **infra-estrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de saudação com o botão direito > **Excluir**.
3. Exclua o servidor de configuração de saudação.
4. Desinstalar manualmente o serviço de mobilidade Olá em execução no servidor de destino mestre da saudação (Isso será um separado ou servidor ou em execução no servidor de configuração de saudação).
5. Desinstale quaisquer servidores de processo adicionais.
6. Desinstale o servidor de configuração de saudação.
7. No servidor de configuração de hello, desinstale a instância de saudação do MySQL que foi instalada pela recuperação de Site.
8. No registro de saudação saudação do servidor de configuração excluir chave Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Cancelar o registro de um servidor VMM conectado

Como melhor prática, recomendamos que você cancelar o registro do servidor do VMM hello quando tooAzure tenha se conectado. Isso garante que as configurações nos servidores do VMM hello (e em outros servidores do VMM com nuvens emparelhados) sejam limpos corretamente. Remova um servidor desconectado somente se houver um problema de conectividade permanente. Se o servidor do VMM Olá não está conectado, será necessário toomanually executar tooclean um script configurações.

1. Pare a replicação de máquinas virtuais em nuvens em Olá servidor VMM que você deseja tooremove.
2. Exclua qualquer mapeamento de rede usado pelo nuvens no hello servidor VMM que você deseja toodelete. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento de rede**, clique o mapeamento de rede hello >  **Excluir**.
3. Desassocie políticas de replicação de nuvens em Olá servidor VMM que você deseja tooremove.  Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada. Clique com botão direito nuvem hello > **desassociar**.
4. Exclua o servidor do VMM hello ou nó ativo do VMM. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **servidores do VMM**, servidor de saudação atalho >  **Excluir**.
5. Desinstale Olá provedor manualmente no servidor do VMM hello. Se você tiver um cluster, remova todos os nós.
6. Se você estiver replicando tooAzure, remova manualmente o agente de serviços de recuperação do Microsoft hello de hosts do Hyper-V nas nuvens Olá excluído.



### <a name="unregister-an-unconnected-vmm-server"></a>Cancelar o registro de um servidor VMM desconectado

1. Pare a replicação de máquinas virtuais em nuvens em Olá servidor VMM que você deseja tooremove.
2. Exclua qualquer mapeamento de rede usado pelo nuvens no servidor do VMM Olá que você deseja toodelete. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento de rede**, clique o mapeamento de rede hello >  **Excluir**.
3. Observe a ID de saudação do servidor do VMM hello.
4. Desassocie políticas de replicação de nuvens em Olá servidor VMM que você deseja tooremove.  Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada. Clique com botão direito nuvem hello > **desassociar**.
5. Exclua o servidor do VMM hello ou nó ativo. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **servidores do VMM**, servidor de saudação atalho >  **Excluir**.
6. Baixe e execute Olá [script de limpeza](http://aka.ms/asr-cleanup-script-vmm) no servidor do VMM hello. Abra o PowerShell com hello **executar como administrador** opção política de execução toochange Olá para o escopo do saudação padrão (LocalMachine). No script hello, especifique a ID de saudação do hello servidor VMM que você deseja tooremove. script Hello remove o registro e informações do servidor de saudação de emparelhamento de nuvem.
5. Execute o script de limpeza de saudação em outros servidores VMM que contêm as nuvens que são combinadas com nuvens de saudação servidor VMM que você deseja tooremove.
6. Execute o script de limpeza de saudação em qualquer outros passivo VMM nós de cluster com hello que provedor instalado.
7. Desinstale Olá provedor manualmente no servidor do VMM hello. Se você tiver um cluster, remova todos os nós.
8. Se você replicar tooAzure, você pode remover agente de serviços de recuperação do Microsoft hello de hosts do Hyper-V em nuvens Olá excluído.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Cancelar o registro de um host Hyper-V em um site do Hyper-V

Os hosts Hyper-V que não são gerenciados pelo VMM são reunidos em um site do Hyper-V. Remova um host de um site do Hyper-V da seguinte maneira:

1. Desabilite a replicação para máquinas virtuais do Hyper-V localizado no host de saudação.
2. Desassocie políticas para o site do Hyper-V hello. Em **infra-estrutura de recuperação de Site** > **para Sites do Hyper-V** >  **políticas de replicação**, clique duas vezes em diretiva de saudação associada. Site de saudação do botão direito do mouse > **desassociar**.
3. Exclua os hosts Hyper-V. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **Hosts Hyper-V**, servidor de saudação atalho >  **Excluir**.
4. Exclua site Olá Hyper-V depois que todos os hosts foram removidos dele. Em **infra-estrutura de recuperação de Site** > **para o System Center VMM** > **Sites Hyper-V**, site de saudação do botão direito do mouse >  **Excluir**.
5. Execute Olá script a seguir em cada host Hyper-V que foram removidos. Olá script limpa as configurações no servidor de saudação e cancela o registro do cofre hello.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Desabilitar a proteção de uma VM do VMware ou servidor físico

1. Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.
2. Em **Remover Máquina**, selecione uma destas opções:
    - **Desabilite a proteção de máquina da saudação (recomendada)**. Use este toostop opção replicando máquina hello. As configurações do Site Recovery serão limpas automaticamente. Você só verá essa opção em Olá circunstâncias a seguir:
        - **Tamanho do volume VM Olá**— quando você redimensiona uma saudação do volume virtual máquina entra em um estado crítico. Selecione essa proteção de toodisables opção enquanto retém os pontos de recuperação no Azure. Ao habilitar a proteção da máquina Olá novamente, dados de Olá para o volume de saudação redimensionada serão transferido tooAzure.
        - **Executar um failover recentemente**— depois de executar um failover tootest seu ambiente, selecione esse toostart opção protegendo máquinas locais novamente. Ele desabilita a cada máquina virtual e, em seguida, você precisa tooenable proteção para-los novamente. Desabilitar máquina Olá com essa configuração não afeta Olá máquina de virtual de réplica no Azure. Não desinstale o serviço de mobilidade de saudação da máquina de saudação.
    - **Parar de gerenciar a máquina Olá**. Se você selecionar essa opção, Olá máquina só será removida do cofre hello. As configurações de proteção de locais para a máquina de saudação não serão afetadas. configurações de tooremove máquina hello e tooremove máquina Olá Olá assinatura do Azure, você precisar de configurações de saudação tooclean Desinstalando o serviço de mobilidade hello.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Desabilitar a proteção de uma VM Hyper-V em uma nuvem do VMM

1. Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.
2. Em **Remover Máquina**, selecione uma destas opções:

    - **Desabilite a proteção de máquina da saudação (recomendada)**. Use este toostop opção replicando máquina hello. As configurações do Site Recovery serão limpas automaticamente.
    - **Parar de gerenciar a máquina Olá**. Se você selecionar essa opção, Olá máquina só será removida do cofre hello. As configurações de proteção de locais para a máquina de saudação não serão afetadas. configurações de tooremove máquina hello e tooremove máquina Olá Olá assinatura do Azure, você precisar tooclean Olá configurações backup manualmente, usando instruções de saudação abaixo. Observe que se você selecionar a máquina de virtual toodelete hello e seus discos rígidos, eles serão removidos do local de destino de saudação.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Limpar as configurações de proteção - local do replication tooa secundário do VMM

Se você selecionou **parar de gerenciar a máquina Olá** e você replicando tooa site secundário, execute este script no tooclean do servidor primário Olá configurações Olá da máquina virtual primária de saudação. No console do VMM Olá clique console do hello PowerShell botão tooopen Olá PowerShell do VMM. Substitua SQLVM1 com o nome da saudação de sua máquina virtual.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. No servidor VMM secundário Olá execute tooclean este script configurações Olá da máquina virtual secundária de saudação:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. No servidor VMM secundário hello, atualize máquinas virtuais de saudação no servidor de host do Hyper-V Olá, portanto hello VM secundário obtém detectado novamente no console do VMM hello.
4. Olá acima etapas limpar as configurações de replicação Olá no servidor do VMM hello. Se você quiser toostop replicação da máquina virtual de hello, executar Olá seguir script AH Olá VMs primárias e secundárias. Substitua SQLVM1 com o nome da saudação de sua máquina virtual.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Limpar as configurações de proteção - tooAzure de replicação

1. Se você selecionou **parar de gerenciar a máquina Olá** e replicar tooAzure, execute este script no servidor do VMM de origem de hello, usando o PowerShell do console do VMM hello.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Olá acima etapas limpar as configurações de replicação de saudação no servidor do VMM hello. replicação toostop para a máquina virtual de saudação em execução no servidor de host do Hyper-V hello, execute este script. Substitua SQLVM1 pelo nome de saudação da sua máquina virtual e host01.contoso.com com o nome de saudação do servidor de host do Hyper-V hello.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Desabilitar a proteção de uma VM do Hyper-V em um site do Hyper-V

Use este procedimento se você estiver replicando tooAzure de VMs Hyper-V sem um servidor do VMM.

1. Em **itens protegidos** > **itens replicados**, máquina de saudação do botão direito do mouse > **excluir**.
2. Em **remover máquina**, você pode selecionar Olá as opções a seguir:

   - **Desabilite a proteção de máquina da saudação (recomendada)**. Use este toostop opção replicando máquina hello. As configurações do Site Recovery serão limpas automaticamente.
   - **Parar de gerenciar a máquina Olá**. Se você selecionar essa opção Olá máquina só será removida do cofre hello. As configurações de proteção de locais para a máquina de saudação não serão afetadas. configurações de tooremove na máquina hello e tooremove Olá virtual machine de saudação assinatura do Azure, você precisar tooclean Olá configurações backup manualmente. Se você selecionar a máquina de virtual toodelete hello e seus discos rígidos, eles serão removidos do local de destino hello.
3. Se você selecionou **parar de gerenciar a máquina Olá**, executar esse script no servidor de host do Hyper-V de origem hello, tooremove replicação da máquina virtual de saudação. Substitua SQLVM1 com o nome da saudação de sua máquina virtual.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
