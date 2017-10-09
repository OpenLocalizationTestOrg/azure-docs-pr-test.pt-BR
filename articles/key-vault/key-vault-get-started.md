---
title: "aaaGet de Introdução ao Cofre de chaves do Azure | Microsoft Docs"
description: "Use este tutorial toohelp você obter Introdução ao Azure Key Vault toocreate um contêiner de proteção no Azure, toostore e gerenciar chaves de criptografia e segredos no Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Introdução ao Cofre da Chave do Azure
O Cofre da Chave do Azure está disponível na maioria das regiões. Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução
Use este tutorial toohelp você obter Introdução ao Azure Key Vault toocreate um contêiner protegido (um cofre) no Azure, toostore e gerenciar chaves de criptografia e segredos no Azure. Orienta você pelo processo de saudação do uso do Azure PowerShell toocreate um cofre que contém uma chave ou a senha que você pode usar com um aplicativo do Azure. Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.

**Estimado tempo toocomplete:** 20 minutos

> [!NOTE]
> Este tutorial não inclui instruções sobre como Olá toowrite aplicativo do Azure que inclua a uma das etapas hello, ou seja, como tooauthorize toouse um aplicativo uma chave ou segredo na chave Olá cofre.
>
> Este tutorial usa o Azure PowerShell. Para obter instruções de interface de linha de comando entre diferentes plataformas, consulte [este tutorial equivalente](key-vault-manage-with-cli2.md).
>
>

Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você deve ter Olá a seguir:

* TooMicrosoft uma assinatura do Azure. Se você não tiver uma, poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell, **versão mínima: 1.1.0**. tooinstall PowerShell do Azure e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Se você já tiver instalado o PowerShell do Azure e não souber a versão de hello, no console do Azure PowerShell hello, digite `(Get-Module azure -ListAvailable).Version`. Quando você tiver o Azure PowerShell versão 0.9.1 até 0.9.8 instalado, ainda poderá usar este tutorial com algumas pequenas alterações. Por exemplo, você deve usar o hello `Switch-AzureMode AzureResourceManager` comando e alguns comandos do Azure Key Vault Olá foram alterados. Para obter uma lista de cmdlets do Cofre de chaves para as versões 0.9.1 por meio de 0.9.8 de hello, consulte [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).
* Um aplicativo que será a chave de saudação toouse configurado ou a senha criados por você neste tutorial. Um aplicativo de exemplo está disponível no hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Para obter instruções, consulte Olá que acompanha o arquivo Leiame.

