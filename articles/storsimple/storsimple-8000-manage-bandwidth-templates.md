---
title: "Gerenciar modelos de largura de banda para StorSimple série 8000 | Microsoft Docs"
description: Descreve como gerenciar modelos de largura do StorSimple, que permitem controlar o consumo da largura de banda.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 50d0a920bef097013feddc828d2c37133b9057b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="8da4c-103">Usar o serviço do Gerenciador de Dispositivos do StorSimple para gerenciar modelos de largura de banda do StorSimple</span><span class="sxs-lookup"><span data-stu-id="8da4c-103">Use the StorSimple Device Manager service to manage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="8da4c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8da4c-104">Overview</span></span>

<span data-ttu-id="8da4c-105">Os modelos de largura de banda permitem configurar a largura de banda de rede em várias agendas do dia para dispor os dados do dispositivo StorSimple em camadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8da4c-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="8da4c-106">Com agendas de limitação da largura de banda, você pode:</span><span class="sxs-lookup"><span data-stu-id="8da4c-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="8da4c-107">Especifica as agendas de largura de banda personalizadas dependendo dos usos da rede de carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8da4c-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="8da4c-108">Centralizar o gerenciamento e reutilizar as agendas em vários dispositivos de uma maneira fácil e direta.</span><span class="sxs-lookup"><span data-stu-id="8da4c-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="8da4c-109">Este recurso está disponível somente para dispositivos físicos StorSimple (modelos 8100 e 8600) e não para Dispositivos de Nuvem StorSimple (modelos 8010 e 8020).</span><span class="sxs-lookup"><span data-stu-id="8da4c-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="the-bandwidth-templates-blade"></a><span data-ttu-id="8da4c-110">A folha Modelos de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-110">The Bandwidth templates blade</span></span>

<span data-ttu-id="8da4c-111">A folha **Modelos de largura de banda** apresenta todos os modelos de largura de banda para seu serviço exibidos em um formato tabular e contêm as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8da4c-111">The **Bandwidth templates** blade has all the bandwidth templates for your service in a tabular format, and contains the following information:</span></span>

* <span data-ttu-id="8da4c-112">**Nome** : um nome exclusivo atribuído ao modelo de largura de banda quando ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="8da4c-112">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="8da4c-113">**Agenda** : o número de agendas contidas em um determinado modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-113">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="8da4c-114">**Usado por** : o número de volumes usando os modelos de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-114">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="8da4c-115">Você também pode encontrar informações adicionais que ajudam a configurar modelos de largura de banda em:</span><span class="sxs-lookup"><span data-stu-id="8da4c-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* [<span data-ttu-id="8da4c-116">Perguntas e respostas sobre modelos de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="8da4c-117">Práticas recomendadas para modelos de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="8da4c-118">Adicionar um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-118">Add a bandwidth template</span></span>

<span data-ttu-id="8da4c-119">Execute as etapas a seguir para criar um novo modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="8da4c-120">Para adicionar um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-120">To add a bandwidth template</span></span>

