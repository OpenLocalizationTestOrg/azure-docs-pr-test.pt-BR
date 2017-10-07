---
title: "Relatórios de aaaConfigure para Backup do Azure"
description: "Este artigo fala sobre como configurar relatórios do Power BI para Backup do Azure usando o cofre dos Serviços de Recuperação."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Configurar relatórios de Backup do Azure
Este artigo aborda etapas tooconfigure relatórios para o Azure Backup usando o Cofre de serviços de recuperação e tooaccess esses relatórios usando o Power BI. Depois de executar essas etapas, você pode diretamente vá tooPower BI tooview todos os relatórios de hello, personalizar e criar relatórios. 

## <a name="supported-scenarios"></a>Cenários com suporte
1. Relatórios de Backup do Azure têm suporte para a máquina virtual do Azure backup e arquivo/pasta backup toocloud usando o agente de serviços de recuperação do Azure.
2. Não há suporte para relatórios do SQL Azure, DPM e Servidor de Backup do Azure no momento.
3. Você pode exibir relatórios em cofres e em assinaturas, se a mesma conta de armazenamento é configurada para cada um dos cofres hello. Conta de armazenamento selecionada deve estar no hello Cofre de serviços da mesma região que a recuperação.
4. frequência de saudação da atualização agendada para relatórios de saudação é 24 horas no Power BI. Você também pode executar uma atualização do ad-hoc Olá relatórios no Power BI, em que dados de caso mais recentes na conta de armazenamento do cliente são usados para renderizar relatórios. 

