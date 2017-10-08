---
title: aaaDeployment perguntas frequentes para aplicativos web do Azure | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre implantação para recursos de aplicativos Web de saudação do serviço de aplicativo do Azure."
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
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Perguntas frequentes sobre implantação de Aplicativos Web no Azure

Este artigo possui respostas toofrequently perguntas frequentes (FAQs) sobre problemas de implantação para Olá [recurso de aplicativos Web do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Estou começando a usar os aplicativos Web do Serviço de Aplicativo. Como fazer para publicar meu código?

Estas são algumas opções para publicar seu código do aplicativo Web:

*   Implante usando o Visual Studio. Se você tiver a solução do Visual Studio hello, projeto de aplicativo web hello e, em seguida, selecione **publicar**.
*   Implante usando um cliente FTP. Olá portal do Azure, download Olá publicará perfil do aplicativo web de saudação que você deseja toodeploy seu código. Em seguida, carregue Olá arquivos too\site\wwwroot usando Olá mesmo publicar credenciais do perfil FTP.

Para obter mais informações, consulte [implantar seu aplicativo tooApp serviço](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Vejo uma mensagem de erro quando tento toodeploy do Visual Studio. Como resolver isso?

Se você vir a seguinte mensagem de saudação, talvez usando uma versão mais antiga do hello SDK: "Erro durante a implantação do recurso 'YourResourceName' no grupo de recursos 'YourResourceGroup': MissingRegistrationForLocation: assinatura de saudação não está registrada para Olá tipo de recurso 'componentes' local Olá 'Central EUA'. Registre de novo para este provedor local de toothis ordem toohave acesso." 

tooresolve este erro, a atualização toohello [SDK mais recente](https://azure.microsoft.com/downloads/). Se você vir essa mensagem e ter Olá SDK mais recente, envie uma solicitação de suporte.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Como posso implantar um aplicativo ASP.NET do Visual Studio tooApp serviço?
<a id="deployasp"></a>

tutorial de saudação [criar seu primeiro aplicativo web ASP.NET no Azure em cinco minutos](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) mostra como toodeploy uma ASP.NET web application tooa web app no serviço de aplicativo usando o Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Quais são Olá diferentes tipos de credenciais de implantação?

O Serviço de Aplicativo dá suporte a dois tipos de credenciais para a implantação local do Git e a implantação de FTP/S. Para obter mais informações sobre como tooconfigure credenciais de implantação, consulte [configurar credenciais de implantação para o serviço de aplicativo](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>O que é a estrutura de arquivo ou diretório de saudação do meu aplicativo do serviço de aplicativo web?

Para obter informações sobre a estrutura do arquivo de saudação do seu aplicativo de serviço de aplicativo, consulte [estrutura de arquivos no Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Como resolver "FTP erro 550 - lá não é suficiente espaço em disco hello" quando tento tooFTP Meus arquivos?

Se você vir essa mensagem, é provável que você está executando em uma cota de disco no plano de serviço Olá para seu aplicativo web. Talvez seja necessário tooscale a camada de serviço superior tooa com base em suas necessidades de espaço em disco. Para obter mais informações sobre planos de preços e limites de recursos, consulte [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Como fazer para configurar a implantação contínua em meu aplicativo Web do Serviço de Aplicativo?

Configure a implantação contínua por meio de vários recursos, incluindo o Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox e outros repositórios Git. Essas opções estão disponíveis no portal de saudação. [Implantação contínua tooApp serviço](app-service-continuous-deployment.md) é um tutorial úteis que explica como tooset a implantação contínua.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Como fazer para solucionar problemas com a implantação contínua do GitHub e do Bitbucket?

Para obter ajuda sobre como investigar problemas com a implantação contínua do GitHub ou do Bitbucket, consulte [Investigando a implantação contínua](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Não consigo toomy site de FTP e publicar meu código. Como resolver isso?

problemas de tooresolve FTP:

1. Verifique se que você está inserindo credenciais e o nome de host correto hello. Para obter informações detalhadas sobre os diferentes tipos de credenciais e como toouse-los, consulte [credenciais de implantação](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Verifique se que as portas FTP de saudação não estão bloqueadas por um firewall. portas de saudação devem ter essas configurações:
    * Porta de conexão de controle FTP: 21
    * Porta de conexão de dados FTP: 989, 10001-10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Como publicar tooApp meu código serviço?

Olá início rápido do Azure é projetado toohelp implantar seu aplicativo usando a pilha de implantação hello e método de sua escolha. Olá toouse início rápido, em Olá portal do Azure, vá muito**configurações** > **implantação de aplicativo**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Por que meu aplicativo às vezes, reinicia após a implantação tooApp serviço?

toolearn sobre circunstâncias Olá sob a qual uma implantação de aplicativo pode resultar em uma reinicialização, consulte [implantação versus problemas de tempo de execução](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Como Olá descreve, o serviço de aplicativo implanta na pasta wwwroot toohello arquivos. Ele nunca reinicia o aplicativo diretamente.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Como fazer para integrar o código do Visual Studio Team Services ao Serviço de Aplicativo?

Você tem duas opções para usar a implantação contínua com o Visual Studio Team Services:

*   Use um projeto Git. Conecte-se por meio do serviço de aplicativo usando as opções de implantação de saudação desse repositório.
*   Use um projeto TFVC (Controle de Versão do Team Foundation). Implante usando o agente de compilação Olá para serviço de aplicativo.

A implantação contínua de código para essas duas opções depende dos fluxos de trabalho existentes do desenvolvedor e dos procedimentos de check-in. Para obter mais informações, consulte estes artigos: 

*   [Implementar a implantação contínua do seu site do Azure de tooan do aplicativo](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Configurar uma conta do Visual Studio Team Services para que ele pode implantar o aplicativo da web de tooa](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Como usar FTP ou FTPS toodeploy tooApp meu aplicativo serviço?

Para obter informações sobre como usar o FTP ou FTPS toodeploy seu tooApp de aplicativo web Service, consulte [implantar seu serviço de tooApp do aplicativo usando o FTP/S](app-service-deploy-ftp.md).
