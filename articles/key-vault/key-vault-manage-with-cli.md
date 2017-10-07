---
title: Cofre de chave do Azure usando a CLI do aaaManage | Microsoft Docs
description: "Use este tutorial tooautomate as tarefas comuns no cofre de chaves usando Olá CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>Gerenciar Cofre da Chave usando a CLI

O Cofre da Chave do Azure está disponível na maioria das regiões. Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução

Use este tutorial toohelp você obter Introdução ao Azure Key Vault toocreate um contêiner protegido (um cofre) no Azure, toostore e gerenciar chaves de criptografia e segredos no Azure. Orienta você pelo processo de saudação do uso de Interface de linha de comando de plataforma cruzada do Azure toocreate um cofre que contém uma chave ou a senha que você pode usar com um aplicativo do Azure. Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.

**Estimado tempo toocomplete:** 20 minutos

> [!NOTE]
> Este tutorial não inclui instruções sobre como toowrite Olá aplicativo do Azure que uma das etapas de saudação inclui, que mostra como tooauthorize toouse um aplicativo uma chave ou segredo na chave Olá cofre.
> 
> No momento, você não pode configurar o Cofre de chaves do Azure no portal do Azure de saudação. Em vez disso, use as instruções da Interface de Linha de Comando de Plataforma Cruzada do Azure. Ou, para obter instruções do PowerShell do Azure, consulte [este tutorial equivalente](key-vault-get-started.md).
> 
> 

Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você deve ter Olá a seguir:

* TooMicrosoft uma assinatura do Azure. Se não tiver uma assinatura, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial).
* Interface de Linha de Comando versão 0.9.1 ou posterior. tooinstall Olá a versão mais recente e conecte-se tooyour assinatura do Azure, consulte [instalar e configurar Olá Interface de linha de comando de plataforma cruzada do Azure](../cli-install-nodejs.md).
* Um aplicativo que será a chave de saudação toouse configurado ou a senha criados por você neste tutorial. Um aplicativo de exemplo está disponível no hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Para obter instruções, consulte Olá que acompanha o arquivo Leiame.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Obtendo ajuda com a interface de linha de comando de plataforma cruzada do Azure

Este tutorial presume que você esteja familiarizado com a interface de linha de comando da saudação (Bash, Terminal, prompt de comando)

Hello – ajuda -h parâmetro ou pode ser usado tooview ajuda para comandos específicos. Como alternativa, hello azure help [comando] [Opções] formato também pode ser usado tooreturn Olá mesmas informações. Por exemplo, a seguir Olá comandos retornam todas as mesmas informações de hello:

    azure account set --help

    azure account set -h

    azure help account set

Em caso de dúvida sobre parâmetros Olá necessários por um comando, consulte usando toohelp – ajuda, -h ou azure help [comando].

Você também pode ler Olá tutoriais tooget familiarizado com o Azure Resource Manager na Interface de linha de comando de plataforma cruzada do Azure a seguir:

* [Como tooinstall e configurar a Interface de linha de comando de plataforma cruzada do Azure](../cli-install-nodejs.md)
* [Usando a interface de linha de comando de plataforma cruzada do Azure com o Gerenciador de Recursos do Azure](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Conecte-se tooyour assinaturas

toolog usando uma conta organizacional, use Olá comando a seguir:

    azure login -u username -p password

ou se você quiser toolog no digitando interativamente

    azure login

> [!NOTE]
> método de logon Hello só funciona com contas da organização. Uma conta institucional é um usuário gerenciado pela organização e definido no locatário do Active Directory do Azure da organização.
> 
> 

Se você não tem uma conta organizacional e estiver usando um toolog de conta da Microsoft em tooyour assinatura do Azure, você pode criar facilmente usando um Olá seguintes etapas.

1. Logon toohello Login toohello [Portal de gerenciamento](https://manage.windowsazure.com/)e clique em Active Directory.
2. Se a pasta não existir, selecione Criar seu diretório e fornecer Olá informações solicitadas.
3. Selecione o diretório e adicione um novo usuário. Esse novo usuário é uma conta institucional. Durante a criação de saudação do usuário hello, você é fornecido com um endereço de email para o usuário hello e uma senha temporária. Salve essas informações como elas são usadas em outra etapa.
4. No portal de hello, selecione configurações e administradores. Selecione Adicionar e adicionar Olá novo usuário como coadministrador. Isso permite Olá conta organizacional toomanage sua assinatura do Azure.
5. Por fim, faça logoff de saudação portal do Azure e, em seguida, faça logon usando a nova conta organizacional de saudação. Se isso for Olá primeiro log de tempo com essa conta, será solicitada toochange senha de saudação.

Para obter mais informações sobre como usar contas institucionais no Microsoft Azure, consulte [Inscrever-se no Microsoft Azure como uma organização](../active-directory/sign-up-organization.md).

Se você tiver várias assinaturas e desejar toospecify um um toouse específico para o Cofre de chaves do Azure, digite Olá assinaturas de saudação toosee para sua conta a seguir:

    azure account list

Toouse de assinatura do hello de toospecify, em seguida,, tipo:

    azure account set <subscription name>

Para obter mais informações sobre como configurar a Interface de linha de comando de plataforma cruzada do Azure, consulte [como tooInstall e configurar a Interface de linha de comando de plataforma cruzada do Azure](../cli-install-nodejs.md).

## <a name="switch-toousing-azure-resource-manager"></a>Alternar toousing Gerenciador de recursos do Azure
Olá Cofre de chaves requer o Azure Resource Manager, digite Olá tooswitch tooAzure Gerenciador de recursos modo a seguir:

    azure config mode arm

## <a name="create-a-new-resource-group"></a>Criar um novo grupo de recursos
Ao usar o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados em um grupo de recursos. Criaremos um novo grupo de recursos “ContosoResourceGroup” para este tutorial.

    azure group create 'ContosoResourceGroup' 'East Asia'

Olá primeiro parâmetro é o nome do grupo de recursos e Olá segundo parâmetro é o local de saudação. Para local, use o comando Olá `azure location list` tooidentify como toospecify toohello um local alternativo uma neste exemplo. Se precisar de mais informações, digite: `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Registrar o provedor de recursos do Cofre de chaves Olá
Verifique se o provedor de recursos do Cofre de Chaves está registrado em sua assinatura:

`azure provider register Microsoft.KeyVault`

Isso só precisa toobe feito uma vez por assinatura.

## <a name="create-a-key-vault"></a>Criar um cofre de chave

Saudação de uso `azure keyvault create` comando toocreate um cofre de chaves. Esse script tem três parâmetros obrigatórios: um nome de grupo de recursos, um nome de Cofre de chaves e localização geográfica hello.

Por exemplo, se você usar o nome do cofre Olá de ContosoKeyVault, nome do grupo de recursos de saudação do ContosoResourceGroup e o local de saudação do Leste Asiático, digite:

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

saída de Hello desse comando mostra as propriedades do Cofre de chaves de saudação que você acabou de criar. Olá duas propriedades de mais importantes são:

* **Nome**: no exemplo hello, isso é ContosoKeyVault. Você usará esse nome para outros cmdlets do Cofre da Chave.
* **vaultUri**: no exemplo hello, isso é https://contosokeyvault.vault.azure.net. Aplicativos que usam seu cofre via API REST devem usar esse URI.

Sua conta do Azure é agora tooperform autorizado todas as operações nesta chave de cofre. Até o momento, ninguém mais está.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Adicionar uma chave ou segredo toohello Cofre de chaves

Se você quiser Azure Key Vault toocreate uma chave protegida por software para você, use Olá `azure key create` de comando e digite Olá a seguir:

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

No entanto, se você tiver uma chave existente em um arquivo. PEM salvo como arquivo local em um arquivo chamado softkey.pem que você deseja tooupload tooAzure Cofre de chaves, digite Olá seguir tooimport chave de saudação de saudação. Arquivo PEM, que protege a chave de saudação pelo software no hello serviço de Cofre de chaves:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

Agora você pode referenciar chave Olá que foi criada ou carregada tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obter a versão atual do hello e usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget essa versão específica.

tooadd um cofre toohello secreta, que é uma senha chamada SQLPassword e que tem o valor de saudação do Pa$ $w0rd tooAzure Cofre de chaves, Olá tipo a seguir:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

Agora você pode referenciar essa senha que você adicionou tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obter a versão atual do hello e usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget essa versão específica.

Vejamos chave hello ou chave secreta que você acabou de criar:

* tooview sua chave, tipo:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview seu segredo, tipo:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Registrar um aplicativo com o Active Directory do Azure

Esta etapa geralmente seria feita por um desenvolvedor, em um computador separado. Ele não é específico tooAzure Cofre de chaves, mas é incluído aqui, para fins de integridade.

> [!IMPORTANT]
> tutorial de saudação toocomplete, sua conta, cofre hello e aplicativo hello que registrar-se nesta etapa devem ser no hello mesmo diretório do Azure.
> 
> 

Aplicativos que usam um cofre de chave devem ser autenticados usando um token do Active Directory do Azure. toodo, Olá proprietário do aplicativo hello deve primeiro registrar aplicativo hello no seu Active Directory do Azure. No final de saudação do registro, o proprietário do aplicativo hello obtém Olá valores a seguir:

* Um **ID do aplicativo** (também conhecido como uma ID de cliente) e **chave de autenticação** (também conhecido como segredo compartilhado Olá). aplicativo Hello deve apresentar ambos tooAzure esses valores do Active Directory, tooget um token. Como o aplicativo hello está configurado toodo que isso depende do aplicativo hello. Para Olá aplicativo de exemplo do Cofre de chaves, o proprietário do aplicativo hello define esses valores no arquivo App. config de saudação.

aplicativo de hello tooregister no Active Directory do Azure:

1. Entrar toohello portal do Azure.
2. Olá esquerda, clique em **do Active Directory**e, em seguida, selecione o diretório de saudação na qual você registrará o seu aplicativo. <br> <br> 

>[!NOTE] 
> Você deve selecionar Olá Olá mesmo diretório que contém a assinatura do Azure com o qual você criou seu Cofre de chaves. Se você não souber qual diretório isto é, clique em **configurações**, identificar Olá assinatura com a qual você criou seu Cofre de chaves e nome de saudação de observação do diretório Olá exibido na última coluna de saudação.

3. Clique em **APLICATIVOS**. Se nenhum aplicativo adicionou tooyour diretório, essa página mostrará apenas Olá **adicionar um aplicativo** link. Clique em link hello, ou como alternativa, você pode clicar em Olá **adicionar** na barra de comandos de saudação.
4. Em Olá **Adicionar aplicativo** assistente, em Olá **o que fazer você deseja toodo?** , clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.
5. Em Olá **Conte-nos sobre seu aplicativo** página, especifique um nome para seu aplicativo e selecione **aplicativo de WEB e/ou API WEB** (Olá padrão). Clique em próximo ícone de saudação.
6. Em Olá **propriedades do aplicativo** especifique Olá **URL de logon** e **URI da ID do aplicativo** para seu aplicativo da web. Se seu aplicativo não tiver esses valores, você pode inventá-los para esta etapa (por exemplo, você poderia especificar http://test1.contoso.com para as duas caixas). Não importa se existirem a esses sites; o importante é que aplicativo hello URI de ID para cada aplicativo é diferente para cada aplicativo em seu diretório. diretório de saudação usa tooidentify essa cadeia de caracteres em seu aplicativo.
7. Clique em Olá ícone completa toosave suas alterações no Assistente de saudação.
8. Na página início rápido hello, clique em **configurar**.
9. Role toohello **chaves** seção, selecione a duração de saudação e, em seguida, clique em **salvar**. página de saudação é atualizada e agora mostra um valor de chave. Você deve configurar seu aplicativo com esse valor de chave e hello **ID do cliente** valor. (As instruções para esta configuração são específicas do aplicativo).
10. Copie valor de ID de cliente Olá nessa página, que você usará Olá próxima etapa tooset permissões em seu cofre.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autorizar Olá aplicativo toouse Olá chave ou segredo
tooauthorize Olá aplicativo tooaccess Olá chave ou segredo no cofre hello, use Olá `azure keyvault set-policy` comando.

Por exemplo, se o nome do cofre for ContosoKeyVault e hello aplicativo deseja tooauthorize tem uma ID de cliente de 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você deseja tooauthorize Olá aplicativo toodecrypt e entre com as chaves em seu cofre, execute Olá a seguir:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> Se você estiver executando no prompt de comando do Windows, substituir aspas com aspas duplas e aspas duplas interno de saudação de escape também. Por exemplo: "[\"decrypt\",\"sign\"]".
> 
> 

Se você quiser tooauthorize esse mesmo segredos de tooread do aplicativo em seu cofre, execute o seguinte de saudação:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Se você quiser toouse um módulo de segurança de hardware (HSM)
Para garantia extra, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello. Olá HSMs são FIPS 140-2 nível 2 validado. Se esse requisito não se aplica a tooyou, ignore esta seção e vá muito[excluir Cofre de chaves hello e chaves associadas e segredos](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate essas chaves protegidas por HSM, você deve ter uma assinatura do cofre que dá suporte a chaves protegidas por HSM.

Quando você cria keyvault Olá, adicione um parâmetro de 'sku' hello:

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e o Cofre de chaves protegidas por HSM toothis. toocreate uma chave protegida por HSM, too'HSM de parâmetro de destino do conjunto de saudação ':

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

Você pode usar o hello após o comando tooimport uma chave de um arquivo. PEM em seu computador. Este comando importa chave Olá para HSMs em Olá serviço de Cofre de chaves:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

comando Avançar Olá importa um "Traga sua própria chave" pacote (BYOK). Isso permite que você gerar sua chave em seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

Para obter mais instruções sobre como toogenerate esse pacote BYOK, consulte [como toouse HSM-Protected chaves com Cofre de chaves do Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Excluir o Cofre de chaves hello e chaves associadas e segredos
Se você não precisar mais Cofre de chaves hello e chave de saudação ou segredo que ele contém, você pode excluir o Cofre de chaves hello usando o comando de exclusão de keyvault de saudação do azure:

    azure keyvault delete --vault-name 'ContosoKeyVault'

Ou, você pode excluir um grupo de recursos do Azure inteiro, que inclui o Cofre de chaves de saudação e outros recursos incluídos no grupo:

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Outros comandos da interface de linha de comando de plataforma cruzada do Azure
Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.

Este comando lista uma exibição em tabela de todas as chaves e propriedades selecionadas:

    azure keyvault key list --vault-name 'ContosoKeyVault'

Este comando exibe uma lista completa das propriedades de chave especificado hello:

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas:

    azure keyvault secret list --vault-name 'ContosoKeyVault'

Aqui está um exemplo de como tooremove uma chave específica:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Aqui está um exemplo de como tooremove um segredo específico:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>Próximas etapas
Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).

