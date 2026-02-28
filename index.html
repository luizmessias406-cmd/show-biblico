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
</style>
</head>
<body>

<h1>🎤 Show do Milhão Bíblico</h1>

<div class="container">
    <div id="premio"></div>
    <h2 id="pergunta"></h2>
    <div id="opcoes"></div>
</div>

<script>

const premios = [
"R$ 1.000","R$ 2.000","R$ 3.000","R$ 5.000","R$ 10.000",
"R$ 20.000","R$ 30.000","R$ 40.000","R$ 50.000","R$ 75.000",
"R$ 100.000","R$ 150.000","R$ 200.000","R$ 300.000","R$ 400.000",
"R$ 500.000","R$ 600.000","R$ 700.000","R$ 800.000","R$ 900.000",
"R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000","R$ 1.000.000"
];

let perguntasOriginais = [
{pergunta:"Quem construiu a arca?", opcoes:["Moisés","Abraão","Noé","Davi"], correta:2},
{pergunta:"Quem foi lançado na cova dos leões?", opcoes:["José","Daniel","Paulo","Elias"], correta:1},
{pergunta:"Quantos discípulos Jesus escolheu?", opcoes:["7","10","12","15"], correta:2},
{pergunta:"Quem enfrentou Golias?", opcoes:["Saul","Davi","Samuel","Josué"], correta:1},
{pergunta:"Quem liderou o povo na saída do Egito?", opcoes:["Abraão","Moisés","Josué","Noé"], correta:1},
{pergunta:"Quem foi engolido por um grande peixe?", opcoes:["Jonas","Pedro","Tiago","Isaías"], correta:0},
{pergunta:"Quem negou Jesus três vezes?", opcoes:["Pedro","João","Tiago","Paulo"], correta:0},
{pergunta:"Quem escreveu muitos Salmos?", opcoes:["Davi","Moisés","Isaías","Elias"], correta:0},
{pergunta:"Qual o primeiro livro da Bíblia?", opcoes:["Êxodo","Gênesis","Levítico","Números"], correta:1},
{pergunta:"Quem traiu Jesus?", opcoes:["Pedro","Judas","Tomé","Mateus"], correta:1},
{pergunta:"Onde Jesus nasceu?", opcoes:["Jerusalém","Belém","Nazaré","Roma"], correta:1},
{pergunta:"Quem construiu o templo?", opcoes:["Davi","Salomão","Saul","Samuel"], correta:1},
{pergunta:"Quem era o pai de Isaque?", opcoes:["Abraão","Jacó","José","Noé"], correta:0},
{pergunta:"Quem abriu o Mar Vermelho?", opcoes:["Moisés","Josué","Elias","Abraão"], correta:0},
{pergunta:"Quem foi o homem mais forte da Bíblia?", opcoes:["Sansão","Davi","Saul","Josué"], correta:0},
{pergunta:"Quem interpretou sonhos no Egito?", opcoes:["José","Daniel","Elias","Paulo"], correta:0},
{pergunta:"Qual apóstolo duvidou da ressurreição?", opcoes:["Tomé","Pedro","Tiago","André"], correta:0},
{pergunta:"Quem foi a mãe de Jesus?", opcoes:["Maria","Marta","Rute","Ana"], correta:0},
{pergunta:"Quem escreveu Apocalipse?", opcoes:["Paulo","João","Pedro","Lucas"], correta:1},
{pergunta:"Quem subiu ao céu em um redemoinho?", opcoes:["Elias","Eliseu","Isaías","Jeremias"], correta:0},
{pergunta:"Quem foi o primeiro rei de Israel?", opcoes:["Davi","Saul","Salomão","Samuel"], correta:1},
{pergunta:"Qual discípulo era cobrador de impostos?", opcoes:["Mateus","Pedro","João","Tiago"], correta:0},
{pergunta:"Quem era o gigante derrotado por Davi?", opcoes:["Golias","Saul","Faraó","Absalão"], correta:0},
{pergunta:"Qual livro fala sobre a criação?", opcoes:["Êxodo","Gênesis","Salmos","Provérbios"], correta:1},
{pergunta:"Quem foi vendido pelos irmãos?", opcoes:["José","Davi","Isaac","Noé"], correta:0},
{pergunta:"Quem recebeu os Dez Mandamentos?", opcoes:["Moisés","Abraão","Elias","Samuel"], correta:0}
];

let perguntas = [];
let indice = 0;

function embaralhar(array){
    return array.sort(()=>Math.random()-0.5);
}

function iniciarJogo(){
    perguntas = embaralhar([...perguntasOriginais]);
    indice = 0;
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

iniciarJogo();

</script>
</body>
</html>
