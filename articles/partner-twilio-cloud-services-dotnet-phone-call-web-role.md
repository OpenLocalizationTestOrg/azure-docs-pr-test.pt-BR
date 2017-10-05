---
title: "Como fazer uma chamada telefônica do Twilio (.NET) | Microsoft Docs"
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Amostras de código gravadas no .NET."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="b3c74-104">Como fazer uma chamada telefônica usando a Twilio em uma função web no Azure</span><span class="sxs-lookup"><span data-stu-id="b3c74-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="b3c74-105">Este guia demonstra como usar a Twilio para fazer uma chamada de uma página da web hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3c74-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="b3c74-106">O aplicativo resultante solicita ao usuário para fazer uma chamada com o número e mensagem determinados, conforme mostrado na seguinte captura de tela.</span><span class="sxs-lookup"><span data-stu-id="b3c74-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Formulário de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="b3c74-108"><a name="twilio-prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3c74-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="b3c74-109">Você precisará fazer o seguinte para usar o código deste tópico:</span><span class="sxs-lookup"><span data-stu-id="b3c74-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="b3c74-110">Adquirir uma conta e um token de autenticação da Twilio do seu [Console do Twilio][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="b3c74-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="b3c74-111">Para começar com a Twilio, inscreva-se em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="b3c74-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="b3c74-112">Você pode avaliar os preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="b3c74-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="b3c74-113">Para obter informações sobre a API fornecida pela Twilio, veja [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b3c74-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="b3c74-114">Adicione a *biblioteca do .NET da Twilio* à sua função web.</span><span class="sxs-lookup"><span data-stu-id="b3c74-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="b3c74-115">Consulte **Para adicionar as bibliotecas da Twilio ao seu projeto de função web**, posteriormente neste tópico.</span><span class="sxs-lookup"><span data-stu-id="b3c74-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="b3c74-116">Você deve estar familiarizado com a criação de uma [Função web básica no Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="b3c74-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="b3c74-117"><a name="howtocreateform"></a>Como criar um formulário Web para fazer uma chamada</span><span class="sxs-lookup"><span data-stu-id="b3c74-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="b3c74-118"><a id="use_nuget"></a>Para adicionar as bibliotecas Twilio ao seu projeto de função Web:</span><span class="sxs-lookup"><span data-stu-id="b3c74-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="b3c74-119">Abra sua solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3c74-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="b3c74-120">Clique com o botão direito do mouse em **Referências**.</span><span class="sxs-lookup"><span data-stu-id="b3c74-120">Right-click **References**.</span></span>
3. <span data-ttu-id="b3c74-121">Clique em **Gerenciar Pacotes NuGet**</span><span class="sxs-lookup"><span data-stu-id="b3c74-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="b3c74-122">Clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="b3c74-122">Click **Online**.</span></span>
5. <span data-ttu-id="b3c74-123">Na caixa Pesquisar Online, digite *tiwlio*.</span><span class="sxs-lookup"><span data-stu-id="b3c74-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="b3c74-124">Clique em **Instalar** no pacote Twilio.</span><span class="sxs-lookup"><span data-stu-id="b3c74-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="b3c74-125">O código a seguir mostra como criar um formulário da web para recuperar dados do usuário para fazer uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b3c74-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="b3c74-126">Neste exemplo, uma Função web do ASP.NET chamada **TwilioCloud** é criada.</span><span class="sxs-lookup"><span data-stu-id="b3c74-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="b3c74-127"><a id="howtocreatecode"></a>Como criar o código para fazer a chamada</span><span class="sxs-lookup"><span data-stu-id="b3c74-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="b3c74-128">O código a seguir, que é chamado quando o usuário preenche o formulário, cria a mensagem de chamada e gera a chamada.</span><span class="sxs-lookup"><span data-stu-id="b3c74-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="b3c74-129">Neste exemplo, o código é executado no manipulador de eventos onclick do botão no formulário.</span><span class="sxs-lookup"><span data-stu-id="b3c74-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="b3c74-130">(Use sua conta e o token de autenticação da Twilio em vez dos valores de espaço reservado atribuídos a `accountSID` e `authToken` no código a seguir.)</span><span class="sxs-lookup"><span data-stu-id="b3c74-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="b3c74-131">A chamada é feita, e o ponto de extremidade da Twilio, a versão da API e o status da chamada são exibidos.</span><span class="sxs-lookup"><span data-stu-id="b3c74-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="b3c74-132">A captura de tela a seguir mostra a saída de uma execução de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b3c74-132">The following screenshot shows output from a sample run.</span></span>

![Resposta de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="b3c74-134">Mais informações sobre TwiML podem ser localizadas em [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="b3c74-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="b3c74-135">Mais informações sobre &lt;Say&gt; e outros verbos da Twilio podem ser localizadas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="b3c74-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="b3c74-136"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3c74-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="b3c74-137">Esse código foi fornecido para mostrar a funcionalidade básica usando a Twilio em uma função web do ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="b3c74-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="b3c74-138">Antes de implantar o Azure na produção, convém adicionar mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="b3c74-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="b3c74-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b3c74-139">For example:</span></span>

* <span data-ttu-id="b3c74-140">Em vez de usar um formulário da web, você pode usar o armazenamento de Blob do Azure ou uma instância do Banco de Dados SQL do Azure para armazenar números de telefone e texto de chamada.</span><span class="sxs-lookup"><span data-stu-id="b3c74-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="b3c74-141">Para obter mais informações sobre como usar blobs no Azure, consulte [Como usar o serviço de Armazenamento de Blobs do Azure no .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b3c74-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="b3c74-142">Para obter informações sobre como usar o Banco de Dados SQL, consulte [Como usar o Banco de Dados SQL do Azure em aplicativos .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b3c74-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="b3c74-143">Você pode usar `RoleEnvironment.getConfigurationSettings` para recuperar a ID da conta e o token de autenticação da Twilio nas definições da configuração da implantação, em vez de embutir valores no código de seu formulário.</span><span class="sxs-lookup"><span data-stu-id="b3c74-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="b3c74-144">Para obter informações sobre a classe `RoleEnvironment`, consulte [Microsoft.WindowsAzure.ServiceRuntime Namespace (Namespace Microsoft.WindowsAzure.ServiceRuntime)][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="b3c74-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="b3c74-145">Leia as Diretrizes de segurança da Twilio em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="b3c74-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="b3c74-146">Saiba mais sobre a Twilio em [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="b3c74-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="b3c74-147"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="b3c74-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="b3c74-148">Como usar o Twilio para funcionalidades de voz e SMS do Azure</span><span class="sxs-lookup"><span data-stu-id="b3c74-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
