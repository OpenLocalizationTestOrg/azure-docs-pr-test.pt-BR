---
title: "aaaAzure criptografia do serviço de armazenamento de dados em repouso | Microsoft Docs"
description: "Use tooencrypt de recurso de criptografia do serviço de armazenamento do Azure Olá seu armazenamento de BLOBs do Azure no lado do serviço de saudação ao armazenar dados de saudação e descriptografá-lo ao recuperar dados de saudação."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Criptografia do Serviço de Armazenamento do Azure para dados em repouso
Azure Storage Service criptografia (SSE) para dados em repouso ajuda você a proteger e proteger seu dados toomeet seu compromissos de conformidade e segurança da organização. Com esse recurso, o armazenamento do Azure automaticamente criptografa seu toostorage toopersisting anteriores de dados e descriptografa tooretrieval anterior. Olá criptografia, descriptografia e gerenciamento de chaves são toousers totalmente transparente.

Olá seções a seguir fornecem orientação detalhada sobre como recursos de criptografia do serviço de armazenamento de saudação toouse bem como Olá suporte para cenários e as experiências do usuário.

## <a name="overview"></a>Visão geral
Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança que juntos permitem que os desenvolvedores de aplicativos seguros toobuild. Os dados podem ser protegidos em trânsito, entre um aplicativo e o Azure, usando a [Criptografia do lado do cliente](storage-client-side-encryption.md), HTTPs ou SMB 3.0. A Criptografia do Serviço de Armazenamento fornece criptografia em repouso, lidando com a criptografia, a descriptografia e o gerenciamento de chaves de forma totalmente transparente. Todos os dados são criptografados usando 256 bits [criptografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), um bloqueio mais forte Olá codificações disponíveis.

SSE funciona por meio da criptografia de dados de saudação quando ele é gravado tooAzure armazenamento e pode ser usado para o armazenamento de arquivo e armazenamento de BLOBs do Azure. Ele funciona para os seguintes hello:

* Armazenamento Standard: contas de armazenamento de uso geral para o armazenamento de Blobs e Arquivos e contas de armazenamento de Blobs
* Armazenamento Premium 
* Todos os níveis de redundância (LRS, ZRS, GRS e RA-GRS)
* Contas de armazenamento do Azure Resource Manager (mas não clássico) 
* Todas as regiões.

toolearn mais, consulte Perguntas frequentes sobre o toohello.

