---
title: "aaaConfigure os aplicativos web no serviço de aplicativo do Azure"
description: "Como tooconfigure um aplicativo web de serviços de aplicativo do Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Configurar aplicativos Web no Serviço de Aplicativo do Azure
Este tópico explica como tooconfigure um aplicativo web usando Olá [Portal do Azure].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Configurações do aplicativo
1. Em Olá [Portal do Azure], abra folha Olá para o aplicativo web de saudação.
2. Clique em **Todas as Configurações**.
3. Clique em **Configurações do Aplicativo**.

![Configurações do aplicativo][configure01]

Olá **configurações de aplicativo** folha tem configurações agrupadas em várias categorias.

### <a name="general-settings"></a>Configurações gerais
**Versão do Framework**. Configurar essas opções se seu aplicativo usa qualquer um desses frameworks: 

* **.NET framework**: conjunto Olá a versão do .NET framework. 
* **PHP**: versão do conjunto de PHP hello, ou **OFF** toodisable PHP. 
* **Java**: versão do Java Olá Select ou **OFF** toodisable Java. Saudação de uso **contêiner da Web** toochoose opção entre versões Tomcat e Jetty.
* **Python**: versão do Python selecione hello, ou **OFF** toodisable Python.

Por motivos técnicos, habilitar o Java para seu aplicativo desativa opções de saudação .NET, PHP e Python.

<a name="platform"></a>
**Plataforma**. Seleciona se o seu aplicativo é executado em ambiente de 32 ou 64 bits. ambiente de 64 bits Olá requer modo básico ou padrão. Modos Livre e Compartilhado são sempre executados em um ambiente de 32 bits.

**Web Sockets**. Definir **ON** tooenable Olá protocolo WebSocket; por exemplo, se seu aplicativo web usa [ASP.NET SignalR] ou [socket.io].

<a name="alwayson"></a>
**Sempre ativado**. Por padrão, os aplicativos Web serão descarregados se estiverem ociosos por um determinado período de tempo. Isso permite que o sistema Olá conservar recursos. No modo básico ou padrão, você pode habilitar **AlwaysOn** tookeep Olá aplicativo carregado todo o tempo de saudação. Se seu aplicativo executa trabalhos Web contínuos ou execuções de trabalhos Web disparado usando uma expressão CRON, você deve habilitar **AlwaysOn**, ou trabalhos de web hello podem não ser executado com confiança.

**Versão do Pipeline Gerenciado**. Conjuntos de Olá IIS [modo pipeline]. Deixe este definido tooIntegrated (padrão de saudação), a menos que você tenha um aplicativo herdado que requer uma versão mais antiga do IIS.

**Troca Automática**. Se você habilitar a troca automática para um slot de implantação, do serviço de aplicativo automaticamente alternará Olá web aplicativo em produção quando você enviar por push um slot de toothat de atualização. Para obter mais informações, consulte [implantar toostaging slots para aplicativos web no serviço de aplicativo do Azure](web-sites-staged-publishing.md).

### <a name="debugging"></a>Depurando
**Depuração Remota**. Habilita a depuração remota. Quando habilitado, você pode usar o depurador remoto Olá no Visual Studio tooconnect diretamente tooyour de aplicativo da web. A depuração remota permanecerá habilitada por 48 horas. 

### <a name="app-settings"></a>Configurações do aplicativo
Esta seção contém pares de nome/valor que seu aplicativo Web carregará na inicialização. 

* Para aplicativos .NET, essas configurações serão injetadas em sua configuração `AppSettings` em tempo de execução, substituindo as configurações existentes. 
* Os aplicativos PHP, Python, Java e Nó podem acessar essas configurações como variáveis do ambiente em tempo de execução. Para cada configuração de aplicativo, as duas variáveis de ambiente são criadas; um com o nome de saudação especificado pela entrada de configuração de aplicativo hello e outra com um prefixo de APPSETTING_. Ambos contêm Olá mesmo valor.

### <a name="connection-strings"></a>Cadeias de conexão
Cadeia de conexão para recursos vinculados. 

Para aplicativos .NET, essas cadeias de caracteres de conexão serão injetadas nas configuração do .NET `connectionStrings` configurações em tempo de execução, substituindo as entradas existentes onde é igual a chave Olá Olá nome do banco de dados vinculado. 

Para aplicativos PHP, Python, Java e nó, essas configurações estarão disponíveis como variáveis de ambiente em tempo de execução, prefixado com o tipo de conexão de saudação. prefixos de variável de ambiente Olá são da seguinte maneira: 

* SQL Server: `SQLCONNSTR_`
* MySQL: `MYSQLCONNSTR_`
* Banco de Dados SQL: `SQLAZURECONNSTR_`
* Personalizado: `CUSTOMCONNSTR_`

