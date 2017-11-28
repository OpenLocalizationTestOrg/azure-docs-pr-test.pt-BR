---
title: etapa aaaGeneric etapa por conector do SQL | Microsoft Docs
description: "Este artigo é percorrer você através de um sistema de RH simple usando o passo a passo Olá conector do SQL genérico."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="3b8c5-103">Passo a passo do Conector do SQL Genérico</span><span class="sxs-lookup"><span data-stu-id="3b8c5-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="3b8c5-104">Este tópico é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="3b8c5-105">Ele cria um banco de dados de RH de exemplo simples e o usará para a importação de alguns usuários e sua associação a um grupo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-hello-sample-database"></a><span data-ttu-id="3b8c5-106">Preparar o banco de dados de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3b8c5-106">Prepare hello sample database</span></span>
<span data-ttu-id="3b8c5-107">Em um servidor executando o SQL Server, execute o script SQL de saudação encontrado no [Apêndice A](#appendix-a). Esse script cria um banco de dados de exemplo com o nome hello GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-107">On a server running SQL Server, run hello SQL script found in [Appendix A](#appendix-a). This script creates a sample database with hello name GSQLDEMO.</span></span> <span data-ttu-id="3b8c5-108">modelo de objeto de saudação do hello criados nesta imagem parece de banco de dados:</span><span class="sxs-lookup"><span data-stu-id="3b8c5-108">hello object model for hello created database looks like this picture:</span></span>  
<span data-ttu-id="3b8c5-109">![Modelo de objeto](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="3b8c5-110">Também crie um usuário de banco de dados do toouse tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-110">Also create a user you want toouse tooconnect toohello database.</span></span> <span data-ttu-id="3b8c5-111">Neste passo a passo, usuário Olá é chamado FABRIKAM\SQLUser e localizado no domínio hello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-111">In this walkthrough, hello user is called FABRIKAM\SQLUser and located in hello domain.</span></span>

## <a name="create-hello-odbc-connection-file"></a><span data-ttu-id="3b8c5-112">Criar arquivo de conexão ODBC Olá</span><span class="sxs-lookup"><span data-stu-id="3b8c5-112">Create hello ODBC connection file</span></span>
<span data-ttu-id="3b8c5-113">Olá conector do SQL genérico é usando o servidor remoto do ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-113">hello Generic SQL Connector is using ODBC tooconnect toohello remote server.</span></span> <span data-ttu-id="3b8c5-114">Primeiro, precisamos toocreate um arquivo com hello informações de conexão do ODBC.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-114">First we need toocreate a file with hello ODBC connection information.</span></span>

1. <span data-ttu-id="3b8c5-115">Inicie o utilitário de gerenciamento de ODBC Olá em seu servidor:</span><span class="sxs-lookup"><span data-stu-id="3b8c5-115">Start hello ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="3b8c5-117">Guia de saudação selecione **DSN de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-117">Select hello tab **File DSN**.</span></span> <span data-ttu-id="3b8c5-118">Clique em **Adicionar...**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-118">Click **Add...**.</span></span>  
   <span data-ttu-id="3b8c5-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="3b8c5-120">Olá out-of-box drivers funciona bem, para selecioná-lo e clique em **próximo >**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-120">hello out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="3b8c5-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="3b8c5-122">Dê um nome de arquivo hello como **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-122">Give hello file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="3b8c5-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="3b8c5-124">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-124">Click **Finish**.</span></span>  
   <span data-ttu-id="3b8c5-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="3b8c5-126">Conexão de saudação do tooconfigure de tempo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-126">Time tooconfigure hello connection.</span></span> <span data-ttu-id="3b8c5-127">Dê a fonte de dados Olá uma descrição válida e fornecer o nome de saudação do servidor de saudação executando o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-127">Give hello data source a good description and provide hello name of hello server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="3b8c5-129">Selecione como tooauthenticate com SQL.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-129">Select how tooauthenticate with SQL.</span></span> <span data-ttu-id="3b8c5-130">Nesse caso, usamos a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="3b8c5-132">Fornecer nome de saudação do banco de dados de exemplo hello, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-132">Provide hello name of hello sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="3b8c5-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="3b8c5-134">Mantenha todas as opções como padrão nesta tela.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-134">Keep everything default on this screen.</span></span> <span data-ttu-id="3b8c5-135">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-135">Click **Finish**.</span></span>  
   <span data-ttu-id="3b8c5-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="3b8c5-137">tooverify tudo está funcionando conforme o esperado, clique em **fonte de dados de teste**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-137">tooverify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="3b8c5-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="3b8c5-139">Certifique-se de saudação teste for bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-139">Make sure hello test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="3b8c5-141">arquivo de configuração de ODBC Olá agora deve estar visível no DSN de arquivo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-141">hello ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="3b8c5-143">Agora temos arquivo hello precisamos e pode começar a criar hello conector.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-143">We now have hello file we need and can start creating hello Connector.</span></span>

## <a name="create-hello-generic-sql-connector"></a><span data-ttu-id="3b8c5-144">Criar hello conector do SQL genérico</span><span class="sxs-lookup"><span data-stu-id="3b8c5-144">Create hello Generic SQL Connector</span></span>
1. <span data-ttu-id="3b8c5-145">No hello UI Synchronization Service Manager, selecione **conectores** e **criar**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-145">In hello Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="3b8c5-146">Selecione **SQL Genérico (Microsoft)** e dê a ele um nome descritivo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="3b8c5-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="3b8c5-148">Localizar o arquivo DSN Olá que você criou na seção anterior hello e carregá-lo toohello server.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-148">Find hello DSN file you created in hello previous section and upload it toohello server.</span></span> <span data-ttu-id="3b8c5-149">Fornece o banco de dados do hello credenciais tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-149">Provide hello credentials tooconnect toohello database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="3b8c5-151">Neste passo a passo, estamos facilitando nosso trabalho dizendo que há dois tipos de objeto, **User** e **Group**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="3b8c5-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="3b8c5-153">atributos de saudação toofind, queremos Olá conector toodetect desses atributos, observando a própria tabela hello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-153">toofind hello attributes, we want hello Connector toodetect those attributes by looking at hello table itself.</span></span> <span data-ttu-id="3b8c5-154">Como **usuários** é uma palavra reservada no SQL, é preciso tooprovide-lo no quadrado colchetes [].</span><span class="sxs-lookup"><span data-stu-id="3b8c5-154">Since **Users** is a reserved word in SQL, we need tooprovide it in square brackets [ ].</span></span>  
   <span data-ttu-id="3b8c5-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="3b8c5-156">Atributo de âncora tempo toodefine hello e atributo DN de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-156">Time toodefine hello anchor attribute and hello DN attribute.</span></span> <span data-ttu-id="3b8c5-157">Para **usuários**, usamos a combinação de saudação do nome de usuário do hello dois atributos e EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-157">For **Users**, we use hello combination of hello two attributes username and EmployeeID.</span></span> <span data-ttu-id="3b8c5-158">Para **Group**, usamos GroupName (não realista na vida real, mas funcionará nesse passo a passo).</span><span class="sxs-lookup"><span data-stu-id="3b8c5-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="3b8c5-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="3b8c5-160">Nem todos os tipos de atributo podem ser detectados em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="3b8c5-161">tipo de atributo de referência de saudação em particular não pode.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-161">hello reference attribute type in particular cannot.</span></span> <span data-ttu-id="3b8c5-162">Para o tipo de objeto de grupo hello, precisamos toochange Olá OwnerID e MemberID tooreference.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-162">For hello group object type, we need toochange hello OwnerID and MemberID tooreference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="3b8c5-164">atributos de saudação selecionamos como atributos de referência na etapa anterior Olá exigem esses valores são uma referência ao tipo de objeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-164">hello attributes we selected as reference attributes in hello previous step require hello object type these values are a reference to.</span></span> <span data-ttu-id="3b8c5-165">Em nosso caso, Olá tipo de objeto do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-165">In our case, hello User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="3b8c5-167">Na página de parâmetros globais hello, selecione **marca d'água** como estratégia de delta hello.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-167">On hello Global Parameters page, select **Watermark** as hello delta strategy.</span></span> <span data-ttu-id="3b8c5-168">Digite também no formato de data/hora Olá **AAAA-MM-dd hh**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-168">Also type in hello date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="3b8c5-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="3b8c5-170">Em Olá **configurar partições e hierarquias** , selecione os dois tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-170">On hello **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="3b8c5-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="3b8c5-172">Em Olá **selecionar tipos de objeto** e **selecionar atributos**, selecione os tipos de objeto e todos os atributos.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-172">On hello **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="3b8c5-173">Em Olá **configurar âncoras** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-173">On hello **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="3b8c5-174">Criar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="3b8c5-174">Create Run Profiles</span></span>
1. <span data-ttu-id="3b8c5-175">No hello UI Synchronization Service Manager, selecione **conectores**, e **configurar perfis de execução**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-175">In hello Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="3b8c5-176">Clique em **Novo Perfil**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-176">Click **New Profile**.</span></span> <span data-ttu-id="3b8c5-177">Começamos com **Importação Completa**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="3b8c5-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="3b8c5-179">Selecione o tipo de saudação **importação completa (somente estágio)**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-179">Select hello type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="3b8c5-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="3b8c5-181">Selecione a partição Olá **objeto = usuário**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-181">Select hello partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="3b8c5-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="3b8c5-183">Selecione **Tabela** e digite **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="3b8c5-184">Role para baixo da seção de tipo de objeto múltiplos toohello e inserir dados de saudação como Olá figura abaixo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-184">Scroll down toohello multi-valued object type section and enter hello data as in hello following picture.</span></span> <span data-ttu-id="3b8c5-185">Selecione **concluir** toosave etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-185">Select **Finish** toosave hello step.</span></span>  
   <span data-ttu-id="3b8c5-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="3b8c5-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="3b8c5-188">Selecione **Nova Etapa**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-188">Select **New Step**.</span></span> <span data-ttu-id="3b8c5-189">Desta vez, selecione **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="3b8c5-190">Na última página de hello, use a configuração de hello como Olá figura abaixo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-190">On hello last page, use hello configuration as in hello following picture.</span></span> <span data-ttu-id="3b8c5-191">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-191">Click **Finish**.</span></span>  
   <span data-ttu-id="3b8c5-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="3b8c5-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="3b8c5-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="3b8c5-194">Opcional: se quiser, você poderá configurar perfis de execução adicionais.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="3b8c5-195">Para este passo a passo, Olá importação completa é usada.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-195">For this walkthrough, only hello Full Import is used.</span></span>
7. <span data-ttu-id="3b8c5-196">Clique em **Okey** toofinish alterando perfis de execução.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-196">Click **OK** toofinish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-hello-import"></a><span data-ttu-id="3b8c5-197">Adicione alguns importação de saudação teste dados e de teste</span><span class="sxs-lookup"><span data-stu-id="3b8c5-197">Add some test data and test hello import</span></span>
<span data-ttu-id="3b8c5-198">Preencha alguns dados de teste no banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="3b8c5-199">Quando estiver pronto, selecione **Executar** e **Importação completa**.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="3b8c5-200">Aqui está um usuário com dois números de telefone e um grupo com alguns membros.</span><span class="sxs-lookup"><span data-stu-id="3b8c5-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="3b8c5-203">Apêndice A</span><span class="sxs-lookup"><span data-stu-id="3b8c5-203">Appendix A</span></span>
<span data-ttu-id="3b8c5-204">**Banco de dados do SQL script toocreate Olá exemplo**</span><span class="sxs-lookup"><span data-stu-id="3b8c5-204">**SQL script toocreate hello sample database**</span></span>

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
