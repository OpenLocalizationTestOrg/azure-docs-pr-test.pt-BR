---
title: aaaHow toocreate uma imagem de modelo personalizado para o Azure RemoteApp | Microsoft Docs
description: "Saiba como toocreate um modelo personalizado de imagem para o Azure RemoteApp. Você pode usar este modelo com uma coleção de nuvem ou híbrida."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>Como a imagem toocreate um modelo personalizado para o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp usa um toohost de imagem de modelo do Windows Server 2012 R2 todos os programas de saudação que você deseja tooshare com seus usuários. toocreate uma imagem personalizada do RemoteApp, você pode começar com uma imagem existente ou criar um novo. 

> [!TIP]
> Você sabia que pode criar uma imagem de uma VM do Azure? História real e reduz tempo total de saudação ele leva tooimport Olá imagem. Check-out etapas Olá [aqui](remoteapp-image-on-azurevm.md).
> 
> 

requisitos de saudação de imagem Olá que podem ser carregados para uso com o Azure RemoteApp são:

* tamanho da imagem Olá deve ser um múltiplo de MBs. Se você tentar tooupload uma imagem que não é um múltiplo exato, carregamento Olá falhará.
* tamanho da imagem Olá deve ser 127 GB ou menores.
* Ela deve estar em um arquivo VHD (não há suporte atualmente para arquivos VHDX [discos rígidos virtuais Hyper-V]).
* Olá VHD não deve ser uma máquina virtual de geração 2.
* Olá VHD pode ser um tamanho fixo ou expansão dinâmica. Um VHD de expansão dinâmica é recomendado porque ela usa menos tooAzure tooupload de tempo que um arquivo VHD de tamanho fixo.
* disco Olá deve ser inicializado usando o estilo de particionamento Olá registro mestre de inicialização (MBR). Não há suporte para a saudação estilo de partição GUID partição GPT (tabela).
* Olá VHD deve conter uma única instalação do Windows Server 2012 R2. Ele deve conter vários volumes, mas apenas um que contenha uma instalação do Windows.
* função de Host de sessão de área de trabalho remota (RDSH) Hello e o recurso Experiência Desktop de saudação devem ser instalados.
* função de agente de Conexão de área de trabalho remota Olá deve *não* ser instalado.
* Olá Encrypting File System (EFS) deve ser desabilitada.
* Olá imagem deve ser submetida a Sysprep usando parâmetros de saudação **/oobe /generalize /shutdown** (não use Olá **/Mode: VM** parâmetro).
* Não há suporte para carregar o VHD de uma cadeia de instantâneo.

**Antes de começar**

Você precisa toodo Olá seguinte antes de criar o serviço de saudação:

