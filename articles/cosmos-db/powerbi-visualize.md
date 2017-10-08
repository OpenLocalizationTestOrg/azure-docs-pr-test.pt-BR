---
title: tutorial de BI aaaPower para conector de banco de dados do Azure Cosmos | Microsoft Docs
description: "Use este tooimport tutorial do Power BI JSON, criar relatórios sofisticados e visualizar dados usando o conector do Power BI e o banco de dados do Azure Cosmos hello."
keywords: tutorial do power bi, visualizar dados, conector do power bi
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: cd1b7f70-ef99-40b7-ab1c-f5f3e97641f7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: mimig
ms.openlocfilehash: ca0bb8b76db8ef2ec936722b682af6a9488a3501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="power-bi-tutorial-for-azure-cosmos-db-visualize-data-using-hello-power-bi-connector"></a>Tutorial do Power BI para o banco de dados do Azure Cosmos: visualizar dados usando o conector do Power BI Olá
[PowerBI.com](https://powerbi.microsoft.com/) é um serviço online, onde você pode criar e compartilhar relatórios e painéis com dados tooyou importante e sua organização.  Power BI Desktop é dedicado dados de relatório que permite que você ferramenta de criação tooretrieve de várias fontes de dados, mesclar e transformar dados hello, criar visualizações e relatórios avançados e publicar relatórios de saudação tooPower BI.  Com a versão mais recente de saudação do Power BI Desktop, agora você pode conectar tooyour Cosmos DB conta por meio do conector do banco de dados do Cosmos Olá para o Power BI.   

Neste tutorial do Power BI, vamos percorrer Olá etapas tooconnect tooa conta de banco de dados do Cosmos no Power BI Desktop, navegue coleção tooa onde desejamos tooextract Olá dados usando Olá Navigator, transformar dados JSON em formato tabular, usando a consulta de área de trabalho do Power BI Editor e criar e publicar um relatório tooPowerBI.com.

Após concluir este tutorial do Power BI, você será capaz de tooanswer Olá perguntas a seguir:  

* Como posso criar relatórios com os dados do Cosmos DB usando o Power BI Desktop?
* Como conectar a conta de banco de dados do Cosmos tooa no Power BI Desktop?
* Como posso recuperar dados de uma coleção no Power BI Desktop?
* Como posso transformar dados JSON aninhados no Power BI Desktop?
* Como posso publicar e compartilhar meus relatórios no PowerBI.com?

> [!NOTE]
> conector do Power BI Olá para o banco de dados do Azure Cosmos conecta tooPower BI Desktop para extração e transformação de dados. Os relatórios criados no Power BI Desktop podem ser publicados tooPowerBI.com. Extração direta e transformação de dados do Azure Cosmos DB não podem ser executadas no PowerBI.com. 

## <a name="prerequisites"></a>Pré-requisitos
Antes de seguir as instruções de saudação neste tutorial do Power BI, certifique-se de que você tenha acesso toohello recursos a seguir:

* [versão mais recente de saudação do Power BI Desktop](https://powerbi.microsoft.com/desktop).
* Conta de demonstração do acesso tooour ou dados em sua conta do banco de dados do Cosmos.
  * conta de demonstração de Olá é preenchida com dados de vulcões de saudação mostrados neste tutorial. Essa conta de demonstração não está vinculada por nenhum SLA e se destina apenas a fins de demonstração.  Nós reservamos toothis para modificações Olá toomake direita demonstração conta incluindo mas não limitado a, encerrando Olá conta, alterando a chave de hello, restringindo o acesso, alterar e excluir dados Olá, a qualquer momento sem aviso antecipado ou motivo.
    * URL: https://analytics.documents.azure.com
    * Chave somente leitura: MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==
  * Ou, toocreate sua própria conta, consulte [criar uma conta de banco de dados do banco de dados do Azure Cosmos usando Olá portal do Azure](https://azure.microsoft.com/documentation/articles/create-account/). Em seguida, tooget exemplo vulcões dados semelhante toowhat usados neste tutorial (mas não contém blocos de GeoJSON Olá), consulte Olá [site NOAA](https://www.ngdc.noaa.gov/nndc/struts/form?t=102557&s=5&d=5) e, em seguida, importar dados de saudação com hello [migração de dados do banco de dados do Azure Cosmos ferramenta](import-data.md).

tooshare seus relatórios no PowerBI.com, você deve ter uma conta no PowerBI.com.  toolearn mais sobre o Power BI para gratuito e o Power BI Pro, visite [https://powerbi.microsoft.com/pricing](https://powerbi.microsoft.com/pricing).

## <a name="lets-get-started"></a>Vamos começar
Neste tutorial, vamos imaginar que você é um geologist estudar basquete mundo hello.  dados de vulcões Olá são armazenados em uma conta de banco de dados do Cosmos e documentos JSON Olá aparência Olá documento de exemplo a seguir.

    {
        "Volcano Name": "Rainier",
           "Country": "United States",
          "Region": "US-Washington",
          "Location": {
            "type": "Point",
            "coordinates": [
              -121.758,
              46.87
            ]
          },
          "Elevation": 4392,
          "Type": "Stratovolcano",
          "Status": "Dendrochronology",
          "Last Known Eruption": "Last known eruption from 1800-1899, inclusive"
    }

Você deseja tooretrieve Olá vulcões dados Olá Cosmos DB de conta e visualizar dados em um relatório interativo do Power BI como Olá relatórios a seguir.

![Ao concluir este tutorial do Power BI com o conector do Power BI hello, você será capaz de toovisualize dados com hello relatório do Power BI Desktop vulcões](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

Pronto toogive it um try? Vamos começar.

1. Execute o Power BI Desktop em sua estação de trabalho.
2. Depois de iniciar o Power BI Desktop, uma tela de *Boas-Vindas* é exibida.
   
    ![Tela de boas-vindas do Power BI Desktop — conector do Power BI](./media/powerbi-visualize/power_bi_connector_welcome.png)
3. Você pode **obter dados**, consulte **fontes recentes**, ou **abrir outros relatórios** diretamente da saudação *bem-vindo* tela.  Clique em Olá X na tela de saudação de tooclose Olá canto superior direito. Olá **relatório** Power BI Desktop é exibida.
   
    ![Exibição de relatório do Power BI Desktop — conector do Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview.png)
4. Selecione Olá **início** de faixa de opções, clique no **obter dados**.  Olá **obter dados** janela deve ser exibida.
5. Clique em **Azure**, selecione **Microsoft Azure DocumentDB (Beta)** e clique em **Conectar**. 

    ![Obtenção de dados do Power BI Desktop — conector do Power BI](./media/powerbi-visualize/power_bi_connector_pbigetdata.png)   
6. Em Olá **visualização conector** , clique em **continuar**. Olá **Connect do Microsoft Azure DocumentDB** janela é exibida.
7. Especificar Olá o URL de ponto de extremidade Cosmos DB conta seria como dados Olá tooretrieve, conforme mostrado abaixo e, em seguida, clique em **Okey**. toouse sua própria conta, você pode recuperar Olá caixa URL do URI de Olá Olá  **[chaves](manage-account.md#keys)**  folha de saudação portal do Azure. Olá toouse conta de demonstração, insira `https://analytics.documents.azure.com` Olá URL. 
   
    Deixe instrução SQL, nome da coleção e nome de banco de dados de saudação em branco como esses campos são opcionais.  Em vez disso, vamos usar Olá navegador tooselect Olá banco de dados e coleção tooidentify onde vêm os dados de saudação.
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Janela Conexão da Área de Trabalho](./media/powerbi-visualize/power_bi_connector_pbiconnectwindow.png)
8. Se você estiver conectando o ponto de extremidade toothis para Olá primeira vez, você será solicitado para a chave de conta hello. Para sua própria conta, recuperar a chave de saudação do hello **chave primária** caixa Olá  **[chaves somente leitura](manage-account.md#keys)**  folha de saudação portal do Azure. Para a conta de demonstração de Olá, chave de saudação é `MSr6kt7Gn0YRQbjd6RbTnTt7VHc5ohaAFu7osF0HdyQmfR+YhwCH2D2jcczVIR1LNK3nMPNBD31losN7lQ/fkw==`. Insira a chave apropriada hello e, em seguida, clique em **conectar**.
   
    Recomendamos que use Olá somente leitura ao criar relatórios.  Isso impedirá que a exposição desnecessária Olá chave mestra toopotential de riscos de segurança. chave de saudação somente leitura está disponível no hello [chaves](manage-account.md#keys) folha de Olá portal do Azure, ou você pode usar informações de conta de demonstração de Olá fornecidas acima.
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Chave de Conta](./media/powerbi-visualize/power_bi_connector_pbidocumentdbkey.png)
    
    > [!NOTE] 
    > Se você receber um erro que diz "banco de dados de saudação especificado não foi encontrado." Consulte as etapas de solução de saudação neste [problema do Power BI](https://community.powerbi.com/t5/Issues/Document-DB-Power-BI/idi-p/208200).
    
9. Quando a conta de saudação estiver conectada com êxito, Olá **navegador** será exibida.  Olá **navegador** mostrará uma lista de bancos de dados na conta de saudação.
10. Clique e expanda o banco de dados de Olá onde Olá dados para o relatório de saudação virão, se você estiver usando uma conta de demonstração de Olá, selecione **volcanodb**.   
11. Agora, selecione uma coleção que você irá recuperar dados de saudação do. Se você estiver usando a conta de demonstração de Olá, selecione **volcano1**.
    
    no painel de visualização Olá mostra uma lista de **registro** itens.  Um Documento é representado como um tipo **Registro** no Power BI. Da mesma forma, um bloco JSON aninhado dentro de um documento é também um **Registro**.
    
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Janela Navegador](./media/powerbi-visualize/power_bi_connector_pbinavigator.png)
12. Clique em **editar** toolaunch Olá Editor de consultas em uma nova janela tootransform Olá de dados.

## <a name="flattening-and-transforming-json-documents"></a>Nivelando e transformando documentos JSON
1. Alternar janela do Editor de consultas do Power BI toohello, onde hello **documento** coluna no painel central de saudação.
   ![Editor de Consultas do Power BI Desktop](./media/powerbi-visualize/power_bi_connector_pbiqueryeditor.png)
2. Clique em expansor Olá Olá direita da saudação **documento** cabeçalho de coluna.  menu de contexto de saudação com uma lista de campos aparecerá.  Selecionar campos Olá precisa para o relatório, por exemplo, nome vulcões, país, região, local, elevação, tipo, Status e último jogo saber e clique **Okey**.
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Expandir documentos](./media/powerbi-visualize/power_bi_connector_pbiqueryeditorexpander.png)
3. Painel de central Olá exibirá uma visualização dos resultados de saudação com hello campos selecionados.
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Nivelar resultados](./media/powerbi-visualize/power_bi_connector_pbiresultflatten.png)
4. Em nosso exemplo, a saudação propriedade local é um bloco de GeoJSON em um documento.  Como você pode ver, o Local é representado como um tipo **Registro** no Power BI Desktop.  
5. Clique em expansor Olá direita Olá Olá local do cabeçalho da coluna.  menu de contexto de saudação com campos de coordenadas e o tipo será exibida.  Vamos selecionar Olá coordenadas campo e clique em **Okey**.
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Registro de localização](./media/powerbi-visualize/power_bi_connector_pbilocationrecord.png)
6. Olá painel central agora mostra uma coluna de coordenadas de **lista** tipo.  Conforme mostrado no início de saudação do tutorial hello, Olá dados GeoJSON neste tutorial é do tipo de ponto com valores de Latitude e Longitude registrados na matriz de coordenadas de saudação.
   
    Olá coordenadas [0] elemento representa Longitude enquanto coordenadas [1] representa Latitude.
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Lista de coordenadas](./media/powerbi-visualize/power_bi_connector_pbiresultflattenlist.png)
7. Olá tooflatten coordena a matriz, criaremos um **coluna personalizada** chamado LatLong.  Selecione Olá **adicionar coluna** de faixa de opções e clique em **adicionar coluna personalizada**.  Olá **adicionar coluna personalizada** janela deve ser exibida.
8. Forneça um nome para a nova coluna hello, por exemplo, LatLong.
9. Em seguida, especifique a fórmula personalizada Olá para nova coluna de saudação.  Para nosso exemplo, valores de Latitude e Longitude de Olá separados por vírgula, como mostrado a seguir usando a seguinte fórmula de saudação serão concatenados: `Text.From([coordinates]{1})&","&Text.From([coordinates]{0})`. Clique em **OK**.
   
    Para obter mais informações sobre o DAX (Data Analysis Expressions), incluindo as funções DAX, visite [Noções básicas do DAX no Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/554619-dax-basics-in-power-bi-desktop).
   
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Adicionar Coluna Personalizada](./media/powerbi-visualize/power_bi_connector_pbicustomlatlong.png)
10. Agora, painel de central Olá mostrará Olá nova LatLong coluna preenchida com hello Latitude e valores de Longitude separados por uma vírgula.
    
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Coluna LatLong personalizada](./media/powerbi-visualize/power_bi_connector_pbicolumnlatlong.png)
    
    Se você receber um erro na coluna nova hello, verifique se etapas Olá aplicado em configurações de consulta correspondem Olá figura a seguir:
    
    ![As etapas aplicadas devem ser Origem, Navegação, Document.Location Expandido, Personalizado Adicionado](./media/powerbi-visualize/power-bi-applied-steps.png)
    
    Se as etapas são diferentes, exclua Olá etapas adicionais e tente adicionar coluna personalizada Olá novamente. 