Por exemplo, se uma cadeia de caracteres de conexão MySql foram nomeada `connectionstring1`, ele seria acessado por meio da variável de ambiente Olá `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Documentos padrão
o documento padrão Olá é Olá web página é exibido na URL da raiz de saudação para um site.  Olá primeira correspondência na lista de saudação é usado. 

Os aplicativos Web podem utilizar módulos que rotearão na URL, em vez de atender ao conteúdo estático, nesse caso, não há um documento padrão como tal.    

### <a name="handler-mappings"></a>Mapeamentos de manipulador
Use solicitações de toohandle de processadores de script personalizado para tooadd essa área para extensões de arquivo específico. 

* **Extensão**. Olá toobe de extensão de arquivo é tratado como *.php ou fcgi. 
* **Caminho do Processador de script**. caminho absoluto de saudação do processador de script hello. Toofiles de solicitações que correspondam a extensão de arquivo hello serão processados pelo processador de script hello. Use o caminho de saudação `D:\home\site\wwwroot` diretório de raiz do aplicativo de tooyour toorefer.
* **Argumentos adicionais**. Argumentos de linha de comando opcionais para o processador de script hello 

### <a name="virtual-applications-and-directories"></a>Aplicativos e diretórios virtuais
aplicativos virtuais tooconfigure e diretórios, especifique cada diretório virtual e sua raiz do site correspondente no caminho físico relativo toohello. Opcionalmente, você pode selecionar Olá **aplicativo** caixa de seleção toomark um diretório virtual como um aplicativo.

## <a name="enabling-diagnostic-logs"></a>Habilitar logs de diagnóstico
logs de diagnóstico tooenable:

1. Na folha de saudação para seu aplicativo web, clique em **todas as configurações**.
2. Clique em **Logs de diagnóstico**. 

Opções para gravar os logs de diagnóstico de um aplicativo web que ofereça suporte ao registro em log: 

* **Registro do Aplicativo**. Grava logs de aplicativo toohello sistema de arquivos. O registro em log dura por 12 horas. 

**Nível**. Quando o log de aplicativo é habilitado, essa opção especifica Olá de informações que serão gravado (erro, aviso, informações ou detalhado).

**Log do servidor Web**. Logs são salvos no formato de arquivo de log estendido do hello W3C. 

**Mensagens de erro detalhadas**. Salva arquivos .htm de mensagens de erro detalhadas. Olá arquivos são salvos em /LogFiles/DetailedErrors. 

**Rastreamento de solicitações com falha**. Logs de falha solicitações tooXML arquivos. Olá arquivos são salvos em arquivos de log/W3SVC*xxx*, onde xxx é um identificador exclusivo. Esta pasta contém um arquivo XSL e um ou mais arquivos XML. Verifique a saudação de toodownload-se de que o arquivo XSL, porque ele fornece a funcionalidade para formatar e filtragem de conteúdo Olá Olá dos arquivos de XML.

arquivos de log do tooview hello, você deve criar as credenciais FTP, da seguinte maneira:

1. Na folha de saudação para seu aplicativo web, clique em **todas as configurações**.
2. Clique em **Credenciais de implantação**.
3. Digite um nome de usuário e uma senha.
4. Clique em **Salvar**.

![Definir credenciais de implantação][configure03]

nome de usuário FTP completo Olá é "app\username" onde *aplicativo* é o nome de saudação do seu aplicativo web. Olá nome de usuário está listado na folha de saudação do aplicativo web, em **Essentials**.  

![Credenciais de implantação FTP][configure02]

## <a name="other-configuration-tasks"></a>Outras tarefas de configuração
### <a name="ssl"></a>SSL
no modo Básico ou Padrão, você pode carregar certificados SSL para domínios personalizados. Para obter mais informações, veja [Habilitar HTTPS para um aplicativo Web]. 

tooview os certificados carregados, clique **todas as configurações** > **domínios personalizados e SSL**.

### <a name="domain-names"></a>Nomes de domínio
Adicione nomes de domínio personalizados para seu aplicativo Web. Para obter mais informações, veja [Configurar um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure].

tooview seus nomes de domínio, clique **todas as configurações** > **domínios personalizados e SSL**.

### <a name="deployments"></a>Implantações
* Configure a implantação contínua. Consulte [toodeploy Git usando aplicativos Web no serviço de aplicativo do Azure](web-sites-deploy.md).
* Slots de implantação. Consulte [implantar ambientes tooStaging para aplicativos Web no serviço de aplicativo do Azure].

tooview seus slots de implantação, clique **todas as configurações** > **slots de implantação**.

### <a name="monitoring"></a>Monitoramento
No modo básico ou padrão, você pode testar disponibilidade Olá de pontos de extremidade HTTP ou HTTPS, de locais distribuídos geograficamente de toothree. Teste de monitoramento falhará se Olá código de resposta HTTP é um erro (4xx ou 5xx) ou resposta Olá leva mais de 30 segundos. Um ponto de extremidade é considerado disponível se os testes de monitoramento Olá bem-sucedida de todos os Olá especificou locais. 

Para saber mais, consulte [Como monitorar o status de pontos de extremidade da Web].

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo], onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]
* [Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]
* [Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]
* [Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Portal do Azure]: https://portal.azure.com/
[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-domain.md
[implantar ambientes tooStaging para aplicativos Web no serviço de aplicativo do Azure]: ./web-sites-staged-publishing.md
[Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-ssl.md
[Como monitorar o status de pontos de extremidade da Web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]: ./web-sites-monitor.md
[modo pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[tente do serviço de aplicativo]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
