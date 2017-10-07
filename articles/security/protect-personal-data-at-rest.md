---
title: aaaAzure proteger os dados pessoais em repouso com criptografia | Microsoft Docs
description: "Este artigo faz parte de uma série de ajudá-lo a usar dados pessoais tooprotect do Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a>Tecnologias de criptografia do Azure: proteger dados pessoais em repouso com criptografia

Este artigo ajuda você a entender e usar dados de toosecure de tecnologias de criptografia do Azure em repouso.

Criptografia de dados em repouso é essencial como um melhor prática tooprotect dados confidenciais ou pessoais e toomeet conformidade e requisitos de privacidade de dados.
Criptografia em repouso é projetado tooprevent invasor de saudação acessem dados descriptografado de saudação assegurando Olá dados são criptografados quando no disco.

## <a name="scenario"></a>Cenário 

Uma empresa cruzeiro grandes, com sede em Olá Estados Unidos, está expandindo suas roteiros de toooffer operações Olá Mediterrâneo e mares báltico, bem como Olá Britânicas. toosupport os esforços adquiriu várias linhas de cruzeiro menores com base na Itália, Alemanha, Dinamarca e Olá Reino Unido

empresa de saudação usa dados corporativos do Microsoft Azure toostore na nuvem hello. Isso pode incluir funcionário e/ou informações do cliente, como:

- endereços
- números de telefone
- números de identificação fiscal
- informações de médicas
- informações de cartão de crédito

empresa Olá deve proteger a privacidade de Olá do funcionário e dados do cliente ao fazer departamentos toothose acessível de dados que precisam dela. (como departamentos de folha de pagamento e reservas)

linha de cruzeiro Olá também mantém um banco de dados grande de membros do programa de recompensa e fidelidade que incluem informações pessoais tootrack relações com os clientes atuais e anteriores.

### <a name="problem-statement"></a>Problema declarado

empresa Olá deve proteger a privacidade de saudação dos dados pessoais dos funcionários e clientes ao fazer departamentos toothose acessível de dados que precisam dela (por exemplo, os departamentos de folha de pagamento e reservas). Esses dados pessoais são armazenados fora do Centro de dados corporativos controlados hello e não está sob controle físico da empresa hello.

### <a name="company-goal"></a>Meta da empresa

Como parte de uma estratégia de segurança em várias camadas de defesa em profundidade, é um tooensure de meta da empresa que todas as fontes de dados que contêm dados pessoais são criptografadas, incluindo aqueles que residem no armazenamento em nuvem. Se não estiver autorizado pessoas ganho acessar toohello os dados pessoais, deve ser em um formulário que será renderizado ilegível. A aplicação da criptografia deve ser fácil ou transparente – para os usuários e administradores.

## <a name="solutions"></a>Soluções

Os serviços do Azure fornecem vários toohelp ferramentas e tecnologias de proteger dados pessoais em repouso criptografando-os.

### <a name="azure-key-vault"></a>Cofre da Chave do Azure

[Cofre de chaves do Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) fornece armazenamento seguro para as chaves de saudação usadas tooencrypt dados em repouso em serviços do Azure e Olá recomenda solução de armazenamento e gerenciamento de chave. Gerenciamento de chaves de criptografia é essencial toosecuring armazenado dados.

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a>Como usar as chaves de tooprotect do Cofre de chaves do Azure que criptografam dados pessoais?

toouse Cofre de chaves do Azure, você precisa de uma assinatura tooan conta do Azure. Você também precisa do Azure PowerShell instalado. As etapas incluem o uso de cmdlets do PowerShell, a seguir Olá toodo:

1. Conecte-se tooyour assinaturas

2. Criar um cofre de chave

3. Adicionar uma chave ou segredo toohello Cofre de chaves

4. Registrar aplicativos que irá usar o Cofre de chaves Olá com Active Directory do Azure

5. Autorizar Olá aplicativos toouse Olá chave ou segredo

toocreate um cofre de chaves, use Olá cmdlet do PowerShell New-AzureRmKeyVault. Você atribuirá um nome de cofre, um nome do grupo de recursos e a localização geográfica. Você usará o nome do cofre hello quando o gerenciamento de chaves por meio de outros Cmdlets. Aplicativos que usam o cofre Olá por meio da API REST de saudação usará o Cofre de saudação URI.

O Azure Key Vault pode fornecer uma chave protegida por software para você ou você pode importar uma chave existente em um arquivo .PFX. Você também pode armazenar segredos (senhas) no cofre hello.

Você também pode gerar uma chave no seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello.

Para obter instruções detalhadas sobre como usar o Cofre de chaves do Azure, siga as etapas em Olá [Introdução ao Cofre de chaves do Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)

