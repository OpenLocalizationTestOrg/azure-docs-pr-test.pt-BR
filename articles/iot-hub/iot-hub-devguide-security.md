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
# <a name="control-access-tooiot-hub"></a><span data-ttu-id="e3b7f-104">Controlar acesso tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="e3b7f-104">Control access tooIoT Hub</span></span>

<span data-ttu-id="e3b7f-105">Este artigo descreve as opções de saudação para proteger seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-105">This article describes hello options for securing your IoT hub.</span></span> <span data-ttu-id="e3b7f-106">IoT Hub usa *permissões* ponto de extremidade do toogrant acesso tooeach IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-106">IoT Hub uses *permissions* toogrant access tooeach IoT hub endpoint.</span></span> <span data-ttu-id="e3b7f-107">Permissões de limitam hub Olá acesso tooan IoT baseada na funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-107">Permissions limit hello access tooan IoT hub based on functionality.</span></span>

<span data-ttu-id="e3b7f-108">Este artigo descreve:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-108">This article describes:</span></span>

* <span data-ttu-id="e3b7f-109">Olá diferentes permissões que você pode conceder tooa dispositivo ou aplicativo de back-end tooaccess seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-109">hello different permissions that you can grant tooa device or back-end app tooaccess your IoT hub.</span></span>
* <span data-ttu-id="e3b7f-110">Olá tokens de processo e hello de autenticação usa tooverify permissões.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-110">hello authentication process and hello tokens it uses tooverify permissions.</span></span>
* <span data-ttu-id="e3b7f-111">Como tooscope credenciais toospecific toolimit acessar os recursos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-111">How tooscope credentials toolimit access toospecific resources.</span></span>
* <span data-ttu-id="e3b7f-112">Suporte de Hub IoT para certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="e3b7f-113">Mecanismos de autenticação de dispositivo personalizados que usam registros de identidade de dispositivo existente ou esquemas de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="e3b7f-114">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="e3b7f-114">When toouse</span></span>

<span data-ttu-id="e3b7f-115">Você deve ter permissões apropriadas tooaccess qualquer um dos pontos de extremidade de Hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-115">You must have appropriate permissions tooaccess any of hello IoT Hub endpoints.</span></span> <span data-ttu-id="e3b7f-116">Por exemplo, um dispositivo deve incluir um token que contém as credenciais de segurança junto com todas as mensagens que ele envia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-116">For example, a device must include a token containing security credentials along with every message it sends tooIoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="e3b7f-117">Controle e permissões de acesso</span><span class="sxs-lookup"><span data-stu-id="e3b7f-117">Access control and permissions</span></span>

