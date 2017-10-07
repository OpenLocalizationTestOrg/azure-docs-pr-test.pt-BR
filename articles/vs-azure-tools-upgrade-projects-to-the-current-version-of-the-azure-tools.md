---
title: "aaaHow tooupgrade projetos toohello versão atual do hello ferramentas do Azure | Microsoft Docs"
description: "Saiba como tooupgrade um Azure projeto na versão atual do Visual Studio toohello de saudação ferramentas do Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Como tooupgrade projetos toohello a versão atual do hello ferramentas do Azure para Visual Studio
## <a name="overview"></a>Visão geral
Depois de instalar a versão atual de saudação do hello Azure Tools (ou uma versão anterior que é mais recente de 1.6), os projetos que foram criados usando ferramentas do Azure versão antes de 1.6 (novembro de 2011) serão atualizados automaticamente assim que você abri-los. Se você criou projetos usando Olá versão de 1.6 (novembro de 2011) dessas ferramentas e você ainda tiver a versão instalada, você pode abrir esses projetos na versão mais antiga do hello e posteriormente decidir se tooupgrade-los.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Como o projeto muda quando você o atualiza
Se um projeto é atualizado automaticamente ou se você especificar que você deseja tooupgrade, seu projeto é modificado toowork com as versões atuais de determinados assemblies e algumas propriedades também são alteradas conforme descrito nesta seção. Se seu projeto requer outros toobe alterações compatível com a versão mais recente Olá das ferramentas de saudação, você deve fazer essas alterações manualmente.

* arquivo Web. config de saudação para funções da web e arquivo App. config de saudação para funções de trabalho são tooreference atualizado hello mais recente da versão de Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll.
* assemblies Microsoft.WindowsAzure.StorageClient.dll, Microsoft.WindowsAzure.Diagnostics.dll e Microsoft.WindowsAzure.ServiceRuntime.dll de saudação são atualizados toohello novas versões.
* Perfis de publicação que foram armazenados no arquivo de projeto do Azure hello (. ccproj) são arquivo separado tooa movido, com hello extensão. azurePubxml no hello **publicar** subdiretório.
* Perfil de publicação de algumas propriedades em hello é atualizado toosupport recursos novos e alterados. **AllowUpgrade** é substituído por **DeploymentReplacementMethod** porque você pode atualizar um serviço de nuvem implantado simultaneamente ou gradativamente.
* Olá propriedade **UseIISExpressByDefault** é adicionada e definida toofalse para que hello servidor web que é usado para depurar não será automaticamente alterado de serviços de informações da Internet (IIS) tooIIS Express. O IIS Express é Olá servidor web para projetos que são criados com as versões mais recentes das ferramentas de Olá Olá.
* Se o cache do Azure está hospedado em uma ou mais funções de seu projeto, algumas propriedades na configuração de serviço de saudação (arquivo. cscfg) e a definição de serviço (arquivo. csdef) são alteradas quando um projeto é atualizado. Se o projeto Olá usa o pacote do NuGet do Azure Caching Olá, projeto Olá é toohello atualizado a versão mais recente do pacote de saudação. Você deve abrir o arquivo Web. config de saudação e verificar que configuração de saudação do cliente foi mantida corretamente durante o processo de atualização de saudação. Se você adicionou assemblies de cliente de cache do hello referências tooAzure sem usar o pacote do NuGet hello, esses assemblies não serão atualizados; Você deve atualizar manualmente essas novas versões do referências toohello.

> [!IMPORTANT]
> Para projetos F #, você deve atualizar manualmente os assemblies de tooAzure referências para que eles fazem referência a versões mais recentes Olá desses assemblies.
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>Como tooupgrade um Azure projeto versão atual toohello
1. Instalar Olá versão atual do hello ferramentas do Azure para instalação de saudação do Visual Studio que você deseja toouse para Olá atualizada projeto e hello, em seguida, abrir projeto que você deseja tooupgrade. Se o projeto de saudação foi criado com ferramentas do Azure versão antes de 1.6 (novembro de 2011), o projeto de saudação é versão atual toohello atualizado automaticamente. Se projeto Olá foi criado com hello versão de novembro de 2011 e essa versão ainda estiver instalada, o projeto de saudação é aberto nessa versão.
2. No Solution Explorer, no menu de atalho Olá aberta para o nó do projeto hello, escolha **propriedades**e, em seguida, escolha Olá **aplicativo** guia saudação da caixa de diálogo que aparece.
   
    Olá **aplicativo** guia mostra a versão das ferramentas de saudação que está associado ao projeto hello. Se for exibida a versão atual do hello das ferramentas do Azure, Olá projeto já foi atualizado. Se você instalou uma versão mais recente das ferramentas de saudação que mostra quais guia Olá, um **atualização** botão é exibido.
3. Escolha Olá **atualização** botão tooupgrade uma versão atual do projeto toohello das ferramentas de saudação.
4. Criar projeto hello e resolva os erros resultantes das alterações de API. Para obter informações sobre como toomodify seu código para a nova versão de hello, consulte a documentação de saudação para Olá API específica.

