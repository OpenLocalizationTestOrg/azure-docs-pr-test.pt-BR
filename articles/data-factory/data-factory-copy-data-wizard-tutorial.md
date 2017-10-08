---
title: "Tutorial: criar um pipeline usando o Assistente de Cópia | Microsoft Docs"
description: "Neste tutorial, você criar um pipeline da fábrica de dados do Azure com uma atividade de cópia usando Olá Assistente para cópia de suporte pela fábrica de dados"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Tutorial: Criar um pipeline com a Atividade de Cópia usando o Assistente de Cópia do Data Factory
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

Este tutorial mostra como Olá toouse **Assistente para cópia de** toocopy dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. 

saudação do Azure Data Factory **Assistente para cópia** permite que você tooquickly criar um pipeline de dados que copia dados de um repositório de dados de destino origem com suporte dados repositório tooa com suporte. Portanto, recomendamos que você use o Assistente de saudação como uma primeira toocreate da etapa um pipeline de exemplo para seu cenário de movimentação de dados. Para obter uma lista de armazenamentos de dados com suporte como origens e destinos, consulte [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Este tutorial mostra como toocreate uma fábrica de dados do Azure, Olá Iniciar Assistente para cópia, passar por uma série de detalhes de tooprovide etapas sobre seu cenário de inclusão/movimentação de dados. Quando você concluir as etapas no Assistente de saudação, o Assistente de saudação cria automaticamente um pipeline com dados de toocopy uma atividade de cópia de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. Para saber mais sobre a atividade de cópia, confira [Atividades de movimentação de dados](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Pré-requisitos
Conclua os pré-requisitos listados em Olá [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artigo antes de executar este tutorial.

## <a name="create-data-factory"></a>Criar um data factory
Nesta etapa, você usa Olá toocreate portal do Azure uma fábrica de dados do Azure denominada **ADFTutorialDataFactory**.

1. Faça logon no muito[portal do Azure](https://portal.azure.com).
2. Clique em **+ novo** no canto superior esquerdo de saudação, clique em **dados + análise**e clique em **Data Factory**. 
   
   ![Novo -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. Em Olá **nova fábrica de dados** folha:
   
   1. Digite **ADFTutorialDataFactory** para Olá **nome**.
       nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo. Se você receber o erro Olá: `Data factory name “ADFTutorialDataFactory” is not available`, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFTutorialDataFactoryYYYYMMDD) e tente criar novamente. Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.  
      
       ![Nome da data factory indisponível](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Selecione sua **assinatura**do Azure.
   3. Para o grupo de recursos, siga um destes Olá etapas a seguir: 
      
      - Selecione **usar existente** tooselect um grupo de recursos existente.
      - Selecione **criar novo** tooenter um nome para um grupo de recursos.
          
        Algumas das etapas neste tutorial Olá pressupõem que você use o nome da saudação: **ADFTutorialResourceGroup** Olá para grupo de recursos. toolearn sobre grupos de recursos, consulte [usando o recurso de grupos de toomanage os recursos do Azure](../azure-resource-manager/resource-group-overview.md).
   4. Selecione um **local** Olá fábrica de dados.
   5. Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.  
   6. Clique em **Criar**.
      
       ![Folha Nova data factory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir:
   
   ![Página inicial da data factory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Iniciar o Assistente de cópia
1. Na folha de fábrica de dados hello, clique em **copiar dados [visualização]** toolaunch Olá **Assistente para cópia de**. 
   
   > [!NOTE]
   > Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** definindo as configurações do navegador hello (ou) manter ele habilitado e criar uma exceção para  **login.microsoftonline.com** e tente iniciar o Assistente de saudação novamente.
2. Em Olá **propriedades** página:
   
   1. Insira **CopyFromBlobToAzureSql** para o **Nome da tarefa**
   2. Insira uma **descrição** (opcional).
   3. Saudação de alteração **data/hora inicial** e hello **data hora de término** para que a data de término hello é definir tootoday e iniciar data toofive dias.  
   4. Clique em **Avançar**.  
      
      ![Ferramenta de Cópia - página Propriedades](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Em Olá **repositório de dados de origem** , clique em **armazenamento de BLOBs do Azure** lado a lado. Você pode usar esse repositório de dados de origem do página toospecify Olá para tarefas de cópia de saudação. 
   
    ![Ferramenta de Cópia - página de repositório de dados de origem](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Em Olá **especificar conta de armazenamento de BLOBs do Azure Olá** página:
   
   1. Insira **AzureStorageLinkedService** para o **Nome do serviço vinculado**.
   2. Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.
   3. Selecione sua **assinatura**do Azure.  
   4. Selecione um **conta de armazenamento do Azure** de saudação lista de armazenamento do Azure contas disponível na assinatura de saudação selecionada. Você também pode escolher tooenter configurações de conta de armazenamento manualmente selecionando **inserir manualmente** opção Olá **método de seleção de conta**e, em seguida, clique em **próximo**. 
      
      ![Copie a ferramenta - especificar conta de armazenamento de BLOBs do Azure Olá](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. Em **pasta ou escolha o arquivo de entrada hello** página:
   
   1. Clique duas vezes em **adftutorial** (pasta).
   2. Selecione **emp.txt** e clique em **Escolher**
      
      ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Em Olá **pasta ou escolha o arquivo de entrada hello** , clique em **próximo**. Não selecione **Cópia binária**. 
   
    ![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Em Olá **as configurações de formato de arquivo** página, consulte delimitadores hello e esquema de saudação que é detectada automaticamente pelo Assistente de saudação Analisando arquivo hello. Você também pode inserir delimitadores Olá manualmente para Olá cópia Assistente toostop detectar automaticamente ou toooverride. Clique em **próximo** Após examinar delimitadores hello e visualizar dados. 
   
    ![Ferramenta de Cópia - configurações de formato de arquivo](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Em dados de destino de saudação repositório de página, selecione **banco de dados do SQL Azure**e clique em **próximo**.
   
    ![Ferramenta de Cópia - escolha o repositório de destino](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. Em **banco de dados do SQL Azure especifique Olá** página:
   
   1. Digite **AzureSqlLinkedService** para Olá **nome de Conexão** campo.
   2. Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de servidor/banco de dados**.
   3. Selecione sua **assinatura**do Azure.  
   4. Selecione **Nome do servidor** e **Banco de Dados**.
   5. Insira o **Nome de usuário** e a **Senha**.
   6. Clique em **Avançar**.  
      
      ![Ferramenta de Cópia - especifique o banco de dados SQL do Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Em Olá **mapeamento de tabela** página, selecione **emp** para Olá **destino** campo da lista suspensa de saudação, clique em **a seta para baixo** (opcional) toosee Olá esquema e toopreview Olá dados.
    
     ![Ferramenta de Cópia - mapeamento de tabela](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Em Olá **mapeamento de esquema** , clique em **próximo**.
    
    ![Ferramenta de Cópia - mapeamento de esquema](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Em Olá **as configurações de desempenho** , clique em **próximo**. 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Revise informações Olá **resumo** página e, em seguida, clique em **concluir**. Assistente de saudação cria um pipeline, dois conjuntos de dados (de entrada e saída) e dois serviços vinculados na fábrica de dados de saudação (a partir de onde você iniciou Olá Assistente para copiar). 
    
    ![Ferramenta de cópia - configurações de desempenho](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Iniciar o monitor e gerenciar aplicativo
1. Em Olá **implantação** página, clique no link de saudação: `Click here toomonitor copy pipeline`.
   
   ![Ferramenta de Cópia - implantação bem-sucedida](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. saudação de monitoramento do aplicativo é iniciada em uma guia separada em seu navegador da web.   
   
   ![Aplicativo de Monitoramento](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. toosee hello mais recente status de fatias de hora em hora, clique em **atualizar** botão Olá **atividade WINDOWS** lista na parte inferior da saudação. Você vê cinco janelas de atividade de cinco dias entre horários de início e término para o pipeline de saudação. lista de saudação não será atualizada automaticamente, para que você pode precisar tooclick atualizar algumas vezes antes de ver todas as janelas de atividade de saudação em estado pronto do hello. 
4. Selecione uma janela de atividade na lista de saudação. Consulte os detalhes Olá sobre ele Olá **Pesquisador de objetos de janela de atividade** em saudação à direita.

    ![Detalhes da janela Atividade](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Observe que as datas de saudação 11, 12, 13, 14 e 15 na cor verde, o que significa que já foram produzidas Olá diário fatias de saída para essas datas. Também consulte essa codificação por cores no pipeline hello e Olá conjunto de dados de saída no modo de exibição de diagrama de saudação. Na etapa anterior de Olá, observe que duas fatias já foram produzidas, uma fatia está sendo processada no momento e hello outros dois estão esperando toobe processada (com base em Olá codificação por cores). 

    Para saber mais sobre como usar o aplicativo, confira [Monitorar e gerenciar o pipeline usando o aplicativo de monitoramento](data-factory-monitor-manage-app.md) artigo.

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Para obter detalhes sobre campos/propriedades que você vê no Assistente para cópia de saudação para um repositório de dados, clique o link Olá Olá repositório de dados na tabela de saudação. 
