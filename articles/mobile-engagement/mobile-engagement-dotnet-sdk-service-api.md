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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="1ce7c-103">Usando o SDK do .NET tooaccess APIs de serviço do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1ce7c-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="1ce7c-104">O Azure Mobile Engagement expõe um conjunto de APIs para você toomanage dispositivos, alcance/enviar por Push campanhas etc. toointeract com essas APIs, nós também fornecemos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que você pode usar com ferramentas toogenerate SDKs de sua preferência idioma.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="1ce7c-105">É recomendável usar Olá [AutoRest](https://github.com/Azure/AutoRest) ferramenta toogenerate o SDK do nosso arquivo Swagger.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce7c-106">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="1ce7c-107">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="1ce7c-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="1ce7c-108">Criamos um SDK .NET de maneira semelhante, que permite que você toointeract com essas APIs usando um wrapper em c# e você não tiver toodo Olá negociação do token de autenticação e atualização por conta própria.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="1ce7c-109">Este exemplo passa pelo conjunto de saudação de etapas toofollow toouse Olá .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="1ce7c-110">Em primeiro lugar, você precisa toosetup autenticação de saudação para suas APIs usando hello Azure Active Directory conforme descrito [aqui](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="1ce7c-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="1ce7c-111">Final Olá dessas etapas, você deve ter uma opção válida **SubscriptionId**, **TenantId**, **ApplicationId** e **segredo**.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="1ce7c-112">Usaremos uma toodemonstrate de aplicativo de Console do Windows simple trabalhar com hello SDK .NET com cenário de saudação de criação de uma campanha de anúncio.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="1ce7c-113">Portanto, abra o Visual Studio e crie um **Aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="1ce7c-114">Em seguida você precisa Olá toodownload .NET SDK que está disponível como **biblioteca de gerenciamento do Microsoft Azure contrato** na Galeria do Nuget Olá [aqui](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="1ce7c-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="1ce7c-115">Se você estiver instalando Olá Nuget do Visual Studio, você precisa tooensure que você tenha seleção marcada Olá **incluir pré-lançamento** opção durante a pesquisa para o pacote de saudação:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="1ce7c-116">Em Olá `Program.cs` de arquivo, adicione Olá namespaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="1ce7c-117">Em seguida, você precisa toodefine Olá seguintes constantes que usaremos para autenticação e interagir com hello Mobile Engagement aplicativo no qual você está criando campanha de anúncio hello:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
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
6. <span data-ttu-id="1ce7c-118">Definir Olá `EngagementManagementClient` variável que vamos usar métodos de SDK do Mobile Engagement Olá toocall:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="1ce7c-119">Adicionar Olá após tooyour `Main` método:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-119">Add hello following tooyour `Main` method:</span></span>
   
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
8. <span data-ttu-id="1ce7c-120">Definir Olá seguinte método que cuida do Inicializando Olá `EngagementManagementClient` autenticando primeiro e, em seguida, associar próprio Olá Mobile Engagement aplicativo no qual você planeja campanha de anúncio Olá toocreate:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
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
   > <span data-ttu-id="1ce7c-121">Observe que você precisa Olá toouse **nome de recurso do aplicativo** conforme definido no portal de gerenciamento do Azure Olá para o parâmetro de AppName hello.</span><span class="sxs-lookup"><span data-stu-id="1ce7c-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="1ce7c-122">Por fim, definir o método de CreateCampaign de saudação que será responsável por usando Olá inicializado anteriormente EngagementClient toocreate simples **a qualquer momento** & **apenas de notificação** campanha com um título e a mensagem:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
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
10. <span data-ttu-id="1ce7c-123">Olá execução aplicativo de console e você verá a seguinte Olá em criação bem-sucedida de campanha hello:</span><span class="sxs-lookup"><span data-stu-id="1ce7c-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="1ce7c-124">**A Id da campanha “159” foi criada com êxito e está em estado de “rascunho”**</span><span class="sxs-lookup"><span data-stu-id="1ce7c-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