1. <span data-ttu-id="8da4c-121">Acesse o serviço do Gerenciador de Dispositivos do StorSimple, clique em **Modelos de largura de banda** e em **+ Adicionar modelo de largura de banda**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-121">Go to your StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![Clique em + Adicionar modelo de largura de banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="8da4c-123">Na folha **Adicionar modelo de largura de banda**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8da4c-123">In the **Add bandwidth template** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="8da4c-124">Especifique um nome exclusivo para o modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="8da4c-125">Defina uma agenda de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="8da4c-126">Para criar uma agenda:</span><span class="sxs-lookup"><span data-stu-id="8da4c-126">To create a schedule:</span></span>
   
        1. <span data-ttu-id="8da4c-127">Na lista suspensa, escolha os **Dias** da semana para os quais a agenda será configurada.</span><span class="sxs-lookup"><span data-stu-id="8da4c-127">From the drop-down list, choose the **Days** of the week the schedule is configured for.</span></span> <span data-ttu-id="8da4c-128">É possível selecionar vários dias.</span><span class="sxs-lookup"><span data-stu-id="8da4c-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="8da4c-129">Insira uma **Hora Inicial** no formato _hh:mm_.</span><span class="sxs-lookup"><span data-stu-id="8da4c-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="8da4c-130">Essa é a hora em que a agenda será iniciada.</span><span class="sxs-lookup"><span data-stu-id="8da4c-130">This is when the schedule will begin.</span></span>

        3. <span data-ttu-id="8da4c-131">Insira uma **Hora Final** no formato _hh:mm_.</span><span class="sxs-lookup"><span data-stu-id="8da4c-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="8da4c-132">Essa é a hora em que a agenda será encerrada.</span><span class="sxs-lookup"><span data-stu-id="8da4c-132">This is when the schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="8da4c-133">Não há permissão para os agendamentos sobrepostos.</span><span class="sxs-lookup"><span data-stu-id="8da4c-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="8da4c-134">Se as horas de início e término resultarem em um agendamento sobreposto, você verá uma mensagem de erro sobre isso.</span><span class="sxs-lookup"><span data-stu-id="8da4c-134">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>

        4. <span data-ttu-id="8da4c-135">Especifique a **Taxa da Largura de Banda**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-135">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="8da4c-136">Essa é a largura de banda em Megabits por segundo (Mbps) usada pelo dispositivo StorSimple em operações que envolvem a nuvem (uploads e downloads).</span><span class="sxs-lookup"><span data-stu-id="8da4c-136">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="8da4c-137">Forneça um número entre 1 e 1.000 para esse campo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![Defina uma agenda de largura de banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="8da4c-139">Repita as etapas acima para definir várias agendas para seu modelo até terminar.</span><span class="sxs-lookup"><span data-stu-id="8da4c-139">Repeat the above steps to define multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="8da4c-140">Clique em **Adicionar** para começar a criar um modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-140">Click **Add** to start creating a bandwidth template.</span></span> <span data-ttu-id="8da4c-141">O modelo criado é adicionado à lista de modelos de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-141">The created template is added to the list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="8da4c-142">Editar um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-142">Edit a bandwidth template</span></span>

<span data-ttu-id="8da4c-143">Execute as etapas a seguir para editar um modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-143">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="8da4c-144">Para editar um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-144">To edit a bandwidth template</span></span>

1. <span data-ttu-id="8da4c-145">Acesse o serviço do Gerenciador de Dispositivos do StorSimple e clique em **Modelos de largura de banda**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-145">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="8da4c-146">Na lista de modelos de largura de banda, selecione o modelo que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="8da4c-146">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="8da4c-147">Clique com botão direito do mouse e no menu de contexto, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-147">Right-click and from the context menu, select **Delete**.</span></span>
3. <span data-ttu-id="8da4c-148">Quando sua confirmação for solicitada, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="8da4c-149">Isso excluirá o modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-149">This should delete the bandwidth template.</span></span> 
4. <span data-ttu-id="8da4c-150">A lista de modelos de largura de banda é atualizada para refletir a exclusão.</span><span class="sxs-lookup"><span data-stu-id="8da4c-150">The list of bandwidth templates updates to reflect the deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="8da4c-151">Você não poderá salvar as alterações se a agenda editada se sobrepor a uma agenda existente no modelo de largura de banda que você está modificando.</span><span class="sxs-lookup"><span data-stu-id="8da4c-151">You cannot save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="8da4c-152">Excluir um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-152">Delete a bandwidth template</span></span>

<span data-ttu-id="8da4c-153">Execute as etapas a seguir para excluir um modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-153">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="8da4c-154">Para excluir um modelo de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-154">To delete a bandwidth template</span></span>

