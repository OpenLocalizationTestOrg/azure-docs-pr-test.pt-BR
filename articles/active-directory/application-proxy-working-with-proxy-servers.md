---
title: Trabalhar com servidores proxy locais existentes e o Azure AD | Microsoft Docs
description: Cobre como trabalhar com os servidores proxy locais existentes.
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
ms.openlocfilehash: bdca442755507c4ffe8d43692c5b7f2aa3a746f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a><span data-ttu-id="3ef4d-103">Trabalhar com servidores proxy locais existentes</span><span class="sxs-lookup"><span data-stu-id="3ef4d-103">Work with existing on-premises proxy servers</span></span>

<span data-ttu-id="3ef4d-104">Este artigo explica como configurar conectores de Proxy de aplicativo do Azure Active Directory (AD do Azure) para trabalhar com servidores de proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-104">This article explains how to configure Azure Active Directory (Azure AD) Application Proxy connectors to work with outbound proxy servers.</span></span> <span data-ttu-id="3ef4d-105">Ele destina-se aos clientes com ambientes de rede que já têm proxies.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-105">It is intended for customers with network environments that have existing proxies.</span></span>

<span data-ttu-id="3ef4d-106">Começamos analisando este principais cenários de implantação:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-106">We start by looking at these main deployment scenarios:</span></span>
* <span data-ttu-id="3ef4d-107">Configure os conectores para ignorar os proxies de saída locais.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-107">Configure connectors to bypass your on-premises outbound proxies.</span></span>
* <span data-ttu-id="3ef4d-108">Configure os conectores para usar um proxy de saída para acessar o Proxy do Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-108">Configure connectors to use an outbound proxy to access Azure AD Application Proxy.</span></span>

