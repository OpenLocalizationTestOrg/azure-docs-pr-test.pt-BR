---
title: "aaaUse Olá toocreate portal do Azure um IoT Hub | Microsoft Docs"
description: "Como toocreate, gerenciar e excluir hubs de IoT do Azure por meio de saudação portal do Azure. Inclui informações sobre tipos de preço, escala, segurança e configurações de mensagens."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="51ec1-104">Criar um hub IoT usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51ec1-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="51ec1-105">Este artigo descreve:</span><span class="sxs-lookup"><span data-stu-id="51ec1-105">This article describes:</span></span>

* <span data-ttu-id="51ec1-106">Como toofind Olá serviço de IoT Hub no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ec1-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="51ec1-107">Como toocreate e gerenciar os hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="51ec1-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="51ec1-108">Onde toofind Olá serviço IoT Hub</span><span class="sxs-lookup"><span data-stu-id="51ec1-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="51ec1-109">Você pode encontrar hello serviço IoT Hub Olá seguintes locais no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="51ec1-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="51ec1-110">Escolha **+ Novo**, em seguida, escolha **Internet das Coisas**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="51ec1-111">No hello Marketplace, escolha **Internet das coisas**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="51ec1-112">Crie um hub IoT</span><span class="sxs-lookup"><span data-stu-id="51ec1-112">Create an IoT hub</span></span>

<span data-ttu-id="51ec1-113">Você pode criar um hub IoT usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="51ec1-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="51ec1-114">Olá **+ novo** opção abre a folha de saudação mostrada na seguinte captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="51ec1-115">Olá etapas para criar o hub IoT de saudação por este método e por meio do marketplace Olá são idênticas.</span><span class="sxs-lookup"><span data-stu-id="51ec1-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="51ec1-116">No hello Marketplace, escolha **criar** folha de saudação tooopen mostrada na seguinte captura de tela de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="51ec1-117">Olá, seções a seguir descrevem Olá um hub IoT toocreate de várias etapas:</span><span class="sxs-lookup"><span data-stu-id="51ec1-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="51ec1-118">Escolher nome de saudação do hub IoT de saudação</span><span class="sxs-lookup"><span data-stu-id="51ec1-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="51ec1-119">toocreate um hub IoT, você deve nomear o hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="51ec1-120">Esse nome deve ser exclusivo entre todos os Hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="51ec1-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="51ec1-121">Escolha a saudação de preço</span><span class="sxs-lookup"><span data-stu-id="51ec1-121">Choose hello pricing tier</span></span>

<span data-ttu-id="51ec1-122">Você pode escolher entre quatro camadas: **Gratuita**, **Padrão 1**, **Padrão 2** e **Padrão S3**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="51ec1-123">camada gratuita Olá permite somente 500 toobe de dispositivos conectados toohello IoT hub e backup too8, 000 mensagens por dia.</span><span class="sxs-lookup"><span data-stu-id="51ec1-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="51ec1-124">**Standard S1**: edição de saudação S1 de uso para soluções de IoT com um grande número de dispositivos que cada um gerará pequenas quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="51ec1-125">Cada unidade de edição Olá S1 permite que até too400, 000 mensagens por dia em todos os dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="51ec1-126">**Standard S2**: edição de saudação S2 Use para soluções de IoT em quais dispositivos geram grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="51ec1-127">Cada unidade de edição de S2 Olá permite que até too6 milhões de mensagens por dia entre todos os dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="51ec1-128">**Standard S3**: edição de saudação S3 de uso para soluções de IoT que gerem grandes quantidades de dados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="51ec1-129">Cada unidade de edição de S3 Olá permite que até too300 milhões de mensagens por dia entre todos os dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="51ec1-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="51ec1-130">O Hub IoT só permite um hub gratuito por assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ec1-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="51ec1-131">Unidades do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="51ec1-131">IoT hub units</span></span>

