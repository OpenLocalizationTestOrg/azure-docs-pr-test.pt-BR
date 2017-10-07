---
title: "aaaRetrain um serviço da web clássico | Microsoft Docs"
description: "Saiba como tooprogrammatically treinar novamente um modelo e a atualização Olá web serviço toouse Olá recentemente treinado no aprendizado de máquina do Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Treinar novamente um serviço Web Clássico
Olá previsão serviço Web é implantado é o padrão de saudação ponto de extremidade de pontuação. Pontos de extremidade padrão são mantidos em sincronia com hello originais de treinamento e pontuação experiências e, portanto, hello treinado para o ponto de extremidade do saudação padrão não pode ser substituído. serviço de web hello tooretrain, adicione um novo serviço da web de toohello ponto de extremidade. 

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter configurado um Teste de Treinamento e um Experimento de Previsão, como mostrado em [Readaptar os modelos do Machine Learning de forma programática](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> experiência de previsão Olá deve ser implantada como uma serviço web de aprendizado de máquina clássico. 
> 
> 

Para obter mais informações sobre como implantar os serviços Web, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Adicionar um novo ponto de extremidade
Olá previsão serviço Web que você implantou contém um ponto de extremidade que é mantido em sincronizado com o treinamento original hello e pontuação treinado experiências de pontuação padrão. tooupdate toowith seu serviço web um novo modelo treinado, você deve criar um novo ponto de extremidade de pontuação. 

toocreate um novo pontuação ponto de extremidade em Olá previsão serviço Web que pode ser atualizada com o modelo treinado hello:

> [!NOTE]
> Certifique-se de que você está adicionando toohello de ponto de extremidade Olá serviço Web de previsão, Olá serviço da Web de treinamento. Se você tiver implantado corretamente um serviço Web de previsão e um serviço da Web de treinamento, você verá dois serviços Web separados listados. Olá serviço Web de previsão deve terminar com "[previsão exp]"..
> 
> 

Há três maneiras em que você pode adicionar um novo serviço da web de tooa ponto de extremidade:

1. Programaticamente
2. Usar o portal de serviços Web do Microsoft Azure Olá
3. Use Olá portal clássico do Azure

### <a name="programmatically-add-an-endpoint"></a>Adicionar um ponto de extremidade programaticamente
Você pode adicionar pontos de extremidade de pontuação usando o código de exemplo hello fornecido neste [repositório github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Use tooadd um ponto de extremidade do portal de serviços Web do Microsoft Azure de saudação
1. No estúdio de aprendizado de máquina, na coluna de navegação à esquerda do hello, clique em serviços da Web.
2. Na parte inferior de saudação do painel de serviço web hello, clique em **visualização de pontos de extremidade de gerenciar**.
3. Clique em **Adicionar**.
4. Digite um nome e uma descrição para o novo ponto de extremidade de saudação. Selecione o nível de log hello e se os dados de exemplo estão habilitados. Para obter mais informações sobre registro em log, consulte [Habilitar o log de serviços Web de Machine Learning](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Use Olá tooadd portal clássico do Azure um ponto de extremidade
1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No menu à esquerda do hello, clique em **aprendizado de máquina**.
3. Em Nome, clique em seu espaço de Em Nome, clique em seu espaço de trabalho e, em seguida, clique em **Serviços Web**.
4. Em Nome, clique em **Modelo de Censo [exp. preditivo]**.
5. Final Olá Olá página, clique em **Adicionar ponto de extremidade**. Para saber mais sobre a adição de pontos de extremidade, veja [Criação de pontos de extremidade](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Saudação de atualização adicionado treinado do ponto de extremidade
processo novos treinamentos do toocomplete hello, você deve atualizar treinado Olá de saudação novo ponto de extremidade que você adicionou.

* Se você adicionou Olá novo ponto de extremidade usando o portal do Azure clássico de saudação, clique no nome hello novo ponto de extremidade no portal de saudação e Olá **UpdateResource** link tooget Olá URL seria necessário modelo tooupdate saudação do ponto de extremidade.
* Se você adicionou o ponto de extremidade de saudação usando o código de exemplo hello, isso inclui o local da URL de ajuda Olá identificado pelo Olá *HelpLocationURL* valor na saída de hello.

tooretrieve Olá caminho URL:

1. Copie e cole a URL de saudação no seu navegador.
2. Clique o link de recurso de atualização de saudação.
3. Copie Olá postar na URL de solicitação de PATCH hello. Por exemplo:
   
     URL DO PATCH: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

Agora você pode usar Olá Olá de tooupdate treinado pontuação de ponto de extremidade que você criou anteriormente.

Olá, código de exemplo a seguir mostra como Olá toouse *BaseLocation*, *RelativeLocation*, *SasBlobToken*e o ponto de extremidade do URL de PATCH tooupdate hello.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Olá *apiKey* e hello *endpointUrl* para chamada hello pode ser obtida no painel de controle do ponto de extremidade.

Olá valor Olá *nome* parâmetro em *recursos* deve saudação de correspondência de nome do recurso de saudação salvo treinado no experimento previsão hello. Olá tooget nome do recurso:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No menu à esquerda do hello, clique em **aprendizado de máquina**.
3. Em Nome, clique em seu espaço de Em Nome, clique em seu espaço de trabalho e, em seguida, clique em **Serviços Web**.
4. Em Nome, clique em **Modelo de Censo [exp. preditivo]**.
5. Clique em Olá novo ponto de extremidade que é adicionado.
6. No painel de controle de ponto de extremidade hello, clique em **recurso de atualização**.
7. Na página de documentação de API do recurso de atualização de saudação para serviço web de saudação, você pode encontrar hello **nome do recurso** em **recursos atualizáveis**.

Se seu token SAS expirar antes de você terminar de atualizar o ponto de extremidade hello, você deve executar um GET com a Id do trabalho de saudação tooobtain um novo token.

Quando o código de saudação foi executado com êxito, novo ponto de extremidade de saudação deve começar a usar o modelo Olá treinados novamente em aproximadamente 30 segundos.

## <a name="summary"></a>Resumo
Usando Olá APIs de treinamento, você pode atualizar o modelo treinado de saudação de um serviço Web previsão habilitar cenários, como:

* Readaptação de modelo periódico com novos dados.
* Distribuição de um modelo toocustomers com objetivo de saudação de permitir que eles treinar novamente o modelo de saudação usando seus próprios dados.

## <a name="next-steps"></a>Próximas etapas
[Solução de problemas Olá treinamento de um serviço da web clássico de aprendizado de máquina do Azure](machine-learning-troubleshooting-retraining-models.md)

