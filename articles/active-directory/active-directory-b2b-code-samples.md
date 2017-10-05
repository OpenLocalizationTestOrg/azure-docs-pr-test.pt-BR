---
title: "Exemplos de código e do PowerShell para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Exemplos de código e do PowerShell para colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: cae69f57627b3058bf96c3d1eea7dadc81147153
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-code-and-powershell-samples"></a><span data-ttu-id="bfd30-103">Exemplos de código e do PowerShell para colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfd30-103">Azure Active Directory B2B collaboration code and PowerShell samples</span></span>

## <a name="powershell-example"></a><span data-ttu-id="bfd30-104">Exemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfd30-104">PowerShell example</span></span>
<span data-ttu-id="bfd30-105">É possível convidar usuários externos em massa para uma organização com base em endereços de email que você armazenou em um arquivo .CSV.</span><span class="sxs-lookup"><span data-stu-id="bfd30-105">You can bulk-invite external users to an organization from email addresses that you have stored in a .CSV file.</span></span>

1. <span data-ttu-id="bfd30-106">Prepare o arquivo .CSV, crie um novo arquivo .CSV e nomeie-o invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="bfd30-106">Prepare the .CSV file Create a new CSV file and name it invitations.csv.</span></span> <span data-ttu-id="bfd30-107">Neste exemplo, o arquivo é salvo em C:\data e contém as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="bfd30-107">In this example, the file is saved in C:\data, and contains the following information:</span></span>
  
  <span data-ttu-id="bfd30-108">Nome</span><span class="sxs-lookup"><span data-stu-id="bfd30-108">Name</span></span>                  |  <span data-ttu-id="bfd30-109">InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="bfd30-109">InvitedUserEmailAddress</span></span>
  --------------------- | --------------------------
  <span data-ttu-id="bfd30-110">Convidado Gmail B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-110">Gmail B2B Invitee</span></span>     | b2binvitee@gmail.com
  <span data-ttu-id="bfd30-111">Convidado Outlook B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-111">Outlook B2B invitee</span></span>   | b2binvitee@outlook.com


