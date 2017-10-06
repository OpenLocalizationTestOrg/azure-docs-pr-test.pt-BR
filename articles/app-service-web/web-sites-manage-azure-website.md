---
title: "aaaManage um aplicativo web no serviço de aplicativo do Azure"
description: "Links tooresources para gerenciar um aplicativo web no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Gerenciar um aplicativo Web no Serviço de Aplicativo do Azure
Este tópico contém links tooresources para gerenciar um aplicativo web no [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). O gerenciamento inclui todas as tarefas de saudação que manter seu aplicativo web funcionando sem problemas. 

Em tempo de vida de saudação de um aplicativo web, você executará diversas tarefas de gerenciamento, quando você vai de atualizações, manutenção e operação de toonormal implantação inicial.

Muitas tarefas de gerenciamento de aplicativo da web podem ser executadas em Olá Portal do Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Antes de implantar seu tooproduction de aplicativo web
### <a name="choose-a-tier"></a>Escolha uma faixa
O Serviço de Aplicativo do Azure é oferecido em cinco níveis: Gratuito, Compartilhado, Básico, Padrão e Premium. Para obter informações sobre os recursos de saudação e preços para cada camada, consulte [detalhes de preços](https://azure.microsoft.com/pricing/details/app-service/). 

* [Planos de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) permitem agrupar vários aplicativos web em Olá mesma camada.
* Você sempre pode [alternar as camadas](web-sites-scale.md) após criar seu aplicativo Web.

### <a name="configuration"></a>Configuração
Saudação de uso [Portal do Azure](https://portal.azure.com/) tooset várias opções de configuração. Para obter detalhes, consulte [Configurar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-configure.md). Aqui está uma lista de verificação rápida:

* Selecione **versões de tempo de execução** para .NET, PHP, Java ou Python, se necessário.
* Habilitar **WebSockets** se seu aplicativo web usa o protocolo WebSocket de saudação. (Isto inclui aplicativos que usam o [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Você está executando trabalhos web contínuos? Se estiver, habilite **Sempre ativo**.
* Saudação de conjunto **documento padrão**, como index. HTML.

Adição toothese configurações básicas, convém a seguir Olá tooconfigure:

* **Secure Socket Layer (SSL)** . toouse SSL com um nome de domínio personalizado, você deve obter um SSL de certificados e configurar seu toouse de aplicativo web-lo. Consulte [Habilitar HTTPS para um aplicativo Web no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-ssl.md).
* **Nome de domínio personalizado.** Seu aplicativo Web tem automaticamente um subdomínio em azurewebsites.net. Você pode associar um nome de domínio personalizado, por exemplo, contoso.com. Consulte [Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure](app-service-web-tutorial-custom-domain.md).

Configuração específica de idioma:

* **PHP**: [configurar o PHP em aplicativos Web do Serviço de Aplicativo do Azure](web-sites-php-configure.md).
* **Python**: [configurando o Python com Aplicativos Web do Serviço de Aplicativo do Azure](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Enquanto seu aplicativo Web está em execução
Enquanto seu aplicativo web é executado, você deseja toomake se ele está disponível e que ele é dimensionado toomeet tráfego do usuário. Talvez também seja necessário tootroubleshoot erros.

### <a name="monitoring"></a>Monitoramento
* Por meio de Olá Portal do Azure, você pode [adicionar métricas de desempenho](web-sites-monitor.md) como uso de CPU e o número de solicitações de cliente.
* [Dimensionar seu aplicativo web](web-sites-scale.md) em tootraffic de resposta. Dependendo de sua camada, você pode dimensionar o número de saudação de máquinas virtuais e/ou tamanho Olá Olá de instâncias de VM. Saudação padrão e as camadas Premium, você também pode configurar dimensionamento automático, para que seu aplicativo web é dimensionado automaticamente, em uma cronograma fixo ou em tooload de resposta.  

### <a name="backups"></a>Backups
* Defina [backups automáticos](web-sites-backup.md) de seu aplicativo Web. Saiba mais sobre backups [neste vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Saiba mais sobre opções de saudação para [recuperação de banco de dados](../sql-database/sql-database-business-continuity.md) no banco de dados do SQL Azure.

### <a name="troubleshooting"></a>Solucionar problemas
* Se algo der errado, você pode [solucionar problemas no Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), usando logs de diagnóstico e de depuração na nuvem Olá dinâmica. 
* Fora do Visual Studio, existem vários logs de diagnóstico toocollect maneiras. Consulte [Habilitar o registro de log de diagnóstico para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-enable-diagnostic-log.md).
* Para aplicativos do Node.js, consulte [como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Restaurando dados
* [Restaure](web-sites-restore.md) um aplicativo Web no qual foi realizado o backup anteriormente.

## <a name="when-you-update-your-web-app"></a>Ao atualizar seu aplicativo Web
Se você não habilitou os backups automáticos, você pode criar um [backup manual](web-sites-backup.md).

Considere o uso de uma [implantação em estágios](web-sites-staged-publishing.md). Essa opção permite que você publique atualizações tooa preparação de implantação que executa lado a lado com a implantação de produção. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


