---
title: "Como usar Hubs de notificação com Python"
description: "Aprenda a usar Hubs de Notificação do Azure de um back-end Python."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 5640dd4a-a91e-4aa0-a833-93615bde49b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: python
ms.devlang: php
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9ceedb9940759427fc8cec74a1307e42472563a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-python"></a><span data-ttu-id="b8e91-103">Como usar Hubs de notificação do Python</span><span class="sxs-lookup"><span data-stu-id="b8e91-103">How to use Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="b8e91-104">Você pode acessar todos os recursos dos Hubs de Notificação por meio de um back-end do Java/PHP/Python/Ruby usando a interface REST do Hub de Notificação, conforme descrito no tópico do MSDN [APIs REST dos Hubs de Notificação](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8e91-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="b8e91-105">Isso é uma implementação de referência de exemplo para implementar o envia notificação em Python e não é oficialmente suportada notificações Hub Python SDK.</span><span class="sxs-lookup"><span data-stu-id="b8e91-105">This is a sample reference implementation for implementing the notification sends in Python and is not the officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="b8e91-106">Este exemplo é escrito usando Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="b8e91-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="b8e91-107">Neste tópico, mostramos como:</span><span class="sxs-lookup"><span data-stu-id="b8e91-107">In this topic we show how to:</span></span>

