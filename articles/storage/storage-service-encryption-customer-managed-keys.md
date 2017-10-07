---
title: "aaaAzure criptografia do serviço de armazenamento usando o cliente gerenciado chaves no cofre de chaves do Azure | Microsoft Docs"
description: "Use tooencrypt de recurso de criptografia do serviço de armazenamento do Azure Olá seu armazenamento de BLOBs do Azure no lado do serviço de saudação ao armazenar dados de saudação e descriptografá-lo ao recuperar dados hello usando o cliente gerenciado chaves."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Criptografia do Serviço de Armazenamento usando chaves gerenciadas pelo cliente no Azure Key Vault

O Microsoft Azure é fortemente comprometido toohelping proteger e proteger seu dados toomeet seu compromissos de conformidade e segurança da organização.  Uma maneira de proteger seus dados em repouso é toouse criptografia de serviço de armazenamento (SSE), que automaticamente criptografa os dados quando escrever toostorage e descriptografa os dados quando recuperá-los. Olá criptografia e descriptografia é completamente transparente e automática e usa 256 bits [criptografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), um bloqueio mais forte Olá codificações disponíveis.

Use chaves de criptografia gerenciadas pela Microsoft com a SSE ou suas próprias chaves de criptografia. Este artigo abordaremos Olá último. Para obter mais informações sobre como usar chaves gerenciadas pela Microsoft ou sobre a SSE em geral, consulte [Criptografia do Serviço de Armazenamento para dados em repouso](storage-service-encryption.md).

capacidade de saudação de tooprovide toouse suas próprias chaves de criptografia, SSE para armazenamento de Blob é integrado com o Azure Key Vault (AKV). Você pode criar suas próprias chaves de criptografia e armazená-las em AKV, ou você pode usar as chaves de criptografia de toogenerate APIs do AKV. Não só AKV permitem toomanage e controlar suas chaves, ele também permite que você tooaudit o uso da chave. 

Por que você queira toocreate suas próprias chaves? Oferece mais flexibilidade, incluindo Olá capacidade toocreate, girar, desabilitar e definir os controles de acesso e tooaudit Olá criptografia chaves usadas tooprotect seus dados.

## <a name="sse-with-customer-managed-keys-preview"></a>Versão prévia da SSE com chaves gerenciadas pelo cliente

Esse recurso está atualmente na visualização. toouse esse recurso, você precisa toocreate uma nova conta de armazenamento. Crie um novo cofre de chaves e uma nova chave ou use um cofre de chaves e uma chave existentes. conta de armazenamento Hello e cofre da chave Olá devem estar no hello mesma região, mas eles podem ser em assinaturas diferentes.

