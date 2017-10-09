---
title: "aaaBackup máquinas virtuais do Windows Azure | Microsoft Docs"
description: Proteja as VMs do Windows fazendo backup delas com o Backup do Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Fazer backup de máquinas virtuais do Windows no Azure

Você pode proteger seus dados fazendo backups em intervalos regulares. O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica. Quando você restaurar de um ponto de recuperação, você poderá restaurar Olá VM inteira ou apenas determinados arquivos. Este artigo explica como toorestore um único arquivo tooa VM que executa o Windows Server e o IIS. Se você ainda não tiver um toouse VM, você pode criar um usando Olá [início rápido do Windows](quick-create-portal.md). Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um backup de uma VM
> * Agendar um backup diário
> * Restaurar um arquivo de um backup




## <a name="backup-overview"></a>Visão geral do backup

Quando Olá serviço Backup do Azure inicia um trabalho de backup, ela aciona Olá extensão backup tootake um instantâneo point-in-time. saudação de serviço de Backup do Azure usa Olá _VMSnapshot_ extensão. extensão de saudação é instalado durante o primeiro backup VM Olá se Olá VM está em execução. Se hello VM não está em execução, Olá serviço de Backup tira um instantâneo de saudação armazenamento subjacente (já que nenhum aplicativo grava ocorre durante a saudação que VM estiver parada).

Ao tirar um instantâneo de máquinas virtuais do Windows, o serviço de Backup Olá coordena com hello Volume Shadow Copy Service (VSS) tooget um instantâneo consistente dos discos da máquina de virtual hello. Depois de saudação serviço Backup do Azure usa instantâneo hello, dados saudação são toohello transferidos cofre. toomaximize eficiência, o serviço de saudação identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior de saudação hello.

Quando a transferência de dados de saudação for concluída, Olá é removido e um ponto de recuperação é criado.


## <a name="create-a-backup"></a>Criar um backup
Crie um simple agendado diariamente backup tooa Cofre de serviços de recuperação. 

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. No menu Olá Olá esquerda, selecione **máquinas virtuais**. 
3. Olá, selecione lista tooback uma VM para cima.
4. Na folha VM hello, em Olá **configurações** seção, clique em **Backup**. Olá **habilitar backup** folha é aberta.
5. Em **Cofre de serviços de recuperação**, clique em **criar novo** e fornecer nome hello novo cofre de saudação. Um novo cofre é criado no hello mesmo grupo de recursos e o local da máquina virtual de saudação.
6. Clique em **Política de backup**. Neste exemplo, lembre-Olá padrões e clique em **Okey**.
7. Em Olá **habilitar backup** folha, clique em **habilitar Backup**. Isso cria um backup diário com base no agendamento de padrão de saudação.
10. toocreate um ponto de recuperação inicial, em Olá **Backup** folha clique **Backup agora**.
11. Em Olá **Backup agora** folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.
12. Em Olá **Backup** folha para sua VM, você verá Olá número de pontos de recuperação completa.

    ![Pontos de Recuperação](./media/tutorial-backup-vms/backup-complete.png)
    
primeiro backup de saudação leva cerca de 20 minutos. Depois que o backup for concluído, vá toohello próxima parte deste tutorial.

## <a name="recover-a-file"></a>Recuperar um arquivo

Se você excluir ou fazer alterações tooa arquivo acidentalmente, você pode usar o arquivo de saudação do toorecover de recuperação de arquivos do seu Cofre de backup. Recuperação de arquivos usa um script que é executado em Olá VM, ponto de recuperação toomount hello como unidade local. Essas unidades permanecerá montadas por 12 horas para que você possa copiar arquivos de ponto de recuperação de saudação e restaurá-los toohello VM.  

Neste exemplo, mostramos como toorecover Olá arquivo de imagem que é usado na página saudação padrão da web para o IIS. 

1. Abra um navegador e conecte-se o endereço IP toohello da página IIS Olá VM tooshow saudação padrão.

    ![Página da Web padrão do IIS](./media/tutorial-backup-vms/iis-working.png)

2. Conecte-se toohello VM.
3. No hello VM, abra **Explorador de arquivos** e navegue too\inetpub\wwwroot e exclua o arquivo hello **iisstart.png**.
4. No computador local, a atualização Olá navegador toosee que Olá imagem na página IIS padrão Olá será excluída.

    ![Página da Web padrão do IIS](./media/tutorial-backup-vms/iis-broken.png)

5. No computador local, abra uma nova guia e vá Olá Olá [portal do Azure](https://portal.azure.com).
6. No menu Olá Olá esquerda, selecione **máquinas virtuais** e selecione Olá VM formulário Olá lista.
8. Na folha VM hello, em Olá **configurações** seção, clique em **Backup**. Olá **Backup** folha é aberta. 
9. No menu de saudação na parte superior de saudação da folha de saudação, selecione **recuperação de arquivo**. Olá **recuperação de arquivo** folha é aberta.
10. Em **etapa 1: selecione o ponto de recuperação**, selecione um ponto de recuperação na lista suspensa hello.
11. No **etapa 2: baixar o script toobrowse e recuperar arquivos**, clique em hello **executável baixar** botão. Salvar Olá arquivo tooyour **Downloads** pasta.
12. No computador local, abra **Explorador de arquivos** e navegue tooyour **Downloads** Olá pasta e copie o arquivo de .exe baixado. nome de arquivo Hello será prefixado pelo nome da sua VM. 
13. Na sua VM (sobre Olá conexão RDP) cole Olá .exe arquivo toohello área de trabalho da VM. 
14. Navegue até toohello a área de trabalho da VM e clique duas vezes em .exe hello. Isso iniciará um prompt de comando e em seguida, monte o ponto de recuperação hello como um compartilhamento de arquivos que você pode acessar. Quando ele for concluído criar compartilhamento de hello, digite **p** tooclose prompt de comando de saudação.
15. Em sua VM, abra **Explorador de arquivos** e navegue toohello letra da unidade que foi usada para o compartilhamento de arquivo hello.
16. Navegue too\inetpub\wwwroot e cópia **iisstart.png** do arquivo hello compartilhar e cole-o em \Inetpub\Wwwroot.. Por exemplo, copie F:\inetpub\wwwroot\iisstart.png e cole-o em um arquivo de saudação do c:\inetpub\wwwroot toorecover.
17. No computador local, abra a guia do navegador de saudação em que você está conectado toohello endereço IP de saudação VM mostrando Olá IIS padrão a página. Pressione CTRL + F5 página do navegador Olá toorefresh. Agora, você verá que Olá imagem foi restaurada.
18. No computador local, volte toohello guia do navegador para Olá portal do Azure e na **etapa 3: desmontar discos Olá após a recuperação** clique Olá **desmontar discos** botão. Se você esquecer toodo nesta etapa, ponto de montagem do hello conexão toohello é fechar automaticamente após 12 horas. Após as 12 horas, é necessário toodownload um novo toocreate de script um novo ponto de montagem.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar um backup de uma VM
> * Agendar um backup diário
> * Restaurar um arquivo de um backup

Avançar toohello toolearn próximo de tutorial sobre o monitoramento de máquinas virtuais.

> [!div class="nextstepaction"]
> [Monitorar máquinas virtuais](tutorial-monitoring.md)