* [Inscrever-se](https://azure.microsoft.com/services/remoteapp/) no RemoteApp.
* Crie uma conta de usuário no Active Directory toouse como Olá conta de serviço do RemoteApp. Restringir as permissões de saudação para essa conta para que ele só pode ingressar em domínio de toohello máquinas. Consulte [Configurar o Active Directory do Azure para o RemoteApp](remoteapp-ad.md) para obter mais informações.
* Colete informações sobre a sua rede local: informações sobre endereço IP e detalhes do dispositivo VPN.
* Instalar Olá [Azure PowerShell](/powershell/azure/overview) módulo.
* Colete informações sobre usuários Olá que você deseja toogrant access. Podem ser informações da conta da Microsoft ou da conta corporativa do Active Directory para usuários ou grupos.

## <a name="create-a-template-image"></a>Criar uma imagem do modelo
Estas são etapas de nível superior de saudação toocreate uma nova imagem de modelo a partir do zero:

1. Localize um DVD de atualização do Windows Server 2012 R2 ou a imagem ISO.
2. Crie um arquivo VHD.
3. Instale o Windows Server 2012 R2.
4. Instale a função de Host de sessão de área de trabalho remota (RDSH) hello e o recurso Experiência Desktop de saudação.
5. Instale os recursos adicionais necessários pelos seus aplicativos.
6. Instale e configure os seus aplicativos. aplicativos de compartilhamento de toomake mais fácil, adicionar todos os aplicativos ou programas que você deseja tooshare toohello **iniciar** menu da imagem hello, especificamente na **%systemdrive%\ProgramData\Microsoft\Windows\Start Iniciar\Programas.
7. Execute quaisquer configurações adicionais do Windows necessárias para os seus aplicativos.
8. Desabilite Olá Encrypting File System (EFS).
9. **OBRIGATÓRIA:** vá tooWindows atualização e instale todas as atualizações importantes.
10. Imagem de saudação do SYSPREP.

Olá etapas detalhadas para criar uma nova imagem são:

1. Localize um DVD de atualização do Windows Server 2012 R2 ou a imagem ISO.
2. Crie um arquivo VHD usando o Disk Management.
   
   1. Inicialize o Disk Management (diskmgmt.msc).
   2. Crie um VHD de expansão dinâmica com 40 GB ou com tamanho maior. (Estimar a quantidade de saudação do espaço necessário para Windows, seus aplicativos e as personalizações. Windows Server com a função de RDSH hello e o recurso Experiência Desktop instalado exigirá cerca de 10 GB de espaço).
      
      1. Clique em **Ação > Criar VHD**.
      2. Especifica local de hello, tamanho e formato VHD. Selecione **Expandir dinamicamente**, em seguida, clique em **OK**.
      
      A execução demorará vários segundos. Quando Olá criação do VHD estiver concluída, você verá um novo disco sem qualquer letra de unidade e no estado "Não inicializado" no console de gerenciamento de disco hello.
      
      * Clique no disco hello (não espaço não alocado de saudação) e clique **inicializar disco**. Selecione **MBR** (registro mestre de inicialização) como o estilo de partição hello e clique **Okey**.
      * Crie um novo volume: clique Olá espaço não alocado e, em seguida, clique em **Novo Volume simples**. Você pode aceitar os padrões de saudação no Assistente de saudação, mas certifique-se que atribuir uma unidade letra tooavoid problemas ao carregar a imagem de modelo hello.
      * Clique no disco Olá e clique **desanexar VHD**.
3. Instalar o Windows Server 2012 R2:
   
   1. Criar uma nova máquina virtual. Use Olá Assistente de nova máquina Virtual no Gerenciador do Hyper-V ou Hyper-V cliente.
      1. Na página de especificar geração hello, escolha **geração 1**.
      2. Na página conectar disco rígido Virtual de saudação, selecione **usar um disco rígido virtual existente**e procurar toohello VHD que você criou na etapa anterior hello.
      3. Na página de opções de instalação hello, selecione **instalar um sistema operacional de uma inicialização de CD/DVD_ROM**e, em seguida, selecione o local de saudação da sua mídia de instalação do Windows Server 2012 R2.
      4. Escolha outras opções de saudação de assistente necessário tooinstall Windows e seus aplicativos. Conclua o Assistente de saudação.
   2. Após a conclusão do assistente Olá, editar configurações de saudação da máquina virtual de saudação e faça as alterações necessárias tooinstall Windows e seus programas, como o número de saudação de processadores virtuais e, em seguida, clique em **Okey**.
   3. Conecte-se a máquina virtual de toohello e instale o Windows Server 2012 R2.
4. Instale a função de Host de sessão de área de trabalho remota (RDSH) hello e o recurso Experiência Desktop de saudação:
   1. Inicialize o Gerenciador do Servidor.
   2. Clique em **adicionar funções e recursos** ou na tela de boas-vindas Olá Olá **gerenciar** menu.
   3. Clique em **próximo** na página de saudação antes de começar.
   4. Selecione **Instalação baseada em função ou recurso** e clique em **Próximo**.
   5. Selecione máquina local Olá Olá lista e, em seguida, clique em **próximo**.
   6. Selecione **Serviços da Área de Trabalho Remota**, em seguida, clique em **Próximo**.
   7. Expanda **Interfaces de Usuário e Infraestrutura** e selecione **Experiência da Área de Trabalho**.
   8. Clique em **Adicionar Recursos**, em seguida, clique em **Próximo**.
   9. Na página de serviços de área de trabalho remota hello, clique em **próximo**.
   10. Clique em **Host da Sessão da Área de Trabalho Remota**.
   11. Clique em **Adicionar Recursos**, em seguida, clique em **Próximo**.
   12. Na página Olá Confirmar instalação seleções, selecione **reinicialização do servidor de destino Olá automaticamente, se necessário**e, em seguida, clique em **Sim** no hello reinicie o aviso.
   13. Clique em **Instalar**. Olá computador será reiniciado.
5. Instale recursos adicionais necessários para seus aplicativos, como saudação do .NET Framework 3.5. recursos tooinstall hello, executar Olá assistente Adicionar funções e recursos.
6. Instalar e configurar programas hello e aplicativos que você deseja toopublish por meio do RemoteApp.

> [!IMPORTANT]
> Instalar a função de RDSH Olá antes de instalar aplicativos tooensure que problemas de compatibilidade do aplicativo são descobertos Olá imagem anterior é carregado tooRemoteApp.
> 
> Certifique-se de um aplicativo de tooyour de atalho (**. lnk** arquivo) aparece na Olá **iniciar** menu para todos os usuários (%systemdrive%\ProgramData\Microsoft\Windows\Start Iniciar\Programas). Certifique-se também que ícone Olá você vê no hello **iniciar** menu é que você deseja toosee de usuários. Caso contrário, altere-o. (Você não *ter* menu Iniciar do tooadd Olá aplicativo toohello, mas ele torna muito mais fácil aplicação de saudação toopublish no RemoteApp. Caso contrário, você tem tooprovide Olá instalação caminho para o aplicativo hello quando você publicar o aplicativo hello.)
> 
> 

1. Execute quaisquer configurações adicionais do Windows necessárias para os seus aplicativos.
2. Desabilite Olá Encrypting File System (EFS). Olá executar comando em uma janela de comando com privilégios elevados a seguir:
   
     Fsutil behavior set disableencryption 1
   
   Como alternativa, você pode definir ou adicionar Olá seguinte valor DWORD no registro hello:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Se você estiver criando sua imagem dentro de uma máquina virtual do Azure, renomear Olá  **\%windir%\Panther\Unattend.xml** de arquivos, pois isso bloqueará o script de carregamento Olá usado posteriormente no trabalho. Altere o nome de saudação do tooUnattend.old arquivo para que você ainda terá Olá arquivo caso você precise toorevert sua implantação.
4. Vá tooWindows atualização e instale todas as atualizações importantes. Talvez seja necessário toorun Windows Update várias vezes tooget todas as atualizações. (Às vezes, você pode instalar uma atualização e essa atualização em si requerer uma atualização.)
5. Imagem de saudação do SYSPREP. Em um prompt de comando com privilégios elevados, execute Olá comando a seguir:
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **Observação:** não use Olá **/Mode: VM** switch de saudação SYSPREP comando mesmo que isso é uma máquina virtual.

## <a name="next-steps"></a>Próximas etapas
Agora que você tem a imagem de modelo personalizado, é necessário tooupload tooyour essa imagem coleção do RemoteApp. Use sua coleção de informações de Olá em Olá toocreate artigos a seguir:

* [Como toocreate uma coleção híbrida do RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Como toocreate uma coleção de nuvem do RemoteApp](remoteapp-create-cloud-deployment.md)