1. <span data-ttu-id="8da4c-155">Acesse o serviço do Gerenciador de Dispositivos do StorSimple e clique em **Modelos de largura de banda**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-155">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="8da4c-156">Na lista de modelos de largura de banda, selecione o modelo que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="8da4c-156">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="8da4c-157">Clique com botão direito do mouse e, no menu de contexto, selecione Excluir.</span><span class="sxs-lookup"><span data-stu-id="8da4c-157">Right-click and from the context menu, select Delete.</span></span>
3. <span data-ttu-id="8da4c-158">Quando sua confirmação for solicitada, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="8da4c-159">Isso excluirá o modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-159">This should delete the bandwidth template.</span></span>
4. <span data-ttu-id="8da4c-160">A lista de modelos de largura de banda é atualizada para refletir a exclusão.</span><span class="sxs-lookup"><span data-stu-id="8da4c-160">The list of bandwidth templates updates to reflect the deletion.</span></span>

<span data-ttu-id="8da4c-161">Se o modelo estiver sendo usado por algum volume, você não poderá excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-161">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="8da4c-162">Você verá uma mensagem de erro indicando que o modelo está em uso.</span><span class="sxs-lookup"><span data-stu-id="8da4c-162">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="8da4c-163">Uma caixa de diálogo de mensagem de erro será exibida avisando que todas as referências ao modelo devem ser removidas.</span><span class="sxs-lookup"><span data-stu-id="8da4c-163">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="8da4c-164">É possível excluir todas as referências ao modelo acessando a página **Contêineres de Volume** e modificando os contêineres de volume que usam esse modelo para que eles usem outro modelo ou usem uma configuração de largura de banda personalizada ou ilimitada.</span><span class="sxs-lookup"><span data-stu-id="8da4c-164">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="8da4c-165">Quando todas as referências forem removidas, você poderá excluir o modelo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-165">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="8da4c-166">Usar um modelo de largura de banda padrão</span><span class="sxs-lookup"><span data-stu-id="8da4c-166">Use a default bandwidth template</span></span>

<span data-ttu-id="8da4c-167">Um modelo de largura de banda padrão é fornecido e usado pelos contêineres de volume, por padrão, para impor controles de largura de banda durante o acesso à nuvem.</span><span class="sxs-lookup"><span data-stu-id="8da4c-167">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="8da4c-168">O modelo padrão também serve como uma referência pronta para os usuários que criam seus próprios modelos.</span><span class="sxs-lookup"><span data-stu-id="8da4c-168">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="8da4c-169">Os detalhes desse modelo padrão são:</span><span class="sxs-lookup"><span data-stu-id="8da4c-169">The details of this default template are:</span></span>

* <span data-ttu-id="8da4c-170">**Nome** : noites e fins de semana ilimitados</span><span class="sxs-lookup"><span data-stu-id="8da4c-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="8da4c-171">**Agenda** : uma única agenda de segunda-feira a sexta-feira que se aplica a uma taxa de largura de banda de 1 Mbps no horário das 8:00 às 17:00 do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-171">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="8da4c-172">A largura de banda é definida como Ilimitada para o restante da semana.</span><span class="sxs-lookup"><span data-stu-id="8da4c-172">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="8da4c-173">O modelo padrão pode ser editado.</span><span class="sxs-lookup"><span data-stu-id="8da4c-173">The default template can be edited.</span></span> <span data-ttu-id="8da4c-174">O uso desse modelo (incluindo versões editadas) é rastreado.</span><span class="sxs-lookup"><span data-stu-id="8da4c-174">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="8da4c-175">Criar um modelo de largura de banda de dia inteiro que comece em uma hora especificada</span><span class="sxs-lookup"><span data-stu-id="8da4c-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="8da4c-176">Siga este procedimento para criar uma agenda que comece em uma hora especificada e seja executada o dia todo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-176">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="8da4c-177">No exemplo, a agenda inicia às 9:00 e é executada até às 9:00 do dia seguinte.</span><span class="sxs-lookup"><span data-stu-id="8da4c-177">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="8da4c-178">É importante observar que as horas de início e término de uma determinada agenda devem estar contidas na mesma agenda de 24 horas e não podem abranger vários dias.</span><span class="sxs-lookup"><span data-stu-id="8da4c-178">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="8da4c-179">Se precisar configurar modelos de largura de banda que se estendam por vários dias, você precisará usar várias agendas (conforme mostrado no exemplo).</span><span class="sxs-lookup"><span data-stu-id="8da4c-179">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="8da4c-180">Para criar um modelo de largura de banda de dia inteiro</span><span class="sxs-lookup"><span data-stu-id="8da4c-180">To create an all-day bandwidth template</span></span>

