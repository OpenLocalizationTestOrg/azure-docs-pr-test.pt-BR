---
title: "aaaMigrate de serviços móveis tooan aplicativo móvel do serviço de aplicativo"
description: "Saiba como tooeasily migrar seu aplicativo de serviços móveis tooan aplicativo móvel do serviço de aplicativo"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Migrar seu tooAzure de serviço móvel do Azure do serviço de aplicativo existente
Com hello [disponibilidade geral do serviço de aplicativo do Azure], serviços móveis do Azure sites podem ser facilmente migrados in-loco tootake aproveitar todos os recursos de saudação do serviço de aplicativo do Azure.  Este documento explica quais tooexpect ao migrar seu site de serviços móveis do Azure tooAzure do serviço de aplicativo.

## <a name="what-does-migration-do"></a>O que migração faz tooyour site
Migração de seu serviço móvel Azure ativa o seu serviço móvel em um [do serviço de aplicativo do Azure] aplicativo sem afetar o código de saudação.  Os hubs de notificação, a conexão de dados do SQL, as configurações de autenticação, os trabalhos agendados e nome de domínio permanecem inalterados.  Clientes móveis usando o seu serviço móvel Azure continuam toooperate normalmente.  Migração reinicia o serviço depois que ele é transferido tooAzure do serviço de aplicativo.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Por que você deve migrar seu site
Microsoft recomenda que você migrar seu serviço móvel do Azure tootake aproveitar Olá recursos do serviço de aplicativo do Azure, incluindo:

* Novos recursos de host, incluindo [Trabalhos Web] e [nomes de domínio personalizados].
* Conectividade tooyour recursos usando local [VNet] além muito[conexões híbridas].
* Monitorando e solucionando problemas com o New Relic ou o [Application Insights].
* Ferramentas do DevOps internas, incluindo [slots de preparo], reversão e testes em produção.
* [Dimensionamento automático], balanceamento de carga e [monitoramento de desempenho].

Para obter mais informações sobre os benefícios de saudação do serviço de aplicativo do Azure, consulte Olá [vs de serviços móveis. Serviço de Aplicativo].

## <a name="before-you-begin"></a>Antes de começar
Antes de começar qualquer trabalho importante no o site, você deve fazer backup dos scripts do serviço móvel e do Banco de Dados SQL.

## <a name="migrating-site"></a>Migrando seus sites
o processo de migração Olá migra todos os sites em uma única região do Azure.

toomigrate seu site:

1. Faça logon no toohello [Portal clássico do Azure].
2. Selecione um serviço móvel na região Olá desejar toomigrate.
3. Clique em Olá **migrar tooApp serviço** botão.

   ![Olá botão de migração][0]
4. Ler a caixa de diálogo serviço tooApp de migração de saudação.
5. Insira o nome de saudação do seu serviço móvel na caixa Olá fornecida.  Por exemplo, se o nome de domínio for contoso.azure mobile.net, em seguida, digite *contoso* na caixa Olá fornecida.
6. Clique o botão de escala de saudação.

Monitorar o status de saudação de migração Olá no monitor de atividade de saudação. O site está listado como *migrando* em Olá Portal clássico do Azure.

  ![Monitor de atividade de migração][1]

Cada migração pode levar de 3 minutos too15 por serviço móvel que está sendo migrado.  O site permanece disponível durante a migração de saudação.
Seu site é reiniciado no final de Olá Olá do processo de migração.  Olá site não está disponível durante o processo de reinicialização hello, que pode durar alguns segundos.

## <a name="finalizing-migration"></a>Olá Finalizando a migração
Planeje tootest seu site de um cliente móvel final Olá Olá do processo de migração.  Certifique-se de que você pode executar todas as ações comuns do cliente sem alterações toohello de cliente móveis.  

### <a name="update-app-service-tier"></a>Selecione um tipo de preço de Serviço de Aplicativo apropriado
Você tem mais flexibilidade no preço depois de migrar tooAzure do serviço de aplicativo.

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **plano do serviço de aplicativo** no menu de configurações de saudação.
5. Clique em Olá **preço** lado a lado.
6. Requisitos de saudação tooyour apropriado, clique **selecione**.  Talvez seja necessário tooClick **exibir todos os** toosee Olá disponível de camadas de preços.

