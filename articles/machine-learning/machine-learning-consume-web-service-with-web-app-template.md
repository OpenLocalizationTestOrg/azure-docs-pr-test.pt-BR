---
title: "aaaConsume um serviço web de aprendizado de máquina com um modelo de aplicativo da web | Microsoft Docs"
description: "Use um modelo de aplicativo da web no Azure Marketplace tooconsume um serviço web de previsão no aprendizado de máquina do Azure."
keywords: "serviço Web, operacionalização, API REST, aprendizado de máquina"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Consumir um serviço Web de Azure Machine Learning com um modelo de aplicativo Web

Uma vez você tiver desenvolvido seu modelo de previsão e implantá-lo como um serviço web do Azure usando o estúdio de aprendizado de máquina, ou usando ferramentas como o R ou Python, você pode acessar o modelo operacionalizados hello, usando uma API REST.

Há várias maneiras de tooconsume Olá API REST do serviço e acesso Olá web. Por exemplo, você pode escrever um aplicativo em c#, R, ou Python usando Olá exemplo de código gerado para você quando você implantou o serviço web de saudação (disponível no hello [Portal de serviços de Web de aprendizado de máquina](https://services.azureml.net/quickstart) ou no painel de serviço web Olá no Estúdio de aprendizado de máquina). Ou você pode usar o livro do Microsoft Excel de exemplo hello criado para você no hello simultaneamente.

