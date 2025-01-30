// Declara um array vazio para armazenar os números já sorteados.
let listaDeNumerosSorteados = [];

// Define o número máximo que pode ser sorteado.
let numeroLimite = 10;
// Gera o número secreto aleatório.
let numeroSecreto = gerarNumeroAleatorio();
// Inicializa o número de tentativas.
let tentativas = 1;

// Função para exibir texto em um elemento HTML e falar o texto.
function exibirTextoNaTela(tag, texto){
    // Seleciona o elemento HTML pela tag.
    let campo = document.querySelector(tag);
    // Define o texto do elemento HTML.
    campo.innerHTML = texto;
    // Usa a biblioteca responsiveVoice para falar o texto.
    responsiveVoice.speak(texto, 'Brazilian Portuguese Female', {rate:1.2});
}

// Função para exibir a mensagem inicial do jogo.
function exibirMensagemInicial(){
    // Exibe o título do jogo.
    exibirTextoNaTela('h1', 'Jogo do número secreto');
    // Exibe a mensagem para escolher um número.
    exibirTextoNaTela('p', 'Escolha um número de 1 a 10');
}

// Chama a função para exibir a mensagem inicial.
exibirMensagemInicial();

// Função para verificar o chute do jogador.
function verificarChute(){
    // Obtém o valor do chute do jogador.
    let chute = document.querySelector('input').value;

    // Verifica se o chute é igual ao número secreto.
    if(chute == numeroSecreto){
        // Exibe a mensagem de parabéns.
        exibirTextoNaTela('h1', 'Acertou!');
        // Define a palavra tentativa ou tentativas de acordo com o número de tentativas.
        let palavraTentativa = tentativas > 1 ? 'tentativas' : 'tentativa';
        // Exibe a mensagem com o número de tentativas.
        let mensagemTentativas = `Você descobriu o número secreto com ${tentativas} ${palavraTentativa}!`;
        exibirTextoNaTela('p', mensagemTentativas);
        // Remove o atributo disabled do botão reiniciar.
        document.getElementById('reiniciar').removeAttribute('disabled');
    }else{
        // Verifica se o chute é maior que o número secreto.
        if(chute > numeroSecreto){
            // Exibe a mensagem que o número secreto é menor.
            exibirTextoNaTela('p', 'O número secreto é menor');
        }else{
            // Exibe a mensagem que o número secreto é maior.
            exibirTextoNaTela('p', 'O número secreto é maior');
        }
        // Incrementa o número de tentativas.
        tentativas++;
        // Limpa o campo de chute.
        limparCampo();
    }
}

// Função para gerar um número aleatório.
function gerarNumeroAleatorio(){
    // Gera um número aleatório entre 1 e o número limite.
    let numeroEscolhido = parseInt(Math.random() * numeroLimite + 1);
    // Obtém a quantidade de elementos na lista de números sorteados.
    let quantidadeDeElementosNaLista =  listaDeNumerosSorteados.length;

    // Verifica se a lista de números sorteados está cheia.
    if(quantidadeDeElementosNaLista == numeroLimite){
        // Limpa a lista de números sorteados.
        listaDeNumerosSorteados = [];
    }else{
        // Adiciona o número escolhido na lista de números sorteados.
        listaDeNumerosSorteados.push(numeroEscolhido);
        // Exibe a lista de números sorteados no console.
        console.log(listaDeNumerosSorteados);
        // Retorna o número escolhido.
        return numeroEscolhido;
    }
}

// Função para limpar o campo de chute.
function limparCampo(){
    // Seleciona o campo de chute.
    chute = document.querySelector('input');
    // Limpa o valor do campo de chute.
    chute.value = '';
}

// Função para reiniciar o jogo.
function reiniciarJogo(){
    // Gera um novo número secreto.
    numeroSecreto = gerarNumeroAleatorio();
    // Limpa o campo de chute.
    limparCampo();
    // Reinicia o número de tentativas.
    tentativas = 1;
    // Exibe a mensagem inicial do jogo.
    exibirMensagemInicial();
    // Adiciona o atributo disabled ao botão reiniciar.
    document.getElementById('reiniciar').setAttribute('disabled', true);
}
