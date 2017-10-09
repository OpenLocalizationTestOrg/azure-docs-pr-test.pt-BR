---
title: "aaaEncode ou decodificar arquivos simples em aplicativos lógicos do Azure | Microsoft Docs"
description: "Como toouse Olá codificador de arquivo do arquivo ou decodificador em Olá Enterprise Integration Pack em seus aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Visão geral da integração corporativa com arquivos simples

Talvez você queira tooencode XML conteúdo antes de enviá-la tooa parceiro de negócios em um cenário entre empresas (B2B). Em um aplicativo de lógica, você pode usar o arquivo simples de saudação codificação conector toodo isso. Olá aplicativo lógico que você criar pode obter seu XML conteúdo de uma variedade de fontes, inclusive de um gatilho de solicitação HTTP, de outro aplicativo ou até mesmo em uma saudação muitas [conectores](../connectors/apis-list.md). Para obter mais informações sobre aplicativos lógicos, consulte Olá [documentação de aplicativos lógica](logic-apps-what-are-logic-apps.md "saber mais sobre aplicativos lógicos").  

## <a name="create-hello-flat-file-encoding-connector"></a>Criar o conector de codificação de arquivo simples de saudação
Siga estas etapas tooadd um conector tooyour lógica aplicativo de codificação de arquivo simples.

1. Criar um aplicativo de lógica e [vinculá-lo a conta de integração de tooyour](logic-apps-enterprise-integration-accounts.md "Saiba toolink um aplicativo de conta tooa lógica da integração"). Esta conta contém o esquema de saudação usará tooencode Olá dados XML.  
2. Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.  
   ![Captura de tela de gatilho tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Adicione arquivo simples de saudação codificação ação, da seguinte maneira:
   
    a. Selecione Olá **mais** sinal.
   
    b. Selecione Olá **adicionar uma ação** link (aparece depois que você selecionou o sinal de adição Olá).
   
    c. Na caixa de pesquisa hello, digite *simples* toofilter todos Olá toohello ações um que você deseja toouse.
   
    d. Selecione Olá **codificação de arquivo simples** opção na lista de saudação.   
   ![Captura de tela da opção Codificação de Arquivo Simples](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Em Olá **codificação de arquivo simples** caixa de diálogo, selecione Olá **conteúdo** caixa de texto.  
   ![Captura de tela da caixa de texto Conteúdo](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Selecione a marca de corpo de Olá como Olá conteúdo que você deseja tooencode. marca de corpo Olá preencherá o campo de conteúdo de saudação.     
   ![Captura de tela da marca body](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Selecione Olá **nome do esquema** caixa de listagem e escolha o conteúdo de entrada de esquema Olá deseja toouse tooencode hello.    
   ![Captura de tela da caixa de listagem Nome do Esquema](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Salve seu trabalho.   
   ![Captura de tela do ícone Salvar](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

Neste ponto, você já configurou seu conector de codificação de arquivo simples. Em um aplicativo do mundo real, convém toostore dados de saudação codificado em um aplicativo de linha de negócios, como o Salesforce. Ou você pode enviar essa tooa dados codificados parceiro comercial. Você pode adicionar facilmente uma saída de hello toosend ação de saudação codificação tooSalesforce de ação ou tooyour de parceiro comercial, usando qualquer um dos Olá outros conectores fornecidos.

Agora você pode testar seu conector, um ponto de extremidade HTTP de toohello de solicitação e incluindo o conteúdo XML de saudação no corpo de saudação de solicitação de saudação.  

## <a name="create-hello-flat-file-decoding-connector"></a>Criar o arquivo simples de saudação decodificação de conector

> [!NOTE]
> toocomplete essas etapas, você precisa toohave um arquivo de esquema já carregado na conta de integração.

1. Adicionar um **solicitar - quando HTTP de uma solicitação é recebida** gatilho tooyour lógica aplicativo.  
   ![Captura de tela de gatilho tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Adicione arquivo simples de saudação decodificação de ação, da seguinte maneira:
   
    a. Selecione Olá **mais** sinal.
   
    b. Selecione Olá **adicionar uma ação** link (aparece depois que você selecionou o sinal de adição Olá).
   
    c. Na caixa de pesquisa hello, digite *simples* toofilter todos Olá toohello ações um que você deseja toouse.
   
    d. Selecione Olá **decodificação de arquivo simples** opção na lista de saudação.   
   ![Captura de tela da opção Decodificação de Arquivo Simples](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Selecione Olá **conteúdo** controle. Isso produz uma lista de conteúdo anteriores etapas que você pode usar como toodecode conteúdo Olá Olá. Observe que Olá *corpo* de saudação solicitação HTTP de entrada está disponível toobe usado como Olá toodecode conteúdo. Você também pode inserir toodecode conteúdo Olá diretamente em Olá **conteúdo** controle.     
4. Selecione Olá *corpo* marca. Aviso Olá corpo marca está agora no hello **conteúdo** controle.
5. Selecione o nome de saudação do esquema de saudação que você deseja que o conteúdo de saudação do toouse toodecode. Olá seguinte captura de tela mostra que *OrderFile* é o nome de esquema selecionado hello. Esse nome de esquema tiver foi carregado na conta de integração de saudação anteriormente.
   
   ![Captura de tela da caixa de diálogo Decodificação de Arquivo Simples](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Salve seu trabalho.  
   ![Captura de tela do ícone Salvar](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

Neste ponto, você já configurou seu conector de decodificação de arquivo simples. Em um aplicativo do mundo real, pode deseja toostore Olá decodificar dados em um aplicativo de linha de negócios, como a equipe de vendas. Você pode adicionar facilmente uma saída de hello toosend ação de saudação decodificação tooSalesforce de ação.

Agora você pode testar seu conector fazendo um ponto de extremidade HTTP de toohello de solicitação e incluindo Olá XML conteúdo você deseja toodecode no corpo de saudação de solicitação de saudação.  

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise").  