* <span data-ttu-id="b8e91-108">Crie um cliente REST para recursos de Hubs de notificação em Python.</span><span class="sxs-lookup"><span data-stu-id="b8e91-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="b8e91-109">Envie notificações usando a interface do Python para as API do REST do Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="b8e91-109">Send notifications using the Python interface to the Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="b8e91-110">Obtenha um despejo da solicitação/resposta HTTP REST para fins educativos/depuração.</span><span class="sxs-lookup"><span data-stu-id="b8e91-110">Get a dump of the HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="b8e91-111">Você pode seguir o [tutorial Introdução](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) para a plataforma móvel da sua escolha, implementando a parte de back-end em Python.</span><span class="sxs-lookup"><span data-stu-id="b8e91-111">You can follow the [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing the back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e91-112">O escopo do exemplo é limitado apenas para enviar notificações e não faz nenhum gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="b8e91-112">The scope of the sample is only limited to send notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="b8e91-113">Interface do cliente</span><span class="sxs-lookup"><span data-stu-id="b8e91-113">Client interface</span></span>
<span data-ttu-id="b8e91-114">A principal interface do cliente pode fornecer os mesmos métodos que estão disponíveis no [SDK dos Hubs de Notificação .NET](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8e91-114">The main client interface can provide the same methods that are available in the [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="b8e91-115">Isso permitirá a tradução diretamente de todos os tutoriais e exemplos atualmente disponíveis neste site e que conta com a colaboração da comunidade na Internet.</span><span class="sxs-lookup"><span data-stu-id="b8e91-115">This will allow you to directly translate all the tutorials and samples currently available on this site, and contributed by the community on the internet.</span></span>

<span data-ttu-id="b8e91-116">Você pode encontrar todo o código disponível na [amostra de wrapper REST Python].</span><span class="sxs-lookup"><span data-stu-id="b8e91-116">You can find all the code available in the [Python REST wrapper sample].</span></span>

<span data-ttu-id="b8e91-117">Por exemplo, para criar um cliente:</span><span class="sxs-lookup"><span data-stu-id="b8e91-117">For example, to create a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="b8e91-118">Para enviar uma notificação do sistema Windows:</span><span class="sxs-lookup"><span data-stu-id="b8e91-118">To send a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="b8e91-119">Implementação</span><span class="sxs-lookup"><span data-stu-id="b8e91-119">Implementation</span></span>
<span data-ttu-id="b8e91-120">Se ainda não fez isso, siga o nosso [tutorial Introdução] até a última seção, onde será necessário implementar o back-end.</span><span class="sxs-lookup"><span data-stu-id="b8e91-120">If you did not already, please follow our [Get started tutorial] up to the last section where you have to implement the back-end.</span></span>

<span data-ttu-id="b8e91-121">Todos os detalhes para implementar um wrapper completo do REST podem ser encontrados em [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8e91-121">All the details to implement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="b8e91-122">Nesta seção, descreveremos a implementação Python das principais etapas necessárias para acessar os pontos de extremidade REST de Hubs de notificação e envio de notificações</span><span class="sxs-lookup"><span data-stu-id="b8e91-122">In this section we will describe the Python implementation of the main steps required to access Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="b8e91-123">Analisar a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b8e91-123">Parse the connection string</span></span>
2. <span data-ttu-id="b8e91-124">Gerar o token de autorização</span><span class="sxs-lookup"><span data-stu-id="b8e91-124">Generate the authorization token</span></span>
3. <span data-ttu-id="b8e91-125">Enviar uma notificação usando a API REST do HTTP</span><span class="sxs-lookup"><span data-stu-id="b8e91-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-the-connection-string"></a><span data-ttu-id="b8e91-126">Analisar a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b8e91-126">Parse the connection string</span></span>
<span data-ttu-id="b8e91-127">Aqui está a principal classe que implementa o cliente cujos construtor analisa a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="b8e91-127">Here is the main class implementing the client, whose constructor parses the connection string:</span></span>

    class NotificationHub:
        API_VERSION = "?api-version=2013-10"
        DEBUG_SEND = "&test"

        def __init__(self, connection_string=None, hub_name=None, debug=0):
            self.HubName = hub_name
            self.Debug = debug

            # Parse connection string
            parts = connection_string.split(';')
            if len(parts) != 3:
                raise Exception("Invalid ConnectionString.")

            for part in parts:
                if part.startswith('Endpoint'):
                    self.Endpoint = 'https' + part[11:]
                if part.startswith('SharedAccessKeyName'):
                    self.SasKeyName = part[20:]
                if part.startswith('SharedAccessKey'):
                    self.SasKeyValue = part[16:]


### <a name="create-security-token"></a><span data-ttu-id="b8e91-128">Criar token de segurança</span><span class="sxs-lookup"><span data-stu-id="b8e91-128">Create security token</span></span>
<span data-ttu-id="b8e91-129">Os detalhes da criação de token de segurança estão disponíveis [aqui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="b8e91-129">The details of the security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="b8e91-130">Os métodos a seguir devem ser adicionados à classe **NotificationHub** para criar o token com base no URI da solicitação atual e as credenciais extraídas da cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="b8e91-130">The following methods have to be added to the **NotificationHub** class to create the token based on the URI of the current request and the credentials extracted from the connection string.</span></span>

    @staticmethod
    def get_expiry():
        # By default returns an expiration of 5 minutes (=300 seconds) from now
        return int(round(time.time() + 300))

    @staticmethod
    def encode_base64(data):
        return base64.b64encode(data)

    def sign_string(self, to_sign):
        key = self.SasKeyValue.encode('utf-8')
        to_sign = to_sign.encode('utf-8')
        signed_hmac_sha256 = hmac.HMAC(key, to_sign, hashlib.sha256)
        digest = signed_hmac_sha256.digest()
        encoded_digest = self.encode_base64(digest)
        return encoded_digest

    def generate_sas_token(self):
        target_uri = self.Endpoint + self.HubName
        my_uri = urllib.parse.quote(target_uri, '').lower()
        expiry = str(self.get_expiry())
        to_sign = my_uri + '\n' + expiry
        signature = urllib.parse.quote(self.sign_string(to_sign))
        auth_format = 'SharedAccessSignature sig={0}&se={1}&skn={2}&sr={3}'
        sas_token = auth_format.format(signature, expiry, self.SasKeyName, my_uri)
        return sas_token

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="b8e91-131">Enviar uma notificação usando a API REST do HTTP</span><span class="sxs-lookup"><span data-stu-id="b8e91-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="b8e91-132">Primeiro, vamos definir uma classe que representa uma notificação.</span><span class="sxs-lookup"><span data-stu-id="b8e91-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of the following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="b8e91-133">Essa classe é um contêiner para um corpo de notificação nativa ou um conjunto de propriedades no caso de uma notificação de modelo, um conjunto de cabeçalhos que contém o formato (plataforma nativa ou modelo) e propriedades específicas da plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).</span><span class="sxs-lookup"><span data-stu-id="b8e91-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="b8e91-134">Consulte a [documentação de APIs REST dos Hubs de Notificação](http://msdn.microsoft.com/library/dn495827.aspx) e os formatos específicos de notificação das plataformas para conhecer todas as opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b8e91-134">Please refer to the [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and the specific notification platforms' formats for all the options available.</span></span>

<span data-ttu-id="b8e91-135">Agora, com essa classe, podemos escrever a enviar os métodos de notificação dentro da classe **NotificationHub** .</span><span class="sxs-lookup"><span data-stu-id="b8e91-135">Now with this class, we can write the send notification methods inside of the **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about the PNS send notification outcome
            url += self.DEBUG_SEND
            print("--- REQUEST ---")
            print("URI: " + url)
            print("Headers: " + json.dumps(headers, sort_keys=True, indent=4, separators=(' ', ': ')))
            print("--- END REQUEST ---\n")

        connection.request('POST', url, payload, headers)
        response = connection.getresponse()

        if self.Debug > 0:
            # print out detailed response information for debugging purpose
            print("\n\n--- RESPONSE ---")
            print(str(response.status) + " " + response.reason)
            print(response.msg)
            print(response.read())
            print("--- END RESPONSE ---")

        elif response.status != 201:
            # Successful outcome of send message is HTTP 201 - Created
            raise Exception(
                "Error sending notification. Received HTTP code " + str(response.status) + " " + response.reason)

        connection.close()

    def send_notification(self, notification, tag_or_tag_expression=None):
        url = self.Endpoint + self.HubName + '/messages' + self.API_VERSION

        json_platforms = ['template', 'apple', 'gcm', 'adm', 'baidu']

        if any(x in notification.format for x in json_platforms):
            content_type = "application/json"
            payload_to_send = json.dumps(notification.payload)
        else:
            content_type = "application/xml"
            payload_to_send = notification.payload

        headers = {
            'Content-type': content_type,
            'Authorization': self.generate_sas_token(),
            'ServiceBusNotification-Format': notification.format
        }

        if isinstance(tag_or_tag_expression, set):
            tag_list = ' || '.join(tag_or_tag_expression)
        else:
            tag_list = tag_or_tag_expression

        # add the tags/tag expressions to the headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers to the headers collection that the user may have added
        if notification.headers is not None:
            headers.update(notification.headers)

        self.make_http_request(url, payload_to_send, headers)

    def send_apple_notification(self, payload, tags=""):
        nh = Notification("apple", payload)
        self.send_notification(nh, tags)

    def send_gcm_notification(self, payload, tags=""):
        nh = Notification("gcm", payload)
        self.send_notification(nh, tags)

    def send_adm_notification(self, payload, tags=""):
        nh = Notification("adm", payload)
        self.send_notification(nh, tags)

    def send_baidu_notification(self, payload, tags=""):
        nh = Notification("baidu", payload)
        self.send_notification(nh, tags)

    def send_mpns_notification(self, payload, tags=""):
        nh = Notification("windowsphone", payload)

        if "<wp:Toast>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'toast', 'X-NotificationClass': '2'}
        elif "<wp:Tile>" in payload:
            nh.headers = {'X-WindowsPhone-Target': 'tile', 'X-NotificationClass': '1'}

        self.send_notification(nh, tags)

    def send_windows_notification(self, payload, tags=""):
        nh = Notification("windows", payload)

        if "<toast>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/toast'}
        elif "<tile>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/tile'}
        elif "<badge>" in payload:
            nh.headers = {'X-WNS-Type': 'wns/badge'}

        self.send_notification(nh, tags)

    def send_template_notification(self, properties, tags=""):
        nh = Notification("template", properties)
        self.send_notification(nh, tags)

<span data-ttu-id="b8e91-136">Os métodos acima enviam uma solicitação de HTTP POST para o ponto de extremidade /messages de seu hub de notificação, com o corpo e os cabeçalhos corretos para o envio da notificação.</span><span class="sxs-lookup"><span data-stu-id="b8e91-136">The above methods send an HTTP POST request to the /messages endpoint of your notification hub, with the correct body and headers to send the notification.</span></span>

### <a name="using-debug-property-to-enable-detailed-logging"></a><span data-ttu-id="b8e91-137">Usando a propriedade de depuração para habilitar o registro em log detalhado</span><span class="sxs-lookup"><span data-stu-id="b8e91-137">Using debug property to enable detailed logging</span></span>
<span data-ttu-id="b8e91-138">A habilitação da propriedade de depuração ao inicializar o Hub de notificação gravará as informações do registro em log detalhadas sobre a solicitação HTTP e despejo da resposta, bem como o resultado do envio da mensagem de notificação detalhada.</span><span class="sxs-lookup"><span data-stu-id="b8e91-138">Enabling debug property while initializing the Notification Hub will write out detailed logging information about the HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="b8e91-139">Recentemente, adicionamos esta propriedade chamada [propriedade TestSend de Hubs de Notificação](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) que retorna informações detalhadas sobre o resultado de envio da notificação.</span><span class="sxs-lookup"><span data-stu-id="b8e91-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about the notification send outcome.</span></span> <span data-ttu-id="b8e91-140">Para usá-la - inicialize usando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b8e91-140">To use it - initialize using the following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="b8e91-141">O Envio do Hub de notificação solicita que a URL HTTP seja anexada com uma querystring "test" como um resultado.</span><span class="sxs-lookup"><span data-stu-id="b8e91-141">The Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="b8e91-142"><a name="complete-tutorial"></a>Concluir o tutorial</span><span class="sxs-lookup"><span data-stu-id="b8e91-142"><a name="complete-tutorial"></a>Complete the tutorial</span></span>
<span data-ttu-id="b8e91-143">Agora você pode concluir o Tutorial de introdução ao enviar a notificação de um back-end do Python.</span><span class="sxs-lookup"><span data-stu-id="b8e91-143">Now you can complete the Get Started tutorial by sending the notification from a Python back-end.</span></span>

<span data-ttu-id="b8e91-144">Inicialize seu cliente dos Hubs de Notificação (substitua a cadeia de conexão e o nome do hub conforme indicado no [tutorial Introdução]):</span><span class="sxs-lookup"><span data-stu-id="b8e91-144">Initialize your Notification Hubs client (substitute the connection string and hub name as instructed in the [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="b8e91-145">Em seguida, adicione o código de envio dependendo da sua plataforma móvel de destino.</span><span class="sxs-lookup"><span data-stu-id="b8e91-145">Then add the send code depending on your target mobile platform.</span></span> <span data-ttu-id="b8e91-146">Este exemplo também adiciona métodos de nível superiores para habilitar as notificações de envio baseadas na plataforma send_windows_notification por exemplo, para windows e send_apple_notification (para a apple) etc.</span><span class="sxs-lookup"><span data-stu-id="b8e91-146">This sample also adds higher level methods to enable sending notifications based on the platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="b8e91-147">Windows Store e Windows Phone 8.1 (não Silverlight)</span><span class="sxs-lookup"><span data-stu-id="b8e91-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="b8e91-148">Silverlight para Windows Phone 8.0 e 8.1</span><span class="sxs-lookup"><span data-stu-id="b8e91-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="b8e91-149">iOS</span><span class="sxs-lookup"><span data-stu-id="b8e91-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="b8e91-150">Android</span><span class="sxs-lookup"><span data-stu-id="b8e91-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="b8e91-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="b8e91-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="b8e91-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="b8e91-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="b8e91-153">Executar o código do Python deve produzir uma notificação que aparece em seu dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="b8e91-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="b8e91-154">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="b8e91-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="b8e91-155">Habilitar propriedade de depuração</span><span class="sxs-lookup"><span data-stu-id="b8e91-155">Enabling debug property</span></span>
<span data-ttu-id="b8e91-156">Quando você ativa o sinalizador de depuração ao inicializar o NotificationHub então verá detalhada a solicitação HTTP e despejo de resposta, bem como NotificationOutcome semelhante ao seguinte onde você possa entender quais cabeçalhos HTTP são passados na solicitação e qual a resposta HTTP foi recebida do Hub de notificação:![][1]</span><span class="sxs-lookup"><span data-stu-id="b8e91-156">When you enable debug flag while initializing the NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like the following where you can understand what HTTP headers are passed in the request and what HTTP response was received from the Notification Hub: ![][1]</span></span>

<span data-ttu-id="b8e91-157">Você verá o resultado do Hub de notificação detalhado, p. ex.</span><span class="sxs-lookup"><span data-stu-id="b8e91-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="b8e91-158">quando a mensagem é enviada com êxito para o serviço de notificação por Push.</span><span class="sxs-lookup"><span data-stu-id="b8e91-158">when the message is successfully sent to the Push Notification Service.</span></span> 
  
        <Outcome>The Notification was successfully sent to the Push Notification System</Outcome>
* <span data-ttu-id="b8e91-159">Se não houvesse nenhum destino encontrado para qualquer notificação por push, em seguida, você provavelmente veria o seguinte na resposta (que indica que não havia nenhum registro encontrado para entregar a notificação provavelmente porque os registros tinham algumas marcas incompatíveis)</span><span class="sxs-lookup"><span data-stu-id="b8e91-159">If there were no targets found for any push notification then you are likely going to see the following in the response (which indicates that there were no registrations found to deliver the notification probably because the registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-to-windows"></a><span data-ttu-id="b8e91-160">Transmissão de notificação do sistema para Windows</span><span class="sxs-lookup"><span data-stu-id="b8e91-160">Broadcast toast notification to Windows</span></span>
<span data-ttu-id="b8e91-161">Observe os cabeçalhos que são enviados quando você está enviando uma transmissão de notificação do sistema para cliente do Windows.</span><span class="sxs-lookup"><span data-stu-id="b8e91-161">Notice the headers that get sent out when you are sending a broadcast toast notification to Windows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="b8e91-162">Enviar notificação especificando uma marca (ou expressão de marca)</span><span class="sxs-lookup"><span data-stu-id="b8e91-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="b8e91-163">Observe as Marcas do cabeçalho HTTP que são adicionadas à solicitação HTTP (no exemplo a seguir, está enviando a notificação somente para os registros com carga 'esportes')</span><span class="sxs-lookup"><span data-stu-id="b8e91-163">Notice the Tags HTTP header which gets added to the HTTP request (in the example below, we are sending the notification only to registrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="b8e91-164">Enviar notificação especificando várias marcas</span><span class="sxs-lookup"><span data-stu-id="b8e91-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="b8e91-165">Observe como as Marcas do cabeçalho HTTP se alteram quando várias marcas são enviadas.</span><span class="sxs-lookup"><span data-stu-id="b8e91-165">Notice how the Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="b8e91-166">Notificação modelada</span><span class="sxs-lookup"><span data-stu-id="b8e91-166">Templated notification</span></span>
<span data-ttu-id="b8e91-167">Observe que o Formato de cabeçalho HTTP se altera e o corpo da carga é enviado como parte do corpo da solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="b8e91-167">Notice that the Format HTTP header changes and the payload body is sent as part of the HTTP request body:</span></span>

<span data-ttu-id="b8e91-168">**No lado cliente - modelo registrado**</span><span class="sxs-lookup"><span data-stu-id="b8e91-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="b8e91-169">**No lado servidor - envio da carga**</span><span class="sxs-lookup"><span data-stu-id="b8e91-169">**Server side - sending the payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="b8e91-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b8e91-170">Next Steps</span></span>
<span data-ttu-id="b8e91-171">Neste tópico, mostramos como criar um cliente REST simples do Python para os Hubs de Notificação.</span><span class="sxs-lookup"><span data-stu-id="b8e91-171">In this topic we showed how to create a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="b8e91-172">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="b8e91-172">From here you can:</span></span>

* <span data-ttu-id="b8e91-173">Baixe o [amostra de wrapper REST Python]completo, que contém todo o código acima.</span><span class="sxs-lookup"><span data-stu-id="b8e91-173">Download the full [Python REST wrapper sample], which contains all the code above.</span></span>
* <span data-ttu-id="b8e91-174">Continue a aprender sobre o recurso de marcação dos Hubs de Notificação no [tutorial Últimas notícias]</span><span class="sxs-lookup"><span data-stu-id="b8e91-174">Continue learning about Notification Hubs tagging feature in the [Breaking News tutorial]</span></span>
* <span data-ttu-id="b8e91-175">Continue a aprender sobre o recurso de modelos de Hubs de notificação no [tutorial Localização de notícias]</span><span class="sxs-lookup"><span data-stu-id="b8e91-175">Continue learning about Notification Hubs Templates feature in the [Localizing News tutorial]</span></span>

<!-- URLs -->
<span data-ttu-id="b8e91-176">[amostra de wrapper REST Python]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span><span class="sxs-lookup"><span data-stu-id="b8e91-176">[Python REST wrapper sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python</span></span>
<span data-ttu-id="b8e91-177">[tutorial Introdução]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="b8e91-177">[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="b8e91-178">[tutorial Últimas notícias]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="b8e91-178">[Breaking News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/</span></span>
<span data-ttu-id="b8e91-179">[tutorial Localização de notícias]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span><span class="sxs-lookup"><span data-stu-id="b8e91-179">[Localizing News tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

