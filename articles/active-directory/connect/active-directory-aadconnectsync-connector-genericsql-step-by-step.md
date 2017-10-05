---
title: "Passo a passo do Conector SQL Genérico | Microsoft Docs"
description: "Este artigo explicará um passo a passo simples do sistema de RH usando o Conector do SQL Genérico."
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
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="904e7-103">Passo a passo do Conector do SQL Genérico</span><span class="sxs-lookup"><span data-stu-id="904e7-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="904e7-104">Este tópico é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="904e7-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="904e7-105">Ele cria um banco de dados de RH de exemplo simples e o usará para a importação de alguns usuários e sua associação a um grupo.</span><span class="sxs-lookup"><span data-stu-id="904e7-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="904e7-106">Preparar o banco de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="904e7-106">Prepare the sample database</span></span>
<span data-ttu-id="904e7-107">Em um servidor que executa o SQL Server, execute o script SQL encontrado no [Apêndice A](#appendix-a). Esse script cria um banco de dados de exemplo com o nome GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="904e7-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="904e7-108">O modelo de objeto para o banco de dados criado é semelhante a esta imagem: </span><span class="sxs-lookup"><span data-stu-id="904e7-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="904e7-109">![Modelo de objeto](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="904e7-110">Também crie um usuário que deseja usar para se conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="904e7-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="904e7-111">Neste passo a passo, o usuário é chamado FABRIKAM\SQLUser e está localizado no domínio.</span><span class="sxs-lookup"><span data-stu-id="904e7-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="904e7-112">Criar o arquivo de conexão ODBC</span><span class="sxs-lookup"><span data-stu-id="904e7-112">Create the ODBC connection file</span></span>
<span data-ttu-id="904e7-113">O Conector do SQL Genérico está usando o ODBC para se conectar ao servidor remoto.</span><span class="sxs-lookup"><span data-stu-id="904e7-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="904e7-114">Primeiro, precisamos criar um arquivo com as informações de conexão ODBC.</span><span class="sxs-lookup"><span data-stu-id="904e7-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="904e7-115">Inicie o utilitário de gerenciamento ODBC no servidor: </span><span class="sxs-lookup"><span data-stu-id="904e7-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="904e7-117">Selecione a guia **DSN de Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="904e7-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="904e7-118">Clique em **Adicionar...**.</span><span class="sxs-lookup"><span data-stu-id="904e7-118">Click **Add...**.</span></span>  
   <span data-ttu-id="904e7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="904e7-120">O driver pronto para uso funciona bem, então, selecione-o e clique em **Avançar>**.</span><span class="sxs-lookup"><span data-stu-id="904e7-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="904e7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="904e7-122">Nomeie o arquivo, como **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="904e7-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="904e7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="904e7-124">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="904e7-124">Click **Finish**.</span></span>  
   <span data-ttu-id="904e7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="904e7-126">Hora de configurar a conexão.</span><span class="sxs-lookup"><span data-stu-id="904e7-126">Time to configure the connection.</span></span> <span data-ttu-id="904e7-127">Forneça uma boa descrição à fonte de dados e o nome do servidor que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="904e7-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="904e7-129">Selecione como deseja se autenticar com o SQL.</span><span class="sxs-lookup"><span data-stu-id="904e7-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="904e7-130">Nesse caso, usamos a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="904e7-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="904e7-132">Forneça o nome do banco de dados de exemplo, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="904e7-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="904e7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="904e7-134">Mantenha todas as opções como padrão nesta tela.</span><span class="sxs-lookup"><span data-stu-id="904e7-134">Keep everything default on this screen.</span></span> <span data-ttu-id="904e7-135">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="904e7-135">Click **Finish**.</span></span>  
   <span data-ttu-id="904e7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="904e7-137">Para verificar se tudo está funcionando como esperado, clique em **Testar Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="904e7-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="904e7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="904e7-139">Verifique se o teste foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="904e7-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="904e7-141">O arquivo de configuração ODBC agora deverá estar visível no DSN de Arquivo.</span><span class="sxs-lookup"><span data-stu-id="904e7-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="904e7-143">Agora temos o arquivo necessário e podemos começar a criar o Conector.</span><span class="sxs-lookup"><span data-stu-id="904e7-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="904e7-144">Criar o Conector do SQL Genérico</span><span class="sxs-lookup"><span data-stu-id="904e7-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="904e7-145">Na interface do usuário do Synchronization Service Manager, selecione **Conectores** e **Criar**.</span><span class="sxs-lookup"><span data-stu-id="904e7-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="904e7-146">Selecione **SQL Genérico (Microsoft)** e dê a ele um nome descritivo.</span><span class="sxs-lookup"><span data-stu-id="904e7-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="904e7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="904e7-148">Encontre o arquivo DSN criado na seção anterior e o carregue no servidor.</span><span class="sxs-lookup"><span data-stu-id="904e7-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="904e7-149">Forneça as credenciais para se conectar ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="904e7-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="904e7-151">Neste passo a passo, estamos facilitando nosso trabalho dizendo que há dois tipos de objeto, **User** e **Group**.</span><span class="sxs-lookup"><span data-stu-id="904e7-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="904e7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="904e7-153">Para encontrar os atributos, queremos que o Conector os detecte observando a própria tabela.</span><span class="sxs-lookup"><span data-stu-id="904e7-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="904e7-154">Já que **Users** é uma palavra reservada no SQL, precisamos fornecê-la entre colchetes [ ].</span><span class="sxs-lookup"><span data-stu-id="904e7-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="904e7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="904e7-156">Hora de definir o atributo de âncora e o atributo DN.</span><span class="sxs-lookup"><span data-stu-id="904e7-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="904e7-157">Para **Users**, usamos a combinação dos dois atributos username e EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="904e7-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="904e7-158">Para **Group**, usamos GroupName (não realista na vida real, mas funcionará nesse passo a passo).</span><span class="sxs-lookup"><span data-stu-id="904e7-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="904e7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="904e7-160">Nem todos os tipos de atributo podem ser detectados em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="904e7-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="904e7-161">Em particular, o tipo de atributo de referência não tem essa capacidade.</span><span class="sxs-lookup"><span data-stu-id="904e7-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="904e7-162">Para o tipo de objeto de grupo, precisamos alterar a OwnerID e a MemberID para fazer referência a elas.</span><span class="sxs-lookup"><span data-stu-id="904e7-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="904e7-164">Os atributos que selecionamos como referência na etapa anterior exigem o tipo de objeto para o qual esses valores são uma referência.</span><span class="sxs-lookup"><span data-stu-id="904e7-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="904e7-165">Em nosso caso, o tipo de objeto de Usuário.</span><span class="sxs-lookup"><span data-stu-id="904e7-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="904e7-167">Na página Parâmetros Globais, selecione **Marca-d'água** como a estratégia delta.</span><span class="sxs-lookup"><span data-stu-id="904e7-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="904e7-168">Digite também o formato de data/hora **aaaa-MM-dd HH:mm:ss**.</span><span class="sxs-lookup"><span data-stu-id="904e7-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="904e7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="904e7-170">Na página **Configurar Partições e Hierarquias**, escolha ambos os tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="904e7-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="904e7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="904e7-172">Em **Selecionar Tipos de Objeto** e **Selecionar Atributos**, selecione os dois tipos de objeto e todos os atributos.</span><span class="sxs-lookup"><span data-stu-id="904e7-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="904e7-173">Na página **Configurar Âncoras**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="904e7-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="904e7-174">Criar perfis de execução</span><span class="sxs-lookup"><span data-stu-id="904e7-174">Create Run Profiles</span></span>
1. <span data-ttu-id="904e7-175">Na interface do usuário do Synchronization Service Manager, selecione **Conectores** e **Configurar Perfis de Execução**.</span><span class="sxs-lookup"><span data-stu-id="904e7-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="904e7-176">Clique em **Novo Perfil**.</span><span class="sxs-lookup"><span data-stu-id="904e7-176">Click **New Profile**.</span></span> <span data-ttu-id="904e7-177">Começamos com **Importação Completa**.</span><span class="sxs-lookup"><span data-stu-id="904e7-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="904e7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="904e7-179">Selecione o tipo **Importação Completa (Somente Estágio)**.</span><span class="sxs-lookup"><span data-stu-id="904e7-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="904e7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="904e7-181">Selecione a partição **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="904e7-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="904e7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="904e7-183">Selecione **Tabela** e digite **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="904e7-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="904e7-184">Role para baixo até a seção de tipo de objeto com vários valores e insira os dados como na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="904e7-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="904e7-185">Selecione **Concluir** para salvar a etapa.</span><span class="sxs-lookup"><span data-stu-id="904e7-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="904e7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="904e7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="904e7-188">Selecione **Nova Etapa**.</span><span class="sxs-lookup"><span data-stu-id="904e7-188">Select **New Step**.</span></span> <span data-ttu-id="904e7-189">Desta vez, selecione **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="904e7-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="904e7-190">Na última página, use a configuração como na imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="904e7-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="904e7-191">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="904e7-191">Click **Finish**.</span></span>  
   <span data-ttu-id="904e7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="904e7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="904e7-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="904e7-194">Opcional: se quiser, você poderá configurar perfis de execução adicionais.</span><span class="sxs-lookup"><span data-stu-id="904e7-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="904e7-195">Para este passo a passo, foi usada apenas a Importação Completa.</span><span class="sxs-lookup"><span data-stu-id="904e7-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="904e7-196">Clique em **OK** para concluir a alteração de perfis de execução.</span><span class="sxs-lookup"><span data-stu-id="904e7-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="904e7-197">Adicionar alguns dados de teste e testar a importação</span><span class="sxs-lookup"><span data-stu-id="904e7-197">Add some test data and test the import</span></span>
<span data-ttu-id="904e7-198">Preencha alguns dados de teste no banco de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="904e7-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="904e7-199">Quando estiver pronto, selecione **Executar** e **Importação completa**.</span><span class="sxs-lookup"><span data-stu-id="904e7-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="904e7-200">Aqui está um usuário com dois números de telefone e um grupo com alguns membros.</span><span class="sxs-lookup"><span data-stu-id="904e7-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="904e7-203">Apêndice A</span><span class="sxs-lookup"><span data-stu-id="904e7-203">Appendix A</span></span>
<span data-ttu-id="904e7-204">**Script SQL para criar o banco de dados de exemplo**</span><span class="sxs-lookup"><span data-stu-id="904e7-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
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
