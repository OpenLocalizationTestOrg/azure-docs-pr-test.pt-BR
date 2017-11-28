---
title: "aaaHow toouse Hubs de notificação com Python"
description: "Saiba como toouse Hubs de notificação do Azure de um back-end do Python."
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
ms.openlocfilehash: 21d5aaf7fc24c9936fac8e0a8de640c66c51ab0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-python"></a><span data-ttu-id="7b04b-103">Como toouse Hubs de notificação do Python</span><span class="sxs-lookup"><span data-stu-id="7b04b-103">How toouse Notification Hubs from Python</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="7b04b-104">Você pode acessar todos os recursos de Hubs de notificação de um back-end do Java/PHP/Python/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b04b-104">You can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="7b04b-105">Este é um exemplo da implementação de referência para implementar Olá notificação envia em Python e não é Olá suporte oficial para SDK de Python do Hub de notificações.</span><span class="sxs-lookup"><span data-stu-id="7b04b-105">This is a sample reference implementation for implementing hello notification sends in Python and is not hello officially supported Notifications Hub Python SDK.</span></span>
> 
> <span data-ttu-id="7b04b-106">Este exemplo é escrito usando Python 3.4.</span><span class="sxs-lookup"><span data-stu-id="7b04b-106">This sample is written using Python 3.4.</span></span>
> 
> 

<span data-ttu-id="7b04b-107">Neste tópico, mostramos como:</span><span class="sxs-lookup"><span data-stu-id="7b04b-107">In this topic we show how to:</span></span>

* <span data-ttu-id="7b04b-108">Crie um cliente REST para recursos de Hubs de notificação em Python.</span><span class="sxs-lookup"><span data-stu-id="7b04b-108">Build a REST client for Notification Hubs features in Python.</span></span>
* <span data-ttu-id="7b04b-109">Envie notificações usando Olá Python interface toohello APIs de REST do Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="7b04b-109">Send notifications using hello Python interface toohello Notification Hub REST APIs.</span></span> 
* <span data-ttu-id="7b04b-110">Obter um despejo de saudação resposta da solicitação HTTP REST para fins educativos/depuração.</span><span class="sxs-lookup"><span data-stu-id="7b04b-110">Get a dump of hello HTTP REST request/response for debugging/educational purpose.</span></span> 

<span data-ttu-id="7b04b-111">Você pode seguir Olá [tutorial de Introdução Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) para sua plataforma móvel de preferência, Implementando a parte de back-end de saudação em Python.</span><span class="sxs-lookup"><span data-stu-id="7b04b-111">You can follow hello [Get started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) for your mobile platform of choice, implementing hello back-end portion in Python.</span></span>

> [!NOTE]
> <span data-ttu-id="7b04b-112">escopo de saudação do exemplo hello é apenas notificações de toosend limitada e não faz nenhum gerenciamento de registro.</span><span class="sxs-lookup"><span data-stu-id="7b04b-112">hello scope of hello sample is only limited toosend notifications and it doesn't do any registration management.</span></span>
> 
> 

