---
title: Cofre de chave do Azure usando a CLI do aaaManage | Microsoft Docs
description: "Use este tutorial tooautomate as tarefas comuns no cofre de chaves usando Olá 2.0 do CLI"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>Gerenciar o Key Vault usando a CLI 2.0
O Cofre da Chave do Azure está disponível na maioria das regiões. Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introdução
Use este tutorial toohelp você obter Introdução ao Azure Key Vault toocreate um contêiner protegido (um cofre) no Azure, toostore e gerenciar chaves de criptografia e segredos no Azure. Orienta você pelo processo de saudação do uso de Interface de linha de comando de plataforma cruzada do Azure toocreate um cofre que contém uma chave ou a senha que você pode usar com um aplicativo do Azure. Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.

**Estimado tempo toocomplete:** 20 minutos

> [!NOTE]
> Este tutorial não inclui instruções sobre como toowrite Olá aplicativo do Azure que uma das etapas de saudação inclui, que mostra como tooauthorize toouse um aplicativo uma chave ou segredo na chave Olá cofre.
>
> Este tutorial usa Olá 2.0 mais recentes de CLI do Azure.
>
>

Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você deve ter Olá a seguir:

* TooMicrosoft uma assinatura do Azure. Se não tiver uma assinatura, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial).
* Interface de Linha de Comando versão 2.0 ou posterior. tooinstall Olá a versão mais recente e conecte-se tooyour assinatura do Azure, consulte [instalar e configurar Olá 2.0 de Interface de linha de comando de plataforma cruzada do Azure](/cli/azure/install-azure-cli).
* Um aplicativo que será a chave de saudação toouse configurado ou a senha criados por você neste tutorial. Um aplicativo de exemplo está disponível no hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Para obter instruções, consulte Olá que acompanha o arquivo Leiame.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Obtendo ajuda com a interface de linha de comando de plataforma cruzada do Azure
Este tutorial presume que você esteja familiarizado com a interface de linha de comando da saudação (Bash, Terminal, prompt de comando)

Hello – ajuda -h parâmetro ou pode ser usado tooview ajuda para comandos específicos. Como alternativa, hello azure help [comando] [Opções] formato também pode ser usado tooreturn Olá mesmas informações. Por exemplo, a seguir Olá comandos retornam todas as mesmas informações de hello:

```
az account set --help
az account set -h
```

Em caso de dúvida sobre parâmetros Olá necessários por um comando, consulte usando toohelp – ajuda, -h ou az help [comando].

Você também pode ler Olá tutoriais tooget familiarizado com o Azure Resource Manager na Interface de linha de comando de plataforma cruzada do Azure a seguir:

