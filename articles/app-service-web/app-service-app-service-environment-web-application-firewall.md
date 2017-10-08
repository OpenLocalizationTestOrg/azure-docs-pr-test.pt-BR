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
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo
## <a name="overview"></a>Visão geral
Web firewalls de aplicativo como Olá [WAF Barracuda Azure](https://www.barracuda.com/programs/azure) que está disponível no hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) ajuda a proteger seus aplicativos web ao inspecionar o tráfego de entrada da web tooblock SQL inclusões, scripts intersites, carregamentos de malware & aplicativo DDoS e outros ataques. Ele também inspeciona respostas de saudação de servidores de web de back-end de Olá para prevenção de perda de dados (DLP). Combinado com isolamento hello e dimensionamento adicionais fornecidos pelo ambientes de serviço de aplicativo, isso fornece um ambiente ideal toohost aplicativos de web críticos de negócios que precisam de solicitação mal-intencionada toowithstand e alto volume de tráfego.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configuração
Para este documento, configuraremos nosso ambiente de serviço de aplicativo por trás da carga de vários com balanceamento de instâncias do Barracuda WAF para que apenas o tráfego de saudação WAF pode alcançar Olá ambiente de serviço de aplicativo e ele não poderá ser acessado de saudação DMZ. Também teremos Azure Traffic Manager na frente do nosso saldo de tooload instâncias WAF Barracuda em data centers do Azure e regiões. Um diagrama de alto nível da instalação Olá aparência que é mostrado abaixo.

![Arquitetura][Architecture] 

> Observação: com introdução de saudação do [ILB suporte para o ambiente de serviço de aplicativo](app-service-environment-with-internal-load-balancer.md), configure Olá ASE toobe acessada da saudação DMZ e ser apenas a rede privada toohello disponíveis. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configurando o Ambiente do Serviço de Aplicativo
tooconfigure um ambiente de serviço de aplicativo consulte muito[nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) no assunto hello. Quando você tiver um ambiente de serviço de aplicativo criado, você pode criar [aplicativos Web](app-service-web-overview.md), [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md) e [aplicativos móveis](../app-service-mobile/app-service-mobile-value-prop.md) neste ambiente que será protegido por trás Olá WAF nós Configure na próxima seção, Olá.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configurando o Serviço de Nuvem Barracuda WAF
O Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implantar seu WAF em uma máquina virtual no Azure. Mas porque deseja redundância e não a introdução de um ponto único de falha, você deseja toodeploy pelo menos 2 WAF instância VMs Olá mesmo serviço de nuvem quando seguir estas instruções.

### <a name="adding-endpoints-toocloud-service"></a>Adicionando pontos de extremidade tooCloud serviço
Depois que você tiver 2 ou mais VM de WAF instâncias no serviço de nuvem, você pode usar Olá [portal do Azure](https://portal.azure.com/) tooadd HTTP e HTTPS pontos de extremidade que são usados por seu aplicativo, conforme mostrado na imagem de saudação abaixo.

![Configurar ponto de extremidade][ConfigureEndpoint]

Se seus aplicativos usam outros pontos de extremidade, verifique tooadd-se de que esses lista toothis também. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configuração do Barracuda WAF por meio do Portal de Gerenciamento
O Barracuda WAF usa a porta TCP 8000 para configuração por meio do respectivo portal de gerenciamento. Como temos várias instâncias de saudação WAF VMs, você precisará toorepeat Olá etapas para cada instância VM. 

> Observação: Depois que você concluir configuração WAF, remova ponto de extremidade TCP/8000 Olá de todos os seu tookeep WAF VMs sua WAF segura.
> 
> 

Adicione Olá gerenciamento ponto de extremidade como mostrado na imagem de saudação abaixo tooconfigure seu WAF Barracuda.

![Adicionar ponto de extremidade de gerenciamento][AddManagementEndpoint]

Use um ponto de extremidade de gerenciamento do navegador toobrowse toohello em seu serviço de nuvem. Se seu serviço de nuvem é chamado test.cloudapp.net, você acessaria esse ponto de extremidade navegando toohttp://test.cloudapp.net:8000. Você deve ver uma página de logon como abaixo que você pode fazer logon usando as credenciais especificadas na fase de configuração VM Olá WAF.

![Página de logon de gerenciamento][ManagementLoginPage]

Uma vez logon você verá um painel como Olá uma imagem Olá abaixo que será apresentado estatísticas básicas sobre Olá proteção WAF.

![Painel de gerenciamento][ManagementDashboard]

Clicando na guia Serviços de saudação permitirá que você a configurar seu WAF para serviços que ele está protegendo. Para obter mais detalhes sobre a configuração do Barracuda WAF, consulte [a respectiva documentação](https://techlib.barracuda.com/waf/getstarted1). No exemplo hello abaixo de um aplicativo Web do Azure que serve o tráfego HTTP e HTTPS foi configurada.

![Adicionar de gerenciamento de serviços][ManagementAddServices]

> Observação: Dependendo de como os aplicativos são configurados e quais recursos estão sendo usados no seu ambiente de serviço de aplicativo, você precisará tooforward tráfego para as portas TCP que não seja a 80 e 443, por exemplo, se você tiver a configuração de IP SSL para um aplicativo Web. Para obter uma lista de portas de rede usado em ambientes de serviço de aplicativo, consulte muito[da documentação de controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) seção de portas de rede.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configurando o Gerenciador de Tráfego do Microsoft Azure (OPCIONAL)
Se seu aplicativo está disponível em várias regiões, você desejaria saldo tooload-los por trás de [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo para que você pode adicionar um ponto de extremidade de saudação [portal clássico do Azure](https://manage.azure.com) usando o nome de serviço de nuvem de saudação para seu WAF no perfil do Traffic Manager Olá conforme mostrado na imagem de saudação abaixo. 

![Ponto de extremidade do Gerenciador de Tráfego][TrafficManagerEndpoint]

Se seu aplicativo exigir autenticação, certifique-se de que você tem algum recurso que não requerem qualquer autenticação para o Gerenciador de tráfego tooping para disponibilidade de saudação do seu aplicativo. Você pode configurar a URL de saudação na seção Configuração de saudação em Olá [portal clássico do Azure](https://manage.azure.com) conforme mostrado abaixo.

![Configurar o Gerenciador de Tráfego][ConfigureTrafficManager]

pings de Gerenciador de tráfego tooforward saudação do seu aplicativo de tooyour WAF, é necessário toosetup site traduções em seu aplicativo Barracuda WAF tooforward tráfego tooyour conforme mostrado no exemplo hello abaixo.

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Proteger o tráfego tooApp serviço ambiente usando rede segurança grupos (NSG)
Siga Olá [documentação de controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre como restringir o tráfego tooyour ambiente de serviço de aplicativo do hello WAF apenas usando o endereço VIP de saudação do seu serviço de nuvem. Veja um exemplo de comando do PowerShell para executar essa tarefa para a porta TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Substitua Olá SourceAddressPrefix Olá endereço de IP Virtual (VIP) do WAF serviço de nuvem.

> Observação: Olá VIP de seu serviço de nuvem mudará quando você excluir e recriar Olá serviço de nuvem. Certifique-se de que tooupdate Olá endereço IP no grupo de recursos de rede de hello quando você fizer isso. 
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