<span data-ttu-id="3ef4d-109">Para saber mais sobre como funcionam os conectores, consulte [Noções básicas sobre conectores de proxy de aplicativo do Azure AD](application-proxy-understand-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="3ef4d-109">For more information about how connectors work, see [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md).</span></span>

## <a name="configure-the-outbound-proxy"></a><span data-ttu-id="3ef4d-110">Configurar o proxy de saída</span><span class="sxs-lookup"><span data-stu-id="3ef4d-110">Configure the outbound proxy</span></span>

<span data-ttu-id="3ef4d-111">Se você tiver um proxy de saída no seu ambiente, use uma conta com permissões apropriadas para configurar o proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-111">If you have an outbound proxy in your environment, use an account with appropriate permissions to configure the outbound proxy.</span></span> <span data-ttu-id="3ef4d-112">Como o instalador é executado no contexto do usuário que está fazendo a instalação, você pode verificar a configuração usando o Microsoft Edge ou outro navegador da Internet.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-112">Because the installer runs in the context of the user who's doing the installation, you can check the configuration by using Microsoft Edge or another Internet browser.</span></span>

<span data-ttu-id="3ef4d-113">Para definir as configurações do proxy usando o Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-113">To configure the proxy settings in Microsoft Edge:</span></span>

1. <span data-ttu-id="3ef4d-114">Vá para **Configurações** > **Exibir Configurações Avançadas** > **Abrir Configurações do Proxy** > **Configuração do Proxy Manual**.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-114">Go to **Settings** > **View Advanced Settings** > **Open Proxy Settings** > **Manual Proxy Setup**.</span></span>
2. <span data-ttu-id="3ef4d-115">Defina **Usar um servidor proxy** para **Ativado**, selecione a caixa de texto **Não usar o servidor proxy para endereços locais (intranet)**, em seguida, altere o endereço e a porta para refletir seu servidor proxy local.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-115">Set **Use a proxy server** to **On**, select the **Don’t use the proxy server for local (intranet) addresses** check box, and then change the address and port to reflect your local proxy server.</span></span>
3. <span data-ttu-id="3ef4d-116">Preencha as configurações do proxy necessárias.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-116">Fill in the necessary proxy settings.</span></span>

   ![Caixa de diálogo para as configurações do proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a><span data-ttu-id="3ef4d-118">Ignorar proxies de saída</span><span class="sxs-lookup"><span data-stu-id="3ef4d-118">Bypass outbound proxies</span></span>

<span data-ttu-id="3ef4d-119">Conectores têm componentes subjacentes do sistema operacional que fazem solicitações de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-119">Connectors have underlying OS components that make outbound requests.</span></span> <span data-ttu-id="3ef4d-120">Esses componentes automaticamente tentam localizar um servidor proxy na rede.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-120">These components automatically attempt to locate a proxy server on the network.</span></span> <span data-ttu-id="3ef4d-121">Eles usarão a Descoberta Automática de Proxy da Rede (WPAD), se ela estiver habilitada no ambiente.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-121">They use Web Proxy Auto-Discovery (WPAD), if it's enabled in the environment.</span></span>

<span data-ttu-id="3ef4d-122">Os componentes do SO tentam localizar um servidor proxy realizando uma pesquisa de DNS para wpad.domainsuffix.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-122">The OS components attempt to locate a proxy server by carrying out a DNS lookup for wpad.domainsuffix.</span></span> <span data-ttu-id="3ef4d-123">Se isso for resolvido no DNS, uma solicitação HTTP será feita para o endereço IP de wpad.dat.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-123">If this resolves in DNS, an HTTP request is then made to the IP address for wpad.dat.</span></span> <span data-ttu-id="3ef4d-124">Essa solicitação se tornará o script de configuração do proxy em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-124">This request becomes the proxy configuration script in your environment.</span></span> <span data-ttu-id="3ef4d-125">O conector usará o script para selecionar um servidor proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-125">The connector uses this script to select an outbound proxy server.</span></span> <span data-ttu-id="3ef4d-126">No entanto, o tráfego do conector ainda pode continuar interrompido devido às definições de configuração adicionais necessárias no proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-126">However, connector traffic might still not go through, because of additional configuration settings needed on the proxy.</span></span>

<span data-ttu-id="3ef4d-127">É possível configurar o conector para ignorar o proxy local de modo a garantir que ele use uma conectividade direta com os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-127">You can configure the connector to bypass your on-premises proxy to ensure that it uses direct connectivity to the Azure services.</span></span> <span data-ttu-id="3ef4d-128">Isso é o que recomendamos (se sua política de rede permitir), porque significa que você terá uma menor configuração para manter.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-128">We recommend this approach (if your network policy allows for it), because it means that you have one less configuration to maintain.</span></span>

<span data-ttu-id="3ef4d-129">Para desabilitar o uso do proxy de saída para o conector, edite o arquivo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config e adicione a seção *system.net* mostrada neste exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-129">To disable outbound proxy usage for the connector, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample:</span></span>

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
<span data-ttu-id="3ef4d-130">Para garantir que o serviço Atualizador do Conector também ignore o proxy, faça uma alteração semelhante no arquivo ApplicationProxyConnectorUpdaterService.exe.config localizado em C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-130">To ensure that the Connector Updater service also bypasses the proxy, make a similar change to the ApplicationProxyConnectorUpdaterService.exe.config file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater.</span></span>

<span data-ttu-id="3ef4d-131">Faça cópias dos arquivos originais, caso você precise voltar para os arquivos .config padrão.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-131">Be sure to make copies of the original files, in case you need to revert to the default .config files.</span></span>

## <a name="use-the-outbound-proxy-server"></a><span data-ttu-id="3ef4d-132">Usar o servidor proxy de saída</span><span class="sxs-lookup"><span data-stu-id="3ef4d-132">Use the outbound proxy server</span></span>

<span data-ttu-id="3ef4d-133">Como mencionado antes, alguns ambientes requerem que todo o tráfego de saída passe por um proxy de saída, sem exceção.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-133">Some environments require all outbound traffic to go through an outbound proxy, without exception.</span></span> <span data-ttu-id="3ef4d-134">Consequentemente, ignorar o proxy não é uma opção.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-134">As a result, bypassing the proxy is not an option.</span></span>

<span data-ttu-id="3ef4d-135">Você pode configurar que o tráfego do conector passe pelo proxy de saída, como mostrado no diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-135">You can configure the connector traffic to go through the outbound proxy, as shown in the following diagram:</span></span>

 ![Configurar o tráfego do conector para passar por um proxy de saída para o Proxy do Aplicativo do Azure AD](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

<span data-ttu-id="3ef4d-137">Como consequência de ter apenas o tráfego de saída, não há necessidade de configurar o acesso de entrada por meio de firewalls.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-137">As a result of having only outbound traffic, there's no need to configure inbound access through your firewalls.</span></span>

### <a name="step-1-configure-the-connector-and-related-services-to-go-through-the-outbound-proxy"></a><span data-ttu-id="3ef4d-138">Etapa 1: Configurar o conector e serviços relacionados para passar pelo proxy de saída</span><span class="sxs-lookup"><span data-stu-id="3ef4d-138">Step 1: Configure the connector and related services to go through the outbound proxy</span></span>

<span data-ttu-id="3ef4d-139">Como descrito antes, se a WPAD estiver habilitada no ambiente e corretamente configurada, o conector descobrirá automaticamente o servidor proxy de saída e tentará usá-lo.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-139">As covered earlier, if WPAD is enabled in the environment and configured appropriately, the connector will automatically discover the outbound proxy server and attempt to use it.</span></span> <span data-ttu-id="3ef4d-140">No entanto, você pode configurar explicitamente o conector para passar por um proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-140">However, you can explicitly configure the connector to go through an outbound proxy.</span></span>

<span data-ttu-id="3ef4d-141">Para isso, edite o arquivo C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config e adicione a seção *system.net* mostrada no exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-141">To do so, edit the C:\Program Files\Microsoft AAD App Proxy Connector\ApplicationProxyConnectorService.exe.config file and add the *system.net* section shown in this code sample.</span></span> <span data-ttu-id="3ef4d-142">Altere *proxyserver:8080* para refletir o nome do servidor proxy local ou o endereço IP e a porta na qual ele está escutando.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-142">Change *proxyserver:8080* to reflect your local proxy server name or IP address, and the port that it's listening on.</span></span>

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

<span data-ttu-id="3ef4d-143">Em seguida, configure o serviço Atualizador do Conector para usar o proxy, fazendo uma alteração semelhante no arquivo localizado em C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-143">Next, configure the Connector Updater service to use the proxy by making a similar change to the file located at C:\Program Files\Microsoft AAD App Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.</span></span>

### <a name="step-2-configure-the-proxy-to-allow-traffic-from-the-connector-and-related-services-to-flow-through"></a><span data-ttu-id="3ef4d-144">Etapa 2: Configurar o proxy para permitir o tráfego a partir do conector e que os serviços relacionados passem por ele</span><span class="sxs-lookup"><span data-stu-id="3ef4d-144">Step 2: Configure the proxy to allow traffic from the connector and related services to flow through</span></span>

<span data-ttu-id="3ef4d-145">Há quatro aspectos a considerar no proxy de saída:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-145">There are four aspects to consider at the outbound proxy:</span></span>
* <span data-ttu-id="3ef4d-146">Regras de saída do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-146">Proxy outbound rules</span></span>
* <span data-ttu-id="3ef4d-147">Autenticação do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-147">Proxy authentication</span></span>
* <span data-ttu-id="3ef4d-148">Portas do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-148">Proxy ports</span></span>
* <span data-ttu-id="3ef4d-149">Inspeção SSL</span><span class="sxs-lookup"><span data-stu-id="3ef4d-149">SSL inspection</span></span>

#### <a name="proxy-outbound-rules"></a><span data-ttu-id="3ef4d-150">Regras de saída do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-150">Proxy outbound rules</span></span>
<span data-ttu-id="3ef4d-151">Permita o acesso aos seguintes pontos de extremidade para acesso ao serviço de conector:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-151">Allow access to the following endpoints for connector service access:</span></span>

* <span data-ttu-id="3ef4d-152">*.msappproxy.net</span><span class="sxs-lookup"><span data-stu-id="3ef4d-152">*.msappproxy.net</span></span>
* <span data-ttu-id="3ef4d-153">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="3ef4d-153">*.servicebus.windows.net</span></span>

<span data-ttu-id="3ef4d-154">Para o registro inicial, permita o acesso aos seguintes pontos de extremidade:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-154">For initial registration, allow access to the following endpoints:</span></span>

* <span data-ttu-id="3ef4d-155">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="3ef4d-155">login.windows.net</span></span>
* <span data-ttu-id="3ef4d-156">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="3ef4d-156">login.microsoftonline.com</span></span>

<span data-ttu-id="3ef4d-157">Se você não puder permitir a conectividade pelo FQDN e precisar especificar intervalos IP, use estas opções:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-157">If you can't allow connectivity by FQDN and need to specify IP ranges instead, use these options:</span></span>

* <span data-ttu-id="3ef4d-158">permitir o acesso de saída do conector para todos os destinos.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-158">Allow the connector outbound access to all destinations.</span></span>
* <span data-ttu-id="3ef4d-159">permitir o acesso de saída do conector para os [intervalos IP do datacenter do Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="3ef4d-159">Allow the connector outbound access to [Azure datacenter IP ranges](https://www.microsoft.com/en-gb/download/details.aspx?id=41653).</span></span> <span data-ttu-id="3ef4d-160">O desafio de usar a lista de intervalos IP do datacenter do Azure é que ela é atualizada semanalmente.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-160">The challenge with using the list of Azure datacenter IP ranges is that it's updated weekly.</span></span> <span data-ttu-id="3ef4d-161">Você precisa implantar um processo para garantir que as regras de acesso sejam atualizadas de acordo.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-161">You need to put a process in place to ensure that your access rules are updated accordingly.</span></span>

#### <a name="proxy-authentication"></a><span data-ttu-id="3ef4d-162">Autenticação do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-162">Proxy authentication</span></span>

<span data-ttu-id="3ef4d-163">No momento, não há suporte à autenticação do proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-163">Proxy authentication is not currently supported.</span></span> <span data-ttu-id="3ef4d-164">Nossa recomendação atual é permitir acesso anônimo ao conector aos destinos da Internet.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-164">Our current recommendation is to allow the connector anonymous access to the Internet destinations.</span></span>

#### <a name="proxy-ports"></a><span data-ttu-id="3ef4d-165">Portas do proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-165">Proxy ports</span></span>

<span data-ttu-id="3ef4d-166">O conector faz conexões de saída baseadas em SSL usando o método CONNECT.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-166">The connector makes outbound SSL-based connections by using the CONNECT method.</span></span> <span data-ttu-id="3ef4d-167">Basicamente, esse método configura um túnel pelo proxy de saída.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-167">This method essentially sets up a tunnel through the outbound proxy.</span></span> <span data-ttu-id="3ef4d-168">Configure o servidor proxy para permitir o túnel para as portas 443 e 80.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-168">Configure the proxy server to allow tunneling to ports 443 and 80.</span></span>

>[!NOTE]
><span data-ttu-id="3ef4d-169">Quando o Barramento de Serviço for executado por HTTPS, ele usará a porta 443.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-169">When Service Bus runs over HTTPS, it uses port 443.</span></span> <span data-ttu-id="3ef4d-170">No entanto, por padrão, o Barramento de Serviço tenta as conexões TCP diretas e voltará para o HTTPS somente se a conectividade direta falhar.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-170">However, by default, Service Bus attempts direct TCP connections and falls back to HTTPS only if direct connectivity fails.</span></span>

<span data-ttu-id="3ef4d-171">Para garantir que o tráfego do Barramento de Serviço também seja enviado pelo servidor proxy de saída, verifique se o conector não pode conectar diretamente os serviços do Azure pelas portas 9350, 9352 e 5671.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-171">To ensure that the Service Bus traffic is also sent through the outbound proxy server, ensure that the connector cannot directly connect to the Azure services for ports 9350, 9352, and 5671.</span></span>

#### <a name="ssl-inspection"></a><span data-ttu-id="3ef4d-172">Inspeção SSL</span><span class="sxs-lookup"><span data-stu-id="3ef4d-172">SSL inspection</span></span>
<span data-ttu-id="3ef4d-173">Não use a inspeção SSL para o tráfego do conector, pois isso causa problemas no tráfego dele.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-173">Do not use SSL inspection for the connector traffic, because it causes problems for the connector traffic.</span></span>

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a><span data-ttu-id="3ef4d-174">Solucionar problemas do proxy do conector e problemas de conectividade do serviço</span><span class="sxs-lookup"><span data-stu-id="3ef4d-174">Troubleshoot connector proxy problems and service connectivity issues</span></span>
<span data-ttu-id="3ef4d-175">Agora, você deve ver todo o tráfego fluindo pelo proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-175">Now you should see all traffic flowing through the proxy.</span></span> <span data-ttu-id="3ef4d-176">Se você tiver problemas, as seguintes informações de solução de problemas deverão ajudar.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-176">If you have problems, the following troubleshooting information should help.</span></span>

<span data-ttu-id="3ef4d-177">A melhor maneira de identificar e solucionar os problemas de conectividade do conector é usar uma captura da rede no serviço do conector ao iniciar tal serviço.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-177">The best way to identify and troubleshoot connector connectivity issues is to take a network capture on the connector service while starting the connector service.</span></span> <span data-ttu-id="3ef4d-178">Como essa tarefa pode ser um tanto quanto assustadora, vamos observar umas dicas rápidas sobre como capturar e filtrar rastreamentos de rede.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-178">This can be a daunting task, so let’s look at quick tips on capturing and filtering network traces.</span></span>

<span data-ttu-id="3ef4d-179">Você pode usar a ferramenta de monitoramento de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-179">You can use the monitoring tool of your choice.</span></span> <span data-ttu-id="3ef4d-180">Para este artigo, usamos o Microsoft Network Monitor 3.4.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-180">For the purposes of this article, we used Microsoft Network Monitor 3.4.</span></span> <span data-ttu-id="3ef4d-181">Você pode [baixá-lo na Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span><span class="sxs-lookup"><span data-stu-id="3ef4d-181">You can [download it from Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).</span></span>

<span data-ttu-id="3ef4d-182">Os exemplos e filtros que usamos nas seções a seguir são específicos do Monitor de Rede, mas os princípios podem ser aplicados a qualquer ferramenta de análise.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-182">The examples and filters that we use in the following sections are specific to Network Monitor, but the principles can be applied to any analysis tool.</span></span>

### <a name="take-a-capture-by-using-network-monitor"></a><span data-ttu-id="3ef4d-183">Fazer uma captura usando o Monitor de Rede</span><span class="sxs-lookup"><span data-stu-id="3ef4d-183">Take a capture by using Network Monitor</span></span>

<span data-ttu-id="3ef4d-184">Para iniciar uma captura:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-184">To start a capture:</span></span>

1. <span data-ttu-id="3ef4d-185">Abra o Monitor de Rede e clique em **Nova Captura**.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-185">Open Network Monitor and click **New Capture**.</span></span>
2. <span data-ttu-id="3ef4d-186">Clique no botão **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-186">Click the **Start** button.</span></span>

   ![Janela Monitor de Rede](./media/application-proxy-working-with-proxy-servers/network-capture.png)

<span data-ttu-id="3ef4d-188">Depois de concluir uma captura, clique no botão **Parar** para encerrar.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-188">After you complete a capture, click the **Stop** button to end it.</span></span>

### <a name="take-a-capture-of-connector-traffic"></a><span data-ttu-id="3ef4d-189">Fazer uma captura do tráfego do conector</span><span class="sxs-lookup"><span data-stu-id="3ef4d-189">Take a capture of connector traffic</span></span>

<span data-ttu-id="3ef4d-190">Para a solução de problemas inicial, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-190">For initial troubleshooting, perform the following steps:</span></span>

1. <span data-ttu-id="3ef4d-191">Em services.msc, pare o serviço Conector do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-191">From services.msc, stop the Azure AD Application Proxy Connector service.</span></span>
2. <span data-ttu-id="3ef4d-192">Inicie a captura da rede.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-192">Start the network capture.</span></span>
3. <span data-ttu-id="3ef4d-193">Inicie o serviço Conector do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-193">Start the Azure AD Application Proxy Connector service.</span></span>
4. <span data-ttu-id="3ef4d-194">Pare a captura de rede.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-194">Stop the network capture.</span></span>

   ![Serviço Conector do Proxy de Aplicativo do Azure AD em services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-the-requests-from-the-connector-to-the-proxy-server"></a><span data-ttu-id="3ef4d-196">Examinar as solicitações do conector para o servidor proxy</span><span class="sxs-lookup"><span data-stu-id="3ef4d-196">Look at the requests from the connector to the proxy server</span></span>

<span data-ttu-id="3ef4d-197">Agora que você tem uma captura de rede, está pronto para filtrá-la.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-197">Now that you’ve got a network capture, you're ready to filter it.</span></span> <span data-ttu-id="3ef4d-198">O mais importante ao examinar o rastreamento é entender como filtrar a captura.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-198">The key to looking at the trace is understanding how to filter the capture.</span></span>

<span data-ttu-id="3ef4d-199">Um filtro é como a seguir (onde 8080 é a porta do serviço proxy):</span><span class="sxs-lookup"><span data-stu-id="3ef4d-199">One filter is as follows (where 8080 is the proxy service port):</span></span>

<span data-ttu-id="3ef4d-200">**(http.Request ou http.Response) e tcp.port==8080**</span><span class="sxs-lookup"><span data-stu-id="3ef4d-200">**(http.Request or http.Response) and tcp.port==8080**</span></span>

<span data-ttu-id="3ef4d-201">Se você inserir esse filtro na janela **Filtro de Exibição** e selecionar **Aplicar**, ele filtrará o tráfego capturado com base no filtro.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-201">If you enter this filter in the **Display Filter** window and select **Apply**, it filters the captured traffic based on the filter.</span></span>

<span data-ttu-id="3ef4d-202">O filtro anterior mostra apenas as solicitações e respostas HTTP para/da porta do proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-202">The preceding filter shows just the HTTP requests and responses to/from the proxy port.</span></span> <span data-ttu-id="3ef4d-203">Para a inicialização de um conector, na qual ele está configurado para usar um servidor proxy, o filtro mostraria algo assim:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-203">For a connector startup where the connector is configured to use a proxy server, the filter would show something like this:</span></span>

 ![Lista de exemplo das solicitações e respostas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

<span data-ttu-id="3ef4d-205">Agora, você está procurando especificamente as solicitações CONNECT que mostram a comunicação com o servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-205">You're now specifically looking for the CONNECT requests that show communication with the proxy server.</span></span> <span data-ttu-id="3ef4d-206">No caso de êxito, você obterá uma resposta HTTP OK (200).</span><span class="sxs-lookup"><span data-stu-id="3ef4d-206">Upon success, you get an HTTP OK (200) response.</span></span>

<span data-ttu-id="3ef4d-207">Se você vir outros códigos de resposta, como 407 ou 502, o proxy está exigindo autenticação ou não está permitindo o tráfego por algum outro motivo.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-207">If you see other response codes, such as 407 or 502, the proxy is requiring authentication or not allowing the traffic for some other reason.</span></span> <span data-ttu-id="3ef4d-208">Neste ponto, você interage com a equipe de suporte do servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-208">At this point, you engage your proxy server support team.</span></span>

### <a name="identify-failed-tcp-connection-attempts"></a><span data-ttu-id="3ef4d-209">Identificar tentativas de conexão TCP com falha</span><span class="sxs-lookup"><span data-stu-id="3ef4d-209">Identify failed TCP connection attempts</span></span>

<span data-ttu-id="3ef4d-210">Outro cenário comum no qual você pode estar interessado é quando o conector está tentando conectar diretamente, mas está falhando.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-210">The other common scenario that you may be interested in is when the connector is trying to connect directly, but it's failing.</span></span>

<span data-ttu-id="3ef4d-211">Outro filtro do Monitor de Rede que ajuda a identificar com facilidade o problema é:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-211">Another Network Monitor filter that helps you to easily identify this problem is:</span></span>

<span data-ttu-id="3ef4d-212">**property.TCPSynRetransmit**</span><span class="sxs-lookup"><span data-stu-id="3ef4d-212">**property.TCPSynRetransmit**</span></span>

<span data-ttu-id="3ef4d-213">Um pacote SYN é o primeiro pacote enviado para estabelecer uma conexão TCP.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-213">A SYN packet is the first packet sent to establish a TCP connection.</span></span> <span data-ttu-id="3ef4d-214">Se o pacote não retornar uma resposta, o SYN fará uma nova tentativa.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-214">If this packet doesn’t return a response, the SYN is reattempted.</span></span> <span data-ttu-id="3ef4d-215">Você pode usar o filtro anterior para ver quaisquer SYNs retransmitidos.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-215">You can use the preceding filter to see any retransmitted SYNs.</span></span> <span data-ttu-id="3ef4d-216">Assim, você pode verificar se eles correspondem ao tráfego relacionado a algum conector.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-216">Then, you can check whether these SYNs correspond to any connector-related traffic.</span></span>

<span data-ttu-id="3ef4d-217">O exemplo a seguir mostra uma tentativa de conexão que falhou na porta 9352 do Barramento de Serviço:</span><span class="sxs-lookup"><span data-stu-id="3ef4d-217">The following example shows a failed connection attempt to Service Bus port 9352:</span></span>

 ![Resposta de exemplo para uma tentativa de conexão com falha](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

<span data-ttu-id="3ef4d-219">Se você vir algo como a resposta anterior, o conector está tentando comunicar-se diretamente com o Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-219">If you see something like the preceding response, the connector is trying to communicate directly with the Azure Service Bus service.</span></span> <span data-ttu-id="3ef4d-220">Se você espera que o conector faça conexões diretas com os serviços do Azure, essa resposta será uma clara indicação de que há um problema de rede ou firewall.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-220">If you expect the connector to make direct connections to the Azure services, this response is a clear indication that you have a network or firewall problem.</span></span>

>[!NOTE]
><span data-ttu-id="3ef4d-221">Se você estiver configurado para usar um servidor proxy, essa resposta poderá significar que o Barramento de Serviço está tentando uma conexão TCP direta antes de tentar uma conexão via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-221">If you are configured to use a proxy server, this response might mean that Service Bus is attempting a direct TCP connection before switching to attempting a connection over HTTPS.</span></span>
>

<span data-ttu-id="3ef4d-222">A análise do rastreamento da rede não é para qualquer um.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-222">Network trace analysis is not for everyone.</span></span> <span data-ttu-id="3ef4d-223">Mas pode ser uma ferramenta valiosa para obter informações rápidas sobre o que está acontecendo com sua rede.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-223">But it can be a valuable tool to get quick information about what's going on with your network.</span></span>

<span data-ttu-id="3ef4d-224">Se você continuar a ter dificuldades com os problemas de conectividade do conector, crie um tíquete com nossa equipe de suporte.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-224">If you continue to struggle with connector connectivity issues, create a ticket with our support team.</span></span> <span data-ttu-id="3ef4d-225">A equipe pode ajudar a solucionar problemas no futuro.</span><span class="sxs-lookup"><span data-stu-id="3ef4d-225">The team can assist you with further troubleshooting.</span></span>

<span data-ttu-id="3ef4d-226">Para obter informações sobre como resolver os erros do Conector do Proxy do Aplicativo, consulte [Solucionar Problemas do Proxy do Aplicativo](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span><span class="sxs-lookup"><span data-stu-id="3ef4d-226">For information about resolving errors with Application Proxy Connector, see [Troubleshoot Application Proxy](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ef4d-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3ef4d-227">Next steps</span></span>

[<span data-ttu-id="3ef4d-228">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ef4d-228">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)<br><span data-ttu-id="3ef4d-229">
[Como instalar silenciosamente o Conector de Proxy de Aplicativo do Azure AD](active-directory-application-proxy-silent-installation.md)</span><span class="sxs-lookup"><span data-stu-id="3ef4d-229">
[How to silently install the Azure AD Application Proxy Connector ](active-directory-application-proxy-silent-installation.md)</span></span>
