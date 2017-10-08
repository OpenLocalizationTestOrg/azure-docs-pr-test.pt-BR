---
title: "aaaCreate uma função que se integra com aplicativos de lógica do Azure | Microsoft Docs"
description: "Criar uma função que integra o sentimento de tweet toocategorize Azure lógica de aplicativos e serviços cognitivas do Azure e enviar notificações quando o sentimento é ruim."
services: functions, logic-apps, cognitive-services
keywords: "fluxo de trabalho, aplicativos de nuvem, serviços de nuvem, processos de negócios, integração de sistemas, integração de aplicativos empresariais, EAI"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Criar uma função que se integra aos Aplicativos Lógicos do Azure

As funções do Azure integra os aplicativos lógicos do Azure Olá lógica do Designer de aplicativos. Essa integração permite que você usar Olá computando a energia de funções em orquestrações com outros serviços de terceiros e o Azure. 

Este tutorial mostra como toouse funciona com lógica de aplicativos e serviços cognitivas Azure sentimento tooanalyze de postagens no Twitter. Uma função HTTP disparado categoriza tweets como verde, amarelo ou vermelho com base na classificação de sentimento hello. Um email é enviado quando um sentimento inadequado é detectado. 

![imagem dos dois primeiros passos do aplicativo no Designer de Aplicativos Lógicos](media/functions-twitter-email/designer1.png)

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar uma conta dos Serviços Cognitivos.
> * Crie uma função que categorize o sentimento do tweet.
> * Crie um aplicativo lógico que se conecta tooTwitter.
> * Adicione aplicativo de lógica de toohello de detecção sensibilidade. 
> * Conecte-se a função de toohello de aplicativo hello lógica.
> * Envie um email com base na resposta de saudação do função hello.

## <a name="prerequisites"></a>Pré-requisitos