Como ponto de partida, recomendamos Olá níveis a seguir:

| Tipo de Preço do Serviço Móvel | Tipo de Preço do Serviço de Aplicativo |
|:--- |:--- |
| Grátis |F1 Gratuito |
| Basic |B1 Básico |
| Standard |S1 Standard |

Não há considerável flexibilidade na escolha de saudação à direita de preço para o seu aplicativo.  Consulte também[preços do serviço de aplicativo] para obter detalhes completos sobre preços de saudação do seu novo serviço de aplicativo.

> [!TIP]
> camada padrão de serviço do aplicativo Hello contém recursos de toomany de acesso que convém toouse, incluindo [slots de preparo], backups automáticos e o dimensionamento automático.  Confira os novos recursos de saudação lá!
>
>

### <a name="review-migration-scheduler-jobs"></a>Examine Olá migrados Agendador de trabalhos
Os trabalhos do agendador não estarão visíveis até cerca de 30 minutos após a migração.  Trabalhos agendados continuam toorun no plano de fundo de saudação.
tooview os trabalhos agendados depois que elas fiquem visíveis novamente:

1. Faça logon no toohello [portal do Azure].
2. Selecione **procurar >**, digite **agenda** em Olá *filtro* caixa e, em seguida, selecione **Agendador coleções**.

Há um número limitado de trabalhos do agendador gratuito disponíveis após a migração.  Examine o uso e hello [planos de Agendador do Azure].

### <a name="configure-cors"></a>Configure o CORS, se necessário
Compartilhamento de recursos entre origens é uma técnica tooallow tooaccess um site uma API da Web em um domínio diferente.  Se você estiver usando os serviços móveis do Azure com um site associado, você precisa tooconfigure CORS como parte da migração de saudação.  Se você estiver acessando serviços móveis do Azure exclusivamente a partir de dispositivos móveis, CORS não precisa toobe configurada, exceto em casos raros.

As configurações de CORS migradas estão disponíveis como Olá **MS_CrossDomainWhitelist** configuração do aplicativo.  toomigrate toohello seu site recurso CORS de serviço de aplicativo:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **CORS** no menu de saudação API.
5. Insira qualquer origem permitida na caixa de saudação fornecida, pressionando Enter depois de cada um.
6. Depois de sua lista de origens permitidas estiver correta, clique botão de salvar de saudação.