<span data-ttu-id="51ec1-132">número de saudação de mensagens permitido por unidade por dia depende de preço do hub.</span><span class="sxs-lookup"><span data-stu-id="51ec1-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="51ec1-133">Por exemplo, se você quiser Olá ingresso de toosupport de hub IoT de 700.000 mensagens, escolha duas unidades de camada de S1.</span><span class="sxs-lookup"><span data-stu-id="51ec1-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="51ec1-134">Partições de toocloud do dispositivo e grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="51ec1-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="51ec1-135">Você pode alterar o número de saudação de partições para um hub IoT.</span><span class="sxs-lookup"><span data-stu-id="51ec1-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="51ec1-136">número de partições do saudação padrão é 4, você pode escolher um número diferente de lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="51ec1-137">Você não precisa tooexplicitly criar um grupo de recurso vazio.</span><span class="sxs-lookup"><span data-stu-id="51ec1-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="51ec1-138">Quando você cria um recurso, você pode escolher qualquer toocreate um novo ou use um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="51ec1-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="51ec1-139">Escolha uma assinatura</span><span class="sxs-lookup"><span data-stu-id="51ec1-139">Choose subscription</span></span>

<span data-ttu-id="51ec1-140">IoT Hub do Azure automaticamente Olá listas de conta de usuário de saudação de assinaturas do Azure está vinculado.</span><span class="sxs-lookup"><span data-stu-id="51ec1-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="51ec1-141">Você pode escolher Olá assinatura do Azure tooassociate Olá IoT hub.</span><span class="sxs-lookup"><span data-stu-id="51ec1-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="51ec1-142">Escolha o local de saudação</span><span class="sxs-lookup"><span data-stu-id="51ec1-142">Choose hello location</span></span>

<span data-ttu-id="51ec1-143">opção de local de saudação fornece uma lista de regiões Olá onde o IoT Hub está disponível.</span><span class="sxs-lookup"><span data-stu-id="51ec1-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="51ec1-144">Criar hello IoT hub</span><span class="sxs-lookup"><span data-stu-id="51ec1-144">Create hello IoT hub</span></span>

<span data-ttu-id="51ec1-145">Quando todas as etapas anteriores forem concluídas, você pode criar o hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="51ec1-146">Clique em **criar** toostart Olá toocreate do processo de back-end e implantar o hub IoT de saudação com opções de saudação escolhidas.</span><span class="sxs-lookup"><span data-stu-id="51ec1-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="51ec1-147">Pode levar alguns hub IoT toocreate Olá de minutos como demora Olá toorun de implantação de back-end em servidores do hello local apropriado.</span><span class="sxs-lookup"><span data-stu-id="51ec1-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="51ec1-148">Alterar as configurações de saudação do hub IoT de saudação</span><span class="sxs-lookup"><span data-stu-id="51ec1-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="51ec1-149">Você pode alterar as configurações de saudação de um hub IoT existente depois que ele é criado da saudação folha de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="51ec1-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="51ec1-150">**Políticas de acesso compartilhado**: essas políticas definem permissões de saudação para dispositivos e serviços tooconnect tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="51ec1-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="51ec1-151">Você pode acessar essas políticas clicando em **Políticas de acesso compartilhado** em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="51ec1-152">Nessa folha, você pode modificar as políticas existentes ou adicionar uma nova política.</span><span class="sxs-lookup"><span data-stu-id="51ec1-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="51ec1-153">Criar uma política</span><span class="sxs-lookup"><span data-stu-id="51ec1-153">Create a policy</span></span>