11. Agora podemos concluiu dados nivelamento de saudação em formato tabular.  Você pode aproveitar todos os recursos de saudação disponíveis no hello tooshape do Editor de consultas e transformar dados no banco de dados do Cosmos.  Se você estiver usando o exemplo hello, altere o tipo de dados Olá para elevação muito**número inteiro** alterando Olá **tipo de dados** em Olá **início** faixa de opções.
    
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Alterar tipo de coluna](./media/powerbi-visualize/power_bi_connector_pbichangetype.png)
12. Clique em **fechar e aplicar** toosave modelo de dados de saudação.
    
    ![Tutorial do Power BI para o conector do Azure Cosmos DB para Power BI – Fechar e Aplicar](./media/powerbi-visualize/power_bi_connector_pbicloseapply.png)

<a id="build-the-reports"></a>
## <a name="build-hello-reports"></a>Criar relatórios de saudação
O modo de exibição do Power BI Desktop relatório é onde você pode começar a criar relatórios toovisualize dados.  Você pode criar relatórios arrastando e soltando campos no hello **relatório** tela.

![Exibição de relatório do Power BI Desktop — conector do Power BI](./media/powerbi-visualize/power_bi_connector_pbireportview2.png)

Em Olá exibição de relatório, você deve encontrar:

1. Olá **campos** painel, isso é onde você verá uma lista de modelos de dados com campos que você pode usar para seus relatórios.
2. Olá **visualizações** painel. Um relatório pode conter uma ou várias visualizações.  Selecione tipos de visual Olá atende às suas necessidades de saudação **visualizações** painel.
3. Olá **relatório** tela, isso é onde você irá criar visuais Olá para o relatório.
4. Olá **relatório** página. Você pode adicionar várias páginas do relatório no Power BI Desktop.