Para obter uma lista de Cmdlets do PowerShell usados com o Azure Key Vault, consulte [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

### <a name="azure-disk-encryption-for-windows"></a>Azure Disk Encryption para o Windows

O [Azure Disk Encryption para VMs IaaS Windows e Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protege dados pessoais em repouso em máquinas virtuais do Azure e é integrado ao Azure Key Vault. Criptografia de disco do Azure usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) no Windows e [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) no Linux tooencrypt ambos Olá discos de dados do sistema operacional e hello. Há suporte para o Azure Disk Encryption no Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 e nos clientes Windows 8 e Windows 10.

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a>Como usa os dados pessoais de tooprotect de criptografia de disco do Azure?

toouse criptografia de disco do Azure, você precisa de uma assinatura tooan conta do Azure. Criptografia de disco de Azure tooenable para Windows e VMs do Linux, Olá a seguir:

1. Usar o modelo do Gerenciador de recursos de criptografia de disco do Azure hello, PowerShell ou criptografia de disco de tooenable Olá interface de linha de comando (CLI) e especifique a configuração de criptografia. 

2. Conceder acesso toohello plataforma Windows Azure tooread Olá material de criptografia do seu Cofre de chaves.

3. Forneça um Azure Active Directory (AAD) aplicativo identidade toowrite Olá criptografia tooyour material de chave Cofre de chaves.

Azure atualizar hello VM e configuração do Cofre de chaves hello e configurar sua VM criptografado.

Quando você configura seu Cofre de chaves de toosupport criptografia de disco do Azure, você pode adicionar uma chave de criptografia de chave (KEK) para maior segurança e toosupport backup de máquinas de virtuais criptografadas.

![](media/protect-personal-data-at-rest/create-key.png)

Instruções detalhadas para cenários de implantação específicos e as experiências do usuário são incluídas em [Azure Disk Encryption para VMs IaaS Windows e Linux.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="azure-storage-service-encryption"></a>Criptografia do Serviço de Armazenamento do Azure

[Azure Storage Service criptografia (SSE) para dados em repouso](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) ajuda a proteger e proteger seu dados toomeet seus compromissos de segurança e conformidade organizacionais. Armazenamento do Azure automaticamente criptografa os dados usando toostorage de toopersisting anterior de criptografia de AES de 256 bits e a descriptografa tooretrieval anterior. Esse serviço está disponível para Blobs e Arquivos do Azure.

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a>Como usa os dados pessoais de tooprotect de criptografia do serviço de armazenamento?

tooenable criptografia do serviço de armazenamento, Olá a seguir:

1. Faça logon no hello portal do Azure.

2. Selecione uma conta de armazenamento.

3. Em configurações, na seção de serviço Blob hello, selecione a criptografia.

4. Em Olá seção serviço do arquivo, selecione a criptografia.

Depois de clicar em configuração de criptografia hello, você pode habilitar ou desabilitar a criptografia do serviço de armazenamento.

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

Novos dados serão criptografados. Os dados em arquivos existentes nesta conta de armazenamento permanecerão não criptografados.

Depois de habilitar a criptografia, copie a conta de armazenamento toohello dados usando um dos métodos a seguir de saudação:

1. Copiar blobs ou arquivos com hello [utilitário de linha de comando AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).

2. [Montar um compartilhamento de arquivos usando SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) , você pode usar um utilitário como o Robocopy toocopy arquivos.

3. Copiar blob ou arquivo de dados tooand do armazenamento de blob ou entre contas de armazenamento usando [bibliotecas de cliente de armazenamento como .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).

4.  Use um [Gerenciador de armazenamento](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour conta de armazenamento de blobs com criptografia ativada.

### <a name="transparent-data-encryption"></a>Transparent Data Encryption

Criptografia de dados transparente (TDE) é um recurso do SQL Azure pelo qual você pode criptografar os dados em ambos os níveis de banco de dados e servidor de saudação. A TDE agora é habilitada por padrão em todos os bancos de dados recém-criados. A TDE realiza a criptografia de e/s e a descriptografia da saudação dados e arquivos de log em tempo real.

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a>Como usa os dados pessoais do TDE tooprotect?

Você pode configurar TDE por meio de saudação portal do Azure, usando Olá API REST ou usando o PowerShell. tooenable TDE em um banco de dados existente usando Olá Portal do Azure, Olá a seguir:

1. Visite hello Azure portal em <https://portal.azure.com> e entrar com sua conta de administrador do Azure ou colaborador.

2. Na faixa esquerda do hello, clique tooBROWSE e, em seguida, clique em bancos de dados SQL.

3. Com bancos de dados SQL selecionados no painel esquerdo do hello, clique em seu banco de dados do usuário.

4. Na folha de banco de dados de saudação, clique em todas as configurações.

5. Na folha de configurações de saudação, clique em folha de criptografia transparente de dados criptografia parte tooopen Olá transparente de dados.

6. Na folha de criptografia de dados hello, mover Olá tooOn de botão de criptografia de dados e, em seguida, clique em Salvar (na parte superior de saudação da página Olá) tooapply configuração de saudação. Olá status de criptografia aproximará o progresso de Olá Olá transparente de criptografia de dados.

![Habilitando a criptografia de dados](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

Instruções sobre como o tooenable TDE e obter informações sobre a descriptografia de bancos de dados protegido por TDE e muito mais podem ser encontrados no artigo Olá [Transparent Data Encryption com o banco de dados do SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)

## <a name="summary"></a>Resumo

empresa Olá pode realizar sua meta de criptografar os dados pessoais armazenados na nuvem do Azure de saudação. Eles podem fazer isso usando a criptografia de disco do Azure muito proteger volumes inteiros. Isso pode incluir arquivos do sistema operacional hello e arquivos de dados que contêm informações de identificação pessoal e outros dados confidenciais. Criptografia do serviço de armazenamento do Azure pode ser usado tooprotect dados pessoais que são armazenados em arquivos e blobs. Para dados armazenados em bancos de dados SQL do Azure, a Transparent Data Encryption oferece proteção contra a exposição não autorizada de informações pessoais.

tooprotect Olá as chaves usadas tooencrypt dados no Azure, a empresa de Olá pode usar o Cofre de chaves do Azure. Isso simplifica o processo de gerenciamento de chaves de saudação e habilita Olá controle toomaintain de empresa de chaves que acessam e criptografar dados pessoais.

## <a name="next-steps"></a>Próximas etapas

- [Guia de solução de problemas do Azure Disk Encryption](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [Criptografar uma Máquina Virtual do Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [Criptografia de dados no Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [Criptografia de banco de dados em repouso do Azure Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
