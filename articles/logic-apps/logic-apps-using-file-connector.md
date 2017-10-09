---
title: "sistemas de aplicativos do Azure lógica de arquivo local aaaConnect tooon | Microsoft Docs"
description: "Conectar sistemas de arquivo de tooon local de seu fluxo de trabalho de aplicativo lógica por meio do gateway de dados local hello e conector de sistema de arquivos"
keywords: sistemas de arquivos
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Conectar sistemas de arquivos local tooon de lógica de aplicativos com o conector de saudação do sistema de arquivo

Conectividade de nuvem híbrida é toologic central aplicativos, dados de caso toomanage e com segurança acesso em recursos locais, seus aplicativos lógicos podem usar o gateway de dados local hello. Neste artigo, mostramos como tooconnect tooan local sistema de arquivos com um cenário básico: copiar um arquivo que tooa de tooDropbox carregado compartilhamento de arquivos, em seguida, envie um email.

## <a name="prerequisites"></a>Pré-requisitos

- Instalar e configurar hello mais recente [gateway de dados no local](https://www.microsoft.com/download/details.aspx?id=53127).
- Instalar o gateway de dados mais recente no local hello, a versão 1.15.6150.1 ou superior. [Conecte-se o gateway de dados local toohello](http://aka.ms/logicapps-gateway) listas Olá etapas. gateway de saudação deve ser instalado em um computador local antes de continuar com o restante de saudação das etapas de saudação.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Adicionar o gatilho e ações para conectar-se o sistema de arquivos tooyour

1. Crie um aplicativo lógico e adicione este gatilho do Dropbox: **Quando um arquivo é criado** 
2. Em um gatilho de saudação, escolha **próxima etapa** > **adicionar uma ação**. 
3. Na caixa de pesquisa hello, digite `file system` para que você possa exibir ações todos com suporte para o conector do sistema de arquivo hello.

   ![Procurar conector de arquivo](media/logic-apps-using-file-connector/search-file-connector.png)

2. Escolha Olá **criar arquivo** ação e criar um sistema de arquivos de tooyour de conexão.

   Se você não tiver uma conexão existente, você é solicitado toocreate um.

   1. Escolha **Conectar por meio do gateway de dados local**. Outras propriedades serão exibidas.
   2. Selecione a pasta raiz do sistema de arquivos.
      
       > [!NOTE]
       > Olá raiz pasta é Olá pai principal, que é usado para caminhos relativos para todas as ações relacionadas ao arquivo. Você pode especificar uma pasta local no computador de saudação onde o gateway de dados local hello está instalado ou pasta Olá pode ser um compartilhamento de rede que Olá máquina pode acessar.

   3. Digite hello username e password para gateway de saudação.
   4. Selecione o gateway Olá instalada anteriormente.

       ![Configurar conexão](media/logic-apps-using-file-connector/create-file.png)

3. Depois de fornecer todos os detalhes de saudação, escolha **criar**. 

   Lógica de aplicativos configura e testa a conexão, certificando-se de que a conexão Olá funcione corretamente. 
   Se a conexão hello está configurado corretamente, você verá opções para a ação de saudação que você selecionou anteriormente. 
   conector de sistema de arquivo Hello agora está pronto para uso.

4. Especifique que você deseja toocopy arquivos da pasta do Dropbox toohello raiz para o compartilhamento de arquivos local.

   ![Ação Criar arquivo](media/logic-apps-using-file-connector/create-file-filled.png)

5. Depois de seu arquivo de saudação de cópias de aplicativo lógica, adicione uma ação do Outlook que envia um email para que usuários relevantes saber sobre o novo arquivo de saudação. Insira os destinatários hello, o título e o corpo do email hello. 

   No seletor de conteúdo dinâmico Olá, você pode escolher saídas de dados do conector de arquivo hello, assim você pode adicionar o email de toohello mais detalhes.

   ![Ação Enviar email](media/logic-apps-using-file-connector/send-email.png)

6. Salve seu aplicativo lógico. Teste seu aplicativo carregando um arquivo tooDropbox. arquivo Hello deve conseguir um compartilhamento de arquivos copiados toohello local e você receberá um email sobre a operação de saudação.

   > [!TIP] 
   > Saiba como muito[monitorar seus aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Parabéns, você agora tem um aplicativo de lógica de trabalho que pode conectar-se o sistema de arquivos local tooyour. Tente explorar outras funcionalidades que Olá ofertas de conector, por exemplo:

- Criar arquivo
- Lista de arquivos na pasta
- Acrescentar arquivo
- Excluir arquivo
- Obter conteúdo do arquivo
- Obter o conteúdo do arquivo usando o caminho
- Obter Metadados do Arquivo
- Obter Metadados do Arquivo usando o caminho
- Lista de arquivos na pasta-raiz
- Atualizar arquivo

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/fileconnector/). 

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder às perguntas e saber quais outros aplicativos do Azure lógica os usuários estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

- [Conecte-se a dados locais tooon](../logic-apps/logic-apps-gateway-connection.md) de aplicativos lógicos
- Saiba mais sobre a [integração de empresas](../logic-apps/logic-apps-enterprise-integration-overview.md)
