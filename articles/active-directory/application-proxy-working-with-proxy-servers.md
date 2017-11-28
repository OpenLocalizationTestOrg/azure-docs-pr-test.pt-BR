---
title: aaaWork com existente local servidores proxy e o Azure AD | Microsoft Docs
description: Aborda como toowork com existente local servidores proxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="f2ec7-103">Trabalhar com servidores proxy locais existentes</span><span class="sxs-lookup"><span data-stu-id="f2ec7-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="f2ec7-104">Este artigo explica como tooconfigure toowork de conectores de Proxy de aplicativo do Azure Active Directory (AD do Azure) com servidores de proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-104">This article explains how tooconfigure Azure Active Directory (Azure AD) Application Proxy connectors toowork with outbound proxy servers.</span></span> <span data-ttu-id="f2ec7-105">Ele destina-se aos clientes com ambientes de rede que já têm proxies.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="f2ec7-106">Começamos analisando este principais cenários de implantação:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="f2ec7-107">Configure conectores toobypass os proxies de saída do local.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-107">Configure connectors toobypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="f2ec7-108">Configure conectores toouse tooaccess um proxy de saída Proxy de aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-108">Configure connectors toouse an outbound proxy tooaccess Azure AD Application Proxy.</span></span>

<span data-ttu-id="f2ec7-109">Para saber mais sobre como funcionam os conectores, consulte [Noções básicas sobre conectores de proxy de aplicativo do Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="f2ec7-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-hello-outbound-proxy"></a><span data-ttu-id="f2ec7-110">Configurar o proxy de saída Olá</span><span class="sxs-lookup"><span data-stu-id="f2ec7-110">Configure hello outbound proxy</span></span>

<span data-ttu-id="f2ec7-111">Se você tiver um proxy de saída em seu ambiente, use uma conta com o proxy de saída tooconfigure Olá permissões apropriadas.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-111">If you have an outbound proxy in your environment, use an account with appropriate permissions tooconfigure hello outbound proxy.</span></span> <span data-ttu-id="f2ec7-112">Porque o instalador Olá é executado no contexto de saudação do usuário de saudação que está fazendo a instalação Olá, você pode verificar a configuração hello usando o Microsoft Edge ou outro navegador da Internet.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-112">Because hello installer runs in hello context of hello user who's doing hello installation, you can check hello configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="f2ec7-113">configurações de proxy tooconfigure Olá no Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-113">tooconfigure hello proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="f2ec7-114">Vá muito**configurações** > **configurações avançadas de exibição** > **abrir configurações de Proxy** > **Manual de configuração de Proxy** .</span><span class="sxs-lookup"><span data-stu-id="f2ec7-114">Go too**Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="f2ec7-115">Definir **usar um servidor proxy** muito**na**, selecione Olá **não usar Olá proxy para endereços locais (intranet)** caixa de seleção e, em seguida, alterar Olá tooreflect de endereço e porta o servidor de proxy local.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-115">Set **Use a proxy server** too**On**, select hello **Don’t use hello proxy server for local (intranet) addresses** check box, and then change hello address and port tooreflect your local proxy server.</span></span>
3. <span data-ttu-id="f2ec7-116">Preencha as configurações de proxy necessário de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-116">Fill in hello necessary proxy settings.</span></span>

   ![Caixa de diálogo para as configurações do proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="f2ec7-118">Ignorar proxies de saída</span><span class="sxs-lookup"><span data-stu-id="f2ec7-118">Bypass outbound proxies</span></span>

<span data-ttu-id="f2ec7-119">Conectores têm componentes subjacentes do sistema operacional que fazem solicitações de saída.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="f2ec7-120">Esses componentes automaticamente tentam toolocate um servidor proxy na rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-120">These components automatically attempt toolocate a proxy server on hello network.</span></span> <span data-ttu-id="f2ec7-121">Eles usam a descoberta automática de Proxy da Web (WPAD), se ele estiver habilitado no ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in hello environment.</span></span>

<span data-ttu-id="f2ec7-122">componentes do sistema operacional Olá tentam toolocate um servidor proxy, executando uma pesquisa de DNS para wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-122">hello OS components attempt toolocate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="f2ec7-123">Se isso for resolvido no DNS, uma solicitação HTTP é feita toohello IP endereço para WPAD.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-123">If this resolves in DNS, an HTTP request is then made toohello IP address for wpad.dat.</span></span> <span data-ttu-id="f2ec7-124">Essa solicitação se torna o script de configuração de proxy de saudação em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-124">This request becomes hello proxy configuration script in your environment.</span></span> <span data-ttu-id="f2ec7-125">conector de saudação usa esse tooselect um servidor de proxy de saída do script.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-125">hello connector uses this script tooselect an outbound proxy server.</span></span> <span data-ttu-id="f2ec7-126">No entanto, o tráfego do conector pode ainda não passar por, devido às configurações de configuração adicional necessárias no proxy hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-126">However, connector traffic might still not go through, because of additional configuration settings needed on hello proxy.</span></span>

<span data-ttu-id="f2ec7-127">Você pode configurar Olá conector toobypass seu tooensure de proxy local que usa direcionar toohello de conectividade do Azure services.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-127">You can configure hello connector toobypass your on-premises proxy tooensure that it uses direct connectivity toohello Azure services.</span></span> <span data-ttu-id="f2ec7-128">Recomendamos essa abordagem (se a política de rede permite que ele), pois isso significa que você tenha um menos toomaintain de configuração.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration toomaintain.</span></span>

<span data-ttu-id="f2ec7-129">toodisable uso de proxy de saída para o conector Olá, edite o arquivo de C:\Program Files\Microsoft AAD aplicativo Proxy Connector\ApplicationProxyConnectorService.exe.config de saudação e adicionar Olá *system.net* seção mostrada nesse exemplo de código :</span><span class="sxs-lookup"><span data-stu-id="f2ec7-129">toodisable outbound proxy usage for hello connector, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
<span data-ttu-id="f2ec7-130">tooensure que o serviço de conector Updater Olá também ignora proxy hello, fazer um localizado em C:\Program Files\Microsoft atualizador do conector AAD aplicativo Proxy alteração toohello ApplicationProxyConnectorUpdaterService.exe.config arquivo semelhante.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-130">tooensure that hello Connector Updater service also bypasses hello proxy, make a similar change toohello ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="f2ec7-131">Ser se cópias de toomake arquivos originais de hello, caso você precise de arquivos. config do toorevert toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-131">Be sure toomake copies of hello original files, in case you need toorevert toohello default .config files.</span></span>

## <a name="use-hello-outbound-proxy-server"></a><span data-ttu-id="f2ec7-132">Usar um servidor proxy de saída Olá</span><span class="sxs-lookup"><span data-stu-id="f2ec7-132">Use hello outbound proxy server</span></span>

<span data-ttu-id="f2ec7-133">Alguns ambientes exigem que todos os toogo de tráfego de saída por meio de um proxy de saída, sem exceção.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-133">Some environments require all outbound traffic toogo through an outbound proxy, without exception.</span></span> <span data-ttu-id="f2ec7-134">Como resultado, ignorar o proxy de saudação não é uma opção.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-134">As a result, bypassing hello proxy is not an option.</span></span>

<span data-ttu-id="f2ec7-135">Você pode configurar Olá conector tráfego toogo por meio do proxy de saída hello, conforme mostrado no diagrama a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-135">You can configure hello connector traffic toogo through hello outbound proxy, as shown in hello following diagram:</span></span>

 ![Configurando o conector toogo de tráfego por meio de um proxy de saída de tooAzure AD Proxy de aplicativo](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="f2ec7-137">Como resultado de ter somente o tráfego de saída, há tooconfigure sem necessidade de acesso por meio de seus firewalls de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-137">As a result of having only outbound traffic, there's no need tooconfigure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a><span data-ttu-id="f2ec7-138">Etapa 1: Configurar conector hello e relacionadas toogo de serviços por meio do proxy de saída Olá</span><span class="sxs-lookup"><span data-stu-id="f2ec7-138">Step 1: Configure hello connector and related services toogo through hello outbound proxy</span></span>

<span data-ttu-id="f2ec7-139">Conforme abordado anteriormente, se WPAD estiver habilitado no ambiente hello e configurado corretamente, conector Olá descobrirá automaticamente toouse de servidor e a tentativa de proxy de saída Olá-lo.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-139">As covered earlier, if WPAD is enabled in hello environment and configured appropriately, hello connector will automatically discover hello outbound proxy server and attempt toouse it.</span></span> <span data-ttu-id="f2ec7-140">No entanto, você pode configurar explicitamente Olá conector toogo por meio de um proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-140">However, you can explicitly configure hello connector toogo through an outbound proxy.</span></span>

<span data-ttu-id="f2ec7-141">toodo assim, edite Olá C:\Program Files\Microsoft AAD aplicativo Proxy Connector\ApplicationProxyConnectorService.exe.config arquivo e adicione Olá *system.net* seção mostrada nesse exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-141">toodo so, edit hello C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add hello *system.net* section shown in this code sample.</span></span> <span data-ttu-id="f2ec7-142">Alterar *proxyserver:8080* tooreflect o nome do servidor proxy local ou o endereço IP e a saudação da porta que ele está escutando.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-142">Change *proxyserver:8080* tooreflect your local proxy server name or IP address, and hello port that it's listening on.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

<span data-ttu-id="f2ec7-143">Em seguida, configure o proxy de Olá Olá atualizador do conector serviço toouse fazendo um arquivo de toohello de alteração semelhante localizado em C:\Program Files\Microsoft AAD aplicativo Proxy do conector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-143">Next, configure hello Connector Updater service toouse hello proxy by making a similar change toohello file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a><span data-ttu-id="f2ec7-144">Etapa 2: Configurar o tráfego de tooallow Olá proxy do conector hello e tooflow serviços relacionados por meio de</span><span class="sxs-lookup"><span data-stu-id="f2ec7-144">Step 2: Configure hello proxy tooallow traffic from hello connector and related services tooflow through</span></span>

<span data-ttu-id="f2ec7-145">Há quatro tooconsider de aspectos no proxy de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-145">There are four aspects tooconsider at hello outbound proxy:</span></span>
* <span data-ttu-id="f2ec7-146">Regras de saída do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-146">Proxy outbound rules</span></span>
* <span data-ttu-id="f2ec7-147">Autenticação do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-147">Proxy authentication</span></span>
* <span data-ttu-id="f2ec7-148">Portas do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-148">Proxy ports</span></span>
* <span data-ttu-id="f2ec7-149">Inspeção SSL</span><span class="sxs-lookup"><span data-stu-id="f2ec7-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="f2ec7-150">Regras de saída do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-150">Proxy outbound rules</span></span>
<span data-ttu-id="f2ec7-151">Permitir acesso toohello pontos de extremidade para acesso ao serviço de conector a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-151">Allow access toohello following endpoints for connector service access:</span></span>

* <span data-ttu-id="f2ec7-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="f2ec7-152">*.msappproxy.net</span></span>
* <span data-ttu-id="f2ec7-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f2ec7-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="f2ec7-154">Para o registro inicial, permitir acesso toohello pontos de extremidade a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-154">For initial registration, allow access toohello following endpoints:</span></span>

* <span data-ttu-id="f2ec7-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="f2ec7-155">login.windows.net</span></span>
* <span data-ttu-id="f2ec7-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f2ec7-156">login.microsoftonline.com</span></span>

<span data-ttu-id="f2ec7-157">Se você não pode permitir a conectividade pelo FQDN e precisar toospecify intervalos IP em vez disso, use estas opções:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-157">If you can't allow connectivity by FQDN and need toospecify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="f2ec7-158">Permitir acesso de saída de conector Olá tooall destinos.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-158">Allow hello connector outbound access tooall destinations.</span></span>
* <span data-ttu-id="f2ec7-159">Permitir acesso de saída de conector Olá muito[intervalos IP do datacenter do Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="f2ec7-159">Allow hello connector outbound access too[Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="f2ec7-160">Olá desafio usando Olá lista de intervalos IP do datacenter do Azure é que ela é atualizada semanalmente.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-160">hello challenge with using hello list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="f2ec7-161">É necessário tooput um processo em vigor tooensure que as regras de acesso são atualizadas.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-161">You need tooput a process in place tooensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="f2ec7-162">Autenticação do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-162">Proxy authentication</span></span>

<span data-ttu-id="f2ec7-163">No momento, não há suporte à autenticação do proxy.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="f2ec7-164">Nossa recomendação atual é destinos de Internet de toohello tooallow Olá conector acesso anônimo.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-164">Our current recommendation is tooallow hello connector anonymous access toohello Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="f2ec7-165">Portas do proxy</span><span class="sxs-lookup"><span data-stu-id="f2ec7-165">Proxy ports</span></span>

<span data-ttu-id="f2ec7-166">conector de saudação torna as conexões de saída baseada em SSL usando o método de conexão hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-166">hello connector makes outbound SSL-based connections by using hello CONNECT method.</span></span> <span data-ttu-id="f2ec7-167">Esse método essencialmente configura um túnel por meio do proxy de saída hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-167">This method essentially sets up a tunnel through hello outbound proxy.</span></span> <span data-ttu-id="f2ec7-168">Configure Olá proxy server tooallow túnel tooports 443 e 80.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-168">Configure hello proxy server tooallow tunneling tooports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="f2ec7-169">Quando o Barramento de Serviço for executado por HTTPS, ele usará a porta 443.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="f2ec7-170">No entanto, por padrão, o barramento de serviço tentativas de conexões TCP diretas e reverterá tooHTTPS somente se a conectividade direta com falha.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-170">However, by default, Service Bus attempts direct TCP connections and falls back tooHTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="f2ec7-171">tooensure que Olá tráfego também for enviado pelo servidor de proxy de saída de saudação do barramento de serviço, certifique-se de que esse conector Olá não é possível conectar-se diretamente toohello serviços do Azure para portas 9350, 9352 e 5671.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-171">tooensure that hello Service Bus traffic is also sent through hello outbound proxy server, ensure that hello connector cannot directly connect toohello Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="f2ec7-172">Inspeção SSL</span><span class="sxs-lookup"><span data-stu-id="f2ec7-172">SSL inspection</span></span>
<span data-ttu-id="f2ec7-173">Não use inspeção SSL para o tráfego de conector hello, porque ele causa problemas para o tráfego de conector de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-173">Do not use SSL inspection for hello connector traffic, because it causes problems for hello connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="f2ec7-174">Solucionar problemas do proxy do conector e problemas de conectividade do serviço</span><span class="sxs-lookup"><span data-stu-id="f2ec7-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="f2ec7-175">Agora você deve ver todo o tráfego que passam por meio do proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-175">Now you should see all traffic flowing through hello proxy.</span></span> <span data-ttu-id="f2ec7-176">Se você tiver problemas, deve ajudar a saudação informações de solução de problemas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-176">If you have problems, hello following troubleshooting information should help.</span></span>

<span data-ttu-id="f2ec7-177">Olá tooidentify de maneira recomendada e solucionar problemas de conectividade do conector problemas é tootake uma rede de captura no serviço de conector de saudação ao iniciar o serviço do conector hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-177">hello best way tooidentify and troubleshoot connector connectivity issues is tootake a network capture on hello connector service while starting hello connector service.</span></span> <span data-ttu-id="f2ec7-178">Como essa tarefa pode ser um tanto quanto assustadora, vamos observar umas dicas rápidas sobre como capturar e filtrar rastreamentos de rede.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="f2ec7-179">Você pode usar Olá, ferramenta de sua escolha de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-179">You can use hello monitoring tool of your choice.</span></span> <span data-ttu-id="f2ec7-180">Para fins de saudação deste artigo, usamos Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-180">For hello purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="f2ec7-181">Você pode [baixá-lo na Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="f2ec7-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="f2ec7-182">exemplos de saudação e filtros que usamos na Olá seções a seguir são específico tooNetwork Monitor, mas princípios Olá podem ser aplicadas tooany ferramenta de análise.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-182">hello examples and filters that we use in hello following sections are specific tooNetwork Monitor, but hello principles can be applied tooany analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="f2ec7-183">Fazer uma captura usando o Monitor de Rede</span><span class="sxs-lookup"><span data-stu-id="f2ec7-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="f2ec7-184">toostart uma captura:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-184">toostart a capture:</span></span>

1. <span data-ttu-id="f2ec7-185">Abra o Monitor de Rede e clique em **Nova Captura**.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="f2ec7-186">Clique em Olá **iniciar** botão.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-186">Click hello **Start** button.</span></span>

   ![Janela Monitor de Rede](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="f2ec7-188">Depois de concluir uma captura, clique em Olá **parar** botão tooend-lo.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-188">After you complete a capture, click hello **Stop** button tooend it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="f2ec7-189">Fazer uma captura do tráfego do conector</span><span class="sxs-lookup"><span data-stu-id="f2ec7-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="f2ec7-190">Para solução de problemas iniciais, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-190">For initial troubleshooting, perform hello following steps:</span></span>

1. <span data-ttu-id="f2ec7-191">De Services. msc, pare o serviço de conector de Proxy de aplicativo do AD do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-191">From services.msc, stop hello Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="f2ec7-192">Inicie a captura de rede hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-192">Start hello network capture.</span></span>
3. <span data-ttu-id="f2ec7-193">Inicie serviço de conector de Proxy de aplicativo do AD do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-193">Start hello Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="f2ec7-194">Pare a captura de rede hello.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-194">Stop hello network capture.</span></span>

   ![Serviço Conector do Proxy de Aplicativo do Azure AD em services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a><span data-ttu-id="f2ec7-196">Examinar as solicitações de saudação do servidor de proxy Olá conector toohello</span><span class="sxs-lookup"><span data-stu-id="f2ec7-196">Look at hello requests from hello connector toohello proxy server</span></span>

<span data-ttu-id="f2ec7-197">Agora que temos uma captura de rede, você está pronto toofiltê-lo.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-197">Now that you’ve got a network capture, you're ready toofilter it.</span></span> <span data-ttu-id="f2ec7-198">Olá toolooking de chave no rastreamento de saudação é entender como toofilter Olá capturar.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-198">hello key toolooking at hello trace is understanding how toofilter hello capture.</span></span>

<span data-ttu-id="f2ec7-199">Um filtro é o seguinte (onde 8080 é a porta de serviço de proxy Olá):</span><span class="sxs-lookup"><span data-stu-id="f2ec7-199">One filter is as follows (where 8080 is hello proxy service port):</span></span>

<span data-ttu-id="f2ec7-200">**(http.Request ou http.Response) e tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="f2ec7-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="f2ec7-201">Se você inserir esse filtro Olá **exibir filtro** janela e selecione **aplicar**, ele filtra o tráfego de saudação capturado com base no filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-201">If you enter this filter in hello **Display Filter** window and select **Apply**, it filters hello captured traffic based on hello filter.</span></span>

<span data-ttu-id="f2ec7-202">Olá filtro anterior mostra apenas Olá solicitações e respostas HTTP de porta de proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-202">hello preceding filter shows just hello HTTP requests and responses to/from hello proxy port.</span></span> <span data-ttu-id="f2ec7-203">Para a inicialização do conector em que o conector de saudação é toouse configurado um servidor proxy, filtro Olá mostraria algo assim:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-203">For a connector startup where hello connector is configured toouse a proxy server, hello filter would show something like this:</span></span>

 ![Lista de exemplo das solicitações e respostas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="f2ec7-205">Você agora está procurando especificamente Olá que conectar solicita que mostram a comunicação com o servidor de proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-205">You're now specifically looking for hello CONNECT requests that show communication with hello proxy server.</span></span> <span data-ttu-id="f2ec7-206">No caso de êxito, você obterá uma resposta HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="f2ec7-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="f2ec7-207">Se você ver outros códigos de resposta, como 407 ou 502, proxy Olá é exigir autenticação ou não permitir o tráfego do hello por algum outro motivo.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-207">If you see other response codes, such as 407 or 502, hello proxy is requiring authentication or not allowing hello traffic for some other reason.</span></span> <span data-ttu-id="f2ec7-208">Neste ponto, você interage com a equipe de suporte do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="f2ec7-209">Identificar tentativas de conexão TCP com falha</span><span class="sxs-lookup"><span data-stu-id="f2ec7-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="f2ec7-210">Olá outro cenário comum que pode estar interessado em é quando hello conector está tentando tooconnect diretamente, mas ele falha.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-210">hello other common scenario that you may be interested in is when hello connector is trying tooconnect directly, but it's failing.</span></span>

<span data-ttu-id="f2ec7-211">Outro filtro de Monitor de rede que ajuda você tooeasily identificar esse problema é:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-211">Another Network Monitor filter that helps you tooeasily identify this problem is:</span></span>

<span data-ttu-id="f2ec7-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="f2ec7-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="f2ec7-213">Um pacote SYN é o primeiro pacote de saudação enviado tooestablish uma conexão TCP.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-213">A SYN packet is hello first packet sent tooestablish a TCP connection.</span></span> <span data-ttu-id="f2ec7-214">Se esse pacote não retornar uma resposta, Olá SYN é reativada.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-214">If this packet doesn’t return a response, hello SYN is reattempted.</span></span> <span data-ttu-id="f2ec7-215">Você pode usar Olá anterior filtro toosee qualquer SYNs retransmitidos.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-215">You can use hello preceding filter toosee any retransmitted SYNs.</span></span> <span data-ttu-id="f2ec7-216">Em seguida, você pode verificar se essas SYNs correspondem tooany relacionados ao conector tráfego.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-216">Then, you can check whether these SYNs correspond tooany connector-related traffic.</span></span>

<span data-ttu-id="f2ec7-217">Olá exemplo a seguir mostra uma tentativa de conexão com falha tooService porta 9352:</span><span class="sxs-lookup"><span data-stu-id="f2ec7-217">hello following example shows a failed connection attempt tooService Bus port 9352:</span></span>

 ![Resposta de exemplo para uma tentativa de conexão com falha](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="f2ec7-219">Se você vir algo como Olá anterior resposta, conector hello está tentando toocommunicate diretamente com hello barramento de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-219">If you see something like hello preceding response, hello connector is trying toocommunicate directly with hello Azure Service Bus service.</span></span> <span data-ttu-id="f2ec7-220">Se você esperar Olá conector toomake conexões diretas toohello Azure services, essa resposta é uma indicação clara de que você tem um problema de rede ou de um firewall.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-220">If you expect hello connector toomake direct connections toohello Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="f2ec7-221">Se você estiver toouse configurado um servidor proxy, essa resposta pode significar que o barramento de serviço está tentando uma conexão TCP direto antes de alternar tooattempting uma conexão via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-221">If you are configured toouse a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching tooattempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="f2ec7-222">A análise do rastreamento da rede não é para qualquer um.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="f2ec7-223">Mas ele pode ser uma ferramenta valiosa tooget rápido saber o que está acontecendo com a sua rede.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-223">But it can be a valuable tool tooget quick information about what's going on with your network.</span></span>

<span data-ttu-id="f2ec7-224">Se você continuar toostruggle com problemas de conectividade do conector, crie um tíquete com nossa equipe de suporte.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-224">If you continue toostruggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="f2ec7-225">equipe de saudação pode ajudá-lo com solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f2ec7-225">hello team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="f2ec7-226">Para obter informações sobre como resolver os erros do Conector do Proxy do Aplicativo, consulte [Solucionar Problemas do Proxy do Aplicativo](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="f2ec7-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2ec7-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2ec7-227">Next steps</span></span>

[<span data-ttu-id="f2ec7-228">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2ec7-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="f2ec7-229">
[Como instalar o toosilently Olá conector de Proxy de aplicativo do AD do Azure](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="f2ec7-229">
[How toosilently install hello Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