* <span data-ttu-id="51ec1-154">Clique em **adicionar** tooopen uma folha.</span><span class="sxs-lookup"><span data-stu-id="51ec1-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="51ec1-155">Aqui você pode digitar o nome da nova política hello e permissões de saudação que você deseja tooassociate com essa política, conforme mostrado na seguinte Olá Figura:</span><span class="sxs-lookup"><span data-stu-id="51ec1-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="51ec1-156">Há várias permissões que podem ser associadas a essas políticas compartilhadas.</span><span class="sxs-lookup"><span data-stu-id="51ec1-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="51ec1-157">Olá **registro ler** e **gravação de registro** políticas concederem leitura e registro de identidade de toohello de direitos de acesso de gravação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="51ec1-158">Escolhendo a opção de gravação da saudação automaticamente escolhe Olá ler opção.</span><span class="sxs-lookup"><span data-stu-id="51ec1-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="51ec1-159">Olá **conexão de serviço** diretiva concede pontos de extremidade do serviço de permissão tooaccess como **receber o dispositivo para nuvem**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="51ec1-160">Olá **dispositivo se conectar** diretiva concede permissões para enviar e receber mensagens usando pontos de extremidade Olá IoT Hub do lado do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51ec1-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="51ec1-161">Clique em **criar** tooadd nesse recém-criado lista existente de toohello de política.</span><span class="sxs-lookup"><span data-stu-id="51ec1-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="51ec1-162">Pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="51ec1-162">Endpoints</span></span>

<span data-ttu-id="51ec1-163">Clique em **pontos de extremidade** toodisplay uma lista de pontos de extremidade de hub IoT Olá que você está modificando.</span><span class="sxs-lookup"><span data-stu-id="51ec1-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="51ec1-164">Há dois tipos de pontos de extremidade: pontos de extremidade que são integrados ao hub IoT de saudação e pontos de extremidade que você adicione toohello IoT hub após sua criação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="51ec1-165">Pontos de extremidade internos</span><span class="sxs-lookup"><span data-stu-id="51ec1-165">Built-in endpoints</span></span>

<span data-ttu-id="51ec1-166">Há dois pontos de extremidade internos: **toodevice comentários de nuvem** e **eventos**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="51ec1-167">**Nuvem comentários toodevice** configurações: essa configuração tem duas subsettings: **tooDevice TTL de nuvem** (time-to-live) e **tempo de retenção** (em horas) para mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="51ec1-168">Quando seu primeiro criar um hub IoT, essas duas configurações tem valor padrão de saudação de uma hora.</span><span class="sxs-lookup"><span data-stu-id="51ec1-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="51ec1-169">tooadjust essas configurações, use os controles deslizantes de saudação ou digite os valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="51ec1-170">Configurações de **Eventos**: essa configuração tem várias subconfigurações, algumas das quais são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="51ec1-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="51ec1-171">Olá lista a seguir descreve essas configurações:</span><span class="sxs-lookup"><span data-stu-id="51ec1-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="51ec1-172">**Partições**: um valor padrão é definido quando Olá IoT hub é criado.</span><span class="sxs-lookup"><span data-stu-id="51ec1-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="51ec1-173">Você pode alterar o número de saudação de partições por meio dessa configuração.</span><span class="sxs-lookup"><span data-stu-id="51ec1-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="51ec1-174">**Nome do evento compatível com o Hub e o ponto de extremidade**: quando Olá IoT hub é criado, um Hub de eventos é criado internamente que você pode precisar acessar toounder determinadas circunstâncias.</span><span class="sxs-lookup"><span data-stu-id="51ec1-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="51ec1-175">Não é possível personalizar os valores de nome e o ponto de extremidade Olá compatível com o Hub de eventos, mas você pode copiá-los clicando **cópia**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="51ec1-176">**Tempo de retenção**: definir dia tooone por padrão, mas você pode alterá-la usando a lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="51ec1-177">Esse valor é em dias para a configuração de dispositivo para nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="51ec1-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="51ec1-178">**Grupos de consumidores**: grupos de consumidores habilitar várias mensagens de tooread leitores independentemente do hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="51ec1-179">Todos os Hub IoT são criados com um grupo de consumidores padrão.</span><span class="sxs-lookup"><span data-stu-id="51ec1-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="51ec1-180">No entanto, você pode adicionar ou excluir hubs de IoT consumidor grupos tooyour usando essa configuração.</span><span class="sxs-lookup"><span data-stu-id="51ec1-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="51ec1-181">grupo de consumidores saudação padrão não pode ser editado ou excluído.</span><span class="sxs-lookup"><span data-stu-id="51ec1-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="51ec1-182">Pontos de extremidade personalizados</span><span class="sxs-lookup"><span data-stu-id="51ec1-182">Custom endpoints</span></span>

