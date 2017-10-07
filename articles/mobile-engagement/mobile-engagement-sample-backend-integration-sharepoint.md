---
title: "aaaAzure Mobile Engagement - integração do back-end"
description: Conecte-se do Azure Mobile Engagement com um campanhas de toocreate de back-end do SharePoint do SharePoint
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
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="80e27-103">Integração da API do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="80e27-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="80e27-104">Em um sistema automatizado de marketing, criar e ativar Olá campanhas de marketing também ocorrem automaticamente.</span><span class="sxs-lookup"><span data-stu-id="80e27-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="80e27-105">Para essa finalidade - o Azure Mobile Engagement permite criar essas campanhas de marketing automatizadas usando também as APIs.</span><span class="sxs-lookup"><span data-stu-id="80e27-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="80e27-106">Os clientes usam Olá Mobile Engagement front-end interface toocreate anúncios/pesquisas etc como parte de suas campanhas de marketing.</span><span class="sxs-lookup"><span data-stu-id="80e27-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="80e27-107">No entanto, como Olá se tornam consolidadas de campanhas de marketing, é necessário tooleverage Olá os dados bloqueados em sistemas de back-end de saudação (como qualquer sistema CRM ou sistema CMS como SharePoint) para que possa ser criado um pipeline totalmente automatizado que cria campanhas no celular Contrato dinamicamente com base em fluxo de sistemas de back-end de saudação de dados hello.</span><span class="sxs-lookup"><span data-stu-id="80e27-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="80e27-108">Este tutorial vai por meio do cenário em que um usuário de negócios do SharePoint preenche uma lista do SharePoint com dados de marketing e um processo automatizado seleciona itens da lista de saudação e conecta-se com hello Mobile Engagement sistema usando Olá disponíveis APIs de REST toocreate uma campanha de marketing de dados do SharePoint de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e27-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="80e27-109">Em geral, você pode usar este exemplo como um ponto de partida para entender como toocall qualquer API de REST do Mobile Engagement como detalhes Olá dois aspectos-chave da chamada hello APIs - autenticando e passando parâmetros.</span><span class="sxs-lookup"><span data-stu-id="80e27-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="80e27-110">Integração do SharePoint</span><span class="sxs-lookup"><span data-stu-id="80e27-110">SharePoint integration</span></span>
1. <span data-ttu-id="80e27-111">Aqui está o exemplo hello aparência de lista do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="80e27-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="80e27-112">**Título**, **categoria**, **NotificationTitle**, **mensagem** e **URL** são usadas para criar o anúncio de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e27-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="80e27-113">Há uma coluna chamada **IsProcessed** que é usada pelo processo de automação de exemplo hello na forma de saudação de um programa de console.</span><span class="sxs-lookup"><span data-stu-id="80e27-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="80e27-114">Você pode executar esse programa de console como um trabalho de Web do Azure para que agendá-la ou diretamente você pode usar Olá SharePoint fluxo de trabalho tooprogram criando e comunicado de saudação de ativação quando um item é inserido na lista do SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="80e27-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="80e27-115">Neste exemplo, usamos programa do console Olá que vai nos itens de saudação de saudação do SharePoint lista e criar o anúncio no Azure Mobile Engagement para cada um deles e, em seguida, por fim, marca Olá **IsProcessed** true toobe sinalizador criação bem-sucedida de anúncio.</span><span class="sxs-lookup"><span data-stu-id="80e27-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="80e27-116">Estamos usando o código de saudação do exemplo hello *autenticação remota na saudação do SharePoint Online usando o modelo de objeto do cliente* [aqui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate com a lista do SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="80e27-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="80e27-117">Uma vez autenticado, executamos um loop Olá toofind de itens de lista os itens criados recentemente (que tem **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="80e27-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="80e27-118">Integração do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="80e27-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="80e27-119">Quando encontramos um item que requer processamento - é extrair informações Olá necessárias toocreate um anúncio da saudação do item de lista e chame `CreateAzMECampaign` toocreate-lo e, subsequentemente, `ActivateAzMECampaign` tooactivate-lo.</span><span class="sxs-lookup"><span data-stu-id="80e27-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="80e27-120">Esses são essencialmente chamadas da API REST chamar back-end do toohello Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="80e27-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="80e27-121">Olá APIs de REST do Mobile Engagement exigem um **cabeçalho de autorização HTTP do esquema de autenticação básica** que é composto de saudação `ApplicationId` e hello `ApiKey` que você obtém do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="80e27-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="80e27-122">Certifique-se de que você está usando Olá chave do hello **chaves de api** seção e *não* de saudação **sdk chaves** seção.</span><span class="sxs-lookup"><span data-stu-id="80e27-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="80e27-123">Para criar tipo de anúncio de saudação da campanha - consulte toohello [documentação](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="80e27-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="80e27-124">Você precisa toomake-se de que você está especificando campanha Olá `kind` como *comunicado* e hello [carga](https://msdn.microsoft.com/library/azure/mt683751.aspx) e passá-lo como FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="80e27-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
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
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
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
4. <span data-ttu-id="80e27-125">Uma vez que o anúncio Olá criado, você verá algo parecido com hello a seguir no portal do Mobile Engagement hello (Observe que Olá estado = rascunho e ativado = n/d)</span><span class="sxs-lookup"><span data-stu-id="80e27-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="80e27-126">`CreateAzMECampaign`cria uma campanha de anúncio e retorna seu chamador toohello de Id.</span><span class="sxs-lookup"><span data-stu-id="80e27-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="80e27-127">`ActivateAzMECampaign`requer essa Id como campanha de Olá Olá parâmetro tooactivate.</span><span class="sxs-lookup"><span data-stu-id="80e27-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
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
   
                // Send hello POST request
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
6. <span data-ttu-id="80e27-128">Uma vez que o anúncio Olá ativado, você verá algo parecido com hello seguinte no portal do Mobile Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="80e27-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="80e27-129">Assim que a campanha Olá obtém ativada, quaisquer dispositivos que satisfazem o critério Olá campanha Olá iniciará vendo notificações.</span><span class="sxs-lookup"><span data-stu-id="80e27-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="80e27-130">Você observará aquele item de lista Olá marcado com IsProcessed = false tiver sido definido tooTrue quando Olá comunicado campanha foi criada.</span><span class="sxs-lookup"><span data-stu-id="80e27-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="80e27-131">Este exemplo criado uma campanha de anúncio simples especificando principalmente Olá necessário propriedades.</span><span class="sxs-lookup"><span data-stu-id="80e27-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="80e27-132">Você pode personalizá-la tanto quanto pode do portal hello usando informações de saudação [aqui](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="80e27-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



