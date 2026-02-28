<!DOCTYPE html>
<html lang="pt-br">
<head>
<meta charset="UTF-8">
<title>Show do Milhão Bíblico</title>
<style>
body {
    font-family: Arial, sans-serif;
    background: radial-gradient(circle, #001f4d, #000814);
    color: white;
    text-align: center;
    padding: 20px;
}
.container {
    max-width: 750px;
    margin: auto;
    background: #012a4a;
    padding: 25px;
    border-radius: 15px;
    box-shadow: 0 0 25px gold;
}
h1 { color: gold; }
button {
    display: block;
    width: 100%;
    padding: 12px;
    margin: 8px 0;
    border: none;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
}
button:hover {
    background: gold;
    color: black;
}
#premio {
    font-size: 20px;
    color: gold;
    margin-bottom: 15px;
}
.ajudas button {
    background: #003566;
}
</style>
</head>
<body>

<h1>🎤 Show do Milhão Bíblico</h1>

<div class="container">
    <div id="premio"></div>
    <h2 id="pergunta"></h2>
    <div id="opcoes"></div>

    <div class="ajudas">
        <button onclick="pular()">📞 Pular</button>
        <button onclick="universitarios()">🧠 Universitários</button>
        <button onclick="cartas()">🃏 Cartas</button>
    </div>
</div>

<script>

const premios = [
"R$ 1.000","R$ 2.000","R$ 3.000","R$ 5.000","R$ 10.000",
"R$ 20.000","R$ 30.000","R$ 40.000","R$ 50.000","R$ 75.000",
"R$ 100.000","R$ 150.000","R$ 200.000","R$ 300.000","R$ 400.000",
"R$ 500.000","R$ 600.000","R$ 700.000","R$ 800.000","R$ 900.000",
"R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000"
];

let perguntasOriginais = [...]; // MANTENHA SUAS 26 PERGUNTAS AQUI

let perguntas = [];
let indice = 0;
let ajudaPular = false;
let ajudaUniversitarios = false;
let ajudaCartas = false;

function embaralhar(array){
    return array.sort(()=>Math.random()-0.5);
}

function iniciarJogo(){
    perguntas = embaralhar([...perguntasOriginais]);
    indice = 0;
    ajudaPular = false;
    ajudaUniversitarios = false;
    ajudaCartas = false;
    carregarPergunta();
}

function carregarPergunta(){
    if(indice >= 26){
        document.querySelector(".container").innerHTML =
        "<h2>🎉 PARABÉNS!</h2><p>Você conquistou R$ 1.000.000!</p><button onclick='iniciarJogo()'>Jogar Novamente</button>";
        return;
    }

    document.getElementById("premio").innerText = "Valendo: " + premios[indice];
    document.getElementById("pergunta").innerText = perguntas[indice].pergunta;

    const opcoesDiv = document.getElementById("opcoes");
    opcoesDiv.innerHTML = "";

    perguntas[indice].opcoes.forEach((opcao,i)=>{
        const btn = document.createElement("button");
        btn.innerText = opcao;
        btn.id = "opcao"+i;
        btn.onclick = ()=> verificar(i);
        opcoesDiv.appendChild(btn);
    });
}

function verificar(resposta){
    if(resposta === perguntas[indice].correta){
        indice++;
        carregarPergunta();
    }else{
        document.querySelector(".container").innerHTML =
        "<h2>💥 Resposta errada!</h2><p>Nova tentativa iniciando...</p>";
        setTimeout(iniciarJogo,2000);
    }
}

function pular(){
    if(!ajudaPular){
        ajudaPular = true;
        indice++;
        carregarPergunta();
    } else {
        alert("Você já usou o Pular!");
    }
}

function universitarios(){
    if(!ajudaUniversitarios){
        ajudaUniversitarios = true;
        alert("A maioria acredita que é: " + perguntas[indice].opcoes[perguntas[indice].correta]);
    } else {
        alert("Você já usou essa ajuda!");
    }
}

function cartas(){
    if(!ajudaCartas){
        ajudaCartas = true;

        let erradas = perguntas[indice].opcoes
        .map((_,i)=>i)
        .filter(i=>i !== perguntas[indice].correta);

        erradas = embaralhar(erradas).slice(0,2);

        erradas.forEach(i=>{
            document.getElementById("opcao"+i).style.display="none";
        });

    } else {
        alert("Você já usou as Cartas!");
    }
}

iniciarJogo();

</script>
</body>
</html>
