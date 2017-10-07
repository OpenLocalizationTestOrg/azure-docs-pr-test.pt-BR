---
title: aaaUse Robomongo para o banco de dados do Azure Cosmos | Microsoft Docs
description: 'Saiba como toouse Robomongo com um banco de dados do Azure Cosmos: API de conta do MongoDB'
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Usar o Robomongo com uma conta do Azure Cosmos DB: API para MongoDB
tooconnect tooan o banco de dados do Azure Cosmos: API de conta do MongoDB usando Robomongo, você deve:

* Baixar e instalar o [Robomongo](https://robomongo.org/)
* Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB

## <a name="connect-using-robomongo"></a>Conectar usando o Robomongo
tooadd seu banco de dados do Azure Cosmos: API para o MongoDB conta toohello Robomongo MongoDB conexões, executar Olá etapas a seguir.

1. Recuperar o banco de dados do Azure Cosmos: API de informações de conexão da conta de MongoDB usando instruções Olá [aqui](connect-mongodb-account.md).

    ![Captura de tela da folha de cadeia de caracteres de conexão Olá](./media/mongodb-robomongo/connectionstringblade.png)
2. Execute *Robomongo.exe*

3. Botão de conexão Olá em **arquivo** toomanage suas conexões. Em seguida, clique em **criar** em Olá **MongoDB conexões** janela, que será aberta, Olá **configurações de Conexão** janela.

4. Em Olá **configurações de Conexão** janela, escolha um nome. Em seguida, localize Olá **Host** e **porta** de suas informações de conexão na etapa 1 e inseri-las em **endereço** e **porta**, respectivamente .

    ![Captura de tela de saudação Robomongo gerenciar conexões](./media/mongodb-robomongo/manageconnections.png)
5. Em Olá **autenticação** , clique em **executar autenticação**. Em seguida, insira seu Banco de dados (o padrão é *Admin*), **Nome de Usuário** e **Senha**.
Tanto o **Nome de Usuário** quanto a **Senha** podem ser encontrados em suas informações de conexão na Etapa 1.

    ![Captura de tela de saudação Robomongo guia de autenticação](./media/mongodb-robomongo/authentication.png)
6. Em Olá **SSL** guia, verifique **protocolo usar SSL**, em seguida, altere a saudação **método de autenticação** muito**certificado autoassinado**.

    ![Captura de tela de saudação Robomongo SSL guia](./media/mongodb-robomongo/SSL.png)
7. Por fim, clique em **teste** tooverify que você está tooconnect pode, em seguida, **salvar**.

## <a name="next-steps"></a>Próximas etapas
* Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.
