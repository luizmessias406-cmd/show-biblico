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
    max-width: 700px;
    margin: auto;
    background: #012a4a;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 0 20px gold;
}
h1 {
    color: gold;
}
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
    margin: 10px 0;
}
#timer {
    font-size: 18px;
    color: #ffcc00;
}
.ajudas {
    margin-top: 10px;
}
</style>
</head>
<body>

<h1>🎤 Show do Milhão Bíblico</h1>

<div class="container">
    <div id="premio">Valendo: R$ 1.000</div>
    <div id="timer">Tempo: 30</div>
    <h2 id="pergunta"></h2>
    <div id="opcoes"></div>

    <div class="ajudas">
        <button onclick="pular()">📞 Pular Pergunta</button>
        <button onclick="universitarios()">🧠 Ajuda dos Universitários</button>
    </div>
</div>

<script>
const premios = [
    "R$ 1.000",
    "R$ 5.000",
    "R$ 10.000",
    "R$ 50.000",
    "R$ 100.000",
    "R$ 1.000.000"
];

const perguntas = [
{
pergunta: "Quem construiu a arca?",
opcoes: ["Moisés", "Abraão", "Noé", "Davi"],
correta: 2
},
{
pergunta: "Quem foi lançado na cova dos leões?",
opcoes: ["José", "Daniel", "Paulo", "Elias"],
correta: 1
},
{
pergunta: "Quantos discípulos Jesus escolheu?",
opcoes: ["7", "10", "12", "15"],
correta: 2
},
{
pergunta: "Quem enfrentou Golias?",
opcoes: ["Saul", "Davi", "Samuel", "Josué"],
correta: 1
},
{
pergunta: "Quem liderou o povo na saída do Egito?",
opcoes: ["Abraão", "Moisés", "Josué", "Noé"],
correta: 1
},
{
pergunta: "Quem foi engolido por um grande peixe?",
opcoes: ["Jonas", "Pedro", "Tiago", "Isaías"],
correta: 0
}
];

let indice = 0;
let tempo = 30;
let intervalo;
let ajudaUsada = false;
let puloUsado = false;

function iniciarTimer(){
tempo = 30;
document.getElementById("timer").innerText = "Tempo: " + tempo;
intervalo = setInterval(()=>{
tempo--;
document.getElementById("timer").innerText = "Tempo: " + tempo;
if(tempo === 0){
clearInterval(intervalo);
fimDeJogo();
}
},1000);
}

function carregarPergunta(){
if(indice >= perguntas.length){
fimDeJogo(true);
return;
}

document.getElementById("premio").innerText = "Valendo: " + premios[indice];
document.getElementById("pergunta").innerText = perguntas[indice].pergunta;
const opcoesDiv = document.getElementById("opcoes");
opcoesDiv.innerHTML = "";

perguntas[indice].opcoes.forEach((opcao,i)=>{
const btn = document.createElement("button");
btn.innerText = opcao;
btn.onclick = ()=> verificar(i);
opcoesDiv.appendChild(btn);
});

iniciarTimer();
}

function verificar(resposta){
clearInterval(intervalo);
if(resposta === perguntas[indice].correta){
indice++;
carregarPergunta();
}else{
fimDeJogo();
}
}

function fimDeJogo(vitoria=false){
document.querySelector(".container").innerHTML =
vitoria ?
"<h2>🎉 PARABÉNS!</h2><p>Você ganhou R$ 1.000.000!</p>" :
"<h2>💥 Você perdeu!</h2><p>Continue estudando a Palavra 📖</p>";
}

function pular(){
if(!puloUsado){
puloUsado = true;
indice++;
carregarPergunta();
}else{
alert("Você já usou o pulo!");
}
}

function universitarios(){
if(!ajudaUsada){
ajudaUsada = true;
alert("A maioria acha que é: " + perguntas[indice].opcoes[perguntas[indice].correta]);
}else{
alert("Você já usou essa ajuda!");
}
}

carregarPergunta();
</script>

</body>
</html>
