---
title: "aaaAzure SDK para notas de versão do .NET 2.9"
description: "Notas de versão do SDK do Azure para .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Notas de versão do SDK do Azure para .NET 2.9

Este tópico inclui as notas de versão para as versões 2.9 e 2.9.6 do SDK do Azure para .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Resumo da versão do SDK do Azure para .NET 2.9.6

Data do lançamento: 16/11/2016
 
Sem alterações de quebra toohello Azure SDK 2.9 foram introduzidos nesta versão. Há também não tooleverage do processo de atualização necessário este SDK com projetos de serviço de nuvem existentes.

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 versão Release Candidate

- No Visual Studio RC de 2017, esta versão do hello Azure SDK para .NET é criado de Olá carga de trabalho do Azure. Todas as ferramentas de saudação necessário toodo desenvolvimento do Azure farão parte do Visual Studio 2017 RC no futuro. Para o Visual Studio 2015 e Visual Studio 2013, Olá SDK ainda estarão disponível por meio do WebPI. Suspenderemos o SDK do Azure para versões .NET para o Visual Studio 2013, quando o Visual Studio 2017 for lançado como um produto final. Siga este toodownload link Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Diagnóstico do Azure

- Olá alterados comportamento tooonly armazenar uma cadeia de caracteres de conexão parcial com chave Olá substituído por um token de cadeia de conexão de armazenamento de diagnóstico de serviços de nuvem. chave de armazenamento real do Hello agora é armazenada na pasta de perfil de usuário Olá assim seu acesso pode ser controlado. O Visual Studio lerá a chave de armazenamento de saudação da pasta de perfil de usuário para depuração local e o processo de publicação. 
- Na resposta, altere toohello descrito acima, Visual Studio Online team Olá avançado modelo de tarefa de implantação de serviços de nuvem do Azure para que usuários podem especificar a chave de armazenamento de saudação para definir a extensão de diagnóstico ao publicar tooAzure na integração contínua e a implantação.
- Fizemos-a cadeia de caracteres de conexão segura toostore possíveis e geração de tokens para diagnóstico WAD (Azure), toohelp você solucionar problemas de configuração em environements.
 
### <a name="windows-server-2016-virtual-machines"></a>Máquinas virtuais do Windows Server 2016

- O Visual Studio agora oferece suporte a implantação dos serviços de nuvem tooOS máquinas virtuais de família 5 (Windows Server 2016). Para serviços de nuvem existente, você pode alterar sua configurações tootarget Olá nova família de sistemas operacionais. Ao criar novos serviços em nuvem, se você escolher toocreate Olá serviço usando o .net 4.6 ou posterior, o padrão será Olá serviço toouse 5 de família do sistema operacional.  Para obter mais informações, você pode examinar Olá [família do sistema operacional convidado suporte tabela](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Problemas conhecidos

- SDK do .NET do Azure 2.9.6 introduziu uma restrição que bloqueia a implantação de projetos usando tooany de estruturas (como o .NET 4.6) sem suporte .NET família do sistema operacional < 5. Uma solução alternativa é fornecida [aqui](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Cache na função do Azure 

- O suporte para o Cache na Função do Azure termina em 30 de novembro de 2016. Para obter mais detalhes, clique [aqui](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Modelos do Azure Resource Manager para o Azure Stack

- Apresentamos o Azure Stack como um destino de implantação para seus Modelos do Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Resumo do SDK para .NET 2.9

## <a name="overview"></a>Visão geral
Este documento contém notas de versão de saudação do hello Azure SDK versão 2.9 .NET. 

Para obter informações detalhadas sobre atualizações nesta versão, consulte Olá [post de lançamento do Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Atualização 2 do SDK do Azure 2.9 para Visual Studio 2015 e Visual Studio "15" Preview
Esta atualização inclui Olá correções de bug a seguir:

* Emitir tooREST relacionado geração de API de cliente na cadeia de caracteres que hello "Tipo desconhecido" deverá aparecer como Olá nome da pasta de geração de código hello e/ou Olá Olá namespace soltas no código Olá gerado.
* Emita WebJobs tooScheduled relacionados nos quais Olá informações de autenticação foi com falha toobe passado toohello o processo de provisionamento de Agendador.

Esta atualização inclui Olá novo recurso a seguir:

* Suporte para serviços de aplicativo secundários na guia "Serviços" Olá Olá caixa de diálogo de provisionamento do serviço de aplicativo. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Atualização 2 das Ferramentas do Azure Data Lake para Visual Studio 2015
Esta atualização inclui os seguintes de saudação:

* **Azure Data Lake Tools** para Visual Studio agora é mesclado hello Azure SDK para a versão do .NET. ferramenta de saudação é instalada automaticamente quando você instala o SDK do Azure. 
  
    ferramenta de saudação é atualizada com frequência, vá [aqui](http://aka.ms/datalaketool) tooget Olá atualizações.
* **Gerenciador de servidores** agora permite que você tooview todos e criar algumas entidades de metadados U-SQL. Para saber mais, confira [este](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.

## <a name="hdinsight-tools"></a>Ferramentas do HDInsight
**Ferramentas do HDInsight** para Visual Studio agora dão suporte ao HDInsight versão 3.3, incluindo a exibição de gráficos Tez e outras correções de linguagem.

## <a name="azure-resource-manager"></a>Gerenciador de Recursos do Azure
Essa versão adiciona o suporte para [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) para modelos do Resource Manager.

## <a name="see-also"></a>Consulte também
[Postagem de anúncio do SDK 2.9 do Azure](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

