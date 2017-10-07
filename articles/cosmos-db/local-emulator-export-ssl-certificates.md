---
title: "certificados de emulador do Azure Cosmos DB Olá aaaExport | Microsoft Docs"
description: "Ao desenvolver em idiomas e tempos de execução que não usam o repositório de certificados do Windows hello será necessário tooexport e gerencie certificados SSL de saudação. Esta postagem fornece instruções passo a passo."
services: cosmos-db
documentationcenter: 
keywords: Emulador do Azure Cosmos DB
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Exportar hello Azure Cosmos DB emulador certificados para uso com o Java, Python e Node.js

[**Baixar Olá emulador**](https://aka.ms/cosmosdb-emulator)

Hello Azure Cosmos DB emulador fornece um ambiente local que emula Olá serviço de banco de dados do Azure Cosmos para fins de desenvolvimento, incluindo o uso de conexões SSL. Esta postagem demonstra como tooexport Olá SSL certificados para uso em idiomas e tempos de execução que não integram Olá repositório de certificados do Windows, como Java que usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) e Python que usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html) e Node. js que usa [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Você pode ler mais sobre o emulador de saudação do [Olá Use Azure Cosmos DB Emulator para desenvolvimento e teste](./local-emulator.md).

Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Rotação de certificados
> * Exportando o certificado SSL
> * Aprender como toouse Olá certificado em Java, Python e Node.js

## <a name="certification-rotation"></a>Rotação de certificação

Certificados no hello que emulador Local do banco de dados do Azure Cosmos são gerados Olá primeira execução do emulador hello. Há dois certificados. Um usado para conectar um emulador local toohello e para gerenciar segredos no emulador de saudação. Olá certificado tooexport é certificado de conexão de saudação com o nome amigável do hello "DocumentDBEmulatorCertificate".

Ambos os certificados podem ser regenerados clicando **Redefinir dados** conforme mostrado abaixo do Azure Cosmos DB emulador em execução no hello bandeja do Windows. Se você gerar novamente os certificados de saudação e instalou-los no repositório de certificados do Java hello ou usá-los em outro lugar, você precisará tooupdate-las, caso contrário, se seu aplicativo não conectará toohello um emulador local.

![Redefinição de dados do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Como tooexport Olá certificado SSL de banco de dados do Azure Cosmos

1. Inicie o Gerenciador de certificados do Windows hello executando certlm.msc e navegue toohello pessoal -> pasta certificados e certificado Olá aberta com o nome amigável da saudação **DocumentDbEmulatorCertificate**.

    ![Etapa 1 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Clique em **Detalhes** e depois em **OK**.

    ![Etapa 2 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Clique em **copiar tooFile... **.

    ![Etapa 3 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Clique em **Avançar**.

    ![Etapa 4 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Clique em **Não, não exportar a chave privada** e, em seguida, clique em **Avançar**.

    ![Etapa 5 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Clique em **X.509 codificado em Base-64 (.CER)** e depois em **Avançar**.

    ![Etapa 6 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Dê um nome de certificado hello. Nesse caso, **documentdbemulatorcert** e, em seguida, clique em **Avançar**.

    ![Etapa 7 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Clique em **Concluir**.

    ![Etapa 8 de exportação do emulador local do Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Como toouse Olá certificado em Java

Durante a execução de aplicativos Java ou MongoDB que usam o cliente de Java Olá é mais fácil certificado de saudação tooinstall no repositório de certificados do hello Java padrão que passando hello "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" sinalizadores. Por exemplo hello incluído [aplicativo Java demonstração](https://localhost:8081/_explorer/index.html) depende do repositório de certificados saudação padrão.

Siga as instruções de Olá Olá [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport Olá x. 509 do certificado no repositório de certificados de Java saudação padrão. Lembre-Lembre-se estará trabalhando no diretório Olá % JAVA_HOME % durante a execução keytool.

Uma vez hello "CosmosDBEmulatorCertificate" SSL certificado está instalado seu aplicativo deve ser capaz de tooconnect e use Olá emulador local de banco de dados de Cosmos do Azure. Se você continuar toohave problemas convém Olá toofollow [conexões de SSL/TLS depuração](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) artigo. É muito provável certificado Olá não está instalado no repositório de %JAVA_HOME%/jre/lib/security/cacerts hello. Por exemplo, se você tiver várias versões instaladas do Java seu aplicativo pode estar usando um repositório cacerts diferentes de Olá uma atualização.

## <a name="how-toouse-hello-certificate-in-python"></a>Como toouse Olá certificado no Python

Por saudação padrão [SDK(version 2.0.0 or higher) Python](documentdb-sdk-python.md) para Olá API DocumentDB não tente e usar certificado SSL da saudação ao se conectar a um emulador local toohello. Se, no entanto, você deseja toouse SSL validação, você pode seguir exemplos Olá Olá [Python soquete wrappers](https://docs.python.org/2/library/ssl.html) documentação.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Como toouse Olá certificado no Node. js

Por saudação padrão [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) para Olá API DocumentDB não tente e usar certificado SSL da saudação ao se conectar a um emulador local toohello. Se, no entanto, você deseja toouse SSL validação, você pode seguir exemplos Olá Olá [Node. js documentação](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Trocou certificados
> * Certificado SSL hello exportada
> * Aprendeu como toouse Olá certificado em Java, Python e Node.js

Você pode continuar toohello seção conceitos para obter mais informações sobre o banco de dados do Cosmos.

> [!div class="nextstepaction"]
> [Distribuição global](distribute-data-globally.md) 
