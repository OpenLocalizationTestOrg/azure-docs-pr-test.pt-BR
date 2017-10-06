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
# <a id="unity-roll-a-ball"></a>Criar um jogo Roll a Ball do Unity
Este tutorial orienta pelas etapas principais para um pouco modificada a saudação [Unity reverter um tutorial de bola](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial). O jogo de exemplo consiste em um objeto Esférico 'player' que é controlado pelo usuário do aplicativo hello e objetivo de saudação do jogo Olá é too'collect' coleção objetos pelo objeto de player Olá colisão com esses objetos de coleção. Isso pressupõe familiaridade básica com o ambiente de editor do Unity. Se você tiver algum problema, em seguida, você deve consultar o tutorial completo toohello. 

### <a name="setting-up-hello-game"></a>Configurando o jogo Olá
Olá etapas a seguir são de saudação [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)

1. Abra o **Editor do Unity** e clique em **Novo**. 
   
    ![][51] 
2. Forneça um **Nome do projeto** & **Local**, selecione **3D** e clique em **Criar projeto**.
   
    ![][52]
3. Salvar cena de padrão de saudação acabou de criar como parte do novo projeto de saudação assim como acontece com nome hello **MiniGame** dentro de um novo  **\_cenas** pasta sob **ativos** pasta:
   
    ![][53]
4. Criar um **objeto 3D -> plano** como Olá reproduzindo campo e renomear este objeto de plano como **Terra**
   
    ![][1]
5. Componente de transformação de saudação de redefinição para este **Terra** para que ele seja Olá origem do objeto. 
   
    ![][3]
6. Desmarque **Mostrar grade de** de **menu largue as** para Olá **Terra** objeto.
   
    ![][4]
7. Saudação de atualização **escala** componente para Olá **Terra** objeto toobe [X = 2, Y = 1, Z = 2]. 
   
    ![][5]
8. Adicionar um novo **objeto 3D -> esfera** toohello projeto e renomear este esfera de objeto como **Player**. 
   
    ![][6]
9. Selecione Olá **Player** do objeto e clique em **redefinir transformação** objeto de plano toohello semelhante. 
10. Atualização **transformação -> Posição -> coordenada Y** componente para Olá Player Y como 0,5.  
    
    ![][7]
11. Criar uma nova pasta chamada **material** no projeto Olá onde criaremos player de saudação do hello toocolor material. 
12. Crie um novo **Material** chamado **Tela de fundo** nessa pasta. 
    
    ![][8]
13. Atualizar cor de saudação do material Olá atualizando Olá **Albedo** propriedade dele. Você pode selecionar valores RGB de saudação do [0,32,64]. 
    
    ![][9]
14. Arraste este material para Olá cena exibição tooapply cor toohello **Terra** objeto. 
    
    ![][10]
15. Atualizar finalmente Olá **transformação -> rotação -> Y** too60 no objeto de luz direcional Olá para maior clareza. 
    
    ![][12]

### <a name="moving-hello-player"></a>Player de saudação móvel
Olá etapas a seguir são de saudação [tutorial do Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)

1. Adicionar um **RigidBody** componente toohello **Player** objeto. 
   
    ![][13]
2. Criar uma nova pasta chamada **Scripts** no projeto de saudação. 
3. Clique em **Adicionar Componente -> Novo Script -> Script em C#**. Nomeie-o como **PlayerController** e clique em **Criar e Adicionar**. Isso criará e anexar um objeto do script toohello Player.  
   
    ![][14]
4. Mover esse script em Olá **Scripts** pasta no projeto de saudação. 
5. Abra script hello para edição em seu editor favorito de script, atualize o código de script hello com hello código a seguir e salvá-lo. 
   
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
6. Observe o script hello acima usa um **velocidade** propriedade. No editor do Unity hello, atualize Olá velocidade propriedade too10.  
   
    ![][15]
7. Acertos **reproduzir** em Olá Unity Editor. Agora você deve ser capaz de toocontrol bola de hello usando o teclado de saudação e ele deve girar e mover-se. 

### <a name="moving-hello-camera"></a>Câmera de saudação móvel
Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e associam Olá **principal câmera** toohello **Player** objeto. 

1. Saudação de atualização **Transform.Position** toobe X = 0, Y = 10.5, Z =-10.  
2. Saudação de atualização **Transform.Rotation** toobe X = 45, Y = 0, Z = 0.  
   
    ![][16]
3. Adicionar um novo script chamado **CameraController** toohello **MainCamera** e mova-o na pasta de Scripts de saudação. 
   
    ![][17]
4. Abra o script hello para edição e adicione Olá código a seguir:
   
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
5. No ambiente do Unity - arraste variável do Player Olá no slot de Player de saudação do objeto de câmera principal Olá, de modo que hello dois estão associados com uma outra. 
   
    ![][18]
6. Agora se você clicar em executar no editor do Unity hello e objeto de bola de Player de saudação girar, em seguida, você verá Olá câmera subsequentes na movimentação de saudação.  

