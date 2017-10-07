---
title: "aaaCreate um bloco de anotações do Jupyter/IPython | Microsoft Docs"
description: "Saiba como toodeploy Olá Notebook Jupyter/IPython em uma máquina virtual Linux criado com o modelo de implantação de Gerenciador de recursos de saudação no Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a>Criando uma VM do Azure, instalando o Jupyter, e executando um Notebook do Jupyter no Azure
Olá [Jupyter projeto](http://jupyter.org), Olá anteriormente [IPython projeto](http://ipython.org), fornece um conjunto de ferramentas para computação científica usando poderosos shells interativos que combinam execução de código com a criação de saudação de um documento computacional ao vivo. Esses arquivos de notebook podem conter textos arbitrários, fórmulas matemáticas, códigos de entrada, resultados, gráficos, vídeos e qualquer outro tipo de mídia que um navegador da Web moderno é capaz de exibir. Se você estiver tooPython totalmente nova e deseja toolearn-lo em divertido, ambiente interativo ou fazer algumas grave paralelo/técnico de computação, Olá Jupyter Notebook é uma ótima opção.

![Captura de tela de](./media/jupyter-notebook/ipy-notebook-spectral.png) usando SciPy e Matplotlib pacotes tooanalyze Olá a estrutura de uma gravação de som.

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a>Duas maneiras para o Jupyter: Blocos de nota do Azure ou implantação personalizada
O Azure fornece um serviço que você pode usar também[iniciar rapidamente usando Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).  Usando hello Azure Notebook Service, você pode facilmente obter interface web acessível do tooJupyter acesso aos recursos computacionais escalonáveis com todo o poder de saudação do Python e suas bibliotecas de muitos.  Desde que a instalação de saudação é tratada pelo serviço Olá, os usuários podem acessar esses recursos sem necessidade de saudação de administração e configuração por usuário hello.

Se o serviço de bloco de anotações de saudação não funciona para seu cenário continue tooread deste artigo que será mostrará como toodeploy Olá Jupyter Notebook no Microsoft Azure, usando máquinas virtuais do Linux (VMs).

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a>Criar e configurar uma VM no Azure
primeira etapa de saudação é toocreate uma máquina virtual (VM) em execução no Azure.
Essa VM é um sistema operacional completo na nuvem hello e será usado para executar Olá anotações do Jupyter. O Azure é capaz de executar máquinas virtuais Linux e Windows, e abordaremos a instalação de saudação do Jupyter em ambos os tipos de máquinas virtuais.

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a>Criar uma VM Linux e abrir uma porta para o Jupyter
Siga as instruções de saudação dadas [aqui] [ portal-vm-linux] toocreate uma máquina virtual de saudação *Ubuntu* distribuição. Este tutorial usa o Ubuntu Server 14.04 LTS. Vamos supor que o nome de usuário Olá *azureuser*.

Depois de máquina virtual de saudação implanta precisamos tooopen uma regra de segurança no grupo de segurança de rede hello.  De Olá portal do Azure, vá muito**grupos de segurança de rede** e guia de saudação aberto para tooyour correspondente do grupo de segurança de saudação VM. Você precisa tooadd uma regra de segurança de entrada com hello configurações a seguir: **TCP** para protocolo hello,  **\***  para a porta de origem (público) hello e **9999** para porta de destino (privado) Hello.

![Captura de tela](./media/jupyter-notebook/azure-add-endpoint.png)

Enquanto estiver no seu grupo de segurança de rede, clique em **Interfaces de rede** e observe hello **endereço IP público** pois ela será necessária tooconnect tooyour VM na próxima etapa do hello.

## <a name="install-required-software-on-hello-vm"></a>Instalar o software necessário Olá VM
toorun Olá Jupyter Notebook em nosso VM, é necessário primeiro instalar Jupyter e suas dependências. Conecte-se a vm do linux tooyour usando ssh e par de nome de usuário/senha Olá você escolheu ao criar hello vm. Neste tutorial, usaremos PuTTY e conectaremos do Windows.

### <a name="installing-jupyter-on-ubuntu"></a>Instalando o Jupyter no Ubuntu
Instalar Anaconda, uma distribuição de python de ciência de dados populares, usando um dos links de saudação fornecidos pelo [continuidade análise](https://www.continuum.io/downloads).  A partir da gravação da saudação deste documento, Olá links a seguir são hello mais toodate versões de backup.

#### <a name="anaconda-installs-for-linux"></a>Instalações de Anaconda para Linux
<table>
  <th>Python 3.4</th>
  <th>Python 2,7</th>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </td>
  </tr>
  <tr>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>
    <td>
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a>Instalando o Anaconda3 2.3.0 de 64 bits no Ubuntu
Veja um exemplo de como você pode instalar o Anaconda no Ubuntu

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Captura de tela](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a>Configurando o Jupyter e usando SSL
Depois de instalar precisamos tootake arquivos de configuração um pouco toosetup Olá para Jupyter. Se você tiver problemas com a configuração Jupyter pode ser útil toolook em Olá [Jupyter documentação para a execução de um servidor de Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).

Next é `cd` toohello perfil diretório toocreate nosso certificado SSL e editar o arquivo de configuração de perfis de saudação.

No Linux, use Olá comando a seguir.

    cd ~/.jupyter

Use Olá comando toocreate Olá certificado SSL (Linux e Windows) a seguir.

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Observe que já que estamos criando um certificado SSL autoassinado, ao conectar-se o bloco de anotações toohello seu navegador fornecerá um aviso de segurança.  Para uso em produção a longo prazo, você desejará toouse um certificado apropriadamente assinado associado à sua organização.  Como o gerenciamento de certificado está além do escopo de saudação desta demonstração, manteremos certificado autoassinado tooa por enquanto.

Além disso toousing um certificado, você deve também fornecer tooprotect uma senha anotações contra uso não autorizado.  Por motivos de segurança Jupyter usa senhas criptografadas em seu arquivo de configuração, por isso você terá tooencrypt sua senha pela primeira vez.  IPython fornece um utilitário toodo isso; no prompt de comando, execute Olá comando a seguir.

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

Isso solicitará uma senha e a confirmação e imprimirá senha hello. Observação: isso para Olá etapa a seguir.

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

Em seguida, Editaremos o arquivo de configuração do perfil hello, que é o `jupyter_notebook_config.py` arquivo no diretório Olá estão em.  Observe que esse arquivo não pode existir – criá-la apenas se for esse caso de saudação.  Esse arquivo tem diversos campos, todos comentados por padrão.  Você pode abrir este arquivo com qualquer editor de texto de sua preferência, e você deve garantir que ele tem pelo menos Olá conteúdo a seguir. **Ser c.NotebookApp.password de saudação tooreplace-se na configuração de saudação com hello sha1 da etapa anterior Olá**.

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a>Executar Olá anotações do Jupyter
Neste momento, estamos toostart pronto Olá anotações do Jupyter. toodo isso, navegue toohello directory você deseja toostore notebooks e iniciar Olá servidor de Jupyter Notebook com hello comando a seguir.

    /anaconda3/bin/jupyter-notebook

Agora, você deve ser capaz de tooaccess seu Jupyter Notebook no endereço Olá `https://[PUBLIC-IP-ADDRESS]:9999`.

Quando você acessa pela primeira vez o bloco de anotações, página de logon Olá solicita sua senha. E, depois de entrar, você verá hello "Painel de Notebook Jupyter", que é o Centro de ontrole para todas as operações de bloco de anotações.  Nessa página, é possível criar novos notebooks e abrir os que já existem.

![Captura de tela](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a>Usando Olá anotações do Jupyter
Se você clicar em Olá **novo** botão, você verá Olá após a página de abertura.

![Captura de tela](./media/jupyter-notebook/jupyter-untitled-notebook.png)

área de saudação marcados com um `In []:` prompt é a área de entrada hello, aqui você pode digitar qualquer código Python válido e ela será executada quando você clicar em `Shift-Enter` ou clique no ícone de "Executar" hello (Olá Triângulo apontando na barra de ferramentas de saudação).

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a>Um paradigma avançado: documentos computacionais dinâmicos com mídia rica
notebook Olá em si deve se sentir tooanyone muito natural que usou Python e um processador de textos, porque se trata de certa forma uma mistura de ambos: você pode executar blocos de código Python, mas você pode manter notas e outro texto, alterando o estilo de saudação de uma célula de "Código" muito "Ma rkdown"usando o menu suspenso de saudação na barra de ferramentas.

O Jupyter é muito mais que um processador de texto, pois permite a combinação de computação e mídia rica (texto, gráficos, vídeos e praticamente qualquer coisa que um navegador da Web moderno pode exibir). Você pode misturar texto, códigos, vídeos e muito mais!

![Captura de tela](./media/jupyter-notebook/jupyter-editing-experience.png)

E com capacidade de saudação do muitas bibliotecas excelentes do Python para computação científica e técnica, em Olá seguinte captura de tela, um cálculo simples pode ser executado com hello iguais facilitam como uma análise de redes complexas, tudo em um ambiente.

Esse paradigma de potência de saudação do web moderna Olá a mistura de computação ao vivo oferece muitas possibilidades e é ideal para a nuvem Olá; Olá Notebook pode ser usado:

* Como um toorecord de computação de teste exploratório funcionam em um problema.
* tooshare resultados com colegas, no formulário computacional 'dinâmico' ou em cópia impressa formatos (HTML, PDF).
* toodistribute e presente materiais de ensino ao vivo que envolvem a computação, para que os alunos imediatamente podem testar com o código real de Olá, modificam-o e execute novamente interativamente.
* tooprovide "papers executável" que apresentam os resultados de saudação de pesquisa de uma maneira que pode ser reproduzida imediatamente, validar e estendido por outras pessoas.
* Como uma plataforma de computação colaborativa: vários usuários podem fazer logon no toothe mesmo servidor de notebook tooshare uma sessão ao vivo de computação.

Se você acessar o código-fonte IPython toohello [repositório][repository], você encontrará um diretório inteiro com exemplos de bloco de anotações que você pode baixar e, em seguida, experimente na sua própria máquina virtual Jupyter do Azure.  Basta baixar Olá `.ipynb` arquivos de saudação do site e carregá-las no painel de saudação do bloco de anotações VM do Azure (ou baixá-los diretamente no hello VM).

## <a name="conclusion"></a>Conclusão
saudação de anotações do Jupyter fornece uma interface avançada para acessar interativamente power saudação do ecossistema de Python Olá no Azure.  Ela abrange diversos casos de uso, incluindo exploração simples, aprendizado do Python, análise de dados e visualização, simulação e computação paralela. documentos de Notebook resultantes Olá contêm um registro completo de computações Olá que são executadas e pode ser compartilhada com outros usuários do Jupyter.  saudação de anotações do Jupyter pode ser usada como um aplicativo local, mas ele é ideal para implantações de nuvem no Azure

Olá principais recursos do Jupyter também estão disponíveis no Visual Studio por meio de [ferramentas Python para Visual Studio] [ Python Tools for Visual Studio] (PTVS). O PTVS é um plug-in gratuito e de código aberto da Microsoft que transforma o Visual Studio em um ambiente de implantação avançado do Python, incluindo um editor avançado com IntelliSense, depuração, criação de perfil e integração de computação paralela.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