1. <span data-ttu-id="8da4c-181">Crie uma agenda que inicie às 9:00 e seja executada até a meia-noite.</span><span class="sxs-lookup"><span data-stu-id="8da4c-181">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="8da4c-182">Adicione outra agenda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-182">Add another schedule.</span></span> <span data-ttu-id="8da4c-183">Configure a segunda agenda para execução da meia-noite até às 9:00.</span><span class="sxs-lookup"><span data-stu-id="8da4c-183">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="8da4c-184">Salve o modelo de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-184">Save the bandwidth template.</span></span>

<span data-ttu-id="8da4c-185">A agenda composta terá início na hora de sua escolha e será executa o dia todo.</span><span class="sxs-lookup"><span data-stu-id="8da4c-185">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="8da4c-186">Perguntas e respostas sobre modelos de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="8da4c-187">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-187">**Q**.</span></span> <span data-ttu-id="8da4c-188">O que acontece aos controles de largura de banda quando você está entre as agendas?</span><span class="sxs-lookup"><span data-stu-id="8da4c-188">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="8da4c-189">(Uma agenda foi encerrada e outra ainda não foi iniciada.)</span><span class="sxs-lookup"><span data-stu-id="8da4c-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="8da4c-190">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-190">**A**.</span></span> <span data-ttu-id="8da4c-191">Nesses casos, nenhum controle de largura de banda será utilizado.</span><span class="sxs-lookup"><span data-stu-id="8da4c-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="8da4c-192">Isso significa que o dispositivo pode usar a largura de banda ilimitada ao dispor dados em camadas na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8da4c-192">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="8da4c-193">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-193">**Q**.</span></span> <span data-ttu-id="8da4c-194">Você pode modificar os modelos de largura de banda em um dispositivo offline?</span><span class="sxs-lookup"><span data-stu-id="8da4c-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="8da4c-195">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-195">**A**.</span></span> <span data-ttu-id="8da4c-196">Você não poderá modificar os modelos de largura de banda em contêineres de volumes se o dispositivo correspondente estiver offline.</span><span class="sxs-lookup"><span data-stu-id="8da4c-196">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="8da4c-197">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-197">**Q**.</span></span> <span data-ttu-id="8da4c-198">Você pode editar um modelo de largura de banda associado a um contêiner de volume quando os volumes associados estão offline?</span><span class="sxs-lookup"><span data-stu-id="8da4c-198">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="8da4c-199">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-199">**A**.</span></span> <span data-ttu-id="8da4c-200">Você pode modificar um modelo de largura de banda associado a um contêiner de volume cujos volumes estejam offline.</span><span class="sxs-lookup"><span data-stu-id="8da4c-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="8da4c-201">Observe que quando os volumes estiverem offline, nenhum dado será disposto em camadas do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="8da4c-201">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="8da4c-202">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-202">**Q**.</span></span> <span data-ttu-id="8da4c-203">Você pode excluir um modelo padrão?</span><span class="sxs-lookup"><span data-stu-id="8da4c-203">Can you delete a default template?</span></span>

