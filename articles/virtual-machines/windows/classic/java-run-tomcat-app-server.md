---
title: "servidor de aplicativos Java aaaRun em uma VM clássico do Azure | Microsoft Docs"
description: "Este tutorial usa recursos criados com o modelo de implantação clássico hello e mostra como toocreate um Virtual do Windows do computador e configure-o servidor de aplicativos do Apache Tomcat toorun."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Como toorun um servidor de aplicativos Java em uma máquina virtual criada com o modelo de implantação clássico Olá
> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Para um modelo de Gerenciador de recursos toodeploy um aplicativo Web com o Java 8 e do Tomcat, consulte [aqui](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

Com o Azure, você pode usar os recursos de servidor de tooprovide uma máquina virtual. Por exemplo, uma máquina virtual em execução no Azure pode ser configurado toohost um servidor de aplicativos Java, como o Apache Tomcat.

Depois de concluir este guia, você terá uma compreensão de como toocreate uma máquina virtual em execução no Azure e configurá-lo toorun um servidor de aplicativos Java. Você saiba e executar Olá tarefas a seguir:

* Como toocreate uma máquina virtual do computador que tem um Java Development Kit (JDK) já está instalado.
* Como tooremotely entrar na máquina virtual de tooyour.
* Como tooinstall um servidor de aplicativos Java – Apache Tomcat - em sua máquina virtual.
* Como toocreate um ponto de extremidade para sua máquina virtual.
* Como tooopen uma porta no hello de firewall para o servidor de aplicativos.

Olá concluída resultados da instalação no Tomcat em execução em uma máquina virtual.

![Máquina virtual executando o Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate uma máquina virtual
1. Entrar toohello [portal do Azure](https://portal.azure.com).  
2. Clique em **novo**, clique em **de computação**, em seguida, clique em **ver todos os** em Olá **aplicativos em destaque**.
3. Clique em **JDK**, clique em **JDK 8** em Olá **JDK** painel.  
   Imagens de máquina virtual que dão suporte a **JDK 6** e **JDK 7** estão disponíveis se você tiver aplicativos herdados que não estão pronto toorun JDK 8.
4. No painel de saudação JDK 8 Selecione **clássico**, em seguida, clique em **criar**.
5. Em Olá **Noções básicas sobre** folha:
   1. Especifique um nome para a máquina virtual de saudação.
   2. Insira um nome para o administrador de saudação em Olá **nome de usuário** campo. Lembre-se esse nome e Olá senha associada que segue no campo próximo hello. Você precisa-os quando entram remotamente na máquina virtual de toohello.
   3. Digite uma senha na Olá **nova senha** campo e digite-a novamente no hello **Confirmar senha** campo. Essa senha é para Olá conta de administrador.
   4. Selecione Olá apropriado **assinatura**.
   5. Para Olá **grupo de recursos**, clique em **criar novo** e insira o nome de saudação do novo grupo de recursos. Ou, clique em **usar existente** e selecione um dos grupos de recursos disponíveis de saudação.
   6. Selecione um local onde Olá máquina de virtual reside, como **Centro Sul dos EUA**.
6. Clique em **Avançar**.
7. Em Olá **tamanho da imagem de máquina Virtual** folha, selecione **A1 padrão** ou outra imagem apropriada.
8. Clique em **Selecionar**.

9. Em Olá **configurações** folha, clique em **Okey**. Você pode usar valores padrão de saudação fornecidos pelo Azure.  
10. Em Olá **resumo** folha, clique em **Okey**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely logon na máquina virtual de tooyour
1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Máquinas virtuais (clássicas)**. Se necessário, clique em **mais serviços** em Olá inferior esquerda em categorias de serviço hello. Olá **máquinas virtuais (clássicas)** entrada será listada em Olá **de computação** grupo.
3. Clique Olá nome da máquina virtual Olá que você deseja toosign no.
4. Após a inicialização da máquina virtual hello, um menu na parte superior de saudação do painel Olá permite conexões.
5. Clique em **Conectar**.
6. Responda toohello prompts como máquina de virtual toohello tooconnect necessários. Normalmente, você salva ou abre arquivo. rdp Olá que contém os detalhes de conexão de saudação. Você pode ter toocopy Olá url: porta como a última parte Olá da primeira linha de saudação do arquivo. rdp de saudação e cole-o em um aplicativo de logon remoto.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall um servidor de aplicativos Java em sua máquina virtual
Você pode copiar uma máquina virtual do Java application server tooyour, ou você pode instalar um servidor de aplicativos Java por meio de um instalador.

Este tutorial usa Tomcat como Olá Java application server tooinstall.

1. Quando você está conectado na máquina virtual de tooyour, abra uma sessão do navegador muito[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Clique duas vezes no link Olá para **instalador de serviço do Windows de 32 bits/64 bits**. Ao usar essa técnica, o Tomcat é instalado como um serviço Windows.
3. Quando solicitado, escolha o instalador de saudação toorun.
4. Dentro de saudação **Apache Tomcat instalação** assistente, siga Olá solicita tooinstall Tomcat. Para fins de saudação deste tutorial, aceitando os padrões de saudação é bom. Quando você chegar Olá **Olá Concluindo o Assistente de instalação do Apache Tomcat** caixa de diálogo, você pode verificar opcionalmente **executar Apache Tomcat** toohave início do Tomcat agora. Clique em **concluir** toocomplete Olá o processo de instalação do Tomcat.

## <a name="toostart-tomcat"></a>toostart Tomcat

Você pode iniciar manualmente Tomcat abrindo um prompt de comando em sua máquina virtual e executando o comando Olá **net&nbsp;iniciar&nbsp;Tomcat8**.

Quando Tomcat estiver em execução, você pode acessar o Tomcat digitando a URL de saudação <http://localhost:8080> no navegador Olá máquina virtual.

toosee Tomcat em execução de computadores externos, você precisa toocreate um ponto de extremidade e abre uma porta.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate um ponto de extremidade para sua máquina virtual
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Máquinas virtuais (clássicas)**.
3. Clique em nome de saudação da máquina virtual Olá que está executando o servidor de aplicativos Java.
4. Clique em **Pontos de Extremidade**.
5. Clique em **Adicionar**.
6. Em Olá **Adicionar ponto de extremidade** caixa de diálogo:
   1. Especifique um nome para o ponto de extremidade Olá; Por exemplo, **HttpIn**.
   2. Selecione **TCP** para o protocolo de saudação.
   3. Especifique **80** para a porta pública hello.
   4. Especifique **8080** para a porta privada hello.
   5. Selecione **desabilitado** para Olá flutuante endereço IP.
   6. Deixe a lista de controle de acesso hello como está.
   7. Clique em Olá **Okey** botão caixa de diálogo tooclose hello e criar o ponto de extremidade de saudação.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen uma porta no firewall Olá para sua máquina virtual
1. Entrar na máquina virtual de tooyour.
2. Clique em **Iniciar do Windows**.
3. Clique em **Painel de Controle**.
4. Clique em **Sistema e Segurança**, clique em **Firewall do Windows** e, em seguida, clique em **Configurações Avançadas**.
5. Clique em **Regras de Entrada** e, em seguida, clique em **Nova Regra**.  
   ![Nova regra de entrada][NewIBRule]
6. Para Olá **tipo de regra**, selecione **porta**e, em seguida, clique em **próximo**.  
   ![Nova porta de regra de entrada][NewRulePort]
7. Em Olá **protocolo e portas** tela, selecione **TCP**, especifique **8080** como Olá **porta local específica**e, em seguida, clique em **Próxima**.  
  ![Nova regra de entrada][NewRuleProtocol]
8. Em Olá **ação** tela, selecione **Permitir conexão Olá**e, em seguida, clique em **próximo**.
   ![Nova ação de regra de entrada][NewRuleAction]
9. Em Olá **perfil** tela, verifique se **domínio**, **privada**, e **pública** estão selecionados e, em seguida, clique em **Avançar** .
   ![Novo perfil de regra de entrada][NewRuleProfile]
10. Em Olá **nome** tela, especifique um nome para a regra de saudação, como **HttpIn** (nome da regra de saudação não é necessário toomatch Olá ponto de extremidade nome, no entanto) e, em seguida, clique em **concluir**.  
    ![Nome da nova regra de entrada][NewRuleName]

Neste ponto, o site do Tomcat deverá estar visível em um navegador externo. Na janela de endereço do navegador hello, digite uma URL do formulário de saudação  **http://*sua\_DNS\_nome*. cloudapp.net**, onde ***sua\_DNS\_nome*** é nome DNS de saudação você especificou quando criou a máquina virtual de saudação.

## <a name="application-lifecycle-considerations"></a>Considerações sobre o ciclo de vida do aplicativo
* Você pode criar seu próprio arquivo de aplicativo da web (WAR) e adicioná-lo toohello **webapps** pasta. Por exemplo, crie um projeto Web dinâmico JSP (Página de Serviço Java) básico e exporte-o como um arquivo WAR. Em seguida, copie Olá WAR toohello Apache Tomcat **webapps** pasta na máquina virtual de hello, em seguida, executá-lo em um navegador.
* Por padrão quando Olá serviço Tomcat é instalado, ele é definido toostart manualmente. Você pode desativá-toostart automaticamente usando o snap-in de serviços de saudação. Inicie o snap-in de serviços de saudação clicando **inicial do Windows**, **ferramentas administrativas**e, em seguida, **serviços**. Clique duas vezes em Olá **Apache Tomcat** de serviço e defina **o tipo de inicialização** muito**automática**.

    ![Configuração de um serviço toostart automaticamente][service_automatic_startup]

    Olá benefício de ter Tomcat iniciar automaticamente é que ela começa em execução quando a máquina virtual de saudação é reinicializada (por exemplo, após a instalação atualizações de software que exigem uma reinicialização).

## <a name="next-steps"></a>Próximas etapas
Você pode aprender sobre outros serviços (como o armazenamento do Azure, barramento de serviço e banco de dados SQL) que podem ser tooinclude com seus aplicativos Java. Exibir informações de saudação disponíveis a saudação [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
