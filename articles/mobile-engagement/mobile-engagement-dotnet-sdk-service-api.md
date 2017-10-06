---
title: "aaaUsing tooaccess .NET SDK APIs de serviço do Azure Mobile Engagement"
description: "Descreve como toouse Olá .NET SDK do Mobile Engagement tooaccess APIs de serviço do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>Usando o SDK do .NET tooaccess APIs de serviço do Azure Mobile Engagement
O Azure Mobile Engagement expõe um conjunto de APIs para você toomanage dispositivos, alcance/enviar por Push campanhas etc. toointeract com essas APIs, nós também fornecemos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que você pode usar com ferramentas toogenerate SDKs de sua preferência idioma. É recomendável usar Olá [AutoRest](https://github.com/Azure/AutoRest) ferramenta toogenerate o SDK do nosso arquivo Swagger.

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Criamos um SDK .NET de maneira semelhante, que permite que você toointeract com essas APIs usando um wrapper em c# e você não tiver toodo Olá negociação do token de autenticação e atualização por conta própria.  

Este exemplo passa pelo conjunto de saudação de etapas toofollow toouse Olá .NET SDK:

1. Em primeiro lugar, você precisa toosetup autenticação de saudação para suas APIs usando hello Azure Active Directory conforme descrito [aqui](mobile-engagement-api-authentication.md#authentication). Final Olá dessas etapas, você deve ter uma opção válida **SubscriptionId**, **TenantId**, **ApplicationId** e **segredo**. 
2. Usaremos uma toodemonstrate de aplicativo de Console do Windows simple trabalhar com hello SDK .NET com cenário de saudação de criação de uma campanha de anúncio. Portanto, abra o Visual Studio e crie um **Aplicativo de Console**.   
3. Em seguida você precisa Olá toodownload .NET SDK que está disponível como **biblioteca de gerenciamento do Microsoft Azure contrato** na Galeria do Nuget Olá [aqui](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Se você estiver instalando Olá Nuget do Visual Studio, você precisa tooensure que você tenha seleção marcada Olá **incluir pré-lançamento** opção durante a pesquisa para o pacote de saudação:
   
    ![][1]
4. Em Olá `Program.cs` de arquivo, adicione Olá namespaces a seguir:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Em seguida, você precisa toodefine Olá seguintes constantes que usaremos para autenticação e interagir com hello Mobile Engagement aplicativo no qual você está criando campanha de anúncio hello:
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. Definir Olá `EngagementManagementClient` variável que vamos usar métodos de SDK do Mobile Engagement Olá toocall:
   
        static EngagementManagementClient engagementClient; 
7. Adicionar Olá após tooyour `Main` método:
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. Definir Olá seguinte método que cuida do Inicializando Olá `EngagementManagementClient` autenticando primeiro e, em seguida, associar próprio Olá Mobile Engagement aplicativo no qual você planeja campanha de anúncio Olá toocreate:
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > Observe que você precisa Olá toouse **nome de recurso do aplicativo** conforme definido no portal de gerenciamento do Azure Olá para o parâmetro de AppName hello. 
   > 
   > 
9. Por fim, definir o método de CreateCampaign de saudação que será responsável por usando Olá inicializado anteriormente EngagementClient toocreate simples **a qualquer momento** & **apenas de notificação** campanha com um título e a mensagem: 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. Olá execução aplicativo de console e você verá a seguinte Olá em criação bem-sucedida de campanha hello:
    
    **A Id da campanha “159” foi criada com êxito e está em estado de “rascunho”**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
