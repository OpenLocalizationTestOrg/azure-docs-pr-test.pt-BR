---
title: "aaaEncryption no repositório Azure Data Lake | Microsoft Docs"
description: "Entenda como a rotação de chaves e criptografia funciona no Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Criptografia de dados no Azure Data Lake Store

A criptografia no Azure Data Lake Store ajuda a proteger seus dados, implementar políticas de segurança da empresa e atender aos requisitos de conformidade normativa. Este artigo fornece uma visão geral do design de saudação e descreve alguns aspectos técnicos de saudação da implementação.

O Data Lake Store dá suporte à criptografia de dados em repouso e em trânsito. Para dados em repouso, o Data Lake Store oferece suporte à criptografia “ativada por padrão”, transparente. Aqui está o que esses termos significam um pouco mais detalhadamente:

* **Em por padrão**: quando você cria uma nova conta do repositório Data Lake, a configuração padrão de saudação habilita a criptografia. Depois disso, dados armazenados no repositório Data Lake são sempre criptografado toostoring anterior na mídia persistente. Este é o comportamento de Olá para todos os dados e não pode ser alterado depois que uma conta é criada.
* **Transparente**: repositório Data Lake automaticamente criptografa toopersisting anteriores de dados e descriptografa tooretrieval anteriores de dados. criptografia de saudação é configurada e gerenciada no nível do repositório Data Lake do hello por um administrador. Nenhuma alteração é feita toohello dados acessar APIs. Portanto, nenhuma alteração é necessária nos aplicativos e serviços que interagem com o Data Lake Store devido à criptografia.

Dados em trânsito (também conhecidos como dados em movimento) também são sempre criptografados no Data Lake Store. Além disso mídia toopersistent do tooencrypting dados toostoring anterior, Olá dados são sempre protegidos em trânsito usando HTTPS. HTTPS é Olá único protocolo com suporte para Olá que interfaces Data Lake repositório REST. Olá diagrama a seguir mostra como os dados serão criptografados no repositório Data Lake:

![Diagrama de criptografia de dados no Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Configurar a criptografia com o Data Lake Store

A criptografia para o Data Lake Store é configurada durante a criação da conta, ela está sempre habilitada por padrão. Você pode gerenciar chaves de saudação por conta própria, ou permitir que o repositório Data Lake toomanage por você (esse é o padrão de saudação).

Para saber mais, consulte o [Guia de Introdução](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Como funciona a criptografia no Data Lake Store

Olá informações a seguir abordam como chaves de criptografia mestra toomanage e explica Olá três tipos diferentes de chaves que você pode usar na criptografia de dados para o repositório Data Lake.

### <a name="master-encryption-keys"></a>Chaves de criptografia mestras

O Data Lake Store oferece dois modos de gerenciamento de chaves de criptografia mestras (MEKs). Por enquanto, suponha que essa chave de criptografia mestra Olá é a chave de nível superior de saudação. Chave de criptografia mestra toohello acesso é necessário toodecrypt todos os dados armazenados no repositório Data Lake.

modos de saudação duas para o gerenciamento de chave de criptografia mestra Olá são da seguinte maneira:

*   Chaves gerenciadas de serviço
*   Chaves gerenciadas do cliente

Em ambos os modos, a chave de criptografia mestra Olá é protegida por fazê-lo no cofre de chaves do Azure. Cofre de chaves é um serviço altamente seguro totalmente gerenciado no Azure que pode ser usado toosafeguard as chaves de criptografia. Para obter mais informações, consulte [Key Vault](https://azure.microsoft.com/services/key-vault).

Aqui está uma breve comparação dos recursos fornecidos por dois modos de saudação do gerenciamento Olá MEKs.

|  | Chaves gerenciadas de serviço | Chaves gerenciadas do cliente |
| --- | --- | --- |
|Como os dados são armazenados?|Sempre criptografado toobeing anterior armazenado.|Sempre criptografado toobeing anterior armazenado.|
|Olá mestre de chave de criptografia de armazenamento?|Cofre de Chaves|Cofre de Chaves|
|Tem qualquer criptografia de chaves armazenadas no hello limpar fora do Cofre de chaves? |Não|Não|
|Olá MEK pode ser recuperada pelo Cofre de chaves?|Não. Depois de Olá que MEK é armazenada no cofre de chaves, ele só pode ser usado para criptografia e descriptografia.|Não. Depois de Olá que MEK é armazenada no cofre de chaves, ele só pode ser usado para criptografia e descriptografia.|
|Quem possui a instância do Cofre de chaves hello e hello MEK?|saudação de serviço de repositório Data Lake|Você possui a instância de Cofre de chaves hello, que pertence a sua própria assinatura do Azure. Olá MEK no cofre de chaves pode ser gerenciado pelo software ou hardware.|
|Você pode revogar o acesso toohello MEK para Olá serviço de repositório Data Lake?|Não|Sim. Você pode gerenciar listas de controle de acesso no cofre de chaves e remover a identidade de serviço acesso controle entradas toohello para Olá serviço de repositório Data Lake.|
|Você pode excluir permanentemente Olá MEK?|Não|Sim. Se você excluir Olá MEK do Cofre de chaves, dados Olá Olá conta do repositório Data Lake não podem ser descriptografados por qualquer pessoa, incluindo o serviço de repositório Data Lake hello. <br><br> Se você tiver explicitamente feito Olá MEK anterior toodeleting-lo do Cofre de chaves, Olá MEK pode ser restaurado e Olá dados, em seguida, podem ser recuperados. No entanto, se você não fez backup Olá MEK anterior toodeleting-lo de Cofre de chaves, Olá dados na conta do repositório Data Lake do hello podem nunca ser descriptografados posteriormente.|


Além dessa diferença de que gerencia Olá MEK e instância de Cofre de chaves de saudação no qual ele reside, restante de saudação do design de saudação é hello mesmo para ambos os modos.

É a seguir Olá tooremember importante quando você escolher modo de saudação do hello chaves de criptografia mestra:

*   Você pode escolher se toouse gerenciados pelo cliente chaves ou as chaves de serviço gerenciado ao provisionar uma conta do repositório Data Lake.
*   Depois que uma conta do repositório Data Lake for fornecida, o modo de saudação não pode ser alterado.

### <a name="encryption-and-decryption-of-data"></a>Criptografia e descriptografia de dados

Há três tipos de chaves que são usadas no design de saudação de criptografia de dados. Olá, a tabela a seguir fornece um resumo:

| Chave                   | Abreviação | Associado a | Local de armazenamento                             | Tipo       | Observações                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Chave de criptografia mestra | MEK          | Uma conta Data Lake Store | Cofre da Chave                              | Assimétrica | Pode ser gerenciado pelo Data Lake Store ou por você.                                                              |
| Chave de criptografia de dados   | DEK          | Uma conta Data Lake Store | Armazenamento persistente, gerenciado pelo serviço do Data Lake Store | Simétrica  | Olá DEK Olá MEK é criptografada. Olá que DEK criptografada é o que é armazenado na mídia persistente. |
| Chave de criptografia de bloco  | BEK          | Um bloco de dados | Nenhum                                         | Simétrica  | Olá BEK é derivado do hello DEK e bloco de dados de saudação.                                                      |

Olá diagrama a seguir ilustra esses conceitos:

![Chaves na criptografia de dados](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Algoritmo de pseudo quando um arquivo é toobe descriptografado:
1.  Verifique se o hello DEK para a conta do repositório Data Lake Olá é armazenado em cache e pronta para uso.
    - Caso contrário, ler Olá criptografado DEK do armazenamento persistente e enviá-lo tooKey cofre toobe descriptografada. Saudação de cache descriptografada DEK na memória. Agora é toouse pronto.
2.  Para cada bloco de dados no arquivo hello:
    - Bloco criptografado de saudação de leitura de dados de armazenamento persistente.
    - Gere hello BEK de saudação DEK e bloco criptografado de saudação de dados.
    - Use Olá BEK toodecrypt dados.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Algoritmo de pseudo quando um bloco de dados é toobe criptografado:
1.  Verifique se o hello DEK para a conta do repositório Data Lake Olá é armazenado em cache e pronta para uso.
    - Caso contrário, ler Olá criptografado DEK do armazenamento persistente e enviá-lo tooKey cofre toobe descriptografada. Saudação de cache descriptografada DEK na memória. Agora é toouse pronto.
2.  Gere um BEK exclusivo para o bloco de saudação de dados de saudação DEK.
3.  Criptografe o bloco de dados Olá com hello BEK, usando a criptografia AES-256.
4.  Bloco de dados criptografados Olá de repositório de dados no armazenamento persistente.

> [!NOTE] 
> Por motivos de desempenho, Olá DEK em Olá limpar é armazenado em cache na memória por um curto período e imediatamente é apagada posteriormente. Na mídia persistente, sempre é armazenada criptografada por Olá MEK.

## <a name="key-rotation"></a>Alteração de chaves

Quando você estiver usando chaves gerenciados pelo cliente, você pode girar Olá MEK. toolearn como tooset uma conta do repositório Data Lake com chaves gerenciados pelo cliente, consulte [Introdução](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Pré-requisitos

Quando você configura Olá conta do repositório Data Lake, você escolheu toouse suas próprias chaves. Essa opção não pode ser alterada depois Olá conta foi criada. Olá etapas a seguir pressupõem que você está usando chaves gerenciados pelo cliente (ou seja, você escolheu suas próprias chaves do Cofre de chaves).

Observe que, se você usar opções de padrão de saudação para criptografia, seus dados sempre são criptografados usando chaves gerenciadas pelo repositório Data Lake. Essa opção, você não tem chaves de toorotate de capacidade de hello, como eles são gerenciados pelo repositório Data Lake.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Como toorotate Olá MEK no repositório Data Lake

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Procure toohello instância de Cofre de chaves que armazena suas chaves associadas à sua conta do repositório Data Lake. Selecione **Chaves**.

    ![Captura de tela do Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Selecione Olá chave associada à sua conta do repositório Data Lake e criar uma nova versão dessa chave. Observe que repositório Data Lake atualmente suporta apenas a rotação de chaves tooa nova versão de uma chave. Ele não oferece suporte a rotação chave tooa.

   ![Captura de tela da janela de Chaves, com a Nova versão realçada](./media/data-lake-store-encryption/keynewversion.png)

4.  Procure a conta de armazenamento do repositório Data Lake toohello e selecione **criptografia**.

    ![Captura de tela da janela da conta de armazenamento do Data Lake Store, com Criptografia realçada](./media/data-lake-store-encryption/select-encryption.png)

5.  Uma mensagem informa que uma nova versão de chave da chave hello está disponível. Clique em **rotação da chave** nova versão do tooupdate Olá toohello chave.

    ![Captura de tela da janela do Data Lake Store com a mensagem e Alterar realçados](./media/data-lake-store-encryption/rotatekey.png)

Esta operação deve levar menos de dois minutos, e não há nenhum tempo de inatividade esperado devido tookey rotação. Após a conclusão da operação de hello, Olá nova versão da chave hello está em uso.
