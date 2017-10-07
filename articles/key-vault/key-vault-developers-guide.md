---
title: Guia do desenvolvedor do cofre chave aaaAzure
description: Os desenvolvedores podem usar chaves de criptografia do Azure Key Vault toomanage no ambiente do Microsoft Azure hello.
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 631cea1315964cd0b97e8b2cf3311754230fb801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-developers-guide"></a>Guia do desenvolvedor do Cofre da Chave do Azure

Cofre de chaves permite que você toosecurely acesso informações confidenciais de seus aplicativos:

- Chaves e segredos são protegidos sem a necessidade de código de saudação toowrite por conta própria e são facilmente toouse-os de seus aplicativos.
- Você está toohave capaz de seus clientes próprios e gerenciar suas próprias chaves para que você possa se concentrar no fornecimento de recursos de software Olá core. Dessa forma, seus aplicativos não possuirá responsabilidade hello ou responsabilidade potencial para segredos e chaves de locatário de seus clientes.
- Seu aplicativo pode usar chaves de assinatura e criptografia ainda mantém o gerenciamento de chaves Olá externo a partir de seu aplicativo, permitindo a sua solução toobe adequado como um aplicativo distribuído geograficamente.
- A partir da versão de setembro de 2016 saudação do Cofre de chaves, os aplicativos agora podem usar o Cofre de chaves [certificados](https://docs.microsoft.com/rest/api/keyvault/certificate-operations). Para obter mais informações, consulte [Sobre chaves, segredos e certificados](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Para obter mais informações gerais sobre o Cofre de Chaves do Azure, confira [O que é o Cofre de Chaves](key-vault-whatis.md).

## <a name="public-previews"></a>Visualizações públicas

Periodicamente, lançamos uma visualização pública de um novo recurso do Key Vault. Experimente-as e diga-no o que você acha via azurekeyvault@microsoft.com, nosso endereço de email para comentários.

### <a name="storage-account-keys---july-10-2017"></a>Chaves da Conta de Armazenamento – 10 de julho de 2017

>[!NOTE]
>Para esta atualização de saudação somente do Azure Key Vault **chaves da conta de armazenamento** recurso está em visualização.

Essa versão prévia inclui nosso novo recurso de Chaves de Conta de Armazenamento, disponível por meio destas interfaces: [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) e [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Para obter mais informações sobre o novo recurso de chaves de conta de armazenamento hello, consulte [visão geral de chaves de conta de armazenamento Azure Key Vault](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>Vídeos

Este vídeo mostra como toocreate sua própria chave de cofre e toouse do hello aplicativo de exemplo 'Hello Cofre de chaves'.

- [Desenvolvedor do Key Vault – guia de início rápido](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Recursos mencionados no vídeo acima:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Código de exemplo do Cofre de Chaves do Azure](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Criando e gerenciando Cofres da Chave

Antes de trabalhar com o Cofre de chaves do Azure no seu código, você pode criar e gerenciar cofres por meio de REST, modelos do Gerenciador de recursos, PowerShell ou CLI, conforme descrito em Olá artigos a seguir:

- [Criar e gerenciar Cofres de Chaves com a CLI](https://docs.microsoft.com/rest/api/keyvault/)
- [Criar e gerenciar Cofres das Chaves com o PowerShell](key-vault-get-started.md)
- [Criar e gerenciar Cofres das Chaves com a CLI](key-vault-manage-with-cli2.md)
- [Criar um cofre de chaves e adicionar um segredo por meio de um modelo do Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Operações em relação a cofres de chaves são autenticadas por meio do AAD e autorizadas por meio da própria política de acesso do Cofre da Chave, definido por cofre.

## <a name="coding-with-key-vault"></a>Codificação com o Cofre da Chave

Olá sistema de gerenciamento do Cofre de chaves para os programadores consiste em várias interfaces, com o restante como base hello. Por meio da interface REST de Olá, todos os recursos de cofres de chaves são acessíveis; chaves, segredos e certificados. [Referência da API REST do Key Vault](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Linguagens de programação compatíveis

#### <a name="net"></a>.NET

- [Referência da .NET API do Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Para obter mais informações sobre versão 2. x Olá Olá .NET SDK, consulte Olá [notas de versão](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java SDK para Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

Node. js, API de gerenciamento de cofre hello e API de objeto de cofre Olá são separadas. O Gerenciamento do Key Vault permite criar e atualizar seu cofre de chaves. API de Operações do Key Vault é para trabalhar com objetos de cofre como chaves, segredos e certificados. 

- [Referência da API do Node.js para gerenciamento do Key Vault](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Referência da API do Node.js para operações do Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Início rápido

- [Criar Cofre da Chave](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Introdução ao Key Vault em Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Exemplos de código

Para obter exemplos completos sobre como usar o Cofre de Chaves com seus aplicativos, confira:

- [Exemplos de código do Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) – aplicativo de exemplo do .NET *HelloKeyVault* e um exemplo do serviço Web do Azure. 
- [Usar o Cofre de chaves do Azure de um aplicativo Web](key-vault-use-from-web-application.md) -toohelp tutorial você aprenderá como toouse chave do Azure Cofre de um aplicativo web no Azure. 

## <a name="how-tos"></a>Instruções

Olá artigos e cenários a seguir fornecem diretrizes específicas da tarefa para trabalhar com o Cofre de chaves do Azure:

- [ID de locatário de Cofre de chaves de alteração após a assinatura mover](key-vault-subscription-move-fix.md) - quando você mover sua assinatura do Azure de um tootenant B de locatário, os cofres de chaves existentes são inacessíveis a saudação entidades de segurança (usuários e aplicativos) no locatário B. Corrija este usando este guia.
- [Acessar o Cofre de chaves por trás do firewall](key-vault-access-behind-firewall.md) -tooaccess uma chave de cofre seu Cofre de chaves cliente aplicativo necessidades toobe capaz de tooaccess vários pontos de extremidade para várias funcionalidades.
- [Como tooGenerate e Transfer HSM-Protected chaves para o Azure Key Vault](key-vault-hsm-protected-keys.md) -isso irá ajudá-lo a planejar, gerar e transferir sua própria toouse chaves protegidas por HSM com o Cofre de chaves do Azure.
- [Como o toopass proteger valores (como senhas) durante a implantação](../azure-resource-manager/resource-manager-keyvault-parameter.md) - quando você precisa toopass um valor seguro (como uma senha) como um parâmetro durante a implantação, você pode armazenar esse valor como um segredo em um valor de saudação Cofre de chaves do Azure e referência em outros Modelos do Gerenciador de recursos.
- [Como toouse Cofre de chaves para o gerenciamento extensível de chaves com o SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) -Olá SQL Server Connector para Cofre de chaves do Azure habilita o SQL Server e SQL em VM tooleverage hello Azure Key Vault serviço como um provedor de gerenciamento de chave extensível (EKM) tooprotect a criptografia das chaves de link de aplicativos; Criptografia transparente de dados, criptografia de Backup e criptografia de nível de coluna.
- [Como toodeploy tooVMs de certificados do Cofre de chaves](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - um aplicativo em nuvem em execução em uma VM no Azure necessidades um certificado. Como você obtém esse certificado para essa VM atualmente?
- [Como tooset o Cofre de chaves com final tooend chave rotação e auditoria](key-vault-key-rotation-log-monitoring.md) -isso explica como tooset a auditoria com o Cofre de chaves do Azure e a rotação de chaves.
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) (Implantando o certificado de aplicativo Web do Azure por meio do Key Vault) fornece instruções passo a passo para implantar certificados armazenados no Key Vault como parte da oferta do [Certificado do Serviço de Aplicativo](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Conceder permissão toomany aplicativos tooaccess um cofre de chaves](key-vault-group-permissions-for-apps.md) política de controle de acesso do Cofre de chaves dá suporte somente a 16 entradas. No entanto, você pode criar um grupo de segurança do Azure Active Directory. Adicione todos os hello associado do grupo de segurança de toothis de entidades de serviço e, em seguida, concede acesso toothis segurança grupo tooKey cofre.
- Para obter mais diretrizes específicas da tarefa sobre como integrar e usar os Cofres de Chaves com o Azure, consulte os [Exemplos de modelo do Azure Resource Manager do Ryan Jones para o Cofre de Chaves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Como toouse Cofre de chaves soft-exclusão com CLI](key-vault-soft-delete-cli.md) orienta você através de uso de saudação e ciclo de vida de um cofre de chaves e de vários objetos de Cofre de chaves com exclusão reversível habilitada.
- [Como toouse Cofre de chaves soft-exclusão com o PowerShell](key-vault-soft-delete-powershell.md) orienta você através de uso de saudação e ciclo de vida de um cofre de chaves e de vários objetos de Cofre de chaves com exclusão reversível habilitada.

## <a name="integrated-with-key-vault"></a>Introdução ao Cofre de Chaves

Estes artigos abordam outros cenários e serviços que usam ou se integram ao Key Vault.

- [Criptografia de disco do Azure](../security/azure-security-disk-encryption.md) aproveita Olá padrão da indústria [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) recurso do Windows e hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) recurso de criptografia de volume tooprovide Linux para hello sistema operacional e dados de saudação discos. solução de saudação é integrada ao Azure Key Vault toohelp controlar e gerenciar chaves de criptografia de disco hello e segredos em sua assinatura do Cofre de chaves, garantindo que todos os dados em discos da máquina virtual Olá sejam criptografados em repouso no armazenamento do Azure.
- [Repositório Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md) fornece a opção de criptografia de dados que são armazenados na conta de saudação. Para gerenciamento de chaves, o repositório Data Lake oferece dois modos de gerenciar suas chaves de criptografia mestra (MEKs), que são necessários para descriptografar os dados que são armazenados no hello repositório Data Lake. Você também pode deixar repositório Data Lake gerenciar Olá MEKs para você, ou escolha tooretain apropriar MEKs hello usando sua conta do Azure Key Vault. Especifique o modo de saudação do gerenciamento de chaves ao criar uma conta do repositório Data Lake. 
- [O Azure Information Protection](/information-protection/plan-design/plan-implement-tenant-key) permite que você toomanager sua própria chave de locatário. Por exemplo, em vez da Microsoft gerenciar sua chave de locatário (saudação padrão), você pode gerenciar sua próprias toocomply de chave de locatário com as normas específicas que se aplicam a organização tooyour. Gerenciar sua chave de locatário também é chamados tooas Traga sua própria chave ou BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Visões gerais e conceitos do Key Vault

- [Comportamento de exclusão reversível do Cofre de chaves](key-vault-ovw-soft-delete.md) descreve um recurso que permite a recuperação de objetos excluídos, se a exclusão de saudação foi acidental ou intencional.
- [Cliente de Cofre de chaves limitação](key-vault-ovw-throttling.md) orienta você toohello os conceitos básicos de limitação e oferece uma abordagem para seu aplicativo.
- [Visão geral de chaves de conta de armazenamento Cofre de chaves](key-vault-ovw-storage-keys.md) descreve Olá chaves de contas de armazenamento do Azure de integração de Cofre de chaves.
- [Mundos de segurança do Cofre de chaves](key-vault-ovw-security-worlds.md) descreve Olá relações entre regiões e áreas de segurança.

## <a name="social"></a>Redes sociais

- [Blog do Cofre de Chaves](http://aka.ms/kvblog)
- [Fórum do Cofre de Chaves](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Bibliotecas de Suporte

- A [Biblioteca Principal do Microsoft Azure Key Vault](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) fornece as interfaces **IKey** e **IKeyResolver** para localizar chaves com base em identificadores e realizar operações com chaves.
- As [Extensões do Cofre de Chaves do Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) fornecem recursos estendidos para o Cofre de Chaves do Azure.


