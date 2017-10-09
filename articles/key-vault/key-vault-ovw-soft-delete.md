---
ms.assetid: 
title: "exclusão reversível do Cofre de chaves aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Visão geral de exclusão reversível do Azure Key Vault

Recurso de exclusão reversível do cofre da chave permite a recuperação de cofres Olá excluído e objetos de cofre, conhecidos como exclusão reversível. Especificamente, podemos endereço Olá os seguintes cenários:

- Suporte à exclusão reversível de cofres de chaves
- Suporte à exclusão recuperável de objetos do cofre de chaves (por exemplo, chaves, segredos, certificados)

## <a name="supporting-interfaces"></a>Interfaces de suporte

Olá recurso soft excluir está inicialmente disponível por meio Olá REST, .NET / interfaces do c# e do PowerShell. Para obter mais detalhes, consulte referências toohello [referência de chave de cofre](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Cenários

Os Azure Key Vaults são recursos controlados, gerenciados pelo Azure Resource Manager. O Azure Resource Manager também especifica um comportamento bem definido para a exclusão, que exige que uma operação DELETE bem-sucedida faça com que esse recurso não esteja mais acessível. endereços de recurso de exclusão reversível Olá Olá recuperação do objeto Olá excluído, se a exclusão de saudação foi acidental ou intencional.

1. No cenário típico de saudação, um usuário pode ter inadvertidamente excluído um cofre de chaves ou um objeto de Cofre de chaves. Se esse Cofre de chaves ou uma chave de cofre objeto foram toobe recuperáveis por um período predeterminado, o usuário de saudação pode desfazer a exclusão de saudação e recuperar seus dados.

2. Em um cenário diferente, um usuário mal-intencionado pode tentar toodelete um cofre de chaves ou um objeto de Cofre de chaves, como uma chave dentro de um cofre, toocause uma interrupção dos negócios. Separar a exclusão de saudação do Cofre de chaves hello ou objeto de Cofre de chaves de exclusão real de saudação do hello dados subjacentes pode ser usado como uma medida de segurança, por exemplo, restringindo as permissões de tooa de exclusão de dados diferente, confiável de função. Essa abordagem efetivamente exige quorum para uma operação que, de outro modo, poderá resultar em uma perda de dados imediata.

### <a name="soft-delete-behavior"></a>Comportamento de exclusão reversível

Com esse recurso, Olá a operação de exclusão em um cofre de chaves ou objeto de Cofre de chaves é um software-delete, mantendo efetivamente recursos Olá por um período de retenção especificado, enquanto dando a aparência de saudação objeto Olá é excluído. serviço de saudação ainda mais fornece um mecanismo para recuperar o objeto Olá excluído, essencialmente, desfazendo exclusão hello. 

A exclusão reversível é um comportamento opcional do Key Vault e **não está habilitado por padrão** nesta versão. Para obter detalhes sobre como habilitar a exclusão reversível para seu Cofre de chaves, consulte Olá orientação específica sobre referência de saudação para interface de saudação de sua escolha, [referência de chave de cofre](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Recuperação do cofre de chaves

Após excluir um cofre de chaves, serviço Olá cria um recurso de proxy na assinatura hello, adicionar metadados suficientes para recuperação. recursos de proxy de saudação é um objeto armazenado, disponível no hello mesmo local que o Cofre de chaves Olá excluído. 

### <a name="key-vault-object-recovery"></a>Recuperação de objetos do cofre de chaves

Após a exclusão de um objeto de Cofre de chaves, como uma chave, serviço Olá colocará objeto Olá em estado excluído, tornando as operações de recuperação de tooany inacessível. Nesse estado, objeto de chave de cofre Olá só pode ser listado, recuperado, ou forçar/será excluída permanentemente. 

Em Olá mesmo tempo, chave de cofre agendará exclusão de saudação do hello subjacente toohello correspondente de dados excluído Cofre de chaves ou objeto de Cofre de chaves para execução após um intervalo de retenção predeterminado. Olá DNS registro toohello cofre correspondente também é mantido por duração de saudação do intervalo de retenção de saudação.

### <a name="soft-delete-retention-period"></a>Período de retenção da exclusão reversível

Os recursos excluídos de maneira reversível são mantidos por um período definido de tempo, 90 dias. Durante o intervalo de retenção de exclusão reversível hello, Olá seguinte se aplica:

- Você pode listar todos os cofres chave hello e objetos de Cofre de chaves em estado de exclusão reversível Olá para sua assinatura bem como informações de exclusão e recuperação de acesso sobre eles.
    - Somente usuários com permissões especiais podem listar os cofres excluídos. Recomendamos que nossos usuários criem uma função personalizada com essas permissões especiais para a manipulação dos cofres excluídos.
- Um cofre de chaves com hello mesmo nome não pode ser criado em Olá mesmo local. de forma correspondente, um objeto de Cofre de chaves não pode ser criado um determinado cofre se o Cofre de chaves que contém um objeto com hello mesmo nome e que está no estado excluído 
- Apenas um usuário privilegiado especificamente pode restaurar um cofre de chaves ou o objeto de Cofre de chaves ao emitir um comando de recuperação no recurso de proxy Olá correspondente.
    - usuário Hello, membro de função personalizada de Olá, com Olá privilégio toocreate um cofre de chaves em um grupo de recursos de saudação pode restaurar cofre hello.
- Somente um usuário com privilégios especificamente à força pode excluir um cofre de chaves ou o objeto de Cofre de chaves ao emitir um comando delete no recurso de proxy Olá correspondente.

A menos que um cofre de chaves ou o objeto de Cofre de chaves é recuperado, a saudação final do serviço de saudação do intervalo de retenção de saudação executa uma limpeza do Cofre de chaves Olá excluídos por software ou objeto de Cofre de chaves e seu conteúdo. A exclusão de recursos não pode ser reagendada.

### <a name="permitted-purge"></a>Limpeza permitida

Permanentemente excluindo, limpeza, um cofre de chaves é possível por meio de uma operação POST no recurso de proxy hello e requer privilégios especiais. Em geral, proprietário da assinatura Olá só será capaz de toopurge um cofre de chaves. gatilhos de operação POST Olá Olá exclusão imediata e irrecuperável de que os. 

Toothis uma exceção é o caso de Olá Olá assinatura do Azure foi marcada como *não excluível*. Nesse caso, apenas o serviço de saudação pode executar exclusão real hello e faz isso como um processo agendado. 



