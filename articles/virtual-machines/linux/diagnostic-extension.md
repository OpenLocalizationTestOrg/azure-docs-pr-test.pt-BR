---
title: "Computação de aaaAzure - extensão de diagnóstico do Linux | Microsoft Docs"
description: "Como tooconfigure Olá métricas de toocollect Azure Linux diagnóstico extensão (LAD) e registrar eventos de VMs do Linux em execução no Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Usar os logs e métricas de toomonitor de extensão de diagnóstico do Linux

Este documento descreve a versão 3.0 e versões mais recente de saudação extensão de diagnóstico do Linux.

> [!IMPORTANT]
> Para saber mais sobre a versão 2.3 e anteriores, veja [este documento](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Introdução

Olá extensão de diagnóstico do Linux ajuda uma usuário monitorar Olá a integridade de uma VM do Linux em execução no Microsoft Azure. Ele tem Olá recursos a seguir:

* Coleta métricas de desempenho do sistema de saudação VM e os armazena em uma tabela específica em uma conta de armazenamento designadas.
* Recupera o log de eventos de syslog e os armazena em uma tabela específica no hello designado a conta de armazenamento.
* Permite que os usuários toocustomize Olá as métricas de dados que são coletadas e carregadas.
* Habilita recursos de syslog usuários toocustomize hello e níveis de severidade dos eventos que são coletados e carregados.
* Permite que os usuários tooupload log especificado arquivos tooa armazenamento designadas tabela.
* Oferece suporte ao envio de log e métricas eventos tooarbitrary EventHub pontos de extremidade e blobs formatada em JSON em Olá designado como conta de armazenamento.

Essa extensão funciona com os dois modelos de implantação do Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Instalação da extensão Olá em sua VM

Você pode habilitar esta extensão usando cmdlets do PowerShell do Azure hello, scripts de CLI do Azure ou modelos de implantação do Azure. Para saber mais, veja [Recursos de extensões](./extensions-features.md).

Olá portal do Azure não pode ser usado tooenable ou configurar LAD 3.0. Em vez disso, ele instala e configura a versão 2.3. Alertas e gráficos do portais do azure trabalham com dados de ambas as versões da extensão de saudação.

Estas instruções de instalação e uma [configuração de amostra para download](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configuram o LAD 3.0 para:

* captura e armazenamento Olá mesmas métricas que foram fornecidos pela LAD 2.3;
* capturar um conjunto útil de métricas do sistema de arquivo, novo tooLAD 3.0;
* capturar a coleção de syslog padrão Olá habilitada por LAD 2.3;
* Habilite Olá experiência do portal do Azure para criar gráficos e alertas em métricas VM.

configuração para download Olá é apenas um exemplo; Modifique toosuit suas necessidades.

### <a name="prerequisites"></a>Pré-requisitos

* **Agente Linux do Azure versão 2.2.0 ou posterior**. A maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.2.7 ou posterior. Executar `/usr/sbin/waagent -version` versão Olá tooconfirm no hello VM. Se Olá VM estiver executando uma versão mais antiga do agente de convidado hello, siga [estas instruções](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate-lo.
* **CLI do Azure**. [Configurar hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente em seu computador.
* Olá wget comando, se ainda não tiver: executar `sudo apt-get install wget`.
* Uma assinatura do Azure existente e um armazenamento existente conta nele toostore dados de saudação.

### <a name="sample-installation"></a>Instalação de exemplo

Preencha parâmetros corretos Olá Olá três primeiras linhas, em seguida, executar este script como raiz:

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

saudação URL para a configuração de exemplo hello e seu conteúdo, é toochange de assunto. Baixe uma cópia do arquivo JSON de configurações do portal hello e personalizá-la para suas necessidades. Os modelos ou as automações que você construir deverão usar sua própria cópia em vez de baixar essa URL toda vez.

### <a name="updating-hello-extension-settings"></a>Atualizando configurações de extensão Olá

Depois que você alterou seu protegidos ou as configurações públicas, implantá-los toohello VM executando Olá mesmo comando. Se nada alterado nas configurações de Olá, configurações de saudação atualizada sejam enviadas toohello extensão. LAD de recargas de configuração hello e reinicia em si.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migração de versões anteriores da extensão de saudação

Olá a versão mais recente da extensão de saudação é **3.0**. **As versões anteriores (2.x) antigas são substituídas e podem ser canceladas em ou após 31 de julho de 2018**.

> [!IMPORTANT]
> Essa extensão apresenta a configuração de toohello recentes alterações de extensão de saudação. Uma alteração foi feita a segurança de saudação tooimprove da extensão de saudação; Como resultado, com versões anteriores a compatibilidade com 2. x pode não ser mantida. Além disso, Olá publicador de extensão para esta extensão é diferente do publicador Olá para as versões 2. x de saudação.
>
> toomigrate de 2. x toothis nova versão da extensão hello, você deve desinstalar a extensão antigo hello (no antigo nome do publicador Olá), em seguida, instalar a versão 3 da extensão de saudação.

Recomendações:

* Instale a extensão de saudação com a atualização de versão secundária automático habilitada.
  * No modelo de implantação clássico VMs, especifica '3.*' como versão de hello, se você estiver instalando uma extensão de saudação por meio do Azure XPLAT CLI ou o Powershell.
  * Na implantação do Azure Resource Manager modelo VMs, incluem ' "autoUpgradeMinorVersion": true' no modelo de implantação de VM hello.
* Use uma conta de armazenamento nova/diferente para o LAD 3.0. Há várias pequenas incompatibilidades entre o LAD 2.3 e o LAD 3.0 que dificultam o compartilhamento de uma conta:
  * O LAD 3.0 armazena os eventos de syslog em uma tabela com um nome diferente.
  * counterSpecifier Olá cadeias de caracteres para `builtin` métricas diferem em LAD 3.0.

## <a name="protected-settings"></a>Configurações protegidas

Esse conjunto de informações de configuração contém informações confidenciais que devem ser protegidas da visualização pública, por exemplo, as credenciais de armazenamento. Essas configurações são transmitida tooand armazenado pela extensão de saudação em formato criptografado.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nome | Valor
---- | -----
storageAccountName | nome de Olá Olá da conta de armazenamento na qual os dados são gravados pela extensão de saudação.
storageAccountEndPoint | ponto de extremidade de saudação (opcional) identificando nuvem Olá no qual Olá conta de armazenamento existe. Se essa configuração estiver ausente, LAD padrões toohello nuvem pública do Azure, `https://core.windows.net`. toouse uma conta de armazenamento no Azure Alemanha, governo do Azure ou Azure China, defina este valor adequadamente.
storageAccountSasToken | Um [token SAS de conta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para serviços Blob e tabela (`ss='bt'`), objetos e toocontainers aplicáveis (`srt='co'`), que concede adiciona, criar, listar, atualizar e permissões de gravação (`sp='acluw'`). Fazer *não* incluem hello líder do ponto de interrogação (?).
mdsdHttpProxy | (opcional) As informações necessárias de proxy HTTP tooenable Olá extensão tooconnect toohello especificado a conta de armazenamento e o ponto de extremidade.
sinksConfig | (opcional) Detalhes de destinos alternativos toowhich métricas e eventos podem ser entregues. detalhes específicos de saudação de cada coletor de dados suportados pela extensão de saudação são abordados nas seções de saudação que seguem.

Você pode facilmente construir token SAS Olá necessárias por meio de saudação portal do Azure.

1. Selecione Olá armazenamento geral conta toowhich desejar Olá extensão toowrite
1. Selecione "Assinatura de acesso compartilhado" da parte de configurações de saudação do menu esquerdo Olá
1. Tornar Olá as seções apropriadas conforme descritas anteriormente
1. Clique botão de "Gerar SAS" hello.

![imagem](./media/diagnostic-extension/make_sas.png)

Saudação de cópia gerada SAS no campo de storageAccountSasToken Olá; Remover saudação à esquerda-interrogação ("?").

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Esta seção opcional define destinos adicionais, extensão de saudação toowhich envia informações de saudação coleta. matriz de "sink" Hello contém um objeto para cada coletor de dados adicionais. Olá determina de atributo "type" hello outros atributos no objeto de saudação.

Elemento | Valor
------- | -----
name | Uma cadeia de caracteres usada toorefer toothis coletor em outro lugar na configuração de extensão de saudação.
type | tipo de saudação do coletor está sendo definido. Determina o hello outros valores (se houver) em instâncias desse tipo.

A versão 3.0 do hello extensão de diagnóstico do Linux oferece suporte a dois tipos de coletor: EventHub e JsonBlob.

#### <a name="hello-eventhub-sink"></a>coletor de EventHub Olá

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

entrada de "sasURL" Hello contém Olá URL completa, incluindo o token SAS, Olá dados do Hub de eventos toowhich deve ser publicado. LAD requer uma SAS uma política que permite que a declaração de envio de saudação de nomenclatura. Um exemplo:

* Criar um namespace de Hubs de Eventos chamado `contosohub`
* Criar um Hub de eventos no namespace Olá chamado`syslogmsgs`
* Criar uma política de acesso compartilhado em Olá Hub de eventos denominado `writer` habilita Olá declaração de envio

Se você tiver criado uma SAS válida até meia-noite UTC em 1 de janeiro de 2018, o valor de sasURL de saudação pode ser:

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Para saber mais sobre como gerar tokens de SAS para Hubs de Eventos, veja [esta página da Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>coletor de JsonBlob Olá

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Dados direcionados tooa JsonBlob coletor é armazenado em blobs no armazenamento do Azure. Cada instância de LAD cria um blob a cada hora para cada nome de coletor. Cada blob sempre contém uma matriz de objeto JSON sintaticamente válida. Matriz de toohello atomicamente são adicionadas novas entradas. BLOBs são armazenados em um contêiner com mesmo nome como o coletor de saudação do hello. Olá regras de armazenamento do Azure para nomes de contêiner de blob se aplicam a nomes de toohello de JsonBlob coletores: entre 3 e 63 caracteres ASCII alfanuméricos minúsculos ou traços.

## <a name="public-settings"></a>Configurações públicas

Essa estrutura contém vários blocos de configurações que controlam as informações de saudação coletadas pela extensão de saudação. Cada configuração é opcional. Se você especificar `ladCfg`, também deverá especificar `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Elemento | Valor
------- | -----
StorageAccount | nome de Olá Olá da conta de armazenamento na qual os dados são gravados pela extensão de saudação. Deve ser Olá mesmo nome que seja especificado na Olá [protegido configurações](#protected-settings).
mdsdHttpProxy | (opcional) Mesmo da saudação [protegido configurações](#protected-settings). valor de público Olá é substituído pelo valor de private Olá, se definido. Coloque as configurações de proxy que contêm um segredo, como uma senha, em Olá [protegido configurações](#protected-settings).

elementos restantes da saudação são descritos detalhadamente nas seções a seguir de saudação.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Essa coleta de saudação controles estrutura opcional de métricas e os logs para entrega toohello dados de serviço e tooother de métricas do Azure coletores. Você deve especificar `performanceCounters` ou `syslogEvents`, ou ambos. Você deve especificar Olá `metrics` estrutura.

Elemento | Valor
------- | -----
eventVolume | (opcional) Número de partições criadas na tabela de armazenamento Olá Olá a controles. Pode ser `"Large"`, `"Medium"` ou `"Small"`. Se não for especificado, o valor padrão de saudação é `"Medium"`.
sampleRateInSeconds | intervalo padrão de saudação (opcional) entre o conjunto de métricas (não agregados) brutos. taxa de amostragem Olá menor com suporte é de 15 segundos. Se não for especificado, o valor padrão de saudação é `15`.

#### <a name="metrics"></a>Métricas

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Elemento | Valor
------- | -----
resourceId | ID de recurso do Azure Resource Manager Olá do hello VM ou de escala de máquinas virtuais de saudação definir Olá toowhich que VM pertence. Essa configuração deve ser especificada também se qualquer coletor JsonBlob é usado na configuração de saudação.
scheduledTransferPeriod | frequência de saudação em que as métricas agregadas são toobe computadas e transferidos tooAzure métricas, expressada como um intervalo de tempo é 8601. o período de transferência menor Olá é 60 segundos, ou seja, PT1M. Você deve especificar pelo menos um scheduledTransferPeriod.

Exemplos de saudação métricas especificadas na seção de performanceCounters Olá são coletadas a cada 15 segundos ou na taxa de amostragem Olá definido explicitamente para o contador de saudação. Se vários frequências de scheduledTransferPeriod aparecerem (como exemplo hello), cada agregação é calculada independentemente.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Nesta seção opcional controla coleção Olá de métricas. Exemplos processados são agregados para cada [scheduledTransferPeriod](#metrics) tooproduce estes valores:

* média
* mínimo
* máximo
* valor coletado por último
* Contagem de amostras brutas usado agregação de saudação toocompute

Elemento | Valor
------- | -----
coletores | (opcional) Uma lista separada por vírgulas de nomes de Coletores toowhich que LAD envia resultados agregados de métrica. Todas as métricas agregadas são publicados tooeach listado coletor. Veja [sinksConfig](#sinksconfig). Exemplo: `"EHsink1, myjsonsink"`.
type | Identifica o provedor real de saudação da métrica de saudação.
class | Junto com "counter" identifica a métrica específica Olá no namespace do provedor de saudação.
contador | Junto com "classe", identifica a métrica específica Olá no namespace do provedor de saudação.
counterSpecifier | Identifica a métrica específica Olá no namespace do Azure métricas hello.
condition | (opcional) Seleciona uma instância específica da métrica de Olá Olá objeto toowhich aplica ou selecionará Olá agregação em todas as instâncias do objeto. Para obter mais informações, consulte Olá [ `builtin` definições de métrica](#metrics-supported-by-builtin).
sampleRate | É o intervalo de 8601 que define Olá taxa na qual os exemplos brutos para esta métrica são coletados. Se não estiver definida, o intervalo de coleta de saudação é definido pelo valor de saudação do [sampleRateInSeconds](#ladcfg). taxa de amostra com suporte mais curta do Hello é 15 segundos (PT15S).
unit | Deve ser uma destas cadeias de caracteres: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond". Define a unidade de saudação de métrica de saudação. Os consumidores de dados coletado de saudação esperam Olá coletados toomatch de valores de dados dessa unidade. O LAD ignora esse campo.
displayName | Olá rótulo (na linguagem de saudação especificado pela configuração da localidade Olá associado) toobe anexado toothis dados de métricas do Azure. O LAD ignora esse campo.

counterSpecifier Olá é um identificador arbitrário. Os consumidores de métricas, como Olá gráficos portal do Azure e alerta o recurso, usam counterSpecifier como hello "chave" que identifica uma métrica ou uma instância de uma métrica. Para as métricas `builtin`, é recomendável usar valores counterSpecifier que começam com `/builtin/`. Se você estiver coletando uma instância específica de uma métrica, recomendamos que você anexar o identificador de saudação do valor da saudação instância toohello counterSpecifier. Alguns exemplos:

* `/builtin/Processor/PercentIdleTime` – tempo ocioso médio de todos os núcleos
* `/builtin/Disk/FreeSpace(/mnt)`-Espaço livre para o sistema de arquivos do hello /mnt
* `/builtin/Disk/FreeSpace` – espaço livre com a média de todos os sistemas de arquivos montados

Nem LAD nem Olá portal do Azure espera Olá counterSpecifier valor toomatch nenhum padrão. Seja consistente no modo como você constrói valores counterSpecifier.

Quando você especificar `performanceCounters`, LAD sempre cria a tabela de tooa de dados no armazenamento do Azure. Você pode ter Olá mesmo dados gravados tooJSON blobs e/ou Hubs de eventos, mas não é possível desabilitar tooa tabela de dados de armazenamento. Todas as instâncias de toouse de extensão de diagnóstico configurado Olá Olá conta de armazenamento de mesmo nome e o ponto de extremidade adicionam toohello seus logs e métricas mesma tabela. Se estiver escrevendo um número excessivo de VMs toohello pode acelerar a mesma partição de tabela, o Azure grava toothat partição. Olá eventVolume configuração faz com que as entradas toobe espalhadas por 1 (pequeno), (médio) de 10 ou 100 (grande) diferentes partições. Geralmente, "Médio" é suficiente tooensure tráfego não é limitado. recurso de métricas do Azure de saudação do hello portal do Azure usa dados de saudação nesta gráficos de tooproduce da tabela ou tootrigger alertas. nome da tabela Olá é a concatenação de saudação dessas cadeias de caracteres:

* `WADMetrics`
* Olá "scheduledTransferPeriod" hello agregados valores armazenados na tabela de saudação
* `P10DV2S`
* Uma data, na forma de hello "AAAAMMDD", que altera a cada 10 dias

Os exemplos incluem `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Nesta seção opcional controla a coleção de saudação de eventos de log de syslog. Se a seção de saudação for omitida, os eventos de syslog não são capturados em todos os.

a coleção de syslogEventConfiguration Olá tem uma entrada para cada recurso de syslog de interesse. Se minSeverity for "Nenhum" para um recurso específico, ou se o recurso não aparecerá no elemento de saudação, nenhum evento de recurso é capturado.

Elemento | Valor
------- | -----
coletores | Uma lista separada por vírgulas de nomes de Coletores de log individuais do toowhich eventos são publicados. Todos os eventos de log correspondentes restrições Olá syslogEventConfiguration são publicados tooeach listado coletor. Exemplo: "EHforsyslog"
facilityName | Um nome de recurso de syslog (como "LOG\_USER" ou "LOG\_LOCAL0"). Consulte a seção "recurso" Olá Olá [página syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para a lista completa de saudação.
minSeverity | Um nível de severidade de syslog (como "LOG\_ERR" ou "LOG\_INFO"). Consulte a seção "nível" Olá Olá [página syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para a lista completa de saudação. extensão de saudação captura eventos enviados toohello recurso em ou acima Olá especificado nível.

Quando você especificar `syslogEvents`, LAD sempre cria a tabela de tooa de dados no armazenamento do Azure. Você pode ter Olá mesmo dados gravados tooJSON blobs e/ou Hubs de eventos, mas não é possível desabilitar tooa tabela de dados de armazenamento. Olá comportamento para essa tabela de particionamento é Olá igual ao descrito para `performanceCounters`. nome da tabela Olá é a concatenação de saudação dessas cadeias de caracteres:

* `LinuxSyslog`
* Uma data, na forma de hello "AAAAMMDD", que altera a cada 10 dias

Os exemplos incluem `LinuxSyslog20170410` e `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Essa seção controla a execução de consultas [OMI](https://github.com/Microsoft/omi) arbitrárias.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
namespace | namespace OMI hello (opcional) no qual Olá consulta deve ser executada. Se não for especificado, o valor de padrão de saudação é "raiz/scx", implementada por Olá [provedores de plataforma cruzada do System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Olá OMI toobe de consulta executada.
tabela | tabela de armazenamento do Azure hello (opcional), em Olá designado a conta de armazenamento (consulte [protegido configurações](#protected-settings)).
frequência | número de saudação (opcional) de segundos entre a execução da consulta de saudação. O valor padrão é 300 (5 minutos); o valor mínimo é de 15 segundos.
coletores | (opcional) Uma lista separada por vírgulas de nomes de resultados de métricas adicionais coletores toowhich exemplo bruto deve ser publicada. Nenhuma agregação desses exemplos bruto é calculada pela extensão de saudação ou pelas métricas do Azure.

As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.

### <a name="filelogs"></a>fileLogs

Saudação de controles de captura de arquivos de log. LAD captura novas linhas de texto, como eles são gravados toohello arquivo e grava linhas tootable e/ou qualquer coletores especificados (JsonBlob ou EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Elemento | Valor
------- | -----
file | nome de caminho completo de toobe de arquivo de log Olá Olá observados e capturados. Olá pathname deve nomear um único arquivo; ele não é possível nomear um diretório ou conter curingas.
tabela | tabela de armazenamento do Azure hello (opcional), no armazenamento de saudação designado conta (conforme especificado na configuração de saudação protegida), na qual novas linhas de saudação "final" do arquivo hello é gravados.
coletores | (opcional) Uma lista separada por vírgulas de nomes de Coletores adicionais toowhich log linhas enviadas.

As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Métricas suportadas pelo provedor de builtin Olá

provedor de métrica de builtin Olá é uma origem de métricas mais interessantes tooa amplo conjunto de usuários. Essas métricas enquadram-se em cinco classes amplas:

* Processador
* Memória
* Rede
* Filesystem
* Disco

### <a name="builtin-metrics-for-hello-processor-class"></a>métricas de Builtin para Olá classe do processador

Olá classe processador de métricas fornece informações sobre o uso do processador em Olá VM. Ao agregar porcentagens, o resultado de saudação é média Olá em todas as CPUs. Em uma máquina virtual de núcleos dois, se um núcleo 100% ocupado e outros Olá era 100% ocioso, Olá relatado que percentidletime seria 50. Se cada núcleo foi 50% de disponibilidade para Olá mesmo período, Olá relatou o resultado também seria 50. Em um núcleo quatro VM, com 100% de um núcleo ocupado e Olá outros ocioso, Olá relatado que percentidletime seria 75.

contador | Significado
------- | -------
PercentIdleTime | Porcentagem de tempo durante a janela de agregação de saudação que processadores estavam executando loop ocioso do kernel Olá
PercentProcessorTime | Porcentagem de tempo de execução de um thread não ocioso
PercentIOWaitTime | Porcentagem de tempo de espera para toocomplete de operações de e/s
PercentInterruptTime | Porcentagem de tempo de execução de interrupções de hardware/software e DPCs (chamadas de procedimento deferidas)
PercentUserTime | De tempo não-ocioso durante a janela de agregação hello, porcentagem de saudação do tempo gasto no usuário mais em prioridade normal
PercentNiceTime | Tempo não-ocioso, Olá porcentagem gasta em baixa prioridade (BOM)
PercentPrivilegedTime | Tempo não-ocioso, Olá porcentagem gasta em modo privilegiado (kernel)

Olá primeiro quatro contadores devem ser somadas too100%. Olá última três contadores também soma too100%; eles subdividir a soma de saudação do PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.

tooobtain uma única métrica agregada para todos os processadores, defina `"condition": "IsAggregate=TRUE"`. tooobtain uma métrica para um processador específico, como o segundo processador lógico saudação de um quatro principais VM, defina `"condition": "Name=\\"1\\""`. Número de processadores lógicos está no intervalo de saudação `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>métricas de Builtin para Olá classe de memória

Olá classe memória das métricas fornece informações sobre utilização de memória, paginação e troca.

contador | Significado
------- | -------
AvailableMemory | Memória física disponível em MiB
PercentAvailableMemory | Memória física disponível como uma porcentagem da memória total
UsedMemory | Memória física em uso (MiB)
PercentUsedMemory | Memória física em uso como uma porcentagem da memória total
PagesPerSec | Paginação total (leitura/gravação)
PagesReadPerSec | Páginas lidas do repositório de backup (arquivo de permuta, arquivo de programa, arquivo mapeado etc.)
PagesWrittenPerSec | Páginas escritas toobacking armazenam (arquivo de permuta, arquivo mapeado, etc.)
AvailableSwap | Espaço de permuta não utilizado (MiB)
PercentAvailableSwap | Espaço de troca não utilizado como uma porcentagem da troca total
UsedSwap | Espaço de troca em uso (MiB)
PercentUsedSwap | Espaço de troca em uso como uma porcentagem da troca total

Essa classe de métricas tem apenas uma única instância. atributo de "condição" Hello não úteis de configurações e deve ser omitido.

### <a name="builtin-metrics-for-hello-network-class"></a>métricas de Builtin para Olá classe da rede

Olá classe de métricas de rede fornece informações sobre atividade de rede em um interfaces de rede individuais desde a inicialização. O LAD não expõe as métricas de largura de banda, que podem ser recuperadas de métricas de host.

contador | Significado
------- | -------
BytesTransmitted | Total de bytes enviados desde a inicialização
BytesReceived | Total de bytes recebidos desde a inicialização
BytesTotal | Total de bytes enviados ou recebidos desde a inicialização
PacketsTransmitted | Total de pacotes enviados desde a inicialização
PacketsReceived | Total de pacotes recebidos desde a inicialização
TotalRxErrors | Número de erros de recebimento desde a inicialização
TotalTxErrors | Número de erros de transmissão desde a inicialização
TotalCollisions | Número de relatados pelas portas de rede Olá desde a inicialização

 Embora essa classe seja instanciada, o LAD não oferece suporte à captura de métricas Network agregadas em todos os dispositivos de rede. conjunto de métricas de saudação tooobtain para uma interface específica, como eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>métricas de Builtin para Olá classe do sistema de arquivos

Olá classe de sistema de arquivos de métricas fornece informações sobre o uso do sistema de arquivos. Valores absolutos e porcentagem são relatados como seriam exibidos tooan usuário comum (não raiz).

contador | Significado
------- | -------
FreeSpace | Espaço em disco disponível em bytes
UsedSpace | Espaço em disco usado em bytes
PercentFreeSpace | Porcentagem de espaço livre
PercentUsedSpace | Porcentagem de espaço usado
PercentFreeInodes | Porcentagem de inodes não utilizados
PercentUsedInodes | Porcentagem de inodes alocados (em uso) somados em todos os sistemas de arquivos
BytesReadPerSecond | Bytes lidos por segundo
BytesWrittenPerSecond | Bytes gravados por segundo
BytesPerSecond | Bytes lido ou gravados por segundo
ReadsPerSecond | Operações de leitura por segundo
WritesPerSecond | Operações de gravação por segundo
TransfersPerSecond | Operações de leitura ou gravação por segundo

Os valores agregados em todos os sistemas de arquivo podem ser obtidos pela configuração `"condition": "IsAggregate=True"`. Os valores para um sistema de arquivos montado específico, como "/mnt", podem ser obtidos pela configuração `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>métricas de Builtin para Olá classe disco

Olá classe disco das métricas fornece informações sobre o uso do dispositivo de disco. Essas estatísticas se aplicam a toda a unidade toohello. Se houver vários sistemas de arquivos em um dispositivo, Olá contadores para o dispositivo são, na verdade, agregados em todos eles.

contador | Significado
------- | -------
ReadsPerSecond | Operações de leitura por segundo
WritesPerSecond | Operações de gravação por segundo
TransfersPerSecond | Operações totais por segundo
AverageReadTime | Média de segundos por operação de leitura
AverageWriteTime | Média de segundos por operação de gravação
AverageTransferTime | Média de segundos por operação
AverageDiskQueueLength | Número médio de operações de disco enfileiradas
ReadBytesPerSecond | Número de bytes lidos por segundo
WriteBytesPerSecond | Número de bytes gravados por segundo
BytesPerSecond | Número de bytes lidos ou gravados por segundo

Os valores agregados em todos os discos podem ser obtidos pela configuração `"condition": "IsAggregate=True"`. tooget informações para um dispositivo específico (por exemplo, / desenvolvimento/sdf1), definir `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Instalação e configuração do LAD 3.0 via CLI

Supondo que as configurações protegidas estão no arquivo hello Privateconfig e suas informações de configuração pública estão em PublicConfig.json, execute este comando:

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

comando Olá pressupõe que você esteja usando o modo de gerenciamento de recursos do Azure hello (arm) do hello CLI do Azure. tooconfigure LAD para implantação clássica do modelo de VMs (ASM), alternar muito "asm" modo (`azure config mode asm`) e omitir o nome do grupo de recursos Olá no comando hello. Para obter mais informações, consulte Olá [documentação da CLI de plataforma cruzada](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Uma configuração de exemplo do LAD 3.0

Com base em Olá anterior definições, aqui um exemplo de configuração de extensão de LAD 3.0 com alguma explicação. tooapply caso de tooyour neste exemplo, você deve usar seu próprio nome de conta de armazenamento, conta token SAS e tokens EventHubs SAS.

### <a name="privateconfigjson"></a>PrivateConfig.json

Essas configurações privadas definem os parâmetros de:

* uma conta de armazenamento
* um token de SAS de conta correspondente
* vários coletores (JsonBlob ou EventHubs com tokens de SAS)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Essas configurações públicas fazem o LAD:

* Carregar métricas % tempo de processador e espaço em disco usado toohello `WADMetrics*` tabela
* Carregue as mensagens de syslog recurso "usuário" e gravidade "info" toohello `LinuxSyslog*` tabela
* Carregar bruto OMI consulta resultados (PercentProcessorTime e PercentIdleTime) toohello chamado `LinuxCPU` tabela
* Carregar acrescentadas linhas no arquivo `/var/log/myladtestlog` toohello `MyLadTestLog` tabela

Em cada caso, os dados também são carregados para:

* Armazenamento de BLOBs do Azure (nome do contêiner é conforme definido no coletor de JsonBlob Olá)
* Ponto de extremidade EventHubs (conforme especificado no coletor de EventHubs Olá)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Olá `resourceId` em Olá configuração deve corresponder ao que de escala de máquina virtual VM ou Olá Olá definido.

* Métricas de plataforma Windows Azure, gráficos e alertas sabe resourceId Olá de saudação VM que você está trabalhando. Ele espera dados de saudação toofind para sua VM usando a chave de pesquisa de Olá Olá resourceId.
* Se você usar o dimensionamento automático do Azure, Olá resourceId na configuração de AutoEscala Olá deve corresponder resourceId Olá usado pelo LAD.
* Olá resourceId é criada em nomes de saudação do JsonBlobs gravados pelo LAD.

## <a name="view-your-data"></a>Ver seus dados

Usar dados de desempenho do hello tooview portal do Azure ou definir alertas:

![imagem](./media/diagnostic-extension/graph_metrics.png)

Olá `performanceCounters` dados sempre são armazenados em uma tabela de armazenamento do Azure. As APIs do Armazenamento do Azure estão disponíveis em várias linguagens e plataformas.

Enviado tooJsonBlob Coletores de dados são armazenados em blobs na conta de armazenamento Olá nomeado no hello [protegido configurações](#protected-settings). Você pode consumir dados de blob hello usando quaisquer APIs de armazenamento de Blob do Azure.

Além disso, você pode usar esses dados de saudação de tooaccess de ferramentas de interface do usuário no armazenamento do Azure:

* Gerenciador de Servidores do Visual Studio.
* [Gerenciador de Armazenamento do Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure").

Esse instantâneo de uma sessão do Microsoft Azure Storage Explorer mostra Olá geradas tabelas de armazenamento do Azure e os contêineres de uma extensão de LAD 3.0 corretamente configurada em uma VM de teste. imagem de saudação não corresponde exatamente à saudação [LAD 3.0 de exemplo de configuração](#an-example-lad-30-configuration).

![imagem](./media/diagnostic-extension/stg_explorer.png)

Consulte Olá relevante [EventHubs documentação](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn como tooconsume mensagens publicadas tooan EventHubs endpoint.

## <a name="next-steps"></a>Próximas etapas

* Criar alertas de métrica no [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para métricas de saudação coletar.
* Criar [gráficos de monitoramento](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para suas métricas.
* Saiba como muito[criar um conjunto de escala de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) usando o dimensionamento automático toocontrol de métricas.
