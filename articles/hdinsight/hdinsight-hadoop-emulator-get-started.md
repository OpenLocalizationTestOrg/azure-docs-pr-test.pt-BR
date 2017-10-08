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
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="83b62-104">Introdução a uma área restrita Hadoop, um emulador em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="83b62-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="83b62-105">Saiba como tooinstall Olá área restrita do Hadoop de Hortonworks em um toolearn de máquina virtual sobre o ecossistema de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="83b62-105">Learn how tooinstall hello Hadoop sandbox from Hortonworks on a virtual machine toolearn about hello Hadoop ecosystem.</span></span> <span data-ttu-id="83b62-106">área restrita do Hello fornece um toolearn do ambiente de desenvolvimento local sobre o Hadoop, o sistema de arquivos distribuído da Hadoop (HDFS) e o envio de trabalho.</span><span class="sxs-lookup"><span data-stu-id="83b62-106">hello sandbox provides a local development environment toolearn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="83b62-107">Quando estiver familiarizado com o Hadoop, você poderá começar a usar o Hadoop no Azure, criando um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="83b62-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="83b62-108">Para obter mais informações sobre como começar a tooget, consulte [começar com Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83b62-108">For more information on how tooget started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83b62-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="83b62-109">Prerequisites</span></span>
* <span data-ttu-id="83b62-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="83b62-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="83b62-111">Baixe-o e instale-o [aqui](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="83b62-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-hello-virtual-machine"></a><span data-ttu-id="83b62-112">Baixe e instale a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="83b62-112">Download and install hello virtual machine</span></span>
1. <span data-ttu-id="83b62-113">Procurar toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="83b62-113">Browse toohello [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="83b62-114">Clique em **baixar para VIRTUALBOX** toodownload hello mais recente Hortonworks Sandbox em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="83b62-114">Click **DOWNLOAD FOR VIRTUALBOX** toodownload hello latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="83b62-115">Você está tooregister solicitado com Hortonworks antes de iniciar o download de saudação.</span><span class="sxs-lookup"><span data-stu-id="83b62-115">You are prompted tooregister with Hortonworks before hello download begins.</span></span> <span data-ttu-id="83b62-116">Ele usa um toodownload de horas tootwo dependendo da velocidade da rede.</span><span class="sxs-lookup"><span data-stu-id="83b62-116">It takes one tootwo hours toodownload depending on your network speed.</span></span>
   
    ![Imagem de link para download da Hortonworks Sandbox para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="83b62-118">De hello a mesma página da web, clique em Olá **importação na caixa Virtual** link toodownload um PDF que contém instruções de instalação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="83b62-118">From hello same web page, click hello **Import on Virtual Box** link toodownload a PDF containing installation instructions for hello virtual machine.</span></span>

<span data-ttu-id="83b62-119">toodownload uma proteção de versão mais antiga do HDP, expanda o arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="83b62-119">toodownload an older HDP version sandbox, expand hello archive:</span></span>

![Arquivamento da Área Restrita da Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-hello-virtual-machine"></a><span data-ttu-id="83b62-121">Iniciar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="83b62-121">Start hello virtual machine</span></span>

1. <span data-ttu-id="83b62-122">Abra o Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="83b62-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="83b62-123">De saudação **arquivo** menu, clique em **importação Appliance**e, em seguida, especificar Olá imagem Hortonworks seguro.</span><span class="sxs-lookup"><span data-stu-id="83b62-123">From hello **File** menu, click **Import Appliance**, and then specify hello Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="83b62-124">Selecione Olá Hortonworks seguro, clique **iniciar**e, em seguida, **Normal iniciar**.</span><span class="sxs-lookup"><span data-stu-id="83b62-124">Select hello Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="83b62-125">Depois que a máquina virtual de saudação concluiu o processo de inicialização hello, ele exibe instruções de logon.</span><span class="sxs-lookup"><span data-stu-id="83b62-125">Once hello virtual machine has finished hello boot process, it displays login instructions.</span></span>
   
    ![Início Normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="83b62-127">Abra um navegador da web e navegue toohello URL exibida (geralmente http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="83b62-127">Open a web browser and navigate toohello URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="83b62-128">Definir senhas da Área Restrita</span><span class="sxs-lookup"><span data-stu-id="83b62-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="83b62-129">De saudação **começar** etapa Olá página Hortonworks de proteção, selecione **opções avançadas de exibição**.</span><span class="sxs-lookup"><span data-stu-id="83b62-129">From hello **get started** step of hello Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="83b62-130">Use informações de saudação toolog esta página em área restrita do toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="83b62-130">Use hello information on this page toolog in toohello sandbox using SSH.</span></span> <span data-ttu-id="83b62-131">Use Olá nome e senha fornecidos.</span><span class="sxs-lookup"><span data-stu-id="83b62-131">Use hello name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83b62-132">Se você não tiver um cliente SSH instalado, você pode usar o hello SSH baseado na web é fornecido por máquina virtual de saudação em **http://localhost:4200 /**.</span><span class="sxs-lookup"><span data-stu-id="83b62-132">If you do not have an SSH client installed, you can use hello web-based SSH provided at by hello virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="83b62-133">Olá primeira vez que você se conectar usando SSH, você é solicitadas toochange Olá senha para conta de raiz de saudação.</span><span class="sxs-lookup"><span data-stu-id="83b62-133">hello first time you connect using SSH, you are prompted toochange hello password for hello root account.</span></span> <span data-ttu-id="83b62-134">Insira uma nova senha, que você usa quando faz logon usando SSH.</span><span class="sxs-lookup"><span data-stu-id="83b62-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="83b62-135">Depois de conectado, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="83b62-135">Once logged in, enter hello following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="83b62-136">Quando solicitado, forneça uma senha para Olá Ambari conta de administrador.</span><span class="sxs-lookup"><span data-stu-id="83b62-136">When prompted, provide a password for hello Ambari admin account.</span></span> <span data-ttu-id="83b62-137">Isso é usado quando você acessa a saudação da interface do usuário do Ambari Web.</span><span class="sxs-lookup"><span data-stu-id="83b62-137">This is used when you access hello Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="83b62-138">Usar comandos do Hive</span><span class="sxs-lookup"><span data-stu-id="83b62-138">Use Hive commands</span></span>

1. <span data-ttu-id="83b62-139">De uma área de segurança de toohello conexão SSH, use Olá shell de comando do toostart Olá seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="83b62-139">From an SSH connection toohello sandbox, use hello following command toostart hello Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="83b62-140">Após o início de shell Olá use Olá tooview Olá tabelas que são fornecidas com a área restrita de saudação seguintes:</span><span class="sxs-lookup"><span data-stu-id="83b62-140">Once hello shell has started, use hello following tooview hello tables that are provided with hello sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="83b62-141">Saudação de uso a seguir tooretrieve 10 linhas de saudação `sample_07` tabela:</span><span class="sxs-lookup"><span data-stu-id="83b62-141">Use hello following tooretrieve 10 rows from hello `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="83b62-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83b62-142">Next steps</span></span>
* [<span data-ttu-id="83b62-143">Saiba como toouse Visual Studio com hello Hortonworks seguro</span><span class="sxs-lookup"><span data-stu-id="83b62-143">Learn how toouse Visual Studio with hello Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="83b62-144">Aprendizado ropes de saudação do hello Hortonworks seguro</span><span class="sxs-lookup"><span data-stu-id="83b62-144">Learning hello ropes of hello Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="83b62-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="83b62-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

