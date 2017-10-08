---
title: "aaaBackup e restauração criptografados máquinas virtuais usando o Backup do Azure"
description: "Este artigo fala sobre o backup hello e experiência de restauração para VMs criptografados usando a criptografia de disco do Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Como tooback backup e restauração criptografada máquinas virtuais com o Backup do Azure
Este artigo aborda etapas toobackup e restauração de máquinas virtuais usando o Backup do Azure. Ele também oferece detalhes sobre os cenários com suporte, os pré-requisitos e as etapas de solução de problemas para casos de erro.

## <a name="supported-scenarios"></a>Cenários com suporte
> [!NOTE]
> * O backup e a restauração de VMs criptografadas têm suporte somente para as máquinas virtuais implantadas pelo Resource Manager. Não há suporte para as máquinas virtuais Clássicas. <br>
> * Há suporte para máquinas virtuais Windows e Linux, usando a criptografia de disco do Azure, que aproveita a saudação setor BitLocker recurso padrão do Windows e o recurso de DM Crypt do Linux tooprovide criptografia de discos. <br>
> * Isso só tem suporte para as máquinas virtuais criptografadas usando a Chave de Criptografia BitLocker e a Chave de Criptografia. Não tem suporte para as máquinas virtuais criptografadas usando somente a Chave de Criptografia BitLocker. <br>
>
>

