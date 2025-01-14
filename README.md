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
