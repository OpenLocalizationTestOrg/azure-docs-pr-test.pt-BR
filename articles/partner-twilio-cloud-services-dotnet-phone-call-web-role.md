---
title: aaaHow toomake um telefonema do Twilio (.NET) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Amostras de código gravadas no .NET."
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
ms.openlocfilehash: 857d89961c563a51fef944f4a72828036af79b43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="280b5-104">Como toomake um telefone de chamada usando o Twilio em uma função web no Azure</span><span class="sxs-lookup"><span data-stu-id="280b5-104">How toomake a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="280b5-105">Este guia demonstra como toouse Twilio toomake uma chamada de uma página da web hospedados no Azure.</span><span class="sxs-lookup"><span data-stu-id="280b5-105">This guide demonstrates how toouse Twilio toomake a call from a web page hosted in Azure.</span></span> <span data-ttu-id="280b5-106">Olá resultante aplicativo solicita que Olá usuário toomake uma chamada com hello recebe o número e a mensagem, conforme mostrado no hello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="280b5-106">hello resulting application prompts hello user toomake a call with hello given number and message, as shown in hello following screenshot.</span></span>

![Formulário de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form]

## <span data-ttu-id="280b5-108"><a name="twilio-prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="280b5-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="280b5-109">Você precisará a seguir Olá toodo toouse código Olá neste tópico:</span><span class="sxs-lookup"><span data-stu-id="280b5-109">You will need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="280b5-110">Adquirir uma conta do Twilio e autenticação de token da saudação [Twilio Console][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="280b5-110">Acquire a Twilio account and authentication token from hello [Twilio Console][twilio_console].</span></span> <span data-ttu-id="280b5-111">tooget iniciado com Twilio, entrada em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="280b5-111">tooget started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="280b5-112">Você pode avaliar os preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="280b5-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="280b5-113">Para obter informações sobre Olá API fornecida pelo Twilio, consulte [http://www.twilio.com/voice/api][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="280b5-113">For information about hello API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="280b5-114">Adicionar Olá *biblioteca .NET do Twilio* tooyour função de web.</span><span class="sxs-lookup"><span data-stu-id="280b5-114">Add hello *Twilio .NET libary* tooyour web role.</span></span> <span data-ttu-id="280b5-115">Consulte **projeto de função tooadd Olá Twilio bibliotecas tooyour web**, mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="280b5-115">See **tooadd hello Twilio libraries tooyour web role project**, later in this topic.</span></span>

<span data-ttu-id="280b5-116">Você deve estar familiarizado com a criação de uma [Função web básica no Azure][azure_webroles_get_started].</span><span class="sxs-lookup"><span data-stu-id="280b5-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="280b5-117"><a name="howtocreateform"></a>Como criar um formulário Web para fazer uma chamada</span><span class="sxs-lookup"><span data-stu-id="280b5-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="280b5-118"><a id="use_nuget"></a>tooadd Olá Twilio bibliotecas tooyour projeto de função web:</span><span class="sxs-lookup"><span data-stu-id="280b5-118"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour web role project:</span></span>

1. <span data-ttu-id="280b5-119">Abra sua solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="280b5-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="280b5-120">Clique com o botão direito do mouse em **Referências**.</span><span class="sxs-lookup"><span data-stu-id="280b5-120">Right-click **References**.</span></span>
3. <span data-ttu-id="280b5-121">Clique em **Gerenciar Pacotes NuGet**</span><span class="sxs-lookup"><span data-stu-id="280b5-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="280b5-122">Clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="280b5-122">Click **Online**.</span></span>
5. <span data-ttu-id="280b5-123">Na caixa online de pesquisa de hello, digite *twilio*.</span><span class="sxs-lookup"><span data-stu-id="280b5-123">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="280b5-124">Clique em **instalar** no pacote do Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="280b5-124">Click **Install** on hello Twilio package.</span></span>

<span data-ttu-id="280b5-125">saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados de usuário para fazer uma chamada.</span><span class="sxs-lookup"><span data-stu-id="280b5-125">hello following code shows how toocreate a web form tooretrieve user data for making a call.</span></span> <span data-ttu-id="280b5-126">Neste exemplo, uma Função web do ASP.NET chamada **TwilioCloud** é criada.</span><span class="sxs-lookup"><span data-stu-id="280b5-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

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

