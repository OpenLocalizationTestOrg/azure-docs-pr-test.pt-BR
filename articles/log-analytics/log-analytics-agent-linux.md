---
title: aaaConnect tooOperations seus computadores Linux Management Suite (OMS) | Microsoft Docs
description: "Este artigo descreve como tooconnect Linux hospedado no Azure, outros nuvem ou local tooOMS usando Olá agente do OMS para Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Conecte-se a sua tooOperations de computadores Linux Management Suite (OMS) 

Com o OMS (Microsoft Operations Management Suite), você pode coletar e agir sobre os dados gerados em computadores Linux e soluções de contêiner como o Docker, residindo em seu data center local como servidores físicos ou máquinas virtuais, máquinas virtuais em um serviço hospedado em nuvem como AWS (Amazon Web Services) ou Microsoft Azure. Você também pode usar soluções de gerenciamento disponíveis no OMS, como controle de alterações, alterações de configuração de tooidentify, e tooproactively de atualizações de software do gerenciamento de atualizações toomanage gerenciar o ciclo de vida Olá suas VMs do Linux. 

Olá agente do OMS para Linux se comunica saída com hello serviço OMS usando a porta TCP 443 e se Olá computador se conecta a toocommunicate de servidor proxy ou firewall tooa sobre Olá Internet, consulte [Configurando o agente de saudação para uso com um proxy HTTP servidor ou Gateway do OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand alterações de configuração precisará toobe aplicado.  Se você estiver monitorando o computador de saudação com o System Center 2016 - Operations Manager ou do Operations Manager 2012 R2, pode ser multihomed com o serviço de encaminhamento toohello e os dados de toocollect de serviço do OMS hello e ainda ser monitorado pelo Operations Manager.  Computadores Linux monitorados por um grupo de gerenciamento do Operations Manager está integrado com o OMS não receber a configuração de fontes de dados e encaminhar coletados dados por meio do grupo de gerenciamento de saudação.  agente do OMS Olá não pode ser configurado tooreport toomore que um espaço de trabalho.  

Se suas políticas de segurança de TI não permitir que os computadores em sua toohello tooconnect de rede da Internet, agente Olá pode ser configurado tooconnect toohello OMS Gateway tooreceive configuração informações e enviar os dados coletados dependendo da solução Olá que tiver habilitado. Para obter mais informações e etapas sobre como tooconfigure toocommunicate seu agente Linux do OMS por meio de um serviço OMS do Gateway do OMS toohello, consulte [conectar computadores tooOMS usando Olá OMS Gateway](log-analytics-oms-gateway.md).  

Olá diagrama a seguir ilustra conexão Olá entre computadores Linux gerenciado por agente de saudação e o OMS, incluindo portas e direção hello.

![diagrama Comunicação do agente direto com o OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Requisitos do sistema
Antes de começar, examine Olá tooverify detalhes que você atenda aos pré-requisitos Olá a seguir.

### <a name="supported-linux-operating-systems"></a>Sistemas operacionais Linux com suporte
Olá distribuições do Linux a seguir têm suporte oficialmente.  No entanto, a saudação do agente do OMS para Linux também pode ser executado em outras distribuições não listadas.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 e 7 (x86/x64)
* Oracle Linux 5, 6 e 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)
* Debian GNU/Linux 6, 7 e 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 e 12 (x86/x64)

### <a name="network"></a>Rede
informações de saudação abaixo proxy de saudação da lista e as informações de configuração de firewall necessárias para Olá toocommunicate de agente do Linux com o OMS. O tráfego é de saída do seu serviço OMS do toohello de rede. 

|Recurso de agente| Portas |  
|------|---------|  
|*.ods.opinsights.azure.com | Porta 443|   
|*.oms.opinsights.azure.com | Porta 443|   
|*.blob.core.windows.net/ | Porta 443|   
|*.azure-automation.net | Porta 443|  

### <a name="package-requirements"></a>Requisitos do pacote

 **Pacote necessário**   | **Descrição**   | **Versão mínima**
--------------------- | --------------------- | -------------------
Glibc | Biblioteca GNU C   | 2.5-12 
Openssl | Bibliotecas OpenSSL | 0.9.8e ou 1.0
Curl | cliente Web cURL | 7.15.5
Python-ctypes | | 
PAM | Módulos de autenticação conectáveis | 

> [!NOTE]
>  O rsyslog ou syslog-ng é necessário toocollect mensagens de syslog. Não há suporte para o daemon do syslog saudação padrão na versão 5 do Red Hat Enterprise Linux, CentOS e Oracle Linux (sysklog) para coleta de eventos de syslog. toocollect dados de syslog dessa versão de distribuições, Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog, 

Agente de saudação inclui vários pacotes. versão de arquivo Hello contém Olá pacotes, disponíveis com o pacote de shell Olá em execução com a seguir `--extract`:

**Pacote** | **Versão** | **Descrição**
----------- | ----------- | --------------
omsagent | 1.4.0 | Olá agente do Operations Management Suite para Linux
omsconfig | 1.1.1 | Agente de configuração para Olá agente do OMS
omi | 1.2.0 | OMI (Open Management Infrastructure) – um servidor CIM leve
scx | 1.6.3 | Provedores de CIM OMI para métricas de desempenho do sistema operacional
apache-cimprov | 1.0.1 | Provedor de monitoramento de desempenho do Servidor HTTP Apache para OMI. Instalado se o Servidor HTTP Apache for detectado.
mysql-cimprov | 1.0.1 | Provedor de monitoramento de desempenho do Servidor MySQL para OMI. Instalado se o servidor MySQL/MariaDB for detectado.
docker-cimprov | 1.0.0 | Provedor do Docker para OMI. Instalado se o Docker for detectado.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibilidade com o System Center Operations Manager
Olá agente do OMS para Linux compartilha binários de agente com o agente do System Center Operations Manager hello. Se você instalar Olá agente do OMS para Linux em um sistema gerenciado atualmente pelo Operations Manager, ele Olá pacotes OMI e SCX na versão mais recente do hello computador tooa. Esta versão, a saudação do OMS e o System Center 2016 - agentes do Operations Manager/Operations Manager 2012 R2 para Linux são compatíveis. 

> [!NOTE]
> System Center 2012 SP1 e versões anteriores atualmente não são compatíveis ou não tem suporte com hello agente do OMS para Linux.<br>
> Se Olá agente do OMS para Linux for instalado tooa computador que atualmente não é monitorado pelo Operations Manager e desejar, em seguida, o computador de saudação toomonitor com o Operations Manager, você deve modificar Olá [configuração do OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) anterior computador de saudação toodiscovering. **Esta etapa é *não* necessário se o agente do Operations Manager de saudação for instalado antes de saudação do agente do OMS para Linux.**

### <a name="system-configuration-changes"></a>Alterações de configuração do sistema
Depois de instalar o hello agente do OMS para Linux pacotes, hello seguintes alterações de configuração de todo o sistema adicionais são aplicadas. Esses artefatos são removidos quando o pacote do hello omsagent é desinstalado.

* Um usuário sem privilégios chamado: `omsagent` é criado. Essa é a conta Olá Olá execuções de daemon omsagent como.
* Um arquivo "include" sudoers é criado em /etc/sudoers.d/omsagent. Isso autoriza o omsagent toorestart Olá syslog e omsagent daemons. Se as diretivas de "inclusão" do sudo não tiverem suporte na versão Olá instalada do sudo, essas entradas são gravadas muito/etc/sudoers.
* configuração de syslog Olá é modificado tooforward um subconjunto do agente de toohello de eventos. Para obter mais informações, consulte Olá **configurar coleta de dados** seção abaixo

### <a name="upgrade-from-a-previous-release"></a>Atualizar de uma versão anterior
A atualização de versões anteriores à 1.0.0-47 tem suporte nesta versão. Executando a instalação Olá com hello `--upgrade` comando atualiza todos os componentes da versão mais recente do toohello Olá agente.

## <a name="installing-hello-agent"></a>Instalando agente Olá

Esta seção descreve como tooinstall Olá agente do OMS para Linux usando um bunndle, que contém Debian e RPM pacotes para cada um dos componentes do agente hello.  Ele pode ser instalado diretamente ou extraído pacotes individuais do tooretrieve hello.  

Primeiro é necessário a ID do espaço de trabalho do OMS e a chave, o que você pode encontrar alternando toohello [portal clássico do OMS](https://mms.microsoft.com).  Em Olá **visão geral** página do menu superior, selecione Olá **configurações**e, em seguida, navegue muito**conectado Sources\Linux servidores**.  Consulte o direito de toohello Olá valor de **ID do espaço de trabalho** e **chave primária**.  Copie e cole os dois em seu editor favorito.    

1. Saudação de download mais recente [agente do OMS para Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) ou [agente do OMS para Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) do GitHub.  
2. Transferência de saudação pacote apropriado (x86 ou x64) tooyour computador Linux usando o scp/sftp.
3. Instalar o pacote de saudação usando Olá `--install` ou `--upgrade` argumento. 

    > [!NOTE]
    > Se houver pacotes estiverem instalados, como quando o agente do System Center Operations Manager Olá para Linux já está instalado, use Olá `--upgrade` argumento. tooconnect tooOperations Management Suite durante a instalação, forneça Olá `-w <WorkspaceID>` e `-s <Shared Key>` parâmetros.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall e integrar diretamente
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>pacote do agente Olá tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall e tooa integrada de espaço de trabalho na nuvem de governo dos EUA
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configurando o agente Olá para uso com um servidor proxy HTTP ou o Gateway do OMS
Olá agente do OMS para Linux dá suporte à comunicação por meio de um servidor proxy HTTP ou HTTPS ou serviço do OMS Gateway toohello OMS.  Há suporte para a autenticação anônima e básica (nome de usuário/senha).  

### <a name="proxy-configuration"></a>Configuração de Proxy
valor de configuração de proxy Olá tem Olá sintaxe a seguir:

`[protocol://][user:password@]proxyhost[:port]`

Propriedade|Descrição
-|-
Protocolo|http ou https
usuário|Nome de usuário opcional para autenticação de proxy
Senha|Senha opcional para autenticação de proxy
proxyhost|Endereço ou FQDN do servidor do proxy de saudação/OMS Gateway
porta|Número da porta opcional para Olá proxy server/OMS Gateway

Por exemplo: `http://user01:password@proxy01.contoso.com:8080`

servidor de proxy Olá pode ser especificado durante a instalação ou modificando o arquivo de configuração do hello proxy.conf após a instalação.   

### <a name="specify-proxy-configuration-during-installation"></a>Especificar a configuração de proxy durante a instalação
Olá `-p` ou `--proxy` argumento para o pacote de instalação omsagent Olá Especifica Olá toouse de configuração de proxy. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Definir a configuração de proxy de saudação em um arquivo
configuração de proxy Olá pode ser definida em arquivos Olá `/etc/opt/microsoft/omsagent/proxy.conf` e `/etc/opt/microsoft/omsagent/conf/proxy.conf `. arquivos de saudação podem ser criados ou editados diretamente, mas suas permissões devem ser atualizada toogrant Olá omiuser leitura do usuário permissão nos arquivos de saudação. Por exemplo:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>Removendo a configuração de proxy de saudação
tooremove uma configuração de proxy definida anteriormente e reverter toodirect conectividade, remova Olá proxy.conf arquivo:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Integração com o Operations Management Suite
Se uma ID do espaço de trabalho e a chave não foram fornecidas durante a instalação do pacote de saudação, agente Olá deve ser registrado posteriormente com o Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Integração usando a linha de comando Olá
Execute Olá omsadmin.sh comando fornecendo o id do espaço de trabalho de saudação e a chave para seu espaço de trabalho. Este comando deve ser executado como raiz (com elevação sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Integração usando um arquivo
1.  Criar arquivo hello `/etc/omsagent-onboard.conf`. arquivo Hello deve ser legível e gravável para a raiz.
`sudo vi /etc/omsagent-onboard.conf`
2.  Inserir saudação linhas no arquivo hello com a ID do espaço de trabalho e a chave compartilhada a seguir:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Execute Olá tooOMS de tooOnboard de comando a seguir:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  Olá arquivo será excluído na integração bem-sucedida.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Habilitar hello agente do OMS para Linux tooreport tooSystem Center Operations Manager
Execute Olá seguindo as etapas tooconfigure Olá agente do OMS para o grupo de gerenciamento do Linux tooreport tooa System Center Operations Manager.  

1. Editar arquivo hello.`/etc/opt/omi/conf/omiserver.conf`
2. Certifique-se de que Olá linha a partir **httpsport =** define Olá porta 1270. Como: `httpsport=1270`
3. Reinicie o servidor OMI de saudação:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Logs do Agente
Olá logs para Olá agente do OMS para Linux pode ser encontrada em: `/var/opt/microsoft/omsagent/<workspace id>/log/` Olá logs para o programa omsconfig (configuração do agente) de saudação pode ser encontrado em: `/var/opt/microsoft/omsconfig/log/` Logs para Olá componentes OMI e SCX (que fornecem dados de métrica de desempenho) podem ser encontrados em:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Configuração de rotação de log##
configuração de rotação de log Olá para omsagent pode ser encontrada em:`/etc/logrotate.d/omsagent-<workspace id>`

as configurações padrão de saudação são: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Saudação de desinstalação do agente do OMS para Linux
Olá pacotes de agente podem ser desinstalados por execução Olá arquivo. sh com hello `--purge` argumento, que remove completamente agente hello e sua configuração do computador hello.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problema: O tooconnect não é possível por meio do proxy tooOMS

#### <a name="probable-causes"></a>Causas prováveis
* proxy de saudação especificado durante a integração estava incorreto
* pontos de extremidade de serviço de OMS Olá não são whitelistested em seu data center 

#### <a name="resolutions"></a>Resoluções
1. Reonboard toohello serviço OMS com hello agente do OMS para Linux usando Olá após o comando com a opção de saudação `-v` habilitado. Isso permite que a saída detalhada do agente de saudação se conectam por meio do proxy de saudação toohello serviço OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Examine a seção de saudação [agente de saudação configurando para uso com um proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify você configurou corretamente Olá toocommunicate agent por meio de um servidor proxy.    
* Verifique que Olá seguintes pontos de extremidade de serviço do OMS estão na lista de permissões:

    |Recurso de agente| Portas |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Porta 443|   
    |*.oms.opinsights.azure.com | Porta 443|   
    |ods.systemcenteradvisor.com | Porta 443|   
    |*.blob.core.windows.net/ | Porta 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problema: Você recebe um erro 403 durante a tentativa de tooonboard

#### <a name="probable-causes"></a>Causas prováveis
* A data e a hora estão incorretas no servidor Linux 
* A ID e a Chave do Espaço de Trabalho usadas estão incorretas

#### <a name="resolution"></a>Resolução

1. Verificar o tempo de saudação em seu servidor Linux com data de comando hello. Se houver tempo Olá + /-15 minutos da hora atual, integração falhará. toocorrect desta atualização Olá data e/ou o fuso horário do servidor Linux. 
2. Verifique se que você instalou a versão mais recente Olá de saudação do agente do OMS para Linux.  versão mais recente do Hello agora notifica se a diferença de horário está causando a falha de integração de saudação.
3. Reonboard usando a ID do espaço de trabalho correto e a chave de espaço de trabalho seguindo instruções de instalação Olá neste tópico.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problema: Você verá um erro de 500 e 404 no arquivo de log Olá logo após a integração
Esse é um problema conhecido que ocorre durante o primeiro upload de dados do Linux em um espaço de trabalho do OMS. Isso não afeta os dados sendo enviados ou a experiência do serviço.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problema: Você não visualizar todos os dados no portal do OMS Olá

#### <a name="probable-causes"></a>Causas prováveis

- Falha de serviço do OMS toohello de integração
- Conexão toohello serviço OMS está bloqueado
- Os dados do Agente do OMS para Linux têm o backup realizado

#### <a name="resolutions"></a>Resoluções
1. Verifique se integração Olá serviço OMS foi bem-sucedida verificando se hello seguinte arquivo existir:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard usando Olá `omsadmin.sh` instruções de linha de comando
3. Se usar um proxy, consulte toohello etapas de resolução de proxy fornecidas anteriormente.
4. Em alguns casos, quando Olá agente do OMS para Linux não pode se comunicar com hello serviço OMS, dados de agente Olá estão tamanho de buffer cheio toohello em fila, que é 50 MB. Olá agente do OMS para Linux deve ser reiniciado executando o comando a seguir de saudação: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Esse problema foi corrigido nas versões 1.1.0-28 e posteriores do Agente.
> 