---
title: "um serviço web de aprendizado de máquina do aaaDeploy | Microsoft Docs"
description: "Como tooconvert um treinamento experimentar tooa experimento de previsão, prepará-la para implantação, em seguida, implantá-lo como um serviço web de aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Implantar um serviço Web de Azure Machine Learning
O aprendizado de máquina do Azure permite que você toobuild, testar e implantar soluções de análise preditivas.

Em um ponto de exibição de alto nível, isso é feito em três etapas:

* **[Criar uma experiência de treinamento]**  -estúdio de aprendizado de máquina do Azure é um ambiente de colaboração de desenvolvimento visual que você use tootrain e testar um análise de previsão de modelo usando dados de treinamento que você fornecer.
* **[Convertê-lo a experiência de previsão tooa]**  - uma vez que o modelo foi treinado com dados existentes e você está pronto toouse-tooscore novos dados, preparar e simplificar sua experiência para previsões.
* **[Implantá-lo como um serviço Web]**: você pode implantar um teste preditivo como um serviço Web do Azure [novo] ou [clássico]. Os usuários podem enviar o modelo de dados de tooyour e receber as previsões do modelo.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Criar um teste de treinamento
tootrain um modelo de análise preditiva, que você usar o estúdio de aprendizado de máquina do Azure toocreate uma experiência de treinamento em que você incluir vários módulos tooload treinamento dados, preparar dados Olá conforme necessário, aplica algoritmos de aprendizagem de máquina e avaliar os resultados de saudação . Você pode iterar em uma experiência e tente toocompare de algoritmos de aprendizado de máquina diferente e avaliar os resultados de saudação.

processo de saudação de criar e gerenciar experiências de treinamento é abordado mais detalhadamente em outro lugar. Para obter mais informações, consulte estes artigos:

* 
            [Criar um experimento simples no Azure Machine Learning Studio](machine-learning-create-experiment.md)
* 
            [Desenvolver uma solução preditiva com o Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)
