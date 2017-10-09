---
title: "aaaSet uma máquina virtual como um servidor de bloco de anotações do IPython | Microsoft Docs"
description: "Configure uma Máquina Virtual do Azure para uso em um ambiente de ciência de dados com o IPython Server para análise avançada."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 818617c1-048e-49c2-b941-f9a983f93998
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: 58386140ec7742ade1f7e183ec842a2b09b9dfca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurar uma máquina virtual do Azure como um servidor do IPython Notebook para análises avançadas
Este tópico mostra como tooprovision e configurar uma máquina virtual do Azure para análise avançada que pode ser usado como parte de um ambiente de ciência de dados. máquina de virtual do Windows Hello está configurada com ferramentas como bloco de anotações do IPython, Azure Storage Explorer, AzCopy, bem como outros utilitários que são úteis para projetos de análise avançada de suporte. Azure Storage Explorer e AzCopy, por exemplo, fornecem maneiras convenientes armazenamento de blob de tooAzure tooupload dados do seu computador local ou toodownload-tooyour o computador local do armazenamento de blob.

## <a name="create-vm"></a>Etapa 1: criar uma máquina virtual do Azure com finalidade geral
Se você já tiver uma máquina virtual do Azure e deseja apenas tooset um servidor de bloco de anotações do IPython nele, você pode ignorar esta etapa e continue muito[etapa 2: adicionar um ponto de extremidade para a máquina virtual existente de tooan anotações do IPython](#add-endpoint).

Antes de iniciar o processo de saudação de criação de uma máquina virtual no Azure, você precisa ter tamanho de Olá toodetermine da máquina de saudação que é necessário tooprocess Olá dados para seu projeto. Máquinas menores têm menos memória e menos núcleos de CPU que máquinas maiores, mas elas também são mais baratas. Para obter uma lista de tipos de máquina e preços, consulte Olá <a href="http://azure.microsoft.com/pricing/details/virtual-machines/" target="_blank">preços das máquinas virtuais </a> página

1. Entrar muito<a href="https://manage.windowsazure.com" target="_blank">portal clássico do Azure</a>e clique em **novo** no canto do hello inferior esquerdo. Uma janela será exibida. Selecione **COMPUTAÇÃO** -> **MÁQUINA VIRTUAL** -> **DA GALERA**.
   
    ![Criar espaço de trabalho][24]
2. Escolha uma saudação imagens a seguir:
   
   * Windows Server 2012 R2 Datacenter
   * Experiência do Windows Server Essentials (Windows Server 2012 R2)
     
     Clique em seta Olá apontando para Olá inferior direita toogo Olá próxima página de configuração.
     
     ![Criar espaço de trabalho][25]
3. Insira um nome para a máquina virtual de saudação deseja toocreate, tamanho de saudação select da máquina de saudação (padrão: A3) com base no tamanho de saudação da máquina de saudação dados Olá é tooprocess contínuo e poderosas como você deseja Olá máquina toobe (memória tamanho e hello número de núcleos de computação) , digite um nome de usuário e senha para a máquina de saudação. Em seguida, clique em Olá seta para direita toogo toohello próxima página de configuração.
   
    ![Criar espaço de trabalho][26]
4. Selecione Olá **AFINIDADE região/grupo/rede VIRTUAL** que contém Olá **conta de armazenamento** que você está planejando toouse para esta máquina virtual e, em seguida, selecione a conta de armazenamento. Adicionar um ponto de extremidade na parte inferior da saudação em Olá **pontos de EXTREMIDADE** campo digitando o nome de saudação do ponto de extremidade de saudação ("IPython" aqui). Você pode escolher qualquer cadeia de caracteres como Olá **nome** de ponto de extremidade hello e qualquer número inteiro entre 0 e 65536 **disponível** como Olá **porta pública**. Olá **porta PRIVADA** tem toobe **9999**. **Evite** usar portas públicas que já tenham sido atribuídas a serviços de Internet. As <a href="http://www.chebucto.ns.ca/~rakerman/port-table.html" target="_blank">Portas para Serviços de Internet</a> fornecem uma lista de portas que foram atribuídas e devem ser evitadas.
   
    ![Criar espaço de trabalho][27]
5. Clique em Olá marca de seleção toostart Olá provisionamento da máquina virtual processo.
   
    ![Criar espaço de trabalho][28]

Pode levar 15 a 25 minutos toocomplete Olá provisionamento da máquina virtual processo. Depois de máquina virtual de saudação tiver sido criada, o status de saudação da máquina deve aparecer como **executando**.

![Criar espaço de trabalho][29]

## <a name="add-endpoint"></a>Etapa 2: Adicionar um ponto de extremidade para a máquina virtual existente de tooan anotações do IPython
Se você criou a máquina virtual de saudação seguindo as instruções de saudação na etapa 1, em seguida, ponto de extremidade de saudação do bloco de anotações do IPython já foi adicionado e essa etapa pode ser ignorada.

Se Olá da máquina virtual já existir e você precisa tooadd um ponto de extremidade para o bloco de anotações do IPython que você instalará na etapa 3 abaixo, primeiro logon tooAzure portal clássico, selecione a máquina virtual de saudação e adicionar ponto de extremidade Olá para o servidor de bloco de anotações do IPython. Olá figura a seguir contém uma captura de tela de portal Olá depois da adição de ponto de extremidade de saudação do bloco de anotações do IPython tooa máquina de virtual do Windows.

![Criar espaço de trabalho][17]

## <a name="run-commands"></a>Etapa 3: instalar o IPython Notebook e outras ferramentas de suporte
Após a criação de máquina virtual de hello, use toolog de protocolo de área de trabalho remota (RDP) na máquina de virtual do Windows toohello. Para obter instruções, consulte [como tooLog no tooa Máquina Virtual executando o Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Olá abrir **Prompt de comando** (**não Olá janela comando do Powershell**) como um **administrador** e execução Olá comando a seguir.

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Quando Olá instalação for concluída, Olá server do bloco de anotações do IPython é iniciado automaticamente no hello *c:\\usuários\\\<nome de usuário\>\\documentos\\IPython Blocos de anotações* directory.

Quando solicitado, insira uma senha para o bloco de anotações do IPython de saudação e a senha de saudação do administrador do computador hello. Isso permite Olá toorun do bloco de anotações do IPython como um serviço no computador de saudação.

## <a name="access"></a>Etapa 4: acesse o IPython Notebooks usando um navegador da Web
Olá tooaccess server do bloco de anotações do IPython, abra uma web navegador e entrada *https://&#60;virtual nome DNS do computador >: &#60; o número de porta pública >* na caixa de texto URL hello. Aqui, Olá *&#60; o número de porta pública >* deve ser um número de porta Olá especificado quando hello ponto de extremidade do bloco de anotações do IPython foi adicionado.

Olá *&#60; o nome DNS da máquina virtual >* pode ser encontrado em Olá portal clássico do Azure. Depois de fazer logon no portal clássico do toohello, clique em **máquinas virtuais**, selecione máquina Olá você criou e, em seguida, selecione **painel**, nome DNS Olá será mostrado da seguinte maneira:

![Criar espaço de trabalho][19]

Você encontrará um aviso informando que *há um problema com o certificado de segurança deste site* (Internet Explorer) ou *sua conexão não é privado* (Chrome), conforme mostrado na seguinte Olá valores. Clique em **continuar toothis site (não recomendado)** (Internet Explorer) ou **avançado** e  **continuar muito &#60;* Nome DNS*> (não seguros) * * toocontinue (Chrome). Em seguida, entrada senha Olá você especificado tooaccess anteriores Olá anotações do IPython.

**Internet Explorer:**
![Criar espaço de trabalho][20]

**Chrome:**
![Criar espaço de trabalho][21]

Depois de fazer logon toohello bloco de anotações do IPython, um diretório *DataScienceSamples* será exibido no navegador de saudação. Este diretório contém anotações do IPython de exemplo que são compartilhadas por tarefas de ciência de dados do Microsoft toohelp usuários realizar. Esses blocos de anotações do IPython de exemplo são check-out do [ **repositório GitHub** ](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) toohello máquinas de virtuais durante a saudação processo de instalação do servidor de bloco de anotações do IPython. A Microsoft mantém e atualiza esse repositório com frequência. Os usuários podem visitar Olá GitHub repositório tooget atualizado mais recentemente exemplo hello anotações do IPython.
![Criar espaço de trabalho][18]

## <a name="upload"></a>Etapa 5: Carregar um bloco de anotações do IPython existente de um toohello servidor do bloco de anotações do IPython do computador local
Anotações do IPython fornecem uma maneira fácil para um bloco de anotações do IPython existente no toohello seus computadores locais server de bloco de anotações do IPython em máquinas virtuais de saudação de tooupload de usuários. Depois de fazer logon toohello bloco de anotações do IPython em um navegador da web, clique em Olá **diretório** que Olá bloco de anotações do IPython será carregado. Selecione um tooupload de arquivo do bloco de anotações do IPython .ipynb na máquina local Olá Olá **Explorador de arquivos**e arraste e solte-toohello diretório de bloco de anotações do IPython no navegador da web de saudação. Clique em Olá **carregar** botão tooupload Olá .ipynb arquivo toohello server do bloco de anotações do IPython. Então, outros usuários podem começar a usá-lo em seus navegadores da web.

![Criar espaço de trabalho][22]

![Criar espaço de trabalho][23]

## <a name="shutdown"></a>Desligar e desalocar a máquina virtual quando ela não estiver em uso
A cobrança das máquinas virtuais do Azure ocorre na forma **pague somente pelo que usa**. tooensure que não estão sendo cobrado quando não estiver usando sua máquina virtual, ele tem toobe em Olá **parado (desalocado)** estado quando não estiver em uso.

> [!NOTE]
> Se você desligar a máquina virtual de saudação do dentro Olá VM (usando as opções de energia do Windows), Olá VM for interrompido, mas permanece alocada. tooensure você não continuar toobe cobrado, sempre irá parar máquinas virtuais de saudação [portal clássico do Azure](http://manage.windowsazure.com/). Você também pode interromper Olá VM por meio do Powershell chamando **ShutdownRoleOperation** "PostShutdownAction" igual muito "StoppedDeallocated".
> 
> 

tooshut para baixo e desalocar máquina virtual de saudação:

1. Faça logon no toohello [portal clássico do Azure](http://manage.windowsazure.com/) usando sua conta.  
2. Selecione **máquinas virtuais** saudação à esquerda na barra de navegação.
3. Na lista de saudação de máquinas virtuais, clique no nome da saudação de sua máquina virtual, vá toohello **painel** página.
4. Final Olá Olá página, clique em **desligamento**.

![Desligamento da VM][15]

máquina virtual de saudação será desalocada mas não excluída. Você pode reiniciar a máquina virtual a qualquer momento de saudação portal clássico do Azure.

## <a name="your-azure-vm-is-ready-toouse-whats-next"></a>Sua VM do Azure está pronto toouse: próximas etapas?
Sua máquina virtual agora está pronto toouse seu exercícios de ciência de dados. máquina de virtual de Olá também está pronta para uso como um servidor de bloco de anotações do IPython para exploração hello e processamento de dados e outras tarefas em conjunto com o aprendizado de máquina do Azure e hello processo de ciência de dados de equipe.

Olá próximas etapas no Olá, equipe de processo de ciência de dados são mapeados em hello [caminho de aprendizado](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas que movem dados para HDInsight, o processo e de exemplo-lo na preparação para aprender com dados saudação com a máquina do Azure Aprendizado.

[15]: ./media/machine-learning-data-science-setup-virtual-machine/vmshutdown.png
[17]: ./media/machine-learning-data-science-setup-virtual-machine/add-endpoints-after-creation.png
[18]: ./media/machine-learning-data-science-setup-virtual-machine/sample-ipnbs.png
[19]: ./media/machine-learning-data-science-setup-virtual-machine/dns-name-and-host-name.png
[20]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning-ie.png
[21]: ./media/machine-learning-data-science-setup-virtual-machine/browser-warning.png
[22]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-1.png
[23]: ./media/machine-learning-data-science-setup-virtual-machine/upload-ipnb-2.png
[24]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-1.png
[25]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-2.png
[26]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-3.png
[27]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-4.png
[28]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-5.png
[29]: ./media/machine-learning-data-science-setup-virtual-machine/create-virtual-machine-6.png
