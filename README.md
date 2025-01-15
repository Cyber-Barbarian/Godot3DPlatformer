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
