---
title: "aaaConfiguring e usando Olá emulador de armazenamento com o Visual Studio | Microsoft Docs"
description: Como configurar e usar o hello emulador de armazenamento com o Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: c8e7996f-6027-4762-806e-614b93131867
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/17/2017
ms.author: kraigb
ms.openlocfilehash: d590f21146c86bcb7bfa6b6164b92c6df5938d5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-and-using-hello-storage-emulator-with-visual-studio"></a>Como configurar e usar o hello emulador de armazenamento com o Visual Studio
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Visão geral
ambiente de desenvolvimento do SDK do Azure Olá inclui o emulador de armazenamento hello, um utilitário que simula Olá Blob, fila e tabela de serviços de armazenamento disponíveis no Azure em sua máquina de desenvolvimento local. Se você estiver criando um serviço de nuvem que utiliza os serviços de armazenamento do Azure hello, ou gravar todos os aplicativos externos chamadas Olá serviços de armazenamento, você pode testar seu código localmente no emulador de armazenamento de saudação. Olá ferramentas do Azure para Microsoft Visual Studio integra o gerenciamento de emulador de armazenamento Olá no Visual Studio. Ferramentas do Azure Olá inicializar banco de dados do emulador de armazenamento de saudação no primeiro uso, inicia Olá serviço emulador de armazenamento quando você executa ou depura seu código do Visual Studio e fornece acesso somente leitura toohello armazenamento emulador dados via hello Azure Storage Explorer.

Para obter informações detalhadas sobre o emulador de armazenamento hello, incluindo requisitos de sistema e instruções de configuração personalizada, consulte [Olá Use Azure Storage Emulator para desenvolvimento e testes](storage/common/storage-use-emulator.md).

> [!NOTE]
> Há algumas diferenças na funcionalidade entre a simulação de emulador de armazenamento hello e serviços de armazenamento do Azure hello. Consulte [Olá diferenças entre o emulador de armazenamento e serviços de armazenamento do Azure](storage/common/storage-use-emulator.md) em Olá documentação do SDK do Azure para obter informações sobre diferenças específicas hello.
> 
> 

## <a name="configuring-a-connection-string-for-hello-storage-emulator"></a>Configurando uma cadeia de caracteres de conexão para o emulador de armazenamento Olá
emulador de armazenamento tooaccess saudação do código dentro de uma função, você desejará tooconfigure uma conexão que emulador de armazenamento toohello pontos de cadeia de caracteres e que posteriormente pode ser alterado toopoint tooan conta de armazenamento do Azure. Uma cadeia de caracteres de conexão é uma configuração que sua função pode ler a conta de armazenamento do tempo de execução tooconnect tooa. Para obter mais informações sobre como toocreate cadeias de caracteres de conexão, consulte [Olá Configurando aplicativos do Azure](https://msdn.microsoft.com/library/azure/2da5d6ce-f74d-45a9-bf6b-b3a60c5ef74e#BK_SettingsPage).

> [!NOTE]
> Você pode retornar uma conta de emulador de armazenamento de toohello de referência no seu código usando Olá **DevelopmentStorageAccount** propriedade. Essa abordagem funciona corretamente se você quiser tooaccess Olá emulador de armazenamento do seu código, mas se você planejar toopublish tooAzure seu aplicativo, será necessário toocreate um tooaccess de cadeia de caracteres de conexão sua conta de armazenamento do Azure e modificar seu código toouse que cadeia de conexão antes de publicá-lo. Se estiver alternando entre a conta do emulador de armazenamento hello e uma conta de armazenamento do Azure com frequência, uma cadeia de caracteres de conexão será simplificar esse processo.
> 
> 

## <a name="initializing-and-running-hello-storage-emulator"></a>Inicializando e executando o emulador de armazenamento Olá
Você pode especificar que, quando você executa ou depurar seu serviço no Visual Studio, o Visual Studio automaticamente inicia o emulador de armazenamento hello. No Solution Explorer, abra o menu de atalho de saudação seu **Azure** do projeto e escolha **propriedades**. Em Olá **desenvolvimento** guia Olá **iniciar o emulador de armazenamento do Azure** , escolha **True** (se ela já não está configurada toothat valor).

Olá a primeira vez que você executar ou depurar seu serviço no Visual Studio, o emulador de armazenamento Olá inicia um processo de inicialização. Esse processo reserva portas locais para o emulador de armazenamento hello e cria o banco de dados de emulador de armazenamento hello. Uma vez concluído, esse processo não precisa toorun novamente, a menos que o banco de dados de emulador de armazenamento Olá é excluído.

> [!NOTE]
> A partir da versão de junho de 2012 de saudação do hello ferramentas do Azure, o emulador de armazenamento Olá é executado, por padrão, no SQL Express LocalDB. Em versões anteriores do hello ferramentas do Azure, o emulador de armazenamento Olá é executado em relação a uma instância padrão do SQL Express 2005 ou 2008, que deve ser instalado antes de instalar o hello SDK do Azure. Você também pode executar o emulador de armazenamento Olá em relação a uma instância nomeada do SQL Express ou um conjunto nomeado ou padrão do Microsoft SQL Server. Se você precisar toorun de emulador de armazenamento tooconfigure Olá em relação a uma instância padrão além hello, consulte [Olá Use Azure Storage Emulator para desenvolvimento e testes](storage/common/storage-use-emulator.md).
> 
> 

emulador de armazenamento Olá fornece um status de saudação do usuário interface tooview Olá local de serviços de armazenamento e toostart, pare e redefini-los. Depois que o serviço do emulador de armazenamento Olá tiver sido iniciado, você pode exibir a interface do usuário hello ou iniciar ou parar o serviço clicando com o ícone da área de notificação para Olá Olá Olá emulador do Microsoft Azure na barra de tarefas de Windows hello.

## <a name="viewing-storage-emulator-data-in-server-explorer"></a>Exibindo dados do emulador de armazenamento no Gerenciador de Servidores
nó de armazenamento do Azure Olá no Gerenciador de servidores permite que você tooview dados e alterar as configurações para o blob e dados de tabela em suas contas de armazenamento, incluindo Olá emulador de armazenamento. Consulte [Gerenciar recursos do Armazenamento de Blobs do Azure com o Gerenciador de Armazenamento (Versão Prévia)](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs) para obter mais informações.