2. <span data-ttu-id="bfd30-112">Obtenha o PowerShell do Azure AD mais recente para usar os novos cmdlets. Instale o módulo atualizado do PowerShell do Azure AD, que você pode baixar da [página de versão do módulo Powershell](https://www.powershellgallery.com/packages/AzureADPreview)</span><span class="sxs-lookup"><span data-stu-id="bfd30-112">Get the latest Azure AD PowerShell To use the new cmdlets, you must install the updated Azure AD PowerShell module, which you can download from [the Powershell module's release page](https://www.powershellgallery.com/packages/AzureADPreview)</span></span>

3. <span data-ttu-id="bfd30-113">Entre em seu locatário</span><span class="sxs-lookup"><span data-stu-id="bfd30-113">Sign in to your tenancy</span></span>

    ```
    $cred = Get-Credential
    Connect-AzureAD -Credential $cred
    ```

4. <span data-ttu-id="bfd30-114">Executar o cmdlet do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bfd30-114">Run the PowerShell cmdlet</span></span>

  ```
  $invitations = import-csv C:\data\invitations.csv
  $messageInfo = New-Object Microsoft.Open.MSGraph.Model.InvitedUserMessageInfo
  $messageInfo.customizedMessageBody = “Hey there! Check this out. I created an invitation through PowerShell”
  foreach ($email in $invitations) {New-AzureADMSInvitation -InvitedUserEmailAddress $email.InvitedUserEmailAddress -InvitedUserDisplayName $email.Name -InviteRedirectUrl https://wingtiptoysonline-dev-ed.my.salesforce.com -InvitedUserMessageInfo $messageInfo -SendInvitationMessage $true}
  ```

<span data-ttu-id="bfd30-115">Esse cmdlet envia um convite para os endereços de email em invitations.csv.</span><span class="sxs-lookup"><span data-stu-id="bfd30-115">This cmdlet sends an invitation to the email addresses in invitations.csv.</span></span> <span data-ttu-id="bfd30-116">Os recursos adicionais desse cmdlet incluem:</span><span class="sxs-lookup"><span data-stu-id="bfd30-116">Additional features of this cmdlet include:</span></span>
- <span data-ttu-id="bfd30-117">Texto personalizado na mensagem de email</span><span class="sxs-lookup"><span data-stu-id="bfd30-117">Customized text in the email message</span></span>
- <span data-ttu-id="bfd30-118">Inclusão de um nome de exibição para o usuário convidado</span><span class="sxs-lookup"><span data-stu-id="bfd30-118">Including a display name for the invited user</span></span>
- <span data-ttu-id="bfd30-119">Envio de mensagens para CCs ou supressão completa de mensagens de email</span><span class="sxs-lookup"><span data-stu-id="bfd30-119">Sending messages to CCs or suppressing email messages altogether</span></span>

## <a name="code-sample"></a><span data-ttu-id="bfd30-120">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="bfd30-120">Code sample</span></span>
<span data-ttu-id="bfd30-121">Aqui, ilustramos como chamar a API de convite, no modo “somente do aplicativo”, para obter a URL de resgate do recurso ao qual você está convidando o usuário B2B.</span><span class="sxs-lookup"><span data-stu-id="bfd30-121">Here we illustrate how to call the invitation API, in "app-only" mode, to get the redemption URL for the resource to which you are inviting the B2B user.</span></span> <span data-ttu-id="bfd30-122">O objetivo é enviar um email de convite personalizado.</span><span class="sxs-lookup"><span data-stu-id="bfd30-122">The goal is to send a custom invitation email.</span></span> <span data-ttu-id="bfd30-123">O email pode ser composto com um cliente HTTP, para que seja possível personalizar a aparência e enviá-lo por meio da API do Graph.</span><span class="sxs-lookup"><span data-stu-id="bfd30-123">The email can be composed with an HTTP client, so you can customize how it looks and send it through Graph API.</span></span>

```
namespace SampleInviteApp
{
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    class Program
    {
        /// <summary>
        /// Microsoft graph resource.
        /// </summary>
        static readonly string GraphResource = "https://graph.microsoft.com";
 
        /// <summary>
        /// Microsoft graph invite endpoint.
        /// </summary>
        static readonly string InviteEndPoint = "https://graph.microsoft.com/v1.0/invitations";
 
        /// <summary>
        ///  Authentication endpoint to get token.
        /// </summary>
        static readonly string EstsLoginEndpoint = "https://login.microsoftonline.com";
 
        /// <summary>
        /// This is the tenantid of the tenant you want to invite users to.
        /// </summary>
        private static readonly string TenantID = "";
 
        /// <summary>
        /// This is the application id of the application that is registered in the above tenant.
        /// The required scopes are available in the below link.
        /// https://developer.microsoft.com/graph/docs/api-reference/v1.0/api/invitation_post
        /// </summary>
        private static readonly string TestAppClientId = "";
 
        /// <summary>
        /// Client secret of the application.
        /// </summary>
        private static readonly string TestAppClientSecret = @"
 
        /// <summary>
        /// This is the email address of the user you want to invite.
        /// </summary>
        private static readonly string InvitedUserEmailAddress = @"";
 
        /// <summary>
        /// This is the display name of the user you want to invite.
        /// </summary>
        private static readonly string InvitedUserDisplayName = @"";
 
        /// <summary>
        /// Main method.
        /// </summary>
        /// <param name="args">Optional arguments</param>
        static void Main(string[] args)
        {
            Invitation invitation = CreateInvitation();
            SendInvitation(invitation);
        }
 
        /// <summary>
        /// Create the invitation object.
        /// </summary>
        /// <returns>Returns the invitation object.</returns>
        private static Invitation CreateInvitation()
        {
            // Set the invitation object.
            Invitation invitation = new Invitation();
            invitation.InvitedUserDisplayName = InvitedUserDisplayName;
            invitation.InvitedUserEmailAddress = InvitedUserEmailAddress;
            invitation.InviteRedirectUrl = "https://www.microsoft.com";
            invitation.SendInvitationMessage = true;
            return invitation;
        }
 
        /// <summary>
        /// Send the guest user invite request.
        /// </summary>
        /// <param name="invitation">Invitation object.</param>
        private static void SendInvitation(Invitation invitation)
        {
            string accessToken = GetAccessToken();
 
            HttpClient httpClient = GetHttpClient(accessToken);
 
            // Make the invite call. 
            HttpContent content = new StringContent(JsonConvert.SerializeObject(invitation));
            content.Headers.Add("ContentType", "application/json");
            var postResponse = httpClient.PostAsync(InviteEndPoint, content).Result;
            string serverResponse = postResponse.Content.ReadAsStringAsync().Result;
            Console.WriteLine(serverResponse);
        }
 
        /// <summary>
        /// Get the HTTP client.
        /// </summary>
        /// <param name="accessToken">Access token</param>
        /// <returns>Returns the Http Client.</returns>
        private static HttpClient GetHttpClient(string accessToken)
        {
            // setup http client.
            HttpClient httpClient = new HttpClient();
            httpClient.Timeout = TimeSpan.FromSeconds(300);
            httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
            httpClient.DefaultRequestHeaders.Add("client-request-id", Guid.NewGuid().ToString());
            Console.WriteLine(
                "CorrelationID for the request: {0}",
                httpClient.DefaultRequestHeaders.GetValues("client-request-id").Single());
            return httpClient;
        }
 
        /// <summary>
        /// Get the access token for our application to talk to microsoft graph.
        /// </summary>
        /// <returns>Returns the access token for our application to talk to microsoft graph.</returns>
        private static string GetAccessToken()
        {
            string accessToken = null;
 
            // Get the access token for our application to talk to microsoft graph.
            try
            {
                AuthenticationContext testAuthContext =
                    new AuthenticationContext(string.Format("{0}/{1}", EstsLoginEndpoint, TenantID));
                AuthenticationResult testAuthResult = testAuthContext.AcquireTokenAsync(
                    GraphResource,
                    new ClientCredential(TestAppClientId, TestAppClientSecret)).Result;
                accessToken = testAuthResult.AccessToken;
            }
            catch (AdalException ex)
            {
                Console.WriteLine("An exception was thrown while fetching the token: {0}.", ex);
                throw;
            }
 
            return accessToken;
        }
 
        /// <summary>
        /// Invitation class.
        /// </summary>
        public class Invitation
        {
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserDisplayName { get; set; }
 
            /// <summary>
            /// Gets or sets display name.
            /// </summary>
            public string InvitedUserEmailAddress { get; set; }
 
            /// <summary>
            /// Gets or sets a value indicating whether Invitation Manager should send the email to InvitedUser.
            /// </summary>
            public bool SendInvitationMessage { get; set; }
 
            /// <summary>
            /// Gets or sets invitation redirect URL
            /// </summary>
            public string InviteRedirectUrl { get; set; }
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="bfd30-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfd30-124">Next steps</span></span>

<span data-ttu-id="bfd30-125">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="bfd30-125">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="bfd30-126">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="bfd30-126">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="bfd30-127">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-127">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="bfd30-128">Como adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="bfd30-128">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="bfd30-129">Delegação de convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-129">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="bfd30-130">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-130">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="bfd30-131">Configuração de aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-131">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="bfd30-132">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-132">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="bfd30-133">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-133">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="bfd30-134">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="bfd30-134">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="bfd30-135">Limitações atuais da colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="bfd30-135">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
