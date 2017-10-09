---
title: cluster de aaaSubmit trabalhos tooan HPC Pack no Azure | Microsoft Docs
description: Saiba como tooset a um toosubmit do computador local trabalhos tooan cluster de HPC Pack no Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Enviar trabalhos HPC de um cluster de HPC Pack local computador tooan implantado no Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Configurar um local cliente computador toosubmit trabalhos tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster no Azure. Este artigo mostra como tooset um computador local com o cliente ferramentas toosubmit trabalho sobre cluster de toohello HTTPS no Azure. Dessa forma, vários usuários do cluster podem enviar trabalhos tooa baseado em nuvem cluster de HPC Pack, mas sem se conectar diretamente toohello VM do nó principal ou acessar uma assinatura do Azure.

![Enviar um cluster de tooa de trabalho no Azure][jobsubmit]

## <a name="prerequisites"></a>Pré-requisitos
* **Nó principal do HPC Pack implantado em uma VM do Azure** -é recomendável que você use ferramentas automatizadas, como um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) ou um [script do PowerShell do Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nó principal do toodeploy hello e cluster. Você precisa nome DNS de saudação do nó principal hello e credenciais de saudação de um administrador de cluster para concluir as etapas neste artigo hello.
* **Computador cliente** – você precisa de um computador Windows Client ou Windows Server que possa executar utilitários de cliente do Pacote HPC (consulte os [requisitos do sistema](https://technet.microsoft.com/library/dn535781.aspx)). Se você desejar somente toouse Olá HPC Pack portal web ou trabalhos de toosubmit da API REST, você pode usar qualquer computador cliente de sua escolha.
* **Mídia de instalação HPC Pack** -tooinstall Olá utilitários de cliente do HPC Pack, o pacote de instalação gratuita Olá para a versão mais recente do HPC Pack (HPC Pack 2012 R2) está disponível a partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Certifique-se de que você baixe Olá mesma versão do HPC Pack está instalado na VM do nó principal hello.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>Etapa 1: Instalar e configurar os componentes da web hello no nó de cabeçalho Olá
tooenable um cluster REST interface toosubmit trabalhos toohello via HTTPS, verifique se os componentes de web do HPC Pack Olá estão configurados no nó principal do HPC Pack hello. Se ainda não estiverem instalados, primeiro instale os componentes da web hello executando o arquivo de instalação HpcWebComponents.msi hello. Em seguida, configure componentes Olá executando o script do HPC PowerShell Olá **Set-hpcwebcomponents.ps1**.

Para obter procedimentos detalhados, consulte [instalar componentes da Web do hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).

> [!TIP]
> Alguns modelos de início rápido do Azure para o HPC Pack instalar e configurar os componentes da web hello automaticamente. Se você usar o hello [script de implantação IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate cluster do hello, opcionalmente, você pode instalar e configurar os componentes da web hello como parte da implantação de saudação.
> 
> 

**componentes da web do tooinstall Olá**

1. Conecte-se toohello VM do nó principal usando credenciais de saudação de um administrador de cluster.
2. Na pasta de instalação do HPC Pack hello, execute HpcWebComponents.msi no nó principal hello.
3. Siga as etapas de Olá Olá Assistente tooinstall Olá web de componentes

**componentes da web do tooconfigure Olá**

1. No nó de cabeçalho hello, inicie o HPC PowerShell como administrador.
2. local de toohello toochange diretório saudação do script de configuração, Olá tipo comando a seguir:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure Olá interface REST e iniciar Olá serviço Web do HPC, Olá tipo comando a seguir:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. Quando solicitada tooselect um certificado, escolha o certificado de saudação correspondente toohello nome DNS público do nó principal hello. Por exemplo, se você implantar o nó principal do hello VM usando o modelo de implantação clássico Olá, nome do certificado Olá aparência CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net. Se você usar o modelo de implantação do Gerenciador de recursos de Olá, nome do certificado Olá aparência CN =&lt;*HeadNodeDnsName*&gt;.&lt; *região*&gt;. cloudapp.azure.com.
   
   > [!NOTE]
   > Selecione este certificado mais tarde quando você envia o nó principal do toohello de trabalhos de um computador local. Não selecione nem configure um certificado que corresponde a toohello o nome do computador do nó principal do hello no domínio do Active Directory hello (por exemplo, CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. portal de web tooconfigure Olá para envio de trabalho, Olá tipo comando a seguir:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Após a conclusão do script hello, pare e reinicie o hello serviço de Agendador de trabalho do HPC digitando Olá comandos a seguir:
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>Etapa 2: Instalar utilitários de cliente Olá HPC Pack em um computador local
Se você quiser utilitários de cliente tooinstall Olá HPC Pack em seu computador, baixe os arquivos de instalação HPC Pack (instalação completa) de saudação [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024). Quando você começar a instalação hello, escolha a opção de instalação de saudação para Olá **utilitários de cliente do HPC Pack**.

ferramentas de cliente de HPC Pack Olá toouse toosubmit trabalhos toohello VM do nó principal, você também precisa tooexport um certificado de nó principal hello e instalá-lo no computador do cliente de saudação. Olá certificado deve ser no. Formato CER.

**certificado de saudação tooexport do nó principal Olá**

1. No nó de cabeçalho hello, adicione Olá certificados snap-in tooa Console de gerenciamento Microsoft para Olá conta do computador Local. Para obter etapas tooadd Olá snap-in, consulte [adicionar Olá Snap-in Certificados tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).
2. Na árvore de console hello, expanda **certificados – computador Local** > **pessoal**e, em seguida, clique em **certificados**.
3. Localize Olá certificado que você configurou para web components Olá HPC Pack em [etapa 1: instalar e configurar os componentes da web hello no nó de cabeçalho de saudação](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por exemplo, CN =&lt;*HeadNodeDnsName* &gt;. >.cloudapp.NET).
4. Clique com botão direito certificado hello e, em seguida, clique em **todas as tarefas** > **exportar**.
5. No hello Assistente para exportação de certificado, clique em **próximo**e certifique-se de que **não exportar chave privada Olá** está selecionado.
6. Olá siga restantes etapas de saudação Assistente tooexport Olá certificado DER codificada x. 509 binário (. Formato CER).

**certificado de saudação tooimport no computador do cliente Olá**

1. Copie o certificado de saudação que você exportou da pasta de tooa Olá nó principal no computador do cliente de saudação.
2. No computador do cliente Olá, execute certmgr.msc.
3. No Gerenciador de Certificados, expanda **Certificados – Usuário atual** > **Autoridades de Certificação Confiáveis**, clique com o botão direito do mouse em **Certificados** e clique em **Todas as Tarefas** > **Importar**.
4. No hello Assistente de importação de certificado, clique em **próximo** e siga Olá etapas tooimport Olá certificado que você exportou da saudação nó principal toohello repositório de autoridades de certificação raiz confiáveis.

> [!TIP]
> Você pode ver um aviso de segurança, porque a autoridade de certificação Olá no nó de cabeçalho Olá não é reconhecida pelo computador cliente de saudação. Para fins de teste, você pode ignorar este aviso e concluir importação do certificado hello.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>Etapa 3: Executar trabalhos de teste no cluster Olá
tooverify sua configuração, tente trabalhos em execução saudação do cluster no Azure de saudação local do computador. Por exemplo, você pode usar ferramentas de GUI do HPC Pack ou cluster de toohello comandos de linha de comando toosubmit trabalhos. Você também pode usar um trabalhos toosubmit portal baseado na web.

**comandos de envio de trabalho toorun no computador do cliente Olá**

1. Em um computador cliente onde os utilitários de cliente do HPC Pack Olá estão instalados, inicie um Prompt de comando.
2. Digite um comando de exemplo. Por exemplo, toolist todos os trabalhos no cluster hello, digite um tooone semelhante do comando de hello a seguir, dependendo do nome DNS completo de saudação do nó principal hello:
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    ou o
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Use o nome DNS completo de saudação do nó principal hello, não endereços IP hello, Olá Agendador URL. Se você especificar o endereço IP hello, um erro semelhante também aparecerá "certificado do servidor de saudação precisa tooeither têm uma cadeia válida de confiança ou toobe colocado no repositório de raiz confiável do hello."
   > 
   > 
3. Quando solicitado, digite o nome de usuário da saudação (na forma de saudação &lt;DomainName&gt;\\&lt;UserName&gt;) e a senha de administrador de cluster HPC hello ou outro usuário do cluster que você configurou. Você pode escolher toostore credenciais Olá localmente para mais operações de trabalho.
   
    Uma lista de trabalhos é exibida.

**toouse Gerenciador de trabalhos HPC no computador do cliente Olá**

1. Se anteriormente você não armazenar credenciais de domínio para um usuário de cluster durante o envio de um trabalho, você pode adicionar credenciais Olá no Gerenciador de credenciais.
   
    a. No painel de controle no computador do cliente hello, inicie o Gerenciador de credenciais.
   
    b. Clique nas **Credenciais do Windows** > **Adicionar uma credencial genérica**.
   
    c. Especifique o endereço de Internet da saudação (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt; região&gt;.cloudapp.azure.com/HpcScheduler) e o nome de usuário da saudação (&lt;DomainName&gt;\\&lt;UserName&gt;) e a senha de administrador de cluster hello ou outro usuário de cluster que você configurou.
2. No computador do cliente hello, inicie o Gerenciador de trabalho do HPC.
3. Em Olá **selecionar nó principal** caixa de diálogo, tipo hello URL toohello nó principal no Azure (por exemplo, https://&lt;HeadNodeDnsName&gt;. cloudapp.net ou https://&lt;HeadNodeDnsName&gt;. &lt;região&gt;. cloudapp.azure.com).
   
    Gerenciador de trabalhos HPC é aberto e mostra uma lista de trabalhos no nó de cabeçalho hello.

**portal de web hello toouse em execução no nó principal Olá**

1. Iniciar um navegador da web no computador do cliente hello e insira um Olá endereços, dependendo do nome DNS completo de saudação do nó principal Olá a seguir:
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    ou o
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Na Olá caixa de diálogo de segurança que aparece, digite credenciais de domínio de saudação do administrador de cluster HPC hello. (Você também pode adicionar outros usuários do cluster em funções diferentes. Consulte [Gerenciando Usuários de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)
   
    o portal da web Hello abre o modo de exibição de lista de trabalho toohello.
3. toosubmit um trabalho de exemplo que retorna a cadeia de caracteres de saudação "Olá, mundo" do cluster Olá, clique em **novo trabalho** na navegação esquerda hello.
4. Em Olá **novo trabalho** página em **das páginas de envio**, clique em **HelloWorld**. página de envio de trabalho Olá é exibida.
5. Clique em **Enviar**. Se solicitado, forneça credenciais de domínio de saudação do administrador de cluster HPC hello. Olá trabalho é enviado e ID do trabalho Olá aparece no hello **Meus trabalhos** página.
6. resultados de saudação do tooview de trabalho de saudação enviado, clique em ID do trabalho Olá e, em seguida, clique em **exibir tarefas** tooview saída do comando de saudação (em **saída**).

## <a name="next-steps"></a>Próximas etapas
* Você também pode enviar trabalhos toohello cluster do Azure com hello [API REST do HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).
* Se você quiser toosubmit trabalhos de cluster de um cliente Linux, consulte Olá Python exemplo no hello [SDK do HPC Pack 2012 R2 e o código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
