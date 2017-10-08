---
title: "aaaConfiguring um Firewall de aplicativo Web (WAF) para o ambiente de serviço de aplicativo"
description: "Saiba como um aplicativo web de tooconfigure firewall na frente de seu ambiente de serviço de aplicativo."
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
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a><span data-ttu-id="60cfa-103">Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60cfa-103">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="60cfa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="60cfa-104">Overview</span></span>
<span data-ttu-id="60cfa-105">Web firewalls de aplicativo como Olá [WAF Barracuda Azure](https://www.barracuda.com/programs/azure) que está disponível no hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ajuda a proteger seus aplicativos web ao inspecionar o tráfego de entrada da web tooblock SQL inclusões, scripts intersites, carregamentos de malware & aplicativo DDoS e outros ataques.</span><span class="sxs-lookup"><span data-stu-id="60cfa-105">Web application firewalls like hello [Barracuda WAF for Azure](https://www.barracuda.com/programs/azure) that is available on hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) helps secure your web applications by inspecting inbound web traffic tooblock SQL injections, Cross-Site Scripting, malware uploads & application DDoS and other attacks.</span></span> <span data-ttu-id="60cfa-106">Ele também inspeciona respostas de saudação de servidores de web de back-end de Olá para prevenção de perda de dados (DLP).</span><span class="sxs-lookup"><span data-stu-id="60cfa-106">It also inspects hello responses from hello back-end web servers for Data Loss Prevention (DLP).</span></span> <span data-ttu-id="60cfa-107">Combinado com isolamento hello e dimensionamento adicionais fornecidos pelo ambientes de serviço de aplicativo, isso fornece um ambiente ideal toohost aplicativos de web críticos de negócios que precisam de solicitação mal-intencionada toowithstand e alto volume de tráfego.</span><span class="sxs-lookup"><span data-stu-id="60cfa-107">Combined with hello isolation and additional scaling provided by App Service Environments, this provides an ideal environment toohost business critical web applications that need toowithstand malicious requests and high volume traffic.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a><span data-ttu-id="60cfa-108">Configuração</span><span class="sxs-lookup"><span data-stu-id="60cfa-108">Setup</span></span>
<span data-ttu-id="60cfa-109">Para este documento, configuraremos nosso ambiente de serviço de aplicativo por trás da carga de vários com balanceamento de instâncias do Barracuda WAF para que apenas o tráfego de saudação WAF pode alcançar Olá ambiente de serviço de aplicativo e ele não poderá ser acessado de saudação DMZ.</span><span class="sxs-lookup"><span data-stu-id="60cfa-109">For this document we will configure our App Service Environment behind multiple load balanced instances of Barracuda WAF so that only traffic from hello WAF can reach hello App Service Environment and it will not be accessible from hello DMZ.</span></span> <span data-ttu-id="60cfa-110">Também teremos Azure Traffic Manager na frente do nosso saldo de tooload instâncias WAF Barracuda em data centers do Azure e regiões.</span><span class="sxs-lookup"><span data-stu-id="60cfa-110">We will also have Azure Traffic Manager in front of our Barracuda WAF instances tooload balance across Azure data centers and regions.</span></span> <span data-ttu-id="60cfa-111">Um diagrama de alto nível da instalação Olá aparência que é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-111">A high level diagram of hello setup would look like what is shown below.</span></span>

![Arquitetura][Architecture] 

> <span data-ttu-id="60cfa-113">Observação: com introdução de saudação do [ILB suporte para o ambiente de serviço de aplicativo](app-service-environment-with-internal-load-balancer.md), configure Olá ASE toobe acessada da saudação DMZ e ser apenas a rede privada toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="60cfa-113">Note: With hello introduction of [ILB support for App Service Environment](app-service-environment-with-internal-load-balancer.md), you can configure hello ASE toobe inaccessible from hello DMZ and only be available toohello private network.</span></span> 
> 
> 

## <a name="configuring-your-app-service-environment"></a><span data-ttu-id="60cfa-114">Configurando o Ambiente do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60cfa-114">Configuring your App Service Environment</span></span>
<span data-ttu-id="60cfa-115">tooconfigure um ambiente de serviço de aplicativo consulte muito[nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) no assunto hello.</span><span class="sxs-lookup"><span data-stu-id="60cfa-115">tooconfigure an App Service Environment refer too[our documentation](app-service-web-how-to-create-an-app-service-environment.md) on hello subject.</span></span> <span data-ttu-id="60cfa-116">Quando você tiver um ambiente de serviço de aplicativo criado, você pode criar [aplicativos Web](app-service-web-overview.md), [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md) e [aplicativos móveis](../app-service-mobile/app-service-mobile-value-prop.md) neste ambiente que será protegido por trás Olá WAF nós Configure na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="60cfa-116">Once you have an App Service Environment created, you can create [Web Apps](app-service-web-overview.md), [API Apps](../app-service-api/app-service-api-apps-why-best-platform.md) and [Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) in this environment that will all be protected behind hello WAF we configure in hello next section.</span></span>

## <a name="configuring-your-barracuda-waf-cloud-service"></a><span data-ttu-id="60cfa-117">Configurando o Serviço de Nuvem Barracuda WAF</span><span class="sxs-lookup"><span data-stu-id="60cfa-117">Configuring your Barracuda WAF Cloud Service</span></span>
<span data-ttu-id="60cfa-118">O Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implantar seu WAF em uma máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="60cfa-118">Barracuda has a [detailed article](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) on deploying its WAF on a virtual machine in Azure.</span></span> <span data-ttu-id="60cfa-119">Mas porque deseja redundância e não a introdução de um ponto único de falha, você deseja toodeploy pelo menos 2 WAF instância VMs Olá mesmo serviço de nuvem quando seguir estas instruções.</span><span class="sxs-lookup"><span data-stu-id="60cfa-119">But because we want redundancy and not introduce a single point of failure, you want toodeploy at least 2 WAF instance VMs into hello same Cloud Service when following these instructions.</span></span>

### <a name="adding-endpoints-toocloud-service"></a><span data-ttu-id="60cfa-120">Adicionando pontos de extremidade tooCloud serviço</span><span class="sxs-lookup"><span data-stu-id="60cfa-120">Adding Endpoints tooCloud Service</span></span>
<span data-ttu-id="60cfa-121">Depois que você tiver 2 ou mais VM de WAF instâncias no serviço de nuvem, você pode usar Olá [portal do Azure](https://portal.azure.com/) tooadd HTTP e HTTPS pontos de extremidade que são usados por seu aplicativo, conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-121">Once you have 2 or more WAF VM instances in your Cloud Service you can use hello [Azure portal](https://portal.azure.com/) tooadd HTTP and HTTPS endpoints that are used by your application as shown in hello image below.</span></span>

![Configurar ponto de extremidade][ConfigureEndpoint]

<span data-ttu-id="60cfa-123">Se seus aplicativos usam outros pontos de extremidade, verifique tooadd-se de que esses lista toothis também.</span><span class="sxs-lookup"><span data-stu-id="60cfa-123">If your applications use other endpoints, make sure tooadd those toothis list as well.</span></span> 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a><span data-ttu-id="60cfa-124">Configuração do Barracuda WAF por meio do Portal de Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="60cfa-124">Configuring Barracuda WAF through its Management Portal</span></span>
<span data-ttu-id="60cfa-125">O Barracuda WAF usa a porta TCP 8000 para configuração por meio do respectivo portal de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="60cfa-125">Barracuda WAF uses TCP Port 8000 for configuration through its management portal.</span></span> <span data-ttu-id="60cfa-126">Como temos várias instâncias de saudação WAF VMs, você precisará toorepeat Olá etapas para cada instância VM.</span><span class="sxs-lookup"><span data-stu-id="60cfa-126">Since we have multiple instances of hello WAF VMs you will need toorepeat hello steps here for each VM instance.</span></span> 

> <span data-ttu-id="60cfa-127">Observação: Depois que você concluir configuração WAF, remova ponto de extremidade TCP/8000 Olá de todos os seu tookeep WAF VMs sua WAF segura.</span><span class="sxs-lookup"><span data-stu-id="60cfa-127">Note: Once you are done with WAF configuration, remove hello TCP/8000 endpoint from all your WAF VMs tookeep your WAF secure.</span></span>
> 
> 

<span data-ttu-id="60cfa-128">Adicione Olá gerenciamento ponto de extremidade como mostrado na imagem de saudação abaixo tooconfigure seu WAF Barracuda.</span><span class="sxs-lookup"><span data-stu-id="60cfa-128">Add hello management endpoint as shown in hello image below tooconfigure your Barracuda WAF.</span></span>

![Adicionar ponto de extremidade de gerenciamento][AddManagementEndpoint]

<span data-ttu-id="60cfa-130">Use um ponto de extremidade de gerenciamento do navegador toobrowse toohello em seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="60cfa-130">Use a browser toobrowse toohello management endpoint on your Cloud Service.</span></span> <span data-ttu-id="60cfa-131">Se seu serviço de nuvem é chamado test.cloudapp.net, você acessaria esse ponto de extremidade navegando toohttp://test.cloudapp.net:8000.</span><span class="sxs-lookup"><span data-stu-id="60cfa-131">If your Cloud Service is called test.cloudapp.net, you would access this endpoint by browsing toohttp://test.cloudapp.net:8000.</span></span> <span data-ttu-id="60cfa-132">Você deve ver uma página de logon como abaixo que você pode fazer logon usando as credenciais especificadas na fase de configuração VM Olá WAF.</span><span class="sxs-lookup"><span data-stu-id="60cfa-132">You should see a login page like below that you can login using credentials you specified in hello WAF VM setup phase.</span></span>

![Página de logon de gerenciamento][ManagementLoginPage]

<span data-ttu-id="60cfa-134">Uma vez logon você verá um painel como Olá uma imagem Olá abaixo que será apresentado estatísticas básicas sobre Olá proteção WAF.</span><span class="sxs-lookup"><span data-stu-id="60cfa-134">Once you login you should see a dashboard as hello one in hello image below that will present basic statistics about hello WAF protection.</span></span>

![Painel de gerenciamento][ManagementDashboard]

<span data-ttu-id="60cfa-136">Clicando na guia Serviços de saudação permitirá que você a configurar seu WAF para serviços que ele está protegendo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-136">Clicking on hello Services tab will let you configure your WAF for services it is protecting.</span></span> <span data-ttu-id="60cfa-137">Para obter mais detalhes sobre a configuração do Barracuda WAF, consulte [a respectiva documentação](https://techlib.barracuda.com/waf/getstarted1).</span><span class="sxs-lookup"><span data-stu-id="60cfa-137">For more details on configuring your Barracuda WAF you can consult [their documentation](https://techlib.barracuda.com/waf/getstarted1).</span></span> <span data-ttu-id="60cfa-138">No exemplo hello abaixo de um aplicativo Web do Azure que serve o tráfego HTTP e HTTPS foi configurada.</span><span class="sxs-lookup"><span data-stu-id="60cfa-138">In hello example below an Azure Web App serving traffic on HTTP and HTTPS has been configured.</span></span>

![Adicionar de gerenciamento de serviços][ManagementAddServices]

> <span data-ttu-id="60cfa-140">Observação: Dependendo de como os aplicativos são configurados e quais recursos estão sendo usados no seu ambiente de serviço de aplicativo, você precisará tooforward tráfego para as portas TCP que não seja a 80 e 443, por exemplo, se você tiver a configuração de IP SSL para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60cfa-140">Note: Depending on how your applications are configured and what features are being used in your App Service Environment, you will need tooforward traffic for TCP ports other than 80 and 443, e.g. if you have IP SSL setup for a Web App.</span></span> <span data-ttu-id="60cfa-141">Para obter uma lista de portas de rede usado em ambientes de serviço de aplicativo, consulte muito[da documentação de controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) seção de portas de rede.</span><span class="sxs-lookup"><span data-stu-id="60cfa-141">For a list of network ports used in App Service Environments, please refer too[Control Inbound Traffic documentation's](app-service-app-service-environment-control-inbound-traffic.md) Network Ports section.</span></span>
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a><span data-ttu-id="60cfa-142">Configurando o Gerenciador de Tráfego do Microsoft Azure (OPCIONAL)</span><span class="sxs-lookup"><span data-stu-id="60cfa-142">Configuring Microsoft Azure Traffic Manager (OPTIONAL)</span></span>
<span data-ttu-id="60cfa-143">Se seu aplicativo está disponível em várias regiões, você desejaria saldo tooload-los por trás de [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60cfa-143">If your application is available in multiple regions, then you would want tooload balance them behind [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md).</span></span> <span data-ttu-id="60cfa-144">toodo para que você pode adicionar um ponto de extremidade de saudação [portal clássico do Azure](https://manage.azure.com) usando o nome de serviço de nuvem de saudação para seu WAF no perfil do Traffic Manager Olá conforme mostrado na imagem de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-144">toodo so you can add an endpoint in hello [Azure classic portal](https://manage.azure.com) using hello Cloud Service name for your WAF in hello Traffic Manager profile as shown in hello image below.</span></span> 

![Ponto de extremidade do Gerenciador de Tráfego][TrafficManagerEndpoint]

<span data-ttu-id="60cfa-146">Se seu aplicativo exigir autenticação, certifique-se de que você tem algum recurso que não requerem qualquer autenticação para o Gerenciador de tráfego tooping para disponibilidade de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-146">If your application requires authentication, ensure you have some resource that doesn't require any authentication for Traffic Manager tooping for hello availability of your application.</span></span> <span data-ttu-id="60cfa-147">Você pode configurar a URL de saudação na seção Configuração de saudação em Olá [portal clássico do Azure](https://manage.azure.com) conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-147">You can configure hello URL under hello Configure section on hello [Azure classic portal](https://manage.azure.com) as shown below.</span></span>

![Configurar o Gerenciador de Tráfego][ConfigureTrafficManager]

<span data-ttu-id="60cfa-149">pings de Gerenciador de tráfego tooforward saudação do seu aplicativo de tooyour WAF, é necessário toosetup site traduções em seu aplicativo Barracuda WAF tooforward tráfego tooyour conforme mostrado no exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="60cfa-149">tooforward hello Traffic Manager pings from your WAF tooyour application, you need toosetup Website Translations on your Barracuda WAF tooforward traffic tooyour application as shown in hello example below.</span></span>

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a><span data-ttu-id="60cfa-151">Proteger o tráfego tooApp serviço ambiente usando rede segurança grupos (NSG)</span><span class="sxs-lookup"><span data-stu-id="60cfa-151">Securing Traffic tooApp Service Environment Using Network Security Groups (NSG)</span></span>
<span data-ttu-id="60cfa-152">Siga Olá [documentação de controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre como restringir o tráfego tooyour ambiente de serviço de aplicativo do hello WAF apenas usando o endereço VIP de saudação do seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="60cfa-152">Follow hello [Control Inbound Traffic documentation](app-service-app-service-environment-control-inbound-traffic.md) for details on restricting traffic tooyour App Service Environment from hello WAF only by using hello VIP address of your Cloud Service.</span></span> <span data-ttu-id="60cfa-153">Veja um exemplo de comando do PowerShell para executar essa tarefa para a porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="60cfa-153">Here's a sample Powershell command for performing this task for TCP port 80.</span></span>

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

<span data-ttu-id="60cfa-154">Substitua Olá SourceAddressPrefix Olá endereço de IP Virtual (VIP) do WAF serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="60cfa-154">Replace hello SourceAddressPrefix with hello Virtual IP Address (VIP) of your WAF's Cloud Service.</span></span>

> <span data-ttu-id="60cfa-155">Observação: Olá VIP de seu serviço de nuvem mudará quando você excluir e recriar Olá serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="60cfa-155">Note: hello VIP of your Cloud Service will change when you delete and re-create hello Cloud Service.</span></span> <span data-ttu-id="60cfa-156">Certifique-se de que tooupdate Olá endereço IP no grupo de recursos de rede de hello quando você fizer isso.</span><span class="sxs-lookup"><span data-stu-id="60cfa-156">Make sure tooupdate hello IP address in hello Network Resource group once you do so.</span></span> 
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
