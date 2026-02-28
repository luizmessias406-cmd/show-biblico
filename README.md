
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show do Milhão Bíblico</title>
    <style>
        body { font-family: sans-serif; background: #000050; color: white; text-align: center; padding: 20px; }
        .painel { border: 2px solid gold; padding: 20px; border-radius: 15px; background: rgba(0,0,0,0.5); }
        .pergunta { font-size: 1.2rem; margin-bottom: 20px; min-height: 60px; }
        .btn { display: block; width: 100%; padding: 10px; margin: 10px 0; border: 1px solid white; border-radius: 20px; background: #000080; color: white; font-weight: bold; }
        .btn:active { background: gold; color: black; }
        .btn-ajuda { background: #d9534f; width: 30%; display: inline-block; font-size: 0.8rem; margin: 2px; }
        .info { color: gold; font-weight: bold; margin-bottom: 10px; }
    </style>
</head>
<body>

    <div class="painel">
        <div class="info" id="status">Prêmio: R$ 1.000</div>
        <div class="pergunta" id="pergunta">Carregando pergunta...</div>
        
        <div id="opcoes"></div>

        <hr>
        <p>Ajudas:</p>
        <button class="btn btn-ajuda" onclick="pular()" id="btn-pular">Pular (3)</button>
        <button class="btn btn-ajuda" onclick="ajudaCartas()" id="btn-cartas">Cartas</button>
        <button class="btn btn-ajuda" onclick="ajudaUniv()" id="btn-univ">Univ.</button>
    </div>

    <script>
        const perguntas = [
            { q: "Quem foi o primeiro homem?", o: ["Noé", "Abraão", "Adão", "Davi"], c: 2 },
            { q: "Qual o nome da esposa de Abraão?", o: ["Sara", "Rebeca", "Eva", "Dalila"], c: 0 },
            { q: "Quantos mandamentos Deus deu a Moisés?", o: ["7", "12", "10", "3"], c: 2 },
            { q: "Quem venceu o gigante Golias?", o: ["Saul", "Davi", "Salomão", "Sansão"], c: 1 },
            { q: "Jesus nasceu em qual cidade?", o: ["Jerusalém", "Nazaré", "Belém", "Egito"], c: 2 },
            { q: "Quem foi traído por 30 moedas?", o: ["Jesus", "Pedro", "Judas", "João"], c: 2 }
        ];

        let nivel = 0;
        let pulos = 3;
        const valores = [1000, 2000, 3000, 4000, 5000, 10000, 20000, 40000, 80000, 160000, 320000, 500000, 1000000];

        function carregarPergunta() {
            if (nivel >= valores.length) {
                alert("PARABÉNS! VOCÊ GANHOU 1 MILHÃO!");
                location.reload();
                return;
            }
            document.getElementById("status").innerText = "Prêmio: R$ " + valores[nivel].toLocaleString('pt-BR');
            const p = perguntas[nivel % perguntas.length];
            document.getElementById("pergunta").innerText = p.q;
            
            const divOpc = document.getElementById("opcoes");
            divOpc.innerHTML = "";
            p.o.forEach((txt, i) => {
                divOpc.innerHTML += `<button class="btn" onclick="verificar(${i})">${txt}</button>`;
            });
        }

        function verificar(escolha) {
            const correta = perguntas[nivel % perguntas.length].c;
            if (escolha === correta) {
                alert("Certa Resposta!");
                nivel++;
                carregarPergunta();
            } else {
                alert("Você errou! Fim de jogo.");
                location.reload();
            }
        }

        function pular() {
            if (pulos > 0) {
                pulos--;
                document.getElementById("btn-pular").innerText = "Pular (" + pulos + ")";
                carregarPergunta();
            } else { alert("Sem pulos!"); }
        }

        function ajudaCartas() {
            alert("Você tirou a carta Rei: Nenhuma eliminada!");
            document.getElementById("btn-cartas").style.display = "none";
        }

        function ajudaUniv() {
            const correta = perguntas[nivel % perguntas.length].o[perguntas[nivel % perguntas.length].c];
            alert("Os universitários dizem que a resposta é: " + correta);
            document.getElementById("btn-univ").style.display = "none";
        }

        carregarPergunta();
    </script>
</body>
</html>
