# Relatório - Coelinhos da Páscoa

> [!CAUTION]
> - Lembre-se que você <ins>**não pode utilizar ferramentas de IA para
>   escrever este relatório**</ins>

## Dados do aluno

- **Cartão UFRGS**: <mark>`326011`</mark>
- **Nome**: <mark>`Leonardo Leal Linhares Dias`</mark>

## Passos que eu segui para resolver o problema especificado (em formato de *"prompt"*)

> [!IMPORTANT]
> - Coloque aqui todas as informações necessárias para que alguém
>   (pessoa ou ferramenta de IA) possa reproduzir os seus passos para
>   solucionar o problema
> - Escreva em formato imperativo, como se fosse um *prompt* com as
>   instruções a serem seguidas na solução do problema
> - Seja objetivo e conciso: quanto *menos palavras* você utilizar,
>   melhor
> - Seja técnico e use terminologia adequada: assuma que quem irá ler
>   os seus passos possui conhecimento de Ciência da Computação e
>   Computação Gráfica
> - Caso você queira incluir informações "longas" (como algum *prompt*
>   grande usado com alguma ferramenta de IA), crie arquivos à parte e
>   adicione links no texto (por exemplo, crie o arquivo `PROMPTS.md`
>   e adicione um link markdown `[os prompts detalhados estão
>   aqui](PROMPTS.md)`)
> - Novamente, lembre-se que você *não pode utilizar ferramentas
>   de IA para escrever este relatório*

<mark>Altere a string de criação da janela na chamada glfwCreateWindow do arquivo main.cpp para meu nome e cartão (326011 - Leonardo Leal Linhares Dias). Em shader_fragment.glsl, modifique as variáveis de refletância do modelo de Phong (Kd, Ks e q) nas estruturas condicionais de object_id, parametrizando o coelho com alta especularidade e cor dourada, a esfera como azul com baixo brilho e o plano como verde. No laço principal de renderização do main.cpp, multiplique o retorno de glfwGetTime() por 0.7 para reduzir a velocidade global do sistema e amplie a matriz de escala do PLANE para cobrir o novo raio de animação. Substitua as chamadas estáticas de desenho por um laço iterativo de 15 instâncias para gerar a ciranda de coelhos. Compute as posições X e Z utilizando coordenadas polares com um termo de tempo negativo para que o deslocamento seja no sentido anti-horário. Determine a posição vertical (Y) aplicando o módulo de uma função seno sobre uma fase composta pelo tempo e pelo índice de iteração. Construa a matriz hierárquica model_bunny_base contendo esta translação acoplada a uma rotação no eixo Y projetada para alinhar a face do modelo com a origem (0,0,0). Derive a matriz de renderização do coelho a partir desta base e utilize uma condicional modular (i % 4 == 0) para multiplicar uma rotação negativa no eixo X local, gerando o movimento de backflip proporcional à fase do salto. Para estruturar os dois ovos, herde exclusivamente a matriz model_bunny_base para isolá-los da matriz de backflip. Defina a atitude e cinemática de cada ovo compondo a pilha de matrizes com: translação lateral nos ombros (eixo X local), rotação orbital em X utilizando o dobro da frequência da fase do salto, translação de distanciamento equivalente ao raio da órbita (eixo Y local), rotação inversa em X para anular o momento angular e preservar a orientação vertical da geometria em relação ao mundo, e, finalmente, uma matriz de escala tridimensional não-uniforme para deformar a malha esférica no formato de um ovo.</mark>

## Principais dificuldades encontradas durante o desenvolvimento (formato livre)

<mark>A principal dificuldade teórica consistiu em gerenciar a herança de matrizes na modelagem hierárquica. Na minha primeira tentativa, as matrizes dos ovos derivavam da matriz final do coelho. Como resultado, quando o coelho realizava backflip, os ovos herdavam essa rotação extra. A solução encontrada foi criamor uma matriz "base" contendo apenas a translação global e a direção do movimento e a partir dessa matriz base, a rotação do salto mortal e a órbita dos ovos foram calculadas de forma independente.
Outro obstáculo significativo foi o mapeamento do sistema de coordenadas local do modelo 3D importado. A aplicação inicial da matriz de rotação para o pulo causava uma rolagem de lado no coelho. Através de ajustes e testes visuais, notei que o eixo longitudinal do modelo estava, na verdade, alinhado ao eixo X local. Isso exigiu a correção de todas as rotações do backflip e das órbitas para operarem em torno desse eixo específico.
Por fim, manter a orientação geométrica dos ovos estática em relação ao cenário enquanto orbitavam o coelho exigiu certo trabalho, no sentido de perceber o que estava ocorrendo e o motivo. A configuração direta das matrizes fazia com que as esferas girassem em torno de si mesmas durante a trajetória circular. Para corrigir esse comportamento e manter os ovos visualmente "em pé" durante toda a órbita, foi necessário aplicar uma matriz de rotação inversa na pilha de transformações logo antes da aplicação da escala geométrica, anulando o "giro local".</mark>

## Você acha que conseguiu resolver o problema de forma adequada?

<mark>Sim. O resultado apresentado se assemelha bastante com o vídeo de resultado esperado fornecido pelo professor. Porém, em meus testes, o FPS da animação estava bastante baixo (13 FPS, em média), o que creio que se deu pelo fato de estar executando no ambiente WSL, o qual não tem acesso a minha GPU de fato.</mark>

## Se você quiser compartilhar mais alguma coisa, coloque aqui:

<mark>`<preencher>`</mark>

## Se você possui alguma sugestão para o professor sobre esta atividade, coloque aqui:

<mark>`<preencher>`</mark>