## <a name="prerequisites"></a>Pré-requisitos
1. A máquina virtual foi criptografada usando a [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Ele deve ser criptografado usando a Chave de Criptografia BitLocker e a Chave de Criptografia.
2. Cofre de serviços de recuperação foi criado e replicação de armazenamento definida usando as etapas mencionado no artigo Olá [preparar o ambiente para backup](backup-azure-arm-vms-prepare.md).
3. O Backup do Azure tem [Cofre de chaves permissões tooaccess](#provide-permissions-to-azure-backup) que contém chaves, segredos de criptografado VMs.

## <a name="backup-encrypted-vm"></a>Fazer backup da VM criptografada
Usar Olá objetivo backup de tooset as etapas a seguir, definir políticas, configurar itens e o backup do gatilho.

### <a name="configure-backup"></a>Configurar o backup
1. Se você já tiver um cofre de serviços de recuperação aberta, continue toonext etapa. Se você não tiver um aberto de Cofre de serviços de recuperação, mas está em Olá portal do Azure, no menu de Hub hello, clique em **procurar**.

   * Na lista de saudação de recursos, digite **dos serviços de recuperação**.
   * Como começar a digitar, Olá filtros de lista com base em sua entrada. Quando vir a opção **Cofres de Serviços de Recuperação**, clique nela.

      ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     saudação de lista de cofres de serviços de recuperação é exibida. Na lista de saudação de cofres de serviços de recuperação, selecione um cofre.

     painel do cofre selecionado Olá é aberto.
2. Na lista de saudação de itens que aparecem no cofre, clique **Backup** tooopen folha de Backup de saudação.

      ![Abrir a folha Backup](./media/backup-azure-vms-encryption/select-backup.png)
3. Na folha de Backup hello, clique em **meta Backup** folha do tooopen Olá meta de Backup.

      ![Abrir a folha Cenário](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Na folha de meta de Backup hello, defina **onde sua carga de trabalho está executando** tooAzure e **o que fazer você deseja toobackup** tooVirtual máquina e, em seguida, clique em **Okey**.

   folha de meta de Backup Olá fecha e folha de política de Backup Olá é aberta.

   ![Abrir a folha Cenário](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Na folha de política de Backup hello, selecione política de backup de saudação desejado tooapply toohello cofre e clique em **Okey**.

      ![Selecionar a política de backup](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    detalhes de saudação da política de padrão de saudação são listadas nos detalhes de saudação. Se você desejar toocreate uma política, selecione **criar novo** do menu suspenso de saudação. Depois de clicar em **Okey**, política de backup hello está associada ao Cofre hello.

    Em seguida, escolha Olá tooassociate de VMs com o cofre hello.
6. Escolha a saudação criptografado máquinas virtuais tooassociate com hello especificado política e clique em **Okey**.

      ![Selecionar VMs criptografadas](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Esta página mostra uma mensagem sobre o Cofre de chaves associados toohello criptografado VMs selecionadas. Serviço de backup requer chaves de acesso somente leitura de toohello e segredos no cofre de chaves hello. Ele usa a chave de toobackup essas permissões e segredo, juntamente com hello associados VMs. **Você deve atribuir permissões toobackup serviço tooaccess chave de cofre para backups toowork**. Você pode fornecer essas permissões usando [as etapas mencionadas na seção de saudação abaixo](#provide-permissions-to-azure-backup).

      ![Mensagem de VMs criptografada](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Agora que você definiu todas as configurações para o cofre hello, na folha de Backup Olá clique em Habilitar o Backup final Olá Olá página. Habilitar Backup implanta Olá política toohello do cofre e Olá VMs.
8. Hello próxima fase de preparação está instalando Olá agente de VM ou fazer Olá-se de que o agente de VM está instalado. toodo Olá mesmo, siga etapas de saudação mencionadas no artigo Olá [preparar o ambiente para backup](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Disparar o trabalho de backup
Use etapas Olá mencionadas no artigo Olá [Cofre de serviços de VMs do Azure Backup toorecovery](backup-azure-arm-vms.md) tootrigger trabalho de backup.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Continuar os backups de VMs cujo backup já foi realizado com a criptografia habilitada  
Se você tiver VMs já está sendo fazer backup no cofre de serviços de recuperação e ter sido habilitado para criptografia em um momento posterior, você deve atribuir permissões toobackup serviço tooaccess chave de cofre para toocontinue de backups. Você pode fornecer essas permissões usando [as etapas na seção de saudação abaixo](#provide-permissions-to-azure-backup) ou usando o PowerShell etapas mencionadas em **habilitar Backup** seção [documentação do PowerShell](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Forneça permissões tooAzure Backup
Use Olá seguindo as etapas tooprovide permissões relevantes tooAzure tooaccess chave Cofre de Backup e fazer backup de máquinas virtuais criptografados:
1. Selecione **Mais serviços** e pesquise **Cofres de chaves**.

    ![Pesquisar cofre de chaves](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. Na lista de saudação de cofres de chaves, selecione o Cofre de chaves Olá associado à VM criptografado, o que precisa toobe backup.

     ![Selecionar o cofre de chaves](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Clique em **Políticas de acesso** e, em seguida, **Adicionar nova**.

    ![Adicionar política de acesso](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Clique em **Selecione entidade** e tipo **serviço de gerenciamento de Backup** na barra de pesquisa de saudação. 

    ![Pesquisar serviço de backup](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Selecione o **Serviço de Gerenciamento de Backup** e clique no botão Selecionar.

    ![Selecionar o serviço de backup](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Selecione **Backup do Azure** na lista suspensa Configurar usando o modelo. Ele é preenchido previamente permissões Olá necessárias nas permissões de chave e permissões secretas lista suspensa. 

    ![Selecionar backup do Azure](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Clique em **OK**. Observe que o Serviço de Gerenciamento de Backup é adicionado à folha de Políticas de Acesso. 

    ![Política de acesso do serviço de backup](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Clique em **Salvar**. Isso dará Olá necessárias permissões tooAzure Backup.

    ![Política de acesso do serviço de backup](./media/backup-azure-vms-encryption/save-access-policy.png)

Quando as permissões tiverem sido concedidas com êxito, você poderá continuar com a habilitação do backup para VMs criptografadas.

## <a name="restore-encrypted-vm"></a>Restauração a VM criptografada
toorestore criptografados VM, primeiro restaure discos usando as etapas mencionadas na seção **restauração do backup discos** na [a configuração de VM escolhendo restauração](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Depois disso, você pode usar uma saudação as opções a seguir:
* Use Olá PowerShell etapas mencionadas em [criar uma VM de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate completo VM de discos restaurados.
* OR [usar modelo gerado como parte da restauração de discos](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate VMs de discos restaurados. Modelos podem ser usados somente para pontos de recuperação criados após 26 de abril de 2017.

## <a name="troubleshooting-errors"></a>Solucionar erros
| Operação | Detalhes do erro | Resolução |
| --- | --- | --- |
| Backup |Falha na validação pois a máquina virtual é criptografada somente com BEK. Os backups podem ser habilitados somente para máquinas virtuais criptografadas com BEK e KEK. |A máquina virtual deve ser criptografada usando BEK e KEK. Primeiro descriptografar Olá VM e criptografá-la usando BEK e KEK. Habilite o backup após a VM ser criptografada usando BEK e KEK. Saiba mais sobre como você pode [descriptografar e criptografar Olá VM](../security/azure-security-disk-encryption.md)  |
| Restaurar |Você não poderá restaurar essa VM criptografada pois o cofre de chaves associado a essa VM não existe. |Crie o cofre de chaves usando [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md). Consulte o artigo Olá [restaurar a chave de Cofre de chaves e o segredo usando o Azure Backup](backup-azure-restore-key-secret.md) toorestore chave e o segredo se eles são não está presente. |
| Restaurar |Você não poderá restaurar essa VM criptografada pois a chave e o segredo associados a essa VM não existem. |Consulte o artigo Olá [restaurar a chave de Cofre de chaves e o segredo usando o Azure Backup](backup-azure-restore-key-secret.md) toorestore chave e o segredo se eles são não está presente. |
| Restaurar |Serviço de backup não tem recursos de tooaccess de autorização em sua assinatura. |Conforme mencionado acima, primeiro restaure os discos, usando as etapas mencionadas na seção **restauração do backup discos** na [restaurar configuração da VM escolhendo](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Depois, usuário PowerShell muito[criar uma VM de discos restaurados](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Backup | Serviço de Backup do Azure não tem suficientes permissões tooKey Cofre de Backup de criptografado máquinas virtuais | A máquina virtual deve ser criptografado usando a Chave de Criptografia BitLocker e a Chave de Criptografia. Depois disso, o backup deve ser habilitado.  Serviço de backup deve ser fornecido a essas permissões usando [as etapas mencionadas na seção de saudação acima](#provide-permissions-to-azure-backup) ou usando o PowerShell as etapas mencionadas Olá **Habilitar proteção** seção de saudação do PowerShell documentação em [AzureRM.RecoveryServices.Backup Use cmdlets tooback backup de máquinas virtuais](backup-azure-vms-automation.md#back-up-azure-vms). |  