Este tutorial foi desenvolvido para iniciantes do PowerShell do Azure, mas ele pressupõe que você entender os conceitos básicos hello, como sessões, cmdlets e módulos. Para obter mais informações, consulte [Introdução ao Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

tooget ajuda detalhada para qualquer cmdlet que você vê neste tutorial, use Olá **Get-Help** cmdlet.

    Get-Help <cmdlet-name> -Detailed

Por exemplo, tooget ajuda Olá **AzureRmAccount Login** cmdlet, digite:

    Get-Help Login-AzureRmAccount -Detailed

Você também pode ler Olá tutoriais tooget familiarizado com o Azure Resource Manager no Azure PowerShell a seguir:

* [Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)
* [Usando o PowerShell do Azure com o Gerenciador de Recursos](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Conecte-se tooyour assinaturas
Iniciar uma sessão do PowerShell do Azure e entrar tooyour conta do Azure com hello comando a seguir:  

    Login-AzureRmAccount

Observe que se você estiver usando uma instância específica do Azure, por exemplo, o Azure Government usar Olá - parâmetro de ambiente com este comando. Por exemplo: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

Na janela de pop-up do navegador hello, insira seu nome de usuário da conta do Azure e a senha. O Azure PowerShell obtém todas as assinaturas de saudação que estão associadas com essa conta e, por padrão, usa Olá primeiro.

Se você tiver várias assinaturas e desejar toospecify um um toouse específico para o Cofre de chaves do Azure, digite Olá assinaturas de saudação toosee para sua conta a seguir:

    Get-AzureRmSubscription

Toouse de assinatura do hello de toospecify, em seguida,, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Para obter mais informações sobre como configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Criar um novo grupo de recursos
Quando você usa o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados dentro de um grupo de recursos. Nós criaremos um novo grupo de recursos chamado **ContosoResourceGroup** para este tutorial:

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Criar um cofre de chave
Saudação de uso [AzureRmKeyVault novo](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate um cofre de chaves. Esse cmdlet tem três parâmetros obrigatórios: um **nome do grupo de recursos**, um **nome do Cofre de chaves**e hello **geográfica**.

Por exemplo, se você usar o nome de cofre Olá de **ContosoKeyVault**, nome do grupo de recursos de saudação do **ContosoResourceGroup**e o local de saudação do **Ásia Oriental**, tipo:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

saída deste cmdlet Olá mostra propriedades do Cofre de chaves de saudação que você acabou de criar. Olá duas propriedades de mais importantes são:

* **Nome de cofre**: no exemplo hello, isso é **ContosoKeyVault**. Você usará esse nome para outros cmdlets do Cofre da Chave.
* **URI do cofre**: no exemplo hello, isso é https://contosokeyvault.vault.azure.net/. Aplicativos que usam seu cofre via API REST devem usar esse URI.

Sua conta do Azure é agora tooperform autorizado todas as operações nesta chave de cofre. Até o momento, ninguém mais está.

> [!NOTE]
> Se você vir o erro Olá **Olá assinatura não está registrado toouse namespace 'Microsoft.KeyVault'** ao tentar toocreate seu novo cofre de chaves, execute `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` e, em seguida, execute novamente o comando New-AzureRmKeyVault. Para obter mais informações, consulte [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Adicionar uma chave ou segredo toohello Cofre de chaves
Se você quiser Azure Key Vault toocreate uma chave protegida por software para você, use Olá [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet e digite Olá seguinte:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

No entanto, se você tiver uma chave protegida por software em um. PFX arquivo salvo tooyour C:\ unidade em um arquivo chamado softkey.pfx que você deseja tooupload tooAzure Cofre de chaves, Olá tipo após a variável de saudação tooset **securepfxpwd** com uma senha de **123** para hello. Arquivo PFX:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Em seguida, digite Olá seguir tooimport chave de saudação de saudação. Arquivo PFX, que protege a chave de saudação pelo software no hello serviço de Cofre de chaves:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Agora você pode referenciar essa chave que foi criada ou carregada tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obter a versão atual do hello e usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget essa versão específica.  

Olá toodisplay URI para essa chave, tipo:

    $Key.key.kid

tooadd um cofre toohello secreta, que é uma senha chamada SQLPassword e tem valor de saudação do Pa$ $w0rd tooAzure Cofre de chaves, primeiro converter o valor de saudação de cadeia de caracteres segura Pa$ $w0rd tooa digitando Olá seguinte:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Em seguida, digite o seguinte hello:

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Agora você pode referenciar essa senha que você adicionou tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obter a versão atual do hello e usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget essa versão específica.

Olá toodisplay URI para esse segredo, tipo:

    $secret.Id

Vejamos chave hello ou chave secreta que você acabou de criar:

* tooview sua chave, tipo:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview seu segredo, tipo:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Agora, seu Cofre de chaves e a chave ou segredo está pronto para toouse de aplicativos. É necessário autorizar aplicativos toouse-los.  

## <a id="register"></a>Registrar um aplicativo com o Active Directory do Azure
Esta etapa geralmente seria feita por um desenvolvedor, em um computador separado. Ele não é específico tooAzure Cofre de chaves, mas é incluído aqui para fins de integridade.

> [!IMPORTANT]
> tutorial de saudação toocomplete, sua conta, cofre hello e aplicativo hello que registrar-se nesta etapa devem ser no hello mesmo diretório do Azure.
>
>

Aplicativos que usam um cofre de chave devem ser autenticados usando um token do Active Directory do Azure. toodo, Olá proprietário do aplicativo hello deve primeiro registrar aplicativo hello no seu Active Directory do Azure. No final de saudação do registro, o proprietário do aplicativo hello obtém Olá valores a seguir:

* Um **ID do aplicativo** (também conhecido como uma ID de cliente) e **chave de autenticação** (também conhecido como segredo compartilhado Olá). aplicativo Hello deve apresentar ambos esses valores tooAzure do Active Directory, tooget um token. Como o aplicativo hello está configurado toodo que isso depende do aplicativo hello. Para Olá aplicativo de exemplo do Cofre de chaves, o proprietário do aplicativo hello define esses valores no arquivo App. config de saudação.

aplicativo de hello tooregister no Active Directory do Azure:

1. Entrar toohello portal clássico do Azure.
2. Olá esquerda, clique em **do Active Directory**e, em seguida, selecione o diretório de saudação na qual você registrará o seu aplicativo. <br> <br> **Observação:** você deve selecionar Olá Olá mesmo diretório que contém a assinatura do Azure com o qual você criou seu Cofre de chaves. Se você não souber qual diretório isto é, clique em **configurações**, identificar Olá assinatura com a qual você criou seu Cofre de chaves e nome de saudação de observação do diretório Olá exibido na última coluna de saudação.
3. Clique em **APLICATIVOS**. Se nenhum aplicativo adicionou tooyour diretório, essa página mostra somente Olá **adicionar um aplicativo** link. Clique em link hello, ou como alternativa, você pode clicar em **adicionar** na barra de comandos de saudação.
4. Em Olá **Adicionar aplicativo** assistente, em Olá **o que fazer você deseja toodo?** , clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.
5. Em Olá **Conte-nos sobre seu aplicativo** página, especifique um nome para seu aplicativo e, em seguida, selecione **aplicativo de WEB e/ou API WEB** (Olá padrão). Clique em Olá **próximo** ícone.
6. Em Olá **propriedades do aplicativo** especifique Olá **URL de logon** e **URI da ID do aplicativo** para seu aplicativo da web. Se seu aplicativo não tiver esses valores, você pode inventá-los para esta etapa (por exemplo, você poderia especificar http://test1.contoso.com para as duas caixas). Não importa se os sites existem. O importante é que aplicativo hello URI de ID para cada aplicativo é diferente para cada aplicativo em seu diretório. diretório de saudação usa tooidentify essa cadeia de caracteres em seu aplicativo.
7. Clique em Olá **concluir** ícone toosave suas alterações no Assistente de saudação.
8. Em Olá **início rápido** , clique em **configurar**.
9. Role toohello **chaves** seção, selecione a duração de saudação e, em seguida, clique em **salvar**. página de saudação é atualizada e agora mostra um valor de chave. Você deve configurar seu aplicativo com esse valor de chave e hello **ID do cliente** valor. (As instruções para esta configuração são específicas do aplicativo.)
10. Copie valor de ID de cliente Olá nessa página, que você usará Olá próxima etapa tooset permissões em seu cofre.

## <a id="authorize"></a>Autorizar Olá aplicativo toouse Olá chave ou segredo
tooauthorize Olá aplicativo tooaccess Olá chave ou segredo no cofre hello, use o [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.

Por exemplo, se o nome do cofre for **ContosoKeyVault** e aplicativo hello deseja tooauthorize tem uma ID de cliente de 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você deseja tooauthorize Olá aplicativo toodecrypt e entre com as chaves no seu cofre, execute o seguinte hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Se você quiser tooauthorize esse mesmo segredos de tooread do aplicativo em seu cofre, execute o seguinte de saudação:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Se você quiser toouse um módulo de segurança de hardware (HSM)
Para garantia extra, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello. Olá HSMs são FIPS 140-2 nível 2 validado. Se esse requisito não se aplica a tooyou, ignore esta seção e vá muito[excluir Cofre de chaves hello e chaves associadas e segredos](#delete).

toocreate essas chaves protegidas por HSM, você deve usar o hello [chaves protegidas por HSM de toosupport da camada de serviço do Azure Key Vault Premium](https://azure.microsoft.com/pricing/free-trial/). Além disso, observe que essa funcionalidade não está disponível para o Azure China.

Quando você criar o Cofre de chaves Olá, adicionar Olá **- SKU** parâmetro:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e o Cofre de chaves de toothis chaves protegidas por HSM. toocreate uma chave protegida por HSM, Olá conjunto **-destino** too'HSM do parâmetro ':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Você pode usar uma chave de saudação tooimport de comando a seguir um. Arquivo PFX em seu computador. Este comando importa chave Olá para HSMs em Olá serviço de Cofre de chaves:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


comando Avançar Olá importa um "Traga sua própria chave" pacote (BYOK). Este cenário permite que você gerar sua chave em seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Para obter mais instruções sobre como toogenerate esse pacote BYOK, consulte [como toogenerate e transferir chaves protegidas por HSM para o Azure Key Vault](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Excluir o Cofre de chaves hello e chaves associadas e segredos
Se você não precisar mais Cofre de chaves hello e chave de saudação ou segredo que ele contém, você pode excluir o Cofre de chaves hello usando Olá [AzureRmKeyVault remover](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Ou, você pode excluir um grupo de recursos do Azure inteiro, que inclui o Cofre de chaves de saudação e outros recursos incluídos no grupo:

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Outros cmdlets do PowerShell do Azure
Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: este comando obtém uma exibição em tabela de todas as chaves e propriedades selecionadas.
* `$Keys[0]`: Este comando exibe uma lista completa das propriedades de chave especificado Olá
* `Get-AzureKeyVaultSecret`: este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Exemplo como tooremove uma chave específica.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Exemplo como tooremove um segredo específico.

## <a id="next"></a>Próximas etapas
Para um tutorial de acompanhamento que usa o Cofre da Chave do Azure em um aplicativo Web, confira [Usar o Cofre da Chave do Azure em um Aplicativo Web](key-vault-use-from-web-application.md).

toosee como seu Cofre de chaves está sendo usado, consulte [log do Azure Key Vault](key-vault-logging.md).

Para obter uma lista de Olá cmdlets do PowerShell do Azure mais recentes para o Cofre de chaves do Azure, consulte [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).

Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).