## <a name="prerequisites"></a>Pré-requisitos
1. Criar um [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure para relatórios. Essa conta de armazenamento é usada para armazenar dados relacionados a relatórios.
2. [Criar uma conta do Power BI](https://powerbi.microsoft.com/landing/signin/) tooview, personalizar e criar seus próprios relatórios usando o portal do Power BI.
3. Registrar o provedor de recursos de saudação **Insights** se não registrado já, com assinatura de saudação da conta de armazenamento e também com assinatura Olá dos serviços de recuperação cofre tooenable reporting dados tooflow toohello conta de armazenamento. toodo Olá mesmo, você deve ir tooAzure portal > assinatura > provedores de recursos e verifique se há esse provedor tooregistê-lo. 

## <a name="configure-storage-account-for-reports"></a>Configurar a conta de armazenamento para relatórios
Saudação de uso após a conta de armazenamento etapas tooconfigure Olá para o Cofre de serviços de recuperação usando o portal do Azure. Essa é uma configuração única e após configurar a conta de armazenamento, você pode ir tooPower BI diretamente Aproveite e pacote de conteúdo tooview relatórios.
1. Se você já tiver um cofre de serviços de recuperação aberta, continue toonext etapa. Se você não tiver um aberto de Cofre de serviços de recuperação, mas está em Olá portal do Azure, no menu de Hub hello, clique em **procurar**.

   * Na lista de saudação de recursos, digite **dos serviços de recuperação**.
   * Como começar a digitar, Olá filtros de lista com base em sua entrada. Quando vir a opção **Cofres de Serviços de Recuperação**, clique nela.

      ![Criar Cofre de Serviços de Recuperação - etapa 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     saudação de lista de cofres de serviços de recuperação é exibida. Na lista de saudação de cofres de serviços de recuperação, selecione um cofre.

     painel do cofre selecionado Olá é aberto.
2. Na lista de saudação de itens que aparecem no cofre, clique **Backup relatórios** sob monitoramento e relatórios seção tooconfigure Olá conta de armazenamento para relatórios.

      ![Etapa 2 Selecione o item de menu Backup de Relatórios](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Na folha de relatórios de Backup hello, clique em **configurar** botão. Isso abre a folha de informações de aplicativo do Azure Olá que é usada para enviar por push a conta de armazenamento toocustomer de dados.

      ![Etapa 3 Configurar a conta de armazenamento](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Definir botão de alternância de Status de saudação muito**na** e selecione **tooa conta de armazenamento de arquivos** caixa de seleção para que o relatório de dados podem iniciar fluindo na conta de armazenamento toohello.

      ![Etapa 4 Habilitar o diagnóstico](./media/backup-azure-configure-reports/set-status-on.png)
5. Clique em Seletor de conta de armazenamento e a conta de armazenamento Olá selecione da lista de saudação para armazenar dados de relatório e clique em **Okey**.

      ![Etapa 5 Selecionar a conta de armazenamento](./media/backup-azure-configure-reports/select-storage-account.png)
6. Selecione **AzureBackupReport** caixa de seleção e também mover o período de retenção de tooselect Olá controle deslizante para esse dados de relatório. Relatórios de dados na conta de armazenamento Olá são mantidas por período de saudação selecionado usando a barra deslizante.

      ![Etapa 6 Selecione a conta de armazenamento](./media/backup-azure-configure-reports/save-configuration.png)
7. Examine todas as alterações de saudação e clique em **salvar** botão na parte superior, conforme mostrado na figura acima a saudação. Esta ação garante que todas as alterações sejam salvas e a conta de armazenamento agora está configurada para armazenar os dados de relatório.

> [!NOTE]
> Depois que você configurar relatórios, salvando a conta de armazenamento, você deve **Aguarde 24 horas** para toocomplete de envio de dados inicial. Você deverá importar o pacote de conteúdo do Backup do Azure no Power BI somente após esse período. Para obter mais detalhes, consulte a seção [Perguntas frequentes](#frequently-asked-questions). 
>
>

## <a name="view-reports-in-power-bi"></a>Exibir relatórios no Power BI 
Depois de configurar a conta de armazenamento para relatórios usando o Cofre de serviços de recuperação, levará cerca de 24 horas para toostart dados fluindo na emissão de relatórios. Após 24 horas de configurar a conta de armazenamento, as etapas a seguir do uso Olá tooview relatórios no Power BI:
1. [Entrar](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Clique em **Obter Dados** e clique em Obter em **Serviços** na Biblioteca do pacote de conteúdo. Use as etapas mencionadas [pacote de conteúdo do Power BI documentação tooaccess](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Importar o pacote de conteúdo](./media/backup-azure-configure-reports/content-pack-import.png)
3. Digite o **Backup do Azure** na barra Search e clique em **Obter agora**.

      ![Obter pacote de conteúdo](./media/backup-azure-configure-reports/content-pack-get.png)
4. Insira o nome de conta de armazenamento Olá configurada na etapa 5 acima e clique em **próximo** botão.

    ![Insira o nome da conta de armazenamento](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Insira a chave de conta de armazenamento Olá para esta conta de armazenamento. Você pode [exibir e copiar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account) navegando tooyour conta de armazenamento no portal do Azure. 

     ![Insira a conta de armazenamento](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Clique no botão **Entrar**. Depois que o logon for bem-sucedido, você obterá a notificação **Importando dados**.

    ![Importando o pacote de conteúdo](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Depois de algum tempo, você obtém **êxito** notificação após a conclusão da importação de saudação. Pode levar pouco mais tooimport Olá pacote de conteúdo, se houver muitos dados na conta de armazenamento hello.
    
    ![Importar o pacote de conteúdo com sucesso](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Quando dados são importados com êxito, **Backup do Azure** pacote de conteúdo é visível no **aplicativos** no painel de navegação de saudação. lista Olá agora mostra o painel de controle de Backup do Azure, relatórios e conjunto de dados com uma estrela amarela indicando relatórios recém-importados. 

     ![Pacote de conteúdo de Backup do Azure](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Clique em **Backup do Azure** em Painéis, que mostra um conjunto de relatórios chave fixados.

      ![Painel de Backup do Azure](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. conjunto completo de saudação de tooview de relatórios, clique em qualquer relatório no painel de saudação.

      ![Integridade do trabalho de Backup do Azure](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Clique em cada guia em Olá relatórios tooview relatórios nessa área.

      ![Guias para relatórios de Backup do Azure](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Perguntas frequentes
1. **Como verificar se dados de relatório começou fluindo na conta toostorage?**
    
    Você pode ir toohello armazenamento configurados e selecionados contêineres de conta. Se o contêiner de saudação tem uma entrada para informações de logs de azurebackupreport, ele indica que dados de relatórios foi iniciado fluindo.

2. **O que é a frequência de saudação da conta de toostorage de envio de dados e o pacote de conteúdo de Backup do Azure no Power BI?**

   Para usuários do dia 0, levaria conta de toostorage de dados de toopush em torno de 24 horas. Uma vez neste inicial push compelete, dados são atualizados com hello frequência mostrada na figura abaixo a saudação a seguir. 
      * Dados relacionados muito**trabalhos, alertas, itens de Backup, cofres, servidores protegidos e políticas** é enviada por push toocustomer conta de armazenamento como e quando ele estiver conectado.
      * Dados relacionados muito**armazenamento** é enviada a conta de armazenamento toocustomer a cada 24 horas.
   
    ![Frequência de push de dados de relatórios de Backup do Azure](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  O Power BI tem uma [atualização agendada uma vez por dia](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). Você pode executar uma atualização manual dos dados Olá no Power BI para o pacote de conteúdo hello.

3. **Quanto tempo é possível reter Olá relatórios?** 

   Ao configurar a conta de armazenamento, você pode selecionar o período de retenção de dados de relatório na conta de armazenamento hello (usando a etapa 6 em Configurar conta de armazenamento para a seção de relatórios acima). Além disso, você pode [Analisar relatórios no excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) e salvá-los para um período de retenção mais longo, de acordo com as suas necessidades. 

4. **Será exibida todos os meus dados em relatórios depois de configurar a conta de armazenamento Olá?**

   Todos os dados gerados após de hello **"Configurando a conta de armazenamento"** toohello conta de armazenamento será enviado e estarão disponíveis em relatórios. No entanto, **Os trabalhos em andamento não são enviados por push** para a emissão de relatórios. Depois que o trabalho de saudação é concluída ou falha, ela é enviada tooreports.

5. **Se eu já tiver configurado a relatórios de tooview de conta de armazenamento hello, alterar Olá configuração toouse outra conta de armazenamento?** 

   Sim, você pode alterar a conta de armazenamento diferente do hello configuração toopoint tooa. Você deve usar a conta de armazenamento de saudação configurada recentemente ao conectar-se o pacote de conteúdo de Backup tooAzure. Além disso, depois que uma conta de armazenamento diferente for configurada, novos dados fluirão nesta conta de armazenamento. Mas dados mais antigos (antes de alterar a configuração de saudação) ainda permanecerá na conta de armazenamento hello mais antiga.

6. **Posso exibir relatórios entre cofres e assinaturas?** 

   Sim, você pode configurar Olá cofres de mesma conta de armazenamento entre vários relatórios de cofre entre tooview. Além disso, você pode configurar Olá a mesma conta de armazenamento para cofres entre assinaturas. Você pode usar essa conta de armazenamento durante a conexão do pacote de conteúdo de Backup tooAzure em relatórios do Power BI tooview hello. No entanto, a conta de armazenamento Olá selecionada deve estar no hello Cofre de serviços da mesma região que a recuperação.
   
## <a name="next-steps"></a>Próximas etapas
Agora que você configurou a conta de armazenamento hello e pacote de conteúdo de Backup do Azure importado, próxima etapa de saudação é toocustomize esses relatórios e use os relatórios de toocreate de modelo de dados. Consulte Olá seguintes artigos para obter mais detalhes.

* [Usando o modelo de dados de relatórios de Backup do Azure](backup-azure-reports-data-model.md)
* [Filtrando relatórios no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Criando relatórios no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

