---
title: "Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo"
description: "Saiba como configurar um firewall de aplicativo Web no Ambiente do Serviço de Aplicativo."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 3e9e9fa4ddab60a467e8aa793ec0ca269b0bc4e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="71187-103">Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="71187-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="71187-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="71187-104">Overview</span></span>
<span data-ttu-id="71187-105">O firewall de aplicativo Web, como o [Barracuda WAF para Azure](https://www.barracuda.com/programs/azure), que está disponível no [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/), ajuda a proteger aplicativos Web ao inspecionar o tráfego de entrada da Web para bloquear injeções de SQL, Cross-Site Scripting (script entre sites), carregamentos de malware e DDoS de aplicativo, além de outros ataques.</span><span class="sxs-lookup"><span data-stu-id="71187-105">Web application firewalls like the [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic to block SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="71187-106">Ele também inspeciona as respostas dos servidores Web back-end para DLP (Prevenção contra Perda de Dados).</span><span class="sxs-lookup"><span data-stu-id="71187-106">It also inspects the responses from the back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="71187-107">Combinado com o isolamento e a escala adicional fornecidos pelos Ambientes do Serviço de Aplicativo, esse recurso fornece um ambiente ideal para hospedar aplicativos Web críticos que precisam resistir às solicitações mal-intencionadas e ao tráfego de alto volume.</span><span class="sxs-lookup"><span data-stu-id="71187-107">Combined with the isolation and additional scaling provided by App Service Environments, this provides an ideal environment to host business critical web applications that need to withstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="71187-108">Configuração</span><span class="sxs-lookup"><span data-stu-id="71187-108">Setup</span></span>
<span data-ttu-id="71187-109">Neste documento, vamos configurar nosso Ambiente do Serviço de Aplicativo por trás de várias instâncias balanceadas por carga do Barracuda WAF, de modo que somente o tráfego do WAF possa chegar ao Ambiente do Serviço de Aplicativo e que este não possa ser acessado da DMZ.</span><span class="sxs-lookup"><span data-stu-id="71187-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from the WAF can reach the App Service Environment and it will not be accessible from the DMZ.</span></span> <span data-ttu-id="71187-110">Também temos o Gerenciador de Tráfego do Azure em nossas instâncias do Barracuda WAF para balancear carga entre os datacenters e regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="71187-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances to load balance across Azure data centers and regions.</span></span> <span data-ttu-id="71187-111">Um diagrama de alto nível da configuração seria semelhante ao exibido abaixo.</span><span class="sxs-lookup"><span data-stu-id="71187-111">A high level diagram of the setup would look like what is shown below.</span></span>

![Arquitetura][Architecture] 

> <span data-ttu-id="71187-113">Observação: com a introdução do [suporte ILB para o Ambiente de Serviço de Aplicativo](app-service-environment-with-internal-load-balancer.md), você pode configurar o ASE para ser acessado da DMZ e estar disponível apenas para a rede privada.</span><span class="sxs-lookup"><span data-stu-id="71187-113">Note: With the introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure the ASE to be inaccessible from the DMZ and only be available to the private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="71187-114">Configurando o Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="71187-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="71187-115">Para configurar um Ambiente de Serviço de Aplicativo, consulte a [nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) sobre o assunto.</span><span class="sxs-lookup"><span data-stu-id="71187-115">To configure an App Service Environment refer to [our documentation](app-service-web-how-to-create-an-app-service-environment.md) on the subject.</span></span> <span data-ttu-id="71187-116">Depois que você criar um Ambiente do Serviço de Aplicativo, será possível criar [Aplicativos Web](app-service-web-overview.md), [Aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md) e [Aplicativos Móveis](../app-service-mobile/app-service-mobile-value-prop.md) nesse ambiente e todos eles serão protegidos pelo WAF que configuraremos na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="71187-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind the WAF we configure in the next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="71187-117">Configurando o Serviço de Nuvem Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="71187-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="71187-118">O Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implantar seu WAF em uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="71187-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="71187-119">Mas como queremos redundância, e não introduzir um único ponto de falha, você quer implantar pelo menos 2 VMs da instância WAF no mesmo Serviço de Nuvem ao seguir estas instruções.</span><span class="sxs-lookup"><span data-stu-id="71187-119">But because we want redundancy and not introduce a single point of failure, you want to deploy at least 2 WAF instance VMs into the same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-to-cloud-service"></a><span data-ttu-id="71187-120">Adicionando pontos de extremidade ao Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="71187-120">Adding Endpoints to Cloud Service</span></span>
<span data-ttu-id="71187-121">Depois que você tiver 2 ou mais instâncias da VM WAF no seu Serviço de Nuvem, será possível usar o [portal do Azure](https://portal.azure.com/) para adicionar pontos de extremidade HTTP e HTTPS, que são usados pelo seu aplicativo, conforme mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="71187-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use the [Azure portal](https://portal.azure.com/) to add HTTP and HTTPS endpoints that are used by your application as shown in the image below.</span></span>

![Configurar ponto de extremidade][ConfigureEndpoint]

<span data-ttu-id="71187-123">Se seus aplicativos usam outros pontos de extremidade, não se esqueça de adicioná-los à essa lista também.</span><span class="sxs-lookup"><span data-stu-id="71187-123">If your applications use other endpoints, make sure to add those to this list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="71187-124">Configuração do Barracuda WAF por meio do Portal de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="71187-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="71187-125">O Barracuda WAF usa a porta TCP 8000 para configuração por meio do respectivo portal de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="71187-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="71187-126">Uma vez que temos várias instâncias das VMs WAF, você precisará repetir as etapas para cada instância da VM.</span><span class="sxs-lookup"><span data-stu-id="71187-126">Since we have multiple instances of the WAF VMs you will need to repeat the steps here for each VM instance.</span></span> 

> <span data-ttu-id="71187-127">Observação: depois que tiver finalizado a configuração do WAF, remova o ponto de extremidade TCP/8000 de todas as suas VMs WAF para manter o WAF protegido.</span><span class="sxs-lookup"><span data-stu-id="71187-127">Note: Once you are done with WAF configuration, remove the TCP/8000 endpoint from all your WAF VMs to keep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="71187-128">Adicione o ponto de extremidade de gerenciamento, conforme mostrado na imagem abaixo, para configurar seu Barracuda WAF.</span><span class="sxs-lookup"><span data-stu-id="71187-128">Add the management endpoint as shown in the image below to configure your Barracuda WAF.</span></span>

![Adicionar ponto de extremidade de gerenciamento][AddManagementEndpoint]

<span data-ttu-id="71187-130">Use um navegador para navegar até o ponto de extremidade de gerenciamento no Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="71187-130">Use a browser to browse to the management endpoint on your Cloud Service.</span></span> <span data-ttu-id="71187-131">Se seu Serviço de Nuvem se chamar test.cloudapp.net, você poderá acessar esse ponto de extremidade navegando até http://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="71187-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing to http://test.cloudapp.net:8000.</span></span> <span data-ttu-id="71187-132">Você deve ver uma página de logon como abaixo, em que é possível fazer logon usando as credenciais especificadas na fase de configuração da VM WAF.</span><span class="sxs-lookup"><span data-stu-id="71187-132">You should see a login page like below that you can login using credentials you specified in the WAF VM setup phase.</span></span>

![Página de logon de gerenciamento][ManagementLoginPage]

<span data-ttu-id="71187-134">Depois do logon, você deverá ver um painel como o da imagem abaixo, que apresentará estatísticas básicas sobre a proteção do WAF.</span><span class="sxs-lookup"><span data-stu-id="71187-134">Once you login you should see a dashboard as the one in the image below that will present basic statistics about the WAF protection.</span></span>

![Painel de gerenciamento][ManagementDashboard]

<span data-ttu-id="71187-136">Clicar na guia Serviços permitirá configurar seu WAF para serviços que ele está protegendo.</span><span class="sxs-lookup"><span data-stu-id="71187-136">Clicking on the Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="71187-137">Para obter mais detalhes sobre a configuração do Barracuda WAF, consulte [a respectiva documentação](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="71187-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="71187-138">No exemplo abaixo, foi configurado um Aplicativo Web do Azure que atende ao tráfego no HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="71187-138">In the example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Adicionar de gerenciamento de serviços][ManagementAddServices]

> <span data-ttu-id="71187-140">Observação: dependendo de como os aplicativos são configurados e de quais recursos estão sendo usados no Ambiente do Serviço de Aplicativo, você precisará encaminhar o tráfego para portas TCP que não sejam a 80 e a 443; por exemplo, se você tiver IP SSL configurada para um Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="71187-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need to forward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="71187-141">Para obter uma lista de portas de rede usadas nos Ambientes do Serviço de Aplicativo, consulte a seção Portas de Rede da [documentação sobre como Controlar Tráfego de Entrada](app-service-app-service-environment-control-inbound-traffic.md) .</span><span class="sxs-lookup"><span data-stu-id="71187-141">For a list of network ports used in App Service Environments, please refer to [Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="71187-142">Configurando o Gerenciador de Tráfego do Microsoft Azure (OPCIONAL)</span><span class="sxs-lookup"><span data-stu-id="71187-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="71187-143">Se seu aplicativo estiver disponível em várias regiões, convém balancear a carga dele no [Gerenciador de Tráfego do Azure](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71187-143">If your application is available in multiple regions, then you would want to load balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="71187-144">Para isso, é possível adicionar um ponto de extremidade no [portal clássico do Azure](https://manage.azure.com) usando o nome do Serviço de Nuvem do seu WAF no perfil do Gerenciador de Tráfego, como mostrado na imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="71187-144">To do so you can add an endpoint in the [Azure classic portal](https://manage.azure.com) using the Cloud Service name for your WAF in the Traffic Manager profile as shown in the image below.</span></span> 

![Ponto de extremidade do Gerenciador de Tráfego][TrafficManagerEndpoint]

<span data-ttu-id="71187-146">Se seu aplicativo exigir autenticação, certifique-se de que você tem algum recurso que não exija autenticação para que o Gerenciador de Tráfego execute ping pela disponibilidade do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="71187-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager to ping for the availability of your application.</span></span> <span data-ttu-id="71187-147">Você pode configurar a URL na seção Configurar no [portal clássico do Azure](https://manage.azure.com) , como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="71187-147">You can configure the URL under the Configure section on the [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configurar o Gerenciador de Tráfego][ConfigureTrafficManager]

<span data-ttu-id="71187-149">Para encaminhar os pings do Gerenciador de Tráfego do seu WAF para o aplicativo, é preciso configurar Website Translations no Barracuda WAF, a fim de encaminhar o tráfego para o aplicativo, como mostrado no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="71187-149">To forward the Traffic Manager pings from your WAF to your application, you need to setup Website Translations on your Barracuda WAF to forward traffic to your application as shown in the example below.</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="71187-151">Protegendo o tráfego do Ambiente do Serviço de Aplicativo usando NSGs (grupos de segurança de rede)</span><span class="sxs-lookup"><span data-stu-id="71187-151">Securing Traffic to App Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="71187-152">Siga a [documentação sobre como controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre como restringir o tráfego para o Ambiente do Serviço de Aplicativo do WAF apenas usando o endereço VIP do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="71187-152">Follow the [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic to your App Service Environment from the WAF only by using the VIP address of your Cloud Service.</span></span> <span data-ttu-id="71187-153">Veja um exemplo de comando do PowerShell para executar essa tarefa para a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="71187-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="71187-154">Substitua SourceAddressPrefix pelo VIP (Endereço IP Virtual) do Serviço de Nuvem do seu WAF.</span><span class="sxs-lookup"><span data-stu-id="71187-154">Replace the SourceAddressPrefix with the Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="71187-155">Observação: o VIP do Serviço de Nuvem mudará quando você excluir e recriar o Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="71187-155">Note: The VIP of your Cloud Service will change when you delete and re-create the Cloud Service.</span></span> <span data-ttu-id="71187-156">Certifique-se de atualizar o endereço IP no grupo de recursos de rede depois de fazer isso.</span><span class="sxs-lookup"><span data-stu-id="71187-156">Make sure to update the IP address in the Network Resource group once you do so.</span></span> 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
