# Godot3DPlatformer
com base na série de vídeos presentes em https://www.youtube.com/watch?v=SsWGPSZZg-0&amp;list=PL-oJEh-N3A3R3jYDf3PAo1K364Xi6lLMk&amp;index=2


#parte 1 - Introdução
-criamos uma cena 3d com um node 3d simples
- o objeto tem vários gizmos de translação e rotação
- adicionamos como filho um cubo (mesh instance)
- na parte superior da engine, onde tem o símbolo de cubo, podemos fazer altações de posição e rotação locais e globais
- isso permite que rotacionemos somente o objeto ou o ambiente todo
- no 3d, diferente do 2d, precisamos criar uma câmera nas cenas para a godot entender que precisa renderizar
- a câmera possui uma opção preview para ajudar 
- adicionamos também uma luz solar

#parte 2 - Importando Objetos
- baixamos o platformer kit do kenney https://kenney.nl/assets/platformer-kit e extraimos na pasta de assets
- vamos manter somente os glb (ou gltf) models que é o que nos interessa
- ao selecionar um modelo 3d para importar a godot permite uma série de manipulações. vamos clicar em crate.gls e no menu da esquerda, em importar, ao lado de cena, veremos algumas propriedades.
- RigidBody -> sofre física
- vamos alterar o tipo de raiz para RigidBody pois queremos física aplicada a ele e vamos dar como nome raiz "crate" e dar um reimport
- é possível que os objetos 3d fiquem delocados devido à importaçõ pelo kenney. basta clicar no simbolo da cena, abrir no editor, novo herdado e ajustar o position dele para 0,0,0
- isso cria uma nova cena para o objeto. nela adicionamos o colision shape.
- na cena principal ("inicio") deletamos nossa crate e importamos agora a cena crate que criamos. excuímos nosso meshinstance anterior e conseguimos agora ver o crate na câmera
- se afastarmos do chão e rodarmos a cena vamos ver que a caixa agora cai, pois é um rigidBody com física aplicada
- vamos criar o chão. para isso criamos um nó do tipo staticbody, adicionamos uma mesh instance do tipo plane, redimensionamos 
- staticabody -> não sofre física
- falta colocarmos a colisão no nosso chão. para isso ao invés de adicionarmos um colision shape clicamos no nó de mesh instance do nosso chão e vemos na cena 3d o botão de malha aparecer
- ali podemos criar uma forma de colisão irmã trimesh, 
- isso gera um colision shape no mesmo nível do meshinstance, com as mesmas medidas
- duplicando os caixotes algumas vees e soltando de alturas diferentes podemos ver a física agir

#parte 3 - cenário
- todos os nossos materias do tipo "block....glb" vamos fazer um reimport alterando o root type para  NODE3D
- basta pesquisar por 'block  .glb' no filesystem da godot
- vamos de block-grass-corner-low.glb até block-snow.glb
- criamos uma cena MeshLibrary_001 do tipo node 3d
- vamos arrastar os blocks no formato glb (no nosso caso os grass large .glb) para a cena e prosseguir com abrir como herdado para cada um que desejarmos usar
- fazemos a criação de colisão assim como feito no plano mas ao inves de irmã trimesh usamos convexa simples e, ao inves de irmã, linkamos a um static body
- vamos repetir esse processo para muitos outros blocos que são usados na criação de cenário e excluir de nossa cena os que não precisaremos
- a medida que vamos salvando os blocos como novas cenas, deletamos eles da principal e reimportamos aquelas com colisão


- as cenas co colisão serão salvas na pasta MeshLibrary001

**** essa parte não é do tutorial
https://www.youtube.com/watch?v=JxbnStn-BIY
- criei uma cena chamada MeshLibrary01 onde jogei todas as minhas cenas de mapa, clicando e arrastando mesmo, fica tudo um sobre o outro
- no menu de topo clicamos em cena e exportamos como MeshLLbrary.tres o MeshLibrary.meshlib
- na cena do game adicionamo um novo nó do tipo gridmap e dentro desse gridmap jogamos nossa meshlibrary criada
- alteramos o tamanho da célula de nosso gridmap para (1.7,2,1.7) para se adequar aos nossos tiles sem deixar buraquinhos
- para posicionar os tiles no eixo xz basta mexer o mouse. a altura (y é governada pela propriedade chão, ou floor)
- esquerdo coloca o tile, direito apaga
- shift e select pode selecionar uma grande área e ctrl f a preencher
-para rotacionar o bloco nos eixos x, y e z podemos usar a,s,e d
*****


# criando o player
- para criaar o player usamos CharacterBody3D em nova cena
- adicionamos 2 mesh instance (um pro corpo e outro para direção) e um colision shape
- para o body mesh vamos usar um capsule mesh, alinhat no euxo y e colocar a escala em 0.5
- IMPORTANTE: para o colision sha´pe usamos um simples capsule shape. Se usarmos a mesma tecnica que usamos para o terreno a engine vei travar pois entesde o player como kinematic body e static body ao mesmo tempo
- posicionamos de forma que a base fique em 0.5
- criamos um mesh instance prismático em directionmeshinstance para apontar a frente, redimensionamos e encaixamos
- pintamos um mesh de cada cor para dar destaque (inspetor, material, new standard material)
- importamos um script e adicionmos uma função para rotacionar de acordo com o mouse
- temos agora um problema: ao girar estamos acessando o espaço global do personagem, o que causa conflitos de movimento. quero acessar o espaço local
- para resolver isso recorremos a transform.basis e ajustamos os valores do VEC3 default no código
- adicionamos uma câmera nas costas do player

#importando o asset de player
- vamos acessar o asset do kay kit (https://opengameart.org/content/kaykit-character-animations)
- em assets vamos abrir a pasta animations>gltf>KayKit_AnimatedCharacter 
- vamos primeiro clicar 2 vezes e abrir , ir na animação idle e ativar o loop
- vamos reimportar,  abrir como herdada e salvar a cena com o nome de animations
- o prototype pete tem as animações todas prontas 
- vamos clicar em nossa cena de animação e limpar herança. após isso vamos precisar qcriar os nós de ossos no skeleton
- vamos criar 6 one atatchments e nomear conforme está na animação
- baixamos o dungeon pack (https://opengameart.org/content/kaykit-dungeon-pack-10)
- de lá importamos os modelos de character mas so a pasta gltf
- vamos pegar então um dos personagens, abrir como cena herdada e salvar como newPlayer
- também iremos limpar a herança
- vamos arrastar a cena animations como um nó filho da nossa cena newPlayer
- nosso "pete" sobrescreveu, mas não tem problema. 
- no nó importado clicamos com o direito e vamos em editable children
- para cada mesh do nosso player arrastamos para um bone de nossa animação
- em seguida vamos esconder nosso prototypepete e vemos que as animações foram substituídas
- para encaixar armas nos slots de armas, basta procurar elas nos modelos e arrastar para a cena, como cena filha do slot
- ajustamos o escudo e a espada nso slot e alteramos os deslocamentos e ângulos dos mesmos
- importamos nosso newplayer pra dentro do nosso player como cena filha e lá ajeitamos altura e rotação
