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
ms.topic: tutorial
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2eb0958169b175813b0dca775e9250da1cb364d4
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="back-up-linux--virtual-machines-in-azure"></a>Fazer backup de máquinas virtuais do Linux no Azure

Você pode proteger seus dados fazendo backups em intervalos regulares. O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica. Ao restaurar de um ponto de recuperação, você pode restaurar a VM inteira ou apenas arquivos específicos. Este artigo explica como restaurar um único arquivo em uma VM do Linux que executa o nginx. Se você ainda não tem uma VM para usar, você pode criar uma usando o [Início rápido do Linux](quick-create-cli.md). Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar um backup de uma VM
> * Agendar um backup diário
> * Restaurar um arquivo de um backup



## <a name="backup-overview"></a>Visão geral do backup

Quando o serviço de Backup do Azure inicia um backup, ele dispara a extensão de backup para obter um instantâneo pontual. O serviço de Backup do Azure usa a extensão _VMSnapshotLinux_ no Linux. A extensão é instalada durante o primeiro backup de VM se a VM está em execução. Se a VM não estiver em execução, o serviço de Backup criará um instantâneo do armazenamento subjacente (já que nenhuma gravação de aplicativo ocorre enquanto a VM está parada).

Por padrão, o Backup do Azure usa um backup consistente de sistema de arquivos para a VM do Linux, mas ele pode ser configurado para fazer um [backup consistente de aplicativos usando a estrutura de pré e pós-script](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). Depois que o serviço de Backup do Azure gera o instantâneo, os dados são transferidos para o cofre. Para maximizar a eficiência, o serviço identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior.

Quando a transferência de dados é concluída, o instantâneo é removido e um ponto de recuperação é criado.


## <a name="create-a-backup"></a>Criar um backup
Crie um backup diário agendado simples em um Cofre de Serviços de Recuperação. 

1. Entre no [portal do Azure](https://portal.azure.com/).
2. No menu à esquerda, selecione **Máquinas virtuais**. 
3. Na lista, selecione uma VM da qual fazer backup.
4. Na folha da VM, na seção **Configurações**, clique em **Backup**. A folha **Habilitar backup** é aberta.
5. Em **Cofre de Serviços de Recuperação**, clique em **Criar novo** e forneça o nome para o novo cofre. Um novo cofre é criado no mesmo Grupo de Recursos e na mesma localização que a máquina virtual.
6. Clique em **Política de backup**. Para este exemplo, mantenha os padrões e clique em **OK**.
7. Na folha **Habilitar backup**, clique em **Habilitar Backup**. Isso cria um backup diário com base no agendamento padrão.
10. Para criar um ponto de recuperação inicial, na folha **Backup**, clique em **Fazer backup agora**.
11. Na folha **Fazer Backup Agora**, clique no ícone de calendário, use o controle de calendário para selecionar o último dia de retenção desse ponto de recuperação e clique em **Fazer Backup**.
12. Na folha **Backup** de sua VM, você verá o número de pontos de recuperação completos.

    ![Pontos de Recuperação](./media/tutorial-backup-vms/backup-complete.png)

O primeiro backup leva aproximadamente 20 minutos. Prossiga para a próxima parte deste tutorial depois que o backup for concluído.

## <a name="restore-a-file"></a>Restaurar um arquivo

Se você acidentalmente excluir ou fizer alterações em um arquivo, você poderá usar a recuperação de arquivo para recuperar o arquivo de seu cofre de backup. A Recuperação de Arquivo utiliza um script que é executado na VM para montar o ponto de recuperação como uma unidade local. Essas unidades permanecerão montadas por 12 horas para que você possa copiar arquivos do ponto de recuperação e restaurá-los para a VM.  

Neste exemplo, mostramos como recuperar a página Web do nginx padrão /var/www/html/index.nginx-debian.html. O endereço IP público de nossa VM neste exemplo é *13.69.75.209*. Encontre o endereço IP da sua vm usando:

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. No computador local, abra um navegador e digite o endereço IP público de sua VM para ver a página Web do nginx padrão.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

1. SSH em sua VM.

    ```bash
    ssh 13.69.75.209
    ```
2. Exclua /var/www/html/index.nginx-debian.html.

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. No computador local, atualize o navegador teclando em CTRL + F5 para ver se a página padrão do nginx foi removida.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-broken.png)
    
1. No computador local, entre no [Portal do Azure](https://portal.azure.com/).
6. No menu à esquerda, selecione **Máquinas virtuais**. 
7. Selecione a VM na lista.
8. Na folha da VM, na seção **Configurações**, clique em **Backup**. A folha **Backup** é aberta. 
9. No menu na parte superior da folha, selecione **Recuperação de Arquivo**. A folha **Recuperação de arquivo** será aberta.
10. Em **Etapa 1: selecionar um ponto de recuperação**, selecione um ponto de recuperação do menu suspenso.
11. Em **Etapa 2: baixar o script para procurar e recuperar arquivos**, clique no botão **Baixar Executável**. Salve o arquivo baixado em seu computador local.
7. Clique em **Baixar script** para baixar o arquivo de script localmente.
8. Abra um prompt Bash e digite o seguinte, substituindo *Linux_myVM_05-05-2017.sh* pelo caminho e o nome de arquivo do script que você baixou, *azureuser* pelo nome de usuário da VM e *13.69.75.209* pelo endereço IP público de sua VM.
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. No computador local, abra uma conexão SSH para a VM.

    ```bash
    ssh 13.69.75.209
    ```
    
10. Em sua VM, adicione permissões de execução ao arquivo de script.

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. Em sua VM, execute o script para montar o ponto de recuperação como um sistema de arquivos.

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. A saída do script fornece o caminho para o ponto de montagem. A saída deve ser semelhante a esta:

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
                         
    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

12. Em sua VM, copie a página Web nginx padrão do ponto de montagem para o local onde você excluiu o arquivo.

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. No computador local, abra a guia do navegador em que você está conectado ao endereço IP da VM mostrando a página padrão do nginx. Pressione CTRL + F5 para atualizar a página do navegador. Agora você verá que a página padrão está funcionando novamente.

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

18. No computador local, volte para a guia do navegador para o Portal do Azure e, na **Etapa 3: desmontar discos após a recuperação**, clique no botão **Desmontar Discos**. Se você esquecer de fazer isso, a conexão para o ponto de montagem será fechada automaticamente após 12 horas. Após essas 12 horas, você precisa baixar um novo script para criar um novo ponto de montagem.


## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar um backup de uma VM
> * Agendar um backup diário
> * Restaurar um arquivo de um backup

Avance para o próximo tutorial para saber mais sobre o monitoramento de máquinas virtuais.

> [!div class="nextstepaction"]
> [Monitorar máquinas virtuais](tutorial-monitoring.md)

