---
title: "aaaLocal tooAzure de implantação do Git do serviço de aplicativo"
description: "Saiba como tooenable local Git implantação tooAzure do serviço de aplicativo."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>TooAzure local de implantação do Git do serviço de aplicativo
Este tutorial mostra como toodeploy seu aplicativo muito[do serviço de aplicativo do Azure] de um repositório Git no computador local. Serviço de aplicativo oferece suporte a essa abordagem com hello **Git Local** opção de implantação no hello [Portal do Azure].  
Muitos dos comandos do Git Olá descritos neste artigo são executados automaticamente durante a criação de um aplicativo de serviço de aplicativo usando Olá [Interface de linha de comando do Azure] conforme descrito [aqui](app-service-web-get-started.md).

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa:

* Git. Você pode fazer o download de binários de instalação Olá [aqui](http://www.git-scm.com/downloads).  
* Conhecimento básico do Git.
* Uma conta do Microsoft Azure. Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo de início de curta duração no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.  
> 
> 

## <a name="Step1"></a>Etapa 1: Criar um repositório local
Execute Olá tarefas toocreate um novo repositório Git a seguir.

1. Inicie uma ferramenta da linha de comando, como **GitBash** (Windows) ou **Bash** (Unix Shell). Em sistemas de OS X, você pode acessar Olá de linha de comando por meio de saudação **Terminal** aplicativo.
2. Navegue toohello diretório onde Olá toodeploy de conteúdo seja localizado.
3. Use Olá comando tooinitialize um novo repositório Git a seguir:

```bash  
git init
```

## <a name="Step2"></a>Etapa 2: Confirmar seu conteúdo
O Serviço de Aplicativo dá suporte a aplicativos criados em uma variedade de linguagens de programação. 

1. Se o repositório já inclui conteúdo ignorar esse ponto e move toopoint 2 abaixo. Se seu repositório ainda não inclui conteúdo, simplesmente popule-o com um arquivo .html estático da seguinte maneira: 
   
   * Usando um editor de texto, crie um novo arquivo denominado **index** na raiz de saudação do repositório do Git Olá
   * Adicionar Olá depois do texto como conteúdo Olá Olá index de arquivo e salve-o: *Git Olá!*
2. De saudação de linha de comando, verifique se que você está na raiz de saudação do repositório Git. Em seguida, use Olá repositório tooyour do comando tooadd arquivos a seguir:

```bash  
git add -A
```
3. Em seguida, confirmação Olá alterações toohello repositório usando Olá comando a seguir:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Etapa 3: Habilitar Olá repositório de aplicativo de serviço de aplicativo
Execute Olá seguindo as etapas tooenable um repositório Git para seu aplicativo de serviço de aplicativo.

1. Faça logon no toohello [Portal do Azure].
2. Na folha do seu aplicativo do Serviço de Aplicativo, clique em **Configurações > Origem da implantação**. Clique em **Escolher fonte**, em seguida, clique em **Repositório Git Local** e clique em **OK**.  
   
    ![Repositório Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. Se esse for o primeiro tempo configurando um repositório no Azure, você precisa ter credenciais de logon toocreate para ele. Você usará-los toolog em Olá repositório do Azure e por push as alterações no seu repositório Git local. Na folha do aplicativo, clique em **Configurações > Credenciais da implantação**, em seguida, configure o nome de usuário da implantação e a senha. Quando terminar, clique em **Salvar**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Etapa 4: Implantar seu projeto
Use Olá seguindo as etapas toopublish tooApp seu aplicativo usando o Git Local do serviço.

1. Na folha do seu aplicativo em Olá Portal do Azure, clique em **Configurações > propriedades** para Olá **URL do Git**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **URL de Git** é Olá referência remota toodeploy toofrom seu repositório local. Você usará esta URL no hello etapas a seguir.
2. Usando Olá de linha de comando, verifique se você está na raiz de saudação do seu repositório Git local.
3. Use `git remote` referência remota de saudação tooadd listada na **URL de Git** da etapa 1. O comando terá aparência a seguir toohello semelhante:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Olá **remoto** comando adiciona um repositório remoto de tooa Referência nomeada. Neste exemplo, ele cria uma referência chamada ‘azure’ para o repositório do aplicativo Web.
   > 
   > 
4. Enviar por push o serviço de tooApp conteúdo usando Olá novo **azure** remoto você acabou de criar.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Volte tooyour aplicativo hello Portal do Azure. Uma entrada de log de seu envio mais recente deve ser exibida em Olá **implantações** folha. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Clique em Olá **procurar** botão na parte superior de saudação do conteúdo de saudação de tooverify de folha à saudação do aplicativo foi implantado. 

## <a name="Step5"></a>Solucionar problemas
Olá seguem erros ou problemas comumente encontrados ao usar o Git toopublish tooan aplicativo de serviço de aplicativo no Azure:

- - -
**Sintoma**: não é possível tooaccess '[siteURL]': falha tooconnect muito [scmAddress]

**Causa**: este erro pode ocorrer se o aplicativo hello não está em execução.

**Resolução**: Iniciar aplicativo Olá Olá Portal do Azure. Implantação do Git não funcionará a menos que o aplicativo hello está sendo executado. 

- - -
**Sintoma**: não foi possível resolver o nome de host 'host'

**Causa**: este erro pode ocorrer se as informações de endereço de saudação inserido durante a criação de saudação 'azure' remoto estava incorreta.

**Resolução**: Olá Use `git remote -v` comando toolist todos os remotos, juntamente com a URL de saudação associada. Verifique se a URL Olá Olá 'azure' remoto está correto. Se necessário, remova e recrie nesse remoto usando a URL correta do hello.

- - -
**Sintoma**: não há referências em comum e nenhuma especificada; nada é feito. Talvez você deva especificar uma ramificação como 'mestre'.

**Causa**: este erro pode ocorrer se você não especificar uma ramificação ao executar uma operação de envio por push do git e ter não Olá push.default valor fixo usado pelo Git.

**Resolução**: executar a operação de envio de saudação novamente, especificando a ramificação mestre hello. Por exemplo:

```bash  
git push azure master
```
- - -
**Sintoma**: src refspec [branchname] não corresponde a nada.

**Causa**: este erro pode ocorrer se você tentar toopush tooa filial que não seja o mestre de saudação 'azure' remoto.

**Resolução**: executar a operação de envio de saudação novamente, especificando a ramificação mestre hello. Por exemplo:

```bash  
git push azure master
```
- - -
**Sintoma**: falha de RPC; resultado = 22, código HTTP = 502.

**Causa**: este erro pode ocorrer se você tentar toopush um repositório git grande via HTTPS.

**Resolução**: alteração da configuração do git Olá em postBuffer toomake de saudação do computador local Olá maior

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Sintoma**: erro - o repositório de tooremote confirmada alterações mas seu aplicativo web não está atualizado.

**Causa**: esse erro poderá ocorrer se você estiver implantando um aplicativo do Node.js que contém um arquivo package.json que especifica os módulos adicionais necessários.

**Resolução**: as mensagens adicionais contendo 'npm ERR!' deve ser conectado toothis anterior erro e pode fornecer um contexto adicional em caso de falha de saudação. a seguir Olá é conhecida causas desse erro e Olá correspondente 'npm ERR!' mensagem:

* **Arquivo malformado package.json**: npm ERR! Não foi possível ler as dependências.
* **Um módulo nativo que não tenha uma distribuição binária para o Windows**:
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` falhou com 1
    
      OU
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>Recursos adicionais
* [Documentação do Git](http://git-scm.com/documentation)
* [Documentação do projeto Kudu](https://github.com/projectkudu/kudu/wiki)
* [TooAzure implantação contínua do serviço de aplicativo](app-service-continuous-deployment.md)
* [Como toouse PowerShell do Azure](/powershell/azure/overview)
* [Como toouse Olá Interface de linha de comando do Azure](../cli-install-nodejs.md)

[do serviço de aplicativo do Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Portal do Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Interface de linha de comando do Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
