---
title: " Gerenciar um servidor VMware vCenter no Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como adicionar e gerenciar o VMware vCenter no Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Gerenciar um VMware vCenter Server no Azure Site Recovery
Este artigo aborda Olá várias operações de recuperação de Site que podem ser executadas em um VMware vCenter.

## <a name="prerequisites"></a>Pré-requisitos

**Suporte a VMware vCenter e o Host ESX do VMware vSphere** | **Detalhes** |
|--- | --- |
|**Servidores VMware locais** | Um ou mais servidores VMware vSphere, executando 6.0, 5.5, 5.1 com as últimas atualizações. Servidores devem estar localizados no hello mesma rede como o servidor de configuração de hello (ou servidor de processo separado).<br/><br/> Recomendamos um vCenter toomanage hosts do servidor de execução 6.0 ou 5.5 com atualizações mais recentes de saudação. Somente recursos que estão disponíveis no 5.5 têm suporte quando você implanta a versão 6.0.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Preparar uma conta para a descoberta automática
Recuperação de site precisa de acesso tooVMware para tooautomatically de servidor de processo Olá descobrir máquinas virtuais e para failover e failback de máquinas virtuais.

* **Migrar**: se você desejar somente toomigrate tooAzure de máquinas virtuais VMware, sem nunca failback-los, você pode usar uma conta do VMware com uma função somente leitura. Essa função pode executar o failover, mas não pode desligar máquinas de origem protegidas. Isso não é necessário para a migração.
* **Replicar/recuperar**: se você quiser toodeploy conta de saudação de replicação completo (replicação, failover e failback) deve ser capaz de toorun operações como criar e remover discos, ligar a máquina virtual.
* **Descoberta automática**: é necessário ter pelo menos uma conta somente leitura.


|**Tarefas** | **Conta/função necessária** | **Permissões** | **Detalhes**|
|--- | --- | --- | ---|
|**Servidor de processo descobre automaticamente as máquinas virtuais do VMware** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** objeto, os objetos filho toohello (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).|
|**Failover** | Você precisa de pelo menos um usuário somente leitura | Objeto de Data Center –> Propagate tooChild objeto, função = somente leitura | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** toohello os objetos filho (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes) do objeto.<br/><br/> É útil para fins de migração, mas não para replicação completa, failover ou failback.|
|**Failover e failback** | Sugerimos que você cria uma função (AzureSiteRecoveryRole) com permissões necessárias de saudação e, em seguida, atribuir Olá função tooa VMware usuário ou grupo | Objeto de Data Center –> Propagate tooChild objeto, função = AzureSiteRecoveryRole<br/><br/> Armazenamento de dados -> alocar espaço, procurar armazenamento de dados, operações de arquivo de baixo nível, remover arquivo, atualizar arquivos de máquina virtual<br/><br/> Rede -> Atribuição de rede<br/><br/> Recursos -> pool de tooresource atribuir VM, migrar desligado a VM, migrar ligados a VM<br/><br/> Tarefas -> Criar tarefa, atualizar tarefa<br/><br/> Máquina virtual -> Configuração<br/><br/> Máquina virtual -> Interagir -> responder à pergunta, conexão de dispositivo, configurar mídia de CD, configurar mídia de disquete, desligar, ligar, instalação de ferramentas VMware<br/><br/> Máquina virtual -> Inventário -> Criar, registrar, cancelar registro<br/><br/> Máquina virtual -> Provisionamento -> Permitir download de máquina virtual, permitir upload de arquivos de máquina virtual<br/><br/> Máquina virtual -> Instantâneos -> Remover instantâneos | Usuário atribuídos no nível do datacenter e tem acesso tooall Olá objetos em Olá datacenter.<br/><br/> acesso toorestrict, atribuir Olá **nenhum acesso** função com hello **propagar toochild** objeto, os objetos filho toohello (hosts vSphere, armazenamentos de dados, máquinas virtuais e redes).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Criar um servidor do conta tooconnect tooVMware vCenter / host do VMware vSphere EXSi
1. Faça logon em Olá configuração server e inicie Olá cspsconfigtool.exe usando o atalho Olá colocado na área de trabalho de saudação.
2. Clique em **adicionar conta** em Olá **Gerenciar conta** guia.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Olá detalhes da conta e clique em tooadd Okey Olá conta. conta Olá deve ter privilégios de saudação listados no hello [preparar uma conta de descoberta automática](#prepare-an-account-for-automatic-discovery) seção.

  >[!NOTE]
  Demora cerca de 15 minutos para toobe de informações de conta Olá sincronizados backup com o serviço de recuperação de Site hello.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Associar um VMware vCenter/host ESX do VMware vSphere (adicionar vCenter)
* Olá portal do Azure, procurar muito*YourRecoveryServicesVault* > **infra-estrutura de recuperação de Site** > **os servidores de configuração**  >  *ConfigurationServer*
* Na página de detalhes do servidor de configuração Olá clique Olá + vCenter botão.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modificar as credenciais usadas tooconnect toohello-servidor do vCenter / host de ESXi vSphere

1. Fazer logon no hello configuração server e inicie Olá cspsconfigtool.exe
2. Clique em **adicionar conta** em Olá **Gerenciar conta** guia.

  ![add-account](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Forneça detalhes da nova conta hello e clique em tooadd Okey Olá conta. conta Olá deve ter privilégios de saudação listados no hello [preparar uma conta de descoberta automática](#prepare-an-account-for-automatic-discovery) seção.
4. Olá portal do Azure, procurar muito*YourRecoveryServicesVault* > **infra-estrutura de recuperação de Site** > **os servidores de configuração**  >  *ConfigurationServer*
5. Na página de detalhes do servidor de configuração Olá clique Olá **atualização do servidor** botão.
6. Após a conclusão do trabalho de saudação do servidor de atualização, selecione Olá vCenter Server tooopen Olá vCenter página de resumo.
7. Selecione Olá recém-adicionado conta em Olá **conta de host do vCenter server/vSphere** campo e clique em Olá **salvar** botão.

  ![modify-account](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Excluir um vCenter no Azure Site Recovery
1. Olá portal do Azure, procurar muito*YourRecoveryServicesVault* > **infra-estrutura de recuperação de Site** > **os servidores de configuração**  >  *ConfigurationServer*
2. Na página de detalhes do servidor de configuração Olá selecione Olá vCenter Server tooopen Olá vCenter página de resumo.
3. Clique em Olá **excluir** botão toodelete Olá vCenter

  ![delete-account](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Se você precisar toomodify Olá vCenters endereço IP/FQDN, detalhes de porta, você precisa toodelete Olá vCenter Server e adicione-o novamente novamente.