+ Uma conta do [Twitter](https://twitter.com/) ativa. 
+ Uma conta do [Outlook.com](https://outlook.com/) (para enviar notificações).
+ Este tópico usa como seus recursos de saudação ponto inicial criados no [criar sua primeira função da saudação portal do Azure](functions-create-first-azure-function.md).  
Se você ainda não fez isso, conclua toocreate de agora essas etapas seu aplicativo de função.

## <a name="create-a-cognitive-services-account"></a>Criar uma conta dos Serviços Cognitivos

Uma conta de serviços Cognitivos é necessário toodetect Olá sentimento de tweets que está sendo monitorado.

1. Entrar toohello [portal do Azure](https://portal.azure.com/).

2. Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

3. Clique em **Dados + Análise** > **Serviços Cognitivos**. Em seguida, usar Olá configurações como especificado na tabela Olá, aceite os termos de hello e verificar **toodashboard Pin**.

    ![Criar folha de conta Cognitiva](media/functions-twitter-email/cog_svcs_account.png)

    | Configuração      |  Valor sugerido   | Descrição                                        |
    | --- | --- | --- |
    | **Nome** | MyCognitiveServicesAccnt | Escolha um nome de conta exclusivo. |
    | **Tipo de API** | API de Análise de Texto | A API usada tooanalyze texto.  |
    | **Localidade** | Oeste dos EUA | Atualmente, apenas o **Oeste dos EUA** está disponível para análise de texto. |
    | **Tipo de preços** | F0 | Inicie com o nível mais baixo de saudação. Se você executar fora de chamadas, dimensione a camada superior tooa.|
    | **Grupo de recursos** | myResourceGroup | Use Olá mesmo grupo de recursos para todos os serviços neste tutorial.|

4. Clique em **criar** toocreate sua conta. Depois de saudação conta é criada, clique em seu novo painel de toohello fixados da conta de serviços Cognitivos. 

5. Na conta de saudação, clique em **chaves**e, em seguida, copie o valor de saudação do **chave 1** e salvá-lo. Você usa essa chave tooconnect Olá lógica aplicativo tooyour conta de serviços Cognitivos. 
 
    ![simétricas](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Criar função hello

Funções fornece toooffload uma ótima maneira de tarefas de processamento em um fluxo de trabalho de aplicativos de lógica. Este tutorial usa um pontuações HTTP disparado função tooprocess tweet sentimento de serviços Cognitivos e retornar um valor de categoria.  

1. Expanda seu aplicativo de função, clique em Olá  **+**  botão Avançar muito**funções**, clique em Olá **HTTPTrigger** modelo. Tipo `CategorizeSentiment` para a função hello **nome** e clique em **criar**.

    ![Folha Aplicativos de Funções, Funções +](media/functions-twitter-email/add_fun.png)

2. Substituir o conteúdo de saudação do arquivo de run.csx de saudação com hello código a seguir e, em seguida, clique em **salvar**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Esse código de função retorna uma categoria de cor com base em Olá sentimento pontuação recebida na solicitação de saudação. 

3. função de saudação tootest, clique em **teste** no guia de teste de Olá Olá tooexpand extrema direita. Digite um valor de `0.2` para Olá **corpo da solicitação**e, em seguida, clique em **executar**. Um valor de **vermelho** é retornado no corpo de saudação da resposta de saudação. 

    ![Testar função hello em Olá portal do Azure](./media/functions-twitter-email/test.png)

Agora você tem uma função que categoriza as pontuações de sentimento. Em seguida, você pode criar um aplicativo lógico que integra sua função às contas dos Serviços Cognitivos e do Twitter. 

## <a name="create-a-logic-app"></a>Criar um aplicativo lógico   

1. Em Olá portal do Azure, clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Clique em **Integração de Empresas** > **Aplicativo Lógico**. Em seguida, usar configurações de saudação como especificado na tabela Olá, verifique **Pin toodashboard**e clique em **criar**.
 
4. Em seguida, digite um **nome** como `TweetSentiment`, usar configurações de saudação conforme especificado na tabela de saudação, aceite os termos de saudação e verificar **toodashboard Pin**.

    ![Criar aplicativo lógico no hello portal do Azure](./media/functions-twitter-email/new_logicApp.png)

    | Configuração      |  Valor sugerido   | Descrição                                        |
    | ----------------- | ------------ | ------------- |
    | **Nome** | TweetSentiment | Escolha um nome apropriado para seu aplicativo. |
    | **Grupo de recursos** | myResourceGroup | A API usada tooanalyze texto.  |
    | **Localidade** | Leste dos EUA | Escolha um tooyou fechar do local. |
    | **Grupo de recursos** | myResourceGroup | Escolha Olá mesmo grupo de recursos existente como antes.|

4. Clique em **criar** toocreate seu aplicativo lógico. Depois que o aplicativo hello for criado, clique em seu novo painel toohello fixados de aplicativo lógica. Em seguida, no hello lógica do Designer de aplicativos, role para baixo e clique em Olá **aplicativo lógica em branco** modelo. 

    ![Modelo Aplicativo Lógico em Branco](media/functions-twitter-email/blank.png)

Agora você pode usar o hello lógica aplicativos tooadd serviços e disparadores tooyour aplicativo Designer.

## <a name="connect-tootwitter"></a>Conecte-se tooTwitter

Primeiro, crie um conta do Twitter do tooyour de conexão. Olá lógica aplicativo sonda tweets, que disparam Olá toorun de aplicativo.

1. No designer de saudação, clique em Olá **Twitter** de serviço e, em seguida, clique em Olá **quando um novo tweet for lançado** gatilho. Entrar tooyour conta do Twitter e autorizar aplicativos lógicos toouse sua conta.

2. Use configurações de gatilho do Twitter Olá conforme especificado na tabela de saudação. 

    ![Configurações do conector do Twitter](media/functions-twitter-email/azure_tweet.png)

    | Configuração      |  Valor sugerido   | Descrição                                        |
    | ----------------- | ------------ | ------------- |
    | **Texto da pesquisa** | #Azure | Use um hashtag que é popular para toogenerate tweets de novo no intervalo de saudação escolhida. Ao usar a camada gratuita hello e seu hashtag é muito popular, você pode rapidamente usar transações Olá em sua conta de serviços Cognitivos. |
    | **Frequência** | Minuto | unidade de frequência Olá usada para sondagem Twitter.  |
    | **Intervalo** | 15 | tempo de saudação decorrido entre as solicitações do Twitter, em unidades de frequência. |

3.  Clique em **salvar** tooconnect tooyour conta do Twitter. 

Agora o seu aplicativo é tooTwitter conectado. Em seguida, conecte-se sentimento de saudação do tootext análise toodetect de tweets coletados.

## <a name="add-sentiment-detection"></a>Adicionar detecção de sentimento

1. Clique em **Nova Etapa** e em **Adicionar uma ação**.

    ![Nova Etapa e, então, Adicionar uma ação](media/functions-twitter-email/new_step.png)

2. Em **escolher uma ação**, clique em **análises de texto**e, em seguida, clique em Olá **detectar sentimento** ação.

    ![Detectar Sentimento](media/functions-twitter-email/detect_sent.png)

3. Digite um nome de conexão como `MyCognitiveServicesConnection`, cole a chave de saudação para seus serviços Cognitivos conta que você salvou e clique em **criar**.  

4. Clique em **texto tooanalyze** > **Tweet texto**e, em seguida, clique em **salvar**.  

    ![Detectar Sentimento](media/functions-twitter-email/ds_tta.png)

Detecção sensibilidade já está configurado, você pode adicionar uma função de tooyour de conexão que consome a saída de pontuação de sensibilidade hello.

## <a name="connect-sentiment-output-tooyour-function"></a>Conecte-se a função de tooyour de saída de sentimento

1. No hello lógica do Designer de aplicativos, clique em **nova etapa** > **adicionar uma ação**e, em seguida, clique em **funções do Azure**. 

2. Clique em **escolher uma função do Azure**, selecione Olá **CategorizeSentiment** função que você criou anteriormente.  

    ![Caixa de função do Azure mostrando "Escolher uma Função do Azure"](media/functions-twitter-email/choose_fun.png)

3. Em **Corpo da Solicitação**, clique em **Pontuação** e em **Salvar**.

    ![Pontuação](media/functions-twitter-email/trigger_score.png)

Agora, sua função é disparada quando uma pontuação de sensibilidade é enviada do aplicativo lógico de saudação. Uma categoria com codificação de cores é retornada toohello lógica aplicativo por função hello. Em seguida, você adiciona uma notificação por email é enviada quando um valor de sensibilidade de **vermelho** é retornado da função hello. 

## <a name="add-email-notifications"></a>Adicionar notificações por email

Olá última parte do fluxo de trabalho de saudação é tootrigger um email quando o sentimento Olá foi classificado como _vermelho_. Este tópico usa um conector do Outlook.com. Você pode executar semelhante etapas toouse um conector Gmail ou Outlook do Office 365.   

1. No hello lógica do Designer de aplicativos, clique em **nova etapa** > **adicionar uma condição**. 

2. Clique em **Escolha um valor** e clique em **Corpo**. Selecione **é igual a**, clique em **Escolha um valor**, digite `RED`e clique em **Salvar**. 

    ![Adicione um aplicativo de lógica de toohello de condição.](media/functions-twitter-email/condition.png)

3. Em **se Sim, não faça NADA**, clique em **adicionar uma ação**, procurar `outlook.com`, clique em **enviar um email**e entre tooyour conta do Outlook.com.
    
    ![Escolha uma ação para a condição de saudação.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Se você não tiver uma conta do Outlook.com, poderá escolher outro conector, como Gmail ou Outlook do Office 365

4. Em Olá **enviar um email** ação, usar configurações de email hello como especificado na tabela de saudação. 

    ![Configure o email de hello para enviar Olá uma ação de email.](media/functions-twitter-email/sendemail.png)

    | Configuração      |  Valor sugerido   | Descrição  |
    | ----------------- | ------------ | ------------- |
    | **Para** | Digitar endereço de email | endereço de email de saudação que recebe a notificação de saudação. |
    | **Assunto** | Sentimento de tweet negativo detectado  | Olá assunto da notificação por email hello.  |
    | **Corpo** | Texto do Tweet, local | Clique em Olá **Tweet texto** e **local** parâmetros. |

5.  Clique em **Salvar**.

Agora que o fluxo de trabalho de saudação for concluído, você pode habilitar Olá lógica aplicativo e consulte função hello no trabalho.

## <a name="test-hello-workflow"></a>Fluxo de trabalho de saudação de teste

1. No hello lógica de aplicativo Designer, clique em **executar** toostart Olá aplicativo.

2. Na coluna esquerda da saudação, clique em **visão geral** toosee status de saudação do aplicativo de lógica de saudação. 
 
    ![Status de execução do aplicativo lógico](media/functions-twitter-email/over1.png)

3. (Opcional) Clique em uma saudação executa toosee detalhes da execução de saudação.

4. Vá função tooyour, exibir logs hello e verificar que os valores de sentimento foram recebidos e processados.
 
    ![Exibir os logs da função](media/functions-twitter-email/sent.png)

5. Quando um sentimento potencialmente negativo é detectado, você recebe um email. Se você ainda não recebeu um email, você pode alterar a saudação função código tooreturn vermelho sempre:

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Depois que você verificou as notificações por email, altere código de retorno toohello original:

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Depois de concluir este tutorial, você deve desabilitar o aplicativo lógico de saudação. Ao desabilitar o aplicativo hello, você evitar que está sendo carregada para execuções e usar transações Olá em sua conta de serviços Cognitivos.

Agora você viu como é fácil toointegrate funções em um fluxo de trabalho de aplicativos lógicos.

## <a name="disable-hello-logic-app"></a>Desabilitar o aplicativo de lógica de saudação

aplicativo de lógica de saudação toodisable, clique em **visão geral** e, em seguida, clique em **desabilitar** na parte superior de saudação da tela hello. Isso interrompe o aplicativo lógico de saudação em execução e incorrer em encargos sem excluir o aplicativo hello. 

![Logs da função](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar uma conta dos Serviços Cognitivos.
> * Crie uma função que categorize o sentimento do tweet.
> * Crie um aplicativo lógico que se conecta tooTwitter.
> * Adicione aplicativo de lógica de toohello de detecção sensibilidade. 
> * Conecte-se a função de toohello de aplicativo hello lógica.
> * Envie um email com base na resposta de saudação do função hello.

Avançar toolearn tutorial do próximo toohello como toocreate uma API sem servidor de sua função.

> [!div class="nextstepaction"] 
> [Criar uma API sem servidor usando o Azure Functions](functions-create-serverless-api.md)

toolearn mais sobre aplicativos lógicos, consulte [aplicativos do Azure lógica](../logic-apps/logic-apps-what-are-logic-apps.md).

