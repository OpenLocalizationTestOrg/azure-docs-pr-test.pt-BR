---
title: "aaaLog em tooAzure de saudação CLI | Microsoft Docs"
description: Conecte-se tooyour assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure) para Windows, Linux e Mac
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Faça logon no tooAzure de saudação CLI do Azure
Olá CLI do Azure é um conjunto de comandos de software livre, multiplataforma para trabalhar com recursos do Azure. Este artigo descreve Olá diferentes maneiras tooprovide tooyour da CLI do Azure seu Olá conta do Azure credenciais tooconnect assinatura do Azure:

* Executar Olá `azure login` CLI tooauthenticate de comando por meio do Active Directory do Azure. Isso proporciona método acessar comandos tooCLI no [comando modos](#cli-command-modes). Quando você executa o comando Olá sem opções adicionais, `azure login` solicitará que você toocontinue logon interativamente por meio de um portal da web. Para mais `azure login` opções de comando, consulte os cenários de saudação neste artigo ou tipo `azure login --help`.
* Se você precisar somente comandos da CLI toouse gerenciamento de serviços do Azure modo (não recomendados para implantações mais novas), você pode baixar e instalar um arquivo de configurações de publicação no seu computador.

Se você ainda não instalou Olá CLI, consulte [instalação Olá CLI do Azure](cli-install-nodejs.md). Se você não tiver uma assinatura do Azure, poderá criar uma [conta gratuita](http://azure.microsoft.com/free/) em apenas alguns minutos.

Para obter informações sobre identidades de outra conta e sobre as assinaturas do Azure, confira [Como as assinaturas do Azure como são associadas ao Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Cenário 1: logon do azure com logon interativo
Certas contas, Olá CLI requer toorun `azure login` e, em seguida, continuar o processo de logon de saudação com um navegador da web por meio de um portal da web, um processo chamado *logon interativo*. Uma razão comum é quando você tem uma conta corporativa ou escolar (também chamado de um *conta organizacional*) que é configurada toorequire a autenticação multifator. Use também o logon interativo com sua conta da Microsoft, quando você deseja toouse comandos de modo de Gerenciador de recursos.

Logon interativo é fácil: tipo `azure login` – sem opções – conforme mostrado no exemplo a seguir de saudação:

```
azure login
```                                                                                             

saída de Hello será algo parecido com hello seguinte:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Copiar código Olá oferecido tooyou na saída do comando hello e abrir um navegador toohttp://aka.ms/devicelogin ou outra página, se especificado. (Você pode abrir um navegador em Olá mesmo computador, ou em outro computador ou dispositivo.) Insira o código de saudação e, em seguida, você tooenter solicitadas Olá username e password para identidade Olá deseja toouse. Quando esse processo for concluído, o shell de comando Olá conclui o logon de saudação. Ele poderia ser semelhante ao seguinte:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> Com o logon interativo, a autenticação e a autorização são executadas com o Azure Active Directory. Se você usar uma identidade de conta da Microsoft, o processo de logon Olá acessa seu domínio do Active Directory do Azure padrão. (Se você se inscreveu para obter uma conta gratuita do Azure, o Azure Active Directory criou um domínio padrão para a sua conta).
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Cenário 2: logon do Azure com um nome de usuário e senha
Saudação de uso `azure login` com nome de usuário da saudação (`-u`) tooauthenticate parâmetro quando você quiser toouse um trabalho ou escola de conta que não exija a autenticação multifator. Você será solicitado na linha de comando Olá senha hello (ou, opcionalmente, você pode passar senha hello como um parâmetro adicional do hello `azure login` comando). Olá, exemplo a seguir passa Olá nome de usuário de uma conta organizacional:

    azure login -u myUserName@contoso.onmicrosoft.com

Você solicitado tooenter sua senha:

    info:    Executing command login
    Password: *********

conclui o processo de logon Hello.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Se esse for o primeiro log de tempo com essas credenciais, você deverá tooverify que você deseja toocache um token de autenticação. Esse aviso também ocorre se você tiver usado a saudação `azure logout` comando (descrito posteriormente no artigo Olá). toobypass esse prompt para cenários de automação, execute `azure login` com hello `-q` parâmetro.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Cenário 3: logon do Azure com uma entidade de serviço
Se você criar uma entidade de serviço para um aplicativo do Active Directory e entidade de serviço Olá tem permissões em sua assinatura, você pode usar o hello `azure login` entidade de serviço do comando tooauthenticate hello. Dependendo do cenário, você pode fornecer credenciais de saudação da entidade de serviço hello como parâmetros explícitos de saudação `azure login` comando. Por exemplo, hello comando a seguir passa nome principal do serviço hello e ID de locatário do Active Directory:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Você forem solicitada tooprovide Olá senha. Você também pode fornecer credenciais de saudação por meio de um código de script ou aplicativo CLI ou usar uma entidade de serviço do certificado tooauthenticate Olá não interativamente para cenários de automação. Para obter detalhes e exemplos, confira [Autenticando uma entidade de serviço com o Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Cenário 4: usar um arquivo de configurações de publicação
Se você precisar somente comandos da CLI de modo toouse Olá gerenciamento de serviços do Azure (por exemplo, toodeploy VMs do Azure no modelo de implantação clássico Olá), você pode se conectar usando um arquivo de configurações de publicação. Este método instala um certificado no computador local que permite que você tooperform tarefas de gerenciamento para como assinatura hello e certificado Olá são válidos.

* **Olá toodownload Publicar arquivo de configurações** para sua conta, certifique-se de que Olá CLI está no modo de gerenciamento de serviços, digitando `azure config mode asm`. Em seguida, execute Olá comando a seguir:

        azure account download

Isso abre o navegador padrão e solicita que você toosign em toohello [portal clássico do Azure](https://manage.windowsazure.com). Depois de entrar, um arquivo `.publishsettings` é baixado. Anote onde esse arquivo está salvo.

> [!NOTE]
> Se sua conta estiver associada a vários locatários do Active Directory do Azure, você pode ser solicitado tooselect que o Active Directory que você deseja toodownload as configurações de publicação do arquivo para.
>
>

Uma vez selecionado usando a página de download do hello, ou visitando Olá portal clássico do Azure, hello selecionado do Active Directory torna-se saudação padrão usado pelo portal clássico do hello e página de download. Após o estabelecimento de um padrão, consulte o texto de saudação '**clique aqui a página de seleção de toohello tooreturn**' na parte superior de saudação da página de download de saudação. Use Olá fornecido a página de seleção do link tooreturn toohello.

* **Olá tooimport Publicar arquivo de configurações**, execute hello seguinte comando:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> Depois de importar suas configurações de publicação, você deve excluir Olá `.publishsettings` arquivo. Ele não é exigido pela Olá CLI do Azure e apresenta um risco de segurança que pode ser usado toogain acesso tooyour assinatura.
>
>

## <a name="cli-command-modes"></a>Modos de comando da CLI
Olá CLI do Azure oferece dois modos de comando para trabalhar com recursos do Azure, com vários conjuntos de comandos:

* **Modo do Gerenciador de recursos** - para trabalhar com recursos do Azure no modelo de implantação do Gerenciador de recursos de saudação. tooset nesse modo, execute `azure config mode arm`.
* **Modo de gerenciamento de serviço** - para trabalhar com recursos do Azure no modelo de implantação clássico hello. tooset nesse modo, execute `azure config mode asm`.

Quando instalado pela primeira vez, Olá versão atual do hello que CLI está no modo do Gerenciador de recursos.

> [!NOTE]
> modo do Gerenciador de recursos de saudação e modo de gerenciamento de serviço são mutuamente exclusivos. Ou seja, os recursos criados no modo não podem ser gerenciados de saudação outro modo.
>
>

## <a name="multiple-subscriptions"></a>Várias assinaturas
Se você tiver várias assinaturas do Azure, conectar-se tooAzure concede acesso tooall assinaturas associadas com suas credenciais. Uma assinatura é selecionada como padrão hello e usada por Olá CLI do Azure ao executar operações. Você pode exibir assinaturas hello, incluindo assinatura padrão hello, usando Olá `azure account list` comando. Esse comando retorna a seguir toohello semelhante informações:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

Em Olá anterior da lista, Olá **atual** coluna indica Olá atual padrão assinatura do Azure-sub-1. assinatura padrão do hello toochange, use Olá `azure account set` de comando e especifique que você deseja que o padrão de saudação toobe de assinatura de saudação. Por exemplo:

    azure account set Azure-sub-2

Isso altera o saudação padrão assinatura tooAzure-sub-2.

> [!NOTE]
> Alterando saudação padrão assinatura entra em vigor imediatamente e é uma alteração global; novos comandos de CLI do Azure, se você executá-los de Olá mesma instância de linha de comando ou uma instância diferente, use Olá nova assinatura de padrão.
>
>

Se você quiser toouse uma assinatura diferente do padrão com hello CLI do Azure, mas não quiser padrão atual do toochange hello, você pode usar o hello `--subscription` opção comando hello e forneça o nome de saudação de assinatura Olá desejar toouse para operação de saudação.

Quando você estiver conectado tooyour assinatura do Azure, começar a usar o hello toowork de comandos de CLI do Azure com recursos do Azure.

## <a name="storage-of-cli-settings"></a>Armazenamento de configurações da CLI
Se você fazer logon com hello `azure login` comando ou importar configurações de publicação, o perfil CLI e os logs são armazenados em um `.azure` diretório localizado no seu `user` directory. O diretório `user` está protegido pelo seu sistema operacional. No entanto, recomendamos que você execute etapas adicionais tooencrypt seu `user` directory. Você pode fazer isso no hello maneiras a seguir:

* No Windows, modificar propriedades de diretório hello ou usar o BitLocker.
* No Mac, ative o FileVault para diretório de saudação.
* No Ubuntu, use o recurso de diretório de Home criptografado de saudação. Outras distribuições do Linux oferecem recursos semelhantes.

## <a name="logging-out"></a>Fazendo logout
toolog out Olá use comandos a seguir:

    azure logout -u <username>

Se assinaturas Olá associado conta Olá somente são autenticados com o Active Directory, o logout exclui informações de assinatura de saudação do perfil local hello. No entanto, se um arquivo de configurações de publicação também foi importado para assinaturas de hello, logoff somente informações do perfil local Olá relacionadas à exclusões do Active Directory.

## <a name="next-steps"></a>Próximas etapas
* toouse comandos de CLI do Azure, consulte [comandos de CLI do Azure no Gerenciador de recursos de modo](virtual-machines/azure-cli-arm-commands.md) e [comandos de CLI do Azure no modo de gerenciamento de serviço](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn mais sobre Olá CLI do Azure, baixar o código-fonte, relatar problemas, ou contribuir toohello projeto, visite Olá [repositório GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).
* Se você tiver problemas ao usar o hello CLI do Azure ou o Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
