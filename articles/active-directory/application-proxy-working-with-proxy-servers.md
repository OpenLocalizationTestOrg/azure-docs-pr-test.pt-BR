---
title: aaaWork com existente local servidores proxy e o Azure AD | Microsoft Docs
description: Aborda como toowork com existente local servidores proxy.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Trabalhar com servidores proxy locais existentes

Este artigo explica como tooconfigure toowork de conectores de Proxy de aplicativo do Azure Active Directory (AD do Azure) com servidores de proxy de saída. Ele destina-se aos clientes com ambientes de rede que já têm proxies.

Começamos analisando este principais cenários de implantação:
* Configure conectores toobypass os proxies de saída do local.
* Configure conectores toouse tooaccess um proxy de saída Proxy de aplicativo do Azure AD.

Para saber mais sobre como funcionam os conectores, consulte [Noções básicas sobre conectores de proxy de aplicativo do Azure AD](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Configurar o proxy de saída Olá

Se você tiver um proxy de saída em seu ambiente, use uma conta com o proxy de saída tooconfigure Olá permissões apropriadas. Porque o instalador Olá é executado no contexto de saudação do usuário de saudação que está fazendo a instalação Olá, você pode verificar a configuração hello usando o Microsoft Edge ou outro navegador da Internet.

configurações de proxy tooconfigure Olá no Microsoft Edge:

1. Vá muito**configurações** > **configurações avançadas de exibição** > **abrir configurações de Proxy** > **Manual de configuração de Proxy** .
2. Definir **usar um servidor proxy** muito**na**, selecione Olá **não usar Olá proxy para endereços locais (intranet)** caixa de seleção e, em seguida, alterar Olá tooreflect de endereço e porta o servidor de proxy local.
3. Preencha as configurações de proxy necessário de saudação.

   ![Caixa de diálogo para as configurações do proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Ignorar proxies de saída

Conectores têm componentes subjacentes do sistema operacional que fazem solicitações de saída. Esses componentes automaticamente tentam toolocate um servidor proxy na rede de saudação. Eles usam a descoberta automática de Proxy da Web (WPAD), se ele estiver habilitado no ambiente de saudação.

componentes do sistema operacional Olá tentam toolocate um servidor proxy, executando uma pesquisa de DNS para wpad.domainsuffix. Se isso for resolvido no DNS, uma solicitação HTTP é feita toohello IP endereço para WPAD. Essa solicitação se torna o script de configuração de proxy de saudação em seu ambiente. conector de saudação usa esse tooselect um servidor de proxy de saída do script. No entanto, o tráfego do conector pode ainda não passar por, devido às configurações de configuração adicional necessárias no proxy hello.

Você pode configurar Olá conector toobypass seu tooensure de proxy local que usa direcionar toohello de conectividade do Azure services. Recomendamos essa abordagem (se a política de rede permite que ele), pois isso significa que você tenha um menos toomaintain de configuração.

toodisable uso de proxy de saída para o conector Olá, edite o arquivo de C:\Program Files\Microsoft AAD aplicativo Proxy Connector\ApplicationProxyConnectorService.exe.config de saudação e adicionar Olá *system.net* seção mostrada nesse exemplo de código :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure que o serviço de conector Updater Olá também ignora proxy hello, fazer um localizado em C:\Program Files\Microsoft atualizador do conector AAD aplicativo Proxy alteração toohello ApplicationProxyConnectorUpdaterService.exe.config arquivo semelhante.

Ser se cópias de toomake arquivos originais de hello, caso você precise de arquivos. config do toorevert toohello padrão.

## <a name="use-hello-outbound-proxy-server"></a>Usar um servidor proxy de saída Olá

Alguns ambientes exigem que todos os toogo de tráfego de saída por meio de um proxy de saída, sem exceção. Como resultado, ignorar o proxy de saudação não é uma opção.

Você pode configurar Olá conector tráfego toogo por meio do proxy de saída hello, conforme mostrado no diagrama a seguir de saudação:

 ![Configurando o conector toogo de tráfego por meio de um proxy de saída de tooAzure AD Proxy de aplicativo](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Como resultado de ter somente o tráfego de saída, há tooconfigure sem necessidade de acesso por meio de seus firewalls de entrada.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Etapa 1: Configurar conector hello e relacionadas toogo de serviços por meio do proxy de saída Olá

Conforme abordado anteriormente, se WPAD estiver habilitado no ambiente hello e configurado corretamente, conector Olá descobrirá automaticamente toouse de servidor e a tentativa de proxy de saída Olá-lo. No entanto, você pode configurar explicitamente Olá conector toogo por meio de um proxy de saída.

toodo assim, edite Olá C:\Program Files\Microsoft AAD aplicativo Proxy Connector\ApplicationProxyConnectorService.exe.config arquivo e adicione Olá *system.net* seção mostrada nesse exemplo de código. Alterar *proxyserver:8080* tooreflect o nome do servidor proxy local ou o endereço IP e a saudação da porta que ele está escutando.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Em seguida, configure o proxy de Olá Olá atualizador do conector serviço toouse fazendo um arquivo de toohello de alteração semelhante localizado em C:\Program Files\Microsoft AAD aplicativo Proxy do conector Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Etapa 2: Configurar o tráfego de tooallow Olá proxy do conector hello e tooflow serviços relacionados por meio de

Há quatro tooconsider de aspectos no proxy de saída de hello:
* Regras de saída do proxy
* Autenticação do proxy
* Portas do proxy
* Inspeção SSL

#### <a name="proxy-outbound-rules"></a>Regras de saída do proxy
Permitir acesso toohello pontos de extremidade para acesso ao serviço de conector a seguir:

* *.msappproxy.net
* *.servicebus.windows.net

Para o registro inicial, permitir acesso toohello pontos de extremidade a seguir:

* login.windows.net
* login.microsoftonline.com

Se você não pode permitir a conectividade pelo FQDN e precisar toospecify intervalos IP em vez disso, use estas opções:

* Permitir acesso de saída de conector Olá tooall destinos.
* Permitir acesso de saída de conector Olá muito[intervalos IP do datacenter do Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). Olá desafio usando Olá lista de intervalos IP do datacenter do Azure é que ela é atualizada semanalmente. É necessário tooput um processo em vigor tooensure que as regras de acesso são atualizadas.

#### <a name="proxy-authentication"></a>Autenticação do proxy

No momento, não há suporte à autenticação do proxy. Nossa recomendação atual é destinos de Internet de toohello tooallow Olá conector acesso anônimo.

#### <a name="proxy-ports"></a>Portas do proxy

conector de saudação torna as conexões de saída baseada em SSL usando o método de conexão hello. Esse método essencialmente configura um túnel por meio do proxy de saída hello. Configure Olá proxy server tooallow túnel tooports 443 e 80.

>[!NOTE]
>Quando o Barramento de Serviço for executado por HTTPS, ele usará a porta 443. No entanto, por padrão, o barramento de serviço tentativas de conexões TCP diretas e reverterá tooHTTPS somente se a conectividade direta com falha.

tooensure que Olá tráfego também for enviado pelo servidor de proxy de saída de saudação do barramento de serviço, certifique-se de que esse conector Olá não é possível conectar-se diretamente toohello serviços do Azure para portas 9350, 9352 e 5671.

#### <a name="ssl-inspection"></a>Inspeção SSL
Não use inspeção SSL para o tráfego de conector hello, porque ele causa problemas para o tráfego de conector de saudação.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Solucionar problemas do proxy do conector e problemas de conectividade do serviço
Agora você deve ver todo o tráfego que passam por meio do proxy de saudação. Se você tiver problemas, deve ajudar a saudação informações de solução de problemas a seguir.

Olá tooidentify de maneira recomendada e solucionar problemas de conectividade do conector problemas é tootake uma rede de captura no serviço de conector de saudação ao iniciar o serviço do conector hello. Como essa tarefa pode ser um tanto quanto assustadora, vamos observar umas dicas rápidas sobre como capturar e filtrar rastreamentos de rede.

Você pode usar Olá, ferramenta de sua escolha de monitoramento. Para fins de saudação deste artigo, usamos Microsoft Network Monitor 3.4. Você pode [baixá-lo na Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

exemplos de saudação e filtros que usamos na Olá seções a seguir são específico tooNetwork Monitor, mas princípios Olá podem ser aplicadas tooany ferramenta de análise.

### <a name="take-a-capture-by-using-network-monitor"></a>Fazer uma captura usando o Monitor de Rede

toostart uma captura:

1. Abra o Monitor de Rede e clique em **Nova Captura**.
2. Clique em Olá **iniciar** botão.

   ![Janela Monitor de Rede](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Depois de concluir uma captura, clique em Olá **parar** botão tooend-lo.

### <a name="take-a-capture-of-connector-traffic"></a>Fazer uma captura do tráfego do conector

Para solução de problemas iniciais, execute Olá etapas a seguir:

1. De Services. msc, pare o serviço de conector de Proxy de aplicativo do AD do Azure de saudação.
2. Inicie a captura de rede hello.
3. Inicie serviço de conector de Proxy de aplicativo do AD do Azure hello.
4. Pare a captura de rede hello.

   ![Serviço Conector do Proxy de Aplicativo do Azure AD em services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Examinar as solicitações de saudação do servidor de proxy Olá conector toohello

Agora que temos uma captura de rede, você está pronto toofiltê-lo. Olá toolooking de chave no rastreamento de saudação é entender como toofilter Olá capturar.

Um filtro é o seguinte (onde 8080 é a porta de serviço de proxy Olá):

**(http.Request ou http.Response) e tcp.port==8080**

Se você inserir esse filtro Olá **exibir filtro** janela e selecione **aplicar**, ele filtra o tráfego de saudação capturado com base no filtro de saudação.

Olá filtro anterior mostra apenas Olá solicitações e respostas HTTP de porta de proxy de saudação. Para a inicialização do conector em que o conector de saudação é toouse configurado um servidor proxy, filtro Olá mostraria algo assim:

 ![Lista de exemplo das solicitações e respostas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Você agora está procurando especificamente Olá que conectar solicita que mostram a comunicação com o servidor de proxy de saudação. No caso de êxito, você obterá uma resposta HTTP OK (200).

Se você ver outros códigos de resposta, como 407 ou 502, proxy Olá é exigir autenticação ou não permitir o tráfego do hello por algum outro motivo. Neste ponto, você interage com a equipe de suporte do servidor proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Identificar tentativas de conexão TCP com falha

Olá outro cenário comum que pode estar interessado em é quando hello conector está tentando tooconnect diretamente, mas ele falha.

Outro filtro de Monitor de rede que ajuda você tooeasily identificar esse problema é:

**property.TCPSynRetransmit**

Um pacote SYN é o primeiro pacote de saudação enviado tooestablish uma conexão TCP. Se esse pacote não retornar uma resposta, Olá SYN é reativada. Você pode usar Olá anterior filtro toosee qualquer SYNs retransmitidos. Em seguida, você pode verificar se essas SYNs correspondem tooany relacionados ao conector tráfego.

Olá exemplo a seguir mostra uma tentativa de conexão com falha tooService porta 9352:

 ![Resposta de exemplo para uma tentativa de conexão com falha](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Se você vir algo como Olá anterior resposta, conector hello está tentando toocommunicate diretamente com hello barramento de serviço do Azure. Se você esperar Olá conector toomake conexões diretas toohello Azure services, essa resposta é uma indicação clara de que você tem um problema de rede ou de um firewall.

>[!NOTE]
>Se você estiver toouse configurado um servidor proxy, essa resposta pode significar que o barramento de serviço está tentando uma conexão TCP direto antes de alternar tooattempting uma conexão via HTTPS.
>

A análise do rastreamento da rede não é para qualquer um. Mas ele pode ser uma ferramenta valiosa tooget rápido saber o que está acontecendo com a sua rede.

Se você continuar toostruggle com problemas de conectividade do conector, crie um tíquete com nossa equipe de suporte. equipe de saudação pode ajudá-lo com solução de problemas.

Para obter informações sobre como resolver os erros do Conector do Proxy do Aplicativo, consulte [Solucionar Problemas do Proxy do Aplicativo](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Próximas etapas

[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)<br>
[Como instalar o toosilently Olá conector de Proxy de aplicativo do AD do Azure](active-directory-application-proxy-silent-installation.md)
