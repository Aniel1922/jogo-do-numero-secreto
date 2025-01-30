// Declara um array vazio para armazenar os números já sorteados.
let listaDeNumerosSorteados = [];
// Define o número máximo que pode ser sorteado.
let numeroLimite = 10;
// Gera o número secreto aleatório.
let numeroSecreto = gerarNumeroAleatorio();
// Inicializa o número de tentativas.
let tentativas = 1;

// Função para exibir texto em uma tag HTML e falar o texto usando o responsiveVoice.
function exibirTextoNaTela(tag, texto){
    // Seleciona o elemento HTML pela tag.
    let campo = document.querySelector(tag);
    // Define o texto do elemento HTML.
    campo.innerHTML = texto;
    // Usa o responsiveVoice para falar o texto.
    responsiveVoice.speak(texto, 'Brazilian Portuguese Female', {rate:1.2});
}

// Função para exibir a mensagem inicial do jogo.
function exibirMensagemInicial(){
    // Exibe o título do jogo.
    exibirTextoNaTela('h1', 'Jogo do número secreto');
    // Exibe a instrução para o jogador.
    exibirTextoNaTela('p', 'Escolha um número de 1 a 10');
}

// Chama a função para exibir a mensagem inicial.
exibirMensagemInicial();

// Função para verificar o chute do jogador.
function verificarChute(){
    // Obtém o valor do chute do jogador do campo de entrada.
    let chute = document.querySelector('input').value;

    // Verifica se o chute é igual ao número secreto.
    if(chute == numeroSecreto){
        // Exibe a mensagem de parabéns.
        exibirTextoNaTela('h1', 'Acertou!');
        // Determina se a palavra "tentativa" deve ser usada no singular ou plural.
        let palavraTentativa = tentativas > 1 ? 'tentativas' : 'tentativa';
        // Cria a mensagem com o número de tentativas.
        let mensagemTentativas = `Você descobriu o número secreto com ${tentativas} ${palavraTentativa}!`;
        // Exibe a mensagem com o número de tentativas.
        exibirTextoNaTela('p', mensagemTentativas);
        // Remove o atributo "disabled" do botão "Reiniciar".
        document.getElementById('reiniciar').removeAttribute('disabled');
    }else{
        // Verifica se o chute é maior que o número secreto.
        if(chute > numeroSecreto){
            // Exibe a mensagem "O número secreto é menor".
            exibirTextoNaTela('p', 'O número secreto é menor');
        }else{
            // Exibe a mensagem "O número secreto é maior".
            exibirTextoNaTela('p', 'O número secreto é maior');
        }
        // Incrementa o número de tentativas.
        tentativas++;
        // Limpa o campo de entrada.
        limparCampo();
    }
}

// Função para gerar um número aleatório.
function gerarNumeroAleatorio(){
    // Gera um número aleatório entre 1 e o número limite.
    let numeroEscolhido = parseInt(Math.random() * numeroLimite + 1);
    // Obtém a quantidade de números já sorteados.
    let quantidadeDeElementosNaLista =  listaDeNumerosSorteados.length;

    // Verifica se todos os números já foram sorteados.
    if(quantidadeDeElementosNaLista == numeroLimite){
        // Limpa a lista de números sorteados.
        listaDeNumerosSorteados = [];
    }
    // Adiciona o número escolhido à lista de números sorteados.
    listaDeNumerosSorteados.push(numeroEscolhido);
    // Exibe a lista de números sorteados no console.
    console.log(listaDeNumerosSorteados);
    // Retorna o número escolhido.
    return numeroEscolhido;
}

// Função para limpar o campo de entrada.
function limparCampo(){
    // Seleciona o campo de entrada.
    chute = document.querySelector('input');
    // Define o valor do campo de entrada como vazio.
    chute.value = '';
}

// Função para reiniciar o jogo.
function reiniciarJogo(){
    // Gera um novo número secreto.
    numeroSecreto = gerarNumeroAleatorio();
    // Limpa o campo de entrada.
    limparCampo();
    // Reseta o número de tentativas.
    tentativas = 1;
    // Exibe a mensagem inicial do jogo.
    exibirMensagemInicial();
    // Define o atributo "disabled" do botão "Reiniciar" como verdadeiro.
    document.getElementById('reiniciar').setAttribute('disabled', true);
}
