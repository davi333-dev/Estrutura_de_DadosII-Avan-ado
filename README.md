🛡️ Guardiões da AVL — Jogo Didático de Árvores Balanceadas

Projeto desenvolvido para a disciplina de Estruturas de Dados II, do curso de Ciência da Computação.

O projeto consiste na proposta de um jogo educativo do gênero tower defense, com o objetivo de ensinar o funcionamento da árvore AVL por meio da participação ativa do estudante nas etapas de inserção de nós, diagnóstico do desequilíbrio e execução das rotações de rebalanceamento.

🎯 Objetivo

O objetivo do projeto é transformar o estudo da árvore AVL em uma atividade prática, na qual o jogador precisa identificar qual é o caso de desequilíbrio (LL, RR, LR ou RL) e executar corretamente a rotação necessária para restaurar a propriedade de balanceamento da árvore.

Dessa forma, o estudante não apenas observa a execução do rebalanceamento, mas precisa tomar a decisão de cada etapa sob pressão de tempo e recebe feedback imediato sobre suas escolhas.

📚 Contexto do Projeto

O projeto foi desenvolvido a partir da análise de um modelo existente denominado VisuAlgo, um visualizador de estruturas de dados e algoritmos voltado ao ensino, criado em 2011 pelo professor Steven Halim na National University of Singapore. A ferramenta original pode ser acessada em VisuAlgo — Binary Search Tree, AVL Tree.

O modelo analisado apresenta a árvore AVL por meio de animações das operações de inserção, remoção e busca. Entretanto, durante a análise realizada pelo grupo, foi identificada uma limitação didática na forma de interação: o rebalanceamento é executado integralmente pela ferramenta. O estudante informa o valor a ser inserido, e o programa detecta sozinho a violação do fator de balanceamento, classifica o caso e executa a rotação. Ao aluno cabe apenas assistir.

Como referência complementar, foi analisado o DEG4Trees, jogo educacional digital brasileiro sobre árvores binárias de busca e AVL, desenvolvido na Universidade Federal de Goiás (Barbosa et al., WEI/SBC, 2015). O modelo avança ao exigir interação do estudante, porém mantém o foco em responder perguntas sobre as propriedades da árvore, e não na execução da correção.

A proposta preserva a ideia de aprendizagem ativa, transferindo para o estudante as três responsabilidades que hoje ficam a cargo da ferramenta: o diagnóstico, o custo da operação e a consequência do erro.

⚙️ Funcionamento

O jogo é dividido em duas etapas que se alternam ao longo da partida:

1. Inserção das torres

Cada onda de inimigos traz adversários marcados com um número. O jogador posiciona a torre correspondente, e ela não é colocada onde ele aponta: desce pela árvore seguindo a regra da árvore binária de busca até encontrar sua posição.

Valor menor que o nó → subárvore esquerda
Valor maior que o nó → subárvore direita

2. Diagnóstico e rebalanceamento

Após cada inserção, o fator de balanceamento de cada torre é recalculado e exibido em uma barra acima dela. Quando o valor sai do intervalo permitido, um alarme é disparado e o jogador tem poucos segundos para identificar o caso e executar a rotação.

FB(nó) = altura(subárvore esquerda) − altura(subárvore direita)
AVL válida: FB ∈ {-1, 0, +1}

A altura da árvore determina o tempo de recarga do disparo: o tiro sai da raiz e percorre os nós até a torre alvo, custando um décimo de segundo por nível.

Tempo de recarga = níveis percorridos × 0,1s
Altura ideal     = ⌈log₂(n + 1)⌉

Uma partida completa tem 10 ondas, e a cada nova onda chegam mais inimigos, o tempo de alarme diminui e a energia disponível é reduzida.

🕹️ Mecânica do Jogo

O jogador deve identificar qual dos quatro casos de desequilíbrio ocorreu e executar a sequência de gestos correspondente. O jogo exibe o desenho da árvore, mas nunca informa qual é o caso.

⚠️  ALARME — Torre 50 com FB = +2
    Qual é o caso?  [ LL ]  [ RR ]  [ LR ]  [ RL ]
Caso	Como aparece	Gesto
LL	A torre pende para a esquerda e o filho esquerdo também	1 gesto: girar a torre para a direita
RR	A torre pende para a direita e o filho direito também	1 gesto: girar a torre para a esquerda
LR	A torre pende para a esquerda, mas o filho pende para a direita	2 gestos: girar o filho para a esquerda, depois a torre para a direita
RL	A torre pende para a direita, mas o filho pende para a esquerda	2 gestos: girar o filho para a direita, depois a torre para a esquerda

