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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-web-role-on-azure"></a>Como toomake um telefone de chamada usando o Twilio em uma função web no Azure
Este guia demonstra como toouse Twilio toomake uma chamada de uma página da web hospedados no Azure. Olá resultante aplicativo solicita que Olá usuário toomake uma chamada com hello recebe o número e a mensagem, conforme mostrado no hello captura de tela a seguir.

![Formulário de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form]

## <a name="twilio-prereqs"></a>Pré-requisitos
Você precisará a seguir Olá toodo toouse código Olá neste tópico:

1. Adquirir uma conta do Twilio e autenticação de token da saudação [Twilio Console][twilio_console]. tooget iniciado com Twilio, entrada em [https://www.twilio.com/try-twilio][try_twilio]. Você pode avaliar os preços em [http://www.twilio.com/pricing][twilio_pricing]. Para obter informações sobre Olá API fornecida pelo Twilio, consulte [http://www.twilio.com/voice/api][twilio_api].
2. Adicionar Olá *biblioteca .NET do Twilio* tooyour função de web. Consulte **projeto de função tooadd Olá Twilio bibliotecas tooyour web**, mais adiante neste tópico.

Você deve estar familiarizado com a criação de uma [Função web básica no Azure][azure_webroles_get_started].

## <a name="howtocreateform"></a>Como criar um formulário Web para fazer uma chamada
<a id="use_nuget"></a>tooadd Olá Twilio bibliotecas tooyour projeto de função web:

1. Abra sua solução no Visual Studio.
2. Clique com o botão direito do mouse em **Referências**.
3. Clique em **Gerenciar Pacotes NuGet**
4. Clique em **Online**.
5. Na caixa online de pesquisa de hello, digite *twilio*.
6. Clique em **instalar** no pacote do Twilio hello.

saudação de código a seguir mostra como toocreate uma web formam tooretrieve dados de usuário para fazer uma chamada. Neste exemplo, uma Função web do ASP.NET chamada **TwilioCloud** é criada.

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

## <a id="howtocreatecode"></a>Como: criar hello código toomake Olá chamada
Olá código a seguir, que é chamado quando o usuário Olá concluir o formulário de saudação, cria a mensagem de saudação do chamada e gera chamada hello. Neste exemplo, o código de saudação é executado no manipulador de eventos Olá onclick do botão de saudação no formulário de saudação. (Use sua conta do Twilio e autenticação de token em vez de valores de espaço reservado de saudação atribuídos muito`accountSID` e `authToken` no código de saudação abaixo.)

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

Olá chamada é feita e o ponto de extremidade do hello Twilio, a versão da API e status de chamada hello são exibidos. Olá seguinte captura de tela mostra saída de um exemplo de execução.

![Resposta de chamada do Azure usando a Twilio e o ASP.NET][twilio_dotnet_basic_form_output]

Mais informações sobre TwiML podem ser localizadas em [http://www.twilio.com/docs/api/twiml][twiml]. Mais informações sobre &lt;Say&gt; e outros verbos da Twilio podem ser localizadas em [http://www.twilio.com/docs/api/twiml/say][twilio_say].

## <a id="nextsteps"></a>Próximas etapas
Este código foi fornecido tooshow você funcionalidade básica usando o Twilio em uma função da web ASP.NET no Azure. Antes de implantar tooAzure em produção, talvez você queira tooadd mais tratamento de erros ou outros recursos. Por exemplo:

* Em vez de usar um formulário da web, você poderia usar o armazenamento de BLOBs do Azure ou um números de telefone de toostore de instância de banco de dados SQL e chamar o texto. Para obter informações sobre o uso de Blobs no Azure, consulte [como toouse Olá serviço de armazenamento de BLOBs do Azure no .NET][howto_blob_storage_dotnet]. Para obter informações sobre como usar o banco de dados SQL, consulte [como toouse SQL do Azure do banco de dados em aplicativos .NET][howto_sql_azure_dotnet].
* Você pode usar `RoleEnvironment.getConfigurationSettings` ID da conta do Twilio tooretrieve hello e autenticação de token da implantação definições de configuração, em vez de codificar valores de saudação do formulário. Para obter informações sobre Olá `RoleEnvironment` de classe, consulte [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].
* Ler Olá Twilio as diretrizes de segurança em [https://www.twilio.com/docs/security][twilio_docs_security].
* Saiba mais sobre a Twilio em [https://www.twilio.com/docs][twilio_docs].

## <a name="seealso"></a>Consulte também
* [Como toouse Twilio para recursos de voz e SMS do Azure](twilio-dotnet-how-to-use-for-voice-sms.md)

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
