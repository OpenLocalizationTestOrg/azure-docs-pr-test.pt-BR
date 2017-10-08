---
title: "aaaLearn usando uma área restrita de Hadoop - emulador - HDInsight do Azure | Microsoft Docs"
description: "toostart sobre o uso de aprendizado Olá ecossistema de Hadoop, você pode configurar uma proteção de Hadoop de Hortonworks em uma máquina virtual do Azure. "
keywords: "emulador do hadoop,área restrita do hadoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
author: nitinme
documentationcenter: 
tags: azure-portal
ms.assetid: 6ad5bb58-8215-4e3d-a07f-07fcd8839cc6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 91e74f0823fd02e9bb812155a7d09357a77b0736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a>Introdução a uma área restrita Hadoop, um emulador em uma máquina virtual

Saiba como tooinstall Olá área restrita do Hadoop de Hortonworks em um toolearn de máquina virtual sobre o ecossistema de Hadoop hello. área restrita do Hello fornece um toolearn do ambiente de desenvolvimento local sobre o Hadoop, o sistema de arquivos distribuído da Hadoop (HDFS) e o envio de trabalho. Quando estiver familiarizado com o Hadoop, você poderá começar a usar o Hadoop no Azure, criando um cluster do HDInsight. Para obter mais informações sobre como começar a tooget, consulte [começar com Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

## <a name="prerequisites"></a>Pré-requisitos
* [Oracle VirtualBox](https://www.virtualbox.org/). Baixe-o e instale-o [aqui](https://www.virtualbox.org/wiki/Downloads).



## <a name="download-and-install-hello-virtual-machine"></a>Baixe e instale a máquina virtual de saudação
1. Procurar toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).

2. Clique em **baixar para VIRTUALBOX** toodownload hello mais recente Hortonworks Sandbox em uma máquina virtual. Você está tooregister solicitado com Hortonworks antes de iniciar o download de saudação. Ele usa um toodownload de horas tootwo dependendo da velocidade da rede.
   
    ![Imagem de link para download da Hortonworks Sandbox para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. De hello a mesma página da web, clique em Olá **importação na caixa Virtual** link toodownload um PDF que contém instruções de instalação para a máquina virtual de saudação.

toodownload uma proteção de versão mais antiga do HDP, expanda o arquivo hello:

![Arquivamento da Área Restrita da Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a>Iniciar a máquina virtual de saudação

1. Abra o Oracle VM VirtualBox.
2. De saudação **arquivo** menu, clique em **importação Appliance**e, em seguida, especificar Olá imagem Hortonworks seguro.
1. Selecione Olá Hortonworks seguro, clique **iniciar**e, em seguida, **Normal iniciar**. Depois que a máquina virtual de saudação concluiu o processo de inicialização hello, ele exibe instruções de logon.
   
    ![Início Normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. Abra um navegador da web e navegue toohello URL exibida (geralmente http://127.0.0.1:8888).

## <a name="set-sandbox-passwords"></a>Definir senhas da Área Restrita

1. De saudação **começar** etapa Olá página Hortonworks de proteção, selecione **opções avançadas de exibição**. Use informações de saudação toolog esta página em área restrita do toohello usando o SSH. Use Olá nome e senha fornecidos.
   
   > [!NOTE]
   > Se você não tiver um cliente SSH instalado, você pode usar o hello SSH baseado na web é fornecido por máquina virtual de saudação em **http://localhost:4200 /**.
   > 
   
    Olá primeira vez que você se conectar usando SSH, você é solicitadas toochange Olá senha para conta de raiz de saudação. Insira uma nova senha, que você usa quando faz logon usando SSH.

2. Depois de conectado, digite Olá comando a seguir:
   
        ambari-admin-password-reset
   
    Quando solicitado, forneça uma senha para Olá Ambari conta de administrador. Isso é usado quando você acessa a saudação da interface do usuário do Ambari Web.

## <a name="use-hive-commands"></a>Usar comandos do Hive

1. De uma área de segurança de toohello conexão SSH, use Olá shell de comando do toostart Olá seção a seguir:
   
        hive
2. Após o início de shell Olá use Olá tooview Olá tabelas que são fornecidas com a área restrita de saudação seguintes:
   
        show tables;
3. Saudação de uso a seguir tooretrieve 10 linhas de saudação `sample_07` tabela:
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a>Próximas etapas
* [Saiba como toouse Visual Studio com hello Hortonworks seguro](hdinsight-hadoop-emulator-visual-studio.md)
* [Aprendizado ropes de saudação do hello Hortonworks seguro](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