✅ Acerto

Quando a rotação escolhida é a correta:

a árvore é rebalanceada e a altura diminui;
o tempo de recarga do disparo volta a ser curto;
a onda é contida e o jogo prossegue.

❌ Erro

Quando a rotação escolhida é a incorreta:

a energia é consumida mesmo assim, sem corrigir o desequilíbrio;
o alarme continua contando;
o jogador precisa diagnosticar novamente com menos recursos.
🏆 Condições de Vitória e Derrota

Vitória

Sobreviver às 10 ondas com a base intacta e com todas as torres dentro do intervalo {-1, 0, +1} — ou seja, com a árvore ainda sendo uma AVL válida.

Pontuação máxima da fase: se a altura final for a menor possível para a quantidade de torres em jogo, ⌈log₂(n + 1)⌉, o jogador recebe estrelas extras. É o prêmio por manter a árvore efetivamente compacta, e não apenas dentro do limite.

Derrota

A base cai quando a árvore degenera em lista encadeada. Na prática, isso ocorre de três formas:

deixar uma torre com FB fora de {-1, 0, +1} até o alarme zerar — a torre desaba e derruba os filhos junto;
deixar a altura ultrapassar o limite da AVL — o caminho da raiz até a folha passa a ser O(n) em vez de O(log n), e o disparo não chega a tempo;
ficar sem energia com o alarme ligado — sem energia não há rotação, e a árvore trava desequilibrada.

A ideia central que o estudante leva da partida:

árvore torta = tiro lento = derrota
🧠 Conceitos de Estruturas de Dados

O projeto utiliza e demonstra conceitos fundamentais relacionados a árvores balanceadas:

Árvore binária de busca;
Regra de inserção por comparação de chaves;
Altura de árvore e de subárvore;
Fator de balanceamento;
Propriedade de balanceamento da AVL;
Rotação simples à esquerda e à direita;
Rotação dupla (LR e RL);
Diagnóstico dos quatro casos de desequilíbrio;
Relação entre altura e custo de busca;
Complexidade O(log n) e degeneração para O(n);
Participação interativa na execução do rebalanceamento.
📌 Status do Projeto

O projeto encontra-se na fase de documentação e design. O que existe até o momento é o Game Design Document, que descreve a proposta, o diagnóstico do modelo reutilizado, o mapeamento dos conceitos de Estruturas de Dados para as mecânicas de gameplay e as condições de vitória e derrota.

O jogo ainda não foi implementado. As mecânicas descritas nas seções acima correspondem ao comportamento previsto na proposta, e não a um programa em execução.

📁 Arquivos do Projeto
📦 Guardiões da AVL
 ├── 📄 Game Design Document - Guardiões da AVL.docx
 ├── 📄 Guia de Atividade Prática do Estudante - Design de Jogos sobre Árvores Avançadas.pdf
 └── 📄 README.md

Game Design Document - Guardiões da AVL.docx

Documento principal do projeto. Contém:

identificação do grupo;
resumo da proposta;
diagnóstico do modelo reutilizado (VisuAlgo e DEG4Trees);
justificativa da estrutura de dados selecionada;
mapeamento dos conceitos de ED II em mecânicas de gameplay;
regras do core loop e condições de vitória e derrota;
roteiro do pitch de apresentação;
referências bibliográficas.
👥 Integrantes
Davi Reis Ribeiro
Antônio Marcos
Webster Dantas
Arthur Henriques

Disciplina: Estruturas de Dados II · Curso: Ciência da Computação · Data: 17/09/2026

📌 Proposta Educacional

O projeto busca aplicar o conceito de aprender fazendo, transformando o rebalanceamento da árvore AVL em uma decisão que precisa ser tomada pelo jogador.

Em vez de simplesmente animar a rotação automaticamente, a proposta exige que o estudante observe o desenho da árvore, identifique qual dos quatro casos ocorreu e execute a sequência correta de rotações antes que o tempo se esgote.

Assim, o jogo funciona como ferramenta de apoio ao aprendizado, permitindo relacionar o fator de balanceamento com a forma visual da árvore e compreender, de maneira prática, por que a diferença entre O(log n) e O(n) importa.

Em uma frase: o VisuAlgo ensina mostrando; o nosso jogo ensina fazendo.
