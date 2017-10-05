---
title: "Usar o SDK do .NET para acessar as APIs de serviço do Azure Mobile Engagement"
description: "Descreve como usar o SDK do Mobile Engagement para .NET para acessar as APIs de serviço do Azure Mobile Engagement"
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
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="f2c9d-103">Usar o SDK do .NET para acessar as APIs de serviço do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="f2c9d-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="f2c9d-104">O Azure Mobile Engagement expõe um conjunto de APIs para gerenciar Dispositivos, Campanhas de Envio/Alcance, etc. Para interagir com essas APIs, também oferecemos um [arquivo Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que você pode usar com as ferramentas para gerar SDKs para seu idioma preferencial.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="f2c9d-105">Recomendamos usar a ferramenta [AutoRest](https://github.com/Azure/AutoRest) para gerar o SDK do nosso arquivo de Swagger.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="f2c9d-106">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="f2c9d-107">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="f2c9d-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="f2c9d-108">Criamos um SDK do .NET de forma semelhante que permite que você interaja com essas APIs usando um wrapper C#. Você não precisará fazer a negociação do token de autenticação e a atualização por conta própria.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="f2c9d-109">Este exemplo percorre o conjunto de etapas a seguir para usar o SDK do .NET:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="f2c9d-110">Em primeiro lugar, você precisa configurar a autenticação para suas APIs usando o Azure Active Directory, conforme descrito [aqui](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="f2c9d-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="f2c9d-111">No final destas etapas, você deve ter um **SubscriptionId**, **TenantId**, **ApplicationId** e **Secret** válidos.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="f2c9d-112">Usaremos um aplicativo simples do Console do Windows para demonstrar como trabalhar com o SDK do .NET com o cenário de criação de uma campanha de anúncios.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="f2c9d-113">Portanto, abra o Visual Studio e crie um **Aplicativo de Console**.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="f2c9d-114">Em seguida, será preciso baixar o SDK do .NET que está disponível como uma **Biblioteca de Gerenciamento do Microsoft Azure Engagement** na galeria do Nuget [aqui](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="f2c9d-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="f2c9d-115">Se você estiver instalando o Nuget do Visual Studio, precisará marcar a opção **Incluir pré-lançamento** ao procurar o pacote:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="f2c9d-116">No arquivo `Program.cs` , adicione os seguintes namespaces:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="f2c9d-117">Em seguida, você precisa definir as seguintes constantes que serão usadas para autenticação e interação com o aplicativo do Mobile Engagement no qual você está criando a campanha de anúncios:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="f2c9d-118">Defina a variável `EngagementManagementClient` que usaremos para chamar os métodos do SDK do Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="f2c9d-119">Adicione o seguinte ao seu método `Main` :</span><span class="sxs-lookup"><span data-stu-id="f2c9d-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="f2c9d-120">Defina o método a seguir que se encarrega de inicializar o `EngagementManagementClient` primeiro autenticando e, em seguida, se associando ao aplicativo do Mobile Engagement no qual você planeja criar a campanha de anúncios:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="f2c9d-121">Observe que você precisa usar o **nome de recurso do aplicativo** conforme definido no portal de gerenciamento do Azure para o parâmetro AppName.</span><span class="sxs-lookup"><span data-stu-id="f2c9d-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="f2c9d-122">Por fim, defina o método CreateCampaign que se encarregará de usar o EngagementClient inicializado anteriormente para criar uma campanha simples **AnyTime** & **Notification-only** com um título e a mensagem:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="f2c9d-123">Execute o aplicativo de console e você verá o seguinte sobre a criação bem-sucedida da campanha:</span><span class="sxs-lookup"><span data-stu-id="f2c9d-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="f2c9d-124">**A Id da campanha “159” foi criada com êxito e está em estado de “rascunho”**</span><span class="sxs-lookup"><span data-stu-id="f2c9d-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
