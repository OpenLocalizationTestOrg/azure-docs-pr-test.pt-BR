---
title: "aaaUnderstand segurança do Azure IoT Hub | Microsoft Docs"
description: "A guia do desenvolvedor - como toocontrol acessar tooIoT Hub para aplicativos de dispositivos e aplicativos de back-end. Inclui informações sobre tokens de segurança e suporte a certificados x. 509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Controlar acesso tooIoT Hub

Este artigo descreve as opções de saudação para proteger seu hub IoT. IoT Hub usa *permissões* ponto de extremidade do toogrant acesso tooeach IoT hub. Permissões de limitam hub Olá acesso tooan IoT baseada na funcionalidade.

Este artigo descreve:

* Olá diferentes permissões que você pode conceder tooa dispositivo ou aplicativo de back-end tooaccess seu hub IoT.
* Olá tokens de processo e hello de autenticação usa tooverify permissões.
* Como tooscope credenciais toospecific toolimit acessar os recursos.
* Suporte de Hub IoT para certificados X.509.
* Mecanismos de autenticação de dispositivo personalizados que usam registros de identidade de dispositivo existente ou esquemas de autenticação.

### <a name="when-toouse"></a>Quando toouse

Você deve ter permissões apropriadas tooaccess qualquer um dos pontos de extremidade de Hub IoT hello. Por exemplo, um dispositivo deve incluir um token que contém as credenciais de segurança junto com todas as mensagens que ele envia tooIoT Hub.

## <a name="access-control-and-permissions"></a>Controle e permissões de acesso

