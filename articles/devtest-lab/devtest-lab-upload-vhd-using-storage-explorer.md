---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando o Microsoft Azure Storage Explorer | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando o Microsoft Azure Storage Explorer
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Carregar conta de armazenamento do toolab do arquivo VHD usando o Microsoft Azure Storage Explorer

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado. Este artigo ilustra como toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) conta de armazenamento do laboratório tooa tooupload um VHD do arquivo. Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD. Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Olá seguintes etapas walk arquivo por meio de carregar um VHD laboratórios tooDevTest usando [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Baixe e instale a versão mais recente de saudação do hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).

1. Obter nome de saudação do laboratório de saudação conta de armazenamento usando Olá portal do Azure:

    1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.
    
    1. Saudação de laboratórios, selecione lista laboratório desejado hello.  
    
    1. Na folha do laboratório hello, selecione **configuração**. 
    
    1. Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.
    
    1. Em Olá **imagens personalizadas** folha, selecione **+ adicionar**. 
    
    1. Em Olá **imagem personalizada** folha, selecione **VHD**.
    
    1. Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.
    
        ![Carregar o VHD usando o PowerShell][0]
    
    1. Olá **carregue uma imagem usando o PowerShell** folha exibe uma chamada toohello **Add-AzureVhd** cmdlet. Olá primeiro parâmetro (*destino*) contém o nome de conta de armazenamento Olá para o laboratório Olá Olá formato a seguir:
    
        https://<NOME-DA-CONTA-DE-ARMAZENAMENTO>.blob.core.windows.net/uploads/... 

    1. Anote o nome de conta de armazenamento hello, como ele é usado em etapas posteriores.
    
1. Conecte-se tooan conta de assinatura do Azure usando o Gerenciador de armazenamento.

    > [!TIP] 
    > 
    > O Explorer do Armazenamento dá suporte a várias opções de conexão. Esta seção ilustra a conta de armazenamento tooa conexão associada à sua assinatura do Azure. toosee Olá outras opções de conexão tem suportadas pelo Gerenciador de armazenamento, consulte o artigo toohello, [guia de Introdução ao Gerenciador de armazenamento](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Abra o Explorer do Armazenamento.
    
    1. No Explorer do Armazenamento, selecione **Configurações de Conta do Azure**. 
    
        ![Configurações de conta do Azure][1]
    
    1. painel esquerdo Olá exibe você fez logon para contas da Microsoft hello. conta de tooanother tooconnect, selecione **adicionar uma conta**e siga Olá toosign de caixas de diálogo com uma conta da Microsoft que está associada a pelo menos uma assinatura ativa do Azure.
    
        ![Adicionar uma conta][2]
    
    1. Depois que você entrar com êxito com uma conta da Microsoft, o painel esquerdo Olá preenche com hello assinaturas do Azure associadas a essa conta. Selecione Olá assinaturas do Azure com o qual você deseja toowork e, em seguida, selecione **aplicar**. (Selecionar **todas as assinaturas** alterna Olá seleção de todos ou nenhum Olá listadas assinaturas do Azure.)
    
        ![Selecionar assinaturas do Azure][3]
    
    1. painel esquerdo Olá exibe as contas de armazenamento Olá associadas a assinaturas do Azure Olá selecionado.
    
        ![Assinaturas do Azure selecionadas][4]

1. Localize a conta de armazenamento do laboratório hello:

    1. No painel esquerdo do Gerenciador de armazenamento hello, localize e expanda nó Olá Olá assinatura do Azure que possui o laboratório de saudação.
    
    1. No nó da assinatura hello, expanda **contas de armazenamento**.

    1. Expandir nós de tooreveal de nó do laboratório Olá armazenamento conta para **contêineres de Blob**, **compartilhamentos de arquivos**, **filas**, e **tabelas**.
    
    1. Expanda Olá **contêineres de Blob** nó.
    
    1. Selecione toodisplay de contêiner de blob de carregamentos de saudação seu conteúdo no painel direito da saudação.
        
        ![Diretório de carregamento][5]

1. Carregar arquivo VHD hello usando o Gerenciador de armazenamento:

    1. No painel à direita do Gerenciador de armazenamento hello, você deve ver uma lista dos blobs Olá Olá **carrega** contêiner de blob da conta de armazenamento do laboratório hello. Em ferramentas do editor de blob hello, selecione **carregar** 
        
        ![Botão Carregar][6]
    
    1. De saudação **carregar** menu suspenso, selecione **carregar arquivos...** .
    
    1. Em Olá **carregar arquivos** caixa de diálogo, reticências Olá select.
        
        ![Escolher arquivo][8]  

    1. Em Olá **tooupload Selecione arquivos** caixa de diálogo, procurar toohello desejado arquivo VHD, selecioná-lo e, em seguida, selecione **abrir**.
    
    1. Quando retornado toohello **carregar arquivos** caixa de diálogo, altere **tipo de Blob** muito**Blob de página**.
    
    1. Escolha **Carregar**.

        ![Escolher arquivo][9]  
    
    1. Olá Storage Explorer **Log de atividades** painel mostra o status do download de saudação (junto com links toocancel Olá carregamento). processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão. 

        ![Status de carregamento do arquivo][10]  

## <a name="next-steps"></a>Próximas etapas

- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure](devtest-lab-create-template.md)
- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
