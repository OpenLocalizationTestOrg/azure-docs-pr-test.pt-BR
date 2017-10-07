---
title: "aaaManage uma conta de banco de dados do Azure Cosmos por meio de saudação Portal do Azure | Microsoft Docs"
description: "Saiba como toomanage seu banco de dados do Azure Cosmos conta por meio de saudação Portal do Azure. Localize um guia sobre como usar o hello Azure Portal tooview, copiar e excluir contas de acesso."
keywords: Portal do Azure, banco de dados de documentos, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>Como toomanage uma conta de banco de dados do Azure Cosmos
Saiba como trabalhar com chaves tooset de consistência global e excluir uma conta de banco de dados do Azure Cosmos Olá portal do Azure.

## <a id="consistency"></a>Gerenciar as configurações de consistência do Azure Cosmos DB
Selecionar um nível de consistência direita Olá depende da semântica de saudação do seu aplicativo. Você deve se familiarizar com níveis de consistência disponível Olá no banco de dados do Azure Cosmos lendo [usar consistência níveis toomaximize disponibilidade e desempenho no banco de dados do Azure Cosmos][consistency]. O Azure Cosmos DB fornece garantias de consistência, disponibilidade e desempenho, em cada nível de consistência disponível para sua conta de banco de dados. Configurar sua conta de banco de dados com um nível de consistência de alta segurança exige que seus dados são restrita tooa única região do Azure e não está disponível globalmente. Olá outro lado, Olá níveis de consistência reduzida - desatualização associada, sessão ou eventual habilitar você tooassociate qualquer número de regiões do Azure com sua conta do banco de dados. Olá simples etapas a seguir mostra como tooselect Olá nível de consistência de padrão para sua conta de banco de dados. 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>consistência do toospecify saudação padrão para uma conta de banco de dados do Azure Cosmos
1. Em Olá [portal do Azure](https://portal.azure.com/), acessar sua conta do banco de dados do Azure Cosmos.
2. Na folha de conta hello, clique em **padrão consistência**.
3. Em Olá **consistência padrão** folha, o novo nível de consistência Olá selecione e clique em **salvar**.
    ![Sessão de consistência padrão][5]

## <a id="keys"></a>Exibir, copiar e regenerar chaves de acesso
Quando você cria uma conta de banco de dados do Azure Cosmos, o serviço de hello gera duas chaves de acesso principal que podem ser usadas para autenticação quando hello Azure Cosmos DB conta é acessada. Fornecendo duas chaves de acesso, o banco de dados do Azure Cosmos permite chaves de saudação tooregenerate com tooyour sem interrupção conta de banco de dados do Azure Cosmos. 

Em Olá [portal do Azure](https://portal.azure.com/), Olá acesso **chaves** folha no menu recursos Olá Olá de **conta de banco de dados do Azure Cosmos** tooview de folha, copiar e regenerar Olá chaves de acesso que são usados tooaccess sua conta de banco de dados do Azure Cosmos.

![Captura de tela do Portal do Azure, folha Chaves](./media/manage-account/keys.png)

> [!NOTE]
> Olá **chaves** folha também inclui primário e cadeias de caracteres de conexão secundário que podem ser usado tooconnect tooyour conta de saudação [ferramenta de migração de dados](import-data.md).
> 
> 

Chaves somente leitura também estão disponíveis nessa folha. Leituras e consultas são operações somente leitura, ao contrário de criações, exclusões e substituições.

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Copiar uma chave de acesso no hello Portal do Azure
Em Olá **chaves** folha, clique em Olá **cópia** toohello botão à direita da chave de saudação desejar toocopy.

![Exibir e copiar uma chave de acesso no Portal do Azure, folha de chaves de saudação](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>Regenerar chaves de acesso
Você deve alterar a conta de banco de dados do Azure Cosmos Olá acesso chaves tooyour periodicamente toohelp manter suas conexões mais segura. Duas chaves de acesso atribuídas tooenable você toomaintain conexões toohello conta de banco de dados do Azure Cosmos usando uma chave de acesso enquanto você regenera Olá outra chave de acesso.

> [!WARNING]
> Regenerar suas chaves de acesso afeta todos os aplicativos que dependem da chave atual hello. Clientes que usam a conta de banco de dados do Azure Cosmos Olá acesso à chave tooaccess Olá devem ser a nova chave de saudação toouse atualizado.
> 
> 

Se você tiver aplicativos ou serviços de nuvem usando hello Azure Cosmos DB conta, você perderá conexões Olá se você regenerar chaves, a menos que você reverter suas chaves. Olá, etapas a seguir descrevem Olá processo envolvido na substituição de suas chaves.

1. Atualize a chave de acesso de saudação na sua chave de acesso secundária do aplicativo código tooreference Olá de hello Azure Cosmos DB conta.
2. Regenere a chave de acesso primária Olá para sua conta de banco de dados do Azure Cosmos. Em Olá [Portal do Azure](https://portal.azure.com/), acessar sua conta do banco de dados do Azure Cosmos.
3. Em Olá **conta de banco de dados do Azure Cosmos** folha, clique em **chaves**.
4. Em Olá **chaves** folha, clique botão regenerar hello, clique **Okey** tooconfirm que você deseja toogenerate uma nova chave.
    ![Regenerar chaves de acesso](./media/manage-account/regenerate-keys.png)
5. Depois de verificar a nova chave hello está disponível para uso (aproximadamente 5 minutos após a regeneração), atualizar a chave de acesso de saudação na aplicativo código tooreference Olá nova chave de acesso primária.
6. Regenere a chave de acesso secundária hello.
   
    ![Regenerar chaves de acesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> Pode levar vários minutos antes que uma chave gerada mais recentemente pode ser usado tooaccess sua conta de banco de dados do Azure Cosmos.
> 
> 

## <a name="get-hello--connection-string"></a>Obter cadeia de caracteres de conexão Olá
tooretrieve sua conexão de cadeia de caracteres, Olá a seguir: 

1. Em Olá [portal do Azure](https://portal.azure.com), acessar sua conta do banco de dados do Azure Cosmos.
2. No menu de recursos de saudação, clique em **chaves**.
3. Clique em Olá **cópia** toohello próximo botão **cadeia de caracteres de Conexão primária** ou **cadeia de caracteres de Conexão secundária** caixa. 

Se você estiver usando a cadeia de caracteres de conexão de saudação em Olá [ferramenta de migração de banco de dados de banco de dados do Azure Cosmos](import-data.md), acrescente término toohello do nome de banco de dados Olá de cadeia de caracteres de conexão de saudação. `AccountEndpoint=< >;AccountKey=< >;Database=< >`.

## <a id="delete"></a> Excluir uma conta do Azure Cosmos DB
tooremove um banco de dados do Azure Cosmos Olá Portal do Azure que você já não estiver usando nome da conta com o botão direito hello, de conta e clique em **excluir conta**.

![Como a conta de toodelete um banco de dados do Azure Cosmos no hello Portal do Azure](./media/manage-account/deleteaccount.png)

1. Em Olá [portal do Azure](https://portal.azure.com/), acessar a conta de banco de dados do Azure Cosmos Olá desejar toodelete.
2. Em Olá **conta de banco de dados do Azure Cosmos** folha, clique em conta hello e, em seguida, clique em **excluir conta**. 
3. Na folha de confirmação resultante Olá, digite o nome de conta do hello Azure Cosmos DB tooconfirm que você deseja toodelete Olá conta.
4. Clique em Olá **excluir** botão.

![Como a conta de toodelete um banco de dados do Azure Cosmos no hello Portal do Azure](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>Próximas etapas
Saiba como muito[começar com sua conta do banco de dados do Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