Você pode conceder [permissões](#iot-hub-permissions) no hello maneiras a seguir:

* **Políticas de acesso compartilhado no nível do Hub IoT**. As políticas de acesso compartilhado podem conceder qualquer combinação de [permissões](#iot-hub-permissions). Você pode definir políticas em Olá [portal do Azure][lnk-management-portal], ou programaticamente usando Olá [APIs REST de provedor de recursos do IoT Hub][lnk-resource-provider-apis]. Um hub IoT recém-criado tem Olá políticas padrão a seguir:

  * **iothubowner**: política com todas as permissões.
  * **service**: política com a permissão **ServiceConnect**.
  * **device**: política com a permissão **DeviceConnect**.
  * **registryRead**: política com a permissão **RegistryRead**.
  * **registryReadWrite**: política com as permissões **RegistryRead** e RegistryWrite.
  * **Credenciais de segurança de acordo com o dispositivo**. Cada Hub IoT contém um [registro de identidade do dispositivo][lnk-identity-registry]. Para cada dispositivo nesse registro de identidade, você pode configurar credenciais de segurança que concedam **DeviceConnect** as permissões no escopo toohello correspondente pontos de extremidade de dispositivo.

Por exemplo, em uma solução de IoT típica:

* usa o componente de gerenciamento de dispositivo Olá Olá *registryReadWrite* política.
* usa o componente de processador de evento Olá Olá *service* política.
* usa o componente de lógica de negócios de tempo de execução de dispositivo Olá Olá *service* política.
* Dispositivos individuais se conectar usando credenciais armazenadas no registro de identidade do hub do hello IoT.

> [!NOTE]
> Para obter informações detalhadas, consulte [permissões](#iot-hub-permissions).

## <a name="authentication"></a>Autenticação

IoT Hub do Azure concede acesso tooendpoints Verificando um token em relação a políticas de acesso compartilhada de saudação e credenciais de segurança de registro de identidade.

Credenciais de segurança, como chaves simétricas, nunca são enviadas pela transmissão de saudação.

> [!NOTE]
> Olá provedor de recursos do Azure IoT Hub é protegido por meio de sua assinatura do Azure, assim como todos os provedores de saudação [do Azure Resource Manager][lnk-azure-resource-manager].

Para obter mais informações sobre como tooconstruct e use tokens de segurança, consulte [tokens de segurança de IoT Hub][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Especificações de protocolo

Cada protocolo com suporte, como MQTT, AMQP e HTTP, transporta os tokens de maneiras diferentes.

Ao usar MQTT, pacote de conectar saudação tem Olá deviceId como Olá ClientId, {iothubhostname} / {deviceId} no campo de nome de usuário hello e um token SAS no campo de senha hello. {iothubhostname} deve ser Olá CName completa de hub IoT de saudação (por exemplo, contoso.azure-devices.net).

Quando usa [AMQP][lnk-amqp], o Hub IoT dá suporte ao [SASL PLAIN][lnk-sasl-plain] e à [Segurança baseada em declarações AMQP][lnk-cbs].

Se você usar AMQP declarações com base-segurança, Olá padrão especifica como tootransmit esses tokens.

Para SASL simples, Olá **username** pode ser:

* `{policyName}@sas.root.{iothubName}` se forem usados tokens de nível do Hub IoT.
* `{deviceId}@sas.{iothubname}` se forem usados tokens no escopo do dispositivo.

Em ambos os casos, o campo de senha Olá contém o token Olá, conforme descrito em [tokens de segurança de IoT Hub][lnk-sas-tokens].

HTTP implementa a autenticação, incluindo um token válido no hello **autorização** cabeçalho de solicitação.

#### <a name="example"></a>Exemplo

Nome de usuário (a DeviceId diferencia maiúsculas de minúsculas): `iothubname.azure-devices.net/DeviceId`

Senha (token de gerar SAS com hello [explorer dispositivo] [ lnk-device-explorer] ferramenta):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Olá [SDKs do Azure IoT] [ lnk-sdks] gerar tokens automaticamente ao conectar-se o serviço de toohello. Em alguns casos, Olá SDKs do Azure IoT não dão suporte a todos os protocolos de saudação ou todos os métodos de autenticação de saudação.

### <a name="special-considerations-for-sasl-plain"></a>Considerações especiais para SASL PLAIN

Ao usar SASL simples com AMQP, um cliente conectado tooan IoT hub pode usar um único token para cada conexão TCP. Quando Olá token expirar, Olá conexão TCP desconecta do serviço hello e dispara uma reconexão. Esse comportamento, enquanto não problemático para um aplicativo de back-end, é prejudiciais para um aplicativo de dispositivo para Olá motivos a seguir:

* Gateways normalmente se conectam em nome de vários dispositivos. Ao usar SASL simples, eles têm toocreate uma conexão TCP distinto para cada dispositivo conectado tooan IoT hub. Este cenário consideravelmente aumenta o consumo de energia e recursos de rede hello e aumenta a latência de saudação de cada conexão do dispositivo.
* Dispositivos com recursos limitados são afetados negativamente pelo uso de saudação maior de recursos tooreconnect após cada expiração do token.

## <a name="scope-iot-hub-level-credentials"></a>Escopo das credenciais no nível do Hub IoT

Você pode definir o escopo das políticas de segurança no nível do Hub IoT por meio da criação de tokens com um URI de recursos restrito. Por exemplo, mensagens de dispositivo para nuvem de toosend de ponto de extremidade de saudação de um dispositivo é **/devices/ {deviceId} / mensagens e eventos**. Você também pode usar uma política de acesso compartilhado de nível de hub IoT com **DeviceConnect** toosign permissões um token é cujo resourceURI **/devices/ {deviceId}**. Essa abordagem cria um token que só é utilizável toosend mensagens em nome do dispositivo **deviceId**.

Esse mecanismo é semelhante toohello [política de editor de Hubs de eventos][lnk-event-hubs-publisher-policy]e permite que você tooimplement métodos de autenticação personalizados.

## <a name="security-tokens"></a>Tokens de segurança

IoT Hub usa segurança tokens tooauthenticate dispositivos e serviços tooavoid enviar chaves percurso hello. Além disso, os tokens de segurança têm limite de escopo e de prazo de validade. Os [SDKs do IoT do Azure][lnk-sdks] geram tokens automaticamente sem precisar de configuração especial. Alguns cenários exigem que você toogenerate e usar os tokens de segurança diretamente. Esses cenários incluem:

* uso direto de saudação de superfícies de saudação MQTT, AMQP ou HTTP.
* Olá implementação padrão do serviço de token de hello, conforme explicado em [autenticação de dispositivo personalizada][lnk-custom-auth].

IoT Hub também permite que dispositivos tooauthenticate com o IoT Hub usando [certificados x. 509][lnk-x509].

### <a name="security-token-structure"></a>Estrutura do token de segurança

Você pode usar segurança tokens toogrant acesso limitado por tempo toodevices toospecific funcionalidade de serviços e no IoT Hub. tooget autorização tooconnect tooIoT Hub, dispositivos e serviços devem enviar tokens de segurança assinados com um acesso compartilhado ou uma chave simétrica. Essas chaves são armazenadas com uma identidade de dispositivo no registro de identidade hello.

Um token é assinado com uma acesso compartilhado chave concede acesso tooall Olá funcionalidades associadas com permissões de política de acesso compartilhada de saudação. Um token assinado com hello de concessões de única chave simétrica de uma identidade dispositivo **DeviceConnect** permissão Olá associados a identidade do dispositivo.

o token de segurança Olá tem Olá formato a seguir:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Aqui estão os valores esperados de saudação:

| Valor | Descrição |
| --- | --- |
| {signature} |Uma cadeia de caracteres de assinatura de HMAC-SHA256 de formulário Olá: `{URL-encoded-resourceURI} + "\n" + expiry`. **Importante**: chave Olá é decodificar da base64 e usado como chave tooperform computação de saudação HMAC-SHA256. |
| {resourceURI} |Prefixo URI (por segmento) dos pontos de extremidade de saudação que podem ser acessados com esse token, começando com o nome do host do hub IoT de saudação (nenhum protocolo). Por exemplo, `myHub.azure-devices.net/devices/device1` |
| {expiry} |Cadeias de caracteres UTF8 para número de segundos desde Olá época 00:00:00 UTC em 1 de janeiro de 1970. |
| {URL-encoded-resourceURI} |Quanto menor caso a codificação de URL Olá minúscula URI de recurso |
| {policyName} |nome de saudação do hello compartilhado toowhich de política de acesso, que esse token refere-se. Ausente se token Olá refere-se as credenciais de registro toodevice. |

**Observação no prefixo**: prefixo URI de saudação é calculado por segmento e não por caractere. Por exemplo, `/a/b` é um prefixo para `/a/b/c`, mas não para `/a/bc`.

Hello, Node. js trecho a seguir mostra uma função chamada **generateSasToken** calcula Olá token de entradas de saudação `resourceUri, signingKey, policyName, expiresInMins`. seções a seguir Olá detalham como tooinitialize Olá diferentes entradas de token diferente Olá casos de uso.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Como uma comparação, Olá equivalente toogenerate de código Python que é um token de segurança:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Desde que o prazo de validade de saudação do token de saudação é validado em máquinas de IoT Hub, Olá descompasso relógio Olá da máquina de saudação que gera um token de saudação deve ser mínimo.

### <a name="use-sas-tokens-in-a-device-app"></a>Usar tokens SAS em um aplicativo de dispositivo

Há tooobtain de duas maneiras **DeviceConnect** permissões com o IoT Hub com tokens de segurança: use um [chave simétrica de dispositivo de registro de identidade Olá](#use-a-symmetric-key-in-the-identity-registry), ou use um [dechavedeacessocompartilhado](#use-a-shared-access-policy).

Lembre-se que toda funcionalidade acessível por meio de dispositivos fica exposta por padrão em pontos de extremidade com o prefixo `/devices/{deviceId}`.

> [!IMPORTANT]
> Olá única de forma que o IoT Hub autentica um dispositivo específico está usando a chave simétrica de identidade de dispositivo de saudação. Em casos quando uma política de acesso compartilhado é usado tooaccess funcionalidade do dispositivo, solução de saudação deve considerar o componente Olá emitir o token de segurança hello como um subcomponente confiável.

pontos de extremidade do Hello voltados para o dispositivo são (independentemente do protocolo de saudação):

| Ponto de extremidade | Funcionalidade |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Enviar mensagens do dispositivo para a nuvem. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Receber mensagens da nuvem para o dispositivo. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Usar uma chave simétrica no registro de identidade Olá

Ao usar toogenerate um token de chave simétrica da identidade do dispositivo, Olá policyName (`skn`) elemento do token de saudação é omitido.

Por exemplo, um token criado tooaccess todas as funcionalidades do dispositivo deve ter Olá parâmetros a seguir:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* chave de assinatura: qualquer chave simétrica para Olá `{device id}` identidade,
* sem nome de política,
* qualquer data de validade

Um exemplo de uso Olá anterior Node. js função seria:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

resultado de saudação, que concede acesso tooall funcionalidade para device1, seria:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Ele é possível toogenerate um token SAS usando .NET Olá [Gerenciador de dispositivo] [ lnk-device-explorer] ferramenta ou Olá multiplataforma, com base no nó [Gerenciador de Hub IOT] [ lnk-iothub-explorer] utilitário de linha de comando.

### <a name="use-a-shared-access-policy"></a>Usar uma política de acesso compartilhado

Quando você cria um token de uma política de acesso compartilhado, defina Olá `skn` nome do campo toohello da política de saudação. Essa política deve conceder Olá **DeviceConnect** permissão.

Olá dois cenários principais para usar a funcionalidade do dispositivo de tooaccess de políticas de acesso compartilhado são:

* [gateways de protocolo em nuvem][lnk-endpoints],
* [Serviços de token] [ lnk-custom-auth] usado tooimplement esquemas de autenticação personalizada.

Desde Olá política de acesso compartilhado pode potencialmente conceder acesso tooconnect como qualquer dispositivo, é importante toouse Olá correto URI de recurso durante a criação de tokens de segurança. Essa configuração é especialmente importante para os serviços de token, que têm tooscope Olá token tooa dispositivo específico usando o URI do recurso hello. Esse ponto é menos relevante para os gateways de protocolo, pois eles já estão mediando o tráfego para todos os dispositivos.

Por exemplo, um serviço de token usando Olá criado previamente compartilhado política de acesso chamada **dispositivo** criaria um token com hello parâmetros a seguir:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* chave de assinatura: uma das chaves de saudação do hello `device` política,
* nome da política: `device`,
* qualquer data de validade

Um exemplo de uso Olá anterior Node. js função seria:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

resultado de saudação, que concede acesso tooall funcionalidade para device1, seria:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Um gateway de protocolo poderia usar Olá mesmo token para todos os dispositivos simplesmente definindo Olá URI de recurso muito`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Usar tokens de segurança de componentes de serviço

Componentes de serviço só podem gerar tokens de segurança usando políticas de acesso compartilhado conceder as permissões apropriadas Olá conforme explicado anteriormente.

Aqui está a funções de serviço Olá expostas em pontos de extremidade hello:

| Ponto de extremidade | Funcionalidade |
| --- | --- |
| `{iot hub host name}/devices` |Criar, atualizar, recuperar e excluir as identidades do dispositivo. |
| `{iot hub host name}/messages/events` |Receber mensagens do dispositivo para a nuvem. |
| `{iot hub host name}/servicebound/feedback` |Receber comentários das mensagens da nuvem para o dispositivo. |
| `{iot hub host name}/devicebound` |Enviar mensagens da nuvem para o dispositivo. |

Por exemplo, um serviço gerando usando Olá criado previamente compartilhado política de acesso chamada **registryRead** criaria um token com hello parâmetros a seguir:

* URI de recurso: `{IoT hub name}.azure-devices.net/devices`,
* chave de assinatura: uma das chaves de saudação do hello `registryRead` política,
* nome da política: `registryRead`,
* qualquer data de validade

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

resultado de saudação, que concede acesso tooread todas as identidades do dispositivo, seria:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Certificados X.509 com suporte

Você pode usar qualquer tooauthenticate de certificado x. 509 um dispositivo com o IoT Hub. Os certificados incluem:

* **Um certificado X.509 existente**. Talvez um dispositivo já tenha um certificado X.509 associado a ele. dispositivo Olá pode usar este certificado tooauthenticate com o IoT Hub.
* **Um certificado X-509 gerado automaticamente e autoassinado**. Um fabricante de dispositivo ou implantador internamente pode gerar esses certificados e armazenar chave privada correspondente hello (e certificado) no dispositivo de saudação. Você pode usar ferramentas como o [OpenSSL][lnk-openssl] e o utilitário [SelfSignedCertificate][lnk-selfsigned] do Windows para essa finalidade.
* **Certificado X.509 assinado por autoridade de certificação**. tooidentify um dispositivo e autenticá-lo com o IoT Hub, você pode usar um certificado x. 509 gerado e assinado por uma autoridade de certificação (CA). IoT Hub apenas verifica essa impressão digital de saudação apresentado coincide com a impressão digital de saudação configurada. Hub IOT não validar a cadeia de certificados de saudação.

Um dispositivo pode usar um certificado X.509 ou um token de segurança para autenticação, mas não ambos.

### <a name="register-an-x509-certificate-for-a-device"></a>Registrar um certificado X.509 para um dispositivo

Olá [SDK do serviço Azure IoT c#] [ lnk-service-sdk] (versão 1.0.8+) dá suporte ao registrar um dispositivo que usa um certificado x. 509 para autenticação. Outras APIs, como a importação/exportação de dispositivos também oferece suporte a certificados X.509.

### <a name="c-support"></a>Suporte a C\#

Olá **RegistryManager** classe fornece uma maneira programática tooregister um dispositivo. Em particular, Olá **AddDeviceAsync** e **UpdateDeviceAsync** métodos permitem que você tooregister e atualizar um dispositivo de saudação do registro de identidade de IoT Hub. Esses dois métodos têm uma instância **Dispositivo** como entrada. Olá **dispositivo** classe inclui um **autenticação** propriedade que permite que você toospecify primários e secundários x. 509 impressões digitais de certificado. impressão digital de saudação representa um hash SHA-1 do certificado x. 509 de saudação (armazenado usando a codificação binária do DER). Você tem a opção de saudação da especificação de uma impressão digital primária ou uma impressão digital secundária ou ambos. Impressões digitais primários e secundários são cenários de substituição do certificado toohandle com suporte.

> [!NOTE]
> IoT Hub não exige ou armazenar o certificado de x. 509 todo hello, somente impressão digital de saudação.

Aqui está um exemplo C\# um dispositivo usando um certificado x. 509 de tooregister de trecho de código:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Usar um certificado X.509 durante operações em tempo de execução

Olá [dispositivo IoT do Azure SDK para .NET] [ lnk-client-sdk] (versão 1.0.11+) dá suporte ao uso de saudação de certificados x. 509.

### <a name="c-support"></a>Suporte a C\#

Olá classe **DeviceAuthenticationWithX509Certificate** Olá de dá suporte à criação de **DeviceClient** instâncias usando um certificado x. 509. certificado x. 509 de saudação deve estar no formato PFX (também chamado de PKCS #12) Olá que inclui a chave privada hello.

Veja um trecho de código de exemplo:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Autenticação personalizada de dispositivo

Você pode usar o hello IoT Hub [registro identidade] [ lnk-identity-registry] usando de controle de acesso e credenciais de segurança de cada dispositivo tooconfigure [tokens] [ lnk-sas-tokens] . Se uma solução de IoT já tem um esquema de registro e/ou a autenticação de identidade personalizado, considere a criação de um *serviço de token* toointegrate essa infraestrutura com o IoT Hub. Dessa forma, você pode usar outros recursos de IoT em sua solução.

Um serviço de token é um serviço de nuvem personalizado. Ele usa um IoT Hub *política de acesso compartilhado* com **DeviceConnect** permissões toocreate *no escopo do dispositivo* tokens. Esses tokens habilitar um hub IoT de tooyour de tooconnect de dispositivo.

![Etapas do padrão do serviço de token de saudação][img-tokenservice]

Aqui estão as etapas principais de saudação do padrão do serviço de token de saudação:

1. Crie uma política de acesso compartilhado do Hub IoT com permissões **DeviceConnect** para seu Hub IoT. Você pode criar essa política em Olá [portal do Azure] [ lnk-management-portal] ou programaticamente. serviço de token de saudação usa esse tokens de saudação de toosign política cria.
1. Quando um dispositivo precisa tooaccess seu hub IoT, ele solicita um token assinado do serviço de token. dispositivo Olá pode autenticar sua identidade de dispositivo personalizado de identidade do registro/autenticação esquema toodetermine Olá que o serviço de token Olá usa o token de saudação de toocreate.
1. serviço de token de saudação retorna um token. Olá token é criado usando `/devices/{deviceId}` como `resourceURI`, com `deviceId` como dispositivo de saudação que está sendo autenticado. serviço de token de saudação usa o token de saudação do hello acesso compartilhado política tooconstruct.
1. dispositivo Olá usa o token de saudação diretamente com o hub IoT de saudação.

> [!NOTE]
> Você pode usar a classe do .NET Olá [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] ou Olá classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate um token no seu serviço de token.

serviço de token de saudação pode definir a expiração do token Olá conforme desejado. Quando Olá token expirar, hub IoT de saudação os servidores de conexão do dispositivo hello. Em seguida, Olá deve solicitar um novo token do serviço de token de saudação. Um tempo de expiração curto aumenta a carga de saudação em dispositivo hello e o serviço de token de saudação.

Para um hub de tooyour de tooconnect do dispositivo, você ainda deverá adicionar-toohello registro de identidade de IoT Hub — mesmo que o dispositivo hello está usando um token e não um tooconnect de chave do dispositivo. Portanto, você pode continuar o controle de acesso por dispositivo toouse habilitando ou desabilitando as identidades de dispositivo no hello [registro identidade][lnk-identity-registry]. Essa abordagem reduz os riscos de saudação do uso de tokens com tempos de expiração do tempo.

### <a name="comparison-with-a-custom-gateway"></a>Comparação com um gateway personalizado

padrão de serviço de token de saudação é Olá recomendada tooimplement de maneira um esquema de autenticação/registro identidade personalizada com o IoT Hub. Esse padrão é recomendado porque o IoT Hub continua toohandle a maior parte do tráfego de solução de saudação. No entanto, se o esquema de autenticação personalizado Olá é então entrelaçada com protocolo hello, você pode exigir um *gateway personalizado* tooprocess todos Olá tráfego. Um exemplo de tal cenário é usar [TLS (Transport Layer Security) e as PSKs (chaves pré-compartilhadas)][lnk-tls-psk]. Para obter mais informações, consulte Olá [gateway do protocolo] [ lnk-protocols] tópico.

## <a name="reference-topics"></a>Tópicos de referência:

Hello seguinte referência tópicos fornecem mais informações sobre o controle hub de IoT tooyour de acesso.

## <a name="iot-hub-permissions"></a>Permissões de Hub IoT

Olá tabela a seguir lista permissões de saudação, você pode usar o hub IoT do toocontrol acesso tooyour.

| Permissão | Observações |
| --- | --- |
| **RegistryRead** |Registro de identidade de toohello do concede acesso de leitura. Para saber mais, consulte [Registro de identidade][lnk-identity-registry]. <br/>Essa permissão é usada pelos serviços de nuvem de back-end. |
| **RegistryReadWrite** |Concede acesso de leitura e gravação toohello registro identidade. Para saber mais, consulte [Registro de identidade][lnk-identity-registry]. <br/>Essa permissão é usada pelos serviços de nuvem de back-end. |
| **ServiceConnect** |Concede acesso toocloud serviço voltado para a comunicação e os pontos de extremidade de monitoramento. <br/>Concede permissão tooreceive dispositivo para nuvem mensagens, enviar mensagens de nuvem para dispositivo e recuperar Olá correspondente confirmações de entrega. <br/>Carregamentos de confirmações de entrega de tooretrieve concede permissão para o arquivo. <br/>Concede permissão tooaccess dispositivo twins tooupdate marcas e propriedades desejadas, recuperar as propriedades relatadas e executar consultas. <br/>Essa permissão é usada pelos serviços de nuvem de back-end. |
| **DeviceConnect** |Concede acesso toodevice voltados para pontos de extremidade. <br/>Concede permissão toosend dispositivo para nuvem mensagens e receber mensagens de nuvem para dispositivo. <br/>Carregamento do arquivo concede permissão tooperform de um dispositivo. <br/>Concede permissão tooreceive dispositivo duas desejada propriedade notificações e macros relatadas propriedades de dispositivo de atualização. <br/>Arquivo de tooperform concede permissão carrega. <br/>Essa permissão é usada por dispositivos. |

## <a name="additional-reference-material"></a>Material de referência adicional

Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:

* [Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.
* [Limitação e cotas] [ lnk-quotas] descreve cotas hello e comportamentos que se aplicam a toohello serviço de IoT Hub de limitação.
* [SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.
* [Linguagem de consulta de IoT Hub] [ lnk-query] descreve a linguagem de consulta de saudação, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.
* [Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toocontrol acessar o IoT Hub, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:

* [Usar configurações e estado do dispositivo twins toosynchronize][lnk-devguide-device-twins]
* [Invocar um método direto em um dispositivo][lnk-devguide-directmethods]
* [Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]

Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá tutoriais de IoT Hub a seguir:

* [Introdução ao Hub IoT do Azure][lnk-getstarted-tutorial]
* [Como a nuvem para dispositivo toosend mensagens com o IoT Hub][lnk-c2d-tutorial]
* [Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
