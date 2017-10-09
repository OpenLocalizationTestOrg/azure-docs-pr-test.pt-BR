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
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="2557b-103">Como toouse Hubs de notificação do PHP</span><span class="sxs-lookup"><span data-stu-id="2557b-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="2557b-104">Você pode acessar todos os recursos de Hubs de notificação de um back-end do PHP/Java/Ruby usando a interface REST do Hub de notificação de hello conforme descrito no tópico do MSDN Olá [APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2557b-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="2557b-105">Neste tópico, mostramos como:</span><span class="sxs-lookup"><span data-stu-id="2557b-105">In this topic we show how to:</span></span>

* <span data-ttu-id="2557b-106">Criar um cliente REST para recursos dos Hubs de Notificação no PHP;</span><span class="sxs-lookup"><span data-stu-id="2557b-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="2557b-107">Siga Olá [tutorial de Introdução Get](notification-hubs-ios-apple-push-notification-apns-get-started.md) para sua plataforma móvel de preferência, Implementando a parte de back-end de saudação em PHP.</span><span class="sxs-lookup"><span data-stu-id="2557b-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="2557b-108">Interface do cliente</span><span class="sxs-lookup"><span data-stu-id="2557b-108">Client interface</span></span>
<span data-ttu-id="2557b-109">interface de saudação do cliente principal pode fornecer Olá mesmos métodos que estão disponíveis no hello [.NET SDK de Hubs de notificação](http://msdn.microsoft.com/library/jj933431.aspx), isso permitirá que você toodirectly converter todos os tutoriais hello e exemplos no momento disponíveis neste site, e contribuído pela comunidade de saudação em Olá internet.</span><span class="sxs-lookup"><span data-stu-id="2557b-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="2557b-110">Você pode encontrar todos os código Olá disponível no hello [exemplo de wrapper de PHP REST].</span><span class="sxs-lookup"><span data-stu-id="2557b-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="2557b-111">Por exemplo, toocreate um cliente:</span><span class="sxs-lookup"><span data-stu-id="2557b-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="2557b-112">toosend uma notificação nativa do iOS:</span><span class="sxs-lookup"><span data-stu-id="2557b-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="2557b-113">Implementação</span><span class="sxs-lookup"><span data-stu-id="2557b-113">Implementation</span></span>
<span data-ttu-id="2557b-114">Se você ainda não fez, siga nosso [tutorial de Introdução Get] até toohello última seção onde você tem tooimplement Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="2557b-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="2557b-115">Além disso, se você quiser que você pode usar código de saudação do hello [exemplo de wrapper de PHP REST] e vá diretamente toohello [tutorial completo Olá](#complete-tutorial) seção.</span><span class="sxs-lookup"><span data-stu-id="2557b-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="2557b-116">Todos Olá detalhes tooimplement um wrapper REST completo pode ser encontrado em [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="2557b-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="2557b-117">Nesta seção, descreveremos implementação PHP Olá Olá de etapas principais necessárias tooaccess pontos de extremidade REST de Hubs de notificação:</span><span class="sxs-lookup"><span data-stu-id="2557b-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="2557b-118">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="2557b-118">Parse hello connection string</span></span>
2. <span data-ttu-id="2557b-119">Gerar o token de autorização de saudação</span><span class="sxs-lookup"><span data-stu-id="2557b-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="2557b-120">Executar chamada hello HTTP</span><span class="sxs-lookup"><span data-stu-id="2557b-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="2557b-121">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="2557b-121">Parse hello connection string</span></span>
<span data-ttu-id="2557b-122">Aqui é Olá classe principal implementação Olá cliente, cujo construtor analisa a cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="2557b-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="2557b-123">Criar token de segurança</span><span class="sxs-lookup"><span data-stu-id="2557b-123">Create security token</span></span>
<span data-ttu-id="2557b-124">criação de token de segurança Olá Olá detalhes está disponíveis [aqui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="2557b-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="2557b-125">método Hello tem toobe adicionado toohello **NotificationHub** token de saudação toocreate classe com base em Olá URI da solicitação atual hello e credenciais de saudação extraídas da cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2557b-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="2557b-126">Enviar uma notificação</span><span class="sxs-lookup"><span data-stu-id="2557b-126">Send a notification</span></span>
<span data-ttu-id="2557b-127">Primeiro, vamos definir uma classe que representa uma notificação.</span><span class="sxs-lookup"><span data-stu-id="2557b-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="2557b-128">Essa classe é um contêiner para um corpo de notificação nativa ou um conjunto de propriedade no caso de uma notificação de modelo, e um conjunto de cabeçalhos que contém propriedades específicas de formato (plataforma nativa ou modelo) e plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).</span><span class="sxs-lookup"><span data-stu-id="2557b-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="2557b-129">Consulte toohello [documentação de APIs de REST de Hubs de notificação](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos das plataformas específicas de notificação para todas as opções disponíveis de hello.</span><span class="sxs-lookup"><span data-stu-id="2557b-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="2557b-130">Essa classe de posse, agora podemos escrever Olá envio métodos de notificação dentro de saudação **NotificationHub** classe.</span><span class="sxs-lookup"><span data-stu-id="2557b-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="2557b-131">Olá acima métodos enviar um HTTP POST solicitação toohello /messages ponto de extremidade de hub de notificação, com corpo correto hello e notificação de saudação toosend cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="2557b-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="2557b-132"><a name="complete-tutorial"></a>Tutorial de saudação concluída</span><span class="sxs-lookup"><span data-stu-id="2557b-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="2557b-133">Agora você pode concluir o tutorial de Introdução hello, enviando a notificação de saudação de um back-end do PHP.</span><span class="sxs-lookup"><span data-stu-id="2557b-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="2557b-134">Inicialize o cliente de Hubs de notificação (substitua o nome de hub e de cadeia de caracteres de conexão Olá conforme instruído no hello [tutorial de Introdução Get]):</span><span class="sxs-lookup"><span data-stu-id="2557b-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="2557b-135">Adicione código de envio de saudação dependendo de sua plataforma móvel de destino.</span><span class="sxs-lookup"><span data-stu-id="2557b-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="2557b-136">Windows Store e Windows Phone 8.1 (não Silverlight)</span><span class="sxs-lookup"><span data-stu-id="2557b-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="2557b-137">iOS</span><span class="sxs-lookup"><span data-stu-id="2557b-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="2557b-138">Android</span><span class="sxs-lookup"><span data-stu-id="2557b-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="2557b-139">Silverlight para Windows Phone 8.0 e 8.1</span><span class="sxs-lookup"><span data-stu-id="2557b-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="2557b-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="2557b-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="2557b-141">Executar o código PHP agora deve produzir uma notificação que aparece no dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="2557b-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2557b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2557b-142">Next Steps</span></span>
<span data-ttu-id="2557b-143">Neste tópico, mostramos como toocreate um Java simple REST cliente Hubs de notificação.</span><span class="sxs-lookup"><span data-stu-id="2557b-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="2557b-144">A partir daqui, você pode:</span><span class="sxs-lookup"><span data-stu-id="2557b-144">From here you can:</span></span>

* <span data-ttu-id="2557b-145">Baixar Olá completo [exemplo de wrapper de PHP REST], que contém todos os códigos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="2557b-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="2557b-146">Saber mais sobre o recurso de indicação Olá [tutorial últimas notícias] de Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="2557b-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="2557b-147">Saiba mais sobre o envio por push usuários de tooindividual notificações [tutorial notificar usuários]</span><span class="sxs-lookup"><span data-stu-id="2557b-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="2557b-148">Para obter mais informações, consulte também Olá [Centro de desenvolvedores PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2557b-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[exemplo de wrapper de PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial de Introdução Get]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

