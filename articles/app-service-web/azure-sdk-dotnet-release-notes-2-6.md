---
title: "aaaAzure SDK para notas de versão 2.6 .NET"
description: "Notas de versão SDK do Azure para .NET 2.6"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Notas de versão SDK do Azure para .NET 2.6
Este documento contém notas de versão de saudação do hello Azure SDK versão 2.6 do .NET. 

Com o SDK 2.6 do Azure, você pode desenvolver aplicativos de serviço de nuvem (PaaS) direcionando a .NET 4.5.2 ou .NET 4.6, desde que você instalar manualmente o destino de saudação do .NET Framework em Olá função de serviço de nuvem. Consulte [Install .NET on a Cloud Service Role (Instalar o .NET em uma Função do Serviço de Nuvem)](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Atualizações do Barramento de Serviço
* Hubs de Eventos: 
  
  * Agora permite o controle de acesso direcionado ao enviar eventos expondo o ponto de extremidade do editor adicional para Hubs de Eventos.
  * Estabilidade adicional e a melhoria adicionaram tooEvent recurso de Hubs.
  * Adição do suporte do protocolo Amqp sobre WebSocket para sistemas de mensagens e Hubs de Eventos.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Atualizações das Ferramentas do HDInsight para Visual Studio
* **Aprimoramento do IntelliSense**: sugestão de metadados remotos
  
    Agora as Ferramentas do HDInsight para Visual Studio dão suporte à obtenção de metadados remotos quando você estiver editando o script do Hive. Por exemplo, você pode digitar **selecione * FROM** e todos os nomes de tabela Olá serão exibidos. Além disso, os nomes de coluna hello serão mostrados depois de especificar uma tabela.
* **Suporte ao emulador do HDInsight**
  
    Agora ferramentas HDInsight para o suporte do Visual Studio se conectando tooHDInsight emulador, para que você desenvolva seus scripts de Hive localmente sem introduzir qualquer custo, em seguida, execute esses scripts em relação a seus clusters HDInsight. 
  
    Para obter mais informações, consulte muito[esse manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Suporte das Ferramentas do HDInsight para Visual Studio a clusters de Hadoop genéricos** (visualização)
  
    Agora ferramentas HDInsight para Visual Studio oferecem suporte a clusters de Hadoop genéricos, então você pode usar ferramentas do HDInsight para seguir de saudação do Visual Studio toodo:
  
  * Conecte-se o cluster de tooyour 
  * criar uma consulta do Hive com o suporte avançado do IntelliSense/preenchimento automático, 
  * Exiba todos os trabalhos de saudação em seu cluster com uma interface de usuário intuitiva. 
    
    Para obter mais informações, consulte muito[esse manual](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Atualizações do Cache na Função
* **Cache na função** foi atualizada toouse **SDK de armazenamento do Microsoft Azure** versão 4.3. Até agora, Olá **Cache na função** estava usando a versão 1.7 do SDK de armazenamento do Azure.
  
    Os clientes usando o SDK do Azure 2.5 ou abaixo deve atualizar tooAzure SDK 2.6 e mover toohello nova versão do SDK de armazenamento do Azure. 
  
    Esta versão do armazenamento do Azure de tempo 2011-08-18 é agendado toobe removido 1 de agosto de 2016. Quaisquer migrações de Cache na função do Azure SDK 2.5 ou abaixo too2.6 devem ser concluídas neste momento. Para obter mais informações sobre a desativação de saudação do armazenamento do Azure versão 2011-08-18, consulte [serviço de armazenamento do Microsoft Azure versão remoção Update: extensão too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Estamos anunciando Olá 30 de novembro de 2016, desativação para o serviço de Cache gerenciado do Azure e o Cache na função do Azure. É recomendável que você migre tooAzure Cache Redis em preparação para essa desativação. Para obter mais informações sobre datas e diretrizes sobre migração, consulte [Qual oferta de Cache do Azure é adequada para mim?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Ferramentas do Serviço de Aplicativo do Azure
Olá itens a seguir foram atualizado na versão Olá SDK 2.6 do Azure.

* Publicação do Azure aprimorado tooinclude aplicativos de API do Azure como um destino de implantação.
* Aplicativos de API de provisionamento de usuários de tooenable funcionalidade com a criação de API App e funcionalidade de provisionamento.
* Server Explorer alterado tooreflect novo serviço de aplicativo nó, com aplicativos Web, móveis e API agrupados por grupo de recursos.
* Adicionar o gesto de cliente de aplicativo de API do Azure adicionados toomost c# projetos que permite a geração automática de aplicativos de API habilitada Swagger em execução na assinatura do Azure do usuário.
* As ferramentas de Aplicativos de API e os nós de Serviço de Aplicativo no Gerenciador de Servidores estão disponíveis apenas no Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Atualizações das ferramentas do gerenciador de recursos do Azure
ferramentas do Gerenciador de recursos do Azure Olá foram atualizados tooinclude modelos de máquinas virtuais, redes e armazenamento. experiência de edição de JSON Olá foi atualizada tooinclude uma nova exibição de estrutura de tópicos para modelos e Olá capacidade tooedit Olá modelos usando trechos de código do JSON. Modelos implantados no Visual Studio usam um script do PowerShell fornecido com o project Olá, para que as alterações feitas toohello script seja usadas pelo Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Aprimoramentos de diagnóstico para Serviços de Nuvem
2.6 do SDK do Azure recupera o suporte para coletar logs de diagnóstico no emulador de computação do Azure hello e transferi-las toodevelopment armazenamento. Registra qualquer diagnóstico (incluindo os Logs de rastreamento para logs do Windows (ETW), contadores de desempenho, infraestrutura de logs de eventos do windows e de logs de eventos de rastreamento de aplicativo) gerado quando o aplicativo hello está sendo executado no emulador Olá pode ser transferido toodevelopment tooverify de armazenamento que o log de diagnóstico está funcionando no computador local. 

Olá conta de armazenamento de diagnóstico agora pode ser especificado no arquivo de configuração (. cscfg) de serviço Olá tornando mais fácil contas de armazenamento de diagnóstico diferentes toouse para ambientes diferentes. Há algumas diferenças importantes entre como cadeia de caracteres de conexão Olá funcionou no SDK 2.4 do Azure e SDK 2.6 do Azure. Para obter mais informações sobre como ver a cadeia de conexão de armazenamento de diagnóstico de saudação toouse e como ele afeta seus projetos [Configurando o diagnóstico do Azure para serviços de nuvem](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Alterações de última hora
### <a name="azure-resource-manager-tools"></a>Ferramentas do gerenciador de recursos do Azure
* Olá **projetos de implantação de nuvem** disponíveis no hello Azure SDK 2.5 foi renomeado muito do tipo de projeto**o grupo de recursos do Azure**.
* **Projetos de implantação de nuvem** tipo de projetos criados no hello 2.5 do SDK do Azure pode ser usado na versão 2.6 mas haverá falha na implantação de modelo de saudação do Visual Studio. No entanto, a implantação com script do PowerShell de saudação continuarão funcionando como anteriormente.  Para obter informações sobre como toouse **projetos de implantação de nuvem** na versão 2.6 ler este [lançar](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Problemas conhecidos
* Coletar logs de diagnóstico no emulador Olá requer um sistema operacional de 64 bits. Os logs de diagnóstico não serão coletados durante a execução em um sistema operacional de 32 bits. Isso não afeta nenhuma outra funcionalidade do emulador. 
* O SDK do Azure 2.6, lançado, em 29/04/2015, tinha dois problemas: 
  
  * Não foi possível carregar o aplicativo universal no Visual Studio 2015 quando SDK 2.6 do Azure foi instalado na máquina de saudação.
  * Depuração de um projeto de serviço de nuvem falhará no Visual Studio 2013 e Visual Studio 2015 onde o Visual Studio não responde e falhar ao exibir uma caixa de diálogo com a mensagem de saudação "Configurando o diagnóstico para o emulador".
    
    Uma atualização tooAzure 2.6 do SDK foi lançado em 18/5/2015. versão de Hello atualizado é 2.6.30508.1601; ele contém correções para dois problemas descritos acima. Você pode identificar compilação Olá Olá SDK no painel de controle -> Programas e recursos -> Ferramentas do Microsoft Azure para Microsoft Visual Studio 2013 – v 2.6. coluna de versão de Hello exibirá o número de compilação de saudação.
    
    Se você ainda está enfrentando Olá acima problemas, instalar Olá versão mais recente do hello SDK 2.6 do Azure para [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Consulte também
[Suporte e informações de desativação de saudação do Azure SDK para .NET e APIs](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