### <a name="setting-up-hello-play-area"></a>Configurando a área de reprodução Olá
Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141). Vamos criar hello paredes ao redor Olá zero para que hello Player bola objeto não remover fora da área de reprodução de saudação em seu movimento. 

1. Clique em **Criar -> Criar Vazio -> Objeto de Jogo** e nomeie-o como **Paredes**
   
    ![][19]
2. Nesse objeto Paredes, crie um novo **Objeto 3D -> Cubo** e nomeie-o como "Parede oeste". 
   
    ![][20]
3. Saudação de atualização **transformação -> posição** e **transformação -> escala** para este objeto de parede Oeste. 
   
    ![][21]
4. Duplicar Olá Oeste parede toocreate um **parede Leste** com hello atualizado transformar posição e escala. 
   
    ![][22]
5. Duplicar Olá Leste parede toocreate um **parede Norte** com hello atualizado transformar posição & escala. 
   
    ![][23]
6. Duplicar parede de Norte hello e criar um **parede Sul** com hello atualizado transformar posição & escala. 
   
    ![][24]

### <a name="creating-collectible-objects"></a>Criação de objetos colecionáveis
Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141). Vamos criar alguns atraentes pesquisar objetos que formarão conjunto Olá dos objetos de coleção qual objeto de Player bola Olá precisa too'collect' por colisão com eles. 

1. Crie um novo **Objeto Cubo 3D** e nomeie-o como Seleção. 
2. Ajustar Olá **transformação -> rotação** & **transformação -> escala** do objeto de retirada de saudação. 
   
    ![][25]
3. Criar e anexar um **novo Script c#** chamado **AdRotator** toohello objeto de retirada. Tornar-se de script de saudação de tooput sob a pasta de Scripts de saudação. 
   
    ![][26]
4. Abra esse script para edição e atualizá-lo Olá toobe a seguir: 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. Agora o modo de jogo Olá ocorrências em hello Unity Editor e a apresentação de retirada do objeto ser girando em seu eixo.
6. Crie uma nova pasta chamada **Pré-fabricados** 
   
    ![][27]
7. Saudação de arrastar **retirada** do objeto e colocá-la na pasta de Prefabs hello.
   
    ![][28]
8. Crie um novo **Objeto Jogo Vazio** chamado **Seleções**. Redefinir tooorigin sua posição e, em seguida, arraste o objeto de retirada de saudação sob esse objeto de jogo.  
   
    ![][29]
9. Olá duplicado **retirada** do objeto e distribuí-lo em Olá **Terra** objeto ao redor Olá **Player** objeto atualizando Olá **do Transform.Position X & Z**  valores adequadamente. 
   
    ![][30]
10. Criar um **novo material** chamado **retirada** e atualizá-lo toobe vermelho na cor atualizando Olá **propriedade Albedo** toowhat semelhante que para a atualização Olá aterramento do objeto. 
    
    ![][31]
11. Aplica objetos de retirada Olá tooall material Olá 4.
    
    ![][32]

### <a name="collecting-hello-pickup-objects"></a>Coletar objetos retirada Olá
Olá etapas a seguir são de saudação [tutorial Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141). Atualizaremos Olá Player para que ele seja capaz de too'collect' hello objetos retirados por colisão com eles. 

1. Olá, abra **PlayerController** toohello anexado objeto de Player para edição de script e atualizá-lo toohello a seguir:  
   
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
2. Criar um novo **marca** chamado **escolher backup** (deve corresponder o que há no script hello)  
   
    ![][33]
   
    ![][34]
3. Aplicar esta **marca** objeto de retirada Prefab toohello. 
   
    ![][35]
4. Habilitar **IsTrigger** caixa de seleção para o objeto de Prefab hello.
   
    ![][36]
5. Adicione um objeto do corpo rígida tooPickup Prefab. Para otimizar o desempenho atualizaremos collider estático de saudação que usamos collider dinâmico tooa. 
   
    ![][37]
6. Finalmente, verifique Olá **IsKinematic** propriedade Olá prefab do objeto. 
   
    ![][38]
7. Acertos **reproduzir** no editor do Unity hello e você será capaz de tooplay **faça uma bola** jogo movendo Olá objeto Player usando teclas do teclado para a direção de entrada. 

### <a name="updating-hello-game-for-mobile-play"></a>Atualizando Olá jogo Play móvel
seções de saudação acima tutorial básico de saudação concluída do Unity. Agora, vamos modificar Olá jogo toomake-amigável do dispositivo móvel. Observe que usamos entrada do teclado para Olá jogo até agora para teste. Agora podemos modificá-la para que podemos controlar player hello usando o movimento de saudação do hello telefone ou seja, usando o acelerômetro como entrada de saudação. 

Olá, abra **PlayerController** script para Olá edição e atualização **FixedUpdate** movimento de saudação do método toouse do objeto de Player Olá acelerômetro toomove hello. 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

Esse tutorial conclui uma criação básica de jogo com Unity e você pode implantar isso em um dispositivo de jogo escolha tooplay hello. 

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