## <a name="client-interface"></a><span data-ttu-id="7b04b-113">Interface do cliente</span><span class="sxs-lookup"><span data-stu-id="7b04b-113">Client interface</span></span>
<span data-ttu-id="7b04b-114">interface de saudação do cliente principal pode fornecer Olá mesmos métodos que estão disponíveis no hello [.NET SDK de Hubs de notificação](http://msdn.microsoft.com/library/jj933431.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b04b-114">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx).</span></span> <span data-ttu-id="7b04b-115">Isso permitirá que você toodirectly converter todos os tutoriais hello e exemplos no momento disponíveis neste site e contribuído pela comunidade de saudação em Olá internet.</span><span class="sxs-lookup"><span data-stu-id="7b04b-115">This will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="7b04b-116">Você pode encontrar todos os código Olá disponível no hello [amostra do Python REST wrapper].</span><span class="sxs-lookup"><span data-stu-id="7b04b-116">You can find all hello code available in hello [Python REST wrapper sample].</span></span>

<span data-ttu-id="7b04b-117">Por exemplo, toocreate um cliente:</span><span class="sxs-lookup"><span data-stu-id="7b04b-117">For example, toocreate a client:</span></span>

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="7b04b-118">toosend uma janela de notificação do sistema:</span><span class="sxs-lookup"><span data-stu-id="7b04b-118">toosend a Windows toast notification:</span></span>

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a><span data-ttu-id="7b04b-119">Implementação</span><span class="sxs-lookup"><span data-stu-id="7b04b-119">Implementation</span></span>
<span data-ttu-id="7b04b-120">Se você ainda não fez, siga nosso [tutorial de Introdução Get] até toohello última seção onde você tem tooimplement Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="7b04b-120">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>

<span data-ttu-id="7b04b-121">Todos Olá detalhes tooimplement um wrapper REST completo pode ser encontrado em [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b04b-121">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="7b04b-122">Esta seção é descrever a implementação de Python Olá de saudação de etapas principais necessárias tooaccess pontos de extremidade REST de Hubs de notificação e enviar notificações</span><span class="sxs-lookup"><span data-stu-id="7b04b-122">In this section we will describe hello Python implementation of hello main steps required tooaccess Notification Hubs REST endpoints and send notifications</span></span>

1. <span data-ttu-id="7b04b-123">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="7b04b-123">Parse hello connection string</span></span>
2. <span data-ttu-id="7b04b-124">Gerar o token de autorização de saudação</span><span class="sxs-lookup"><span data-stu-id="7b04b-124">Generate hello authorization token</span></span>
3. <span data-ttu-id="7b04b-125">Enviar uma notificação usando a API REST do HTTP</span><span class="sxs-lookup"><span data-stu-id="7b04b-125">Send a notification using HTTP REST API</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="7b04b-126">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="7b04b-126">Parse hello connection string</span></span>
<span data-ttu-id="7b04b-127">Aqui está a classe principal do hello implementando cliente hello, cujo construtor analisa a cadeia de caracteres de conexão de saudação:</span><span class="sxs-lookup"><span data-stu-id="7b04b-127">Here is hello main class implementing hello client, whose constructor parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="7b04b-128">Criar token de segurança</span><span class="sxs-lookup"><span data-stu-id="7b04b-128">Create security token</span></span>
<span data-ttu-id="7b04b-129">criação de token de segurança Olá Olá detalhes está disponíveis [aqui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b04b-129">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="7b04b-130">os métodos seguintes Hello ter toobe adicionado toohello **NotificationHub** token de saudação toocreate classe com base em Olá URI da solicitação atual hello e credenciais de saudação extraídas da cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b04b-130">hello following methods have toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification-using-http-rest-api"></a><span data-ttu-id="7b04b-131">Enviar uma notificação usando a API REST do HTTP</span><span class="sxs-lookup"><span data-stu-id="7b04b-131">Send a notification using HTTP REST API</span></span>
<span data-ttu-id="7b04b-132">Primeiro, vamos definir uma classe que representa uma notificação.</span><span class="sxs-lookup"><span data-stu-id="7b04b-132">First, let use define a class representing a notification.</span></span>

    class Notification:
        def __init__(self, notification_format=None, payload=None, debug=0):
            valid_formats = ['template', 'apple', 'gcm', 'windows', 'windowsphone', "adm", "baidu"]
            if not any(x in notification_format for x in valid_formats):
                raise Exception(
                    "Invalid Notification format. " +
                    "Must be one of hello following - 'template', 'apple', 'gcm', 'windows', 'windowsphone', 'adm', 'baidu'")

            self.format = notification_format
            self.payload = payload

            # array with keynames for headers
            # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
            # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry
            # in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
            self.headers = None

<span data-ttu-id="7b04b-133">Essa classe é um contêiner para um corpo de notificação nativa ou um conjunto de propriedades no caso de uma notificação de modelo, um conjunto de cabeçalhos que contém o formato (plataforma nativa ou modelo) e propriedades específicas da plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).</span><span class="sxs-lookup"><span data-stu-id="7b04b-133">This class is a container for a native notification body or a set of properties in case of a template notification, a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="7b04b-134">Consulte toohello [documentação de APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos das plataformas específicas de notificação para todas as opções disponíveis de hello.</span><span class="sxs-lookup"><span data-stu-id="7b04b-134">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="7b04b-135">Agora com essa classe, podemos gravar Olá enviar os métodos de notificação dentro de saudação **NotificationHub** classe.</span><span class="sxs-lookup"><span data-stu-id="7b04b-135">Now with this class, we can write hello send notification methods inside of hello **NotificationHub** class.</span></span>

    def make_http_request(self, url, payload, headers):
        parsed_url = urllib.parse.urlparse(url)
        connection = http.client.HTTPSConnection(parsed_url.hostname, parsed_url.port)

        if self.Debug > 0:
            connection.set_debuglevel(self.Debug)
            # adding this querystring parameter gets detailed information about hello PNS send notification outcome
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

        # add hello tags/tag expressions toohello headers collection
        if tag_list != "":
            headers.update({'ServiceBusNotification-Tags': tag_list})

        # add any custom headers toohello headers collection that hello user may have added
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

<span data-ttu-id="7b04b-136">Olá acima métodos enviar um HTTP POST solicitação toohello /messages ponto de extremidade de hub de notificação, com corpo correto hello e notificação de saudação toosend cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="7b04b-136">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

### <a name="using-debug-property-tooenable-detailed-logging"></a><span data-ttu-id="7b04b-137">Usar tooenable de propriedade de depuração de registro em log detalhado</span><span class="sxs-lookup"><span data-stu-id="7b04b-137">Using debug property tooenable detailed logging</span></span>
<span data-ttu-id="7b04b-138">Habilitando a propriedade de depuração durante a inicialização Olá Hub de notificação gravará as informações de log detalhadas sobre Olá HTTP resultado de envio de solicitação e despejo de resposta, bem como mensagem de notificação detalhada.</span><span class="sxs-lookup"><span data-stu-id="7b04b-138">Enabling debug property while initializing hello Notification Hub will write out detailed logging information about hello HTTP request and response dump as well as detailed Notification message send outcome.</span></span> <span data-ttu-id="7b04b-139">Adicionamos recentemente essa propriedade chamada [TestSend de Hubs de notificação propriedade](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) que retorna informações detalhadas sobre o resultado de envio de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b04b-139">We recently added this property called [Notification Hubs TestSend property](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) which returns detailed information about hello notification send outcome.</span></span> <span data-ttu-id="7b04b-140">toouse-- inicializar usando Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="7b04b-140">toouse it - initialize using hello following:</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

<span data-ttu-id="7b04b-141">solicitação de envio do Hub de notificação de saudação URL HTTP é anexada com uma querystring "test" como resultado.</span><span class="sxs-lookup"><span data-stu-id="7b04b-141">hello Notification Hub Send request HTTP URL gets appended with a "test" querystring as a result.</span></span> 

## <span data-ttu-id="7b04b-142"><a name="complete-tutorial"></a>Tutorial de saudação concluída</span><span class="sxs-lookup"><span data-stu-id="7b04b-142"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="7b04b-143">Agora você pode concluir o tutorial de Introdução hello, enviando a notificação de saudação de um back-end do Python.</span><span class="sxs-lookup"><span data-stu-id="7b04b-143">Now you can complete hello Get Started tutorial by sending hello notification from a Python back-end.</span></span>

<span data-ttu-id="7b04b-144">Inicialize o cliente de Hubs de notificação (substitua o nome de hub e de cadeia de caracteres de conexão Olá conforme instruído no hello [tutorial de Introdução Get]):</span><span class="sxs-lookup"><span data-stu-id="7b04b-144">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

<span data-ttu-id="7b04b-145">Adicione código de envio de saudação dependendo de sua plataforma móvel de destino.</span><span class="sxs-lookup"><span data-stu-id="7b04b-145">Then add hello send code depending on your target mobile platform.</span></span> <span data-ttu-id="7b04b-146">Este exemplo também adiciona tooenable de métodos de nível superior enviar notificações com base na plataforma hello, por exemplo, send_windows_notification para windows. send_apple_notification (para a apple) etc.</span><span class="sxs-lookup"><span data-stu-id="7b04b-146">This sample also adds higher level methods tooenable sending notifications based on hello platform e.g. send_windows_notification for windows; send_apple_notification (for apple) etc.</span></span> 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="7b04b-147">Windows Store e Windows Phone 8.1 (não Silverlight)</span><span class="sxs-lookup"><span data-stu-id="7b04b-147">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="7b04b-148">Silverlight para Windows Phone 8.0 e 8.1</span><span class="sxs-lookup"><span data-stu-id="7b04b-148">Windows Phone 8.0 and 8.1 Silverlight</span></span>
    hub.send_mpns_notification(toast)

### <a name="ios"></a><span data-ttu-id="7b04b-149">iOS</span><span class="sxs-lookup"><span data-stu-id="7b04b-149">iOS</span></span>
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a><span data-ttu-id="7b04b-150">Android</span><span class="sxs-lookup"><span data-stu-id="7b04b-150">Android</span></span>
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a><span data-ttu-id="7b04b-151">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="7b04b-151">Kindle Fire</span></span>
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a><span data-ttu-id="7b04b-152">Baidu</span><span class="sxs-lookup"><span data-stu-id="7b04b-152">Baidu</span></span>
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

<span data-ttu-id="7b04b-153">Executar o código do Python deve produzir uma notificação que aparece em seu dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="7b04b-153">Running your Python code should produce a notification appearing on your target device.</span></span>

## <a name="examples"></a><span data-ttu-id="7b04b-154">Exemplos:</span><span class="sxs-lookup"><span data-stu-id="7b04b-154">Examples:</span></span>
### <a name="enabling-debug-property"></a><span data-ttu-id="7b04b-155">Habilitar propriedade de depuração</span><span class="sxs-lookup"><span data-stu-id="7b04b-155">Enabling debug property</span></span>
<span data-ttu-id="7b04b-156">Quando você habilita o sinalizador de depuração durante a inicialização Olá NotificationHub, em seguida, você verá detalhadas despejo de solicitação e resposta HTTP, bem como NotificationOutcome como Olá seguinte onde você possa entender quais cabeçalhos HTTP são passados na solicitação hello e quais HTTP resposta foi recebida do hello Hub de notificação:![][1]</span><span class="sxs-lookup"><span data-stu-id="7b04b-156">When you enable debug flag while initializing hello NotificationHub then you will see detailed HTTP request and response dump as well as NotificationOutcome like hello following where you can understand what HTTP headers are passed in hello request and what HTTP response was received from hello Notification Hub: ![][1]</span></span>

<span data-ttu-id="7b04b-157">Você verá o resultado do Hub de notificação detalhado, p. ex.</span><span class="sxs-lookup"><span data-stu-id="7b04b-157">You will see detailed Notification Hub result e.g.</span></span> 

* <span data-ttu-id="7b04b-158">Quando a mensagem de saudação é enviada com êxito toohello Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="7b04b-158">when hello message is successfully sent toohello Push Notification Service.</span></span> 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* <span data-ttu-id="7b04b-159">Se não houvesse nenhum destino encontrado para qualquer notificação por push, em seguida, você provavelmente vai toosee seguinte Olá resposta hello (que indica que não houve nenhum registro encontrado notificação de saudação toodeliver provavelmente porque registros Olá tinham alguns marcas não correspondentes)</span><span class="sxs-lookup"><span data-stu-id="7b04b-159">If there were no targets found for any push notification then you are likely going toosee hello following in hello response (which indicates that there were no registrations found toodeliver hello notification probably because hello registrations had some mismatched tags)</span></span>
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a><span data-ttu-id="7b04b-160">Difusão tooWindows de notificação do sistema</span><span class="sxs-lookup"><span data-stu-id="7b04b-160">Broadcast toast notification tooWindows</span></span>
<span data-ttu-id="7b04b-161">Observe os cabeçalhos de saudação obtenham enviados quando você está enviando um cliente de tooWindows de notificação do sistema de difusão.</span><span class="sxs-lookup"><span data-stu-id="7b04b-161">Notice hello headers that get sent out when you are sending a broadcast toast notification tooWindows client.</span></span> 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a><span data-ttu-id="7b04b-162">Enviar notificação especificando uma marca (ou expressão de marca)</span><span class="sxs-lookup"><span data-stu-id="7b04b-162">Send notification specifying a tag (or tag expression)</span></span>
<span data-ttu-id="7b04b-163">Cabeçalho de HTTP de marcas de saudação de aviso que é adicionado a solicitação HTTP de toohello (no exemplo hello abaixo, estamos enviando Olá notificação apenas tooregistrations com carga 'esportes')</span><span class="sxs-lookup"><span data-stu-id="7b04b-163">Notice hello Tags HTTP header which gets added toohello HTTP request (in hello example below, we are sending hello notification only tooregistrations with 'sports' payload)</span></span>

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a><span data-ttu-id="7b04b-164">Enviar notificação especificando várias marcas</span><span class="sxs-lookup"><span data-stu-id="7b04b-164">Send notification specifying multiple tags</span></span>
<span data-ttu-id="7b04b-165">Observe como o cabeçalho de HTTP de marcas de saudação muda quando várias marcas são enviadas.</span><span class="sxs-lookup"><span data-stu-id="7b04b-165">Notice how hello Tags HTTP header changes when multiple tags are sent.</span></span> 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a><span data-ttu-id="7b04b-166">Notificação modelada</span><span class="sxs-lookup"><span data-stu-id="7b04b-166">Templated notification</span></span>
<span data-ttu-id="7b04b-167">Observe que Olá alterações de cabeçalho HTTP de formato e Olá corpo de carga é enviado como parte do corpo da solicitação HTTP de saudação:</span><span class="sxs-lookup"><span data-stu-id="7b04b-167">Notice that hello Format HTTP header changes and hello payload body is sent as part of hello HTTP request body:</span></span>

<span data-ttu-id="7b04b-168">**No lado cliente - modelo registrado**</span><span class="sxs-lookup"><span data-stu-id="7b04b-168">**Client side - registered template**</span></span>

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

<span data-ttu-id="7b04b-169">**Do lado do servidor - envio de carga Olá**</span><span class="sxs-lookup"><span data-stu-id="7b04b-169">**Server side - sending hello payload**</span></span>

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a><span data-ttu-id="7b04b-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b04b-170">Next Steps</span></span>
<span data-ttu-id="7b04b-171">Neste tópico, mostramos como toocreate um simple Python REST cliente Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="7b04b-171">In this topic we showed how toocreate a simple Python REST client for Notification Hubs.</span></span> <span data-ttu-id="7b04b-172">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="7b04b-172">From here you can:</span></span>

* <span data-ttu-id="7b04b-173">Baixar Olá completo [amostra do Python REST wrapper], que contém todos os códigos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="7b04b-173">Download hello full [Python REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="7b04b-174">Saber mais sobre o recurso de indicação Olá de Hubs de notificação [tutorial últimas notícias]</span><span class="sxs-lookup"><span data-stu-id="7b04b-174">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="7b04b-175">Saber mais sobre o recurso de modelos de Hubs de notificação no hello [tutorial de localização de notícias]</span><span class="sxs-lookup"><span data-stu-id="7b04b-175">Continue learning about Notification Hubs Templates feature in hello [Localizing News tutorial]</span></span>

<!-- URLs -->
[amostra do Python REST wrapper]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-python
[tutorial de Introdução Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[tutorial últimas notícias]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-breaking-news/
[tutorial de localização de notícias]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-send-localized-breaking-news/

<!-- Images. -->
[1]: ./media/notification-hubs-python-backend-how-to/DetailedLoggingInfo.png
[2]: ./media/notification-hubs-python-backend-how-to/BroadcastScenario.png
[3]: ./media/notification-hubs-python-backend-how-to/SendWithOneTag.png
[4]: ./media/notification-hubs-python-backend-how-to/SendWithMultipleTags.png
[5]: ./media/notification-hubs-python-backend-how-to/TemplatedNotification.png