tooenable ou desabilitar a criptografia do serviço de armazenamento para uma conta de armazenamento, faça logon no hello [portal do Azure](https://portal.azure.com) e selecione uma conta de armazenamento. Na folha de configurações hello, procure Olá seção do serviço Blob, conforme mostrado nesta captura de tela e clique em criptografia.

![Captura de tela do Portal mostrando a opção Criptografia](./media/storage-service-encryption/image1.png)
<br/>*Figura 1: habilitar a SSE para serviço Blob (etapa 1)*

![Captura de tela do Portal mostrando a opção Criptografia](./media/storage-service-encryption/image3.png)
<br/>*Figura 2: habilitar a SSE para serviço de arquivo (etapa 1)*

Depois de clicar em configuração de criptografia hello, você pode habilitar ou desabilitar a criptografia do serviço de armazenamento.

![Captura de tela do Portal mostrando as propriedades da criptografia](./media/storage-service-encryption/image2.png)
<br/>*Figura 3: Habilitar a SSE para o Serviço Blob e Arquivo (etapa 2)*

## <a name="encryption-scenarios"></a>Cenários de criptografia
A Criptografia do Serviço de Armazenamento pode ser habilitada no nível da conta de armazenamento. Uma vez habilitada, os clientes escolherão tooencrypt quais serviços. Ele dá suporte a saudação os seguintes cenários de cliente:

* Criptografia do Armazenamento de Blobs e do Armazenamento de Arquivos em contas do Resource Manager.
* Criptografia de Blob e o serviço de arquivos em contas de armazenamento clássicas uma vez migrados contas de armazenamento do Gerenciador de tooResource.

SSE tem Olá seguintes limitações:

* Não há suporte para a criptografia de contas de armazenamento clássicas.
* Os dados existentes - SSE somente criptografa os dados recém-criado depois Olá a criptografia está habilitada. Se, por exemplo você cria uma nova conta de armazenamento do Gerenciador de recursos, mas não ativa a criptografia e, em seguida, você carregar blobs ou conta de armazenamento de toothat VHDs arquivada e, em seguida, ativa SSE, os blobs não serão criptografados, a menos que eles sejam reconfigurados ou copiados.
* Suporte de mercado - habilitar criptografia de máquinas virtuais criada a partir Olá Marketplace usando Olá [portal do Azure](https://portal.azure.com), PowerShell e a CLI do Azure. imagem base do VHD Olá permanecerá não criptografada; No entanto, gravações feitas depois Olá VM girado backup serão criptografadas.
* Dados de filas e tabelas não serão criptografados.

## <a name="getting-started"></a>Introdução
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Etapa 1: [Criar uma nova conta de armazenamento](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Etapa 2: Habilitar a criptografia.
Você pode habilitar a criptografia usando Olá [portal do Azure](https://portal.azure.com).

> [!NOTE]
> Se você desejar tooprogrammatically habilitar ou desabilitar Olá criptografia do serviço de armazenamento em uma conta de armazenamento, você pode usar o hello [API de REST do provedor de recursos de armazenamento do Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx), Olá [biblioteca de cliente do provedor de recursos de armazenamento para .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), ou hello [CLI do Azure](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Etapa 3: Copie dados toostorage
Se você habilitar SSE para Olá serviço Blob, todos os blobs gravados toothat conta de armazenamento serão criptografados. Blobs que já estiverem na conta de armazenamento não serão criptografados até que sejam gravados novamente. Você pode copiar dados saudação do armazenamento de uma conta tooone com SSE criptografado, ou até mesmo habilitar SSE e copiar blobs de saudação de um contêiner tooanother toosure que os dados anteriores serão criptografados. Você pode usar qualquer Olá tooaccomplish ferramentas a seguir para isso. Isso também é Olá mesmo comportamento para armazenamento de arquivos.

#### <a name="using-azcopy"></a>Como usar o AzCopy
AzCopy é um utilitário de linha de comando do Windows criado para copiar dados tooand do armazenamento de BLOBs do Microsoft Azure, o arquivo e a tabela usando comandos simples com um desempenho ideal. Você pode usar este toocopy seus blobs ou arquivos de um tooanother de conta de armazenamento tem SSE habilitado. 

toolearn mais, visite [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

#### <a name="using-smb"></a>Como usar o SMB
Armazenamento de arquivo do Azure oferece compartilhamentos de arquivos na nuvem hello usando o protocolo SMB padrão de saudação. Você pode montar um compartilhamento de arquivo de um cliente no local ou no Azure. Quando montado, ferramentas, como o Robocopy podem ser usados toocopy arquivos over tooAzure que compartilhamentos de arquivos. Para obter mais informações, consulte [como toomount Azure compartilhamento de arquivos no Windows](storage-file-how-to-use-files-windows.md) e [como toomount arquivo Azure compartilhar no Linux](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>Usando bibliotecas de cliente de armazenamento Olá
Você pode copiar o blob ou arquivo tooand de dados do armazenamento de blob ou entre contas de armazenamento usando nosso conjunto completo de bibliotecas de cliente de armazenamento, incluindo .NET, C++, Java, Android, Node.js, PHP, Python e Ruby.

toolearn mais, visite nosso [Introdução ao armazenamento de BLOBs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Como usar o Gerenciador de Armazenamento
Você pode usar contas de armazenamento de armazenamento explorer toocreate, carregar e baixar os dados, exibir o conteúdo dos blobs e navegar pelos diretórios. Você pode usar uma dessas contas de armazenamento tooyour tooupload blobs com criptografia ativada. Com alguns gerenciadores de armazenamento, você também pode copiar dados de blob tooa outro contêiner de armazenamento existente na conta de armazenamento hello ou uma nova conta de armazenamento que tem SSE habilitado.

toolearn mais, visite [gerenciadores de armazenamento do Azure](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Etapa 4: Consultar o status de saudação do hello os dados criptografados
Uma versão atualizada de bibliotecas de saudação do cliente de armazenamento foi implantada e permite que você tooquery estado de saudação do toodetermine objeto se ele está criptografado ou não. Disponível apenas para armazenamento de blobs. Suporte para armazenamento de arquivos é no roteiro hello. 

Olá enquanto isso, você pode chamar [obter propriedades de conta](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify que Olá conta de armazenamento tem criptografia habilitada ou Olá propriedades de conta de armazenamento no portal do Azure de saudação do modo de exibição.

## <a name="encryption-and-decryption-workflow"></a>Fluxo de trabalho da criptografia e da descriptografia
Aqui está uma breve descrição do fluxo de trabalho de criptografia/descriptografia hello:

* Prezado cliente habilita a criptografia na conta de armazenamento hello.
* Quando o cliente Olá grava novos tooBlob de dados (Blob PUT, coloque o bloco, PUT Page, colocar arquivos etc.) ou o armazenamento de arquivos; todas as gravações são criptografadas por meio de 256 bits [criptografia AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), um bloqueio mais forte Olá codificações disponíveis.
* Quando o cliente Olá precisa de dados de tooaccess (obter Blob, etc.), os dados são automaticamente descriptografados antes de retornar o usuário toohello.
* Se a criptografia está desabilitada, novas gravações não são criptografadas e dados criptografados existentes permanecem criptografados até que recriado pelo usuário hello. Embora a criptografia estiver habilitada, grava tooBlob ou armazenamento de arquivos será criptografado. estado Olá dos dados não é alterada com usuário Olá alternando entre a habilitação e desabilitação de criptografia para a conta de armazenamento hello.
* Todas as chaves de criptografia são armazenadas, criptografadas e gerenciadas pela Microsoft.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Perguntas frequentes sobre a Criptografia do Serviço de Armazenamento de dados em repouso
**P: Tenho uma conta de armazenamento clássica. Posso habilitar o SSE nela?**

R: Não, apenas contas de armazenamento do Resource Manager dão suporte à SSE.

**P: Como posso criptografar os dados em minha conta de armazenamento clássica?**

R: você pode criar uma nova conta de armazenamento do Gerenciador de recursos e copie seus dados usando [AzCopy](storage-use-azcopy.md) de sua conta de armazenamento clássicos existentes tooyour recentemente criado a conta de armazenamento do Gerenciador de recursos. 

Se você migrar sua conta de armazenamento clássicas tooa conta de armazenamento do Gerenciador de recursos, esta operação é instantânea, ele altera o tipo de saudação da sua conta, mas não afeta os dados existentes. Todos os novos dados gravados serão criptografados somente depois que a criptografia for habilitada. Para obter mais informações, consulte [plataforma com suporte de IaaS recursos de migração de clássico tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Observe que há suporte para isso apenas nos serviços Blob e Arquivo.

**P: posso ter uma conta de armazenamento do Resource Manager existente. Posso habilitar o SSE nela?**

R: Sim, mas apenas dados gravados recentemente serão criptografados. Ela não criptografa dados que já existiam anteriormente. Isso ainda não é suportado para Olá visualização do armazenamento de arquivo.

**P: eu gostaria que os dados atuais do hello tooencrypt em uma conta de armazenamento do Gerenciador de recursos existente?**

R: Você pode habilitar a SSE a qualquer momento em uma conta de armazenamento do Resource Manager. No entanto, dados que já existiam não serão criptografados. tooencrypt os dados existentes, você pode copiá-los tooanother nome ou outro contêiner e, em seguida, remover versões Olá sem criptografia.

**P: Estou usando o armazenamento Premium. Posso usar o SSE?**

R: Sim, o SSE recebe suporte no Armazenamento Standard e no Armazenamento Premium.  Armazenamento Premium não há suporte para Olá serviço de arquivo.

**P: Se eu criar uma nova conta de armazenamento, habilitar o SSE e depois criar uma nova VM usando a conta de armazenamento, isso significa que minha VM está criptografada?**

R: Sim. Todos os discos criados que usam a nova conta de armazenamento hello serão criptografados, desde que eles são criados depois SSE está habilitado. Se Olá que VM foi criada usando o Azure Marketplace, imagem base do VHD Olá permanecerá não criptografada; No entanto, gravações feitas depois Olá VM girado backup serão criptografadas.

**P: Posso criar novas contas de armazenamento com o SSE habilitado usando o Azure PowerShell e a CLI do Azure?**

R: Sim.

**P: Há algum custo adicional no Armazenamento do Azure se o SSE estiver habilitado?**

R: Não há qualquer custo adicional.

**P: que gerencia chaves de criptografia Olá?**

R: Olá chaves são gerenciadas pela Microsoft.

**P: Posso usar minhas próprias chaves de criptografia?**

R: estamos trabalhando em fornecer recursos para os clientes toobring suas próprias chaves de criptografia.

**P: pode revogar o acesso chaves de criptografia de toohello?**

R: não no momento; chaves de saudação são totalmente gerenciadas pela Microsoft.

**P: O SSE é habilitado por padrão quando eu crio uma nova conta de armazenamento?**

R: SSE não está habilitado por padrão. Você pode usar o hello tooenable portal do Azure-lo. Também por meio de programação, você pode habilitar esse recurso usando Olá API de REST do provedor de recursos de armazenamento.

**P: Qual é a diferença para o Azure Disk Encryption?**

R: esse recurso é usado tooencrypt dados no armazenamento de BLOBs do Azure. Olá criptografia de disco do Azure é usado tooencrypt SO e discos de dados em VMs de IaaS. Para obter mais detalhes, visite nosso [Guia de segurança do armazenamento](storage-security-guide.md).

**P: E se eu habilitar SSE e, em seguida, entrar e habilitar a criptografia de disco do Azure em discos Olá?**

R: Isso funcionará perfeitamente. Os dados serão criptografados pelos dois métodos.

**P: minha conta de armazenamento é configurada toobe replicado geograficamente redundante. Se eu habilitar o SSE, minha cópia redundante também será criptografada?**

R: Sim, todas as cópias da conta de armazenamento Olá são criptografadas e todas as opções de redundância – armazenamento localmente redundante (LRS), armazenamento redundante de zona (ZRS), armazenamento com redundância geográfica (GRS) e armazenamento com redundância geográfica de acesso de leitura (RA-GRS) – têm suporte.

**P: Não consigo habilitar a criptografia em minha conta de armazenamento.**

R: A conta é uma conta de armazenamento do Resource Manager? Não há suporte para contas de armazenamento clássicas. 

**P: A SSE é permitida somente em regiões específicas?**

R: Olá SSE está disponível em todas as regiões para armazenamento de Blob. Verifique se o hello seção de disponibilidade para o armazenamento de arquivos. 

**P: como contatar alguém se eu tiver problemas ou quiser tooprovide comentários?**

R: entre em contato com [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) para qualquer problema relacionado a tooStorage criptografia do serviço.

## <a name="next-steps"></a>Próximas etapas
Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança que juntos permitem que os desenvolvedores de aplicativos seguros toobuild. Para obter mais detalhes, visite Olá [guia de segurança do armazenamento](storage-security-guide.md).

