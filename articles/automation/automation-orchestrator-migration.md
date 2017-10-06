---
title: "aaaMigrating do Orchestrator tooAzure automação | Microsoft Docs"
description: "Descreve como pacotes de integração e toomigrate runbooks do System Center Orchestrator tooAzure automação."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Migrando do Orchestrator tooAzure automação (Beta)
Os runbooks no [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) são baseados nas atividades de pacotes de integração que são escritos especificamente para o Orchestrator, enquanto os runbooks na Automação do Azure são baseados no Windows PowerShell.  [Runbooks gráficos](automation-runbook-types.md#graphical-runbooks) na automação do Azure tem um runbooks de tooOrchestrator aparência semelhante com suas atividades representando ativos, runbooks filho e cmdlets do PowerShell.

Olá [Kit de ferramentas de migração do System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) inclui ferramentas tooassist na conversão de runbooks do Orchestrator tooAzure automação.  Além disso tooconverting runbooks de saudação próprios, você deve converter os pacotes de integração de saudação com atividades de saudação que Olá runbooks usar módulos de toointegration com cmdlets do Windows PowerShell.  

A seguir está o processo básico de saudação para converter tooAzure de runbooks do Orchestrator automação.  Cada uma dessas etapas é descrita em detalhes nas seções de saudação abaixo.

1. Baixar Olá [Kit de ferramentas de migração do System Center Orchestrator](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) que contém as ferramentas de saudação e módulos discutidos neste artigo.
2. Importe o [Módulo de atividades padrão](#standard-activities-module) na Automação do Azure.  Isso inclui versões convertidas de atividades padrão do Orchestrator que podem ser usadas por runbooks convertidos.
3. Importe os [Módulos de Integração do System Center Orchestrator](#system-center-orchestrator-integration-modules) na Automação do Azure para os pacotes de integração usados pelos seus runbooks que acessam o System Center.
4. Converter os pacotes de integração de terceiros e personalizados usando Olá [conversor de pacote de integração](#integration-pack-converter) e importar para a automação do Azure.
5. Converter runbooks do Orchestrator usando Olá [Runbook conversor](#runbook-converter) e instalar na automação do Azure.
6. Crie manualmente ativos do Orchestrator necessários na automação do Azure como Olá conversor de Runbook não converte esses recursos.
7. Configurar um [Hybrid Runbook Worker](#hybrid-runbook-worker) em seus runbooks toorun convertido Centro de dados local que irá acessar recursos locais.

## <a name="service-management-automation"></a>Automação de Gerenciamento de Serviços
[Automação de gerenciamento de serviço](http://technet.microsoft.com/library/dn469260.aspx) (SMA) armazena e executa os runbooks em seu data center local como o Orchestrator e usa Olá mesmo módulos de integração como automação do Azure. Olá [Runbook conversor](#runbook-converter) converte embora toographical runbooks do Orchestrator runbooks que não têm suporte no SMA.  Ainda é possível instalar Olá [módulo de atividades padrão](#standard-activities-module) e [módulos de integração do System Center Orchestrator](#system-center-orchestrator-integration-modules) para o SMA, mas você deve manualmente [reescrever seus runbooks](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Hybrid Runbook Worker
Os runbooks do Orchestrator são armazenados em um servidor de banco de dados e executados em servidores runbook, ambos em seu data center local.  Runbooks na automação do Azure são armazenados em Olá nuvem do Azure e podem ser executados em seu datacenter local usando um [Hybrid Runbook Worker](automation-hybrid-runbook-worker.md).  Isso é como você normalmente executar runbooks convertido do Orchestrator, já que eles são projetado toorun em servidores locais.

## <a name="integration-pack-converter"></a>Conversor de Pacote de Integração
Olá conversor de pacote de integração converte os pacotes de integração que foram criados usando Olá [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration módulos com base no Windows PowerShell que podem ser importados para a automação do Azure ou Automação de gerenciamento de serviço.  

Quando você executa Olá conversor de pacote de integração, são apresentados com um assistente que permitirá que você tooselect um arquivo de pacote (. oip) de integração.  Assistente de saudação lista atividades Olá incluídas no pacote de integração e permite que você tooselect que será migrado.  Quando você concluir o Assistente de saudação, ele cria um módulo de integração que inclui um cmdlet correspondente para cada uma das atividades Olá no pacote de integração Olá original.

### <a name="parameters"></a>parâmetros
As propriedades de uma atividade no pacote de integração de saudação são convertidos tooparameters de saudação de cmdlet correspondente no módulo de integração de saudação.  Os cmdlets do Windows PowerShell têm um conjunto de [parâmetros comuns](http://technet.microsoft.com/library/hh847884.aspx) que podem ser usados com todos os cmdlets.  Por exemplo, hello - Verbose parâmetro faz com que um cmdlet toooutput informações detalhadas sobre sua operação.  Nenhum cmdlet pode ter um parâmetro com o mesmo nome como um parâmetro comum de saudação.  Se uma atividade tem uma propriedade com o mesmo nome como um parâmetro comum de hello, Olá assistente solicitará que você tooprovide outro nome para o parâmetro hello.

### <a name="monitor-activities"></a>Monitorar atividades
Monitorar runbooks no início do Orchestrator com um [monitorar a atividade](http://technet.microsoft.com/library/hh403827.aspx) e executar continuamente toobe espera invocado por um evento específico.  Automação do Azure não oferece suporte a runbooks, o monitor para que todas as atividades do monitor no pacote de integração de saudação não serão convertidas.  Em vez disso, um cmdlet de espaço reservado é criado no módulo de integração de saudação para monitorar a atividade de saudação.  Esse cmdlet não tem nenhuma funcionalidade, mas permite que qualquer runbook convertido que utiliza toobe instalado.  Este runbook não será capaz de toorun na automação do Azure, mas ele pode ser instalado para que você pode modificá-lo.

### <a name="integration-packs-that-cannot-be-converted"></a>Pacotes de integração que não podem ser convertidos
Pacotes de integração que não foram criados com OIT não podem ser convertidos com hello conversor de pacote de integração. Há também alguns pacotes de integração fornecidos pela Microsoft que atualmente não podem ser convertidos com essa ferramenta.  As versões convertidas desses pacotes de integração foram [fornecidas para download](#system-center-orchestrator-integration-modules) para que possam ser instaladas na Automação do Azure ou no Service Management Automation.

## <a name="standard-activities-module"></a>Módulo de atividades padrão
O Orchestrator inclui um conjunto de [atividades padrão](http://technet.microsoft.com/library/hh403832.aspx) que não está incluído em um pacote de integração, mas é usado por vários runbooks.  Olá atividades padrão é um módulo de integração que inclui um cmdlet equivalente para cada uma dessas atividades.  Você deve instalar esse módulo de integração na Automação do Azure antes de importar todos os runbooks convertidos que usam uma atividade padrão.

Além disso, toosupporting convertido runbooks, Olá cmdlets no módulo de atividades padrão Olá pode ser usado por alguém que esteja familiarizado com o Orchestrator toobuild novos runbooks na automação do Azure.  Embora a funcionalidade de saudação de todas as atividades de saudação padrão pode ser executada com os cmdlets, eles podem operam de forma diferente.  Olá cmdlets Olá convertido atividades padrão módulo funcionará Olá mesmo conforme suas atividades e use Olá os mesmos parâmetros.  Isso pode ajudar a saudação existente Orchestrator autor do runbook em seu runbooks de automação de tooAzure de transição.

## <a name="system-center-orchestrator-integration-modules"></a>Módulos de Integração do System Center Orchestrator
A Microsoft fornece [pacotes de integração](http://technet.microsoft.com/library/hh295851.aspx) para a criação de componentes do System Center tooautomate runbooks e outros produtos.  Alguns desses pacotes de integração baseiam-se no momento OIT mas no momento não podem ser convertido toointegration módulos devido a problemas conhecidos.  [Módulos de Integração do System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) incluem versões convertidas desses pacotes de integração que podem ser importadas para a Automação do Azure e para o SMA.  

Versão do RTM Olá dessa ferramenta, versões atualizadas dos pacotes de integração de saudação com base em OIT que pode ser convertido com hello que conversor de pacote de integração será publicada.  Orientação também será fornecida tooassist na conversão de runbooks usando atividades de pacotes de integração de saudação não com base nas OIT.

## <a name="runbook-converter"></a>Runbook Converter
Conversor de Runbook Hello converte runbooks do Orchestrator em [runbooks gráficos](automation-runbook-types.md#graphical-runbooks) que podem ser importados para a automação do Azure.  

Conversor de runbook é implementado como um módulo PowerShell com um cmdlet chamado **ConvertFrom SCORunbook** que realiza a conversão de saudação.  Quando você instala a ferramenta hello, ele criará uma sessão do PowerShell tooa de atalho que carrega Olá cmdlet.   

A seguir é Olá processo básico tooconvert um runbook do Orchestrator e importá-lo para automação do Azure.  Olá seções a seguir fornecem mais detalhes sobre como usar a ferramenta hello e trabalhar com runbooks convertido.

1. Exporte um ou mais runbooks do Orchestrator.
2. Obter os módulos de integração para todas as atividades no runbook hello.
3. Converta Olá runbooks do Orchestrator no arquivo hello.
4. Examine as informações nos logs toovalidate Olá conversão e toodetermine todas as tarefas manuais necessárias.
5. Importe runbooks convertidos na Automação do Azure.
6. Crie ativos necessários na Automação do Azure.
7. Edite saudação runbook na automação do Azure toomodify todas as atividades necessárias.

### <a name="using-runbook-converter"></a>Usando o Runbook Converter
Olá sintaxe **ConvertFrom SCORunbook** é o seguinte:

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - exportação de toohello de caminho de arquivo tooconvert de runbooks que contêm hello.
* Módulo – lista delimitada por vírgula dos módulos de integração que contém atividades em Olá runbooks.
* OutputFolder - caminho toohello pasta toocreate convertido runbooks gráficos.

Olá converte Olá runbooks em um arquivo de exportação chamado de comando de exemplo a seguir **MyRunbooks.ois_export**.  Esses runbooks usar saudação do Active Directory e pacotes de integração do Data Protection Manager.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Arquivos de log
Olá conversor de Runbook criará Olá seguintes arquivos de log no hello mesmo local que Olá convertido runbook.  Se Olá arquivos já existirem, eles serão substituídos com informações de conversão de última hello.

| Arquivo | Conteúdo |
|:--- |:--- |
| Runbook Converter - progress.log |Etapas detalhadas de conversão de hello, incluindo informações para cada atividade convertida com êxito e aviso para cada atividade não convertido. |
| Runbook Converter - summary.log |Resumo da saudação conversão, incluindo todos os avisos da última e execute as tarefas que você precisa tooperform como a criação de uma variável necessária para o runbook Olá convertido. |

### <a name="exporting-runbooks-from-orchestrator"></a>Exportando runbooks do Orchestrator
Olá Runbook conversor funciona com um arquivo de exportação do Orchestrator que contém um ou mais runbooks.  Ele cria um runbook de automação do Azure correspondente para cada runbook do Orchestrator no arquivo de exportação de saudação.  

tooexport um runbook do Orchestrator, clique em nome de saudação do hello runbook no Runbook Designer e selecione **exportar**.  tooexport todos os runbooks em uma pasta, clique com botão direito nome saudação da pasta hello e selecione **exportar**.

### <a name="runbook-activities"></a>Atividades de runbook
Olá Runbook conversor converte cada atividade em hello atividade correspondente do Orchestrator runbook tooa na automação do Azure.  As atividades que não podem ser convertidas, uma atividade de espaço reservado é criada no runbook Olá com texto de aviso.  Depois de importar runbook Olá convertido para automação do Azure, você deve substituir qualquer uma dessas atividades com atividades válidas que executam a funcionalidade de saudação necessária.

Todas as atividades de Orchestrator no hello [módulo de atividades padrão](#standard-activities-module) será convertido.  Há algumas atividades padrão do Orchestrator que não estão neste módulo e não são convertidas.  Por exemplo, **enviar evento da plataforma** não tem nenhum equivalente de automação do Azure como evento Olá é tooOrchestrator específico.

[Monitorar atividades](https://technet.microsoft.com/library/hh403827.aspx) não são convertidas porque não há nenhum equivalente toothem na automação do Azure.  Olá exceção são monitorar atividades em [convertido pacotes de integração](#integration-pack-converter) que será convertido toohello atividade de espaço reservado.

Qualquer atividade de um [convertido de pacote de integração](#integration-pack-converter) serão convertidos se você fornecer o módulo de integração do hello caminho toohello com hello **módulos** parâmetro.  Para pacotes de integração do System Center, você pode usar o hello [módulos de integração do System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Recursos do Orchestrator
Olá Runbook conversor converte somente runbooks, não outros recursos do Orchestrator como contadores, variáveis ou conexões.  Não há suporte para contadores na Automação do Azure.  Há suporte para variáveis e conexões, mas você deve criá-los manualmente.  arquivos de log de saudação serão informam se Olá runbook exigir esses recursos e especificar recursos correspondentes que você precisa toocreate na automação do Azure para Olá convertido runbook toooperate corretamente.

Por exemplo, um runbook pode usar uma variável toopopulate um valor específico em uma atividade.  Olá runbook convertido será converter hello atividade e especificar um ativo de variável na automação do Azure com hello mesmo nome como variável de Orchestrator hello.  Isso será indicado Olá **Runbook conversor - Summary. log** arquivo criado após a conversão de saudação.  Você precisará toomanually criar este ativo de variável na automação do Azure antes de usar o runbook hello.

### <a name="input-parameters"></a>Parâmetros de entrada
Runbooks do Orchestrator aceitar parâmetros de entrada com hello **inicializar dados** atividade.  Se o runbook hello está sendo convertido inclui essa atividade, então um [parâmetro de entrada](automation-graphical-authoring-intro.md#runbook-input-and-output) Olá automação do Azure runbook é criado para cada parâmetro na atividade de saudação.  Um [controle de fluxo de trabalho de Script](automation-graphical-authoring-intro.md#activities) atividade é criada no runbook Olá convertido que recupera e retorna cada parâmetro.  Todas as atividades no runbook Olá que usarem um parâmetro de entrada consulte toohello saída dessa atividade.

motivo de saudação que essa estratégia é usada é uma funcionalidade toobest espelho Olá em Olá Orchestrator runbook.  Atividades em novos runbooks gráficos devem consultar diretamente tooinput parâmetros usando uma fonte de dados de entrada do Runbook.

### <a name="invoke-runbook-activity"></a>Invocar a atividade de Runbook
Runbooks do Orchestrator iniciar outros runbooks com hello **invocar Runbook** atividade. Se o runbook hello está sendo convertido inclui essa atividade e hello **aguardar a conclusão** opção é definida, uma atividade de runbook é criada para ele no runbook Olá convertido.  Se hello **aguardar a conclusão** opção não estiver definida, uma atividade de Script de fluxo de trabalho é criada que usa **Start-AzureAutomationRunbook** toostart Olá runbook.  Depois de importar runbook Olá convertido para automação do Azure, você deve modificar esta atividade com informações de saudação especificadas na atividade de saudação.

## <a name="related-articles"></a>Artigos relacionados
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Automação de Gerenciamento de Serviço](https://technet.microsoft.com/library/dn469260.aspx)
* [Runbook Worker Híbrido](automation-hybrid-runbook-worker.md)
* [Atividades padrão do Orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [Baixar o Kit de Ferramentas de Migração do System Center Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
