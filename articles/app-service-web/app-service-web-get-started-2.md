---
title: aplicativo tooyour web primeiro funcionalidade aaaAdd | Microsoft Docs
description: Adicione recursos interessantes tooyour primeiro aplicativo web em alguns minutos.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>Adicionar funcionalidade tooyour primeiro aplicativo web
Em [implantar seu primeiro aplicativo tooAzure da web em cinco minutos](app-service-web-get-started-dotnet.md), você implantou um aplicativo web de exemplo [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md). Neste artigo, você adicionará rapidamente aplicativo de web de tooyour implantado alguns ótimos recursos. Em alguns minutos, você irá:

* impor a autenticação para os usuários
* dimensionar seu aplicativo automaticamente
* receber alertas de desempenho de saudação do aplicativo

Independentemente de qual aplicativo de exemplo implantado no artigo anterior hello, pode acompanhar o tutorial de saudação.

Olá três atividades no tutorial são apenas alguns exemplos de Olá muitos recursos úteis que você obtém quando você colocar o seu aplicativo web no serviço de aplicativo. Muitos dos recursos de saudação estão disponíveis no hello **livre** camada (que é o que seu primeiro aplicativo web está em execução no), e você pode usar o tootry créditos de avaliação, os recursos que exigem mais camadas de preços. Ter certeza de que seu aplicativo web permanece no **livre** camada, a menos que você mude explicitamente tooa diferente de camada de preços.