> [!TIP]
> Uma das vantagens de saudação do uso de um serviço de aplicativo do Azure é que você pode executar seu site da web e o serviço móvel em Olá mesmo site.  Para obter mais informações, consulte Olá [próximas etapas](#next-steps) seção.
>
>

### <a name="download-publish-profile"></a>Baixar um novo perfil de publicação
perfil de publicação de saudação do seu site é alterado durante a migração tooAzure do serviço de aplicativo.  Se você pretende toopublish seu site de dentro do Visual Studio, você precisa de um novo perfil de publicação.  toodownload Olá novo perfil de publicação:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. Clique em **Obter perfil de publicação**.

arquivo de PublishSettings Olá é baixado tooyour computador.  Ele é normalmente chamado de *sitename*.PublishSettings.  Saudação de importação publicar configurações no seu projeto existente:

1. Abra o Visual Studio e o seu projeto de Serviço móvel do Azure.
2. Clique com botão direito seu projeto no hello **Solution Explorer** e selecione **publicar...**
3. Clique em **Importar**
4. Clique em **Procurar** e selecione o arquivo de configurações de publicação baixado.  Clique em **OK**
5. Clique em **Conexão validar** tooensure Olá publique o trabalho de configurações.
6. Clique em **publicar** toopublish seu site.

## <a name="working-with-your-site"></a>Trabalhando com seu site após a migração
Começar a trabalhar com seu novo serviço de aplicativo no hello [portal do Azure] após a migração.  Olá seguem algumas observações sobre operações específicas que você usou tooperform em Olá [Portal clássico do Azure], junto com seus equivalentes do serviço de aplicativo.

### <a name="publishing-your-site"></a>Baixar e publicar seu site migrado
O site está disponível via git ou ftp e pode ser publicado novamente com vários mecanismos diferentes, incluindo WebDeploy, TFS, Mercurial, GitHub e FTP.  credenciais de implantação de saudação são migradas com rest de saudação do seu site.  Se você não definir suas credenciais de implantação ou não se lembrar delas, poderá redefini-las:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **credenciais de implantação** em Olá menu de publicação.
5. Insira novas credenciais de implantação Olá nas caixas de saudação fornecidas e clique em botão de salvar hello.

Você pode usar o site de saudação de tooclone essas credenciais com o git ou configurar a implantações automatizadas do GitHub, TFS ou Mercurial.  Para obter mais informações, consulte Olá [documentação de implantação do serviço de aplicativo do Azure].

### <a name="appsettings"></a>Configurações do aplicativo
A maioria das configurações para um serviço móvel migrado está disponível por meio de Configurações do Aplicativo.  Você pode obter uma lista de configurações de aplicativo de saudação do hello [portal do Azure].
tooview ou alterar as configurações de aplicativo:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **configurações de aplicativo** no menu geral hello.
5. Role toohello seção de configurações do aplicativo e localize a configuração do aplicativo.
6. Clique no valor Olá da saudação aplicativo definindo tooedit Olá valor.  Clique em **salvar** toosave valor de saudação.

Você pode atualizar várias configurações de aplicativo no hello simultaneamente.

> [!TIP]
> Há duas configurações de aplicativo com hello mesmo valor.  Por exemplo, você pode ver *ApplicationKey* e *MS\_ApplicationKey*.  Atualizar ambas as configurações de aplicativo no hello simultaneamente.
>
>

### <a name="authentication"></a>Autenticação
Todas as configurações de autenticação estão disponíveis como configurações de aplicativo no site migrado.  tooupdate suas configurações de autenticação, você deve alterar as configurações de aplicativo apropriado.  Olá tabela a seguir mostra as configurações de aplicativo apropriado Olá para o seu provedor de autenticação:

| Provedor | ID do cliente | Segredo do cliente | Outras configurações |
|:--- |:--- |:--- |:--- |
| Conta da Microsoft |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| AD do Azure |**MS\_AadClientID** | |**MS\_AadTenants** |

Observação: **MS\_AadTenants** é armazenado como uma lista separada por vírgulas de domínios de locatário (campos do hello "Locatários permitido" no portal de serviços móveis Olá).

> [!WARNING]
> **Não usar mecanismos de autenticação Olá no menu de configurações de saudação**
>
> Serviço de aplicativo do Azure fornece um separado "sem código" de autenticação e autorização sistema sob Olá *autenticação / autorização* menu Configurações e hello (preterido) *autenticação móveis* opção de menu de configurações de saudação.  Essas opções são incompatíveis com um Serviço Móvel do Azure migrado.  Você pode [atualizar seu site](app-service-mobile-net-upgrading-from-mobile-services.md) tootake vantagem de autenticação do serviço de aplicativo do Azure hello.
>
>

### <a name="easytables"></a>Dados
Olá *dados* guia nos serviços móveis foi substituído pelo *tabelas fácil* dentro Olá portal do Azure.  tooaccess tabelas fácil:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **tabelas fácil** no menu móveis hello.

Você pode adicionar uma tabela clicando Olá **adicionar** botão ou acessar tabelas existentes, clicando em um nome de tabela.  Há várias operações que você pode executar nessa folha, incluindo:

* Alterando as permissões de tabela
* Editando scripts operacionais Olá
* Gerenciar o esquema da tabela Olá
* Excluir tabela Olá
* Limpar o conteúdo da tabela de saudação
* Excluindo linhas específicas de tabela Olá

### <a name="easyapis"></a>API
Olá *API* guia nos serviços móveis foi substituído pelo *APIs fácil* dentro Olá portal do Azure.  tooaccess fácil APIs:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Clique em **APIs fácil** no menu móveis hello.

Suas APIs migrados já estão listados na folha de saudação.  Você também pode adicionar uma API dessa folha.  toomanage uma API específica, clique em Olá API.
Na folha de novo Olá, você pode ajustar as permissões de saudação e editar scripts Olá para Olá API.

### <a name="on-demand-jobs"></a>Trabalhos do Agendador
Todos os trabalhos do Agendador estão disponíveis por meio de saudação seção coleções de trabalhos do Agendador.  tooaccess os trabalhos do Agendador:

1. Faça logon no toohello [portal do Azure].
2. Selecione **procurar >**, digite **agenda** em Olá *filtro* caixa e, em seguida, selecione **Agendador coleções**.
3. Selecione Olá coleção de trabalhos para o seu site.  Ele é chamado de *sitename*-jobs.
4. Clique em **Configurações**.
5. Clique em **Trabalhos do Agendador** em GERENCIAR.

Trabalhos agendados são listados com frequência Olá especificado antes da migração.  Os trabalhos sob demanda são desabilitados.  toorun um trabalho sob demanda:

1. Selecione o trabalho de saudação desejar toorun.
2. Se necessário, clique em **habilitar** tooenable trabalho de saudação.
3. Clique em **Configurações** e em **Agenda**.
4. Selecione uma Recorrência de **Uma vez** e clique em **Salvar**

Os trabalhos sob demanda estão localizados em `App_Data/config/scripts/scheduler post-migration`.  É recomendável que você converta todos os trabalhos sob demanda muito[Trabalhos Web] ou [funções].  Grave novos trabalhos de agendador como [Trabalhos Web] ou [funções].

### <a name="notification-hubs"></a>Hubs de Notificação
Os Serviços Móveis usam os Hubs de Notificação para notificações por push.  Olá configurações do aplicativo a seguir é usadas toolink Olá Hub de notificação tooyour serviço móvel após a migração:

| Configuração de aplicativo | Descrição |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Olá Namespace de Hub de notificação |
| **MS\_NotificationHubName** |Olá, nome do Hub de notificação |
| **MS\_NotificationHubConnectionString** |saudação de cadeia de Conexão do Hub de notificação |
| **MS\_NamespaceName** |Um alias para MS_PushEntityNamespace |

O Hub de notificação é gerenciado por meio de saudação [portal do Azure].  Observe o nome do Hub de notificação hello (você pode descobrir isso usando as configurações de aplicativo hello):

1. Faça logon no toohello [portal do Azure].
2. Selecione **Procurar**> e depois selecione **Hubs de Notificação**
3. Clique no nome do Hub de notificação Olá associado ao serviço móvel hello.

> [!NOTE]
> Se o Hub de Notificação for um tipo "Misto", ele não será visível.  Hubs de notificação do tipo "misto” utilizam Hubs de notificação e recursos do barramento de serviço herdados.  [Converta seus namespaces mistos] antes de continuar.  Após a conclusão da conversão de saudação, seu hub de notificação aparece no hello [portal do Azure].
>
>

Para obter mais informações, examine Olá [Hubs de notificação] documentação.

> [!TIP]
> Recursos de gerenciamento de Hubs de notificação em Olá [portal do Azure] são ainda no modo de visualização.  Olá [Portal clássico do Azure] permanece disponível para gerenciar todos os seus Hubs de notificação.
>
>

### <a name="legacy-push"></a>Configurações de envio por push herdado
Se você configurou o envio em seu serviço móvel antes da introdução Olá em Hubs de notificação, você está usando *envio por push herdado*.  Se estiver usando o envio por push e não vir um Hub de Notificação listado na configuração, é provável que você esteja usando o *envio por push herdado*.  Esse recurso é migrado com todos os outros recursos.  No entanto, é recomendável que você atualize tooNotification Hubs logo depois Olá migração é concluída.

No hello provisório, todas as configurações de envio por push herdado de saudação (com exceção notável de saudação do certificado APNS Olá) estão disponíveis nas configurações de aplicativo.  Atualize o certificado APNS hello, substituindo o arquivo apropriado de saudação no sistema de arquivos de saudação.

### <a name="app-settings"></a>Outras configurações de aplicativo
Olá, configurações de aplicativo adicionais a seguir é migradas do seu serviço móvel e estão disponíveis em *configurações* > *configurações do aplicativo*:

| Configuração de aplicativo | Descrição |
|:--- |:--- |
| **MS\_MobileServiceName** |nome de saudação do seu aplicativo |
| **MS\_MobileServiceDomainSuffix** |prefixo do domínio Hello. ou seja azure-mobile.net |
| **MS\_ApplicationKey** |A chave do seu aplicativo |
| **MS\_MasterKey** |A chave mestre do aplicativo |

chave de aplicativo Hello e a chave mestre são idêntico toohello chaves do aplicativo do seu serviço móvel original.  Em particular, Olá chave de aplicativo é enviada por clientes móveis toovalidate seu uso da API móvel Olá.

### <a name="cliequivalents"></a>Equivalentes de Linha de Comando
Você pode usar mais Olá *azure móvel* comando toomanage seu site de serviços móveis do Azure.  Em vez disso, muitas funções foram substituídas por Olá *site do azure* comando.  Use Olá equivalentes de toofind da tabela de comandos comuns a seguir:

| Comando *Azure Mobile* | Comando *Azure Site* equivalente |
|:--- |:--- |
| locais móveis |lista do local do site |
| lista móvel |lista de sites |
| mobile show *name* |site show *name* |
| mobile restart *name* |site restart *name* |
| mobile redeploy *name* |site deployment redeploy *commitId* *name* |
| mobile key set *name* *type* *value* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile config list *name* |site appsetting list *name* |
| mobile config get *name* *key* |site appsetting show *key* *name* |
| mobile config set *name* *key* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile domain list *name* |site domain list *name* |
| mobile domain add *name* *domain* |site domain add *domain* *name* |
| mobile domain delete *name* |site domain delete *domain* *name* |
| mobile scale show *name* |site show *name* |
| mobile scale change *name* |site scale mode *mode* *name* <br /> site scale instances *instances* *name* |
| mobile appsetting list *name* |site appsetting list *name* |
| mobile appsetting add *name* *key* *value* |site appsetting add *key*=*value* *name* |
| mobile appsetting delete *name* *key* |site appsetting delete *key* *name* |
| mobile appsetting show *name* *key* |site appsetting delete *key* *name* |

Atualização de autenticação ou notificação por push configurações atualizando Olá configuração apropriada do aplicativo.
Edite arquivos e publique seu site via ftp ou git.

### <a name="diagnostics"></a>Diagnóstico e registro em log
Normalmente, o registro em log de diagnóstico está desabilitado em um Serviço de Aplicativo do Azure.  log de diagnóstico tooenable:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. folha de configurações de saudação é aberto por padrão.
4. Selecione **Logs de diagnóstico** no menu de recursos de saudação.
5. Clique em **ON** para Olá logs a seguir: **(sistema de arquivos) de log de aplicativo**, **mensagens de erro detalhadas**, e **o rastreamento de solicitação com falha**
6. Clique em **sistema de arquivos** para registro em log do servidor Web
7. Clique em **Salvar**

tooview Olá logs:

1. Faça logon no toohello [portal do Azure].
2. Selecione **todos os recursos** ou **serviços de aplicativos** , em seguida, clique em nome de saudação do seu serviço móvel migrados.
3. Clique em Olá **ferramentas** botão
4. Selecione **fluxo de Log** sob o menu OBSERVE hello.

Logs são exibidos na janela de saudação como eles são gerados.  Você também pode baixar logs Olá para análise posterior usando suas credenciais de implantação. Para obter mais informações, consulte Olá [log] documentação.

## <a name="known-issues"></a>Problemas conhecidos
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>Excluir um clone de aplicativo móvel migrado causa uma pane do site
Se você clonar seu serviço móvel migrado usando o PowerShell do Azure, em seguida, excluir Olá clone, entrada DNS para o serviço de produção de hello será removida.  O site não esteja acessível de saudação da Internet.  

Resolução: Se você quiser tooclone seu site, fazê-lo por meio do portal hello.

### <a name="changing-webconfig-does-not-work"></a>A alteração de Web.config não funciona
Se você tiver um site ASP.NET, altera toohello `Web.config` arquivo não serão aplicadas.  saudação do serviço de aplicativo do Azure cria um adequado `Web.config` arquivo durante a execução de serviços móveis inicialização toosupport hello.  Você pode substituir determinadas configurações (como cabeçalhos personalizados) usando um arquivo de transformação XML.  Criar um arquivo chamado no `applicationHost.xdt` -este arquivo deve terminar em Olá `D:\home\site` do hello serviço do Azure.  Carregue o arquivo `applicationHost.xdt` por meio de um script de implantação personalizado ou diretamente, usando o Kudu.  a seguir Olá mostra um exemplo de documento:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Para obter mais informações, consulte Olá [XDT transformar exemplos] documentação no GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Os serviços móveis migrados não pode ser adicionados tooTraffic Manager
Quando você cria um perfil do Gerenciador de tráfego, você não pode escolher diretamente um perfil do serviço móvel migrado toohello.  Use um "ponto de extremidade externo".  O ponto de extremidade externo só pode ser adicionado por meio do PowerShell.  Para obter mais informações, confira o [Tutorial do Gerenciador de Tráfego](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Próximas etapas
Agora que seu aplicativo é migrado tooApp serviço, há ainda mais recursos, que você pode usar:

* Implantação [slots de preparo] permitem toostage site de tooyour de alterações e executar A / B teste.
* [Trabalhos Web] fornecem uma substituição para trabalhos agendados sob demanda.
* Você pode [continuamente implantar] seu site por meio da vinculação de seu site tooGitHub, TFS ou Mercurial.
* Você pode usar [Application Insights] toomonitor seu site.
* Atender um site da Web e uma API de celular de Olá mesmo código.

### <a name="upgrading-your-site"></a>Atualizar seu site de serviços móveis tooAzure SDK de aplicativos móveis
* Para projetos de servidor baseado em Node. js, Olá novos [Mobile aplicativos Node. js SDK] fornece vários recursos novos. Por exemplo, você pode agora fazer desenvolvimento local e a depuração, usar qualquer versão do Node. js acima de 0,10 e personalizar com qualquer middleware Express. js.
* Para. Projetos do servidor com base em NET Olá novos [pacotes NuGet do SDK de aplicativos móveis](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) tem mais flexibilidade em dependências do NuGet.  Esses pacotes oferecem suporte à autenticação de serviço de aplicativo novo hello e compõem com qualquer projeto ASP.NET. Para saber mais sobre a atualização, consulte [atualizar seu tooApp existente do .NET Mobile Service serviço](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Preços do Serviço de Aplicativo]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Dimensionamento automático]: ../app-service-web/web-sites-scale.md
[do serviço de aplicativo do Azure]: ../app-service/app-service-value-prop-what-is.md
[documentação de implantação do serviço de aplicativo do Azure]: ../app-service-web/web-sites-deploy.md
[Portal clássico do Azure]: https://manage.windowsazure.com
[portal do Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[planos de Agendador do Azure]: ../scheduler/scheduler-plans-billing.md
[continuamente implantar]: ../app-service-web/app-service-continuous-deployment.md
[Converta seus namespaces mistos]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[nomes de domínio personalizados]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[disponibilidade geral do serviço de aplicativo do Azure]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[conexões híbridas]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[log]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Mobile aplicativos Node. js SDK]: https://github.com/azure/azure-mobile-apps-node
[vs de serviços móveis. Serviço de Aplicativo]: app-service-mobile-value-prop-migration-from-mobile-services.md
[Hubs de notificação]: ../notification-hubs/notification-hubs-push-notification-overview.md
[monitoramento de desempenho]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[slots de preparo]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[Trabalhos Web]: ../app-service-web/websites-webjobs-resources.md
[XDT transformar exemplos]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[funções]: ../azure-functions/functions-overview.md
