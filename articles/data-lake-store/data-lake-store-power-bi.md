---
title: "dados de aaaAnalyze no repositório Data Lake usando o Power BI | Microsoft Docs"
description: "Usar dados do Power BI tooanalyze armazenados no repositório Azure Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57d19d27-e135-49d9-a7ea-46c48ef4e3bd
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 6a1bfa80fd1b0dda59b7eaaae9ca1585ba42783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-in-data-lake-store-by-using-power-bi"></a>Analisar dados no Repositório Data Lake usando o Power BI
Neste artigo, você aprenderá como toouse Power BI Desktop tooanalyze e visualizar os dados armazenados no repositório Azure Data Lake.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Conta do Repositório Azure Data Lake**. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md). Este artigo pressupõe que você já criou uma conta do repositório Data Lake, chamada **mybidatalakestore**e carregar um arquivo de dados de exemplo (**Drivers.txt**) tooit. Esse exemplo de arquivo está disponível para download no [Repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt).
* **Power BI Desktop**. Você pode baixá-lo no [Centro de Download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=45331). 

## <a name="create-a-report-in-power-bi-desktop"></a>Criar um relatório no Power BI Desktop
1. Inicie o Power BI Desktop em seu computador.
2. De saudação **início** de faixa de opções, clique em **obter dados**e, em seguida, clique em mais. Em Olá **obter dados** caixa de diálogo, clique em **Azure**, clique em **repositório Azure Data Lake**e, em seguida, clique em **conectar**.
   
    ![Conectar tooData Lake repositório](./media/data-lake-store-power-bi/get-data-lake-store-account.png "conectar tooData Lake repositório")
3. Se você vir uma caixa de diálogo sobre o conector de saudação em uma fase de desenvolvimento, optar por toocontinue.
4. Em Olá **Microsoft Azure Data Lake Store** caixa de diálogo, forneça Olá URL tooyour repositório Data Lake conta e, em seguida, clique em **Okey**.
   
    ![URL do Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-url.png "URL para Data Lake Store")
5. Na próxima caixa de diálogo hello, clique em **entrar** toosign na conta do repositório Data Lake. Você será redirecionado na página de entrada tooyour da organização. Siga Olá prompts toosign em conta hello.
   
    ![Entrar no Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-signin.png "Entrar no Data Lake Store")
6. Depois de entrar com sucesso, clique em **Conectar**.
   
    ![Conectar tooData Lake repositório](./media/data-lake-store-power-bi/get-data-lake-store-account-connect.png "conectar tooData Lake repositório")
7. próxima caixa de diálogo Olá mostra arquivo hello que conta do repositório Data Lake tooyour foi carregado. Verifique se as informações de saudação e, em seguida, clique em **carga**.
   
    ![Carregar dados no Data Lake Store](./media/data-lake-store-power-bi/get-data-lake-store-account-load.png "Carregar dados no Data Lake Store")
8. Depois que os dados de saudação foi carregados com êxito para o Power BI, você verá Olá Olá campos a seguir **campos** guia.
   
    ![Importar campos](./media/data-lake-store-power-bi/imported-fields.png "importado campos")
   
    No entanto, toovisualize e analisar dados hello, podemos preferir Olá dados toobe disponível por Olá campos a seguir
   
    ![Desejado campos](./media/data-lake-store-power-bi/desired-fields.png "desejado campos")
   
    Próximas etapas de hello, atualizaremos Olá consultar tooconvert Olá importado dados em formato de saudação desejado.
9. De saudação **início** de faixa de opções, clique em **editar consultas**.
   
    ![Editar consultas](./media/data-lake-store-power-bi/edit-queries.png "editar consultas")
10. Em Olá Editor de consultas, em Olá **conteúdo** coluna, clique em **binário**.
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query1.png "editar consultas")
11. Você verá um ícone de arquivo, que representa a saudação **Drivers.txt** arquivo carregado. Clique com botão direito arquivo hello e, em seguida, clique em **CSV**.    
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query2.png "editar consultas")
12. Você deve ver uma saída parecida com a que está abaixo. Os dados agora estão disponíveis em um formato que você pode usar toocreate visualizações.
    
    ![Editar consultas](./media/data-lake-store-power-bi/convert-query3.png "editar consultas")
13. De saudação **início** de faixa de opções, clique em **fechar e aplicar**e, em seguida, clique em **fechar e aplicar**.
    
    ![Editar consultas](./media/data-lake-store-power-bi/load-edited-query.png "editar consultas")
14. Depois que a consulta Olá é atualizada, Olá **campos** guia Mostrar Olá novos campos disponíveis para visualização.
    
    ![Atualizado campos](./media/data-lake-store-power-bi/updated-query-fields.png "atualizado campos")
15. Vamos crie um gráfico de pizza toorepresent drivers de Olá em cada cidade de um determinado país. Portanto, o toodo Verifique Olá seleções a seguir.
    
    1. Na guia de visualizações hello, clique em símbolo Olá para um gráfico de pizza.
       
        ![Criar um gráfico de pizza](./media/data-lake-store-power-bi/create-pie-chart.png "criar o gráfico de pizza")
    2. colunas de saudação que vamos toouse são **colunas 4** (nome de cidade Olá) e **coluna 7** (nome de país Olá). Arraste essas colunas da **campos** guia muito**visualizações** guia conforme mostrado abaixo.
       
        ![Criar visualizações](./media/data-lake-store-power-bi/create-visualizations.png "Criar visualizações")
    3. gráfico de pizza Olá agora deve se assemelhar como Olá mostrada abaixo.
       
        ![Gráfico de pizza](./media/data-lake-store-power-bi/pie-chart.png "Criar visualizações")
16. Selecionando um país específico de filtros de nível de página hello, agora você pode ver o número de saudação de drivers em cada cidade do país de saudação selecionada. Por exemplo, sob Olá **visualizações** guia em **filtros de nível de página**, selecione **Brasil**.
    
    ![Selecione um país](./media/data-lake-store-power-bi/select-country.png "selecione um país")
17. gráfico de pizza Olá é automaticamente atualizada toodisplay Olá drivers nas cidades de saudação do Brasil.
    
    ![Drivers em um país](./media/data-lake-store-power-bi/driver-per-country.png "Drivers por país")
18. De saudação **arquivo** menu, clique em **salvar** visualização de saudação toosave como um arquivo do Power BI Desktop.

## <a name="publish-report-toopower-bi-service"></a>Publicar relatório tooPower BI serviço
Depois de criar visualizações de saudação no Power BI Desktop, você pode compartilhá-lo com outras pessoas publicando-o serviço do Power BI toohello. Para obter instruções sobre como toodo que, consulte [publicar por meio do Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-upload-desktop-files/).

## <a name="see-also"></a>Consulte também
* [Analisar dados no Repositório Data Lake usando o Análise Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