> [!NOTE]
> Olá web aplicativo criado com a CLI do Azure é executado no **livre** camada, o que permite apenas uma instância compartilhada do VM com as cotas de recursos. Para saber mais sobre o que você obtém com a camada **Gratuita** , confira [Limites do Serviço de Aplicativo](../azure-subscription-service-limits.md#app-service-limits).
> 
> 

## <a name="authenticate-your-users"></a>Autenticar os usuários
Agora, vamos ver como é fácil tooadd autenticação tooyour aplicativo (leituras em [aplicativo de serviço de autenticação/autorização](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)).

1. Na folha de portal Olá para seu aplicativo, que você acabou aberto, clique em **configurações** > **autenticação / autorização**.  
    ![Autenticar - folha de configurações](./media/app-service-web-get-started/aad-login-settings.png)
2. Clique em **na** tooturn na autenticação.  
3. Em **Provedores de Autenticação**, clique em **Azure Active Directory**.  
    ![Autenticar - selecionar AD do Azure](./media/app-service-web-get-started/aad-login-config.png)
4. Em Olá **configurações do Active Directory do Azure** folha, clique em **Express**, em seguida, clique em **Okey**. Olá configurações padrão criar um novo aplicativo do AD do Azure em seu diretório padrão.  
    ![Autenticar - configuração expressa](./media/app-service-web-get-started/aad-login-express.png)
5. Clique em **Salvar**.  
    ![Autenticar - salvar configuração](./media/app-service-web-get-started/aad-login-save.png)
   
    Depois que a alteração de saudação for bem-sucedida, você verá sino de notificação Olá ficar verde, juntamente com uma mensagem amigável.
6. Na folha de portal de saudação do seu aplicativo, clique em Olá **URL** link (ou **procurar** na barra de menus do hello). link de saudação é um endereço HTTP.  
    ![Autenticar - procurar tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    Mas, depois que o aplicativo hello aberta em uma nova guia Olá redirecionamentos de caixa URL várias vezes e termina em seu aplicativo com um endereço HTTPS. O que você está vendo é que você já está registrado no tooyour assinatura do Azure, e você está autenticado automaticamente no aplicativo hello.  
    ![Autenticar - conectado](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    Para se agora é possível abrir uma sessão não autenticada em um navegador diferente, você verá uma tela de logon quando você navega toohello mesma URL.  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    Se você nunca fez nada com o Azure Active Directory, talvez seu diretório padrão não tenha usuários do Azure AD. Nesse caso, provavelmente a única conta Olá lá é Olá conta da Microsoft com sua assinatura do Azure. Que tem por que você estivesse conectado automaticamente no aplicativo toohello em Olá mesmo navegador anteriormente.
    Você pode usar esse mesmo toolog de conta Microsoft em também nesta página de logon.

Parabéns, você estiver autenticando todos os tráfego tooyour web app.

Você pode ter observado em Olá **autenticação / autorização** folha que você pode fazer muito mais, como:

* Habilitar o logon social
* Habilitar várias opções de logon
* Alterar o comportamento padrão de saudação quando pessoas navega pela primeira vez o aplicativo tooyour

Serviço de aplicativo fornece que uma solução turnkey para alguns de autenticação comuns Olá precisa que exige uma lógica de autenticação tooprovide hello.
Para saber mais, veja [Autenticação/Autorização do Serviço de Aplicativo](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

## <a name="scale-your-app-automatically-based-on-demand"></a>Dimensionar seu aplicativo automaticamente com base na demanda
Em seguida, vamos AutoEscala seu aplicativo para que ele automaticamente ajustará capacidade toorespond toouser demanda (leituras em [dimensionar seu aplicativo no Azure](web-sites-scale.md) e [dimensionar a contagem de instância manualmente ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md)).

Com rapidez, você pode dimensionar o aplicativo Web de duas maneiras:

* [Escalar verticalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenha mais CPU, memória, espaço em disco e recursos adicionais como VMs dedicadas, domínios e certificados personalizados, slots de preparação, dimensionamento automático e muito mais. Escalar verticalmente alterando Olá preço do plano de serviço de aplicativo que seu aplicativo pertence.
* [Expansão](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumento Olá número de instâncias VM que executar seu aplicativo.
  Você pode expandir tooas muitos como 50 instâncias, dependendo do tipo de preços.

Sem mais demora, vamos configurar o dimensionamento automático.

1. Primeiro, vamos dimensionar o dimensionamento automático de tooenable. Na folha de portal de saudação do seu aplicativo, clique em **configurações** > **escala backup (plano de serviço de aplicativo)**.  
    ![Escalar verticalmente - folha de configurações](./media/app-service-web-get-started/scale-up-settings.png)
2. Role e selecione Olá **Standard S1** camada, Olá nível mais baixo que dá suporte ao dimensionamento automático (dentro de um círculo na captura de tela), clique em **selecione**.  
    ![Escalar verticalmente - escolher a camada](./media/app-service-web-get-started/scale-up-select.png)
   
    Você concluiu a escala vertical.
   
   > [!IMPORTANT]
   > Esta camada gasta seus créditos de avaliação gratuita. Se você tiver uma conta de pagamento por uso, ela incorre em cobra tooyour conta.
   > 
   > 
3. Em seguida, vamos configurar o dimensionamento automático. Na folha de portal de saudação do seu aplicativo, clique em **configurações** > **expansão (plano de serviço de aplicativo)**.  
    ![Escalar horizontalmente - folha de configurações](./media/app-service-web-get-started/scale-out-settings.png)
4. Alterar **o dimensionamento por** muito**percentual de CPU**. controles deslizantes de saudação sob Olá suspensa atualizar adequadamente. Em seguida, defina um intervalo de **Instâncias** entre **1** e **2**, e um **Intervalo de destino** entre **40** e **80**. Fazer isso digitando nas caixas de saudação ou mover os controles deslizantes de saudação.  
    ![Escalar horizontalmente - configurar o dimensionamento automático](./media/app-service-web-get-started/scale-out-configure.png)
   
    Com base nesta configuração, o aplicativo é escalado horizontalmente de forma automática quando a utilização da CPU é superior a 80% e é escalado verticalmente quando a utilização da CPU é inferior a 40%.
5. Clique em **salvar** na barra de menus do hello.

Parabéns, agora o aplicativo tem o dimensionamento automático.

Você pode ter observado em Olá **configurações de escala** folha que você pode fazer muito mais, como:

* Dimensionar tooa determinado número de instâncias manualmente
* Escalar por outras métricas de desempenho, como percentual de memória ou fila do disco
* Personalizar o comportamento da escala quando uma regra de desempenho é disparada
* Fazer o dimensionamento automático de acordo com uma agenda
* Definir o comportamento de dimensionamento automático para um evento futuro

Para saber mais sobre o dimensionamento do aplicativo, confira [dimensionar seu aplicativo no Azure](web-sites-scale.md). Para obter mais informações sobre o dimensionamento horizontal, consulte [Dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md).

## <a name="receive-alerts-for-your-app"></a>Receber alertas para o aplicativo
Agora que seu aplicativo é o dimensionamento automático, o que acontece quando chega a contagem máxima de instâncias de saudação (2) e CPU estiver acima de utilização desejada (80%)?
Você pode configurar um alerta (leituras em [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform nessa situação, portanto você pode obter mais dimensiona para cima/fora de seu aplicativo, por exemplo. Vamos configurar rapidamente um alerta para esse cenário.

1. Na folha de portal de saudação do seu aplicativo, clique em **ferramentas** > **alertas**.  
    ![Alertas - folha de configurações](./media/app-service-web-get-started/alert-settings.png)
2. Clique em **Adicionar alerta**. Em seguida, no hello **recurso** caixa recurso Olá select que termina com **(serverfarms)**. Esse é seu plano do Serviço de Aplicativo.  
    ![Alertas - adicionar alerta para o plano do Serviço de Aplicativo](./media/app-service-web-get-started/alert-add.png)
3. Especifique o **Nome** como `CPU Maxed`, **Métrica** como **Percentual da CPU** e **Limite** como `90`, em seguida, selecione **Proprietários, colaboradores e leitores de email**, clique em **OK**.   
    ![Alertas - configurar alerta](./media/app-service-web-get-started/alert-configure.png)
   
    Quando o Azure termina de criar alerta hello, você verá ele no hello **alertas** folha.  
    ![Alertas - exibição concluída](./media/app-service-web-get-started/alert-done.png)

Parabéns, agora você está recebendo alertas.

Essa configuração de alerta verifica a utilização da CPU a cada cinco minutos. Se o número ficar acima de 90%, você e qualquer pessoa que estiver autorizada receberão um alerta por email. toosee quem está autorizado tooreceive Olá alertas, vá fazer toohello folha de portal do seu aplicativo e clique em Olá **acesso** botão.  
![Ver quem recebe alertas](./media/app-service-web-get-started/alert-rbac.png)

Você deve ver que **administradores de assinatura** já estão Olá **proprietário** do aplicativo hello. Esse grupo incluiria se você for administrador de conta de saudação da sua assinatura do Azure (por exemplo, sua assinatura de avaliação). Para saber mais sobre o controle de acesso baseado em função do Azure, confira [Controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).

> [!NOTE]
> As Regras de alerta são recursos do Azure. Para obter mais informações, consulte [Receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
> 
> 

## <a name="next-steps"></a>Próximas etapas
Em seu Olá tooconfigure de maneira alerta, você pode ter observado um conjunto avançado de ferramentas do hello **ferramentas** folha. Aqui, você pode solucionar problemas, monitorar o desempenho, testar vulnerabilidades, gerenciar recursos, interagir com o console VM hello e adicionar extensões úteis. Você está convidado tooclick em cada uma dessas ferramentas toodiscover Olá simples e poderosas ferramentas em dicas seu dedo.

Descubra como toodo mais com o aplicativo implantado. Esta é apenas uma lista parcial:

* [Comprar e configurar um nome de domínio personalizado](custom-dns-web-site-buydomains-web-app.md) - compre um domínio atraente para seu aplicativo Web em vez do domínio *.azurewebsites.net. Ou use um domínio que você já tenha.
* [Configurar ambientes de preparo](web-sites-staged-publishing.md) -implantar seu tooa aplicativo URL de preparo antes de colocá-lo em produção. Atualize o aplicativo Web dinâmico com confiança. Configure uma solução DevOps elaborada com vários slots de implantação.
* [Configurar implantação contínua](app-service-continuous-deployment.md) - integre a implantação de aplicativo em seu sistema de controle de origem. Implante no Azure com cada confirmação.
* [Acessar recursos locais](web-sites-hybrid-connection-get-started.md) - acesse um banco de dados local existente ou um sistema CRM.
* [Fazer backup de seu aplicativo](web-sites-backup.md) – configure o backup e a restauração para seu aplicativo Web. Prepare-se para falhas inesperadas e recupere-se delas.
* [Habilitar logs de diagnóstico](web-sites-enable-diagnostic-log.md) -Olá leitura IIS logs de rastreamentos de aplicativo ou do Azure. Leia-os em um fluxo, baixe-os ou porte-os para o [Application Insights](../application-insights/app-insights-overview.md) para análise turn key.
* [Verificar seu aplicativo em busca de vulnerabilidades](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) -
  Verificar seu aplicativo Web em busca de ameaças modernas usando o serviço fornecido pelo [Tinfoil Security](https://www.tinfoilsecurity.com/).
* [Executar trabalhos em segundo plano](../azure-functions/functions-overview.md) - execute trabalhos de processamento de dados, relatórios, etc.
* [Saber como funciona o Serviço de Aplicativo](../app-service/app-service-how-works-readme.md)