a seguir Olá mostra etapas básicas de saudação de criação de um relatório de modo de exibição de mapa interativo simples.

1. Para nosso exemplo, vamos criar um modo de exibição de mapa mostrando Olá local de cada vulcões.  Em Olá **visualizações** painel, clique no tipo de visual de mapa Olá conforme realçado na captura de tela de saudação acima.  Você deve ver o tipo de visual de mapa do hello pintado no hello **relatório** tela.  Olá **visualização** painel também deve exibir um conjunto de propriedades relacionadas toohello tipo visual de mapa.
2. Agora, arraste e solte o campo de LatLong de saudação do hello **campos** painel toohello **local** propriedade **visualizações** painel.
3. Em seguida, arraste e solte Olá vulcões nome campo toohello **legenda** propriedade.  
4. Em seguida, arraste e solte Olá elevação campo toohello **tamanho** propriedade.  
5. Agora você deve ver Olá mapa visual mostrando um conjunto de bolhas que indica o local de saudação de cada vulcões com tamanho de saudação de bolha Olá correlacionando toohello elevação de vulcões hello.
6. Agora você criou um relatório básico.  Você pode personalizar ainda mais relatório Olá adicionando mais visualizações.  Em nosso caso, adicionamos um interativa de relatório tipo vulcões saudação do toomake de segmentação de dados.  
   
    ![Captura de tela de relatório de Power BI Desktop final Olá após a conclusão do tutorial do Power BI Olá para o banco de dados do Azure Cosmos](./media/powerbi-visualize/power_bi_connector_pbireportfinal.png)

