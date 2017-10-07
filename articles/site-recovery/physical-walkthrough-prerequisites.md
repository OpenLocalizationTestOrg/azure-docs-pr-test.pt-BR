---
title: "aaaPrerequisites para replicação do servidor físico tooAzure usando o Azure Site Recovery | Microsoft Docs"
description: "Resume os pré-requisitos de saudação para replicar as cargas de trabalho em execução no tooAzure de servidores Windows/Linux físico, usando o serviço do Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: b0ed53a143079877a2ad21ee17aae5510e0dc058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-physical-server-tooazure-replication"></a>Etapa 2: Examinar os pré-requisitos de saudação para replicação do servidor físico tooAzure

Examine os pré-requisitos de saudação resumidos na tabela de saudação.


**Pré-requisito** | **Detalhes**
--- | ---
**As tabelas** | Saiba mais sobre [requisitos do Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuração local** | Você precisa de um servidor físico (ou VM VMware) executando o Windows Server 2012 R2 ou versão posterior. Você pode configurar este servidor durante a implantação de Site Recovery.<br/><br/> Pelo processo de saudação padrão o servidor e o servidor de destino mestre também são instalados neste computador. Ao escalar verticalmente, talvez seja necessário um servidor de processo separado. Se você fizer isso, ele tem Olá mesmos requisitos do servidor de configuração de saudação.<br/><br/> [Saiba mais](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**VMs locais** | Máquinas que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e estar em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | servidor de configuração de Olá precisa acessar toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).<br/><br/> Permitir que essa URL para download do MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Instalado em todos os servidores replicados.




## <a name="limitations"></a>Limitações

Observe as limitações de saudação resumidas na tabela de saudação antes de implantar.

**Limitação** | **Detalhes**
--- | ---
**As tabelas** | Contas de armazenamento e de rede devem estar no hello mesma região Olá cofre<br/><br/> Se você usar uma conta de armazenamento premium, você também precisa de um padrão de armazenar os logs de conta de replicação toostore<br/><br/> Você não pode replicar contas toopremium no centro e Sul da Índia.
**Servidor de configuração local** | Se você usar uma VM do VMware máquina do servidor de configuração de hello, Olá o tipo de adaptador VM VMware deve ser VMXNET3. Caso contrário, [instale esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> Para uma VM VMware, o vSphere PowerCLI 6.0 deve ser instalado.<br/><br> máquina de saudação não deve ser um controlador de domínio.<br/><br/> máquina de saudação deve ter um endereço IP estático.<br/><br/> nome do host Olá deve ser de 15 caracteres ou menos, e o sistema operacional deve estar em inglês.
**Replicar máquinas** | Verifique [Limitações de VM do Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Você não pode replicar máquinas virtuais com discos criptografados ou máquinas virtuais com inicialização EFI/UEFI.<br/><br> Não há suporte para clusters de disco compartilhado. Se a VM de origem Olá tem agrupamento NIC, ele será convertido tooa única NIC após o failover.<br/><br/> Se as VMs têm um disco iSCSI, recuperação de Site converte arquivo VHD tooa após o failover. Se o destino de iSCSI Olá possa ser alcançado por Olá VM do Azure, ele se conecta tooit e vê-lo e hello VHD. Se isso acontecer, desconecte do destino iSCSI hello.<br/><br/> Se você quiser tooenable consistência de várias VMs, que permite que as VMs em execução Olá mesmo toobe de carga de trabalho recuperado dados consistentes tooa juntos ponto, abrir a porta 20004 no hello VM.<br/><br/> Windows deve ser instalado na unidade C do hello. disco do sistema operacional Olá deve ser básico e não dinâmico. disco de dados Olá pode ser dinâmico.<br/><br/> Linux /etc/hosts arquivos em VMs devem conter entradas que mapeiam Olá host local nome tooIP endereços associados a todos os adaptadores de rede. Olá, nome de host, pontos de montagem, nome do dispositivo, os caminhos de sistema e nomes de arquivo (/ etc; em /usr.) deve ser apenas em inglês.<br/><br/> Tipos específicos de [armazenamento do Linux](site-recovery-support-matrix-to-azure.md#support-for-storage) têm suporte.<br/><br/>Criar ou definir **disk.enableUUID=true** nas configurações de VM hello. Isso fornece uma consistente toohello UUID VMDK, para que ele monta corretamente e garante que as alterações delta somente são transferidos back tooon local durante o failback sem replicação completa.


## <a name="next-steps"></a>Próximas etapas

- Se você estiver fazendo uma implantação completa, vá muito[etapa 3: planejar a capacidade](physical-walkthrough-capacity.md)
- Se você estiver fazendo uma implantação de teste simples, vá muito[etapa 4: planejar a rede](physical-walkthrough-network.md).
