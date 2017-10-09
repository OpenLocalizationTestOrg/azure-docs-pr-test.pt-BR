---
title: aaaConfiguration perguntas frequentes para aplicativos web do Azure | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre problemas de configuração e gerenciamento de recursos de aplicativos Web de saudação do serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Perguntas frequentes sobre configuração e gerenciamento de aplicativos Web no Azure

Este artigo possui respostas toofrequently perguntas frequentes (FAQs) sobre problemas de configuração e gerenciamento de saudação [recurso de aplicativos Web do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Há limitações que deve estar atento se desejar toomove recursos de serviço de aplicativo?

Se você planejar toomove do serviço de aplicativo recursos tooa novo grupo de recursos ou assinatura, alguns toobe de limitações estão cientes de. Para saber mais informações, consulte [Limitações do Serviço de Aplicativo](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Como usar um nome de domínio personalizado para meu aplicativo Web?

Para respostas toocommon perguntas sobre como usar um nome de domínio personalizado com seu aplicativo web do Azure, consulte nosso vídeo de sete minutos [adicionar um nome de domínio personalizado](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Olá vídeo oferece uma explicação passo a passo de como tooadd um nome de domínio personalizado. Descreve como toouse sua própria URL em vez da saudação *. azurewebsites.net URL com seu aplicativo do serviço de aplicativo web. Você também pode ver uma explicação detalhada de [como um nome de domínio personalizado de toomap](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Como comprar um novo domínio personalizado para meu aplicativo web?

toolearn como toopurchase e configurar um domínio personalizado para seu aplicativo do serviço de aplicativo web, consulte [comprar e configurar um nome de domínio personalizado no serviço de aplicativo](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Como carregar e configurar um certificado SSL existente para meu aplicativo web?

toolearn como tooupload e configurar um certificado SSL personalizado existente, consulte [associar um existente personalizado SSL certificado tooan aplicativo web do Azure](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Como comprar e configurar um novo certificado SSL no Azure para meu aplicativo web?

toolearn como toopurchase e configurar um certificado SSL para o aplicativo do serviço de aplicativo web, consulte [adicionar um certificado SSL tooyour aplicativo de serviço de aplicativo](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Como mover recursos do Application Insights?

Atualmente, informações de aplicativo do Azure não dá suporte a operação de movimentação de saudação. Se o grupo de recursos original inclui um recurso do Application Insights, você não pode mover esse recurso. Se você incluir o recurso do Application Insights hello quando você tentar toomove um aplicativo de serviço de aplicativo, Olá todo mover haverá falha na operação. No entanto, Olá plano não é necessário toobe do serviço de aplicativo e o Application Insights Olá mesmo grupo de recursos aplicativo hello para Olá aplicativo toofunction corretamente.

Para saber mais informações, consulte [Limitações do Serviço de Aplicativo](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Onde posso encontrar uma lista de verificação de orientação e saber mais sobre o recurso para mover operações?

[Limitações do serviço de aplicativo](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) mostra como toomove recursos tooeither um novo recurso de assinatura ou tooa novo grupo no hello mesma assinatura. Você pode obter informações sobre a lista de verificação de movimentação de recursos hello, saber quais serviços de suporte para operação de movimentação de saudação e saber mais sobre as limitações do serviço de aplicativo e outros tópicos.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Como definir o fuso horário servidor Olá para meu aplicativo web?

tooset Olá fuso horário do servidor para seu aplicativo web:

1. No hello portal do Azure, na sua assinatura do serviço de aplicativo, vá toohello **configurações de aplicativo** menu.
2. Em **Configurações do aplicativo**, adicionar essa configuração:
    * Chave = WEBSITE_TIME_ZONE
    * Valor = *Olá fuso horário desejado*
3. Selecione **Salvar**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Por que meus WebJobs contínuos às vezes falham?

Por padrão, os aplicativos Web serão descarregados se estiverem ociosos por um período de tempo definido. Isso permite que o sistema Olá conservar recursos. Nos planos básico e padrão, você pode ativar Olá **AlwaysOn** configuração tookeep Olá web aplicativo carregado todo o tempo de saudação. Se seu aplicativo web é executado trabalhos Web contínuos, você deve ativar **AlwaysOn**, ou Olá trabalhos Web pode não ser executados com segurança. Para obter mais informações, consulte [Criar um WebJob de execução contínua](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Como obter endereço IP da saída Olá meu aplicativo web?

lista de saudação tooget de saída endereços IP para seu aplicativo web:

1. No hello portal do Azure, na folha seu aplicativo web, vá toohello **propriedades** menu.
2. Pesquisar **endereços IP de saída**.

saudação de lista de endereços IP de saída é exibida.

Se seu site estiver hospedado em um ambiente de serviço de aplicativo para o PowerApps, toolearn como tooget seu endereço IP de saída, consulte [endereços de rede de saída](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Como obter um endereço IP de entrada dedicado ou reservado para meu aplicativo Web?

tooset um endereço IP dedicado ou reservado para chamadas de entrada feitas tooyour site de aplicativo do Azure, instale e configure um certificado SSL com base em IP.

Observe que toouse dedicado ou endereço IP reservado para chamadas de entrada, o plano de serviço de aplicativo deve estar em um plano de serviço básico ou superior.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Pode exportar o meu toouse do certificado de serviço de aplicativo fora do Azure, como para um site hospedado em outro lugar? 

Certificados de Serviço de Aplicativo são considerados recursos do Azure. Eles não são toouse pretendido fora de seus serviços do Azure. Você não pode exportá-los toouse fora do Azure. Para obter mais informações, consulte [Perguntas frequentes para certificados de Serviço de Aplicativo e domínios personalizados](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Posso exportar meu toouse do certificado de serviço de aplicativo com outros serviços de nuvem do Azure?

portal de saudação fornece uma experiência de primeira classe para implantar um certificado de serviço de aplicativo por meio de aplicativos de serviço do Azure Key Vault tooApp. No entanto, podemos tem recebido solicitações de clientes toouse esses certificados fora Olá plataforma do serviço de aplicativo, por exemplo, com as máquinas virtuais do Azure. toolearn como toocreate uma cópia local do PFX de seu serviço de aplicativo de certificado, você pode usar o certificado de saudação com outros recursos do Azure, consulte [criar uma cópia local do PFX de um certificado de serviço de aplicativo](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Para obter mais informações, consulte [Perguntas frequentes para certificados de Serviço de Aplicativo e domínios personalizados](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Por que vejo a mensagem de saudação "Foi parcialmente bem-sucedida" quando tento tooback o meu aplicativo web?

Uma causa comum de falha de backup é que alguns arquivos estão em uso pelo aplicativo hello. Arquivos que estão em uso são bloqueados enquanto você executa o backup de saudação. Isso impede a realização de backup desses arquivos e pode resultar em um status "Foi parcialmente bem-sucedida". Você pode potencialmente evitar que isso ocorra, excluindo arquivos de saudação do processo de backup. Você pode escolher tooback backup apenas o que é necessário. Para obter mais informações, consulte [Backup apenas Olá partes importantes do seu site com aplicativos web do Azure](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Como remover um cabeçalho de resposta HTTP de Olá?

tooremove cabeçalhos Olá Olá resposta HTTP, atualizar o arquivo. config do site. Para obter mais informações, consulte [Remover cabeçalhos de servidor padrão em seus sites do Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>O Serviço de Aplicativo é compatível com o PCI Standard 3.0 e 3.1?

Atualmente, Olá recurso de aplicativos Web do serviço de aplicativo do Azure está em conformidade com a versão de PCI dados segurança padrão (DSS) 3.0 nível 1. PCI DSS versão 3.1 está em nosso roteiro. Planejamento já está em andamento para como a adoção do padrão mais recente Olá continuará.

A certificação de versão 3.1 PCI DSS requer a desabilitação do protocolo TLS (TLS) 1.0. Atualmente, desabilitar o TLS 1.0 não é uma opção para a maioria dos planos de Serviço de Aplicativo. No entanto, se você usar o ambiente de serviço de aplicativo ou está disposto toomigrate tooApp sua carga de trabalho ambiente de serviço, você pode obter maior controle do seu ambiente. Isso envolve desabilitar o TLS 1.0 entrando em contato com o suporte do Azure. Olá futuro próximo, estamos planejando toomake toousers de acessível essas configurações.

Para obter mais informações, consulte [Conformidade do aplicativo web do Serviço de Aplicativo do Microsoft Azure com o PCI Standard 3.0 e 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Como usar o ambiente e slots de implantação de preparo de saudação?

Nos planos Standard e Premium do serviço de aplicativo, quando você implantar seu aplicativo de web tooApp serviço, você pode implantar tooa slot de implantação separado em vez de slot de produção toohello padrão. Os slots de implantação são aplicativos Web dinâmicos com seus próprios nomes de host. Elementos de conteúdo e configuração de aplicativo da Web podem ser trocados entre os dois slots de implantação, incluindo o slot de produção de hello.

Para obter mais informações sobre como usar os slots de implantação, consulte [Configurar um ambiente de preparo no Serviço de Aplicativo](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Como acessar e examine os logs de WebJob?

logs de trabalho Web tooreview:

1. Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecione Olá WebJob.
3. Selecione Olá **alternar saída** botão.
4. arquivo de saída toodownload hello, selecione Olá **baixar** link.
5. Para execuções individuais, selecione **Invocar individuais**.
6. Selecione Olá **alternar saída** botão.
7. Selecione Olá link de download.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Estou tentando toouse híbrida conexões com o SQL Server. Por que vejo a mensagem de saudação do "System. OverflowException: operação aritmética resultou em um estouro"?

Se você usar conexões híbridas tooaccess do SQL Server, uma atualização do Microsoft .NET em 10 de maio de 2016, pode causar toofail de conexões. Você verá esta mensagem:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Resolução

Estamos trabalhando tooupdate toofix do Gerenciador de Conexão híbrida esse problema. Para soluções alternativas, consulte [erro de conexões híbridas com o SQL Server: System. OverflowException: operação aritmética resultou em um excesso](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Como adicionar ou editar uma regra de regravação de URL?

tooadd ou editar uma regra de regravação de URL:

1. Configure o Gerenciador de serviços de informações da Internet (IIS) para que ele se conecta tooyour aplicativo do serviço de aplicativo web. toolearn como tooconnect serviço tooApp do Gerenciador do IIS, consulte [administração remota de sites do Azure usando o Gerenciador do IIS](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. No Gerenciador do IIS, adicione ou edite uma regra de regravação de URL. toolearn como tooadd ou editar uma URL rewrite regra, consulte [criar regras de reescrita de URL Olá reescreva módulo](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Como controlar o tráfego de entrada tooApp serviço?

No nível de site hello, você tem duas opções para controlar o tráfego de entrada tooApp serviço:

* Ative restrições de IP dinâmico. toolearn como tooturn em restrições de IP dinâmico, consulte [restrições de IP e domínio para sites do Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Ative a Segurança de Módulo. toolearn como tooturn no módulo de segurança, consulte [ModSecurity firewall do aplicativo web em sites do Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Se você usar o ambiente de Serviço de Aplicativo, você pode usar o [firewall Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Como bloquear portas em um aplicativo web do Serviço de Aplicativo?

Saudação do serviço de aplicativo compartilhado ambiente de locatário, não é possível tooblock portas devido à natureza de saudação da infraestrutura de saudação. As portas TCP 4016, 4018 e 4020 também podem ser abertas para depuração remota do Visual Studio.

No ambiente de Serviço de Aplicativo, você tem controle total sobre o tráfego de entrada e saído. Você pode usar grupos de segurança de rede toorestrict ou bloquear portas específicos. Para obter mais informações sobre o ambiente de Serviço de Aplicativo, consulte [apresentando o ambiente de Serviço de Aplicativo](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Como capturar um rastreamento F12?

Você tem duas opções para capturar um rastreamento F12:

* Rastreamento de HTTP F12
* Saída do console F12

### <a name="f12-http-trace"></a>Rastreamento de HTTP F12

1. No Internet Explorer, vá tooyour site. É importante toosign antes de que Olá próximas etapas. Caso contrário, Olá F12 rastreamento captura dados confidenciais de entrada.
2. Pressione F12.
3. Verifique se esse Olá **rede** guia é selecionada e, em seguida, selecione Olá verde **reproduzir** botão.
4. Olá etapas que reproduza o problema de saudação.
5. Selecione Olá vermelho **parar** botão.
6. Selecione Olá **salvar** botão (ícone de disco) e, em seguida, salve o arquivo HAR de saudação (no Internet Explorer e borda) *ou* arquivo HAR de saudação e, em seguida, selecione **Salvar como HAR com conteúdo** ( no Chrome).

### <a name="f12-console-output"></a>Saída do console F12

1. Selecione Olá **Console** guia.
2. Para cada guia que contém itens de maior que zero, selecione a guia de saudação (**erro**, **aviso**, ou **informações**). Se guia Olá não estiver selecionado, o ícone de guia de hello está cinza ou preto quando você move o cursor Olá longe-lo.
3. Na área de mensagem de saudação do painel de saudação e, em seguida, selecione **copiar todos os**.
4. Saudação de colar texto copiado em um arquivo e, em seguida, salve o arquivo hello.

tooview um arquivo HAR, você pode usar o hello [visualizador HAR](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Por que recebo um erro quando tento tooconnect um aplicativo de serviço web aplicativo tooa rede virtual que está conectada tooExpressRoute?

Se você tentar tooconnect uma web do Azure aplicativo tooa rede virtual que tenha se conectado tooAzure rota expressa, ele falha. Olá seguinte mensagem será exibida: "O Gateway não é um gateway de VPN."

No momento, você não pode ter ponto a site VPN conexões tooa rede virtual que está conectada tooExpressRoute. Uma VPN de ponto para site e ExpressRoute não podem coexistir para Olá mesma rede virtual. Para obter mais informações, consulte [Limites e limitações de conexões VPN site a site e ExpressRoute](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Como se conectar uma serviço de aplicativo web aplicativo tooa rede virtual que tem um gateway de (baseado em políticas) roteamento estático?

No momento, não há suporte para se conectar a uma serviço de aplicativo web aplicativo tooa rede virtual que tem um gateway de (baseado em políticas) roteamento estático. Se sua rede virtual de destino já existir, ele deve ter habilitado, com um gateway de roteamento dinâmico, para que possa ser conectada tooan aplicativo VPN de ponto para site. Se o gateway estiver definido toostatic roteamento, você não pode ativar uma VPN ponto a site. 

Para obter mais informações, consulte [Integrar um aplicativo a uma rede virtual do Azure](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>Em meu Ambiente do Serviço de Aplicativo, por que só posso criar um Plano do Serviço de Aplicativo, embora tenha dois processadores disponíveis?

tooprovide tolerância a falhas, o ambiente de serviço de aplicativo requer que cada pool de trabalho precisa de pelo menos um recurso de computação adicionais. recursos de computação adicionais Olá não podem ser atribuído a uma carga de trabalho.

Para obter mais informações, consulte [como toocreate um ambiente de serviço de aplicativo](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Por que vejo tempos limite quando tento toocreate um ambiente de serviço de aplicativo?

Às vezes, a criação de um Ambiente do Serviço de Aplicativo falhará. Nesse caso, você pode ver Olá erro no hello que dos logs de atividades a seguir:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve isso, certifique-se de que nenhuma das Olá seguintes condições for verdadeira:
* subrede Olá é muito pequeno.
* Olá sub-rede não está vazia.
* Rota expressa impede que os requisitos de conectividade de rede de saudação de um ambiente de serviço de aplicativo.
* Um grupo de segurança de rede incorreta impede que os requisitos de conectividade de rede de saudação de um ambiente de serviço de aplicativo.
* O túnel forçado é ativado.

Para obter mais informações, consulte [Problemas frequentes ao implantar (criar) um novo Ambiente do Serviço de Aplicativo do Azure](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Por que não consigo excluir meu plano do Serviço de Aplicativo?

Se todos os aplicativos do serviço de aplicativo associados a saudação plano de serviço de aplicativo, você não pode excluir um plano de serviço de aplicativo. Antes de excluir um plano de serviço de aplicativo, remova todos os aplicativos de serviço de aplicativo associados Olá plano de serviço de aplicativo.

## <a name="how-do-i-schedule-a-webjob"></a>Como agendar um WebJob?

Você pode criar um WebJob agendado usando expressões CRON:

1. Crie um arquivo settings.job.
2. Neste arquivo JSON, inclua uma propriedade de agendamento usando uma expressão Cron: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Para obter mais informações sobre WebJobs agendados, consulte [Criar um WebJob agendado usando uma expressão Cron](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Como executar testes de penetração para meu aplicativo de Serviço de Aplicativo?

teste de penetração tooperform, [enviar uma solicitação](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Como configurar um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo usando o Gerenciador de Tráfego?

toolearn como toouse um nome de domínio personalizado com um aplicativo de serviço de aplicativo que usa o Azure Traffic Manager para balanceamento de carga, consulte [configurar um nome de domínio personalizado para um aplicativo web do Azure com o Gerenciador de tráfego](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Meu certificado de Serviço de Aplicativo está sinalizado para fraude. Como resolver isso?

Durante a verificação de domínio de saudação de uma compra de certificado do serviço de aplicativo, você poderá ver a seguinte mensagem de saudação:

"Seu certificado foi sinalizado para uma possível fraude. solicitação de saudação atualmente está sendo avaliada. Se o certificado de saudação não se tornará utilizável dentro de 24 horas, entre em contato com o suporte do Azure."

Como mensagem de saudação indica, esse processo de verificação de fraude pode levar até too24 horas toocomplete. Durante esse tempo, você continuará a mensagem de saudação do toosee.

Se seu certificado de serviço de aplicativo continuar tooshow esta mensagem após 24 horas, execute Olá script do PowerShell a seguir. saudação de contatos de script Hello [provedor certificate](https://www.godaddy.com/) problema de saudação tooresolve diretamente.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Como funcionam a autenticação e autorização no Serviço de Aplicativo?

Para obter documentação detalhada para autenticação e autorização no Serviço de Aplicativo, consulte [Segurança do Serviço de Aplicativo](../app-service/app-service-security-readme.md). documentação de saudação também tem informações sobre como configurar o serviço de aplicativo toouse vários identificam entradas do provedor:
* [Active Directory do Azure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Conta da Microsoft](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Como redirecionar a padrão hello *. domínio personalizado do aplicativo do Azure web toomy domínio azurewebsites.net?

Quando você cria um novo site por meio de aplicativos Web no Azure, um padrão *sitename*. domínio azurewebsites.net recebe tooyour site. Se você adicionar um site de tooyour do nome de host personalizado e não quiser que os usuários toobe capaz de tooaccess padrão *. azurewebsites.net de domínio, você pode redirecionar a URL da saudação padrão. toolearn como tooredirect todos os tráfego do seu domínio do site padrão domínio tooyour personalizado, consulte [saudação padrão domínio tooyour personalizado domínio de redirecionamento em aplicativos web do Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Como determinar qual versão do .NET versão está instalada no Serviço de Aplicativo?

Olá mais rápida maneira toofind Olá versão do Microsoft .NET é instalado no serviço de aplicativo está usando o console do Kudu Olá. Você pode acessar o console de Kudu de saudação do portal de saudação ou usando a URL de saudação do seu aplicativo de serviço de aplicativo. Para obter instruções detalhadas, consulte [Determine Olá instalado a versão do .NET no serviço de aplicativo](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Por que o dimensionamento automático não está funcionando conforme o esperado?

Se Azure AutoEscala não expandida em ou expandida de instância de aplicativo web hello conforme o esperado, talvez você esteja executando em um cenário em que podemos escolher intencionalmente não tooscale tooavoid um loop infinito devido muito "oscilando". Isso geralmente acontece quando não houver uma margem suficiente entre os limites de escalabilidade horizontal e escala no hello. toolearn como tooavoid "oscilando" e tooread sobre outras práticas recomendadas de dimensionamento automático, consulte [práticas recomendadas de dimensionamento automático](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Por que o dimensionamento automático, às vezes, dimensiona apenas parcialmente?

Dimensionamento automático é acionado quando métricas excedem os limites pré-configurados. Às vezes, você poderá notar que capacidade Olá é preenchida apenas parcialmente toowhat em comparação com o esperado. Isso pode ocorrer quando o número de saudação de instâncias não está disponível. Nesse cenário, AutoEscala parcialmente preenchido com o número de instâncias disponíveis hello. Dimensionamento automático, em seguida, executa Olá rebalanceie lógica tooget mais capacidade. Aloca Olá restantes instâncias. Observe que isso pode levar alguns minutos.

Se você não vir o número esperado de saudação de instâncias após alguns minutos, pode ser porque a recarga parcial Olá foi suficiente métricas de saudação toobring dentro dos limites de saudação. Ou então, dimensionamento automático pode ter reduzida porque atingiu o limite inferior de métricas hello.

Se nenhuma dessas condições se aplicam e Olá o problema persistir, envie uma solicitação de suporte.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Como ativar a compactação HTTP para o conteúdo?

tooturn na compactação para tipos de conteúdo estáticos e dinâmicos, adicione Olá código toohello nível do aplicativo Web. config a seguir:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Você também pode especificar dinâmico específico hello e tipos de MIME estático que você deseja toocompress. Para obter mais informações, consulte nossa resposta tooa fórum pergunta [httpCompression configurações em um site do Azure simple](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Como migrar de um ambiente de local tooApp serviço?

toomigrate sites do Windows e Linux tooApp de servidores de web Service, você pode usar Assistente de migração do serviço de aplicativo do Azure. ferramenta de migração de saudação cria bancos de dados e aplicativos web no Azure, conforme necessário e, em seguida, publica o conteúdo de saudação. Para saber mais, consulte [Assistente de Migração do Serviço de Aplicativo do Azure](https://www.movemetothecloud.net/).
