---
title: Guia do desenvolvedor do Cofre da Chave do Azure
description: Os desenvolvedores podem usar o Cofre da Chave do Azure para gerenciar chaves de criptografia no ambiente do Microsoft Azure.
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: fec4769c0bd571edea84dd2f766bb907d8819be5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-developers-guide"></a>Guia do desenvolvedor do Cofre da Chave do Azure

O Key Vault permite acessar com segurança informações confidenciais nos aplicativos:

- As chaves e os segredos são protegidos sem que você mesmo precise escrever código e você pode usá-los facilmente em seus aplicativos.
- Você pode fazer com que seus clientes possuam e gerenciem suas próprias chaves e se concentrar em fornecer os principais recursos do software. Dessa forma, os aplicativos não serão responsáveis ou potencialmente responsáveis pelas chaves e segredos do locatário de seus clientes.
- Seu aplicativo pode usar chaves para assinatura e criptografia, mas ainda manter o gerenciamento de chaves fora de seu aplicativo, permitindo que sua solução seja adequada a um aplicativo distribuído geograficamente.
- A partir do lançamento de setembro de 2016 do Key Vault, seus aplicativos agora podem usar [certificados](https://docs.microsoft.com/rest/api/keyvault/certificate-operations) do Key Vault. Para obter mais informações, consulte [Sobre chaves, segredos e certificados](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates).

Para obter mais informações gerais sobre o Cofre de Chaves do Azure, confira [O que é o Cofre de Chaves](key-vault-whatis.md).

## <a name="public-previews"></a>Visualizações públicas

Periodicamente, lançamos uma visualização pública de um novo recurso do Key Vault. Experimente-as e diga-no o que você acha via azurekeyvault@microsoft.com, nosso endereço de email para comentários.

### <a name="storage-account-keys---july-10-2017"></a>Chaves da Conta de Armazenamento – 10 de julho de 2017

>[!NOTE]
>Para esta atualização do Azure Key Vault, apenas o recurso **Chaves da Conta de Armazenamento** está em versão prévia.

Essa versão prévia inclui nosso novo recurso de Chaves de Conta de Armazenamento, disponível por meio destas interfaces: [.NET/C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault/), [REST](https://docs.microsoft.com/rest/api/keyvault/) e [PowerShell](https://docs.microsoft.com/powershell/module/azurerm.keyvault/). 

Para obter mais informações sobre o novo recurso de Chaves de Conta de Armazenamento, consulte [Visão geral de chaves de conta de armazenamento Azure Key Vault](key-vault-ovw-storage-keys.md).

## <a name="videos"></a>vídeos

Este vídeo mostra como criar seu próprio cofre de chaves e como usá-lo por meio do aplicativo de exemplo “Hello Key Vault”.

- [Desenvolvedor do Key Vault – guia de início rápido](https://channel9.msdn.com/Blogs/Azure/Azure-Key-Vault-Developer-Quick-Start/player)

Recursos mencionados no vídeo acima:

- [Azure PowerShell](http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409)
- [Código de exemplo do Cofre de Chaves do Azure](http://go.microsoft.com/fwlink/?LinkId=521527&clcid=0x409)

## <a name="creating-and-managing-key-vaults"></a>Criando e gerenciando Cofres da Chave

Antes de trabalhar com o Cofre da Chave do Azure em seu código, você pode criar e gerenciar cofres por meio de REST, modelos de Gerenciador de Recursos, PowerShell ou CLI, conforme descrito nos seguintes artigos:

- [Criar e gerenciar Cofres de Chaves com a CLI](https://docs.microsoft.com/rest/api/keyvault/)
- [Criar e gerenciar Cofres das Chaves com o PowerShell](key-vault-get-started.md)
- [Criar e gerenciar Cofres das Chaves com a CLI](key-vault-manage-with-cli2.md)
- [Criar um cofre de chaves e adicionar um segredo por meio de um modelo do Azure Resource Manager](../azure-resource-manager/resource-manager-template-keyvault.md)

> [!NOTE]
> Operações em relação a cofres de chaves são autenticadas por meio do AAD e autorizadas por meio da própria política de acesso do Cofre da Chave, definido por cofre.

## <a name="coding-with-key-vault"></a>Codificação com o Cofre da Chave

O sistema de gerenciamento do Key Vault para programadores consiste em várias interfaces, com o REST como base. Por meio da interface REST, todos os recursos dos cofres de chaves estão acessíveis; chaves, segredos e certificados. [Referência da API REST do Key Vault](https://docs.microsoft.com/rest/api/keyvault/). 

### <a name="supported-programming-languages"></a>Linguagens de programação compatíveis

#### <a name="net"></a>.NET

- [Referência da .NET API do Key Vault](https://docs.microsoft.com/dotnet/api/microsoft.azure.keyvault) 

Para obter mais informações sobre a versão 2.x do SDK do .NET, consulte as [Notas de versão](key-vault-dotnet2api-release-notes.md).

#### <a name="java"></a>Java

- [Java SDK para Key Vault](https://docs.microsoft.com/java/api/com.microsoft.azure.keyvault)

#### <a name="nodejs"></a>Node.js

No Node.js, a API de gerenciamento do cofre e a API de objeto do cofre são separadas. O Gerenciamento do Key Vault permite criar e atualizar seu cofre de chaves. API de Operações do Key Vault é para trabalhar com objetos de cofre como chaves, segredos e certificados. 

- [Referência da API do Node.js para gerenciamento do Key Vault](http://azure.github.io/azure-sdk-for-node/azure-arm-keyvault/latest/)
- [Referência da API do Node.js para operações do Key Vault](http://azure.github.io/azure-sdk-for-node/azure-keyvault/latest/) 

### <a name="quick-start"></a>Início rápido

- [Criar Cofre da Chave](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
- [Introdução ao Key Vault em Node.js](https://azure.microsoft.com/en-us/resources/samples/key-vault-node-getting-started/)

### <a name="code-examples"></a>Exemplos de código

Para obter exemplos completos sobre como usar o Cofre de Chaves com seus aplicativos, confira:

- [Exemplos de código do Azure Key Vault](http://www.microsoft.com/download/details.aspx?id=45343) – aplicativo de exemplo do .NET *HelloKeyVault* e um exemplo do serviço Web do Azure. 
- [Usar Azure Key Vault de um aplicativo Web](key-vault-use-from-web-application.md) – tutorial para ajudar você a aprender a usar o Azure Key Vault em um aplicativo Web no Azure. 

## <a name="how-tos"></a>Instruções

Os artigos e cenários a seguir fornecem diretrizes específicas da tarefa para trabalhar com o Azure Key Vault:

- [Alterar a ID de locatário do cofre de chaves depois de mover a assinatura](key-vault-subscription-move-fix.md) - quando você mover sua assinatura do Azure do locatário A para o locatário B, os cofres de chaves existentes não poderão ser acessados pelas entidades (usuários e aplicativos) no locatário B. Corrija isso usando este guia.
- [Acessando o Cofre de Chaves por trás do firewall](key-vault-access-behind-firewall.md) - para acessar um cofre de chaves, seu aplicativo cliente do cofre de chaves deve ser capaz de acessar vários pontos de extremidade para várias funcionalidades.
- [Como gerar e transferir chaves protegidas pelo HSM para o Cofre de Chaves do Azure](key-vault-hsm-protected-keys.md) - isso vai ajudá-lo a planejar, gerar e transferir suas próprias chaves protegidas pelo HSM a serem usadas com o Cofre de Chaves do Azure.
- [Como transmitir valores seguros (como senhas) durante a implantação](../azure-resource-manager/resource-manager-keyvault-parameter.md) - Quando você precisa transmitir um valor seguro (como uma senha) como um parâmetro durante a implantação, é possível armazenar esse valor como um segredo em um Cofre de Chaves do Azure e fazer referência ao valor em outros modelos do Resource Manager.
- [Como usar o Cofre de Chaves para o gerenciamento extensível de chaves com o SQL Server](https://msdn.microsoft.com/library/dn198405.aspx) - O Conector do SQL Server para o Cofre de Chaves do Azure permite que o SQL Server e o SQL em uma VM utilizem o serviço do Cofre de Chaves do Azure como um provedor EKM (gerenciamento extensível de chaves) para proteger suas chaves de criptografia para o vínculo de aplicativos; Transparent Data Encryption, Criptografia de Backup e Criptografia de Nível de Coluna.
- [Como implantar certificados em VMs do Cofre de Chaves](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/) - Um aplicativo em nuvem em execução em uma VM no Azure precisa de um certificado. Como você obtém esse certificado para essa VM atualmente?
- [Configurar o Key Vault com a rotação de chaves e auditoria de ponta a ponta](key-vault-key-rotation-log-monitoring.md) – Explica como configurar a auditoria e a rotação de chaves com o Azure Key Vault.
- [Deploying Azure Web App Certificate through Key Vault]( https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/) (Implantando o certificado de aplicativo Web do Azure por meio do Key Vault) fornece instruções passo a passo para implantar certificados armazenados no Key Vault como parte da oferta do [Certificado do Serviço de Aplicativo](https://azure.microsoft.com/blog/internals-of-app-service-certificate/).
- [Grant permission to many applications to access a key vault](key-vault-group-permissions-for-apps.md) (Conceder permissão a muitos aplicativos para acessar um Key Vault) A política de controle de acesso do Key Vault permite apenas 16 entradas. No entanto, você pode criar um grupo de segurança do Azure Active Directory. Adicione todas as entidades de serviço associadas a esse grupo de segurança e, em seguida, conceda a esse grupo de segurança acesso ao Key Vault.
- Para obter mais diretrizes específicas da tarefa sobre como integrar e usar os Cofres de Chaves com o Azure, consulte os [Exemplos de modelo do Azure Resource Manager do Ryan Jones para o Cofre de Chaves](https://github.com/rjmax/ArmExamples/tree/master/keyvaultexamples).
- [Como usar a exclusão reversível do Key Vault com CLI](key-vault-soft-delete-cli.md) orienta pela utilização e ciclo de vida de um cofre de chaves e de vários objetos de cofre de chaves com a exclusão reversível habilitada.
- [Como usar a exclusão reversível do Key Vault com PowerShell](key-vault-soft-delete-powershell.md) orienta pela utilização e ciclo de vida de um cofre de chaves e de vários objetos de cofre de chaves com a exclusão reversível habilitada.

## <a name="integrated-with-key-vault"></a>Introdução ao Cofre de Chaves

Estes artigos abordam outros cenários e serviços que usam ou se integram ao Key Vault.

- A [Azure Disk Encryption](../security/azure-security-disk-encryption.md) aproveita o recurso padrão da indústria [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) do Windows e o recurso [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) do Linux para fornecer criptografia de volume para o SO e os discos de dados. A solução é integrada ao Cofre de Chaves do Azure para ajudá-lo a controlar e a gerenciar as chaves de criptografia de disco e segredos em sua assinatura de cofre de chaves, garantindo ao mesmo tempo que todos os dados nos discos de máquina virtual sejam criptografados em repouso no armazenamento do Azure.
- O [Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md) fornece a opção de criptografia dos dados que são armazenados na conta. Em relação ao gerenciamento de chaves, o Data Lake Store fornece dois modos para gerenciar suas chaves-mestras de criptografia (MEKs), que são necessárias para descriptografar os dados armazenados no Data Lake Store. Você também pode deixar o Data Lake Store gerenciar as MEKs para você ou optar por manter a propriedade das MEKs usando sua conta do Cofre de Chaves do Azure. Você pode especificar o modo de gerenciamento de chaves ao criar uma conta do Data Lake Store. 
- [Proteção de Informações do Azure](/information-protection/plan-design/plan-implement-tenant-key) permite a você gerenciar sua própria chave de locatário. Por exemplo, em vez de a Microsoft gerenciar sua chave de locatário (o padrão), você pode gerenciá-la para cumprir os regulamentos específicos que se aplicam à sua organização. Gerenciar sua própria chave de locatário também é conhecido como "traga sua própria chave", ou BYOK.

## <a name="key-vault-overviews-and-concepts"></a>Visões gerais e conceitos do Key Vault

- [Comportamento de exclusão reversível do Key Vault](key-vault-ovw-soft-delete.md) descreve um recurso que permite a recuperação de objetos excluídos, seja a exclusão acidental ou intencional.
- [Limitação de cliente do Key Vault](key-vault-ovw-throttling.md) orienta você sobre os conceitos básicos de limitação e oferece uma abordagem para seu aplicativo.
- [Visão geral de chaves de conta de armazenamento do Key Vault](key-vault-ovw-storage-keys.md) descreve as chaves de Contas de Armazenamento do Azure de integração do Key Vault.
- [Mundos de segurança do Key Vault](key-vault-ovw-security-worlds.md) descreve as relações entre regiões e áreas de segurança.

## <a name="social"></a>Redes sociais

- [Blog do Cofre de Chaves](http://aka.ms/kvblog)
- [Fórum do Cofre de Chaves](http://aka.ms/kvforum)

## <a name="supporting-libraries"></a>Bibliotecas de Suporte

- A [Biblioteca Principal do Microsoft Azure Key Vault](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core) fornece as interfaces **IKey** e **IKeyResolver** para localizar chaves com base em identificadores e realizar operações com chaves.
- As [Extensões do Cofre de Chaves do Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions) fornecem recursos estendidos para o Cofre de Chaves do Azure.


