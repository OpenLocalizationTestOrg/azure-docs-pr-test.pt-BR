---
title: "aaaAzure Backup - backup Offline ou usando de propagação inicial Olá serviço de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como o Backup do Azure permite toosend dados rede hello usando o serviço de importação/exportação do Azure hello. Este artigo explica Olá offline propagação saudação inicial dos dados de backup usando o serviço de exportação e importação do Azure hello."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Fluxo de trabalho de backup offline no Backup do Azure
Backup do Azure tem várias eficiências internas que poupar custos de rede e armazenamento durante a saudação inicias backups completos de tooAzure de dados. Backups completos inicias normalmente transferir grandes quantidades de dados e exigem mais largura de banda em comparação com backups toosubsequent que transferem apenas Olá deltas/backups incrementais. O Backup do Azure compacta os backups de saudação inicial. Processo de saudação de propagação off-line, Backup do Azure pode usar discos tooupload Olá compactado inicial de dados de backup offline tooAzure.  

Hello offline propagação o processo de Backup do Azure é integrado com hello [serviço de importação/exportação do Azure](../storage/common/storage-import-export-service.md) que permite que você tootransfer dados tooAzure usando discos. Se você tiver terabytes (TB) de dados do backup inicial que precisa toobe transferido em uma rede de alta latência e baixa largura de banda, você pode usar o hello offline propagação fluxo de trabalho tooship Olá cópia de backup inicial em um ou mais discos rígidos tooan datacenter do Azure. Este artigo fornece uma visão geral das etapas de saudação que concluir o fluxo de trabalho.

## <a name="overview"></a>Visão geral
Com recurso offline propagação saudação do Backup do Azure e importação/exportação do Azure, é simples tooupload Olá dados offline tooAzure usando discos. Em vez de transferir a cópia completa inicial Olá pela rede hello, dados de backup Olá são gravados tooa *local de preparo*. Após o local de preparo Olá cópia toohello usando a ferramenta de importação/exportação do Azure hello, esses dados são gravados unidades tooone ou SATA mais, dependendo da quantidade de saudação de dados. Essas unidades são eventualmente fornecido toohello mais próximo do datacenter do Azure.

