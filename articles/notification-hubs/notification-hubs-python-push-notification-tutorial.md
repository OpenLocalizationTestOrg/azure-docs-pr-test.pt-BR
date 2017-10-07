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
# <a name="how-toouse-notification-hubs-from-python"></a>Como toouse Hubs de notificação do Python
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Você pode acessar todos os recursos de Hubs de notificação de um back-end do Java/PHP/Python/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx).

> [!NOTE]
> Este é um exemplo da implementação de referência para implementar Olá notificação envia em Python e não é Olá suporte oficial para SDK de Python do Hub de notificações.
> 
> Este exemplo é escrito usando Python 3.4.
> 
> 

Neste tópico, mostramos como:

* Crie um cliente REST para recursos de Hubs de notificação em Python.
* Envie notificações usando Olá Python interface toohello APIs de REST do Hub de notificação. 
* Obter um despejo de saudação resposta da solicitação HTTP REST para fins educativos/depuração. 

Você pode seguir Olá [tutorial de Introdução Get](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) para sua plataforma móvel de preferência, Implementando a parte de back-end de saudação em Python.

> [!NOTE]
> escopo de saudação do exemplo hello é apenas notificações de toosend limitada e não faz nenhum gerenciamento de registro.
> 
> 

## <a name="client-interface"></a>Interface do cliente
interface de saudação do cliente principal pode fornecer Olá mesmos métodos que estão disponíveis no hello [.NET SDK de Hubs de notificação](http://msdn.microsoft.com/library/jj933431.aspx). Isso permitirá que você toodirectly converter todos os tutoriais hello e exemplos no momento disponíveis neste site e contribuído pela comunidade de saudação em Olá internet.

Você pode encontrar todos os código Olá disponível no hello [amostra do Python REST wrapper].

Por exemplo, toocreate um cliente:

    isDebug = True
    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

toosend uma janela de notificação do sistema:

    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello world!</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

## <a name="implementation"></a>Implementação
Se você ainda não fez, siga nosso [tutorial de Introdução Get] até toohello última seção onde você tem tooimplement Olá back-end.

Todos Olá detalhes tooimplement um wrapper REST completo pode ser encontrado em [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Esta seção é descrever a implementação de Python Olá de saudação de etapas principais necessárias tooaccess pontos de extremidade REST de Hubs de notificação e enviar notificações

1. Analisar a cadeia de conexão Olá
2. Gerar o token de autorização de saudação
3. Enviar uma notificação usando a API REST do HTTP

### <a name="parse-hello-connection-string"></a>Analisar a cadeia de conexão Olá
Aqui está a classe principal do hello implementando cliente hello, cujo construtor analisa a cadeia de caracteres de conexão de saudação:

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


### <a name="create-security-token"></a>Criar token de segurança
criação de token de segurança Olá Olá detalhes está disponíveis [aqui](http://msdn.microsoft.com/library/dn495627.aspx).
os métodos seguintes Hello ter toobe adicionado toohello **NotificationHub** token de saudação toocreate classe com base em Olá URI da solicitação atual hello e credenciais de saudação extraídas da cadeia de caracteres de conexão de saudação.

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

### <a name="send-a-notification-using-http-rest-api"></a>Enviar uma notificação usando a API REST do HTTP
Primeiro, vamos definir uma classe que representa uma notificação.

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

Essa classe é um contêiner para um corpo de notificação nativa ou um conjunto de propriedades no caso de uma notificação de modelo, um conjunto de cabeçalhos que contém o formato (plataforma nativa ou modelo) e propriedades específicas da plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).

Consulte toohello [documentação de APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos das plataformas específicas de notificação para todas as opções disponíveis de hello.

Agora com essa classe, podemos gravar Olá enviar os métodos de notificação dentro de saudação **NotificationHub** classe.

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

Olá acima métodos enviar um HTTP POST solicitação toohello /messages ponto de extremidade de hub de notificação, com corpo correto hello e notificação de saudação toosend cabeçalhos.

### <a name="using-debug-property-tooenable-detailed-logging"></a>Usar tooenable de propriedade de depuração de registro em log detalhado
Habilitando a propriedade de depuração durante a inicialização Olá Hub de notificação gravará as informações de log detalhadas sobre Olá HTTP resultado de envio de solicitação e despejo de resposta, bem como mensagem de notificação detalhada. Adicionamos recentemente essa propriedade chamada [TestSend de Hubs de notificação propriedade](http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx) que retorna informações detalhadas sobre o resultado de envio de notificação de saudação. toouse-- inicializar usando Olá seguintes:

    hub = NotificationHub("myConnectionString", "myNotificationHubName", isDebug)

solicitação de envio do Hub de notificação de saudação URL HTTP é anexada com uma querystring "test" como resultado. 

## <a name="complete-tutorial"></a>Tutorial de saudação concluída
Agora você pode concluir o tutorial de Introdução hello, enviando a notificação de saudação de um back-end do Python.

Inicialize o cliente de Hubs de notificação (substitua o nome de hub e de cadeia de caracteres de conexão Olá conforme instruído no hello [tutorial de Introdução Get]):

    hub = NotificationHub("myConnectionString", "myNotificationHubName")

Adicione código de envio de saudação dependendo de sua plataforma móvel de destino. Este exemplo também adiciona tooenable de métodos de nível superior enviar notificações com base na plataforma hello, por exemplo, send_windows_notification para windows. send_apple_notification (para a apple) etc. 

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store e Windows Phone 8.1 (não Silverlight)
    wns_payload = """<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Test</text></binding></visual></toast>"""
    hub.send_windows_notification(wns_payload)

### <a name="windows-phone-80-and-81-silverlight"></a>Silverlight para Windows Phone 8.0 e 8.1
    hub.send_mpns_notification(toast)

### <a name="ios"></a>iOS
    alert_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_apple_notification(alert_payload)

### <a name="android"></a>Android
    gcm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_gcm_notification(gcm_payload)

### <a name="kindle-fire"></a>Kindle Fire
    adm_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_adm_notification(adm_payload)

### <a name="baidu"></a>Baidu
    baidu_payload = {
        'data':
            {
                'msg': 'Hello!'
            }
    }
    hub.send_baidu_notification(baidu_payload)

Executar o código do Python deve produzir uma notificação que aparece em seu dispositivo de destino.

## <a name="examples"></a>Exemplos:
### <a name="enabling-debug-property"></a>Habilitar propriedade de depuração
Quando você habilita o sinalizador de depuração durante a inicialização Olá NotificationHub, em seguida, você verá detalhadas despejo de solicitação e resposta HTTP, bem como NotificationOutcome como Olá seguinte onde você possa entender quais cabeçalhos HTTP são passados na solicitação hello e quais HTTP resposta foi recebida do hello Hub de notificação:![][1]

Você verá o resultado do Hub de notificação detalhado, p. ex. 

* Quando a mensagem de saudação é enviada com êxito toohello Push Notification Service. 
  
        <Outcome>hello Notification was successfully sent toohello Push Notification System</Outcome>
* Se não houvesse nenhum destino encontrado para qualquer notificação por push, em seguida, você provavelmente vai toosee seguinte Olá resposta hello (que indica que não houve nenhum registro encontrado notificação de saudação toodeliver provavelmente porque registros Olá tinham alguns marcas não correspondentes)
  
        '<NotificationOutcome xmlns="http://schemas.microsoft.com/netservices/2010/10/servicebus/connect" xmlns:i="http://www.w3.org/2001/XMLSchema-instance"><Success>0</Success><Failure>0</Failure><Results i:nil="true"/></NotificationOutcome>'

### <a name="broadcast-toast-notification-toowindows"></a>Difusão tooWindows de notificação do sistema
Observe os cabeçalhos de saudação obtenham enviados quando você está enviando um cliente de tooWindows de notificação do sistema de difusão. 

    hub.send_windows_notification(wns_payload)

![][2]

### <a name="send-notification-specifying-a-tag-or-tag-expression"></a>Enviar notificação especificando uma marca (ou expressão de marca)
Cabeçalho de HTTP de marcas de saudação de aviso que é adicionado a solicitação HTTP de toohello (no exemplo hello abaixo, estamos enviando Olá notificação apenas tooregistrations com carga 'esportes')

    hub.send_windows_notification(wns_payload, "sports")

![][3]

### <a name="send-notification-specifying-multiple-tags"></a>Enviar notificação especificando várias marcas
Observe como o cabeçalho de HTTP de marcas de saudação muda quando várias marcas são enviadas. 

    tags = {'sports', 'politics'}
    hub.send_windows_notification(wns_payload, tags)

![][4]

### <a name="templated-notification"></a>Notificação modelada
Observe que Olá alterações de cabeçalho HTTP de formato e Olá corpo de carga é enviado como parte do corpo da solicitação HTTP de saudação:

**No lado cliente - modelo registrado**

        var template =
                        @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(greeting_en)</text></binding></visual></toast>";

**Do lado do servidor - envio de carga Olá**

        template_payload = {'greeting_en': 'Hello', 'greeting_fr': 'Salut'}
        hub.send_template_notification(template_payload)

![][5]

## <a name="next-steps"></a>Próximas etapas
Neste tópico, mostramos como toocreate um simple Python REST cliente Hubs de notificação. A partir daqui, você pode:

* Baixar Olá completo [amostra do Python REST wrapper], que contém todos os códigos de saudação acima.
* Saber mais sobre o recurso de indicação Olá de Hubs de notificação [tutorial últimas notícias]
* Saber mais sobre o recurso de modelos de Hubs de notificação no hello [tutorial de localização de notícias]

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