* 
            [Importar seus dados de treinamento para o Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* 
            [Gerenciar iterações de teste no Machine Learning Studio do Microsoft Azure](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Converter a experiência de previsão do hello treinamento experimento tooa
Depois que você treinou seu modelo, você está pronto tooconvert experimentar o treinamento para um experiência previsível tooscore novos dados.

Convertendo tooa previsão experiências, você está obtendo o toobe pronto treinado implantado como um serviço web de pontuação. Os usuários do serviço web de saudação podem enviar dados de entrada tooyour modelo e seu modelo enviará resultados da previsão Olá voltar. Como converter tooa previsão experiências, tenha em mente, como você espera que seu toobe modelo usado por outras pessoas.

tooconvert o tooa de experiência de treinamento previsão experiências, clique em **executar** na Olá inferior da tela de experimento hello, clique em **configurar o serviço Web**, em seguida, selecione **serviço Web de previsão** .

![Converter tooscoring experiência](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Para obter mais informações sobre como tooperform essa conversão, consulte [como tooprepare seu modelo de implantação no estúdio de aprendizado de máquina do Azure](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Olá etapas a seguir descrevem a implantação de um experimento previsão como um novo serviço web. Você também pode implantar o experimento hello como serviço de web clássico.

## <a name="deploy-it-as-a-web-service"></a>Implantá-lo como um serviço Web

Você pode implantar o experimento previsão hello como um novo serviço da web ou como um serviço da web clássico.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Implantar o experimento previsão hello como um novo serviço da web
Agora que a experiência de previsão Olá tenha sido preparada, você pode implantá-lo como um novo serviço web do Azure. Usando o serviço web de hello, os usuários podem enviar o modelo de dados de tooyour e modelo Olá retornará suas previsões.

toodeploy experiências, clique em sua previsão **executar** final Olá Olá experimentar tela. Depois que a experiência de saudação concluiu a execução, clique em **implantar o serviço da Web** e selecione **implantar o serviço da Web [novo]**.  página de implantação de saudação do portal do serviço de Web de aprendizado de máquina Olá é aberto.

> [!NOTE] 
> toodeploy um novo serviço da web, você deve ter permissões suficientes no hello assinatura toowhich você implantar o serviço web de saudação. Para obter mais informações, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Página de teste de implantação do portal de Serviços Web do Machine Learning
Na página de teste implantar hello, insira um nome para o serviço web de saudação.
Selecione um plano de preços. Se você tiver um plano de preços existente, que você poderá selecioná-lo, caso contrário, você deve criar um novo plano de preço para o serviço de saudação.

1. Em Olá **plano de preço** lista suspensa, selecione um plano existente ou selecione Olá **selecione novo plano** opção.
2. Em **nome do plano de**, digite um nome que identifique Olá plano na sua conta.
3. Selecione uma saudação **níveis mensal planejar**. plano de saudação camadas padrão toohello planos para sua região padrão e o serviço web é implantado toothat região.

Clique em **implantar** e hello **Quickstart** página para seu serviço da web é aberta.

página de início rápido de serviço Olá web fornece acesso e orientação em tarefas mais comuns hello, que você irá executar depois de criar um serviço web. A partir daqui, você pode acessar facilmente a página de teste hello e consumir página.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Gerenciar seu Novo serviço Web
tootest o novo serviço da web, clique em **testar o serviço web** em tarefas comuns. Na página de teste hello, você pode testar o serviço da web como um serviço de solicitação-resposta (RR) ou um serviço de execução de lote (BES).

página de teste RRS Olá exibe Olá entradas, saídas e quaisquer parâmetros globais que você definiu para o teste de saudação. tootest serviço de web hello, você pode inserir manualmente os valores apropriados para entradas de saudação ou forneça um arquivo formatado do CSV (valor) separada por vírgulas que contém valores de teste de saudação.

tootest usando RRS, de modo de exibição de lista hello, insira os valores apropriados para entradas de saudação e clique em **solicitação-resposta teste**. Exibem os resultados de previsão em Olá toohello de coluna de saída à esquerda.

![Implantar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

tootest BES, clique **lote**. Na página de teste do lote hello, clique em Procurar em sua entrada e selecione um arquivo CSV que contém os valores de exemplo apropriado. Se você não tiver um arquivo CSV e você criou sua experiência de previsão usando o estúdio de aprendizado de máquina, você pode baixar o conjunto de dados Olá para sua experiência de previsão e usá-lo.

conjunto de dados toodownload hello, abrir estúdio de aprendizado de máquina. Abra sua experiência de previsão e entrada Olá para o teste de clique do botão direito. No menu de contexto hello, selecione **dataset** e, em seguida, selecione **baixar**.

![Implantar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Clique em **Testar**. Exibe o status da saudação do seu trabalho de execução de lote direito toohello **trabalhos de lote de teste**.

![Implantar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Em Olá **configuração** página, alterar a descrição da saudação, title, atualizar a chave de conta de armazenamento hello e ativar dados de exemplo para o serviço web.

![Configurar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Quando você tiver implantado o serviço web de saudação, você pode:

* **Acesso** -lo por meio da API do serviço web hello.
* **Gerenciar** -lo por meio de aprendizado de máquina do Azure portal de serviços da web ou Olá portal clássico do Azure.
* **Atualizá-lo** se o seu modelo for alterado.

#### <a name="access-your-new-web-service"></a>Acessar seu Novo serviço Web
Depois de implantar seu serviço web do estúdio de aprendizado de máquina, você pode enviar dados toohello serviço e receber respostas programaticamente.

Olá **consumir** página fornece todas as informações de saudação precisar tooaccess seu serviço web. Por exemplo, a chave de API de saudação é tooallow autorizado acesso toohello serviço fornecido.

Para obter mais informações sobre como acessar um serviço da web de aprendizado de máquina, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Gerenciar seu Novo serviço Web
É possível gerenciar o Novo serviço Web no portal dos Serviços Web do Machine Learning. De saudação [página principal do portal](https://services.azureml-test.net/), clique em **serviços Web**. Na página de serviços web hello, você pode excluir ou copiar um serviço. toomonitor um serviço específico, clique em serviço hello e, em seguida, clique em **painel**. trabalhos de lote toomonitor associados ao serviço web de saudação, clique em **o Log de solicitações de lote**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Implantar a experiência previsível hello como um serviço da web clássico

Agora que tenha sido preparado suficientemente experimento previsão Olá, você pode implantá-lo como um serviço da web do Azure clássico. Usando o serviço web de hello, os usuários podem enviar o modelo de dados de tooyour e modelo Olá retornará suas previsões.

toodeploy experiências, clique em sua previsão **executar** final Olá Olá experimentar tela e, em seguida, clique em **implantar o serviço da Web**. Olá web serviço está configurado e é colocados no painel de serviço web hello.

![Implantar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Testar seu serviço Web Clássico

Você pode testar o serviço web de saudação no portal de serviços de Web do aprendizado de máquina hello ou estúdio de aprendizado de máquina.

Olá tootest serviço web de resposta da solicitação, clique em Olá **teste** botão no painel de serviço web hello. Uma caixa de diálogo é exibida tooask você Olá para dados de entrada para o serviço de saudação. Essas são colunas Olá esperadas pelo Olá experimento de pontuação. Insira um conjunto de dados e clique em **OK**. resultados de saudação gerados pelo serviço da web de saudação são exibidos na parte inferior de saudação do painel de saudação.

Você pode clicar em Olá **teste** visualizar link tootest o serviço no portal de serviços de Web de aprendizado de máquina do Azure hello como mostrado anteriormente Olá nova seção de serviço da web.

Olá tootest serviço de execução de lote, clique em **teste** link de visualização. Na página de teste do lote hello, clique em Procurar em sua entrada e selecione um arquivo CSV que contém os valores de exemplo apropriado. Se você não tiver um arquivo CSV e você criou sua experiência de previsão usando o estúdio de aprendizado de máquina, você pode baixar o conjunto de dados Olá para sua experiência de previsão e usá-lo.

![Testar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Em Olá **configuração** página, você pode alterar o nome para exibição do serviço Olá Olá e dê a ele uma descrição. Olá nome e a descrição é exibida no hello [portal clássico do Azure](http://manage.windowsazure.com/) onde você pode gerenciar seus serviços da web.

Você pode fornecer uma descrição dos dados de entrada, dados de saída e parâmetros de serviço Web inserindo uma cadeia de caracteres para cada coluna em **INPUT SCHEMA**, **OUTPUT SCHEMA**, e **Web SERVICE PARAMETER**. Essas descrições são usadas na documentação de código de exemplo hello fornecida para o serviço web de saudação.

Você pode habilitar o log toodiagnose as falhas que você está vendo quando seu serviço web é acessado. Para obter mais informações, consulte [Habilitar o log de serviços Web de Machine Learning](machine-learning-web-services-logging.md).

![Configurar o serviço web de saudação](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

Você também pode configurar pontos de extremidade de saudação do serviço web de saudação em Olá serviços de Web de aprendizado de máquina do Azure portal toohello procedimento semelhante mostrado anteriormente Olá nova seção de serviço da web. Olá opções forem diferentes, você pode adicionar ou alterar a descrição do serviço hello, habilite o log e habilitar dados de exemplo para teste.

#### <a name="access-your-classic-web-service"></a>Acessar seu serviço Web Clássico
Depois de implantar seu serviço web do estúdio de aprendizado de máquina, você pode enviar dados toohello serviço e receber respostas programaticamente.

Painel de saudação fornece todas as informações de saudação precisar tooaccess seu serviço web. Por exemplo, a chave de API Olá é fornecida tooallow autorizado acesso toohello serviço e páginas de Ajuda da API são fornecidas toohelp que você começar a escrever seu código.

Para obter mais informações sobre como acessar um serviço da web de aprendizado de máquina, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Gerenciar seu serviço Web Clássico
Há várias ações, você pode executar toomonitor um serviço web. Você pode atualizá-lo e excluí-lo. Você também pode adicionar o serviço web do pontos de extremidade adicionais tooa clássico no ponto de extremidade do adição toohello padrão que é criado quando você implantá-lo.

Para obter mais informações, consulte [gerenciar um espaço de trabalho do aprendizado de máquina do Azure](machine-learning-manage-workspace.md) e [gerenciar um serviço web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Olá web serviço de atualização
Você pode fazer alterações tooyour web service, como atualizar o modelo de saudação com dados de treinamento adicional e implantá-lo novamente, substituindo o serviço da web hello.

tooupdate serviço de web Olá, abra experimento previsão original Olá você usou o serviço web do toodeploy Olá e faça uma cópia editável clicando **Salvar como**. Faça as alterações e clique em **Implantar Serviço Web**.

Porque esse teste antes de você implantou, será perguntado se você deseja toooverwrite (serviço de Web clássico) ou serviço existente de saudação de atualização (novo serviço da web). Clicando em **Sim** ou **atualização** interrompe o serviço da web existente de saudação e implanta experimento de previsão nova Olá é implantado em seu lugar.

> [!NOTE]
> Se você fez as alterações de configuração no serviço da web hello, por exemplo, inserindo um novo nome de exibição ou a descrição, você precisará tooenter esses valores novamente.
> 
> 

Uma opção para atualizar o serviço da web é o modelo de saudação do tooretrain programaticamente. Para obter mais informações, consulte [Treinar novamente os modelos de Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md).

<!-- internal links -->
[Criar uma experiência de treinamento]: #create-a-training-experiment
[Convertê-lo a experiência de previsão tooa]: #convert-the-training-experiment-to-a-predictive-experiment
[Implantá-lo como um serviço Web]: #deploy-it-as-a-web-service
[novo]: #deploy-the-predictive-experiment-as-a-new-Web-service
[clássico]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
