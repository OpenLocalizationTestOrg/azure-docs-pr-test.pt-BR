---
title: aaaUnity reverter um tutorial de bola
description: "Etapas toocreate Olá Roll-clássico Unity um jogo que é um pré-requisito para todos os tutoriais do Mobile Engagement Unity"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 10d923682432961207594886b08e5db60cf60d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="97886-103"><a id="unity-roll-a-ball"></a>Criar um jogo Roll a Ball do Unity</span><span class="sxs-lookup"><span data-stu-id="97886-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="97886-104">Este tutorial orienta pelas etapas principais para um pouco modificada a saudação [Unity reverter um tutorial de bola](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span><span class="sxs-lookup"><span data-stu-id="97886-104">This tutorial walks through hello main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="97886-105">O jogo de exemplo consiste em um objeto Esférico 'player' que é controlado pelo usuário do aplicativo hello e objetivo de saudação do jogo Olá é too'collect' coleção objetos pelo objeto de player Olá colisão com esses objetos de coleção.</span><span class="sxs-lookup"><span data-stu-id="97886-105">This sample game consists of a spherical 'player' object which is controlled by hello app user and hello objective of hello game is too'collect' collectible objects by colliding hello player object with these collectible objects.</span></span> <span data-ttu-id="97886-106">Isso pressupõe familiaridade básica com o ambiente de editor do Unity.</span><span class="sxs-lookup"><span data-stu-id="97886-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="97886-107">Se você tiver algum problema, em seguida, você deve consultar o tutorial completo toohello.</span><span class="sxs-lookup"><span data-stu-id="97886-107">If you run into any issues then you should refer toohello full tutorial.</span></span> 