## <span data-ttu-id="280b5-127"><a id="howtocreatecode"></a>Como: criar hello código toomake Olá chamada</span><span class="sxs-lookup"><span data-stu-id="280b5-127"><a id="howtocreatecode"></a>How to: Create hello code toomake hello call</span></span>
<span data-ttu-id="280b5-128">Olá código a seguir, que é chamado quando o usuário Olá concluir o formulário de saudação, cria a mensagem de saudação do chamada e gera chamada hello.</span><span class="sxs-lookup"><span data-stu-id="280b5-128">hello following code, which is called when hello user completes hello form, creates hello call message and generates hello call.</span></span> <span data-ttu-id="280b5-129">Neste exemplo, o código de saudação é executado no manipulador de eventos Olá onclick do botão de saudação no formulário de saudação.</span><span class="sxs-lookup"><span data-stu-id="280b5-129">In this example, hello code is run in hello onclick event handler of hello button on hello form.</span></span> <span data-ttu-id="280b5-130">(Use sua conta do Twilio e autenticação de token em vez de valores de espaço reservado de saudação atribuídos muito`accountSID` e `authToken` no código de saudação abaixo.)</span><span class="sxs-lookup"><span data-stu-id="280b5-130">(Use your Twilio account and authentication token instead of hello placeholder values assigned too`accountSID` and `authToken` in hello code below.)</span></span>

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
            // hello placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of hello Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve hello account, used later tooretrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve hello values entered by hello user.
                var too= PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using hello Twilio message and hello user-entered
                // text. You must replace spaces in hello user's text with '%20'
                // toomake hello text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display hello endpoint, API version, and hello URL for hello message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"hello URL is {url}");

                // Place hello call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="280b5-131">Olá chamada é feita e o ponto de extremidade do hello Twilio, a versão da API e status de chamada hello são exibidos.</span><span class="sxs-lookup"><span data-stu-id="280b5-131">hello call is made, and hello Twilio endpoint, API version, and hello call status are displayed.</span></span> <span data-ttu-id="280b5-132">Olá seguinte captura de tela mostra saída de um exemplo de execução.</span><span class="sxs-lookup"><span data-stu-id="280b5-132">hello following screenshot shows output from a sample run.</span></span>

![Resposta de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form_output]

<span data-ttu-id="280b5-134">Mais informações sobre TwiML podem ser localizadas em [http://www.twilio.com/docs/api/twiml][twiml].</span><span class="sxs-lookup"><span data-stu-id="280b5-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="280b5-135">Mais informações sobre &lt;Say&gt; e outros verbos da Twilio podem ser localizadas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="280b5-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="280b5-136"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="280b5-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="280b5-137">Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em uma função da web ASP.NET no Azure.</span><span class="sxs-lookup"><span data-stu-id="280b5-137">This code was provided tooshow you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="280b5-138">Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos.</span><span class="sxs-lookup"><span data-stu-id="280b5-138">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="280b5-139">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="280b5-139">For example:</span></span>

* <span data-ttu-id="280b5-140">Em vez de usar um formulário da web, você poderia usar o armazenamento de BLOBs do Azure ou um números de telefone de toostore de instância de banco de dados SQL e chamar o texto.</span><span class="sxs-lookup"><span data-stu-id="280b5-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance toostore phone numbers and call text.</span></span> <span data-ttu-id="280b5-141">Para obter informações sobre o uso de Blobs no Azure, consulte [como toouse Olá serviço de armazenamento de BLOBs do Azure no .NET][howto_blob_storage_dotnet].</span><span class="sxs-lookup"><span data-stu-id="280b5-141">For information about using Blobs in Azure, see [How toouse hello Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="280b5-142">Para obter informações sobre como usar o banco de dados SQL, consulte [como toouse SQL do Azure do banco de dados em aplicativos .NET][howto_sql_azure_dotnet].</span><span class="sxs-lookup"><span data-stu-id="280b5-142">For information about using SQL Database, see [How toouse Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="280b5-143">Você pode usar `RoleEnvironment.getConfigurationSettings` ID da conta do Twilio tooretrieve hello e autenticação de token da implantação definições de configuração, em vez de codificar valores de saudação do formulário.</span><span class="sxs-lookup"><span data-stu-id="280b5-143">You could use `RoleEnvironment.getConfigurationSettings` tooretrieve hello Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding hello values in your form.</span></span> <span data-ttu-id="280b5-144">Para obter informações sobre Olá `RoleEnvironment` de classe, consulte [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span><span class="sxs-lookup"><span data-stu-id="280b5-144">For information about hello `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="280b5-145">Ler Olá Twilio as diretrizes de segurança em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="280b5-145">Read hello Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="280b5-146">Saiba mais sobre a Twilio em [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="280b5-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="280b5-147"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="280b5-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="280b5-148">Como toouse Twilio para recursos de voz e SMS do Azure</span><span class="sxs-lookup"><span data-stu-id="280b5-148">How toouse Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

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