entre em contato com tooparticipate na visualização de saudação [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Forneceremos uma tooparticipate link especial na visualização de saudação.

toolearn mais, consulte toohello [perguntas frequentes sobre](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Você deve se inscrever para Olá visualização prévia toofollowing Olá etapas neste artigo. Sem acesso ao preview, você não poderá ser capaz de tooenable esse recurso no portal de saudação.

## <a name="getting-started"></a>Introdução
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Etapa 1: [Criar uma nova conta de armazenamento](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Etapa 2: Habilitar a criptografia
Você pode habilitar SSE Olá conta de armazenamento usando Olá [portal do Azure](https://portal.azure.com). Na folha de configurações Olá Olá conta de armazenamento, procure Olá seção de serviço Blob, conforme mostrado na figura abaixo e clique em criptografia.

![Captura de tela do Portal mostrando a opção Criptografia](./media/storage-service-encryption/image1.png)
<br/>*Habilitar a SSE no Serviço Blob*

Se você desejar tooprogrammatically habilitar ou desabilitar Olá criptografia do serviço de armazenamento em uma conta de armazenamento, você pode usar o hello [API de REST do provedor de recursos de armazenamento do Azure](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), Olá [biblioteca de cliente do provedor de recursos de armazenamento para .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), ou hello [CLI do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

Nessa tela, se você não puder ver hello "usar sua própria chave" caixa de seleção, você não foram aprovados para visualização de saudação. Envie um e-mail muito[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) e solicitar aprovação.

![Captura de tela do portal mostrando a Versão Prévia da Criptografia](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Por padrão, a SSE usará as chaves gerenciadas pela Microsoft. toouse suas próprias chaves, marque a caixa de saudação. Em seguida, você pode especificar sua chave de URI ou selecione uma chave e um cofre de chaves do seletor de saudação de.

## <a name="step-3-select-your-key"></a>Etapa 3: Selecionar a chave

![Captura de tela do portal mostrando a opção Usar sua própria chave da Criptografia](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Captura de tela do portal mostrando a opção Inserir URI da chave da Criptografia](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Se a conta de armazenamento Olá não tem acesso toohello Cofre de chaves, você pode executar o seguinte Olá comando usando contas de armazenamento de toohello do Powershell do Azure toogrant acesso toohello necessário Cofre de chaves.

![Captura de tela do portal mostrando o acesso negado ao cofre de chaves](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Você também pode conceder acesso por meio do portal do Azure de saudação indo toohello Cofre de chaves do Azure no hello portal do Azure e conceder a conta de armazenamento toohello de acesso.

## <a name="step-4-copy-data-toostorage-account"></a>Etapa 4: Copie dados toostorage
Se você quiser dados tootransfer em sua nova conta de armazenamento para que ele é criptografado, consulte muito[etapa 3 do guia de Introdução na criptografia do serviço de armazenamento de dados em repouso](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Etapa 5: Consultar o status de saudação do hello os dados criptografados
status de saudação tooquery de dados criptografado de saudação consulte muito[etapa 4 do guia de Introdução na criptografia do serviço de armazenamento de dados em repouso](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Perguntas frequentes sobre a Criptografia do Serviço de Armazenamento de dados em repouso
**P: Estou usando o armazenamento Premium. Posso usar a SSE com chaves gerenciadas pelo cliente?**

R: Sim, há suporte para a SSE com chaves gerenciadas pela Microsoft e pelo cliente tanto no armazenamento Standard quanto no Premium. 

**P: Posso criar novas contas de armazenamento com a SSE com chaves gerenciadas pelo cliente habilitada usando o Azure PowerShell e a CLI do Azure?**

R: Sim.

**P: Qual é o custo adicional do Armazenamento do Azure se a SSE com chaves gerenciadas pelo cliente é habilitada?**

R: Há um custo associado para o uso do Azure Key Vault. Para obter mais detalhes, visite [Preços do Key Vault](https://azure.microsoft.com/en-us/pricing/details/key-vault/). Não há nenhum custo adicional para o uso da SSE.

**P: pode revogar o acesso chaves de criptografia de toohello?**

R: Sim, você pode revogar o acesso a qualquer momento. Há várias maneiras toorevoke acesso tooyour chaves. Consulte também[do PowerShell do Azure Key Vault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) e [CLI de Cofre de chave do Azure](https://docs.microsoft.com/en-us/cli/azure/keyvault) para obter mais detalhes. Revogar acesso efetivamente bloqueará o acesso tooall blobs na conta de armazenamento hello como Olá chave de criptografia de conta não estiver acessível pelo armazenamento do Azure.

**P: Posso criar uma conta de armazenamento e uma chave em uma região diferente?**

R: não, a conta de armazenamento hello e toobe de necessidade de chaves/chave do cofre no hello mesma região. 

**P: posso habilitar SSE com chaves gerenciada pelo cliente durante a criação de conta de armazenamento Olá?**

R: não. Quando você habilita SSE durante a criação de conta de armazenamento hello, você pode usar somente chaves gerida pela Microsoft. Se você deseja que as chaves do toouse gerenciada pelo cliente, você precisará tooupdate propriedades da conta de armazenamento de saudação. Você pode usar o REST ou uma saudação tooprogrammatically de bibliotecas de cliente de armazenamento atualizar sua conta de armazenamento, ou atualizar propriedades de conta de armazenamento hello usando Olá Portal do Azure depois de criar a conta de saudação.

**P: Posso desabilitar a criptografia durante o uso da SSE com chaves gerenciadas pelo cliente?**

R: Não. Não é possível desabilitar a criptografia durante o uso da SSE com chaves gerenciadas pelo cliente. criptografia toodisable, você precisará tooswitch toousing Microsoft gerenciada chaves. Você pode fazer isso usando Olá portal do Azure ou o PowerShell.

**P: O SSE é habilitado por padrão quando eu crio uma nova conta de armazenamento?**

R: SSE não está habilitado por padrão. Você pode usar o hello tooenable portal do Azure-lo. Também por meio de programação, você pode habilitar esse recurso usando Olá API de REST do provedor de recursos de armazenamento. 

**P: Não consigo habilitar a criptografia em minha conta de armazenamento.**

R: A conta é uma conta de armazenamento do Resource Manager? Não há suporte para contas de armazenamento clássicas. A SSE com chaves gerenciadas pelo cliente também pode ser habilitada apenas em contas de armazenamento do Resource Manager recém-criadas.

**P: A SSE com chaves gerenciadas pelo cliente é permitida somente em regiões específicas?**

R: A SSE está disponível apenas em determinadas regiões para o Armazenamento de blobs nesta versão prévia. Envie um email [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck para disponibilidade e detalhes sobre a visualização. 

**P: como contatar alguém se eu tiver problemas ou quiser tooprovide comentários?**

R: entre em contato com [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) para qualquer problema relacionado a tooStorage criptografia do serviço. 

## <a name="next-steps"></a>Próximas etapas

*   Para obter mais informações sobre o conjunto abrangente de saudação de segurança de recursos que ajudam os desenvolvedores a criar aplicativos seguros, consulte Olá [guia de segurança do armazenamento](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Para obter informações gerais sobre o Azure Key Vault, consulte [O que é o Azure Key Vault?](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)
*   Para começar a usar o Azure Key Vault, consulte [Introdução ao Azure Key Vault](../key-vault/key-vault-get-started.md).