Mas Olá tooaccess de maneira mais rápida e mais fácil é seu serviço web por meio de modelos do aplicativo da Web hello disponíveis no hello [Azure Marketplace de aplicativo Web](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Olá modelos de aplicativo do Azure máquina aprendizado da Web
modelos do aplicativo da web Hello disponíveis no hello Azure Marketplace podem criar um aplicativo da web personalizado que lide com os dados de entrada e resultados esperados do serviço web. Você só precisa toodo é dar Olá web access tooyour da web do serviço de aplicativo e de dados e modelo Olá Olá rest.

Dois modelos estão disponíveis:

* [Modelo do Aplicativo Web do Serviço de Solicitação-Resposta do Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Modelo do aplicativo Web do Serviço de Execução em Lote do Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Cada modelo cria um aplicativo ASP.NET de exemplo, usando Olá URI da API e a chave para o serviço web e o implanta como tooAzure um site da web. modelo de serviço de solicitação-resposta (RR) Olá cria um aplicativo web que permite que você toosend uma única linha de dados toohello web serviço tooget um único resultado. modelo de serviço de execução de lote (BES) Olá cria um aplicativo web que permite que você toosend muitas linhas de dados tooget vários resultados.

Codificação não é necessário toouse esses modelos. Basta fornecer Olá chave de API e o URI e modelo Olá cria o aplicativo hello para você.

chave de API de saudação tooget e URI de solicitação para um serviço web:

1. Em Olá [Portal de serviços da Web](https://services.azureml.net/quickstart), para um novo serviço da web, clique em **serviços Web** na parte superior da saudação. Ou para gerenciar um serviço Web Clássico, clique em **Serviços Web Clássicos**.
2. Clique em Olá web serviço você deseja tooaccess.
3. Para um serviço web clássico, clique em ponto de extremidade de saudação deseja tooaccess.
4. Clique em **consumir** na parte superior da saudação.
5. Saudação de cópia **primário** ou **chave secundária** e salvá-lo.
6. Se você estiver criando um modelo de serviço de solicitação-resposta (RR), copie Olá **solicitação-resposta** URI e salvá-lo. Se você estiver criando um modelo de serviço de execução de lote (BES), copie Olá **solicitações em lote** URI e salvá-lo.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Como toouse Olá modelo de serviço de solicitação-resposta (RR)
Siga estas etapas toouse Olá RRS web modelo de aplicativo, conforme mostrado no diagrama a seguir de saudação.

![Modelo do processo toouse RRS da web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Vá toohello [portal do Azure](https://portal.azure.com), **logon**, clique em **novo**, procure e selecione **aplicativo Web de serviço de solicitação-resposta do Azure ML**, em seguida, clique em **Criar**. 
   
   * Dê um nome exclusivo ao seu aplicativo Web. URL de saudação do aplicativo web de saudação será esse nome seguido por `.azurewebsites.net.` por exemplo,`http://carprediction.azurewebsites.net.`
   * Selecione hello assinatura do Azure e serviços sob a qual o serviço web está em execução.
   * Clique em **Criar**.
     
     ![Criar um aplicativo Web][image5]

4. Quando o Azure concluiu a implantação de aplicativo da web de Olá, clique em Olá **URL** na Olá a página de configurações de aplicativo web no Azure, ou insira Olá URL em um navegador da web. Por exemplo, `http://carprediction.azurewebsites.net.`
5. Olá quando executa primeiro do aplicativo web solicitará que você para hello **API Post URL** e **chave API**.
   Insira valores hello salvos anteriormente (**URI da solicitação** e **chave API**, respectivamente).
     
     Clique em **Enviar**.
     
     ![Insira o URI de Postagem e a Chave de API][image6]

6. Olá web app exibe seu **configuração de aplicativo da Web** página de configurações de serviço da web atual hello. Aqui você pode fazer alterações toohello configurações usadas pelo aplicativo da web de saudação.
   
   > [!NOTE]
   > Alterar as configurações de saudação aqui altera apenas-los para este aplicativo web. Ele não altera as configurações padrão de saudação do serviço web. Por exemplo, se você alterar Olá **descrição** aqui ele não altera a descrição de saudação mostrada no painel de serviço web Olá no estúdio de aprendizado de máquina.
   > 
   > 
   
    Quando terminar, clique em **salvar alterações**e, em seguida, clique em **vá tooHome página**.

7. Página inicial que você pode inserir valores de toosend tooyour web Services da saudação. Clique em **enviar** quando tiver terminado e Olá resultado será retornado.

Se você quiser tooreturn toohello **configuração** página, ir toohello `setting.aspx` página do aplicativo web de saudação. Por exemplo: `http://carprediction.azurewebsites.net/setting.aspx.` será chave de saudação API tooenter solicitadas novamente - você precisa que tooaccess Olá página e atualizar as configurações de saudação.

Você pode parar, reiniciar ou excluir o aplicativo web de Olá Olá portal do Azure como qualquer outro aplicativo web. Enquanto ele está em execução, você pode procurar o endereço inicial toohello e insira novos valores.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Como toouse Olá modelo de serviço de execução de lote (BES)
Você pode usar o hello BES do modelo de aplicativo da web em Olá mesma maneira como modelo RRS Olá, exceto esse aplicativo web de saudação que é criado permitirá toosubmit várias linhas de dados e receber vários resultados.

valores de entrada Hello para um serviço de web de execução de lote podem vir de armazenamento do Azure ou um arquivo local. Olá resultados são armazenados em um contêiner de armazenamento do Azure.
Assim, será necessário um toohold de contêiner de armazenamento do Azure Olá resultados retornados pelo aplicativo de web hello, e você precisará tooget seus dados de entrada pronto.

![Processar toouse BES modelo da web][image2]

1. Siga Olá mesmo saudação do procedimento toocreate BES do aplicativo da web para o modelo RRS hello, exceto go muito[modelo de aplicativo do Azure ML lote execução do serviço Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Olá modelo BES no Azure Marketplace e clique em **criar aplicativo de Web** .

2. toospecify onde você deseja que os resultados de saudação armazenados, insira informações de contêiner de destino Olá na home page do aplicativo de web de saudação. Especifique também onde Olá web aplicativo pode obter valores de entrada de hello, em um arquivo local ou um contêiner de armazenamento do Azure.
   Clique em **Enviar**.
   
    ![Informações de armazenamento][image7]

Olá web app exibirá uma página de status do trabalho.
Quando tiver concluído o trabalho de saudação você terá local Olá dos resultados de saudação no armazenamento de BLOBs do Azure. Você também tem a opção de saudação de download de arquivo local da saudação resultados tooa.

## <a name="for-more-information"></a>Para obter mais informações
toolearn mais sobre...

* como criar uma experiência de aprendizado de máquina com o Machine Learning Studio, veja [Criar seu primeiro teste no Azure Machine Learning Studio](machine-learning-create-experiment.md)
* como toodeploy o aprendizado de máquina de teste como um serviço web, consulte [implantar um serviço web de aprendizado de máquina do Azure](machine-learning-publish-a-machine-learning-web-service.md)
* outras maneiras tooaccess seu serviço web, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