<span data-ttu-id="8da4c-204">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-204">**A**.</span></span> <span data-ttu-id="8da4c-205">Embora você possa excluir um modelo padrão, não é uma boa ideia fazer isso.</span><span class="sxs-lookup"><span data-stu-id="8da4c-205">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="8da4c-206">O uso de um modelo padrão, incluindo versões editadas, é rastreado.</span><span class="sxs-lookup"><span data-stu-id="8da4c-206">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="8da4c-207">Os dados de rastreamento são analisados e, ao longo do tempo, são usados para melhorar o modelo padrão.</span><span class="sxs-lookup"><span data-stu-id="8da4c-207">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="8da4c-208">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-208">**Q**.</span></span> <span data-ttu-id="8da4c-209">Como determinar se seus modelos de largura de banda precisam ser modificados?</span><span class="sxs-lookup"><span data-stu-id="8da4c-209">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="8da4c-210">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-210">**A**.</span></span> <span data-ttu-id="8da4c-211">Um dos sinais que indicam que é preciso modificar os modelos de largura de banda é quando você começa a perceber a lentidão da rede ou reduções várias vezes no dia.</span><span class="sxs-lookup"><span data-stu-id="8da4c-211">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="8da4c-212">Se isso acontecer, monitore a rede de armazenamento e uso examinando os gráficos do desempenho de E/S e da taxa de transferência de rede.</span><span class="sxs-lookup"><span data-stu-id="8da4c-212">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="8da4c-213">Com os dados de taxa de transferência da rede, identifique a hora do dia e os contêineres de volume em que ocorre o afunilamento da rede.</span><span class="sxs-lookup"><span data-stu-id="8da4c-213">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="8da4c-214">Se isso ocorre quando dados estão sendo dispostos em camada na nuvem (obtenha essa informação do desempenho de E/S de todos os contêineres de volume do dispositivo para nuvem), você precisará modificar os modelos de largura de banda associados aos seus contêineres de volume.</span><span class="sxs-lookup"><span data-stu-id="8da4c-214">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="8da4c-215">Depois que os modelos modificados estiverem em uso, você precisara monitorar a rede novamente em busca de latências significativas.</span><span class="sxs-lookup"><span data-stu-id="8da4c-215">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="8da4c-216">Se elas ainda existirem, você precisará rever seus modelos de largura de banda.</span><span class="sxs-lookup"><span data-stu-id="8da4c-216">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="8da4c-217">**P**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-217">**Q**.</span></span> <span data-ttu-id="8da4c-218">O que acontece se vários contêineres de volume em meu dispositivo tiverem agendas que se sobrepõem, mas diferentes limites se aplicarem a cada uma?</span><span class="sxs-lookup"><span data-stu-id="8da4c-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="8da4c-219">**R**.</span><span class="sxs-lookup"><span data-stu-id="8da4c-219">**A**.</span></span> <span data-ttu-id="8da4c-220">Vamos supor que você tenha um dispositivo com 3 contêineres de volume.</span><span class="sxs-lookup"><span data-stu-id="8da4c-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="8da4c-221">As agendas associadas a esses contêineres se sobrepõem completamente.</span><span class="sxs-lookup"><span data-stu-id="8da4c-221">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="8da4c-222">Para cada um desses contêineres, os limites de largura de banda usados são 5, 10 e 15 Mbps, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8da4c-222">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="8da4c-223">Quando a E/S estiver ocorrendo em todos esses contêineres ao mesmo tempo, no mínimo três limites de largura de banda poderão ser aplicados; nesse caso, 5 Mbps, pois essas solicitações de E/S de saída compartilham a mesma fila.</span><span class="sxs-lookup"><span data-stu-id="8da4c-223">When I/O are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="8da4c-224">Práticas recomendadas para modelos de largura de banda</span><span class="sxs-lookup"><span data-stu-id="8da4c-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="8da4c-225">Siga estas práticas recomendadas para seu dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="8da4c-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="8da4c-226">Configure modelos de largura de banda em seu dispositivo para habilitar a limitação variável da taxa de transferência da rede pelo dispositivo em diferentes horas do dia.</span><span class="sxs-lookup"><span data-stu-id="8da4c-226">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="8da4c-227">Esses modelos de largura de banda quando usados com agendas de backup podem aproveitar eficientemente largura de banda de rede adicionais para operações de nuvem fora dos horários de pico.</span><span class="sxs-lookup"><span data-stu-id="8da4c-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="8da4c-228">Calcule a largura de banda real necessária para uma implantação específica com base no tamanho da implantação e no RTO (objetivo de tempo de recuperação) necessário.</span><span class="sxs-lookup"><span data-stu-id="8da4c-228">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8da4c-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8da4c-229">Next steps</span></span>

<span data-ttu-id="8da4c-230">Saiba mais sobre como [usar o serviço Gerenciador de Dispositivos do StorSimple para administrar o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8da4c-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

