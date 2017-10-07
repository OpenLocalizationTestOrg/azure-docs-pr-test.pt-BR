---
title: "banco de dados do Analysis Services aaaAzure de backup e restauração | Microsoft Docs"
description: "Descreve como toobackup e restauração de um Azure Analysis Services banco de dados."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Backup e restauração

Fazendo backup de bancos de dados de modelo de tabela no Azure Analysis Services é muito Olá mesmo que o Analysis Services no local. Olá principal diferença é onde você armazena seus arquivos de backup. Arquivos de backup devem ser salvo tooa contêiner em uma [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md). Você pode usar uma conta de armazenamento e um contêiner que já existam ou eles podem ser criados ao definir as configurações de armazenamento para o seu servidor.

> [!NOTE]
> A criação de uma conta de armazenamento pode resultar em um novo serviço faturável. mais, consulte toolearn [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Os backups são salvos com uma extensão abf. Para modelos tabular na memória, ambos os dados de modelo e metadados são armazenados. Para modelos tabulares do DirectQuery, somente os metadados do modelo são armazenados. Os backups podem ser compactados e criptografados, dependendo das opções Olá selecionadas. 



## <a name="configure-storage-settings"></a>Definir as configurações de armazenamento
Antes de fazer backup, você precisa tooconfigure configurações de armazenamento para o servidor.


### <a name="tooconfigure-storage-settings"></a>configurações de armazenamento tooconfigure
1.  No portal do n Azure > **Configurações**, clique em **Backup**.

    ![Backups em Configurações](./media/analysis-services-backup/aas-backup-backups.png)

2.  Clique em **Habilitado** e, em seguida, clique em **Configurações de armazenamento**.

    ![Habilitar](./media/analysis-services-backup/aas-backup-enable.png)

3. Selecione uma conta de armazenamento ou crie uma nova.

4. Selecione um contêiner ou crie um novo.

    ![Selecione o contêiner](./media/analysis-services-backup/aas-backup-container.png)

5. Salve as configurações de backup.

    ![Salvar as configurações de backup](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Backup

### <a name="toobackup-by-using-ssms"></a>toobackup usando o SSMS

1. No SSMS, clique com o botão direito do mouse em um banco de dados > **Backup**.

2. Em **Banco de Dados de Backup** > **Arquivo de Backup**, clique em **Navegar**.

3. Em Olá **salvar arquivo como** caixa de diálogo, verifique se o caminho da pasta hello e, em seguida, digite um nome para o arquivo de backup hello. 

4. Em Olá **banco de dados de Backup** caixa de diálogo, selecione as opções.

    **Permitir que o arquivo substituir** -Selecione esta opção toooverwrite arquivos de backup Olá mesmo nome. Se essa opção não estiver selecionada, arquivo hello você está salvando não pode ter Olá mesmo nome como um arquivo que já existe no hello mesmo local.

    **Aplicar compactação** -Selecione esta opção toocompress Olá backup de arquivo. Arquivos de backup compactados economizam espaço em disco mas exigem uma utilização de CPU ligeiramente maior. 

    **Criptografar arquivo de backup** -Selecione esta opção tooencrypt Olá backup de arquivo. Essa opção requer um arquivo de backup de saudação do toosecure senha fornecida pelo usuário. senha Olá impede a leitura dos dados de backup Olá qualquer outro meio de uma operação de restauração. Se você escolher tooencrypt backups, armazene a senha de saudação em um local seguro.

5. Clique em **Okey** toocreate e salve o arquivo de backup hello.


### <a name="powershell"></a>PowerShell
Use o cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).

## <a name="restore"></a>Restaurar
Ao restaurar, o arquivo de backup deve ser na conta de armazenamento Olá que você configurou para seu servidor. Se você precisar toomove um arquivo de backup de uma conta de armazenamento local local tooyour, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) ou hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitário de linha de comando. 



> [!NOTE]
> Se você estiver restaurando a partir de um servidor local, você deve remover todos os usuários de domínio de saudação de funções de saudação do modelo e adicioná-los fazer toohello funções como usuários do Active Directory do Azure.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore usando o SSMS

1. No SSMS, clique com o botão direito do mouse em um banco de dados > **Restaurar**.

2. Em Olá **banco de dados de Backup** caixa de diálogo, na **arquivo de Backup**, clique em **procurar**.

3. Em Olá **localizar arquivos de banco de dados** caixa de diálogo, o arquivo hello selecione desejado toorestore.

4. Em **restaurar banco de dados**, selecione o banco de dados de saudação.

5. Especifique as opções. Opções de segurança devem coincidir com as opções de backup Olá usado durante o backup.


### <a name="powershell"></a>PowerShell

Use o cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).


## <a name="related-information"></a>Informações relacionadas

[Contas de Armazenamento do Azure](../storage/common/storage-create-storage-account.md)  
[Alta disponibilidade](analysis-services-bcdr.md)     
[Gerenciar Azure Analysis Services](analysis-services-manage.md)