## <a name="publish-and-share-your-report"></a>Publicar e compartilhar seu relatório
tooshare seu relatório, você deve ter uma conta no PowerBI.com.

1. No hello Power BI Desktop, clique em Olá **início** faixa de opções.
2. Clique em **Publicar**.  Será solicitada tooenter Olá nome e uma senha para sua conta PowerBI.com.
3. Depois que a credencial de saudação foi autenticado, o relatório de Olá é publicado tooyour destino selecionado.
4. Clique em **'PowerBITutorial.pbix' Abrir no Power BI** toosee e compartilhar seu relatório em PowerBI.com.
   
    ![Publicação tooPower BI êxito! Abrir tutorial no Power BI](./media/powerbi-visualize/power_bi_connector_open_in_powerbi.png)

## <a name="create-a-dashboard-in-powerbicom"></a>Criar um painel no PowerBI.com
Agora que você tem um relatório, vamos compartilhá-lo no PowerBI.com

Quando você publicar o relatório do Power BI Desktop tooPowerBI.com, ele gera um **relatório** e um **Dataset** em seu locatário PowerBI.com. Por exemplo, após você publicou um relatório chamado **PowerBITutorial** tooPowerBI.com, você verá PowerBITutorial em ambos os Olá **relatórios** e **conjuntos de dados** seções em PowerBI.com.

   ![Captura de tela de Olá novo relatório e conjunto de dados no PowerBI.com](./media/powerbi-visualize/powerbi-reports-datasets.png)

