---
title: "aaaSet as configurações de replicação para o Azure Site Recovery | Microsoft Docs"
description: "Descreve como a replicação de tooorchestrate de recuperação de Site toodeploy, failover e recuperação de máquinas virtuais do Hyper-V no VMM nuvens tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Gerenciar a política de replicação para VMware tooAzure


## <a name="create-a-replication-policy"></a>Criar uma política de replicação

1. Selecione **Gerenciar** > **Infraestrutura do Site Recovery**.
2. Selecione **Políticas de replicação** em **Para VMware e Computadores físicos**.
3. Selecione **+ Política de replicação**.

    ![Criar política de replicação](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Insira o nome da política de saudação.

5. Em **limite de RPO**, especifique o limite RPO hello. Alertas serão gerados quando a replicação contínua excede esse limite.
6. Em **retenção de ponto de recuperação**, especifique (em horas) Olá duração da janela de retenção Olá para cada ponto de recuperação. Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela de retenção.

    > [!NOTE]
    > Todas as horas de too24 de retenção são suportadas para armazenamento de toopremium replicado de máquinas. Todas as horas de too72 de retenção são suportadas para armazenamento de toostandard replicado de máquinas.

    > [!NOTE]
    > Uma política de replicação para failback é criada automaticamente.

7. Em **Frequência de instantâneos consistente com o aplicativo**, especifique com que frequência (em minutos) serão criados os pontos de recuperação que contém instantâneos consistentes com aplicativos.

8. Clique em **OK**. política de saudação deve ser criada em too60 de 30 segundos.

![Geração de política de replicação](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Associar um servidor de configuração com uma política de replicação
1. Escolha Olá toowhich de política de replicação você deseja que o servidor de configuração de saudação tooassociate.
2. Clique em **Associar**.
![Associar o servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Selecione o servidor de configuração de saudação da lista de saudação de servidores.
4. Clique em **OK**. servidor de configuração de saudação deve ser associado em um tootwo minutos.

![Associação de servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Editar uma política de replicação
1. Escolha a política de replicação de saudação do qual você deseja que as configurações de replicação tooedit.
![Editar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Clique em **Editar Configurações**.
![Editar configurações de política de replicação](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Alterar configurações de saudação com base em suas necessidades.
4. Clique em **Salvar**. política de saudação devem ser salvos em dois toofive minutos, dependendo de quantos VMs estão usando essa política de replicação.

![Salvar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Desassociar um servidor de configuração de uma política de replicação
1. Escolha Olá toowhich de política de replicação você deseja que o servidor de configuração de saudação tooassociate.
2. Clique em **Desassociar**.
3. Selecione o servidor de configuração de saudação da lista de saudação de servidores.
4. Clique em **OK**. servidor de configuração de saudação deve ser desassociada em um tootwo minutos.

    > [!NOTE]
    > Não é possível desassociar um servidor de configuração, se houver pelo menos um item replicado usando a política de saudação. Verifique se não há nenhum item replicado usando a política de saudação antes de você desassociar o servidor de configuração de saudação.

## <a name="delete-a-replication-policy"></a>Excluir uma política de replicação

1. Escolha a política de replicação Olá que você deseja toodelete.
2. Clique em **Excluir**. política de saudação deve ser excluída em too60 de 30 segundos.

    > [!NOTE]
    > Você não pode excluir uma política de replicação se ele tem pelo menos um tooit de associados do servidor de configuração. Verifique se não existem itens replicados usando a política de saudação e exclua que todos os Olá associadas a servidores de configuração antes de excluir a política de saudação.
