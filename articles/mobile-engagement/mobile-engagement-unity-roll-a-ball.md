---
title: Tutorial do Roll a Ball do Unity
description: "Etapas para criar o jogo clássico Roll a Ball do Unity que é um pré-requisito para todos os tutoriais do Unity do Mobile Engagement"
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
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="cad64-103"><a id="unity-roll-a-ball"></a>Criar um jogo Roll a Ball do Unity</span><span class="sxs-lookup"><span data-stu-id="cad64-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="cad64-104">Este tutorial explica as etapas principais para um [Tutorial do Roll a Ball do Unity](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial) ligeiramente modificado.</span><span class="sxs-lookup"><span data-stu-id="cad64-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="cad64-105">Esse jogo de exemplo consiste em um objeto 'jogador' esférico que é controlado pelo usuário do aplicativo. O objetivo do jogo é 'colecionar' objetos colecionáveis colidindo o objeto jogador contra os objetos colecionáveis.</span><span class="sxs-lookup"><span data-stu-id="cad64-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="cad64-106">Isso pressupõe familiaridade básica com o ambiente de editor do Unity.</span><span class="sxs-lookup"><span data-stu-id="cad64-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="cad64-107">Se tiver problemas, consulte o tutorial completo.</span><span class="sxs-lookup"><span data-stu-id="cad64-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="cad64-108">Configuração do jogo</span><span class="sxs-lookup"><span data-stu-id="cad64-108">Setting up the game</span></span>
<span data-ttu-id="cad64-109">As etapas a seguir são do [Tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="cad64-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="cad64-110">Abra o **Editor do Unity** e clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="cad64-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="cad64-111">Forneça um **Nome do projeto** & **Local**, selecione **3D** e clique em **Criar projeto**.</span><span class="sxs-lookup"><span data-stu-id="cad64-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="cad64-112">Salve a cena padrão recém-criada como parte do novo projeto como com o nome **MiniJogo** em uma nova pasta **\_Cenas** na pasta **Ativos**:</span><span class="sxs-lookup"><span data-stu-id="cad64-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="cad64-113">Crie um **Objeto 3D -> Plano** como o campo de jogo e renomeie esse objeto de plano como **Solo**</span><span class="sxs-lookup"><span data-stu-id="cad64-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="cad64-114">Redefina o componente de transformação do objeto **Solo** para que ele esteja na Origem.</span><span class="sxs-lookup"><span data-stu-id="cad64-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="cad64-115">Desmarque **Mostrar Grade** no **Menu Gizmos** para o objeto **Solo**.</span><span class="sxs-lookup"><span data-stu-id="cad64-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="cad64-116">Atualize o componente **Escala** para que o objeto **Solo** seja [X = 2,Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="cad64-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="cad64-117">Adicione um novo **Objeto 3D -> Esfera** ao projeto e renomeie este objeto de esfera como **Jogador**.</span><span class="sxs-lookup"><span data-stu-id="cad64-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="cad64-118">Selecione o objeto **Jogador** e clique em **Redefinir Transformação**, de forma semelhante ao objeto Plano.</span><span class="sxs-lookup"><span data-stu-id="cad64-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="cad64-119">Atualize o componente **Transformação -> Posição -> Coordenada Y** para o Jogador Y como 0,5.</span><span class="sxs-lookup"><span data-stu-id="cad64-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="cad64-120">Crie uma nova pasta chamada **Materiais** no projeto em que vamos criar o material para colorir o jogador.</span><span class="sxs-lookup"><span data-stu-id="cad64-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="cad64-121">Crie um novo **Material** chamado **Tela de fundo** nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="cad64-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="cad64-122">Atualize a cor do material atualizando a respectiva propriedade **Albedo** .</span><span class="sxs-lookup"><span data-stu-id="cad64-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="cad64-123">Você pode selecionar os valores RGB de [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="cad64-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="cad64-124">Arraste esse material para exibição de cena para aplicar cor ao objeto **Solo** .</span><span class="sxs-lookup"><span data-stu-id="cad64-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="cad64-125">Finalmente, atualize a **Transformação -> Rotação -> Y** para 60 no objeto de Luz Direcional para obter claridade.</span><span class="sxs-lookup"><span data-stu-id="cad64-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="cad64-126">Movimentação do jogador</span><span class="sxs-lookup"><span data-stu-id="cad64-126">Moving the player</span></span>
<span data-ttu-id="cad64-127">As etapas a seguir são do [Tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="cad64-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="cad64-128">Adicione um componente **RigidBody** ao objeto **Jogador**.</span><span class="sxs-lookup"><span data-stu-id="cad64-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="cad64-129">Crie uma nova pasta chamada **Scripts** no projeto.</span><span class="sxs-lookup"><span data-stu-id="cad64-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="cad64-130">Clique em **Adicionar Componente -> Novo Script -> Script em C#**.</span><span class="sxs-lookup"><span data-stu-id="cad64-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="cad64-131">Nomeie-o como **PlayerController** e clique em **Criar e Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cad64-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="cad64-132">Isso criará e anexará um script ao objeto Jogador.</span><span class="sxs-lookup"><span data-stu-id="cad64-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="cad64-133">Mova esse script para a pasta **Scripts** no projeto.</span><span class="sxs-lookup"><span data-stu-id="cad64-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="cad64-134">Abra o script para edição em seu editor de script favorito, atualize o código do script com o código a seguir e salve-o.</span><span class="sxs-lookup"><span data-stu-id="cad64-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
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
6. <span data-ttu-id="cad64-135">Observe que o script acima usa uma propriedade **Velocidade** .</span><span class="sxs-lookup"><span data-stu-id="cad64-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="cad64-136">No editor do Unity, atualize a propriedade de velocidade para 10.</span><span class="sxs-lookup"><span data-stu-id="cad64-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="cad64-137">Pressione **Reproduzir** no Editor do Unity.</span><span class="sxs-lookup"><span data-stu-id="cad64-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="cad64-138">Agora você deve ser capaz de controlar a bola usando o teclado, e ela deve girar e mover-se.</span><span class="sxs-lookup"><span data-stu-id="cad64-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="cad64-139">Movimentação da câmera</span><span class="sxs-lookup"><span data-stu-id="cad64-139">Moving the camera</span></span>
<span data-ttu-id="cad64-140">As etapas a seguir são do [Tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e vincularão a **Câmera Principal** ao objeto **Jogador**.</span><span class="sxs-lookup"><span data-stu-id="cad64-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="cad64-141">Atualize **Transform.Position** para ser X = 0, Y = 10,5, Z=-10.</span><span class="sxs-lookup"><span data-stu-id="cad64-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="cad64-142">Atualize **Transform.Rotation** para ser X = 45, Y = 0, Z = 0.</span><span class="sxs-lookup"><span data-stu-id="cad64-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="cad64-143">Adicione um novo script chamado **CameraController** a **MainCamera** e mova-o para a pasta Scripts.</span><span class="sxs-lookup"><span data-stu-id="cad64-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="cad64-144">Abra o script para edição e adicione o seguinte código a ele:</span><span class="sxs-lookup"><span data-stu-id="cad64-144">Open up the script for editing and add the following code in it:</span></span>
   
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
5. <span data-ttu-id="cad64-145">No ambiente do Unity, arraste a variável Jogador para o slot de Jogador do objeto de Câmera Principal, para que os dois sejam associados um ao outro.</span><span class="sxs-lookup"><span data-stu-id="cad64-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="cad64-146">Agora, se pressionar Reproduzir no editor do Unity e girar o objeto Bola do Jogador, você verá a Câmera seguindo-o em movimento.</span><span class="sxs-lookup"><span data-stu-id="cad64-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="cad64-147">Configuração da área de jogo</span><span class="sxs-lookup"><span data-stu-id="cad64-147">Setting up the Play area</span></span>
<span data-ttu-id="cad64-148">As etapas a seguir são do [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="cad64-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="cad64-149">Criaremos as Paredes em torno do Solo para que o objeto Bola do Jogador não vá para fora da área de jogo durante sua movimentação.</span><span class="sxs-lookup"><span data-stu-id="cad64-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="cad64-150">Clique em **Criar -> Criar Vazio -> Objeto de Jogo** e nomeie-o como **Paredes**</span><span class="sxs-lookup"><span data-stu-id="cad64-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="cad64-151">Nesse objeto Paredes, crie um novo **Objeto 3D -> Cubo** e nomeie-o como "Parede oeste".</span><span class="sxs-lookup"><span data-stu-id="cad64-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="cad64-152">Atualize a **Transformação -> Posição** e a **Transformação -> Escala** para esse objeto Parede Oeste.</span><span class="sxs-lookup"><span data-stu-id="cad64-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="cad64-153">Duplique a parede Oeste para criar uma **Parede leste** com a escala e a posição de transformação atualizadas.</span><span class="sxs-lookup"><span data-stu-id="cad64-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="cad64-154">Duplique a parede Leste para criar uma **Parede norte** com a escala e a posição de transformação atualizadas.</span><span class="sxs-lookup"><span data-stu-id="cad64-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="cad64-155">Duplique a parede Norte e crie uma **Parede sul** com a escala e a posição de transformação atualizadas.</span><span class="sxs-lookup"><span data-stu-id="cad64-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="cad64-156">Criação de objetos colecionáveis</span><span class="sxs-lookup"><span data-stu-id="cad64-156">Creating Collectible objects</span></span>
<span data-ttu-id="cad64-157">As etapas a seguir são do [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="cad64-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="cad64-158">Vamos criar alguns objetos de aparência atraente que formarão o conjunto de objetos colecionáveis que o objeto Bola de Jogador precisa 'colecionar' colidindo com eles.</span><span class="sxs-lookup"><span data-stu-id="cad64-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="cad64-159">Crie um novo **Objeto Cubo 3D** e nomeie-o como Seleção.</span><span class="sxs-lookup"><span data-stu-id="cad64-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="cad64-160">Ajuste a **Transformação -> Rotação** & **Transformação -> Escala** do objeto Seleção.</span><span class="sxs-lookup"><span data-stu-id="cad64-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="cad64-161">Crie e anexe um **novo Script em C#** chamado **Rotor** ao objeto Seleção.</span><span class="sxs-lookup"><span data-stu-id="cad64-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="cad64-162">Coloque o script na pasta Scripts.</span><span class="sxs-lookup"><span data-stu-id="cad64-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="cad64-163">Abra esse script para edição e atualize-o para ser o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cad64-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="cad64-164">Agora, pressione o modo de Reprodução no Editor do Unity, e o objeto Seleção será mostrado girando em seu eixo.</span><span class="sxs-lookup"><span data-stu-id="cad64-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="cad64-165">Crie uma nova pasta chamada **Pré-fabricados**</span><span class="sxs-lookup"><span data-stu-id="cad64-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="cad64-166">Arraste o objeto **Seleção** e coloque-o na pasta Pré-fabricados.</span><span class="sxs-lookup"><span data-stu-id="cad64-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="cad64-167">Crie um novo **Objeto Jogo Vazio** chamado **Seleções**.</span><span class="sxs-lookup"><span data-stu-id="cad64-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="cad64-168">Redefina sua posição para a origem e arraste o objeto Seleção para baixo desse objeto de jogo.</span><span class="sxs-lookup"><span data-stu-id="cad64-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="cad64-169">Duplique o objeto **Seleção** e distribua-o no objeto **Solo** ao redor do objeto **Jogador** atualizando os valores **X e Z de Transform.Position** adequadamente.</span><span class="sxs-lookup"><span data-stu-id="cad64-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="cad64-170">Crie um **novo material** chamado **Seleção** e atualize-o para ter a cor vermelha atualizando a **Propriedade Albedo**, de forma semelhante ao que foi feito para atualizar o objeto Solo.</span><span class="sxs-lookup"><span data-stu-id="cad64-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="cad64-171">Aplique o material a todos os quatro objetos Seleção.</span><span class="sxs-lookup"><span data-stu-id="cad64-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="cad64-172">Coleta dos objetos Seleção</span><span class="sxs-lookup"><span data-stu-id="cad64-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="cad64-173">As etapas a seguir são do [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="cad64-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="cad64-174">Atualizaremos o Jogador para que ele seja capaz de 'colecionar' os objetos Seleção colidindo com eles.</span><span class="sxs-lookup"><span data-stu-id="cad64-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="cad64-175">Abra o script **PlayerController** anexado ao objeto Jogador para edição e atualize-o para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cad64-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
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
2. <span data-ttu-id="cad64-176">Crie uma nova **Marca** chamada **Seleção** (ela deve corresponder ao que está no script)</span><span class="sxs-lookup"><span data-stu-id="cad64-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="cad64-177">Aplique essa **Marca** ao objeto Seleção de Pré-fabricado.</span><span class="sxs-lookup"><span data-stu-id="cad64-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="cad64-178">Habilite a caixa de seleção **IsTrigger** para o objeto Pré-fabricado.</span><span class="sxs-lookup"><span data-stu-id="cad64-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="cad64-179">Adicione um corpo Rígido ao objeto Seleção de Pré-fabricado.</span><span class="sxs-lookup"><span data-stu-id="cad64-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="cad64-180">Para otimizar o desempenho, atualizaremos o colisor estático que usamos para um colisor Dinâmico.</span><span class="sxs-lookup"><span data-stu-id="cad64-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="cad64-181">Finalmente, marque a propriedade **IsKinematic** do objeto pré-fabricado.</span><span class="sxs-lookup"><span data-stu-id="cad64-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="cad64-182">Pressione **Reproduzir** no editor do Unity e você poderá jogar o **Roll a Ball** movendo o objeto Jogador com as teclas do teclado para indicar a direção.</span><span class="sxs-lookup"><span data-stu-id="cad64-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="cad64-183">Atualização do jogo para celular</span><span class="sxs-lookup"><span data-stu-id="cad64-183">Updating the game for mobile play</span></span>
<span data-ttu-id="cad64-184">As seções acima concluíram o tutorial básico do Unity.</span><span class="sxs-lookup"><span data-stu-id="cad64-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="cad64-185">Agora, modificaremos o jogo para que ele seja compatível com dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="cad64-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="cad64-186">Observe que, até o momento, usamos a entrada do teclado no jogo para teste.</span><span class="sxs-lookup"><span data-stu-id="cad64-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="cad64-187">Agora, vamos modificá-lo para que possamos controlar o jogador usando o movimento do telefone, ou seja,</span><span class="sxs-lookup"><span data-stu-id="cad64-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="cad64-188">usando o Acelerômetro como entrada.</span><span class="sxs-lookup"><span data-stu-id="cad64-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="cad64-189">Abra o script **PlayerController** para editar e atualizar o método **FixedUpdate** de forma a usar o movimento do acelerômetro para mover o objeto Jogador.</span><span class="sxs-lookup"><span data-stu-id="cad64-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="cad64-190">Esse tutorial conclui a criação de um jogo básico com o Unity, e você pode implantá-lo em um dispositivo de sua escolha para jogá-lo.</span><span class="sxs-lookup"><span data-stu-id="cad64-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

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