### <a name="setting-up-hello-game"></a><span data-ttu-id="97886-108">Configurando o jogo Olá</span><span class="sxs-lookup"><span data-stu-id="97886-108">Setting up hello game</span></span>
<span data-ttu-id="97886-109">Olá etapas a seguir são de saudação [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="97886-109">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="97886-110">Abra o **Editor do Unity** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="97886-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="97886-111">Forneça um **Nome do projeto** & **Local**, selecione **3D** e clique em **Criar projeto**.</span><span class="sxs-lookup"><span data-stu-id="97886-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="97886-112">Salvar cena de padrão de saudação acabou de criar como parte do novo projeto de saudação assim como acontece com nome hello **MiniGame** dentro de um novo  **\_cenas** pasta sob **ativos** pasta:</span><span class="sxs-lookup"><span data-stu-id="97886-112">Save hello default scene just created as part of hello new project as with hello name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="97886-113">Criar um **objeto 3D -> plano** como Olá reproduzindo campo e renomear este objeto de plano como **Terra**</span><span class="sxs-lookup"><span data-stu-id="97886-113">Create a **3D Object -> Plane** as hello playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="97886-114">Componente de transformação de saudação de redefinição para este **Terra** para que ele seja Olá origem do objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-114">Reset hello transform component for this **Ground** object so that it is at hello Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="97886-115">Desmarque **Mostrar grade de** de **menu largue as** para Olá **Terra** objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-115">Uncheck **Show Grid** from **Gizmos menu** for hello **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="97886-116">Saudação de atualização **escala** componente para Olá **Terra** objeto toobe [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="97886-116">Update hello **Scale** component for hello **Ground** object toobe [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="97886-117">Adicionar um novo **objeto 3D -> esfera** toohello projeto e renomear este esfera de objeto como **Player**.</span><span class="sxs-lookup"><span data-stu-id="97886-117">Add a new **3D Object -> Sphere** toohello project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="97886-118">Selecione Olá **Player** do objeto e clique em **redefinir transformação** objeto de plano toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="97886-118">Select hello **Player** object and click **Reset Transform** similar toohello Plane object.</span></span> 
10. <span data-ttu-id="97886-119">Atualização **transformação -> Posição -> coordenada Y** componente para Olá Player Y como 0,5.</span><span class="sxs-lookup"><span data-stu-id="97886-119">Update **Transform -> Position -> Y Coordinate** component for hello Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="97886-120">Criar uma nova pasta chamada **material** no projeto Olá onde criaremos player de saudação do hello toocolor material.</span><span class="sxs-lookup"><span data-stu-id="97886-120">Create a new folder called **Materials** in hello project where we will create hello material toocolor hello player.</span></span> 
12. <span data-ttu-id="97886-121">Crie um novo **Material** chamado **Tela de fundo** nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="97886-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="97886-122">Atualizar cor de saudação do material Olá atualizando Olá **Albedo** propriedade dele.</span><span class="sxs-lookup"><span data-stu-id="97886-122">Update hello color of hello material by updating hello **Albedo** property of it.</span></span> <span data-ttu-id="97886-123">Você pode selecionar valores RGB de saudação do [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="97886-123">You can select hello RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="97886-124">Arraste este material para Olá cena exibição tooapply cor toohello **Terra** objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-124">Drag this material into hello scene view tooapply color toohello **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="97886-125">Atualizar finalmente Olá **transformação -> rotação -> Y** too60 no objeto de luz direcional Olá para maior clareza.</span><span class="sxs-lookup"><span data-stu-id="97886-125">Finally update hello **Transform -> Rotation -> Y** too60 on hello Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-hello-player"></a><span data-ttu-id="97886-126">Player de saudação móvel</span><span class="sxs-lookup"><span data-stu-id="97886-126">Moving hello player</span></span>
<span data-ttu-id="97886-127">Olá etapas a seguir são de saudação [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="97886-127">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="97886-128">Adicionar um **RigidBody** componente toohello **Player** objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-128">Add a **RigidBody** component toohello **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="97886-129">Criar uma nova pasta chamada **Scripts** no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-129">Create a new folder called **Scripts** in hello Project.</span></span> 
3. <span data-ttu-id="97886-130">Clique em **Adicionar Componente -> Novo Script -> Script em C#**.</span><span class="sxs-lookup"><span data-stu-id="97886-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="97886-131">Nomeie-o como **PlayerController** e clique em **Criar e Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97886-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="97886-132">Isso criará e anexar um objeto do script toohello Player.</span><span class="sxs-lookup"><span data-stu-id="97886-132">This will create and attach a script toohello Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="97886-133">Mover esse script em Olá **Scripts** pasta no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-133">Move this script under hello **Scripts** folder in hello project.</span></span> 
5. <span data-ttu-id="97886-134">Abra script hello para edição em seu editor favorito de script, atualize o código de script hello com hello código a seguir e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="97886-134">Open hello script for editing in your favorite script editor, update hello script code with hello following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="97886-135">Observe o script hello acima usa um **velocidade** propriedade.</span><span class="sxs-lookup"><span data-stu-id="97886-135">Note that hello script above uses a **Speed** property.</span></span> <span data-ttu-id="97886-136">No editor do Unity hello, atualize Olá velocidade propriedade too10.</span><span class="sxs-lookup"><span data-stu-id="97886-136">In hello Unity editor, update hello speed property too10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="97886-137">Acertos **reproduzir** em Olá Unity Editor.</span><span class="sxs-lookup"><span data-stu-id="97886-137">Hit **Play** in hello Unity Editor.</span></span> <span data-ttu-id="97886-138">Agora você deve ser capaz de toocontrol bola de hello usando o teclado de saudação e ele deve girar e mover-se.</span><span class="sxs-lookup"><span data-stu-id="97886-138">Now you should be able toocontrol hello ball using hello keyboard and it should rotate and move around.</span></span> 

### <a name="moving-hello-camera"></a><span data-ttu-id="97886-139">Câmera de saudação móvel</span><span class="sxs-lookup"><span data-stu-id="97886-139">Moving hello camera</span></span>
<span data-ttu-id="97886-140">Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e associam Olá **principal câmera** toohello **Player** objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-140">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie hello **Main Camera** toohello **Player** object.</span></span> 

1. <span data-ttu-id="97886-141">Saudação de atualização **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.</span><span class="sxs-lookup"><span data-stu-id="97886-141">Update hello **Transform.Position** toobe X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="97886-142">Saudação de atualização **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="97886-142">Update hello **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="97886-143">Adicionar um novo script chamado **CameraController** toohello **MainCamera** e mova-o na pasta de Scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-143">Add a new script called **CameraController** toohello **MainCamera** and move it under hello Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="97886-144">Abra o script hello para edição e adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="97886-144">Open up hello script for editing and add hello following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="97886-145">No ambiente do Unity - arraste variável do Player Olá no slot de Player de saudação do objeto de câmera principal Olá, de modo que hello dois estão associados com uma outra.</span><span class="sxs-lookup"><span data-stu-id="97886-145">In Unity environment - drag hello Player variable into hello Player slot for hello Main Camera object so that hello two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="97886-146">Agora se você clicar em executar no editor do Unity hello e objeto de bola de Player de saudação girar, em seguida, você verá Olá câmera subsequentes na movimentação de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-146">Now if you hit Play in hello Unity editor and rotate hello Player Ball object then you will see hello Camera following it in hello movement.</span></span>  

### <a name="setting-up-hello-play-area"></a><span data-ttu-id="97886-147">Configurando a área de reprodução Olá</span><span class="sxs-lookup"><span data-stu-id="97886-147">Setting up hello Play area</span></span>
<span data-ttu-id="97886-148">Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="97886-148">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="97886-149">Vamos criar hello paredes ao redor Olá zero para que hello Player bola objeto não remover fora da área de reprodução de saudação em seu movimento.</span><span class="sxs-lookup"><span data-stu-id="97886-149">We will create hello Walls surrounding hello Ground so that hello Player Ball object doesn't drop off hello play area in its movement.</span></span> 

1. <span data-ttu-id="97886-150">Clique em **Criar -> Criar Vazio -> Objeto de Jogo** e nomeie-o como **Paredes**</span><span class="sxs-lookup"><span data-stu-id="97886-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="97886-151">Nesse objeto Paredes, crie um novo **Objeto 3D -> Cubo** e nomeie-o como "Parede oeste".</span><span class="sxs-lookup"><span data-stu-id="97886-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="97886-152">Saudação de atualização **transformação -> posição** e **transformação -> escala** para este objeto de parede Oeste.</span><span class="sxs-lookup"><span data-stu-id="97886-152">Update hello **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="97886-153">Duplicar Olá Oeste parede toocreate um **parede Leste** com hello atualizado transformar posição e escala.</span><span class="sxs-lookup"><span data-stu-id="97886-153">Duplicate hello West wall toocreate an **East wall** with hello updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="97886-154">Duplicar Olá Leste parede toocreate um **parede Norte** com hello atualizado transformar posição & escala.</span><span class="sxs-lookup"><span data-stu-id="97886-154">Duplicate hello East wall toocreate a **North wall** with hello updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="97886-155">Duplicar parede de Norte hello e criar um **parede Sul** com hello atualizado transformar posição & escala.</span><span class="sxs-lookup"><span data-stu-id="97886-155">Duplicate hello North wall and create a **South wall** with hello updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="97886-156">Criação de objetos colecionáveis</span><span class="sxs-lookup"><span data-stu-id="97886-156">Creating Collectible objects</span></span>
<span data-ttu-id="97886-157">Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="97886-157">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="97886-158">Vamos criar alguns atraentes pesquisar objetos que formarão conjunto Olá dos objetos de coleção qual objeto de Player bola Olá precisa too'collect' por colisão com eles.</span><span class="sxs-lookup"><span data-stu-id="97886-158">We will create some attractive looking objects which will form hello set of collectible objects which hello Player Ball object needs too'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="97886-159">Crie um novo **Objeto Cubo 3D** e nomeie-o como Seleção.</span><span class="sxs-lookup"><span data-stu-id="97886-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="97886-160">Ajustar Olá **transformação -> rotação** & **transformação -> escala** do objeto de retirada de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-160">Adjust hello **Transform -> Rotation** & **Transform -> Scale** of hello Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="97886-161">Criar e anexar um **novo Script c#** chamado **AdRotator** toohello objeto de retirada.</span><span class="sxs-lookup"><span data-stu-id="97886-161">Create and attach a **new C# Script** called **Rotator** toohello Pickup object.</span></span> <span data-ttu-id="97886-162">Tornar-se de script de saudação de tooput sob a pasta de Scripts de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-162">Make sure tooput hello script under hello Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="97886-163">Abra esse script para edição e atualizá-lo Olá toobe a seguir:</span><span class="sxs-lookup"><span data-stu-id="97886-163">Open this script for editing and update it toobe hello following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="97886-164">Agora o modo de jogo Olá ocorrências em hello Unity Editor e a apresentação de retirada do objeto ser girando em seu eixo.</span><span class="sxs-lookup"><span data-stu-id="97886-164">Now hit hello Play mode in hello Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="97886-165">Crie uma nova pasta chamada **Pré-fabricados**</span><span class="sxs-lookup"><span data-stu-id="97886-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="97886-166">Saudação de arrastar **retirada** do objeto e colocá-la na pasta de Prefabs hello.</span><span class="sxs-lookup"><span data-stu-id="97886-166">Drag hello **Pickup** object and put it in hello Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="97886-167">Crie um novo **Objeto Jogo Vazio** chamado **Seleções**.</span><span class="sxs-lookup"><span data-stu-id="97886-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="97886-168">Redefinir tooorigin sua posição e, em seguida, arraste o objeto de retirada de saudação sob esse objeto de jogo.</span><span class="sxs-lookup"><span data-stu-id="97886-168">Reset its position tooorigin and then drag hello Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="97886-169">Olá duplicado **retirada** do objeto e distribuí-lo em Olá **Terra** objeto ao redor Olá **Player** objeto atualizando Olá **do Transform.Position X & Z**  valores adequadamente.</span><span class="sxs-lookup"><span data-stu-id="97886-169">Duplicate hello **Pickup** object and spread it on hello **Ground** object around hello **Player** object by updating hello **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="97886-170">Criar um **novo material** chamado **retirada** e atualizá-lo toobe vermelho na cor atualizando Olá **propriedade Albedo** toowhat semelhante que para a atualização Olá aterramento do objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-170">Create a **new material** called **Pickup** and update it toobe Red in color by updating hello **Albedo property** similar toowhat we did for updating hello Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="97886-171">Aplica objetos de retirada Olá tooall material Olá 4.</span><span class="sxs-lookup"><span data-stu-id="97886-171">Apply hello material tooall hello 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a><span data-ttu-id="97886-172">Coletar objetos retirada Olá</span><span class="sxs-lookup"><span data-stu-id="97886-172">Collecting hello Pickup objects</span></span>
<span data-ttu-id="97886-173">Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="97886-173">hello steps below are from hello [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="97886-174">Atualizaremos Olá Player para que ele seja capaz de too'collect' hello objetos retirados por colisão com eles.</span><span class="sxs-lookup"><span data-stu-id="97886-174">We will update hello Player so that it is able too'collect' hello pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="97886-175">Olá, abra **PlayerController** toohello anexado objeto de Player para edição de script e atualizá-lo toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="97886-175">Open up hello **PlayerController** script attached toohello Player object for editing and update it toohello following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="97886-176">Criar um novo **marca** chamado **escolher backup** (deve corresponder o que há no script hello)</span><span class="sxs-lookup"><span data-stu-id="97886-176">Create a new **Tag** called **Pick Up** (it must match what is in hello script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="97886-177">Aplicar esta **marca** objeto de retirada Prefab toohello.</span><span class="sxs-lookup"><span data-stu-id="97886-177">Apply this **Tag** toohello Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="97886-178">Habilitar **IsTrigger** caixa de seleção para o objeto de Prefab hello.</span><span class="sxs-lookup"><span data-stu-id="97886-178">Enable **IsTrigger** checkbox for hello Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="97886-179">Adicione um objeto do corpo rígida tooPickup Prefab.</span><span class="sxs-lookup"><span data-stu-id="97886-179">Add a Rigid body tooPickup Prefab object.</span></span> <span data-ttu-id="97886-180">Para otimizar o desempenho atualizaremos collider estático de saudação que usamos collider dinâmico tooa.</span><span class="sxs-lookup"><span data-stu-id="97886-180">For performance optimization we will update hello static collider that we used tooa Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="97886-181">Finalmente, verifique Olá **IsKinematic** propriedade Olá prefab do objeto.</span><span class="sxs-lookup"><span data-stu-id="97886-181">Finally check hello **IsKinematic** property for hello prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="97886-182">Acertos **reproduzir** no editor do Unity hello e você será capaz de tooplay **faça uma bola** jogo movendo Olá objeto Player usando teclas do teclado para a direção de entrada.</span><span class="sxs-lookup"><span data-stu-id="97886-182">Hit **Play** in hello Unity editor and you will be able tooplay this **Roll a Ball** game by moving hello Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-hello-game-for-mobile-play"></a><span data-ttu-id="97886-183">Atualizando Olá jogo Play móvel</span><span class="sxs-lookup"><span data-stu-id="97886-183">Updating hello game for mobile play</span></span>
<span data-ttu-id="97886-184">seções de saudação acima tutorial básico de saudação concluída do Unity.</span><span class="sxs-lookup"><span data-stu-id="97886-184">hello sections above concluded hello basic tutorial from Unity.</span></span> <span data-ttu-id="97886-185">Agora, vamos modificar Olá jogo toomake-amigável do dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="97886-185">Now we will modify hello game toomake it mobile device friendly.</span></span> <span data-ttu-id="97886-186">Observe que usamos entrada do teclado para Olá jogo até agora para teste.</span><span class="sxs-lookup"><span data-stu-id="97886-186">Note that we used keyboard input for hello game so far for testing.</span></span> <span data-ttu-id="97886-187">Agora podemos modificá-la para que podemos controlar player hello usando o movimento de saudação do hello telefone ou seja, usando o acelerômetro como entrada de saudação.</span><span class="sxs-lookup"><span data-stu-id="97886-187">Now we will modify it so that we can control hello player by using hello motion of hello phone i.e. using Accelerometer as hello input.</span></span> 

<span data-ttu-id="97886-188">Olá, abra **PlayerController** script para Olá edição e atualização **FixedUpdate** movimento de saudação do método toouse do objeto de Player Olá acelerômetro toomove hello.</span><span class="sxs-lookup"><span data-stu-id="97886-188">Open up hello **PlayerController** script for editing and update hello **FixedUpdate** method toouse hello motion from hello accelerometer toomove hello Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="97886-189">Esse tutorial conclui uma criação básica de jogo com Unity e você pode implantar isso em um dispositivo de jogo escolha tooplay hello.</span><span class="sxs-lookup"><span data-stu-id="97886-189">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice tooplay hello game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













