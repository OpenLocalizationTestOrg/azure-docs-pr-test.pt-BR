---
title: aaaAzure perguntas Frequentes do IoT Suite | Microsoft Docs
description: Perguntas frequentes sobre o IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Perguntas frequentes sobre o IoT Suite

Consulte também, Olá fábrica conectado específico [perguntas frequentes sobre](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Onde posso encontrar o código-fonte Olá para soluções de saudação pré-configurado?

código-fonte Olá é armazenado no hello repositórios GitHub a seguir:
* [Solução pré-configurada de monitoramento remoto][lnk-remote-monitoring-github]
* [Solução pré-configurada de manutenção preditiva][lnk-predictive-maintenance-github]
* [Solução pré-configurada de fábrica conectada](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Como atualizar o toohello versão mais recente do remoto solução pré-configurada monitoramento Olá usa Olá recursos de gerenciamento de dispositivo do IoT Hub?

* Se você implantar uma solução pré-configurada do site de https://www.azureiotsuite.com/ hello, sempre implanta uma nova instância da versão mais recente de saudação de solução de saudação.
* Se você implantar uma solução pré-configurada usando a linha de comando hello, você pode atualizar uma implantação existente com o novo código. Consulte [implantação de nuvem] [ lnk-cloud-deployment] em Olá GitHub [repositório][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Como adicionar suporte para um novo dispositivo método toohello solução pré-configurada de monitoramento remoto?

Consulte a seção Olá [adicionar suporte para um novo simulador de toohello método] [ lnk-add-method] em Olá [personalizar uma solução pré-configurada] [ lnk-customize] artigo.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>dispositivo simulado Hello está ignorando as alterações de propriedade desejada, por que?
Em Olá monitoramento remoto pré-configurado solução, Olá simulado dispositivo código só usa Olá **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** propriedades desejadas Olá tooupdate relatado propriedades. Todas as outras solicitações de alteração de propriedade desejadas são ignoradas.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Meu dispositivo não aparecer na lista de saudação de dispositivos no painel da solução hello, por que?

lista de saudação de dispositivos no painel de solução de saudação usa uma lista de saudação do tooreturn de consulta de dispositivos. Atualmente, uma consulta não pode retornar mais de 10 mil dispositivos. Tente fazer os critérios de pesquisa de saudação da consulta mais restritivo.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Qual é a diferença de saudação entre a exclusão de um grupo de recursos no hello Azure portal e clicando em Excluir em uma solução pré-configurada em azureiotsuite.com?

* Se você excluir a solução Olá pré-configurado no [azureiotsuite.com][lnk-azureiotsuite], exclua todos os recursos de saudação que foram provisionados quando você criou a solução Olá pré-configurado. Se você adicionou o grupo de recursos de toohello recursos adicionais, esses recursos também serão excluídos. 
* Se você excluir o grupo de recursos Olá Olá [portal do Azure][lnk-azure-portal], você apenas excluir recursos, Olá desse grupo de recursos. Você também precisa aplicativo de Active Directory do Azure hello toodelete associado com a solução Olá pré-configurado no hello [portal clássico do Azure][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Quantas instâncias do Hub IoT posso provisionar em uma assinatura?

Por padrão, você pode provisionar [10 Hubs IoT por assinatura][link-azuresublimits]. Você pode criar um [tíquete de suporte do Azure] [ link-azuresupportticket] tooraise esse limite. Como resultado, desde que cada solução pré-configurada de provisiona um novo IoT Hub, você só pode provisionar o too10 pré-configurado soluções em uma determinada assinatura. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Quantas instâncias do Azure Cosmos DB posso provisionar em uma assinatura?

Cinquenta. Você pode criar um [tíquete de suporte do Azure] [ link-azuresupportticket] tooraise esse limite, mas, por padrão, você só pode provisionar 50 instâncias de banco de dados do Cosmos por assinatura. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Quantas APIs do Bing Mapas Gratuitas posso provisionar em uma assinatura?

Duas. Você só pode criar dois Bing Mapas de Transações Internas de Nível 1 para planos Enterprise em uma assinatura do Azure. solução de monitoramento remoto Olá é configurada por padrão com o plano de saudação interno transações de nível 1. Como resultado, você só pode provisionar o tootwo soluções em uma assinatura sem modificações de monitoramento remoto.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>Tenho uma implantação de solução de monitoramento remoto com um mapa estático, como posso adicionar um mapa interativo do Bing?

1. Obtenha a QueryKey da API do Bing Mapas para Empresas no [Portal do Azure][lnk-azure-portal]: 
   
   1. Navegue toohello grupo de recursos onde a API do Bing Maps para a empresa está Olá [portal do Azure][lnk-azure-portal].
   2. Clique em **Todas as Configurações** e em **Gerenciamento de Chaves**. 
   3. Você pode ver duas chaves: **MasterKey** e **QueryKey**. Copiar valor Olá **QueryKey**.
      
      > [!NOTE]
      > Você não tem uma conta da API do Bing Maps para Empresa? Criar um no hello [portal do Azure] [ lnk-azure-portal] clicando + novo, procurando a API do Bing Maps para Enterprise e siga solicita toocreate.
      > 
      > 
2. Suspenso código mais recente de saudação do hello [Azure-IoT-monitoramento remoto][lnk-remote-monitoring-github].
3. Executar um local ou seguindo as diretrizes de implantação de linha de comando de saudação na pasta de /docs/ Olá no repositório de saudação de implantação de nuvem. 
4. Depois que você tiver executado um local ou nuvem de implantação, procure na pasta raiz para hello *. config arquivo criado durante a implantação. Abra esse arquivo em um editor de texto. 
5. Alteração Olá linha tooinclude valor de saudação que você copiou de seu **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>Posso criar uma solução pré-configurada se possuo o Microsoft Azure para DreamSpark?

Atualmente, você não pode criar uma solução pré-configurada com uma conta do [Microsoft Azure para DreamSpark][lnk-dreamspark]. No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Poderei criar uma solução pré-configurada se eu tiver uma assinatura do CSP (Provedor de Soluções na Nuvem)?

Atualmente, não é possível criar uma solução pré-configurada com uma assinatura do CSP (Provedor de Soluções na Nuvem). No entanto, você pode criar uma [conta de avaliação gratuita do Azure][lnk-30daytrial] em apenas alguns minutos que permite a você criar uma solução pré-configurada.

### <a name="how-do-i-delete-an-aad-tenant"></a>Como posso excluir um locatário do AAD?

Veja a postagem do blog de Eric Golpe, [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant] (Passo a passo da exclusão de um locatário do Azure AD).

### <a name="next-steps"></a>Próximas etapas

Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:

* [Visão geral da solução pré-configurada de manutenção preditiva][lnk-predictive-overview]
* [Visão geral da solução pré-configurada de fábrica conectada](iot-suite-connected-factory-overview.md)
* [Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
