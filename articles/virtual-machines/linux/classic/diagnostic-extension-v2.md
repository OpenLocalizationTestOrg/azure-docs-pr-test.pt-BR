---
title: "aaaMonitoring uma VM do Linux com uma extensão de VM | Microsoft Docs"
description: "Saiba como toouse Olá extensão de diagnóstico do Linux toomonitor Olá dados de desempenho e diagnóstico de uma VM do Linux no Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Use Olá extensão de diagnóstico do Linux toomonitor Olá dados de desempenho e diagnóstico de uma VM do Linux

Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux.

> [!IMPORTANT]
> Esta versão foi preterida e sua publicação pode ser cancelada a qualquer momento após 30 de junho de 2018. Ela foi substituída pela versão 3.0. Para obter mais informações, consulte Olá [documentação para a versão 3.0 do hello extensão de diagnóstico do Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Introdução

(**Observação**: Olá extensão de diagnóstico do Linux é originado de abertura em [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) onde informações mais recentes de saudação na extensão de saudação são publicadas pela primeira vez. Talvez você queira Olá toocheck [página GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) primeiro.)

Olá extensão de diagnóstico do Linux ajuda uma saudação do usuário monitor VMs do Linux em execução no Microsoft Azure. Ele tem Olá recursos a seguir:

* Coleta e carrega as informações de desempenho do sistema de saudação da tabela de armazenamento do usuário do toohello Olá VM do Linux, incluindo informações de diagnóstico e de syslog.
* Permite que os usuários toocustomize Olá as métricas de dados que serão coletadas e carregadas.
* Permite que os usuários tooupload log especificado arquivos tooa armazenamento designadas tabela.

Na versão atual de saudação 2.3, dados de saudação incluem:

* Todos os logs Rsyslog do Linux, incluindo logs de sistema, de segurança e de aplicativos.
* Todos os dados do sistema que são especificados em [site de soluções de plataforma cruzada do System Center Olá](https://scx.codeplex.com/wikipage?title=xplatproviders).
* Arquivos de log especificados pelo usuário.

Essa extensão funciona com hello clássico e modelos de implantação do Gerenciador de recursos.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Versão atual da extensão hello e substituição de versões antigas

Olá a versão mais recente da extensão de saudação é **2.3**, e **todas as versões antigas (2.0, 2.1 e 2.2) serão preteridas e não publicadas pela extremidade deste ano (2017)**. Se você instalou Olá extensão de diagnóstico do Linux com a atualização automática de versão secundária desabilitada, é altamente recomendável que você desinstale extensão hello e reinstalá-lo com a atualização de versão secundária automático habilitada. Em VMs (ASM) clássicas, você pode obter isso especificando '2.*' como versão de hello, se você estiver instalando uma extensão de saudação por meio do Azure XPLAT CLI ou o Powershell. Em VMs do ARM, você pode obter isso, incluindo ' "autoUpgradeMinorVersion": true' no modelo de implantação de VM hello. Além disso, qualquer nova instalação da extensão de saudação deve ter versão secundária do hello automaticamente a opção de atualização.

## <a name="enable-hello-extension"></a>Habilitar a extensão de saudação

Você pode habilitar esta extensão usando Olá [portal do Azure](https://portal.azure.com/#), Azure PowerShell ou scripts de CLI do Azure.

tooview e configurar o sistema hello e dados de desempenho diretamente da saudação portal do Azure, siga [essas etapas em hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

Este artigo se concentra em como tooenable e configurar a extensão de saudação usando comandos de CLI do Azure. Isso permite tooread e exibir dados de saudação diretamente da tabela de armazenamento hello.

Observe que os métodos de configuração de saudação que são descritos aqui não funcionarão para Olá portal do Azure. tooview e configurar dados de desempenho do sistema e de saudação diretamente da saudação portal do Azure, Olá extensão deve ser habilitada por meio do portal hello.

## <a name="prerequisites"></a>Pré-requisitos

* **Agente Linux do Azure versão 2.0.6 ou posterior**.

  Observe que a maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.0.6 ou posterior. Você pode executar **WAAgent-versão** tooconfirm qual versão está instalada em Olá VM. Se Olá VM estiver executando uma versão anterior ao 2.0.6, você pode seguir [estas instruções no GitHub](https://github.com/Azure/WALinuxAgent "instruções") tooupdate-lo.
* **CLI do Azure**. Execute [neste guia para instalar a CLI](../../../cli-install-nodejs.md) tooset o ambiente de CLI do Azure Olá em seu computador. Depois de instalar a CLI do Azure, você pode usar o hello **azure** comando de sua interface de linha de comando (Bash Terminal comandos ou prompt de comando) tooaccess Olá CLI do Azure. Por exemplo:

  * Execute **azure vm extension set --help** para obter informações de ajuda detalhadas.
  * Executar **logon do azure** toosign em tooAzure.
  * Executar **vm do azure lista** toolist todos Olá máquinas virtuais que você tem no Azure.
* Um armazenamento conta toostore Olá de dados. Você precisará de um nome de conta de armazenamento que foi criado anteriormente e um armazenamento de tooyour acesso tooupload chave Olá dados.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Use Olá CLI do Azure comando tooenable Olá extensão de diagnóstico do Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Cenário 1. Habilitar a extensão de saudação com conjunto de dados padrão de saudação

Na versão 2.3 ou posterior, os dados de padrão de saudação que serão coletados incluem:

* Todas as informações de Rsyslog (incluindo os logs de sistema, segurança e aplicativo).  
* Um conjunto principal de dados base do sistema. Observe que Olá conjunto de dados completo é descrito na Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Se você quiser tooenable dados extras, continue com as etapas de saudação em cenários de 2 e 3.

Etapa 1. Crie um arquivo chamado Privateconfig com hello seguinte conteúdo:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Etapa 2. Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Cenário 2: Personalizar as métricas de saudação do monitor de desempenho

Esta seção descreve como toocustomize Olá desempenho e a tabela de dados de diagnóstico.

Etapa 1. Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1. Além disso, crie um arquivo chamado PublicConfig.json. Especifica dados Olá específicos a serem toocollect.

Para todos os provedores e variáveis, consulte Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders). Você pode ter várias consultas e armazená-los em várias tabelas, acrescentando mais script toohello de consultas.

Por padrão, a saudação Rsyslog dados sempre é coletada.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Etapa 2. Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Cenário 3: Carregar os próprios arquivos de log

Esta seção descreve como os arquivos de log específico toocollect e carregamento tooyour conta de armazenamento. Você precisará toospecify ambos os Olá caminho tooyour log arquivo e hello nome da tabela de saudação onde você deseja toostore seu log. Você pode criar vários arquivos de log com a adição de vários arquivos/tabela entradas toohello de script.

Etapa 1. Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1. Em seguida, crie outro arquivo denominado PublicConfig.json com hello a seguir conteúdo:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Etapa 2. Execute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Observe que, com essa configuração no hello extensão versões anteriores too2.3, todos os logs gravados muito`/var/log/mysql.err` podem estar duplicados muito`/var/log/syslog` (ou `/var/log/messages` dependendo da distribuição de Linux Olá) também. Se você quiser tooavoid duplicidade log, você pode excluir o registro em log de `local6` recurso logs em sua configuração de rsyslog. Ele depende da distribuição de Linux Olá, mas em um sistema Ubuntu 14.04, Olá arquivo toomodify é `/etc/rsyslog.d/50-default.conf` e você pode substituir a linha hello `*.*;auth,authpriv.none -/var/log/syslog` muito`*.*;auth,authpriv,local6.none -/var/log/syslog`. Esse problema é corrigido na versão de hotfix mais recente saudação do 2.3 (2.3.9007), portanto, se você tiver a extensão de saudação versão 2.3, esse problema não deve ocorrer. Se ainda existir mesmo depois de reiniciar a VM,. entre em contato conosco e ajude-na solução de problemas que a versão mais recente de hotfix Olá não é instalado automaticamente.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Cenário 4: Parar extensão Olá colete os logs

Esta seção descreve como extensão de saudação toostop de coleta de logs. Observe que o processo do agente de monitoramento de Olá será ainda em execução até mesmo com essa reconfiguração. Se você desejar Olá toostop completamente o processo de agente de monitoramento, você pode fazer isso desabilitando extensão Olá. Olá comando toodisable Olá extensão é `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Etapa 1. Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1. Crie outro arquivo chamado PublicConfig.json com hello seguinte conteúdo:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Etapa 2. Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

## <a name="review-your-data"></a>Examinar os dados

Olá dados de desempenho e diagnósticos são armazenados em uma tabela de armazenamento do Azure. Revisão [como toouse armazenamento de tabela do Azure do Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn como tooaccess Olá no armazenamento de saudação de tabela por meio de scripts de CLI do Azure.

Além disso, você pode usar a interface do usuário ferramentas tooaccess Olá dados a seguir:

1. Gerenciador de Servidores do Visual Studio. Vá tooyour conta de armazenamento. Olá VM executado por aproximadamente cinco minutos, você verá tabelas padrão de saudação quatro: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog". Clique duas vezes em dados de saudação do hello tabela nomes tooview.
1. [Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure")(Soluções de Plataforma Cruzada do System Center).

![imagem](./media/diagnostic-extension/no1.png)

Se você tiver habilitado o fileCfg ou perfCfg (conforme descrito em cenários de 2 e 3), você pode usar dados de não-padrão tooview Visual Studio Server Explorer e o Azure Storage Explorer.

## <a name="known-issues"></a>Problemas conhecidos

* Olá Rsyslog informações e o arquivo de log especificado pelo cliente só pode ser acessado por meio de scripts.
