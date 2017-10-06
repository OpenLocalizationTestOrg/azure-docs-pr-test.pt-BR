---
title: aplicativos web de tecnologias de origem aaaOpen perguntas frequentes sobre o Azure | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre tecnologias de código-fonte aberto no recurso de aplicativos Web de saudação do serviço de aplicativo do Azure."
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
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Perguntas frequentes sobre tecnologias de código aberto para Aplicativos Web do Azure

Este artigo possui respostas toofrequently perguntas frequentes (FAQs) sobre os problemas com tecnologias de código-fonte aberto para Olá [recurso de aplicativos Web do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Meu banco de dados ClearDB está inoperante. Como resolver isso?

Para problemas relacionados ao banco de dados, entre em contato com o [Suporte do ClearDB](https://www.cleardb.com/developers/help/support). 

Para respostas toocommon dúvidas ClearDB, consulte [ClearDB perguntas frequentes sobre](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Por que meu banco de dados ClearDB não estiver listado no portal de Olá?

Se você criar um banco de dados ClearDB Olá [portal do Azure](http://portal.azure.com/), banco de dados de saudação não aparece na Olá [portal clássico do Azure](http://manage.windowsazure.com/). toowork esse problema, você pode vincular manualmente seu aplicativo de web de toohello do banco de dados.

Da mesma forma, se você criar um banco de dados ClearDB Olá [portal clássico do Azure](http://manage.windowsazure.com/), você não verá o banco de dados em Olá [portal do Azure](http://portal.azure.com/). Nesse caso, nenhuma solução alternativa está disponível. 

Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Por que meu banco de dados ClearDB não migrou durante a migração da minha assinatura?

Quando você executar recursos de migração entre assinaturas, serão aplicadas algumas limitações. O banco de dados MySQL ClearDB é um serviço de terceiros e, portanto, não será migrado durante a migração da assinatura do Azure.

Se você não gerencia a migração de saudação do banco de dados MySQL antes de migrar os recursos do Azure, seu banco de dados ClearDB MySQL pode estar indisponível. tooavoid isso, primeiro, migrar manualmente o banco de dados ClearDB e, em seguida, migrar Olá assinatura do Azure para seu aplicativo web.

Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Como ativar PHP log tootroubleshoot problemas PHP?

tooturn registro em log de PHP:

1. Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. No menu superior do hello, selecione **Console depuração** > **CMD**.
3. Selecione Olá **Site** pasta.
4. Selecione Olá **wwwroot** pasta.
5. Selecione Olá  **+**  ícone e, em seguida, selecione **novo arquivo**.
6. Defina o nome do arquivo hello muito**. user.ini**.
7. Selecione o ícone de lápis Olá Avançar muito**. user.ini**.
8. No arquivo hello, adicione este código:`log_errors=on`
9. Selecione **Salvar**.
10. Selecione o ícone de lápis Olá Avançar muito**config.php wp**.
11. Alterar toohello de texto de saudação código a seguir:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Olá portal do Azure, no menu de aplicativo web hello, reiniciar o seu aplicativo web.

Para obter mais informações, consulte [Habilitar logs de erros do WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Como registrar erros do aplicativo Python em aplicativos que são hospedados no Serviço de Aplicativo?

erros de aplicativo do Python toocapture:

1. No hello portal do Azure, em seu aplicativo web, selecione **configurações**.
2. Em Olá **configurações** guia, selecione **configurações de aplicativo**.
3. Em **configurações do aplicativo**, digite Olá par chave/valor a seguir:
    * Chave: WSGI_LOG
    * Valor: D:\home\site\wwwroot\logs.txt (Insira o nome de arquivo da sua escolha)

Agora você verá erros no arquivo de logs de saudação na pasta wwwroot hello.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Como alterar a versão de saudação do hello aplicativo Node. js que é hospedado no serviço de aplicativo?

toochange Olá versão Olá aplicativo Node. js, você pode usar uma saudação as opções a seguir:

*   Olá portal do Azure, usar **configurações do aplicativo**.
    1. No hello portal do Azure, vá tooyour web app.
    2. Em Olá **configurações** folha, selecione **configurações de aplicativo**.
    3. Em **configurações do aplicativo**, você pode incluir WEBSITE_NODE_DEFAULT_VERSION como chave hello e hello versão do Node. js que desejar como valor de saudação.
    4. Vá tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck Olá versão Node. js, digite Olá comando a seguir:  
   ```
   node -v
   ```
*   Modificar o arquivo de iisnode.yml hello. Versão de Node. js Olá alteração no arquivo de iisnode.yml Olá apenas define ambiente de tempo de execução de saudação que iisnode usa. O cmd Kudu e outros ainda usam a versão de Node. js de saudação que está definida no **configurações do aplicativo** em Olá portal do Azure.

    tooset Olá iisnode.yml manualmente, crie um arquivo de iisnode.yml na pasta raiz do aplicativo. No arquivo hello, incluem hello seguinte linha:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Olá iisnode.yml arquivo de conjunto usando Package. JSON durante a implantação do controle de origem.
    Olá processo de implantação de controle do código-fonte do Azure envolve Olá etapas a seguir:
    1. Move o aplicativo web do Azure de toohello conteúdo.
    2. Cria um script de implantação padrão, se não houver um (Deploy, arquivos .deployment) na pasta raiz do Olá web app.
    3. Executa um script de implantação em que ele cria um arquivo iisnode.yml se mencionar versão do Node. js Olá no arquivo de Package. JSON hello > mecanismo`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. arquivo de iisnode.yml Olá tem Olá a seguinte linha de código:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Vejo a mensagem de saudação "Erro ao estabelecer uma conexão de banco de dados" em meu aplicativo WordPress que é hospedado no serviço de aplicativo. Como solucionar isso?

Se você vir esse erro no aplicativo do Azure WordPress, tooenable php_errors.log e Debug, etapas de saudação completa detalhadas em [logs de erros do WordPress habilitar](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Quando Olá logs são habilitados, reproduza o erro Olá e verifique se Olá logs toosee se você estiver executando sem conexões:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Se você vir esse erro nos arquivos de Debug ou php_errors.log, seu aplicativo é excede o número de saudação de conexões. Se você estiver hospedando no ClearDB, verifique o número de saudação de conexões que estão disponíveis no seu [plano de serviço](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Como depurar um aplicativo Node.js que está hospedado no Serviço de Aplicativo?

1.  Vá tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Pasta de logs de aplicativo do vá tooyour (D:\home\LogFiles\Application).
3.  No arquivo de logging_errors.txt hello, verifique se há conteúdo.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Como instalar módulos Python nativos em um aplicativo web do Serviço de Aplicativo ou aplicativo de API?

Alguns pacotes não podem ser instalados usando o pip no Azure. pacote de saudação pode não estar disponível em Olá Python pacote índice ou um compilador pode ser necessário (um compilador não está disponível no computador de saudação que está executando o aplicativo web de saudação no serviço de aplicativo). Para obter informações sobre como instalar os módulos nativos em aplicativos web do Serviço de Aplicativo e aplicativos de API, consulte [Instalar módulos Python no Serviço de Aplicativo](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Como implantar um aplicativo de Django tooApp serviço usando o Git e Olá a nova versão do Python?

Para obter informações sobre como instalar Django, consulte [Implantando um aplicativo de Django tooApp serviço](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Onde estão os arquivos de log do Tomcat Olá localizados?

Para o Azure Marketplace e implantações personalizadas:

* Local da pasta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* Arquivos de interesse:
    * catalina.*aaaa-mm-dd*.log
    * host-manager.*aaaa-mm-dd*.log
    * localhost.*aaaa-mm-dd*.log
    * manager.*aaaa-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log


Para implantações de **Configurações do aplicativo** do portal:

* Local da pasta: D:\home\LogFiles
* Arquivos de interesse:
    * catalina.*aaaa-mm-dd*.log
    * host-manager.*aaaa-mm-dd*.log
    * localhost.*aaaa-mm-dd*.log
    * manager.*aaaa-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Como solucionar problemas de erros de conexão do driver JDBC?

Você poderá ver Olá seguinte mensagem nos logs Tomcat:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

Erro de saudação tooresolve:

1. Remova o arquivo de sqljdbc*.jar de saudação da sua pasta de aplicativo/lib.
2. Se você estiver usando Olá Tomcat ou o Azure Marketplace Tomcat servidor web personalizado, copie essa pasta lib do. jar arquivo toohello Tomcat.
3. Se você estiver habilitando Java do hello portal do Azure (selecione **Java 1.8** > **servidor Tomcat**), cópia Olá sqljdbc.* jar arquivo hello pasta que é aplicativo tooyour paralela. Em seguida, adicione Olá classpath configuração toohello. config a seguir:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Por que vejo erros quando tento toocopy arquivos de log em tempo real?

Se você tentar toocopy arquivos de log em tempo real para um aplicativo Java (por exemplo, Tomcat), você poderá ver esse erro FTP:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

mensagem de erro de saudação poderão variar, dependendo de cliente Olá FTP.

Todos os aplicativos Java tem esse problema de bloqueio. Somente Kudu oferece suporte a baixar este arquivo enquanto o aplicativo hello está sendo executado.

Parando aplicativo de saudação permite acesso FTP toothese de arquivos.

Outra alternativa é toowrite um trabalho Web que é executado em um agendamento e copia esses diretório diferente de tooa de arquivos. Para um projeto de exemplo, consulte Olá [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projeto.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Onde encontrar os arquivos de log Olá para Jetty?

Para o Marketplace e implantações personalizadas, o arquivo de log de saudação está na pasta de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello. Observe que local da pasta Olá depende da versão de saudação do Jetty que você está usando. Por exemplo, o caminho de saudação fornecidas aqui servem para Jetty 9.1.2. Procure jetty_*YYYY_MM_DD*.stderrout.log.

Para implantações de configuração do aplicativo do portais, o arquivo de log hello está em D:\home\LogFiles. Procure jetty_*YYYY_MM_DD*.stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>Posso enviar email de meu aplicativo web do Azure?

Serviço de Aplicativo não tem uma funcionalidade de email interno. Para algumas boas alternativas para enviar email de seu aplicativo, consulte esta [Discussão de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Por que meu site WordPress redirecionar a URL tooanother?

Se você tiver migrado recentemente tooAzure, WordPress pode URL de redirecionamento toohello antigo domínio. Isso é causado por uma configuração no banco de dados do hello MySQL.

WordPress Buddy + é uma extensão de Site do Azure que você pode usar o URL de redirecionamento de saudação tooupdate diretamente no banco de dados de saudação. Para obter mais informações sobre como usar o WordPress Buddy +, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

Como alternativa, se você preferir a URL de redirecionamento do toomanually atualização hello usando consultas SQL ou PHPMyAdmin, consulte [WordPress: redirecionamento de URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Como alterar minha senha de logon do WordPress?

Se você esqueceu sua senha de logon do WordPress, você pode usar o WordPress Buddy + tooupdate-lo. tooreset sua senha, Olá instalar extensão Site WordPress Buddy + do Azure e as etapas de Olá concluída, em seguida, descritas em [WordPress ferramentas e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Não consigo entrar tooWordPress. Como resolver isso?

Se você estiver o WordPress bloqueado depois de instalar recentemente um plug-in, você pode ter um plug-in com defeito. WordPress Buddy + é uma extensão de Site do Azure que podem ajudá-lo desabilitar plug-ins no WordPress. Para obter mais informações, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Como migrar meu banco de dados do WordPress?

Você tem várias opções de migração Olá MySQL banco de dados conectado tooyour WordPress site:

* Desenvolvedores: Saudação de uso [prompt de comando ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Não-desenvolvedores: Usar [WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Como ajudar a proteger melhor o WordPress?

toolearn sobre as práticas recomendadas de segurança para WordPress, consulte [as práticas recomendadas para segurança do WordPress no Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Estou tentando toouse PHPMyAdmin e posso ver a mensagem "Acesso negado". Como resolver isso?

Se o recurso de no aplicativo hello MySQL não está em execução ainda nesta instância do serviço de aplicativo, você poderá enfrentar esse problema. tooresolve Olá problema, tente tooaccess seu site. Isso inicia processos Olá necessárias, incluindo processo Olá MySQL no aplicativo. tooverify que MySQL no aplicativo está em execução, no Explorador de processos, certifique-se de que mysqld.exe é listado em processos de saudação.

Depois de garantir que o MySQL no aplicativo está em execução, tente toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Recebo um erro de HTTP 403 quando tentar tooimport ou exportar meu banco de dados MySQL no aplicativo usando PHPMyadmin. Como resolver isso?

Se você estiver usando uma versão mais antiga do Chrome, talvez você esteja tendo um bug conhecido. problema de saudação tooresolve, tooa atualizar a versão mais recente do Chrome. Além disso, tente usando um navegador diferente, como o Internet Explorer ou borda, onde Olá problema não ocorre.
