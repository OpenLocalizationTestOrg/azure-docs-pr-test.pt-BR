---
title: "aaaAzure SDK para notas de versão do .NET 3.0 | Microsoft Docs"
description: "Notas de Versão do SDK do Azure para .NET 3.0"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Notas de versão do SDK do Azure para .NET 3.0

Este tópico inclui as notas de versão para a versão 3.0 de saudação do SDK do Azure para .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Resumo da versão do SDK do Azure para .NET 3.0

Data do lançamento: 03/07/2017
 
Nenhum toohello de alterações de quebra do Azure SDK 3.0 foram introduzidos nesta versão. Há também não tooleverage do processo de atualização necessário este SDK com projetos de serviço de nuvem existentes. uso de tooallow de saudação do Azure SDK 3.0 sem a necessidade de um processo de atualização, o Azure SDK 3.0 instala toohello mesmos diretórios do Azure SDK 2.9. A maioria dos componentes de saudação não alterou versão principal de saudação do 2.9 mas recém-atualizado em vez disso, o número de compilação Olá.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- No Visual Studio de 2017, esta versão do hello Azure SDK para .NET é criado na toohello carga de trabalho do Azure. Todas as ferramentas de saudação necessário toodo desenvolvimento do Azure farão parte do Visual Studio de 2017 no futuro. Para Visual Studio 2015 Olá SDK ainda estarão disponível por meio do WebPI. Agora que o Visual Studio 2017 foi lançado, descontinuamos as versões do SDK do Azure para .NET para Visual Studio 2013.

### <a name="azure-diagnostics"></a>Diagnóstico do Azure

- Olá alterados comportamento tooonly armazenar uma cadeia de caracteres de conexão parcial com chave Olá substituído por um token de cadeia de conexão de armazenamento de diagnóstico de serviços de nuvem. chave de armazenamento real do Hello agora é armazenada na pasta de perfil de usuário Olá assim seu acesso pode ser controlado. O Visual Studio lerá a chave de armazenamento de saudação da pasta de perfil de usuário para depuração local e o processo de publicação. 
- Na resposta, altere toohello descrito acima, Visual Studio Online team Olá avançado modelo de tarefa de implantação de serviços de nuvem do Azure para que usuários podem especificar a chave de armazenamento de saudação para definir a extensão de diagnóstico ao publicar tooAzure na integração contínua e a implantação.
- Fizemos-a cadeia de caracteres de conexão segura toostore possíveis e geração de tokens para diagnóstico WAD (Azure), toohelp você solucionar problemas de configuração em environements.
 
### <a name="windows-server-2016-virtual-machines"></a>Máquinas virtuais do Windows Server 2016

- O Visual Studio agora oferece suporte a implantação dos serviços de nuvem tooOS máquinas virtuais de família 5 (Windows Server 2016). Para serviços de nuvem existente, você pode alterar sua configurações tootarget Olá nova família de sistemas operacionais. Ao criar novos serviços em nuvem, se você escolher toocreate Olá serviço usando o .net 4.6 ou posterior, o padrão será Olá serviço toouse 5 de família do sistema operacional.  Para obter mais informações, você pode examinar Olá [família do sistema operacional convidado suporte tabela](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Problemas conhecidos

- O SDK do Azure para .NET 3.0 apresentou um problema ao remover o Visual Studio 2017 em uma configuração lado a lado com o Visual Studio 2015.  Se você tiver Olá SDK do Azure instalado para Visual Studio 2015, Olá emulador de armazenamento do Microsoft Azure e o emulador de computação do Microsoft Azure serão removidos se você desinstalar o Visual Studio de 2017.  Isso produzirá um erro durante a criação e depuração de novos projetos de serviços de nuvem no Visual Studio 2015. Em ordem toofix esse problema, reinstale o hello Azure SDK de Olá Web Platform Installer.  Olá problema será resolvido em uma atualização futura do Visual Studio de 2017.  .

 
### <a name="azure-in-role-cache"></a>Cache na função do Azure 

- O suporte para Cache na Função do Azure terminou em 30 de novembro de 2016. Para obter mais detalhes, clique [aqui](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