Olá [atualização de agosto de 2016 do Backup do Azure (e posterior)](http://go.microsoft.com/fwlink/?LinkID=229525) inclui Olá *ferramenta de preparação de disco do Azure*, denominado AzureOfflineBackupDiskPrep, que:

* Ajuda a preparar suas unidades para importação do Azure usando a ferramenta de importação/exportação do Azure hello.
* Cria automaticamente um trabalho de importação do Azure para Olá serviço de importação/exportação do Azure Olá [portal clássico do Azure](https://manage.windowsazure.com) como toocreating contrário Olá mesmo manualmente com as versões mais antigas do Backup do Azure.

Após carregar Olá Olá tooAzure de dados de backup, Backup do Azure copia Cofre de backup toohello do hello dados de backup e os backups incrementais hello.

> [!NOTE]
> Olá toouse ferramenta de preparação de disco do Azure, certifique-se de que você ter instalado a atualização de agosto de 2016 saudação do Backup do Azure (ou posterior) e executar todas as etapas de saudação do fluxo de trabalho de saudação com ele. Se você estiver usando uma versão mais antiga do Backup do Azure, você pode preparar a unidade SATA de saudação usando a ferramenta de importação/exportação do Azure Olá conforme detalhado nas seções posteriores deste artigo.
>
>

## <a name="prerequisites"></a>Pré-requisitos
* [Familiarize-se com o fluxo de trabalho de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md).
* Antes de iniciar o fluxo de trabalho hello, certifique-se de seguir hello:
  * Um cofre de Backup do Azure foi criado.
  * As credenciais do cofre foram baixadas.
  * Olá agente de Backup do Azure foi instalado em Windows Server/Windows cliente ou servidor do System Center Data Protection Manager e Olá computador é registrado com o Cofre de Backup do Azure hello.
* [Baixar as configurações do arquivo de publicação no Azure Olá](https://manage.windowsazure.com/publishsettings) no computador de saudação do qual você planeja tooback backup de seus dados.
* Prepare um local temporário, que pode ser um compartilhamento de rede ou o disco adicional no computador de saudação. Olá local de preparo é transitório de armazenamento e é usado temporariamente durante esse fluxo de trabalho. Certifique-se de que Olá local de preparo tem suficiente toohold de espaço em disco a cópia inicial. Por exemplo, se você estiver tentando tooback um servidor de arquivo de 500 GB, certifique-se de que área de preparação de saudação é pelo menos 500 GB. (Uma quantidade menor é usada devido toocompression.)
* Verifique se você está usando uma unidade com suporte. Somente 2,5 polegadas SSD ou 2,5 ou 3,5 pol. SATA II ou III discos rígidos internos têm suporte para uso com o serviço de importação/exportação do hello. Você pode usar discos rígidos até too10 TB. Verificar Olá [documentação do serviço de importação/exportação do Azure](../storage/common/storage-import-export-service.md#hard-disk-drives) para Olá último conjunto de unidades que Olá serviço oferece suporte.
* Habilitar o BitLocker Olá computador toowhich gravador de unidade SATA hello está conectado.
* [Baixar a ferramenta de importação/exportação do Azure Olá](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello computador toowhich Olá SATA unidade gravador está conectado. Essa etapa não será necessária se você tiver baixado e instalado a atualização de agosto de 2016 saudação do Backup do Azure (ou posterior).

## <a name="workflow"></a>Fluxo de trabalho
Olá as informações nesta seção ajudarão você a concluir o fluxo de trabalho de backup offline Olá para que os dados podem ser entregues tooan datacenter do Azure e carregados tooAzure armazenamento. Se você tiver dúvidas sobre o serviço de importação de saudação ou qualquer aspecto do processo de hello, consulte Olá [visão geral do serviço de importação](../storage/common/storage-import-export-service.md) documentação mencionada anteriormente.

### <a name="initiate-offline-backup"></a>Iniciar o backup offline
1. Quando você agenda um backup, você verá Olá após a tela (no Windows Server, o cliente do Windows ou o System Center Data Protection Manager).

    ![Tela de importação](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Eis tela correspondente hello no System Center Data Protection Manager: <br/>
    ![Tela de importação do DPM](./media/backup-azure-backup-import-export/dpmoffline.png)

    Descrição de saudação de entradas de saudação é o seguinte:

    * **Local de preparação**: Olá armazenamento temporário local toowhich Olá cópia de backup inicial é gravada. Isso pode estar em um computador local ou em um compartilhamento de rede. Se o computador de cópia hello e o computador de origem forem diferentes, é recomendável que você especifique o caminho de rede completo de saudação do hello local de preparo.
    * **Nome do trabalho de importação do Azure**: nome exclusivo de saudação pelo qual importação do Azure service e o Backup do Azure controlam transferência Olá dos dados enviados em discos tooAzure.
    * **Configurações de publicação do Azure**: um arquivo XML que contém informações sobre seu perfil de assinatura. Ele também contém credenciais seguras associadas à sua assinatura. Você pode [baixar arquivo hello](https://manage.windowsazure.com/publishsettings). Fornecer Olá caminho local toohello Publicar arquivo de configurações.
    * **ID da assinatura do Azure**: Olá ID de assinatura do Azure para onde você planejar o trabalho de importação do Azure Olá tooinitiate de assinatura de saudação. Se você tiver várias assinaturas do Azure, use Olá ID de assinatura de saudação que você deseja tooassociate com o trabalho de importação de saudação.
    * **Conta de armazenamento do Azure**: Olá clássico tipo conta de armazenamento Olá fornecido assinatura do Azure que será associada ao trabalho de importação do Azure hello.
    * **Contêiner de armazenamento do Azure**: nome de saudação do blob de armazenamento de destino Olá em Olá conta de armazenamento do Azure, onde os dados desse trabalho são importados.

    > [!NOTE]
    > Se você tiver registrado tooan seu servidor dos serviços de recuperação do Azure cofre da saudação [portal do Azure](https://portal.azure.com) para seus backups e não estão em uma assinatura do provedor de solução de nuvem (CSP), você ainda pode criar uma conta de armazenamento de tipo clássico de saudação Portal do Azure e usá-lo para o fluxo de trabalho de backup offline hello.
    >
    >

     Salve todas essas informações porque você precisa tooentê-lo novamente em etapas a seguir. Olá somente *local de preparo* é necessário se você usar discos de Olá Olá preparação do disco do Azure ferramenta tooprepare.    
2. Concluir o fluxo de trabalho hello e, em seguida, selecione **backup agora** na cópia de saudação do Azure Backup management console tooinitiate Olá-backup offline. backup de saudação inicial é gravado toohello área de preparo como parte dessa etapa.

    ![Fazer backup agora](./media/backup-azure-backup-import-export/backupnow.png)

    fluxo de trabalho correspondente no System Center Data Protection Manager, do toocomplete Olá clique Olá **grupo de proteção**e, em seguida, escolha Olá **criar ponto de recuperação** opção. Escolha Olá **proteção Online** opção.

    ![Fazer backup agora do DPM](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Após a conclusão da operação de hello, Olá local de preparo está pronto toobe usado para a preparação do disco.

    ![Andamento do backup](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Preparar uma unidade SATA e criar um trabalho de importação do Azure usando a ferramenta de preparação do disco do Azure Olá
ferramenta de preparação do disco do Azure Hello está disponível no diretório de instalação do agente de serviços de recuperação de saudação (atualização de agosto de 2016 e posterior) em Olá que caminho a seguir.

   *\Microsoft* *Azure* *Recovery* *Services* *Agent\Utils\*

1. Vá toohello diretório e Olá cópia **AzureOfflineBackupDiskPrep** computador de cópia de tooa do diretório no qual Olá toobe unidades preparada são montados. Certifique-se de seguir Olá ao computador de cópia de toohello de relação:

    * Olá cópia computador pode acessar Olá local de preparação para fluxo de trabalho Olá propagação offline usando o mesmo caminho que foi fornecido na saudação de rede de saudação **Iniciar backup offline** fluxo de trabalho.
    * O BitLocker é habilitado no computador de saudação.
    * computador Olá pode acessar Olá portal do Azure.

    Se necessário, computador de cópia Olá pode Olá mesmo que o computador de origem hello.
2. Abra um prompt de comando com privilégios elevados no computador de cópia de saudação com o diretório da ferramenta de preparação do disco do Azure hello como o diretório atual Olá e execute Olá comando a seguir:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parâmetro | Descrição |
    | --- | --- |
    | s:&lt;*Caminho do Local de Preparo*&gt; |Entrada obrigatória que usou tooprovide Olá caminho toohello local que você inseriu na saudação de preparo **Iniciar backup offline** fluxo de trabalho. |
    | p:&lt;*tooPublishSettingsFile de caminho*&gt; |Entrada opcional que usou tooprovide Olá caminho toohello **configurações de publicação do Azure** arquivo que você inseriu na Olá **Iniciar backup offline** fluxo de trabalho. |

    > [!NOTE]
    > Olá &lt;tooPublishSettingFile caminho&gt; valor é obrigatório quando o computador de cópia hello e o computador de origem são diferentes.
    >
    >

    Quando você executa o comando Olá, ferramenta Olá solicitações de seleção de saudação do trabalho de importação do Azure Olá correspondente toohello unidades que precisa toobe preparado. Se apenas um trabalho de importação simples está associado a saudação fornecida o local de preparação, você vê uma tela como Olá que segue.

    ![Entrada da ferramenta de preparação do disco do Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Digite a letra da unidade de saudação sem saudação à direita de dois-pontos para disco montado hello, que você deseja tooprepare para tooAzure de transferência. Forneça a confirmação para a formatação de saudação da unidade hello quando solicitado.

    ferramenta Hello, em seguida, começa em disco de saudação tooprepare com dados de backup de saudação. Talvez seja necessário tooattach discos quando for solicitado pela ferramenta Olá Olá fornecido disco não tem espaço suficiente para os dados de backup hello. <br/>

    No final da saudação da execução bem-sucedida da ferramenta hello, um ou mais discos que você forneceu estão preparados para tooAzure de envio. Além disso, um trabalho de importação com o nome da saudação fornecido durante a saudação **Iniciar backup offline** fluxo de trabalho é criado no hello portal clássico do Azure. Finalmente, Olá ferramenta exibe Olá envio endereço toohello datacenter do Azure onde discos Olá necessário toobe enviado e Olá o trabalho de importação de saudação do link toolocate em Olá portal clássico do Azure.

    ![Preparação de disco do Azure concluída](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Remeter saudação discos toohello endereço dessa ferramenta Olá fornecida e lembre-Olá, número de controle para referência futura.<br/>

5. Quando você for toohello vincular essa ferramenta Olá exibida, você verá Olá conta de armazenamento do Azure que você especificou no hello **Iniciar backup offline** fluxo de trabalho. Aqui você pode ver o trabalho de importação Olá recém-criada em hello **importação/exportação** guia Olá da conta de armazenamento.

    ![Trabalho de importação criado](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Clique em **informações de envio** final Olá Olá página tooupdate seu contato detalhes conforme Olá tela a seguir. A Microsoft usa esse tooship informações seu back tooyou de discos depois que o trabalho de importação de saudação for concluída.

    ![Informações de contato](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Digite hello detalhes de envio na próxima tela de saudação. Fornecer Olá **operadora** e **número de controle** detalhes correspondentes toohello discos que você entregue toohello datacenter do Azure.

    ![INFORMAÇÕES DE ENVIO](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Fluxo de trabalho Olá concluída
Após a conclusão do trabalho de importação hello, dados de backup inicias estão disponíveis em sua conta de armazenamento. saudação de agente de serviços de recuperação e Olá copia dados de saudação deste Cofre de Backup toohello conta ou serviços de recuperação de cofre, o que for aplicável. No tempo de backup Olá agendado, o agente de Backup Azure Olá executa backup incremental Olá pela cópia de backup inicial hello.

> [!NOTE]
> Olá seções a seguir se aplicam toousers de versões anteriores do Backup do Azure que não têm a ferramenta de preparação do disco do Azure toohello acesso.
>
>

### <a name="prepare-a-sata-drive"></a>Preparar uma unidade SATA
1. Baixar Olá [ferramenta de importação/exportação do Microsoft Azure](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello computador de cópia. Certifique-se de que Olá local de preparo pode ser acessado do computador Olá planeje toorun Olá próximo conjunto de comandos. Se necessário, computador de cópia Olá pode Olá mesmo que o computador de origem hello.

2. Descompacte o arquivo de WAImportExport.zip hello. Execute a ferramenta de WAImportExport de saudação que formata a unidade SATA de saudação, gravações de disco do hello dados de backup toohello SATA e criptografá-la. Antes de executar Olá comando a seguir, certifique-se de que o BitLocker é habilitado no computador de saudação. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Se você instalou a atualização de agosto de 2016 saudação do Backup do Azure (ou posterior), certifique-se de que Olá preparo local que você inseriu é Olá mesmo Olá uma saudação **backup agora** contém arquivos AIB e Blob de Base e da tela.
    >
    >

| Parâmetro | Descrição |
| --- | --- |
| /j:<*JournalFile*> |arquivo de diário do Hello caminho toohello. Cada unidade deve ter exatamente um arquivo de diário. arquivo de diário Olá não deve estar na unidade de destino hello. extensão de arquivo de diário Olá é .jrn e é criado como parte da execução desse comando. |
| /id:<*SessionId*> |ID da sessão Olá identifica uma sessão de cópia. É usado tooensure de recuperação precisa de uma sessão de cópia interrompida. Arquivos que são copiados em uma sessão de cópia são armazenados em um diretório chamado após Olá ID da sessão na unidade de destino hello. |
| /sk:<*StorageAccountKey*> |chave da conta Olá para dados de saudação do hello armazenamento conta toowhich é importado. Olá principais necessidades toobe Olá mesmo que ele foi inserido durante a criação do grupo de proteção/política de backup. |
| /BlobType |tipo de saudação do blob. Esse fluxo de trabalho só será bem-sucedido se **PageBlob** for especificado. Isso não é saudação padrão opção e deve ser mencionado neste comando. |
| /t:<*TargetDriveLetter*> |Letra de unidade de saudação sem saudação à direita de dois-pontos de disco rígido de destino Olá para sessão de cópia atual de saudação. |
| /format |Olá opção tooformat Olá a unidade. Especifique esse parâmetro quando precisa de unidade Olá toobe formatado; Caso contrário, omiti-lo. Antes de ferramenta Olá formatos unidade hello, ele solicita uma confirmação do console de saudação. toosuppress Olá confirmação, especifique o parâmetro /silentmode. de saudação. |
| /encrypt |Olá opção tooencrypt Olá a unidade. Especifique esse parâmetro quando a unidade de saudação ainda não tiver sido criptografada com BitLocker e necessidades toobe criptografada pela ferramenta hello. Se a unidade de saudação já foi criptografada com BitLocker, omitir esse parâmetro, especificar Olá /bk parâmetro e forneça a chave de BitLocker existente hello. Se você especificar o parâmetro de /format hello, você deve também especificar Olá / criptografar parâmetro. |
| /srcdir:<*SourceDirectory*> |diretório de origem de saudação que contém arquivos toobe copiados toohello unidade de destino. Certifique-se de que esse nome de diretório especificado Olá tem um caminho completo em vez de relativo. |
| /dstdir:<*DestinationBlobVirtualDirectory*> |Olá caminho toohello diretório virtual de destino em sua conta de armazenamento do Azure. Ser toouse-se de que os nomes de contêiner válido quando você especificar diretórios virtuais de destino hello ou blobs. Tenha em mente que os nomes de contêiner devem estar em minúsculas.  Esse nome de contêiner deve ser Olá que você digitou durante a criação do grupo de proteção/política de backup. |

> [!NOTE]
> Um arquivo de diário é criado na pasta de WAImportExport Olá que captura as informações de toda saudação do fluxo de trabalho de saudação. É necessário neste arquivo quando você cria um trabalho de importação no portal do Azure de saudação.
>
>

  ![Saída do PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Criar um trabalho de importação no hello portal do Azure
1. Acesse a conta de armazenamento tooyour Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **importação/exportação**e, em seguida, **criar trabalho de importação** no painel de tarefas de saudação.

    ![Guia de importação/exportação no hello portal do Azure](./media/backup-azure-backup-import-export/azureportal.png)

2. Na etapa 1 do Assistente de saudação, indicam que você preparou sua unidade e se você tem o arquivo de diário de unidade de saudação disponível.

3. Na etapa 2 do Assistente de saudação, forneça as informações de contato para Olá quem é responsável por este trabalho de importação.

4. Na etapa 3, carregar arquivos de diário de unidade de saudação que você obteve na seção anterior hello.

5. Na etapa 4, digite um nome descritivo para o trabalho de importação de saudação que você digitou durante a criação do grupo de proteção/política de backup. nome Hello inserido pode conter apenas letras minúsculas, números, hifens e sublinhados e deve começar com uma letra e não pode conter espaços. nome de saudação que você escolher será usado tootrack seus trabalhos enquanto eles estão em andamento e depois que eles são concluídos.

6. Em seguida, selecione sua região do datacenter na lista de saudação. região do datacenter Olá indica Olá toowhich datacenter e o endereço deve enviar seu pacote.

    ![Selecionar a região do datacenter](./media/backup-azure-backup-import-export/dc.png)

7. Na etapa 5, selecione a operadora de retorno na lista de saudação e insira seu número de conta da operadora. A Microsoft usa essa conta tooship suas unidades fazer tooyou depois que o trabalho de importação for concluído.

8. Envie o disco de saudação e insira Olá status de controle número tootrack Olá de remessa hello. Depois que o disco Olá chega no datacenter Olá, é copiado toohello conta de armazenamento e Olá status é atualizado.

    ![Status concluído](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Fluxo de trabalho Olá concluída
Após os dados de backup inicial Olá disponíveis em sua conta de armazenamento, hello agente de serviços de recuperação do Microsoft Azure copia o conteúdo de saudação do dados saudação deste Cofre de Backup toohello conta ou o Cofre de serviços de recuperação, o que for aplicável. No próximo agendamento de saudação tempo de backup, hello Azure Backup agent executa o backup incremental Olá pela cópia de backup inicial hello.

## <a name="next-steps"></a>Próximas etapas
* Para todas as questões sobre o fluxo de trabalho de importação/exportação do Azure hello, consulte muito[usar Olá importação/exportação do Microsoft Azure serviço tootransfer dados tooBlob armazenamento](../storage/common/storage-import-export-service.md).
* Consulte toohello backup offline seção do hello Azure Backup [perguntas frequentes sobre](backup-azure-backup-faq.md) para dúvidas sobre o fluxo de trabalho de saudação.
