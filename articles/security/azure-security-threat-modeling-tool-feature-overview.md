---
title: "aaaMicrosoft ferramenta de modelagem de ameaças - Azure | Microsoft Docs"
description: "Saiba mais sobre todos os recursos de saudação disponíveis no Olá, ferramenta de modelagem de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="4a05e-103">Visão geral do recurso Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="4a05e-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="4a05e-104">Estamos contentes em escolhido toouse Olá a ferramenta de modelagem de ameaças para suas necessidades de modelagem de ameaças!</span><span class="sxs-lookup"><span data-stu-id="4a05e-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="4a05e-105">Se você ainda não tiver feito isso, visite  **[Getting Started with Olá, ferramenta de modelagem de ameaça](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn Noções básicas de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a05e-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="4a05e-106">Nossa ferramenta é atualizada com frequência, portanto, verifique este guia geralmente toosee nossos recursos e melhorias mais recentes.</span><span class="sxs-lookup"><span data-stu-id="4a05e-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="4a05e-107">Clicando no botão de "Criar um novo modelo de" hello abre uma página em branco inicial, a imagem toohello semelhante abaixo:</span><span class="sxs-lookup"><span data-stu-id="4a05e-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Página inicial em branco](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="4a05e-109">Usar o modelo de ameaça Olá criado pela nossa equipe de saudação  **[Introdução](./azure-security-threat-modeling-tool-getting-started.md)**  exemplo, vamos check-out de todos os recursos de saudação disponíveis na ferramenta Olá hoje.</span><span class="sxs-lookup"><span data-stu-id="4a05e-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Modelo Básico de Ameaça](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="4a05e-111">Navegação</span><span class="sxs-lookup"><span data-stu-id="4a05e-111">Navigation</span></span>

<span data-ttu-id="4a05e-112">Antes de mergulhar nos recursos internos Olá, vamos falar sobre os componentes principais do hello encontrados na ferramenta Olá</span><span class="sxs-lookup"><span data-stu-id="4a05e-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="4a05e-113">Itens de menu</span><span class="sxs-lookup"><span data-stu-id="4a05e-113">Menu items</span></span>

<span data-ttu-id="4a05e-114">experiência de saudação deve ser semelhantes produtos da Microsoft tooother.</span><span class="sxs-lookup"><span data-stu-id="4a05e-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="4a05e-115">Vamos começar por meio de itens de menu de nível superior de saudação:</span><span class="sxs-lookup"><span data-stu-id="4a05e-115">Let’s begin by going through hello top-level menu items:</span></span>

![Itens de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="4a05e-117">Rótulo</span><span class="sxs-lookup"><span data-stu-id="4a05e-117">Label</span></span>                               | <span data-ttu-id="4a05e-118">Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a05e-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-119">**Arquivo**</span><span class="sxs-lookup"><span data-stu-id="4a05e-119">**File**</span></span> | <ul><li><span data-ttu-id="4a05e-120">Abrir, Salvar e Fechar Arquivos</span><span class="sxs-lookup"><span data-stu-id="4a05e-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="4a05e-121">Entrar/Sair das contas do OneDrive</span><span class="sxs-lookup"><span data-stu-id="4a05e-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="4a05e-122">Compartilhar Links (Exibir + Editar)</span><span class="sxs-lookup"><span data-stu-id="4a05e-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="4a05e-123">Exibir Informações do Arquivo</span><span class="sxs-lookup"><span data-stu-id="4a05e-123">View File Information</span></span></li><li><span data-ttu-id="4a05e-124">Aplicar o novo modelo tooExisting modelos</span><span class="sxs-lookup"><span data-stu-id="4a05e-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="4a05e-125">**Editar**</span><span class="sxs-lookup"><span data-stu-id="4a05e-125">**Edit**</span></span> | <span data-ttu-id="4a05e-126">Desfazer/refazer ações, bem como copiar, colar e excluir</span><span class="sxs-lookup"><span data-stu-id="4a05e-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="4a05e-127">**Exibir**</span><span class="sxs-lookup"><span data-stu-id="4a05e-127">**View**</span></span> | <ul><li><span data-ttu-id="4a05e-128">Alternar entre as exibições **Análise** e **Design**</span><span class="sxs-lookup"><span data-stu-id="4a05e-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="4a05e-129">Abrir as janelas fechadas (por exemplo, estênceis, propriedades do elemento e mensagens)</span><span class="sxs-lookup"><span data-stu-id="4a05e-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="4a05e-130">Redefinir layout toodefault configurações</span><span class="sxs-lookup"><span data-stu-id="4a05e-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="4a05e-131">**Diagrama**</span><span class="sxs-lookup"><span data-stu-id="4a05e-131">**Diagram**</span></span> | <span data-ttu-id="4a05e-132">Adicionar/excluir diagramas e navegar pelas "guias" dos diagramas</span><span class="sxs-lookup"><span data-stu-id="4a05e-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="4a05e-133">**Relatórios**</span><span class="sxs-lookup"><span data-stu-id="4a05e-133">**Reports**</span></span> | <span data-ttu-id="4a05e-134">Criar tooshare de relatórios HTML com outras pessoas</span><span class="sxs-lookup"><span data-stu-id="4a05e-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="4a05e-135">**Ajuda**</span><span class="sxs-lookup"><span data-stu-id="4a05e-135">**Help**</span></span> | <span data-ttu-id="4a05e-136">Use a ferramenta de saudação de toohelp de guias</span><span class="sxs-lookup"><span data-stu-id="4a05e-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="4a05e-137">ícones de saudação são atalhos para os menus de nível superior de saudação:</span><span class="sxs-lookup"><span data-stu-id="4a05e-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="4a05e-138">ícone</span><span class="sxs-lookup"><span data-stu-id="4a05e-138">Icon</span></span>                               | <span data-ttu-id="4a05e-139">Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a05e-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-140">**Abrir**</span><span class="sxs-lookup"><span data-stu-id="4a05e-140">**Open**</span></span> | <span data-ttu-id="4a05e-141">Abre um novo arquivo</span><span class="sxs-lookup"><span data-stu-id="4a05e-141">Opens a new file</span></span> |
| <span data-ttu-id="4a05e-142">**Salvar**</span><span class="sxs-lookup"><span data-stu-id="4a05e-142">**Save**</span></span> | <span data-ttu-id="4a05e-143">Salva o arquivo atual</span><span class="sxs-lookup"><span data-stu-id="4a05e-143">Saves current file</span></span> |
| <span data-ttu-id="4a05e-144">**Design**</span><span class="sxs-lookup"><span data-stu-id="4a05e-144">**Design**</span></span> | <span data-ttu-id="4a05e-145">Entra no modo de exibição de design, no qual é possível criar modelos</span><span class="sxs-lookup"><span data-stu-id="4a05e-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="4a05e-146">**Analise**</span><span class="sxs-lookup"><span data-stu-id="4a05e-146">**Analyze**</span></span> | <span data-ttu-id="4a05e-147">Mostra ameaças geradas e suas propriedades</span><span class="sxs-lookup"><span data-stu-id="4a05e-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="4a05e-148">**Adicionar Diagrama**</span><span class="sxs-lookup"><span data-stu-id="4a05e-148">**Add Diagram**</span></span> | <span data-ttu-id="4a05e-149">Adiciona um novo diagrama (guias de toonew semelhante no Excel)</span><span class="sxs-lookup"><span data-stu-id="4a05e-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="4a05e-150">**Excluir Diagrama**</span><span class="sxs-lookup"><span data-stu-id="4a05e-150">**Delete Diagram**</span></span> | <span data-ttu-id="4a05e-151">Exclui o diagrama atual</span><span class="sxs-lookup"><span data-stu-id="4a05e-151">Deletes current diagram</span></span> |
| <span data-ttu-id="4a05e-152">**Copiar/Recortar/Colar**</span><span class="sxs-lookup"><span data-stu-id="4a05e-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="4a05e-153">Copia/recorta/cola elementos</span><span class="sxs-lookup"><span data-stu-id="4a05e-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="4a05e-154">**Desfazer/Refazer**</span><span class="sxs-lookup"><span data-stu-id="4a05e-154">**Undo/Redo**</span></span> | <span data-ttu-id="4a05e-155">Desfaz/refaz ações</span><span class="sxs-lookup"><span data-stu-id="4a05e-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="4a05e-156">**Ampliar/Reduzir**</span><span class="sxs-lookup"><span data-stu-id="4a05e-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="4a05e-157">Aplica zoom dentro e fora do diagrama de saudação para uma melhor exibição</span><span class="sxs-lookup"><span data-stu-id="4a05e-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="4a05e-158">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="4a05e-158">**Feedback**</span></span> | <span data-ttu-id="4a05e-159">Abre a saudação Fórum do MSDN</span><span class="sxs-lookup"><span data-stu-id="4a05e-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="4a05e-160">Tela</span><span class="sxs-lookup"><span data-stu-id="4a05e-160">Canvas</span></span>

<span data-ttu-id="4a05e-161">espaço de saudação em que você arraste e solte elementos em.</span><span class="sxs-lookup"><span data-stu-id="4a05e-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="4a05e-162">Arrastar e soltar é hello mais rápida e modelos de toobuild de maneira mais eficientes.</span><span class="sxs-lookup"><span data-stu-id="4a05e-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="4a05e-163">Você pode também clique direito e selecione no menu hello, que adiciona versões genéricas de elementos de saudação que você está usando, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4a05e-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="4a05e-164">Descartando estêncil Olá na tela hello</span><span class="sxs-lookup"><span data-stu-id="4a05e-164">Dropping hello stencil on hello canvas</span></span>

![Envio para a tela](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="4a05e-166">Clicar em estêncil Olá</span><span class="sxs-lookup"><span data-stu-id="4a05e-166">Clicking on hello stencil</span></span>

![Propriedades do Elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="4a05e-168">Estênceis</span><span class="sxs-lookup"><span data-stu-id="4a05e-168">Stencils</span></span>

<span data-ttu-id="4a05e-169">Onde você pode encontrar todos os estênceis toouse disponível com base no modelo de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="4a05e-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="4a05e-170">Se você não encontrar elementos à direita hello, tente usar outro modelo ou modificar um toofit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="4a05e-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="4a05e-171">Geralmente, você deve ser capaz de toofind uma combinação de categorias como Olá aquelas abaixo:</span><span class="sxs-lookup"><span data-stu-id="4a05e-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="4a05e-172">Nome do Estêncil</span><span class="sxs-lookup"><span data-stu-id="4a05e-172">Stencil Name</span></span>                               | <span data-ttu-id="4a05e-173">Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a05e-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-174">**Processo**</span><span class="sxs-lookup"><span data-stu-id="4a05e-174">**Process**</span></span> | <span data-ttu-id="4a05e-175">Aplicativos, Plug-ins de Navegador, Threads, Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="4a05e-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="4a05e-176">**Interagente Externo**</span><span class="sxs-lookup"><span data-stu-id="4a05e-176">**External Interactor**</span></span> | <span data-ttu-id="4a05e-177">Provedores de Autenticação, Navegadores, Usuários, Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="4a05e-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="4a05e-178">**Armazenamento de Dados**</span><span class="sxs-lookup"><span data-stu-id="4a05e-178">**Data Store**</span></span> | <span data-ttu-id="4a05e-179">Cache, Armazenamento, Arquivos de Configuração, Banco de Dados, Registro</span><span class="sxs-lookup"><span data-stu-id="4a05e-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="4a05e-180">**Fluxo de Dados**</span><span class="sxs-lookup"><span data-stu-id="4a05e-180">**Data Flow**</span></span> | <span data-ttu-id="4a05e-181">Binário, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Pipe Nomeado, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="4a05e-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="4a05e-182">**Limite de Linha/Borda de Confiança**</span><span class="sxs-lookup"><span data-stu-id="4a05e-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="4a05e-183">Redes Corporativas, Internet, Computador, Área Restrita, Modo de Usuário/Kernel</span><span class="sxs-lookup"><span data-stu-id="4a05e-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="4a05e-184">Observações/Mensagens</span><span class="sxs-lookup"><span data-stu-id="4a05e-184">Notes/Messages</span></span>

| <span data-ttu-id="4a05e-185">Componente</span><span class="sxs-lookup"><span data-stu-id="4a05e-185">Component</span></span>                               | <span data-ttu-id="4a05e-186">Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a05e-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-187">**Mensagens**</span><span class="sxs-lookup"><span data-stu-id="4a05e-187">**Messages**</span></span> | <span data-ttu-id="4a05e-188">Lógica de ferramenta interna que alerta os usuários sempre que houver um erro, como ausência de fluxos de dados entre elementos</span><span class="sxs-lookup"><span data-stu-id="4a05e-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="4a05e-189">**Observações**</span><span class="sxs-lookup"><span data-stu-id="4a05e-189">**Notes**</span></span> | <span data-ttu-id="4a05e-190">Notas manuais arquivo toohello adicionadas pelas equipes de engenharia Olá design durante todo esse processo e processo de revisão</span><span class="sxs-lookup"><span data-stu-id="4a05e-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="4a05e-191">Propriedades do elemento</span><span class="sxs-lookup"><span data-stu-id="4a05e-191">Element properties</span></span>

<span data-ttu-id="4a05e-192">Eles variam de acordo com elementos de saudação selecionados.</span><span class="sxs-lookup"><span data-stu-id="4a05e-192">These vary by hello elements selected.</span></span> <span data-ttu-id="4a05e-193">Com exceção dos Limites de Confiança, todos os outros elementos contêm 3 seleções gerais:</span><span class="sxs-lookup"><span data-stu-id="4a05e-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="4a05e-194">Propriedade do Elemento</span><span class="sxs-lookup"><span data-stu-id="4a05e-194">Element Property</span></span>                               | <span data-ttu-id="4a05e-195">Detalhes</span><span class="sxs-lookup"><span data-stu-id="4a05e-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-196">**Nome**</span><span class="sxs-lookup"><span data-stu-id="4a05e-196">**Name**</span></span> | <span data-ttu-id="4a05e-197">Útil para nomear seu toobe processos, lojas, interadores e fluxos facilmente reconhecido</span><span class="sxs-lookup"><span data-stu-id="4a05e-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="4a05e-198">**Fora do Escopo**</span><span class="sxs-lookup"><span data-stu-id="4a05e-198">**Out of Scope**</span></span> | <span data-ttu-id="4a05e-199">Se selecionado, o elemento de saudação é retirado de matriz de geração de ameaça hello (não recomendado)</span><span class="sxs-lookup"><span data-stu-id="4a05e-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="4a05e-200">**Motivo para Estar Fora do Escopo**</span><span class="sxs-lookup"><span data-stu-id="4a05e-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="4a05e-201">Os usuários toolet de campo de justificação sabem por que fora do escopo selecionado</span><span class="sxs-lookup"><span data-stu-id="4a05e-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="4a05e-202">As propriedades são alteradas em cada categoria de elemento.</span><span class="sxs-lookup"><span data-stu-id="4a05e-202">Properties are changed under each element category.</span></span> <span data-ttu-id="4a05e-203">Clique em cada elemento tooinspect Olá as opções disponíveis, ou abra Olá modelo toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="4a05e-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="4a05e-204">Vamos falar recursos hello.</span><span class="sxs-lookup"><span data-stu-id="4a05e-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="4a05e-205">Tela de boas-vindas</span><span class="sxs-lookup"><span data-stu-id="4a05e-205">Welcome screen</span></span>

<span data-ttu-id="4a05e-206">tela de boas-vindas Olá é Olá primeiro que você vê quando você abrir o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="4a05e-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="4a05e-207">Abrir um Modelo</span><span class="sxs-lookup"><span data-stu-id="4a05e-207">Open A model</span></span>

<span data-ttu-id="4a05e-208">Ao passar o mouse sobre o botão "Abrir um Modelo", duas opções ocultas serão exibidas: "Abrir deste Computador" e "Abrir do OneDrive".</span><span class="sxs-lookup"><span data-stu-id="4a05e-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="4a05e-209">Olá primeiro abre a tela de abrir arquivo hello, enquanto Olá segundo leva você através de processo de entrada hello para OneDrive, permitindo que você toopick pastas e arquivos após uma autenticação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="4a05e-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Abrir Modelo](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abrir do Computador ou do OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="4a05e-212">Comentários, sugestões e problemas</span><span class="sxs-lookup"><span data-stu-id="4a05e-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="4a05e-213">Esta opção levará você toohello os fóruns do MSDN para as ferramentas do SDL.</span><span class="sxs-lookup"><span data-stu-id="4a05e-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="4a05e-214">É toocheck uma ótima maneira out que outras pessoas estão falando sobre ferramenta hello, incluindo novas ideias e soluções alternativas.</span><span class="sxs-lookup"><span data-stu-id="4a05e-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Comentários](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="4a05e-216">Modo de exibição de Design</span><span class="sxs-lookup"><span data-stu-id="4a05e-216">Design view</span></span>

<span data-ttu-id="4a05e-217">Sempre que você abrir ou cria um novo modelo, você será levado toohello modo de design.</span><span class="sxs-lookup"><span data-stu-id="4a05e-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="4a05e-218">Adicionando elementos</span><span class="sxs-lookup"><span data-stu-id="4a05e-218">Adding elements</span></span>

<span data-ttu-id="4a05e-219">Há 2 modos tooadd elementos na grade de saudação:</span><span class="sxs-lookup"><span data-stu-id="4a05e-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="4a05e-220">**Arrastar e soltar** – arraste Olá elemento desejado toohello grade, em seguida, usar Olá elemento propriedades tooprovide obter informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="4a05e-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="4a05e-221">**Clique com botão direito** – clique com botão direito em qualquer lugar na grade hello e selecione no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a05e-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="4a05e-222">Uma representação genérica desse elemento será exibido na tela hello.</span><span class="sxs-lookup"><span data-stu-id="4a05e-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="4a05e-223">Conectando elementos</span><span class="sxs-lookup"><span data-stu-id="4a05e-223">Connecting elements</span></span>

<span data-ttu-id="4a05e-224">Há 2 modos tooconnect elementos na ferramenta hello:</span><span class="sxs-lookup"><span data-stu-id="4a05e-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="4a05e-225">**Arrastar e soltar** – arraste Olá grade de toohello de fluxo de dados desejado e conectar os dois elementos apropriados de toohello termina.</span><span class="sxs-lookup"><span data-stu-id="4a05e-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="4a05e-226">**Clique em + Shift** – clique no primeiro elemento de saudação (enviar dados), pressione e mantenha a tecla Shift de hello, em seguida, elemento de segundo select hello (recebimento de dados).</span><span class="sxs-lookup"><span data-stu-id="4a05e-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="4a05e-227">Clique com o botão direito do mouse e selecione "Conectar".</span><span class="sxs-lookup"><span data-stu-id="4a05e-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="4a05e-228">Se você estiver usando um fluxo de dados de bi-direcional, ordem de saudação não é tão importante.</span><span class="sxs-lookup"><span data-stu-id="4a05e-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="4a05e-229">Propriedades</span><span class="sxs-lookup"><span data-stu-id="4a05e-229">Properties</span></span>

<span data-ttu-id="4a05e-230">Mostra todas as propriedades de saudação que podem ser modificadas em estênceis Olá colocadas no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a05e-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="4a05e-231">Propriedades de saudação toosee, basta clicar no estêncil hello e informações hello serão preenchidas adequadamente.</span><span class="sxs-lookup"><span data-stu-id="4a05e-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="4a05e-232">exemplo Hello abaixo mostra antes e depois um estêncil é arrastado para o diagrama de hello "Database":</span><span class="sxs-lookup"><span data-stu-id="4a05e-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="4a05e-233">Antes</span><span class="sxs-lookup"><span data-stu-id="4a05e-233">Before</span></span>

![Antes](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="4a05e-235">após</span><span class="sxs-lookup"><span data-stu-id="4a05e-235">After</span></span>

![após](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="4a05e-237">Mensagens</span><span class="sxs-lookup"><span data-stu-id="4a05e-237">Messages</span></span>

<span data-ttu-id="4a05e-238">Se você criar um modelo de ameaça e esquecer fluxos de dados de tooconnect tooelements, a janela de mensagem de saudação notifica tooact.</span><span class="sxs-lookup"><span data-stu-id="4a05e-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="4a05e-239">Você pode escolher tooignore-lo ou siga Olá problema de saudação toofix instruções.</span><span class="sxs-lookup"><span data-stu-id="4a05e-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Mensagens](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="4a05e-241">Observações</span><span class="sxs-lookup"><span data-stu-id="4a05e-241">Notes</span></span>

<span data-ttu-id="4a05e-242">As guias de tooNotes de mensagens permite que você tooadd notas tooyour diagrama toocapture todas as sugestões</span><span class="sxs-lookup"><span data-stu-id="4a05e-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="4a05e-243">Modo de exibição de análise</span><span class="sxs-lookup"><span data-stu-id="4a05e-243">Analysis view</span></span>

<span data-ttu-id="4a05e-244">Quando terminar de criar seu diagrama, alternar exibição tooanalysis indo toohello seleções de menu superior e escolha Olá Lupa próxima toohello paint paleta.</span><span class="sxs-lookup"><span data-stu-id="4a05e-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Modo de Exibição de Análise](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="4a05e-246">Seleção de ameaça gerada</span><span class="sxs-lookup"><span data-stu-id="4a05e-246">Generated threat selection</span></span>

<span data-ttu-id="4a05e-247">Ao clicar em uma ameaça, você pode aproveitar três funções exclusivas:</span><span class="sxs-lookup"><span data-stu-id="4a05e-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="4a05e-248">Recurso</span><span class="sxs-lookup"><span data-stu-id="4a05e-248">Feature</span></span>                               | <span data-ttu-id="4a05e-249">Informações</span><span class="sxs-lookup"><span data-stu-id="4a05e-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="4a05e-250">**Indicador de Leitura**</span><span class="sxs-lookup"><span data-stu-id="4a05e-250">**Read Indicator**</span></span> | <p><span data-ttu-id="4a05e-251">Ameaça está marcada como leitura, que pode ajudá-lo facilmente manter o controle de itens de saudação que você já seguiu</span><span class="sxs-lookup"><span data-stu-id="4a05e-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Indicador de Lido/Não Lido](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="4a05e-253">**Foco de Interação**</span><span class="sxs-lookup"><span data-stu-id="4a05e-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="4a05e-254">Interação no diagrama Olá pertencentes a ameaça de toothat é realçada</span><span class="sxs-lookup"><span data-stu-id="4a05e-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Foco de Interação](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="4a05e-256">**Propriedades da Ameaça**</span><span class="sxs-lookup"><span data-stu-id="4a05e-256">**Threat Properties**</span></span> | <p><span data-ttu-id="4a05e-257">Informações adicionais sobre a ameaça de saudação são populadas na janela de propriedades de ameaça Olá</span><span class="sxs-lookup"><span data-stu-id="4a05e-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Propriedades da Ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="4a05e-259">Alteração de prioridade</span><span class="sxs-lookup"><span data-stu-id="4a05e-259">Priority change</span></span>

<span data-ttu-id="4a05e-260">Alterar o nível de prioridade de saudação de cada ameaça gerada também altera seu toomake cores-tooidentify fácil ameaças de prioridade alta, média e baixa.</span><span class="sxs-lookup"><span data-stu-id="4a05e-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Alteração de Prioridade](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="4a05e-262">Campos editáveis das propriedades da ameaça</span><span class="sxs-lookup"><span data-stu-id="4a05e-262">Threat properties editable fields</span></span>

<span data-ttu-id="4a05e-263">Conforme mostrado na imagem de saudação acima, os usuários podem alterar informações de saudação geradas pela ferramenta Olá um também adicionar campos de toocertain de informações, como a justificação.</span><span class="sxs-lookup"><span data-stu-id="4a05e-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="4a05e-264">Esses campos são gerados pelo modelo hello, então se você precisar de mais informações para cada uma delas, você está toomake incentivados modificações.</span><span class="sxs-lookup"><span data-stu-id="4a05e-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Propriedades da Ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="4a05e-266">Relatórios</span><span class="sxs-lookup"><span data-stu-id="4a05e-266">Reports</span></span>

<span data-ttu-id="4a05e-267">Quando você terminar as mudanças de prioridades e atualizar status de saudação de cada gerado ameaça, você pode salvar o arquivo hello e/ou imprimir um relatório indo muito "relatório" e, em seguida, "Criar relatório completo."</span><span class="sxs-lookup"><span data-stu-id="4a05e-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="4a05e-268">Você será solicitado o relatório de saudação tooname e depois que você fizer isso, você verá algo semelhante imagem toohello abaixo:</span><span class="sxs-lookup"><span data-stu-id="4a05e-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Relatório](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="4a05e-270">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a05e-270">Next steps</span></span>

<span data-ttu-id="4a05e-271">toocontribute um modelo para a comunidade de hello, acesse tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página.</span><span class="sxs-lookup"><span data-stu-id="4a05e-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="4a05e-272">**[Baixar](https://aka.ms/tmtpreview)**  Olá ferramenta tooget iniciado hoje.</span><span class="sxs-lookup"><span data-stu-id="4a05e-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
