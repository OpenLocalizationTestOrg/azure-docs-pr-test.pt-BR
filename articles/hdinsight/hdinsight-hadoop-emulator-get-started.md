---
title: "Aprender a usar uma área restrita do Hadoop – emulador – Azure HDInsight | Microsoft Docs"
description: "Para começar a aprender a usar o ecossistema Hadoop, você pode definir uma área restrita do Hadoop da Hortonworks em uma máquina virtual do Azure. "
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
ms.openlocfilehash: b701879464205860edd1c097651b532f87bae388
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-a-hadoop-sandbox-an-emulator-on-a-virtual-machine"></a><span data-ttu-id="a9f0b-104">Introdução a uma área restrita Hadoop, um emulador em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a9f0b-104">Get started with a Hadoop sandbox, an emulator on a virtual machine</span></span>

<span data-ttu-id="a9f0b-105">Saiba como instalar uma área restrita do Hadoop da Hortonworks em uma máquina virtual para saber mais sobre o ecossistema do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-105">Learn how to install the Hadoop sandbox from Hortonworks on a virtual machine to learn about the Hadoop ecosystem.</span></span> <span data-ttu-id="a9f0b-106">A área restrita fornece um ambiente de desenvolvimento local para saber mais sobre o Hadoop, o HDFS (Sistema de Arquivos Distribuído Hadoop) e o envio de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-106">The sandbox provides a local development environment to learn about Hadoop, Hadoop Distributed File System (HDFS), and job submission.</span></span> <span data-ttu-id="a9f0b-107">Quando estiver familiarizado com o Hadoop, você poderá começar a usar o Hadoop no Azure, criando um cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-107">Once you are familiar with Hadoop, you can start using Hadoop on Azure by creating an HDInsight cluster.</span></span> <span data-ttu-id="a9f0b-108">Para saber mais sobre como começar, confira [Introdução ao Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a9f0b-108">For more information on how to get started, see [Get started with Hadoop on HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9f0b-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a9f0b-109">Prerequisites</span></span>
* <span data-ttu-id="a9f0b-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span><span class="sxs-lookup"><span data-stu-id="a9f0b-110">[Oracle VirtualBox](https://www.virtualbox.org/).</span></span> <span data-ttu-id="a9f0b-111">Baixe-o e instale-o [aqui](https://www.virtualbox.org/wiki/Downloads).</span><span class="sxs-lookup"><span data-stu-id="a9f0b-111">Download and install it from [here](https://www.virtualbox.org/wiki/Downloads).</span></span>



## <a name="download-and-install-the-virtual-machine"></a><span data-ttu-id="a9f0b-112">Baixar e instalar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a9f0b-112">Download and install the virtual machine</span></span>
1. <span data-ttu-id="a9f0b-113">Navegue até os [downloads da Hortonworks](http://hortonworks.com/downloads/#sandbox).</span><span class="sxs-lookup"><span data-stu-id="a9f0b-113">Browse to the [Hortonworks downloads](http://hortonworks.com/downloads/#sandbox).</span></span>

2. <span data-ttu-id="a9f0b-114">Clique em **BAIXAR PARA VIRTUALBOX** para baixar a Área Restrita da Hortonworks mais recente em uma VM.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-114">Click **DOWNLOAD FOR VIRTUALBOX** to download the latest Hortonworks Sandbox on a VM.</span></span> <span data-ttu-id="a9f0b-115">Será solicitado que você se registre na Hortonworks antes de iniciar o download.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-115">You are prompted to register with Hortonworks before the download begins.</span></span> <span data-ttu-id="a9f0b-116">O download leva de uma a duas horas, dependendo da velocidade da sua rede.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-116">It takes one to two hours to download depending on your network speed.</span></span>
   
    ![Imagem de link para download da Hortonworks Sandbox para VirtualBox](./media/hdinsight-hadoop-emulator-get-started/download-sandbox.png)
3. <span data-ttu-id="a9f0b-118">Na mesma página da Web, clique no link **Import on Virtual Box** para baixar um PDF contendo instruções de instalação para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-118">From the same web page, click the **Import on Virtual Box** link to download a PDF containing installation instructions for the virtual machine.</span></span>

<span data-ttu-id="a9f0b-119">Para baixar uma área restrita da versão mais antiga do HDP, expanda o arquivamento:</span><span class="sxs-lookup"><span data-stu-id="a9f0b-119">To download an older HDP version sandbox, expand the archive:</span></span>

![Arquivamento da Área Restrita da Hortonworks](./media/hdinsight-hadoop-emulator-get-started/hortonworks-sandbox-archive.png)


## <a name="start-the-virtual-machine"></a><span data-ttu-id="a9f0b-121">Iniciar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="a9f0b-121">Start the virtual machine</span></span>

1. <span data-ttu-id="a9f0b-122">Abra o Oracle VM VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-122">Open Oracle VM VirtualBox.</span></span>
2. <span data-ttu-id="a9f0b-123">No menu **Arquivo**, clique em **Importar Dispositivo** e especifique a imagem da Área Restrita da Hortonworks.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-123">From the **File** menu, click **Import Appliance**, and then specify the Hortonworks Sandbox image.</span></span>
1. <span data-ttu-id="a9f0b-124">Selecione a Área Restrita da Hortonworks, clique em **Iniciar** e em **Início Normal**.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-124">Select the Hortonworks Sandbox, click **Start**, and then **Normal Start**.</span></span> <span data-ttu-id="a9f0b-125">Quando a máquina virtual tiver terminado o processo de inicialização, ela exibirá instruções de logon.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-125">Once the virtual machine has finished the boot process, it displays login instructions.</span></span>
   
    ![Início Normal](./media/hdinsight-hadoop-emulator-get-started/normal-start.png)
2. <span data-ttu-id="a9f0b-127">Abra um navegador da Web e acesse a URL exibida (geralmente http://127.0.0.1:8888).</span><span class="sxs-lookup"><span data-stu-id="a9f0b-127">Open a web browser and navigate to the URL displayed (usually http://127.0.0.1:8888).</span></span>

## <a name="set-sandbox-passwords"></a><span data-ttu-id="a9f0b-128">Definir senhas da Área Restrita</span><span class="sxs-lookup"><span data-stu-id="a9f0b-128">Set Sandbox passwords</span></span>

1. <span data-ttu-id="a9f0b-129">Na etapa de **introdução** da página da Hortonworks Sandbox, selecione **Exibir Opções Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-129">From the **get started** step of the Hortonworks Sandbox page, select **View Advanced Options**.</span></span> <span data-ttu-id="a9f0b-130">Use as informações desta página para fazer logon na área restrita usando SSH.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-130">Use the information on this page to log in to the sandbox using SSH.</span></span> <span data-ttu-id="a9f0b-131">Use o nome e a senha fornecidos.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-131">Use the name and password provided.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9f0b-132">Se você não tiver um cliente SSH instalado, use o SSH baseado na Web fornecido pela máquina virtual em **http://localhost:4200/**.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-132">If you do not have an SSH client installed, you can use the web-based SSH provided at by the virtual machine at **http://localhost:4200/**.</span></span>
   > 
   
    <span data-ttu-id="a9f0b-133">Na primeira vez que você se conectar usando SSH, você receberá uma solicitação para alterar a senha da conta raiz.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-133">The first time you connect using SSH, you are prompted to change the password for the root account.</span></span> <span data-ttu-id="a9f0b-134">Insira uma nova senha, que você usa quando faz logon usando SSH.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-134">Enter a new password, which you use when you log in using SSH.</span></span>

2. <span data-ttu-id="a9f0b-135">Depois de conectado, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a9f0b-135">Once logged in, enter the following command:</span></span>
   
        ambari-admin-password-reset
   
    <span data-ttu-id="a9f0b-136">Quando receber uma solicitação, forneça uma senha para a conta de administrador do Ambari.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-136">When prompted, provide a password for the Ambari admin account.</span></span> <span data-ttu-id="a9f0b-137">Isso é usado quando você acessa a interface do usuário da Web do Ambari.</span><span class="sxs-lookup"><span data-stu-id="a9f0b-137">This is used when you access the Ambari Web UI.</span></span>

## <a name="use-hive-commands"></a><span data-ttu-id="a9f0b-138">Usar comandos do Hive</span><span class="sxs-lookup"><span data-stu-id="a9f0b-138">Use Hive commands</span></span>

1. <span data-ttu-id="a9f0b-139">De uma conexão SSH com a área restrita, use o seguinte comando para iniciar o shell do Hive:</span><span class="sxs-lookup"><span data-stu-id="a9f0b-139">From an SSH connection to the sandbox, use the following command to start the Hive shell:</span></span>
   
        hive
2. <span data-ttu-id="a9f0b-140">Quando o shell for iniciado, use o seguinte para exibir as tabelas que são fornecidas com a área restrita:</span><span class="sxs-lookup"><span data-stu-id="a9f0b-140">Once the shell has started, use the following to view the tables that are provided with the sandbox:</span></span>
   
        show tables;
3. <span data-ttu-id="a9f0b-141">Use o seguinte para recuperar 10 linhas da tabela `sample_07` :</span><span class="sxs-lookup"><span data-stu-id="a9f0b-141">Use the following to retrieve 10 rows from the `sample_07` table:</span></span>
   
        select * from sample_07 limit 10;

## <a name="next-steps"></a><span data-ttu-id="a9f0b-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a9f0b-142">Next steps</span></span>
* [<span data-ttu-id="a9f0b-143">Aprenda a usar o Visual Studio com a Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="a9f0b-143">Learn how to use Visual Studio with the Hortonworks Sandbox</span></span>](hdinsight-hadoop-emulator-visual-studio.md)
* [<span data-ttu-id="a9f0b-144">Learning the ropes of the Hortonworks Sandbox</span><span class="sxs-lookup"><span data-stu-id="a9f0b-144">Learning the ropes of the Hortonworks Sandbox</span></span>](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [<span data-ttu-id="a9f0b-145">Hadoop tutorial - Getting started with HDP</span><span class="sxs-lookup"><span data-stu-id="a9f0b-145">Hadoop tutorial - Getting started with HDP</span></span>](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)

