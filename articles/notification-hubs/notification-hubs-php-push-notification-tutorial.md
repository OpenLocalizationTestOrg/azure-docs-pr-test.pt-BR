---
title: "aaaHow toouse Hubs de notificação com o PHP"
description: "Saiba como toouse Hubs de notificação do Azure de um back-end do PHP."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a>Como toouse Hubs de notificação do PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Você pode acessar todos os recursos de Hubs de notificação de um back-end do PHP/Java/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx).

Neste tópico, mostramos como:

* Criar um cliente REST para recursos dos Hubs de Notificação no PHP;
* Siga Olá [tutorial de Introdução Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) para sua plataforma móvel de preferência, Implementando a parte de back-end de saudação em PHP.

## <a name="client-interface"></a>Interface do cliente
interface de saudação do cliente principal pode fornecer Olá mesmos métodos que estão disponíveis no hello [.NET SDK de Hubs de notificação](http://msdn.microsoft.com/library/jj933431.aspx), isso permitirá que você toodirectly converter todos os tutoriais hello e exemplos no momento disponíveis neste site, e contribuído pela comunidade de saudação em Olá internet.

Você pode encontrar todos os código Olá disponível no hello [exemplo de wrapper de PHP REST].

Por exemplo, toocreate um cliente:

    $hub = new NotificationHub("connection string", "hubname");    

toosend uma notificação nativa do iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implementação
Se você ainda não fez, siga nosso [tutorial de Introdução Get] até toohello última seção onde você tem tooimplement Olá back-end.
Além disso, se você quiser que você pode usar código de saudação do hello [exemplo de wrapper de PHP REST] e vá diretamente toohello [tutorial completo Olá](#complete-tutorial) seção.

Todos Olá detalhes tooimplement um wrapper REST completo pode ser encontrado em [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Nesta seção, descreveremos implementação PHP Olá Olá de etapas principais necessárias tooaccess pontos de extremidade REST de Hubs de notificação:

1. Analisar a cadeia de conexão Olá
2. Gerar o token de autorização de saudação
3. Executar chamada hello HTTP

### <a name="parse-hello-connection-string"></a>Analisar a cadeia de conexão Olá
Aqui é Olá classe principal implementação Olá cliente, cujo construtor analisa a cadeia de caracteres de conexão hello:

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a>Criar token de segurança
criação de token de segurança Olá Olá detalhes está disponíveis [aqui](http://msdn.microsoft.com/library/dn495627.aspx).
método Hello tem toobe adicionado toohello **NotificationHub** token de saudação toocreate classe com base em Olá URI da solicitação atual hello e credenciais de saudação extraídas da cadeia de caracteres de conexão de saudação.

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a>Enviar uma notificação
Primeiro, vamos definir uma classe que representa uma notificação.

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

Essa classe é um contêiner para um corpo de notificação nativa ou um conjunto de propriedade no caso de uma notificação de modelo, e um conjunto de cabeçalhos que contém propriedades específicas de formato (plataforma nativa ou modelo) e plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).

Consulte toohello [documentação de APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos das plataformas específicas de notificação para todas as opções disponíveis de hello.

Essa classe de posse, agora podemos escrever Olá envio métodos de notificação dentro de saudação **NotificationHub** classe.

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

Olá acima métodos enviar um HTTP POST solicitação toohello /messages ponto de extremidade de hub de notificação, com corpo correto hello e notificação de saudação toosend cabeçalhos.

## <a name="complete-tutorial"></a>Tutorial de saudação concluída
Agora você pode concluir o tutorial de Introdução hello, enviando a notificação de saudação de um back-end do PHP.

Inicialize o cliente de Hubs de notificação (substitua o nome de hub e de cadeia de caracteres de conexão Olá conforme instruído no hello [tutorial de Introdução Get]):

    $hub = new NotificationHub("connection string", "hubname");    

Adicione código de envio de saudação dependendo de sua plataforma móvel de destino.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Windows Store e Windows Phone 8.1 (não Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Silverlight para Windows Phone 8.0 e 8.1
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

Executar o código PHP agora deve produzir uma notificação que aparece no dispositivo de destino.

## <a name="next-steps"></a>Próximas etapas
Neste tópico, mostramos como toocreate um Java simple REST cliente Hubs de notificação. A partir daqui, você pode:

* Baixar Olá completo [exemplo de wrapper de PHP REST], que contém todos os códigos de saudação acima.
* Saber mais sobre o recurso de indicação Olá [tutorial últimas notícias] de Hubs de notificação
* Saiba mais sobre o envio por push usuários de tooindividual notificações [tutorial notificar usuários]

Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).

[exemplo de wrapper de PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial de Introdução Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