toocreate um dashboard compartilhável, clique em Olá **fixar página dinâmica** botão no seu relatório em PowerBI.com.

   ![Captura de tela de Olá novo relatório e conjunto de dados no PowerBI.com](./media/powerbi-visualize/power-bi-pin-live-tile.png)

Siga as instruções de saudação de [fixar um bloco de um relatório](https://powerbi.microsoft.com/documentation/powerbi-service-pin-a-tile-to-a-dashboard-from-a-report/#pin-a-tile-from-a-report) toocreate um novo painel. 

Você também pode fazer modificações ad hoc tooreport antes de criar um painel. No entanto, é recomendável que você use as modificações do Power BI Desktop tooperform hello e republicar Olá tooPowerBI.com de relatório.

## <a name="refresh-data-in-powerbicom"></a>Atualizar dados no PowerBI.com
Há duas maneiras de dados toorefresh, ad hoc e agendados.

Para uma atualização ad-hoc, basta clicar no eclipses hello (...) por Olá **conjunto de dados**, por exemplo, PowerBITutorial. Você deve ver uma lista de ações, incluindo **Atualizar Agora**. Clique em **atualizar agora** toorefresh dados de saudação.

![Captura de tela de Atualizar Agora no PowerBI.com](./media/powerbi-visualize/power-bi-refresh-now.png)

Para uma atualização agendada, Olá a seguir.

1. Clique em **agendar atualização** na lista de ações de saudação. 

    ![Captura de tela da saudação agendar atualização no PowerBI.com](./media/powerbi-visualize/power-bi-schedule-refresh.png)
2. Em Olá **configurações** página, expanda **credenciais da fonte de dados**. 
3. Clique em **Editar credenciais**. 
   
    pop-up de configurar Olá aparece. 
4. Insira a conta de banco de dados do Cosmos Olá tooconnect chave toohello para esse conjunto de dados, clique em **entrar**. 
5. Expanda **agendar atualização** e configurar a agenda de saudação que deseja toorefresh Olá dataset. 
6. Clique em **aplicar** e terminar Configurando a atualização agendada hello.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre o Power BI, consulte [Introdução ao Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/).
* toolearn mais sobre o banco de dados do Cosmos, consulte Olá [página de aterrissagem do banco de dados do Azure Cosmos documentação](https://azure.microsoft.com/documentation/services/documentdb/).