<span data-ttu-id="51ec1-183">Você pode adicionar pontos de extremidade personalizados em seu hub IoT usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="51ec1-184">De saudação **pontos de extremidade** folha, clique em **adicionar** em Olá tooopen superior Olá **Adicionar ponto de extremidade** folha.</span><span class="sxs-lookup"><span data-stu-id="51ec1-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="51ec1-185">Digite as informações de saudação necessárias e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="51ec1-186">O ponto de extremidade personalizado agora está listado no hello principal **pontos de extremidade** folha.</span><span class="sxs-lookup"><span data-stu-id="51ec1-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="51ec1-187">Você pode ler mais sobre pontos de extremidade personalizados em [Referência — Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="51ec1-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="51ec1-188">Rotas</span><span class="sxs-lookup"><span data-stu-id="51ec1-188">Routes</span></span>

<span data-ttu-id="51ec1-189">Clique em **rotas** toomanage como o IoT Hub envia as mensagens de dispositivo para nuvem.</span><span class="sxs-lookup"><span data-stu-id="51ec1-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="51ec1-190">Você pode adicionar o hub de IoT tooyour rotas clicando **adicionar** na parte superior de saudação do hello **rotas*** folha, inserir informações de saudação necessárias e, em seguida, clicando em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="51ec1-191">A rota é então listada em Olá principal **rotas** folha.</span><span class="sxs-lookup"><span data-stu-id="51ec1-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="51ec1-192">Você pode editar uma rota clicando na lista de saudação de rotas.</span><span class="sxs-lookup"><span data-stu-id="51ec1-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="51ec1-193">tooenable uma rota, clique na lista de saudação de rotas e defina Olá **habilitado** alternar muito**Off**.</span><span class="sxs-lookup"><span data-stu-id="51ec1-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="51ec1-194">alteração de saudação toosave, clique em **Okey** na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="51ec1-195">Preços e dimensionamento</span><span class="sxs-lookup"><span data-stu-id="51ec1-195">Pricing and scale</span></span>

<span data-ttu-id="51ec1-196">Olá preços de um hub IoT existente podem ser alterado por meio de saudação **preços** configurações com hello exceções a seguir:</span><span class="sxs-lookup"><span data-stu-id="51ec1-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="51ec1-197">Na implementação atual do hello, um hub IoT com um SKU livre não é possível alterar tooone de camadas de saudação paga SKUs, ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="51ec1-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="51ec1-198">Pode haver apenas um hub IoT de camada gratuita em Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ec1-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="51ec1-199">Você pode mover de uma camada superior de toolower somente quando o número de Olá de mensagens enviadas desse dia exceder a cota de saudação de nível mais baixo de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ec1-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="51ec1-200">Por exemplo, se o número de saudação de mensagens por dia exceder 400.000, Olá camada para Olá IoT hub pode ser alterado.</span><span class="sxs-lookup"><span data-stu-id="51ec1-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="51ec1-201">No entanto, se você alterar o nível de S1 toohello hub IoT de saudação está limitada para esse dia.</span><span class="sxs-lookup"><span data-stu-id="51ec1-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="51ec1-202">Excluir Olá IoT hub</span><span class="sxs-lookup"><span data-stu-id="51ec1-202">Delete hello IoT hub</span></span>

<span data-ttu-id="51ec1-203">Você pode procurar o hub IoT de toohello toodelete desejado clicando **procurar**, e escolhendo Olá toodelete hub apropriado.</span><span class="sxs-lookup"><span data-stu-id="51ec1-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="51ec1-204">toodelete Olá IoT hub, clique em Olá **excluir** botão abaixo do nome de hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="51ec1-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51ec1-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51ec1-205">Next steps</span></span>

<span data-ttu-id="51ec1-206">Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="51ec1-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="51ec1-207">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="51ec1-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="51ec1-208">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="51ec1-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="51ec1-209">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="51ec1-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="51ec1-210">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="51ec1-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="51ec1-211">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="51ec1-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="51ec1-212">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="51ec1-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="51ec1-213">[Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="51ec1-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
