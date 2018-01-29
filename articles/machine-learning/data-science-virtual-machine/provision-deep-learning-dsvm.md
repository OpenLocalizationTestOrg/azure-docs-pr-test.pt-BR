---
title: "Provisionar a Máquina Virtual de Ciência de Dados do Aprendizado Aprofundado no Azure | Microsoft Docs"
description: "Configure e crie uma Máquina Virtual de Ciência de Dados de Aprendizado Aprofundado no Azure para realizar a análise e o aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 09/10/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: db1360fa54d82c50adc04194697d994925338296
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="provision-a-deep-learning-virtual-machine-on-azure"></a>Provisionar uma Máquina Virtual de Aprendizado Aprofundado no Azure 

A DLVM (Máquina Virtual de Aprendizado Aprofundado) é uma variante especialmente configurada da conhecida DSVM [(Máquina Virtual de Ciência de Dados)](http://aka.ms/dsvm) para tornar mais fácil usar instâncias de VM baseadas em GPU para treinamento rápido de modelos de aprendizado aprofundado. É compatível com Windows 2016 ou Ubuntu DSVM como base. A DLVM compartilha as mesmas imagens de VM de núcleo e, portanto, todo o amplo conjunto de ferramentas que está disponível na DSVM. 

A DLVM contém várias ferramentas para IA, incluindo as edições de GPU de estruturas de aprendizado aprofundado populares, como Kit de Ferramentas de Serviços Cognitivos da Microsoft, TensorFlow, Keras, Caffe2, Chainer, bem como ferramentas para adquirir e pré-processar imagens, dados textuais, ferramentas para atividades de modelagem e desenvolvimento de ciência de dados, como Microsoft R Server Developer Edition, Anaconda Python, notebooks do Jupyter para Python e R, IDEs para Python e R, bancos de dados SQL e muitas outras ferramentas de ML e ciência de dados. 

## <a name="create-your-deep-learning-virtual-machine"></a>Crie sua Máquina Virtual de Aprendizado Aprofundado
Veja as etapas para criar uma instância da Máquina Virtual de Aprendizado Aprofundado: 

1. Navegue até a máquina virtual no [portal do Azure](https://portal.azure.com/#create/microsoft-ads.dsvm-deep-learningtoolkit
).
2. Selecione o botão **Criar** na parte inferior para ser levado para um assistente .![create-dlvm](./media/dlvm-provision-wizard.PNG)
3. O assistente usado para criar a DLVM exige **entradas** para cada uma das **quatro etapas** enumeradas à direita dessa figura. Aqui estão as entradas necessárias para configurar cada uma das seguintes etapas:
   
   1. **Noções básicas**
      
      1. **Nome**: o nome do servidor de ciência de dados que você está criando.
      2. **Selecione o tipo de sistema operacional para a VM de Aprendizado Aprofundado**: escolha Windows ou Linux (para DSVM com base em Windows 2016 e Ubuntu Linux)
      2. **Nome de Usuário**: ID de logon da conta de administrador.
      3. **Senha**: senha da conta de administrador.
      4. **Assinatura**: se você tiver mais de uma assinatura, selecione aquela em que o computador será criado e cobrado.
      5. **Grupo de recursos**: você pode criar um novo ou usar um grupo de recursos existente **vazio** Azure na sua assinatura.
      6. **Local**: selecione o datacenter mais apropriado. Normalmente, é o datacenter que contém a maioria dos seus dados ou que está mais próximo de sua localização física para o acesso mais rápido à rede. 
      
> [!NOTE]
> Como a DLVM é provisionada em instâncias de VM de GPU Série NC do Azure, você deve selecionar um dos locais no Azure que tenha GPUs. Atualmente, os locais que têm VMs de GPU são: **Leste dos EUA, Centro-Norte dos EUA, Centro-Sul dos EUA, Oeste dos EUA 2, Europa Setentrional, Europa Ocidental**. Para obter a lista mais recente, verifique os [Produtos do Azure pela página da região](https://azure.microsoft.com/en-us/regions/services/) e procure **Série NC** em **Computação**. 

   2. **Configurações**: selecione um tamanho de máquina virtual de GPU Série NC que atenda aos seus requisitos funcionais e restrições de custo. Crie uma conta de armazenamento para sua VM.  ![dlvm-settings](./media/dlvm-provision-step-2.PNG)
   
   3. **Resumo**: verifique se todas as informações inseridas estão corretas.
   5. **Comprar**: clique em **Comprar** para iniciar o provisionamento. Um link para os termos da transação é fornecido. A VM não tem encargos adicionais além dos de computação para o tamanho do servidor que você escolheu na etapa **Tamanho** . 

> [!NOTE]
> O provisionamento deve levar cerca de 10 a 20 minutos. O status do provisionamento é exibido no Portal do Azure.
> 


## <a name="how-to-access-the-deep-learning-virtual-machine"></a>Como acessar a Máquina Virtual de Aprendizado Aprofundado

### <a name="windows-edition"></a>Edição do Windows
Depois de criar a máquina virtual, você poderá entrar na área de trabalho remotamente usando as credenciais da conta de administrador configurada anteriormente na seção **Noções básicas** . 

### <a name="linux-edition"></a>Edição do Linux

Após a criação da VM, você poderá entrar nela usando SSH. Use as credenciais da conta criada na seção **Noções básicas** da etapa 3 para a interface shell de texto. Em um cliente Windows, você pode baixar uma ferramenta de cliente SSH como o [Putty](http://www.putty.org). Se você preferir uma área de trabalho gráfica (Sistema do Windows X), poderá usar o encaminhamento X11 no Putty ou instalar o cliente X2Go.

> [!NOTE]
> O cliente X2Go apresentou desempenho melhor do que o encaminhamento X11 nos testes. Recomendamos o uso do cliente X2Go para uma interface gráfica de área de trabalho.
> 
> 

#### <a name="installing-and-configuring-x2go-client"></a>Instalando e configurando o cliente X2Go
A DLVM do Linux já está provisionada com um servidor X2Go e pronta para aceitar conexões de cliente. Para se conectar à área de trabalho gráfica da VM do Linux, realize o seguinte procedimento em seu cliente:

1. Baixe e instale o cliente X2Go para sua plataforma de cliente [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Execute o cliente X2Go e selecione **Nova Sessão**. Ele abrirá uma janela de configuração com várias guias. Insira os seguintes parâmetros de configuração:
   * **Guia Sessão**:
     * **Host**: o nome do host ou endereço IP da sua VM de Ciência de Dados Linux.
     * **Logon**: nome de usuário na VM Linux.
     * **Porta SSH**: deixe-a em 22, o valor padrão.
     * **Tipo de Sessão**: altere o valor para **XFCE**. No momento, a DSVM do Linux dá suporte apenas à área de trabalho XFCE.
   * **Guia Mídia**: você poderá desligar o suporte a som e impressão de cliente se não precisar usá-los.
   * **Pastas compartilhadas**: caso você queira que os diretórios de seus computadores cliente sejam montados na VM Linux, adicione os diretórios de computador cliente que você deseja compartilhar com a VM nesta guia.

Após o logon na VM usando o cliente SSH ou a área de trabalho gráfica XFCE por meio do cliente X2Go, você estará pronto para começar a usar as ferramentas instaladas e configuradas na VM. No XFCE, você pode ver atalhos do menu de aplicativos e ícones da área de trabalho para muitas das ferramentas.

Depois de criar e provisionar sua VM, você estará pronto para começar a usar as ferramentas que estão instaladas e configuradas nela. Há blocos do menu Iniciar e ícones da área de trabalho para várias das ferramentas. 
