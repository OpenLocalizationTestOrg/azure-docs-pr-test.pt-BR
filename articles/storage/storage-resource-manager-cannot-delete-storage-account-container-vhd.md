---
title: "erros de aaaTroubleshoot quando você excluir contas de armazenamento do Azure, contêineres ou VHDs | Microsoft Docs"
description: "Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Solucione erros ao excluir contas de Armazenamento do Azure, contêineres ou VHDs

Você poderá receber erros ao tentar toodelete uma conta de armazenamento do Azure, um contêiner ou um disco rígido virtual (VHD) no hello [portal do Azure](https://portal.azure.com). Este artigo fornece uma solução orientação toohelp resolver Olá problema em uma implantação do Azure Resource Manager.

Se este artigo não resolver o problema do Azure, visite Olá fóruns do Azure em [MSDN e o estouro de pilha](https://azure.microsoft.com/support/forums/). Você pode lançar seu problema nesses fóruns ou too@AzureSupport no Twitter. Além disso, você pode emitir uma solicitação de suporte do Azure, selecionando **obter suporte** em Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Sintomas
### <a name="scenario-1"></a>Cenário 1
Quando você tenta toodelete um VHD em uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:

**Falha ao blob toodelete 'vhds/BlobName.vhd'. Erro: Há uma concessão no blob hello e nenhuma ID de concessão foi especificada na solicitação de saudação.**

Esse problema pode ocorrer porque uma máquina virtual (VM) tem uma concessão no VHD que você está tentando toodelete de saudação.

### <a name="scenario-2"></a>Cenário 2
Quando você tenta toodelete um contêiner em uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:

**Falha no contêiner de armazenamento de toodelete 'vhds'. Erro: Há uma concessão no contêiner hello e nenhuma ID de concessão foi especificada na solicitação de saudação.**

Esse problema pode ocorrer porque o contêiner de saudação tem um VHD que está bloqueado no estado de concessão de saudação.

### <a name="scenario-3"></a>Cenário 3
Quando você tenta toodelete uma conta de armazenamento em uma implantação do Gerenciador de recursos, você receberá Olá a seguinte mensagem de erro:

**Falha na conta de armazenamento toodelete 'StorageAccountName'. Erro: a conta de armazenamento Olá não pode ser excluída devido tooits artefatos estão em uso.**

Esse problema pode ocorrer porque a conta de armazenamento Olá contém um VHD que está em estado de concessão de saudação.

## <a name="solution"></a>Solução 
tooresolve esses problemas, você deve identificar Olá VHD que está causando o erro hello e Olá associados a VM. Em seguida, desanexar Olá VHD da VM da saudação (para discos de dados) ou excluir Olá VM que está usando Olá VHD (para discos do sistema operacional). Isso remove a concessão Olá Olá VHD e permite que ele toobe excluído. 

toodo isso, usar um dos métodos a seguir de saudação:

### <a name="method-1---use-azure-storage-explorer"></a>Método 1 – Usar o Gerenciador de Armazenamento do Azure

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Etapa 1 identificar Olá VHD que impedem a exclusão da conta de armazenamento Olá

1. Quando você exclui a conta de armazenamento hello, será exibida uma caixa de diálogo de mensagem, como a seguir hello: 

    ![mensagem ao excluir a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Verificar Olá **disco URL** conta de armazenamento tooidentify hello e hello VHD que impede que você excluir a conta de armazenamento de saudação. Em Olá exemplo a seguir, Olá cadeia de caracteres antes de ". n e t" é o nome de conta de armazenamento hello e "SCCM2012-2015-08-28.vhd" é o nome do VHD de saudação.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Saudação de exclusão de etapa 2 VHD usando o Azure Storage Explorer

1. Download e instalação Olá última versão do [Azure Storage Explorer](http://storageexplorer.com/). Essa ferramenta é um aplicativo autônomo da Microsoft que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Windows e Linux e macOS.
2. Abra o Gerenciador de Armazenamento do Azure e selecione ![o ícone de conta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) na barra de saudação à esquerda, selecione seu ambiente do Azure e entrar.

3. Selecione todas as assinaturas ou assinatura Olá que contém a conta de armazenamento Olá que deseja toodelete.

    ![adicionar assinatura](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Vá toohello conta de armazenamento que são obtidos Olá disco URL anterior, selecione Olá **contêineres de Blob** > **vhds** e procure Olá VHD que impede que você excluir conta de armazenamento de saudação.
5. Se Olá VHD for encontrado, verifique Olá **nome da VM** Olá toofind de coluna VM que está usando este VHD.

    ![Verifique a VM](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Remova concessão Olá Olá VHD usando o portal do Azure. Para obter mais informações, consulte [remover concessão de saudação do hello VHD](#remove-the-lease-from-the-vhd). 

7. Vá toohello Azure Storage Explorer, clique com botão direito Olá VHD e, em seguida, selecione Excluir.

8. Exclua a conta de armazenamento hello.

### <a name="method-2---use-azure-portal"></a>Método 2 – Usar o Portal do Azure 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Etapa 1: Identificar Olá VHD que impedem a exclusão da conta de armazenamento Olá

1. Quando você exclui a conta de armazenamento hello, será exibida uma caixa de diálogo de mensagem, como a seguir hello: 

    ![mensagem ao excluir a conta de armazenamento Olá](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Verificar Olá **disco URL** conta de armazenamento tooidentify hello e hello VHD que impede que você excluir a conta de armazenamento de saudação. Em Olá exemplo a seguir, Olá cadeia de caracteres antes de ". n e t" é o nome de conta de armazenamento hello e "SCCM2012-2015-08-28.vhd" é o nome do VHD de saudação.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Entrar toohello [portal do Azure](https://portal.azure.com).
3. No menu de Hub hello, selecione **todos os recursos**. Vá toohello conta de armazenamento e, em seguida, selecione **Blobs** > **vhds**.

    ![Captura de tela de portal hello, com conta de armazenamento hello e contêiner de "vhds" hello realçado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Localize Olá VHD que são obtidos da URL de disco Olá anteriormente. Em seguida, determinar quais usando a VM Olá VHD. Normalmente, você pode determinar qual VM contém Olá VHD verificando o nome da saudação VHD:

VM no modelo de desenvolvimento do Resource Manager

   * Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd
   * Discos de dados geralmente seguem esta convenção de nomenclatura: NomeDaVM-AAAA-MM-DD-HHMMSS.vhd

VM no modelo de desenvolvimento clássico

   * Discos de sistema operacional geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd
   * Discos de dados geralmente seguem esta convenção de nomenclatura: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Etapa 2: Remover a concessão de saudação do hello VHD

[Remova a concessão Olá Olá VHD](#remove-the-lease-from-the-vhd)e, em seguida, excluir a conta de armazenamento hello.

## <a name="what-is-a-lease"></a>O que é uma concessão?
Uma concessão é um bloqueio que pode ser usado toocontrol acesso tooa blob (por exemplo, um VHD). Quando um blob é concedido, somente os proprietários de saudação de concessão de saudação podem acessar o blob de saudação. Uma concessão é importante para Olá motivos a seguir:

* Isso impede a corrupção de dados se vários proprietários tente toowrite toohello mesma parte do blob de saudação no hello simultaneamente.
* Ela impede que o blob hello está sendo excluído se algo estiver usando ativamente (por exemplo, uma máquina virtual).
* Isso impedirá a conta de armazenamento Olá sejam excluídas se algo estiver usando ativamente (por exemplo, uma máquina virtual).

### <a name="remove-hello-lease-from-hello-vhd"></a>Remova a concessão Olá Olá VHD
Se Olá VHD é um disco do sistema operacional, você deve excluir a concessão de Olá Olá VM tooremove:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **Hub** menu, selecione **máquinas virtuais**.
3. Selecione Olá VM que contém uma concessão no VHD de saudação.
4. Certifique-se de que nada está usando ativamente Olá de máquina virtual, e que você não precisa Olá máquina virtual.
5. Na parte superior de saudação do hello **VM detalhes** folha, selecione **excluir**e, em seguida, clique em **Sim** tooconfirm.
6. Olá VM deve ser excluído, mas Olá VHD pode ser mantido. No entanto, Olá VHD não deve ter uma concessão nele. Ele pode levar alguns minutos para Olá toobe de concessão liberada. tooverify que Olá concessão for liberada, vá muito**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**. Em Olá **propriedades de Blob** painel, Olá **Status de concessão** o valor deve ser **desbloqueado**.

Se Olá VHD é um disco de dados, desanexe Olá VHD de concessão de Olá Olá VM tooremove:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **Hub** menu, selecione **máquinas virtuais**.
3. Selecione Olá VM que contém uma concessão no VHD de saudação.
4. Selecione **discos** em Olá **VM detalhes** folha.
5. Selecione Olá disco de dados que contém uma concessão no VHD de saudação. Você pode determinar que o VHD está anexado no disco Olá verificando URL Olá Olá VHD.
6. Determine com certeza que nada está usando ativamente o disco de dados hello.
7. Clique em **desanexar** em Olá **disco detalhes** folha.
8. disco Olá agora deve ser desanexado de saudação VM e Olá VHD não deve ter uma concessão nele. Ele pode levar alguns minutos para Olá toobe de concessão liberada. tooverify que Olá concessão foi liberado, vá muito**todos os recursos** > **nome da conta de armazenamento** > **Blobs**  >  **vhds**. Em Olá **propriedades de Blob** painel, Olá **Status de concessão** o valor deve ser **desbloqueado**.

## <a name="next-steps"></a>Próximas etapas
* [Excluir uma conta de armazenamento](storage-create-storage-account.md#delete-a-storage-account)
* [Como toobreak Olá bloqueado concessão de armazenamento de blob no Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
