---
title: "aaaAzure SDK para notas de versão do .NET 2.8"
description: "Notas de versão SDK do Azure para .NET 2.8"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>SDK do Azure para .NET 2.8, 2.8.1 e 2.8.2
## <a name="overview"></a>Visão geral
Este artigo contém as notas de versão de saudação (que inclui os problemas conhecidos e as alterações recentes) para Olá SDK do Azure do 2.8 .NET, 2.8.1 e 2.8.2 versões. 

Para obter uma lista completa dos novos recursos e as atualizações feitas nesta versão, consulte Olá [2.8 do SDK do Azure para Visual Studio 2013 e Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) comunicado. 

## <a name="azure-sdk-for-net-28"></a>SDK do Azure para .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Baixar o SDK do Azure para .NET 2.8
[SDK do Azure para .NET 2.8 para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[SDK do Azure para .NET 2.8 para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Suporte do .NET 4.5.2
#### <a name="known-issues"></a>Problemas conhecidos
2.8 de SDK .NET do Azure permite que você toocreate .NET 4.5.2 pacotes de serviço de nuvem. No entanto o .NET 4.5.2 framework não será instalado no padrão de saudação versão de imagens do sistema operacional convidado até que o sistema operacional convidado de janeiro de 2016. Até lá, a estrutura do .NET 4.5.2 estará disponível por meio de uma versão distinta do SO convidado, de 2 de novembro de 2015. Consulte Olá [versões de sistema operacional convidado do Azure e matriz de compatibilidade do SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack de página quando a imagem de saudação será lançada.  Depois que a imagem do hello novembro de 2015-02 é liberada você pode escolher toouse essa imagem, atualizando o arquivo de configuração serviço de nuvem (. cscfg). Na configuração de serviço Olá arquivo definir atributo de osVersion de saudação de cadeia de caracteres do hello ServiceConfiguration elemento toohello "WA-GUEST-OS-4.26_201511-02". Se você escolher tooopt toouse essa imagem, em seguida, você não receberá atualizações automáticas toohello sistema operacional convidado. tooget Olá atualizações automáticas Olá osVersion deve ser definido muito "*" e o .NET 4.5.2 só estará disponível por meio de atualizações automáticas em janeiro de 2016.

### <a name="azure-data-factory"></a>Fábrica de dados do Azure
#### <a name="known-issues"></a>Problemas conhecidos
Durante uma **modelo de fábrica de dados** dados de exemplo que envolvem a criação de projeto, o script PowerShell do azure pode falhar se a versão do azure power shell instalado na máquina de saudação após 0.9.8.

Em ordem toosuccessfully criar este tipo de projeto, você deve instalar [versão do azure power shell 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Ferramentas do gerenciador de recursos do Azure
#### <a name="breaking-changes"></a>Alterações de última hora
Olá script do PowerShell fornecida pelo projeto do grupo de recursos do Azure Olá foi atualizado no toowork versão com hello novos cmdlets do PowerShell do Azure versão 1.0.  Esse novo script não funcionará de com o Visual Studio ao usar uma versão de hello SDK anterior too2.8.  

Scripts de projetos criados em versões anteriores do SDK de saudação não serão executado de dentro do Visual Studio quando usando Olá 2.8 SDK.  Todos os scripts continuará toowork fora do Visual Studio com versão apropriada de saudação do hello cmdlets do PowerShell do Azure.  

Olá SDK 2.8 requer a versão 1.0 do hello cmdlets do PowerShell do Azure.  Todas as outras versões do SDK do hello exigem a versão 0.9.8 do hello cmdlets do PowerShell do Azure.  Para saber mais, confira [este](http://go.microsoft.com/fwlink/?LinkID=623011) blog.

### <a name="web-tools-extensions"></a>Extensões de Ferramentas da Web
#### <a name="known-issues"></a>Problemas conhecidos
Olá problemas conhecidos a seguir será abordado nas Olá após o lançamento.

* O Serviço de Aplicativo relacionado aos gestos do Gerenciador de Servidores e Nuvem para ambientes de não produção (como clientes do Azure China ou Azure Stack) não funciona. Para clientes nessas áreas afetadas, baixando Olá publicar perfil da saudação portal do Azure permitirá capacidade de publicação. Uma versão futura irá reparar gestos como “Anexar Depurador” e “Exibir Logs de Streaming” para clientes do Azure China e Azure Stack. 
* Os clientes podem ver erros durante a criação de quando ideias de aplicativo hello instância toowhich que estão sendo implantados está em uma região diferente Leste dos EUA do serviço de aplicativo. Nesses cenários, criando um aplicativo de serviço no portal de saudação e baixar Olá perfil de publicação permite cenários de publicação. 

### <a name="azure-hdinsight-tools"></a>Ferramentas do Azure HDInsight
#### <a name="new-updates"></a>Novas atualizações
* Você pode executar sua consulta de Hive no cluster Olá via HiveServer2 com quase nenhuma sobrecarga e ver o trabalho de saudação fizer logon em tempo real.
* Usando Olá nova seção tarefa execução exibição você pode examinar seu trabalho mais profundo encontrar mais detalhes e identificar possíveis problemas.

Para saber mais, confira [SDK 2.8 do Azure para Visual Studio 2013 e Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>SDK do Azure para .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Problemas conhecidos do Visual Studio 2013 e do Visual Studio 2015
1. Disparado WebJob publica tooslots será mostrar e erro e não definir um agendamento, mas ele enviará por push Olá WebJob tooAzure. Os clientes que necessitam de um trabalho agendado, em seguida, podem usar hello Azure Portal tooset agenda Olá para Olá WebJob. 
2. Os clientes do Python podem enfrentar problemas de depuração. Equipe de serviço está implantando uma correção para esse, mas se os clientes são afetados, por favor, permitem que a Microsoft sabe nos fóruns de saudação ou no blog de anúncio hello ou seção de comentários de notas de versão. 
3. Os clientes em determinadas regiões (por exemplo, Sul da Índia) devem passar por erros de provisionamento do Serviço de Aplicativo. Isso é consistente com o portal de saudação e os clientes que esse problema podem usar Olá toorequest portal do Azure acesso toopublish toothese regiões geográficas. Quando eles solicitam acesso toothese regiões usando Olá provisionamento portal do Azure deve funcionar. 

## <a name="azure-sdk-for-net-282"></a>SDK do Azure para .NET 2.8.2
Após a instalação de saudação das ferramentas de saudação 2.8.2, os clientes podem enfrentar Olá problema a seguir.         

* Se você estiver usando o Windows 10 e não tiver instalado o Internet Explorer, poderá receber um erro de "Internet Explorer não encontrado".
  problema de saudação tooresolve, instale o Internet Explorer usando Olá Adicionar/remover a caixa de diálogo de componentes do Windows.

Se você observar esse problema, use o hello para enviar um Smiley recurso tooreport-lo.

Para obter mais informações, confira [esta](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) postagem.

## <a name="other-updates"></a>Outras atualizações
Para obter outras atualizações, confira a [postagem de comunicado do SDK do Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Consulte também
[Postagem de anúncio do SDK 2.8 do Azure](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Suporte e informações de desativação de saudação do Azure SDK para .NET e APIs](https://msdn.microsoft.com/library/azure/dn479282.aspx)