<span data-ttu-id="e3b7f-118">Você pode conceder [permissões](#iot-hub-permissions) no hello maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-118">You can grant [permissions](#iot-hub-permissions) in hello following ways:</span></span>

* <span data-ttu-id="e3b7f-119">**Políticas de acesso compartilhado no nível do Hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="e3b7f-120">As políticas de acesso compartilhado podem conceder qualquer combinação de [permissões](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="e3b7f-121">Você pode definir políticas em Olá [portal do Azure][lnk-management-portal], ou programaticamente usando Olá [APIs REST de provedor de recursos do IoT Hub][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-121">You can define policies in hello [Azure portal][lnk-management-portal], or programmatically by using hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="e3b7f-122">Um hub IoT recém-criado tem Olá políticas padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-122">A newly created IoT hub has hello following default policies:</span></span>

  * <span data-ttu-id="e3b7f-123">**iothubowner**: política com todas as permissões.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="e3b7f-124">**service**: política com a permissão **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="e3b7f-125">**device**: política com a permissão **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="e3b7f-126">**registryRead**: política com a permissão **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="e3b7f-127">**registryReadWrite**: política com as permissões **RegistryRead** e RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="e3b7f-128">**Credenciais de segurança de acordo com o dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-128">**Per-device security credentials**.</span></span> <span data-ttu-id="e3b7f-129">Cada Hub IoT contém um [registro de identidade do dispositivo][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="e3b7f-130">Para cada dispositivo nesse registro de identidade, você pode configurar credenciais de segurança que concedam **DeviceConnect** as permissões no escopo toohello correspondente pontos de extremidade de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped toohello corresponding device endpoints.</span></span>

<span data-ttu-id="e3b7f-131">Por exemplo, em uma solução de IoT típica:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="e3b7f-132">usa o componente de gerenciamento de dispositivo Olá Olá *registryReadWrite* política.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-132">hello device management component uses hello *registryReadWrite* policy.</span></span>
* <span data-ttu-id="e3b7f-133">usa o componente de processador de evento Olá Olá *service* política.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-133">hello event processor component uses hello *service* policy.</span></span>
* <span data-ttu-id="e3b7f-134">usa o componente de lógica de negócios de tempo de execução de dispositivo Olá Olá *service* política.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-134">hello run-time device business logic component uses hello *service* policy.</span></span>
* <span data-ttu-id="e3b7f-135">Dispositivos individuais se conectar usando credenciais armazenadas no registro de identidade do hub do hello IoT.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-135">Individual devices connect using credentials stored in hello IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="e3b7f-136">Para obter informações detalhadas, consulte [permissões](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="e3b7f-137">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e3b7f-137">Authentication</span></span>

<span data-ttu-id="e3b7f-138">IoT Hub do Azure concede acesso tooendpoints Verificando um token em relação a políticas de acesso compartilhada de saudação e credenciais de segurança de registro de identidade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-138">Azure IoT Hub grants access tooendpoints by verifying a token against hello shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="e3b7f-139">Credenciais de segurança, como chaves simétricas, nunca são enviadas pela transmissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-139">Security credentials, such as symmetric keys, are never sent over hello wire.</span></span>

> [!NOTE]
> <span data-ttu-id="e3b7f-140">Olá provedor de recursos do Azure IoT Hub é protegido por meio de sua assinatura do Azure, assim como todos os provedores de saudação [do Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-140">hello Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in hello [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="e3b7f-141">Para obter mais informações sobre como tooconstruct e use tokens de segurança, consulte [tokens de segurança de IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-141">For more information about how tooconstruct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="e3b7f-142">Especificações de protocolo</span><span class="sxs-lookup"><span data-stu-id="e3b7f-142">Protocol specifics</span></span>

<span data-ttu-id="e3b7f-143">Cada protocolo com suporte, como MQTT, AMQP e HTTP, transporta os tokens de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="e3b7f-144">Ao usar MQTT, pacote de conectar saudação tem Olá deviceId como Olá ClientId, {iothubhostname} / {deviceId} no campo de nome de usuário hello e um token SAS no campo de senha hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-144">When using MQTT, hello CONNECT packet has hello deviceId as hello ClientId, {iothubhostname}/{deviceId} in hello Username field, and a SAS token in hello Password field.</span></span> <span data-ttu-id="e3b7f-145">{iothubhostname} deve ser Olá CName completa de hub IoT de saudação (por exemplo, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-145">{iothubhostname} should be hello full CName of hello IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="e3b7f-146">Quando usa [AMQP][lnk-amqp], o Hub IoT dá suporte ao [SASL PLAIN][lnk-sasl-plain] e à [Segurança baseada em declarações AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="e3b7f-147">Se você usar AMQP declarações com base-segurança, Olá padrão especifica como tootransmit esses tokens.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-147">If you use AMQP claims-based-security, hello standard specifies how tootransmit these tokens.</span></span>

<span data-ttu-id="e3b7f-148">Para SASL simples, Olá **username** pode ser:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-148">For SASL PLAIN, hello **username** can be:</span></span>

* <span data-ttu-id="e3b7f-149">`{policyName}@sas.root.{iothubName}` se forem usados tokens de nível do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="e3b7f-150">`{deviceId}@sas.{iothubname}` se forem usados tokens no escopo do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="e3b7f-151">Em ambos os casos, o campo de senha Olá contém o token Olá, conforme descrito em [tokens de segurança de IoT Hub][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-151">In both cases, hello password field contains hello token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="e3b7f-152">HTTP implementa a autenticação, incluindo um token válido no hello **autorização** cabeçalho de solicitação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-152">HTTP implements authentication by including a valid token in hello **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="e3b7f-153">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e3b7f-153">Example</span></span>

<span data-ttu-id="e3b7f-154">Nome de usuário (a DeviceId diferencia maiúsculas de minúsculas): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="e3b7f-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="e3b7f-155">Senha (token de gerar SAS com hello [explorer dispositivo] [ lnk-device-explorer] ferramenta):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="e3b7f-155">Password (Generate SAS token with hello [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="e3b7f-156">Olá [SDKs do Azure IoT] [ lnk-sdks] gerar tokens automaticamente ao conectar-se o serviço de toohello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-156">hello [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting toohello service.</span></span> <span data-ttu-id="e3b7f-157">Em alguns casos, Olá SDKs do Azure IoT não dão suporte a todos os protocolos de saudação ou todos os métodos de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-157">In some cases, hello Azure IoT SDKs do not support all hello protocols or all hello authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="e3b7f-158">Considerações especiais para SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="e3b7f-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="e3b7f-159">Ao usar SASL simples com AMQP, um cliente conectado tooan IoT hub pode usar um único token para cada conexão TCP.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-159">When using SASL PLAIN with AMQP, a client connecting tooan IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="e3b7f-160">Quando Olá token expirar, Olá conexão TCP desconecta do serviço hello e dispara uma reconexão.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-160">When hello token expires, hello TCP connection disconnects from hello service and triggers a reconnect.</span></span> <span data-ttu-id="e3b7f-161">Esse comportamento, enquanto não problemático para um aplicativo de back-end, é prejudiciais para um aplicativo de dispositivo para Olá motivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-161">This behavior, while not problematic for a back-end app, is damaging for a device app for hello following reasons:</span></span>

* <span data-ttu-id="e3b7f-162">Gateways normalmente se conectam em nome de vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="e3b7f-163">Ao usar SASL simples, eles têm toocreate uma conexão TCP distinto para cada dispositivo conectado tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-163">When using SASL PLAIN, they have toocreate a distinct TCP connection for each device connecting tooan IoT hub.</span></span> <span data-ttu-id="e3b7f-164">Este cenário consideravelmente aumenta o consumo de energia e recursos de rede hello e aumenta a latência de saudação de cada conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-164">This scenario considerably increases hello consumption of power and networking resources, and increases hello latency of each device connection.</span></span>
* <span data-ttu-id="e3b7f-165">Dispositivos com recursos limitados são afetados negativamente pelo uso de saudação maior de recursos tooreconnect após cada expiração do token.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-165">Resource-constrained devices are adversely affected by hello increased use of resources tooreconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="e3b7f-166">Escopo das credenciais no nível do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e3b7f-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="e3b7f-167">Você pode definir o escopo das políticas de segurança no nível do Hub IoT por meio da criação de tokens com um URI de recursos restrito.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="e3b7f-168">Por exemplo, mensagens de dispositivo para nuvem de toosend de ponto de extremidade de saudação de um dispositivo é **/devices/ {deviceId} / mensagens e eventos**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-168">For example, hello endpoint toosend device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="e3b7f-169">Você também pode usar uma política de acesso compartilhado de nível de hub IoT com **DeviceConnect** toosign permissões um token é cujo resourceURI **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions toosign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="e3b7f-170">Essa abordagem cria um token que só é utilizável toosend mensagens em nome do dispositivo **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-170">This approach creates a token that is only usable toosend messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="e3b7f-171">Esse mecanismo é semelhante toohello [política de editor de Hubs de eventos][lnk-event-hubs-publisher-policy]e permite que você tooimplement métodos de autenticação personalizados.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-171">This mechanism is similar toohello [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you tooimplement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="e3b7f-172">Tokens de segurança</span><span class="sxs-lookup"><span data-stu-id="e3b7f-172">Security tokens</span></span>

<span data-ttu-id="e3b7f-173">IoT Hub usa segurança tokens tooauthenticate dispositivos e serviços tooavoid enviar chaves percurso hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-173">IoT Hub uses security tokens tooauthenticate devices and services tooavoid sending keys on hello wire.</span></span> <span data-ttu-id="e3b7f-174">Além disso, os tokens de segurança têm limite de escopo e de prazo de validade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="e3b7f-175">Os [SDKs do IoT do Azure][lnk-sdks] geram tokens automaticamente sem precisar de configuração especial.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="e3b7f-176">Alguns cenários exigem que você toogenerate e usar os tokens de segurança diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-176">Some scenarios do require you toogenerate and use security tokens directly.</span></span> <span data-ttu-id="e3b7f-177">Esses cenários incluem:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-177">Such scenarios include:</span></span>

* <span data-ttu-id="e3b7f-178">uso direto de saudação de superfícies de saudação MQTT, AMQP ou HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-178">hello direct use of hello MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="e3b7f-179">Olá implementação padrão do serviço de token de hello, conforme explicado em [autenticação de dispositivo personalizada][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-179">hello implementation of hello token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="e3b7f-180">IoT Hub também permite que dispositivos tooauthenticate com o IoT Hub usando [certificados x. 509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-180">IoT Hub also allows devices tooauthenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="e3b7f-181">Estrutura do token de segurança</span><span class="sxs-lookup"><span data-stu-id="e3b7f-181">Security token structure</span></span>

<span data-ttu-id="e3b7f-182">Você pode usar segurança tokens toogrant acesso limitado por tempo toodevices toospecific funcionalidade de serviços e no IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-182">You use security tokens toogrant time-bounded access toodevices and services toospecific functionality in IoT Hub.</span></span> <span data-ttu-id="e3b7f-183">tooget autorização tooconnect tooIoT Hub, dispositivos e serviços devem enviar tokens de segurança assinados com um acesso compartilhado ou uma chave simétrica.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-183">tooget authorization tooconnect tooIoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="e3b7f-184">Essas chaves são armazenadas com uma identidade de dispositivo no registro de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-184">These keys are stored with a device identity in hello identity registry.</span></span>

<span data-ttu-id="e3b7f-185">Um token é assinado com uma acesso compartilhado chave concede acesso tooall Olá funcionalidades associadas com permissões de política de acesso compartilhada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-185">A token signed with a shared access key grants access tooall hello functionality associated with hello shared access policy permissions.</span></span> <span data-ttu-id="e3b7f-186">Um token assinado com hello de concessões de única chave simétrica de uma identidade dispositivo **DeviceConnect** permissão Olá associados a identidade do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-186">A token signed with a device identity's symmetric key only grants hello **DeviceConnect** permission for hello associated device identity.</span></span>

<span data-ttu-id="e3b7f-187">o token de segurança Olá tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-187">hello security token has hello following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="e3b7f-188">Aqui estão os valores esperados de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-188">Here are hello expected values:</span></span>

| <span data-ttu-id="e3b7f-189">Valor</span><span class="sxs-lookup"><span data-stu-id="e3b7f-189">Value</span></span> | <span data-ttu-id="e3b7f-190">Descrição</span><span class="sxs-lookup"><span data-stu-id="e3b7f-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3b7f-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="e3b7f-191">{signature}</span></span> |<span data-ttu-id="e3b7f-192">Uma cadeia de caracteres de assinatura de HMAC-SHA256 de formulário Olá: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-192">An HMAC-SHA256 signature string of hello form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="e3b7f-193">**Importante**: chave Olá é decodificar da base64 e usado como chave tooperform computação de saudação HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-193">**Important**: hello key is decoded from base64 and used as key tooperform hello HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="e3b7f-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="e3b7f-194">{resourceURI}</span></span> |<span data-ttu-id="e3b7f-195">Prefixo URI (por segmento) dos pontos de extremidade de saudação que podem ser acessados com esse token, começando com o nome do host do hub IoT de saudação (nenhum protocolo).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-195">URI prefix (by segment) of hello endpoints that can be accessed with this token, starting with host name of hello IoT hub (no protocol).</span></span> <span data-ttu-id="e3b7f-196">Por exemplo, `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="e3b7f-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="e3b7f-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="e3b7f-197">{expiry}</span></span> |<span data-ttu-id="e3b7f-198">Cadeias de caracteres UTF8 para número de segundos desde Olá época 00:00:00 UTC em 1 de janeiro de 1970.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-198">UTF8 strings for number of seconds since hello epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="e3b7f-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="e3b7f-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="e3b7f-200">Quanto menor caso a codificação de URL Olá minúscula URI de recurso</span><span class="sxs-lookup"><span data-stu-id="e3b7f-200">Lower case URL-encoding of hello lower case resource URI</span></span> |
| <span data-ttu-id="e3b7f-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="e3b7f-201">{policyName}</span></span> |<span data-ttu-id="e3b7f-202">nome de saudação do hello compartilhado toowhich de política de acesso, que esse token refere-se.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-202">hello name of hello shared access policy toowhich this token refers.</span></span> <span data-ttu-id="e3b7f-203">Ausente se token Olá refere-se as credenciais de registro toodevice.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-203">Absent if hello token refers toodevice-registry credentials.</span></span> |

<span data-ttu-id="e3b7f-204">**Observação no prefixo**: prefixo URI de saudação é calculado por segmento e não por caractere.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-204">**Note on prefix**: hello URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="e3b7f-205">Por exemplo, `/a/b` é um prefixo para `/a/b/c`, mas não para `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="e3b7f-206">Hello, Node. js trecho a seguir mostra uma função chamada **generateSasToken** calcula Olá token de entradas de saudação `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-206">hello following Node.js snippet shows a function called **generateSasToken** that computes hello token from hello inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="e3b7f-207">seções a seguir Olá detalham como tooinitialize Olá diferentes entradas de token diferente Olá casos de uso.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-207">hello next sections detail how tooinitialize hello different inputs for hello different token use cases.</span></span>

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

<span data-ttu-id="e3b7f-208">Como uma comparação, Olá equivalente toogenerate de código Python que é um token de segurança:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-208">As a comparison, hello equivalent Python code toogenerate a security token is:</span></span>

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
> <span data-ttu-id="e3b7f-209">Desde que o prazo de validade de saudação do token de saudação é validado em máquinas de IoT Hub, Olá descompasso relógio Olá da máquina de saudação que gera um token de saudação deve ser mínimo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-209">Since hello time validity of hello token is validated on IoT Hub machines, hello drift on hello clock of hello machine that generates hello token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="e3b7f-210">Usar tokens SAS em um aplicativo de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e3b7f-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="e3b7f-211">Há tooobtain de duas maneiras **DeviceConnect** permissões com o IoT Hub com tokens de segurança: use um [chave simétrica de dispositivo de registro de identidade Olá](#use-a-symmetric-key-in-the-identity-registry), ou use um [dechavedeacessocompartilhado](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-211">There are two ways tooobtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from hello identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="e3b7f-212">Lembre-se que toda funcionalidade acessível por meio de dispositivos fica exposta por padrão em pontos de extremidade com o prefixo `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3b7f-213">Olá única de forma que o IoT Hub autentica um dispositivo específico está usando a chave simétrica de identidade de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-213">hello only way that IoT Hub authenticates a specific device is using hello device identity symmetric key.</span></span> <span data-ttu-id="e3b7f-214">Em casos quando uma política de acesso compartilhado é usado tooaccess funcionalidade do dispositivo, solução de saudação deve considerar o componente Olá emitir o token de segurança hello como um subcomponente confiável.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-214">In cases when a shared access policy is used tooaccess device functionality, hello solution must consider hello component issuing hello security token as a trusted subcomponent.</span></span>

<span data-ttu-id="e3b7f-215">pontos de extremidade do Hello voltados para o dispositivo são (independentemente do protocolo de saudação):</span><span class="sxs-lookup"><span data-stu-id="e3b7f-215">hello device-facing endpoints are (irrespective of hello protocol):</span></span>

| <span data-ttu-id="e3b7f-216">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-216">Endpoint</span></span> | <span data-ttu-id="e3b7f-217">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="e3b7f-218">Enviar mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="e3b7f-219">Receber mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a><span data-ttu-id="e3b7f-220">Usar uma chave simétrica no registro de identidade Olá</span><span class="sxs-lookup"><span data-stu-id="e3b7f-220">Use a symmetric key in hello identity registry</span></span>

<span data-ttu-id="e3b7f-221">Ao usar toogenerate um token de chave simétrica da identidade do dispositivo, Olá policyName (`skn`) elemento do token de saudação é omitido.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-221">When using a device identity's symmetric key toogenerate a token, hello policyName (`skn`) element of hello token is omitted.</span></span>

<span data-ttu-id="e3b7f-222">Por exemplo, um token criado tooaccess todas as funcionalidades do dispositivo deve ter Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-222">For example, a token created tooaccess all device functionality should have hello following parameters:</span></span>

* <span data-ttu-id="e3b7f-223">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="e3b7f-224">chave de assinatura: qualquer chave simétrica para Olá `{device id}` identidade,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-224">signing key: any symmetric key for hello `{device id}` identity,</span></span>
* <span data-ttu-id="e3b7f-225">sem nome de política,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-225">no policy name,</span></span>
* <span data-ttu-id="e3b7f-226">qualquer data de validade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-226">any expiration time.</span></span>

<span data-ttu-id="e3b7f-227">Um exemplo de uso Olá anterior Node. js função seria:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-227">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="e3b7f-228">resultado de saudação, que concede acesso tooall funcionalidade para device1, seria:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-228">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="e3b7f-229">Ele é possível toogenerate um token SAS usando .NET Olá [Gerenciador de dispositivo] [ lnk-device-explorer] ferramenta ou Olá multiplataforma, com base no nó [Gerenciador de Hub IOT] [ lnk-iothub-explorer] utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-229">It is possible toogenerate a SAS token using hello .NET [device explorer][lnk-device-explorer] tool or hello cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="e3b7f-230">Usar uma política de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="e3b7f-230">Use a shared access policy</span></span>

<span data-ttu-id="e3b7f-231">Quando você cria um token de uma política de acesso compartilhado, defina Olá `skn` nome do campo toohello da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-231">When you create a token from a shared access policy, set hello `skn` field toohello name of hello policy.</span></span> <span data-ttu-id="e3b7f-232">Essa política deve conceder Olá **DeviceConnect** permissão.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-232">This policy must grant hello **DeviceConnect** permission.</span></span>

<span data-ttu-id="e3b7f-233">Olá dois cenários principais para usar a funcionalidade do dispositivo de tooaccess de políticas de acesso compartilhado são:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-233">hello two main scenarios for using shared access policies tooaccess device functionality are:</span></span>

* <span data-ttu-id="e3b7f-234">[gateways de protocolo em nuvem][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="e3b7f-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="e3b7f-235">[Serviços de token] [ lnk-custom-auth] usado tooimplement esquemas de autenticação personalizada.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-235">[token services][lnk-custom-auth] used tooimplement custom authentication schemes.</span></span>

<span data-ttu-id="e3b7f-236">Desde Olá política de acesso compartilhado pode potencialmente conceder acesso tooconnect como qualquer dispositivo, é importante toouse Olá correto URI de recurso durante a criação de tokens de segurança.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-236">Since hello shared access policy can potentially grant access tooconnect as any device, it is important toouse hello correct resource URI when creating security tokens.</span></span> <span data-ttu-id="e3b7f-237">Essa configuração é especialmente importante para os serviços de token, que têm tooscope Olá token tooa dispositivo específico usando o URI do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-237">This setting is especially important for token services, which have tooscope hello token tooa specific device using hello resource URI.</span></span> <span data-ttu-id="e3b7f-238">Esse ponto é menos relevante para os gateways de protocolo, pois eles já estão mediando o tráfego para todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="e3b7f-239">Por exemplo, um serviço de token usando Olá criado previamente compartilhado política de acesso chamada **dispositivo** criaria um token com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-239">As an example, a token service using hello pre-created shared access policy called **device** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="e3b7f-240">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="e3b7f-241">chave de assinatura: uma das chaves de saudação do hello `device` política,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-241">signing key: one of hello keys of hello `device` policy,</span></span>
* <span data-ttu-id="e3b7f-242">nome da política: `device`,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-242">policy name: `device`,</span></span>
* <span data-ttu-id="e3b7f-243">qualquer data de validade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-243">any expiration time.</span></span>

<span data-ttu-id="e3b7f-244">Um exemplo de uso Olá anterior Node. js função seria:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-244">An example using hello preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="e3b7f-245">resultado de saudação, que concede acesso tooall funcionalidade para device1, seria:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-245">hello result, which grants access tooall functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="e3b7f-246">Um gateway de protocolo poderia usar Olá mesmo token para todos os dispositivos simplesmente definindo Olá URI de recurso muito`myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-246">A protocol gateway could use hello same token for all devices simply setting hello resource URI too`myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="e3b7f-247">Usar tokens de segurança de componentes de serviço</span><span class="sxs-lookup"><span data-stu-id="e3b7f-247">Use security tokens from service components</span></span>

<span data-ttu-id="e3b7f-248">Componentes de serviço só podem gerar tokens de segurança usando políticas de acesso compartilhado conceder as permissões apropriadas Olá conforme explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-248">Service components can only generate security tokens using shared access policies granting hello appropriate permissions as explained previously.</span></span>

<span data-ttu-id="e3b7f-249">Aqui está a funções de serviço Olá expostas em pontos de extremidade hello:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-249">Here is hello service functions exposed on hello endpoints:</span></span>

| <span data-ttu-id="e3b7f-250">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-250">Endpoint</span></span> | <span data-ttu-id="e3b7f-251">Funcionalidade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="e3b7f-252">Criar, atualizar, recuperar e excluir as identidades do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="e3b7f-253">Receber mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="e3b7f-254">Receber comentários das mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="e3b7f-255">Enviar mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="e3b7f-256">Por exemplo, um serviço gerando usando Olá criado previamente compartilhado política de acesso chamada **registryRead** criaria um token com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-256">As an example, a service generating using hello pre-created shared access policy called **registryRead** would create a token with hello following parameters:</span></span>

* <span data-ttu-id="e3b7f-257">URI de recurso: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="e3b7f-258">chave de assinatura: uma das chaves de saudação do hello `registryRead` política,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-258">signing key: one of hello keys of hello `registryRead` policy,</span></span>
* <span data-ttu-id="e3b7f-259">nome da política: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="e3b7f-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="e3b7f-260">qualquer data de validade</span><span class="sxs-lookup"><span data-stu-id="e3b7f-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="e3b7f-261">resultado de saudação, que concede acesso tooread todas as identidades do dispositivo, seria:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-261">hello result, which would grant access tooread all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="e3b7f-262">Certificados X.509 com suporte</span><span class="sxs-lookup"><span data-stu-id="e3b7f-262">Supported X.509 certificates</span></span>

<span data-ttu-id="e3b7f-263">Você pode usar qualquer tooauthenticate de certificado x. 509 um dispositivo com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-263">You can use any X.509 certificate tooauthenticate a device with IoT Hub.</span></span> <span data-ttu-id="e3b7f-264">Os certificados incluem:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-264">Certificates include:</span></span>

* <span data-ttu-id="e3b7f-265">**Um certificado X.509 existente**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="e3b7f-266">Talvez um dispositivo já tenha um certificado X.509 associado a ele.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="e3b7f-267">dispositivo Olá pode usar este certificado tooauthenticate com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-267">hello device can use this certificate tooauthenticate with IoT Hub.</span></span>
* <span data-ttu-id="e3b7f-268">**Um certificado X-509 gerado automaticamente e autoassinado**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="e3b7f-269">Um fabricante de dispositivo ou implantador internamente pode gerar esses certificados e armazenar chave privada correspondente hello (e certificado) no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-269">A device manufacturer or in-house deployer can generate these certificates and store hello corresponding private key (and certificate) on hello device.</span></span> <span data-ttu-id="e3b7f-270">Você pode usar ferramentas como o [OpenSSL][lnk-openssl] e o utilitário [SelfSignedCertificate][lnk-selfsigned] do Windows para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="e3b7f-271">**Certificado X.509 assinado por autoridade de certificação**.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="e3b7f-272">tooidentify um dispositivo e autenticá-lo com o IoT Hub, você pode usar um certificado x. 509 gerado e assinado por uma autoridade de certificação (CA).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-272">tooidentify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="e3b7f-273">IoT Hub apenas verifica essa impressão digital de saudação apresentado coincide com a impressão digital de saudação configurada.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-273">IoT Hub only verifies that hello thumbprint presented matches hello configured thumbprint.</span></span> <span data-ttu-id="e3b7f-274">Hub IOT não validar a cadeia de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-274">IotHub does not validate hello certificate chain.</span></span>

<span data-ttu-id="e3b7f-275">Um dispositivo pode usar um certificado X.509 ou um token de segurança para autenticação, mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="e3b7f-276">Registrar um certificado X.509 para um dispositivo</span><span class="sxs-lookup"><span data-stu-id="e3b7f-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="e3b7f-277">Olá [SDK do serviço Azure IoT c#] [ lnk-service-sdk] (versão 1.0.8+) dá suporte ao registrar um dispositivo que usa um certificado x. 509 para autenticação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-277">hello [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="e3b7f-278">Outras APIs, como a importação/exportação de dispositivos também oferece suporte a certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="e3b7f-279">Suporte a C\#</span><span class="sxs-lookup"><span data-stu-id="e3b7f-279">C\# Support</span></span>

<span data-ttu-id="e3b7f-280">Olá **RegistryManager** classe fornece uma maneira programática tooregister um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-280">hello **RegistryManager** class provides a programmatic way tooregister a device.</span></span> <span data-ttu-id="e3b7f-281">Em particular, Olá **AddDeviceAsync** e **UpdateDeviceAsync** métodos permitem que você tooregister e atualizar um dispositivo de saudação do registro de identidade de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-281">In particular, hello **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you tooregister and update a device in hello IoT Hub identity registry.</span></span> <span data-ttu-id="e3b7f-282">Esses dois métodos têm uma instância **Dispositivo** como entrada.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="e3b7f-283">Olá **dispositivo** classe inclui um **autenticação** propriedade que permite que você toospecify primários e secundários x. 509 impressões digitais de certificado.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-283">hello **Device** class includes an **Authentication** property that allows you toospecify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="e3b7f-284">impressão digital de saudação representa um hash SHA-1 do certificado x. 509 de saudação (armazenado usando a codificação binária do DER).</span><span class="sxs-lookup"><span data-stu-id="e3b7f-284">hello thumbprint represents a SHA-1 hash of hello X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="e3b7f-285">Você tem a opção de saudação da especificação de uma impressão digital primária ou uma impressão digital secundária ou ambos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-285">You have hello option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="e3b7f-286">Impressões digitais primários e secundários são cenários de substituição do certificado toohandle com suporte.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-286">Primary and secondary thumbprints are supported toohandle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="e3b7f-287">IoT Hub não exige ou armazenar o certificado de x. 509 todo hello, somente impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-287">IoT Hub does not require or store hello entire X.509 certificate, only hello thumbprint.</span></span>

<span data-ttu-id="e3b7f-288">Aqui está um exemplo C\# um dispositivo usando um certificado x. 509 de tooregister de trecho de código:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-288">Here is a sample C\# code snippet tooregister a device using an X.509 certificate:</span></span>

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="e3b7f-289">Usar um certificado X.509 durante operações em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="e3b7f-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="e3b7f-290">Olá [dispositivo IoT do Azure SDK para .NET] [ lnk-client-sdk] (versão 1.0.11+) dá suporte ao uso de saudação de certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-290">hello [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports hello use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="e3b7f-291">Suporte a C\#</span><span class="sxs-lookup"><span data-stu-id="e3b7f-291">C\# Support</span></span>

<span data-ttu-id="e3b7f-292">Olá classe **DeviceAuthenticationWithX509Certificate** Olá de dá suporte à criação de **DeviceClient** instâncias usando um certificado x. 509.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-292">hello class **DeviceAuthenticationWithX509Certificate** supports hello creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="e3b7f-293">certificado x. 509 de saudação deve estar no formato PFX (também chamado de PKCS #12) Olá que inclui a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-293">hello X.509 certificate must be in hello PFX (also called PKCS #12) format that includes hello private key.</span></span>

<span data-ttu-id="e3b7f-294">Veja um trecho de código de exemplo:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="e3b7f-295">Autenticação personalizada de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e3b7f-295">Custom device authentication</span></span>

<span data-ttu-id="e3b7f-296">Você pode usar o hello IoT Hub [registro identidade] [ lnk-identity-registry] usando de controle de acesso e credenciais de segurança de cada dispositivo tooconfigure [tokens] [ lnk-sas-tokens] .</span><span class="sxs-lookup"><span data-stu-id="e3b7f-296">You can use hello IoT Hub [identity registry][lnk-identity-registry] tooconfigure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="e3b7f-297">Se uma solução de IoT já tem um esquema de registro e/ou a autenticação de identidade personalizado, considere a criação de um *serviço de token* toointegrate essa infraestrutura com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* toointegrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="e3b7f-298">Dessa forma, você pode usar outros recursos de IoT em sua solução.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="e3b7f-299">Um serviço de token é um serviço de nuvem personalizado.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="e3b7f-300">Ele usa um IoT Hub *política de acesso compartilhado* com **DeviceConnect** permissões toocreate *no escopo do dispositivo* tokens.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions toocreate *device-scoped* tokens.</span></span> <span data-ttu-id="e3b7f-301">Esses tokens habilitar um hub IoT de tooyour de tooconnect de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-301">These tokens enable a device tooconnect tooyour IoT hub.</span></span>

![Etapas do padrão do serviço de token de saudação][img-tokenservice]

<span data-ttu-id="e3b7f-303">Aqui estão as etapas principais de saudação do padrão do serviço de token de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-303">Here are hello main steps of hello token service pattern:</span></span>

1. <span data-ttu-id="e3b7f-304">Crie uma política de acesso compartilhado do Hub IoT com permissões **DeviceConnect** para seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="e3b7f-305">Você pode criar essa política em Olá [portal do Azure] [ lnk-management-portal] ou programaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-305">You can create this policy in hello [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="e3b7f-306">serviço de token de saudação usa esse tokens de saudação de toosign política cria.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-306">hello token service uses this policy toosign hello tokens it creates.</span></span>
1. <span data-ttu-id="e3b7f-307">Quando um dispositivo precisa tooaccess seu hub IoT, ele solicita um token assinado do serviço de token.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-307">When a device needs tooaccess your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="e3b7f-308">dispositivo Olá pode autenticar sua identidade de dispositivo personalizado de identidade do registro/autenticação esquema toodetermine Olá que o serviço de token Olá usa o token de saudação de toocreate.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-308">hello device can authenticate with your custom identity registry/authentication scheme toodetermine hello device identity that hello token service uses toocreate hello token.</span></span>
1. <span data-ttu-id="e3b7f-309">serviço de token de saudação retorna um token.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-309">hello token service returns a token.</span></span> <span data-ttu-id="e3b7f-310">Olá token é criado usando `/devices/{deviceId}` como `resourceURI`, com `deviceId` como dispositivo de saudação que está sendo autenticado.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-310">hello token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as hello device being authenticated.</span></span> <span data-ttu-id="e3b7f-311">serviço de token de saudação usa o token de saudação do hello acesso compartilhado política tooconstruct.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-311">hello token service uses hello shared access policy tooconstruct hello token.</span></span>
1. <span data-ttu-id="e3b7f-312">dispositivo Olá usa o token de saudação diretamente com o hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-312">hello device uses hello token directly with hello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e3b7f-313">Você pode usar a classe do .NET Olá [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] ou Olá classe Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate um token no seu serviço de token.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-313">You can use hello .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or hello Java class [IotHubServiceSasToken][lnk-java-sas] toocreate a token in your token service.</span></span>

<span data-ttu-id="e3b7f-314">serviço de token de saudação pode definir a expiração do token Olá conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-314">hello token service can set hello token expiration as desired.</span></span> <span data-ttu-id="e3b7f-315">Quando Olá token expirar, hub IoT de saudação os servidores de conexão do dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-315">When hello token expires, hello IoT hub severs hello device connection.</span></span> <span data-ttu-id="e3b7f-316">Em seguida, Olá deve solicitar um novo token do serviço de token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-316">Then, hello device must request a new token from hello token service.</span></span> <span data-ttu-id="e3b7f-317">Um tempo de expiração curto aumenta a carga de saudação em dispositivo hello e o serviço de token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-317">A short expiry time increases hello load on both hello device and hello token service.</span></span>

<span data-ttu-id="e3b7f-318">Para um hub de tooyour de tooconnect do dispositivo, você ainda deverá adicionar-toohello registro de identidade de IoT Hub — mesmo que o dispositivo hello está usando um token e não um tooconnect de chave do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-318">For a device tooconnect tooyour hub, you must still add it toohello IoT Hub identity registry — even though hello device is using a token and not a device key tooconnect.</span></span> <span data-ttu-id="e3b7f-319">Portanto, você pode continuar o controle de acesso por dispositivo toouse habilitando ou desabilitando as identidades de dispositivo no hello [registro identidade][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-319">Therefore, you can continue toouse per-device access control by enabling or disabling device identities in hello [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="e3b7f-320">Essa abordagem reduz os riscos de saudação do uso de tokens com tempos de expiração do tempo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-320">This approach mitigates hello risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="e3b7f-321">Comparação com um gateway personalizado</span><span class="sxs-lookup"><span data-stu-id="e3b7f-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="e3b7f-322">padrão de serviço de token de saudação é Olá recomendada tooimplement de maneira um esquema de autenticação/registro identidade personalizada com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-322">hello token service pattern is hello recommended way tooimplement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="e3b7f-323">Esse padrão é recomendado porque o IoT Hub continua toohandle a maior parte do tráfego de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-323">This pattern is recommended because IoT Hub continues toohandle most of hello solution traffic.</span></span> <span data-ttu-id="e3b7f-324">No entanto, se o esquema de autenticação personalizado Olá é então entrelaçada com protocolo hello, você pode exigir um *gateway personalizado* tooprocess todos Olá tráfego.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-324">However, if hello custom authentication scheme is so intertwined with hello protocol, you may require a *custom gateway* tooprocess all hello traffic.</span></span> <span data-ttu-id="e3b7f-325">Um exemplo de tal cenário é usar [TLS (Transport Layer Security) e as PSKs (chaves pré-compartilhadas)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="e3b7f-326">Para obter mais informações, consulte Olá [gateway do protocolo] [ lnk-protocols] tópico.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-326">For more information, see hello [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="e3b7f-327">Tópicos de referência:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-327">Reference topics:</span></span>

<span data-ttu-id="e3b7f-328">Hello seguinte referência tópicos fornecem mais informações sobre o controle hub de IoT tooyour de acesso.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-328">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="e3b7f-329">Permissões de Hub IoT</span><span class="sxs-lookup"><span data-stu-id="e3b7f-329">IoT Hub permissions</span></span>

<span data-ttu-id="e3b7f-330">Olá tabela a seguir lista permissões de saudação, você pode usar o hub IoT do toocontrol acesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-330">hello following table lists hello permissions you can use toocontrol access tooyour IoT hub.</span></span>

| <span data-ttu-id="e3b7f-331">Permissão</span><span class="sxs-lookup"><span data-stu-id="e3b7f-331">Permission</span></span> | <span data-ttu-id="e3b7f-332">Observações</span><span class="sxs-lookup"><span data-stu-id="e3b7f-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="e3b7f-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="e3b7f-333">**RegistryRead**</span></span> |<span data-ttu-id="e3b7f-334">Registro de identidade de toohello do concede acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-334">Grants read access toohello identity registry.</span></span> <span data-ttu-id="e3b7f-335">Para saber mais, consulte [Registro de identidade][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="e3b7f-336">Essa permissão é usada pelos serviços de nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="e3b7f-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="e3b7f-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="e3b7f-338">Concede acesso de leitura e gravação toohello registro identidade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-338">Grants read and write access toohello identity registry.</span></span> <span data-ttu-id="e3b7f-339">Para saber mais, consulte [Registro de identidade][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="e3b7f-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="e3b7f-340">Essa permissão é usada pelos serviços de nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="e3b7f-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="e3b7f-341">**ServiceConnect**</span></span> |<span data-ttu-id="e3b7f-342">Concede acesso toocloud serviço voltado para a comunicação e os pontos de extremidade de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-342">Grants access toocloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="e3b7f-343">Concede permissão tooreceive dispositivo para nuvem mensagens, enviar mensagens de nuvem para dispositivo e recuperar Olá correspondente confirmações de entrega.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-343">Grants permission tooreceive device-to-cloud messages, send cloud-to-device messages, and retrieve hello corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="e3b7f-344">Carregamentos de confirmações de entrega de tooretrieve concede permissão para o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-344">Grants permission tooretrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="e3b7f-345">Concede permissão tooaccess dispositivo twins tooupdate marcas e propriedades desejadas, recuperar as propriedades relatadas e executar consultas.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-345">Grants permission tooaccess device twins tooupdate tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="e3b7f-346">Essa permissão é usada pelos serviços de nuvem de back-end.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="e3b7f-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="e3b7f-347">**DeviceConnect**</span></span> |<span data-ttu-id="e3b7f-348">Concede acesso toodevice voltados para pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-348">Grants access toodevice-facing endpoints.</span></span> <br/><span data-ttu-id="e3b7f-349">Concede permissão toosend dispositivo para nuvem mensagens e receber mensagens de nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-349">Grants permission toosend device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="e3b7f-350">Carregamento do arquivo concede permissão tooperform de um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-350">Grants permission tooperform file upload from a device.</span></span> <br/><span data-ttu-id="e3b7f-351">Concede permissão tooreceive dispositivo duas desejada propriedade notificações e macros relatadas propriedades de dispositivo de atualização.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-351">Grants permission tooreceive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="e3b7f-352">Arquivo de tooperform concede permissão carrega.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-352">Grants permission tooperform file uploads.</span></span> <br/><span data-ttu-id="e3b7f-353">Essa permissão é usada por dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="e3b7f-354">Material de referência adicional</span><span class="sxs-lookup"><span data-stu-id="e3b7f-354">Additional reference material</span></span>

<span data-ttu-id="e3b7f-355">Outros tópicos de referência Olá guia do desenvolvedor de IoT Hub incluem:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-355">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="e3b7f-356">[Pontos de extremidade de IoT Hub] [ lnk-endpoints] descreve Olá vários pontos de extremidade que expõe a cada hub IoT para operações de tempo de execução e gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-356">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="e3b7f-357">[Limitação e cotas] [ lnk-quotas] descreve cotas hello e comportamentos que se aplicam a toohello serviço de IoT Hub de limitação.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-357">[Throttling and quotas][lnk-quotas] describes hello quotas and throttling behaviors that apply toohello IoT Hub service.</span></span>
* <span data-ttu-id="e3b7f-358">[SDKs do Azure de dispositivo e serviço IoT] [ lnk-sdks] listas Olá SDKs, você pode usar ao desenvolver aplicativos do dispositivo e o serviço que interagem com o IoT Hub de vários idiomas.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-358">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="e3b7f-359">[Linguagem de consulta de IoT Hub] [ lnk-query] descreve a linguagem de consulta de saudação, você pode usar informações de tooretrieve de IoT Hub sobre seus trabalhos e twins do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-359">[IoT Hub query language][lnk-query] describes hello query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="e3b7f-360">[Suporte de IoT Hub MQTT] [ lnk-devguide-mqtt] fornece mais informações sobre o suporte de IoT Hub para o protocolo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="e3b7f-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3b7f-361">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3b7f-361">Next steps</span></span>

<span data-ttu-id="e3b7f-362">Agora que você aprendeu como toocontrol acessar o IoT Hub, você pode estar interessado em Olá tópicos do guia de desenvolvedor de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-362">Now you have learned how toocontrol access IoT Hub, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="e3b7f-363">[Usar configurações e estado do dispositivo twins toosynchronize][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-363">[Use device twins toosynchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="e3b7f-364">[Invocar um método direto em um dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="e3b7f-365">[Agendar trabalhos em vários dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e3b7f-366">Se você quiser tootry alguns dos conceitos de saudação descritos neste artigo, você pode estar interessado em Olá tutoriais de IoT Hub a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3b7f-366">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="e3b7f-367">[Introdução ao Hub IoT do Azure][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="e3b7f-368">[Como a nuvem para dispositivo toosend mensagens com o IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-368">[How toosend cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="e3b7f-369">[Como tooprocess mensagens de dispositivo para a nuvem de IoT Hub][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="e3b7f-369">[How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

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
