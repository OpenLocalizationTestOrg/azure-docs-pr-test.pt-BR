---
title: "Azure Mobile Engagement - integração do back-end"
description: Conectar o Azure Mobile Engagement com um back-end do SharePoint para criar campanhas do SharePoint
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="7c4b7-103">Integração da API do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7c4b7-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="7c4b7-104">Em um sistema automatizado de marketing, a criação e ativação das campanhas de marketing também ocorrerem automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="7c4b7-105">Para essa finalidade - o Azure Mobile Engagement permite criar essas campanhas de marketing automatizadas usando também as APIs.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="7c4b7-106">Normalmente os clientes usam a interface de front-end do Mobile Engagement para criar anúncios/pesquisas etc como parte de suas campanhas de marketing.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="7c4b7-107">No entanto conforme as campanhas de marketing ficam maduras, é necessário aproveitar os dados bloqueados nos sistemas de back-end (como qualquer sistema CRM ou sistema CMS como o SharePoint) para que possa ser criado um pipeline totalmente automatizado que cria campanhas em Mobile Engagement dinamicamente com base nos dados que fluem dos sistemas back-end.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="7c4b7-108">Este tutorial passa pelo cenário em que um usuário de negócios do SharePoint preenche uma lista do SharePoint com dados de marketing e um processo automatizado pega itens da lista e conecta-se com o sistema Mobile Engagement usando as APIs REST disponíveis para criar uma campanha de marketing dos dados do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7c4b7-109">Em geral, é possível usar este exemplo como ponto de partida para entender como chamar qualquer API REST do Mobile Engagement, pois ela detalha os dois principais aspectos de chamar as APIs - autenticação e passagem de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="7c4b7-110">Integração do SharePoint</span><span class="sxs-lookup"><span data-stu-id="7c4b7-110">SharePoint integration</span></span>
1. <span data-ttu-id="7c4b7-111">A lista do SharePoint de exemplo é semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="7c4b7-112">**Title**, **Category**, **NotificationTitle**, **Message** e **URL** são usados para criar o anúncio.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="7c4b7-113">Há uma coluna chamada **IsProcessed** que é usada pelo processo de automação de exemplo na forma de um programa de console.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="7c4b7-114">É possível executar esse console do programa como um Trabalho Web do Azure para que você pode programá-lo ou usar diretamente o fluxo de trabalho do SharePoint para programar a criação e ativação do anúncio quando um item é inserido na lista do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="7c4b7-115">Neste exemplo, usamos o programa de console que vai pelos itens da lista do SharePoint e cria um anúncio no Azure Mobile Engagement para cada um deles e, em seguida, marca o sinalizador **IsProcessed** como true na criação do anúncio com êxito.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="7c4b7-116">Estamos usando o código do exemplo *Autenticação remota no SharePoint Online usando o modelo de objeto do cliente* [aqui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) para autenticar com a lista do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="7c4b7-117">Depois de autenticado, executamos um loop pelos itens de lista para localizar os itens recém-criados (que têm **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="7c4b7-118">Integração do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7c4b7-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="7c4b7-119">Depois de encontrarmos um item que requer processamento - podemos extrair as informações necessárias para criar um anúncio do item de lista e chamada `CreateAzMECampaign` para criá-lo e subsequentemente `ActivateAzMECampaign` para ativá-lo.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="7c4b7-120">Essas são essencialmente chamadas da API REST chamaando para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="7c4b7-121">As APIs REST do Mobile Engagement exigem um **Cabeçalho de autenticação HTTP de esquema de autenticação básica** composto pelo `ApplicationId` e pelo `ApiKey` que você obtém do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="7c4b7-122">Certifique-se de estar usando a chave da seção **chaves de api** e *não* da seção **chaves do sdk**.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="7c4b7-123">Para criar a campanha do tipo do anúncio - consulte a [documentação](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="7c4b7-124">Você precisará se certificar de que está especificando a campanha `kind` como *anúncio* e [carga](https://msdn.microsoft.com/library/azure/mt683751.aspx) e passá-la como FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="7c4b7-125">Uma vez que o anúncio é criado, você verá algo semelhante ao seguinte no portal Mobile Engagement (observe que Estado = Rascunho e Ativado = N/A)</span><span class="sxs-lookup"><span data-stu-id="7c4b7-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="7c4b7-126">`CreateAzMECampaign` cria uma campanha de anúncio e retorna sua identificação para o chamador.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="7c4b7-127">`ActivateAzMECampaign` necessita dessa Id como o parâmetro para ativar a campanha.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="7c4b7-128">Uma vez que o anúncio é ativado, você verá algo semelhante ao seguinte no portal Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="7c4b7-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="7c4b7-129">Assim que a campanha é ativada, os dispositivos que atendem aos critérios da campanha começarão a ver notificações.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="7c4b7-130">Você também observará que o item de lista marcada com IsProcessed = false foi definido como True depois que a campanha de anúncio foi criada.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="7c4b7-131">Esse exemplo criou uma campanha de anúncio simples especificando principalmente as propriedades necessárias.</span><span class="sxs-lookup"><span data-stu-id="7c4b7-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="7c4b7-132">Você pode personalizá-la tanto quanto possível a partir do portal usando as informações [aqui](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="7c4b7-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