* [Instalar a CLI do Azure.](/cli/azure/install-azure-cli)
* [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Conecte-se tooyour assinaturas
toolog usando uma conta organizacional, use Olá comando a seguir:

```
az login -u username@domain.com -p password
```

ou se você quiser toolog no digitando interativamente

```
az login
```

Se você tiver várias assinaturas e desejar toospecify um um toouse específico para o Cofre de chaves do Azure, digite Olá assinaturas de saudação toosee para sua conta a seguir:

```
az account list
```

Toouse de assinatura do hello de toospecify, em seguida,, tipo:

```
az account set --subscription <subscription name or ID>
```

Para obter mais informações sobre como configurar a Interface de Linha de Comando de plataforma cruzada do Azure, consulte [Instalar a CLI do Azure](/cli/azure/install-azure-cli).

## <a name="create-a-new-resource-group"></a>Criar um novo grupo de recursos
Ao usar o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados em um grupo de recursos. Criaremos um novo grupo de recursos “ContosoResourceGroup” para este tutorial.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

Olá primeiro parâmetro é o nome do grupo de recursos e Olá segundo parâmetro é o local de saudação. Para local, use o comando Olá `az account list-locations` tooidentify como toospecify toohello um local alternativo uma neste exemplo. Se precisar de mais informações, digite: `az account list-locations -h`.

## <a name="register-hello-key-vault-resource-provider"></a>Registrar o provedor de recursos do Cofre de chaves Olá
Verifique se o provedor de recursos do Cofre de Chaves está registrado em sua assinatura:

```
az provider register -n Microsoft.KeyVault
```

Isso só precisa toobe feito uma vez por assinatura.

## <a name="create-a-key-vault"></a>Criar um cofre de chave
Saudação de uso `az keyvault create` comando toocreate um cofre de chaves. Esse script tem três parâmetros obrigatórios: um nome de grupo de recursos, um nome de Cofre de chaves e localização geográfica hello.

Por exemplo, se você usar o nome do cofre Olá de ContosoKeyVault, nome do grupo de recursos de saudação do ContosoResourceGroup e o local de saudação do Leste Asiático, digite:
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

saída de Hello desse comando mostra as propriedades do Cofre de chaves de saudação que você acabou de criar. Olá duas propriedades de mais importantes são:

* **nome**: no exemplo hello, isso é ContosoKeyVault. Você usará esse nome para outros comandos do Key Vault.
* **vaultUri**: no exemplo hello, isso é https://contosokeyvault.vault.azure.net. Aplicativos que usam seu cofre via API REST devem usar esse URI.

Sua conta do Azure é agora tooperform autorizado todas as operações nesta chave de cofre. Até o momento, ninguém mais está.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Adicionar uma chave ou segredo toohello Cofre de chaves
Se você quiser Azure Key Vault toocreate uma chave protegida por software para você, use Olá `az key create` de comando e digite Olá a seguir:
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
No entanto, se você tiver uma chave existente em um arquivo. PEM salvo como arquivo local em um arquivo chamado softkey.pem que você deseja tooupload tooAzure Cofre de chaves, digite Olá seguir tooimport chave de saudação de saudação. Arquivo PEM, que protege a chave de saudação pelo software no hello serviço de Cofre de chaves:
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
Agora você pode referenciar chave Olá que foi criada ou carregada tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obter a versão atual do hello e usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget essa versão específica.

tooadd um cofre toohello secreta, que é uma senha chamada SQLPassword e que tem o valor de saudação do Pa$ $w0rd tooAzure Cofre de chaves, Olá tipo a seguir:
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
Agora você pode referenciar essa senha que você adicionou tooAzure Cofre de chaves, usando seu URI. Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obter a versão atual do hello e usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget essa versão específica.

Vejamos chave hello ou chave secreta que você acabou de criar:

* tooview sua chave, tipo:`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview seu segredo, tipo:`az keyvault secret list --vault-name 'ContosoKeyVault'`

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
2. Olá esquerda, clique em **Active Directory do Azure**e, em seguida, selecione o diretório de saudação na qual você registrará o seu aplicativo. <br> <br> 

> [!Note] 
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
tooauthorize Olá aplicativo tooaccess Olá chave ou segredo no cofre hello, use Olá `az keyvault set-policy` comando.

Por exemplo, se o nome do cofre for ContosoKeyVault e hello aplicativo deseja tooauthorize tem uma ID de cliente de 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você deseja tooauthorize Olá aplicativo toodecrypt e entre com as chaves em seu cofre, execute Olá a seguir:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

Se você quiser tooauthorize esse mesmo segredos de tooread do aplicativo em seu cofre, execute o seguinte de saudação:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Se você quiser toouse um módulo de segurança de hardware (HSM)
Para garantia extra, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello. Olá HSMs são FIPS 140-2 nível 2 validado. Se esse requisito não se aplica a tooyou, ignore esta seção e vá muito[excluir Cofre de chaves hello e chaves associadas e segredos](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate essas chaves protegidas por HSM, você deve ter uma assinatura do cofre que dá suporte a chaves protegidas por HSM.

Quando você cria keyvault Olá, adicione um parâmetro de 'sku' hello:

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e o Cofre de chaves protegidas por HSM toothis. toocreate uma chave protegida por HSM, too'HSM de parâmetro de destino do conjunto de saudação ':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

Você pode usar o hello após o comando tooimport uma chave de um arquivo. PEM em seu computador. Este comando importa chave Olá para HSMs em Olá serviço de Cofre de chaves:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
comando Avançar Olá importa um "Traga sua própria chave" pacote (BYOK). Isso permite que você gerar sua chave em seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
Para obter mais instruções sobre como toogenerate esse pacote BYOK, consulte [como toouse HSM-Protected chaves com Cofre de chaves do Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Excluir o Cofre de chaves hello e chaves associadas e segredos
Se você não precisar mais Cofre de chaves hello e chave de saudação ou segredo que ele contém, você pode excluir o Cofre de chaves hello usando Olá `az keyvault delete` comando:

```
az keyvault delete --name 'ContosoKeyVault'
```

Ou, você pode excluir um grupo de recursos do Azure inteiro, que inclui o Cofre de chaves de saudação e outros recursos incluídos no grupo:

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Outros comandos da interface de linha de comando de plataforma cruzada do Azure
Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.

Este comando lista uma exibição em tabela de todas as chaves e propriedades selecionadas:

az keyvault key list --vault-name 'ContosoKeyVault'

Este comando exibe uma lista completa das propriedades de chave especificado hello:

az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas:

az keyvault secret list --vault-name 'ContosoKeyVault'

Aqui está um exemplo de como tooremove uma chave específica:

az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Aqui está um exemplo de como tooremove um segredo específico:

az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'


## <a name="next-steps"></a>Próximas etapas
Para obter a referência completa da CLI do Azure de comandos do cofre de chaves, consulte [referência da CLI do Key Vault](/cli/azure/keyvault)

Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).
