---
title: Fazer backup de VMs do Linux do Azure | Microsoft Docs
description: Proteja as VMs do Linux fazendo backup delas com o Backup do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Fazer backup de máquinas virtuais do Linux no Azure

Você pode proteger seus dados fazendo backups em intervalos regulares. O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica. Quando você restaurar de um ponto de recuperação, você poderá restaurar Olá VM inteira ou apenas determinados arquivos. Este artigo explica como toorestore um único arquivo tooa nginx de VM do Linux em execução. Se você ainda não tiver um toouse VM, você pode criar um usando Olá [Linux quickstart](quick-create-cli.md). Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um backup de uma VM
> * Agendar um backup diário
> * Restaurar um arquivo de um backup



## <a name="backup-overview"></a>Visão geral do backup

Quando Olá serviço Backup do Azure inicia um backup, ela aciona Olá extensão backup tootake um instantâneo point-in-time. saudação de serviço de Backup do Azure usa Olá _VMSnapshotLinux_ extensão no Linux. extensão de saudação é instalado durante o primeiro backup VM Olá se Olá VM está em execução. Se hello VM não está em execução, Olá serviço de Backup tira um instantâneo de saudação armazenamento subjacente (já que nenhum aplicativo grava ocorre durante a saudação que VM estiver parada).

Por padrão, Backup do Azure usa um backup consistente de sistema de arquivos para a VM do Linux, mas pode ser configurado tootake [backup consistente de aplicativo usando o script de pré e pós-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Depois de saudação serviço Backup do Azure usa instantâneo hello, dados saudação são toohello transferidos cofre. toomaximize eficiência, o serviço de saudação identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior de saudação hello.

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

## <a name="restore-a-file"></a>Restaurar um arquivo

Se você excluir ou fazer alterações tooa arquivo acidentalmente, você pode usar o arquivo de saudação do toorecover de recuperação de arquivos do seu Cofre de backup. Recuperação de arquivos usa um script que é executado em Olá VM, ponto de recuperação toomount hello como unidade local. Essas unidades permanecerá montadas por 12 horas para que você possa copiar arquivos de ponto de recuperação de saudação e restaurá-los toohello VM.  

Neste exemplo, mostramos como toorecover Olá padrão nginx página da web /var/www/html/index.nginx-debian.html. endereço IP público de saudação do nosso VM neste exemplo é *13.69.75.209*. Você pode encontrar o endereço IP de saudação do vm usando:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. No computador local, abra um navegador e digite no endereço IP público de saudação VM toosee saudação padrão nginx da página da web.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

1. SSH em sua VM.

    ```bash
    ssh 13.69.75.209
    ```
2. Exclua /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. No computador local, atualize o navegador de saudação pressionando CTRL + F5 toosee que nginx página padrão não existe mais.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-broken.png)
    
1. Em seu computador local, faça logon no toohello [portal do Azure](https://portal.azure.com/).
6. No menu Olá Olá esquerda, selecione **máquinas virtuais**. 
7. Olá, selecione lista Olá VM.
8. Na folha VM hello, em Olá **configurações** seção, clique em **Backup**. Olá **Backup** folha é aberta. 
9. No menu de saudação na parte superior de saudação da folha de saudação, selecione **recuperação de arquivo**. Olá **recuperação de arquivo** folha é aberta.
10. Em **etapa 1: selecione o ponto de recuperação**, selecione um ponto de recuperação na lista suspensa hello.
11. No **etapa 2: baixar o script toobrowse e recuperar arquivos**, clique em hello **executável baixar** botão. Salve o computador local do tooyour Olá arquivo baixado.
7. Clique em **baixar script** arquivo de script de saudação toodownload localmente.
8. Abra um Bash prompt e digite Olá a seguir, substituindo *Linux_myVM_05-05-2017.sh* com hello corrija o caminho e nome de arquivo para o script hello baixado, *azureuser* com nome de usuário Olá para Olá VM e *13.69.75.209* com endereço IP público de saudação para sua VM.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. No computador local, abra uma conexão de SSH toohello VM.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Na sua VM, adicionar executar o arquivo de script de toohello de permissões.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Na sua VM, execute o ponto de recuperação de saudação do hello script toomount como um sistema de arquivos.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. Olá saída de hello script fornece que Olá o caminho para o ponto de montagem de saudação. saída de Hello parece semelhante toothis:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. Na sua VM, copie a página da web do hello nginx padrão do hello montagem ponto back toowhere você excluir o arquivo hello.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. No computador local, abra a guia do navegador de saudação em que você está conectado toohello endereço IP de saudação VM mostrando Olá nginx padrão a página. Pressione CTRL + F5 página do navegador Olá toorefresh. Agora, você verá que Olá página padrão está funcionando novamente.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

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

