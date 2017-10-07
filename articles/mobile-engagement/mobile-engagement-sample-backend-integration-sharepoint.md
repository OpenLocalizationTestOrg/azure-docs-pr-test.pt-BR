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
# <a name="azure-mobile-engagement---api-integration"></a>Integração da API do Azure Mobile Engagement
Em um sistema automatizado de marketing, criar e ativar Olá campanhas de marketing também ocorrem automaticamente. Para essa finalidade - o Azure Mobile Engagement permite criar essas campanhas de marketing automatizadas usando também as APIs. 

Os clientes usam Olá Mobile Engagement front-end interface toocreate anúncios/pesquisas etc como parte de suas campanhas de marketing. No entanto, como Olá se tornam consolidadas de campanhas de marketing, é necessário tooleverage Olá os dados bloqueados em sistemas de back-end de saudação (como qualquer sistema CRM ou sistema CMS como SharePoint) para que possa ser criado um pipeline totalmente automatizado que cria campanhas no celular Contrato dinamicamente com base em fluxo de sistemas de back-end de saudação de dados hello. 

![][5]

Este tutorial vai por meio do cenário em que um usuário de negócios do SharePoint preenche uma lista do SharePoint com dados de marketing e um processo automatizado seleciona itens da lista de saudação e conecta-se com hello Mobile Engagement sistema usando Olá disponíveis APIs de REST toocreate uma campanha de marketing de dados do SharePoint de saudação. 

> [!IMPORTANT]
> Em geral, você pode usar este exemplo como um ponto de partida para entender como toocall qualquer API de REST do Mobile Engagement como detalhes Olá dois aspectos-chave da chamada hello APIs - autenticando e passando parâmetros. 
> 
> 

## <a name="sharepoint-integration"></a>Integração do SharePoint
1. Aqui está o exemplo hello aparência de lista do SharePoint. **Título**, **categoria**, **NotificationTitle**, **mensagem** e **URL** são usadas para criar o anúncio de saudação. Há uma coluna chamada **IsProcessed** que é usada pelo processo de automação de exemplo hello na forma de saudação de um programa de console. Você pode executar esse programa de console como um trabalho de Web do Azure para que agendá-la ou diretamente você pode usar Olá SharePoint fluxo de trabalho tooprogram criando e comunicado de saudação de ativação quando um item é inserido na lista do SharePoint hello. Neste exemplo, usamos programa do console Olá que vai nos itens de saudação de saudação do SharePoint lista e criar o anúncio no Azure Mobile Engagement para cada um deles e, em seguida, por fim, marca Olá **IsProcessed** true toobe sinalizador criação bem-sucedida de anúncio.
   
    ![][1]
2. Estamos usando o código de saudação do exemplo hello *autenticação remota na saudação do SharePoint Online usando o modelo de objeto do cliente* [aqui](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate com a lista do SharePoint hello.
3. Uma vez autenticado, executamos um loop Olá toofind de itens de lista os itens criados recentemente (que tem **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Integração do Mobile Engagement
1. Quando encontramos um item que requer processamento - é extrair informações Olá necessárias toocreate um anúncio da saudação do item de lista e chame `CreateAzMECampaign` toocreate-lo e, subsequentemente, `ActivateAzMECampaign` tooactivate-lo. Esses são essencialmente chamadas da API REST chamar back-end do toohello Mobile Engagement. 
2. Olá APIs de REST do Mobile Engagement exigem um **cabeçalho de autorização HTTP do esquema de autenticação básica** que é composto de saudação `ApplicationId` e hello `ApiKey` que você obtém do hello portal do Azure. Certifique-se de que você está usando Olá chave do hello **chaves de api** seção e *não* de saudação **sdk chaves** seção. 
   
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
3. Para criar tipo de anúncio de saudação da campanha - consulte toohello [documentação](https://msdn.microsoft.com/library/azure/mt683750.aspx). Você precisa toomake-se de que você está especificando campanha Olá `kind` como *comunicado* e hello [carga](https://msdn.microsoft.com/library/azure/mt683751.aspx) e passá-lo como FormUrlEncodedContent. 
   
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
4. Uma vez que o anúncio Olá criado, você verá algo parecido com hello a seguir no portal do Mobile Engagement hello (Observe que Olá estado = rascunho e ativado = n/d)
   
    ![][3]
5. `CreateAzMECampaign`cria uma campanha de anúncio e retorna seu chamador toohello de Id. `ActivateAzMECampaign`requer essa Id como campanha de Olá Olá parâmetro tooactivate. 
   
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
6. Uma vez que o anúncio Olá ativado, você verá algo parecido com hello seguinte no portal do Mobile Engagement hello:
   
    ![][4]
7. Assim que a campanha Olá obtém ativada, quaisquer dispositivos que satisfazem o critério Olá campanha Olá iniciará vendo notificações. 
8. Você observará aquele item de lista Olá marcado com IsProcessed = false tiver sido definido tooTrue quando Olá comunicado campanha foi criada.  

Este exemplo criado uma campanha de anúncio simples especificando principalmente Olá necessário propriedades. Você pode personalizá-la tanto quanto pode do portal hello usando informações de saudação [aqui](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



