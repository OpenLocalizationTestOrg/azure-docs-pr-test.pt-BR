---
title: "aaaPrepare recursos do VMware para tooAzure de replicação com o Azure Site Recovery local | Microsoft Docs"
description: "Resume as etapas de saudação que é necessário para replicar as cargas de trabalho em execução em máquinas virtuais do VMware tooAzure armazenamento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 6aba0e89-ad7c-467e-9db2-cfb3bfe4c7d6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 09d81f15f6ee764135a62f5555e458c55fa30048
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-on-premises-vmware-replication-tooazure"></a>Etapa 6: Preparar tooAzure de replicação do VMware no local

Use instruções Olá este artigo tooprepare local VMware servidores toointeract com o Azure Site Recovery e preparar VMs VMWare para a instalação do serviço de mobilidade de saudação. Agente de serviço de mobilidade Olá deve ser instalado em todas as VMs no local que você deseja tooreplicate tooAzure.

## <a name="prepare-for-automatic-discovery"></a>Preparar para a descoberta automática

O Site Recovery detecta automaticamente as VMs em execução em hosts ESXi vSphere (com ou sem um servidor do vCenter). Para a descoberta automática, hosts de tooaccess uma conta de necessidades de recuperação de Site e servidores:

1. toouse uma conta dedicada, crie uma função (no nível do vCenter Olá, com permissões de saudação descritos na tabela de saudação abaixo. Use um nome como **Azure_Site_Recovery**.
2. Em seguida, crie um usuário no servidor de vCenter/host vSphere hello e atribuir Olá função toohello usuário. Você especifica essa conta de usuário durante a implantação de Site Recovery.


### <a name="vmware-account-permissions"></a>Permissões de conta do VMware

Recuperação de site precisa de acesso tooVMware para tooautomatically de servidor de processo Olá descobrir máquinas virtuais e para failover e failback de máquinas virtuais.

- **Migrar**: se você quiser apenas toomigrate VMs VMware tooAzure, sem nunca failback-los, você pode usar uma conta do VMware com uma função somente leitura. Essa função pode executar o failover, mas não pode desligar máquinas de origem protegidas. Isso não é necessário para a migração.
- **Replicar/recuperar**: se você quiser toodeploy conta de saudação de replicação completo (replicação, failover e failback) deve ser capaz de toorun operações como criar e remover discos, ligar VMs etc.
- **Descoberta automática**: é necessário ter pelo menos uma conta somente leitura.


**Tarefa** | **Conta/função necessária** | **Permissões** | **Detalhes**
--- | --- | --- | ---
**Servidor de processo descobre automaticamente as VMs VMware** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** de objetos, toohello filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).
**Failover** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** toohello os objetos filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes) do objeto.<br/><br/> É útil para fins de migração, mas não para replicação completa, failover ou failback.
**Failover e failback** | Sugerimos que você cria uma função (Azure_Site_Recovery) com permissões necessárias de saudação e, em seguida, atribuir Olá função tooa VMware usuário ou grupo | Objeto de Data Center –> Propagate tooChild objeto, função = Azure_Site_Recovery<br/><br/> Armazenamento de dados -> alocar espaço, procurar armazenamento de dados, operações de arquivo de baixo nível, remover arquivo, atualizar arquivos de máquina virtual<br/><br/> Rede -> Atribuição de rede<br/><br/> Recursos -> pool de tooresource atribuir VM, migrar desligado a VM, migrar ligados a VM<br/><br/> Tarefas -> Criar tarefa, atualizar tarefa<br/><br/> Máquina virtual -> Configuração<br/><br/> Máquina virtual -> Interagir -> responder à pergunta, conexão de dispositivo, configurar mídia de CD, configurar mídia de disquete, desligar, ligar, instalação de ferramentas VMware<br/><br/> Máquina virtual -> Inventário -> Criar, registrar, cancelar registro<br/><br/> Máquina virtual -> Provisionamento -> Permitir download de máquina virtual, permitir upload de arquivos de máquina virtual<br/><br/> Máquina virtual -> Instantâneos -> Remover instantâneos | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** de objetos, toohello filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).


## <a name="prepare-for-push-installation-of-hello-mobility-service"></a>Preparar para a instalação por push do serviço de mobilidade de saudação

Olá serviço de mobilidade deve ser instalado em todas as máquinas virtuais que você deseja tooreplicate. Há uma série de maneiras tooinstall Olá serviço, incluindo a instalação manual, a instalação por push do servidor de processo de recuperação de Site Olá e a instalação usando métodos, como o System Center Configuration Manager.

Se você quiser toouse a instalação por push, é necessário tooprepare uma conta que a recuperação de Site pode usar tooaccess Olá VM.

- Você pode usar uma conta local ou de domínio
- Para Windows, se você não estiver usando uma conta de domínio, você precisa toodisable controle de acesso de usuário remoto na máquina local hello. toodo, Olá registrar em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, adicionar entrada DWORD Olá **LocalAccountTokenFilterPolicy**, com um valor de 1.
- Entrada de registro tooadd Olá para Windows de uma CLI, digite:``REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.``
- Para o Linux, a conta de Olá deve ser raiz no servidor do hello origem Linux.



## <a name="next-steps"></a>Próximas etapas

Vá muito[etapa 7: criar um cofre](vmware-walkthrough-create-vault.md)
