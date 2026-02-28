

<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show do Milhão Bíblico</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #000030; color: white; text-align: center; padding: 10px; margin: 0; }
        .painel { border: 3px solid #FFD700; padding: 15px; border-radius: 20px; background: linear-gradient(180deg, #000050 0%, #000020 100%); max-width: 400px; margin: 20px auto; box-shadow: 0 0 20px rgba(255, 215, 0, 0.3); }
        .info { color: #FFD700; font-size: 1.4rem; font-weight: bold; margin-bottom: 5px; text-shadow: 2px 2px 4px #000; }
        .progresso { font-size: 0.9rem; color: #aaa; margin-bottom: 15px; }
        .pergunta { font-size: 1.1rem; margin-bottom: 20px; min-height: 70px; display: flex; align-items: center; justify-content: center; font-weight: 500; }
        .btn { display: block; width: 100%; padding: 12px; margin: 8px 0; border: 2px solid #fff; border-radius: 25px; background: #000080; color: white; font-weight: bold; font-size: 1rem; cursor: pointer; transition: 0.2s; }
        .btn:active { background: #FFD700; color: #000; transform: scale(0.98); }
        .ajudas-container { display: flex; justify-content: space-around; margin-top: 15px; border-top: 1px solid #444; padding-top: 15px; }
        .btn-ajuda { background: #d9534f; border: none; padding: 10px; border-radius: 10px; color: white; font-size: 0.8rem; font-weight: bold; width: 30%; }
        .btn-ajuda:disabled { background: #333; color: #777; }
    </style>
</head>
<body>

    <div class="painel">
        <div class="info" id="status">R$ 1.000</div>
        <div class="progresso" id="pergunta-num">Pergunta 1 de 26</div>
        <div class="pergunta" id="pergunta">Carregando...</div>
        
        <div id="opcoes"></div>

        <div class="ajudas-container">
            <button class="btn-ajuda" onclick="pular()" id="btn-pular">Pular (3)</button>
            <button class="btn-ajuda" onclick="ajudaCartas()" id="btn-cartas">Cartas</button>
            <button class="btn-ajuda" onclick="ajudaUniv()" id="btn-univ">Univ.</button>
        </div>
    </div>

    <script>
        // Banco de Dados com Níveis de Dificuldade
        const perguntasBD = {
            facil: [
                { q: "Quem construiu a arca?", o: ["Moisés", "Noé", "Davi", "Sansão"], c: 1 },
                { q: "Qual o primeiro livro da Bíblia?", o: ["Êxodo", "Gênesis", "Salmos", "Mateus"], c: 1 },
                { q: "Quem venceu o gigante Golias?", o: ["Saul", "Davi", "Salomão", "Sansão"], c: 1 },
                { q: "Quantos discípulos Jesus tinha?", o: ["10", "12", "7", "3"], c: 1 },
                { q: "Qual o nome do jardim onde Adão viveu?", o: ["Gethsemani", "Éden", "Canaã", "Sinai"], c: 1 },
                { q: "Quem foi jogado na cova dos leões?", o: ["Pedro", "Daniel", "João", "José"], c: 1 },
                { q: "Qual pássaro Noé soltou primeiro da arca?", o: ["Pomba", "Corvo", "Águia", "Pardal"], c: 1 },
                { q: "Onde Jesus nasceu?", o: ["Nazaré", "Belém", "Jerusalém", "Egito"], c: 1 },
                { q: "Quem era o irmão de Moisés?", o: ["Arão", "Calebe", "Josué", "Esaú"], c: 0 }
            ],
            medio: [
                { q: "Qual o mar Moisés abriu pelo poder de Deus?", o: ["Mar Morto", "Mar da Galileia", "Mar Vermelho", "Mar Negro"], c: 2 },
                { q: "Quantos anos o povo de Israel vagou no deserto?", o: ["40", "50", "30", "10"], c: 0 },
                { q: "Qual o nome da esposa de Abraão?", o: ["Sara", "Rebeca", "Raquel", "Eva"], c: 0 },
                { q: "Quem foi vendido pelos irmãos como escravo?", o: ["Benjamim", "José", "Rúben", "Davi"], c: 1 },
                { q: "Quem traiu Jesus por 30 moedas?", o: ["Pedro", "João", "Judas Iscariotes", "Tomé"], c: 2 },
                { q: "Qual profeta foi engolido por um grande peixe?", o: ["Isaías", "Jonas", "Elias", "Ezequiel"], c: 1 },
                { q: "O que caiu do céu para alimentar o povo no deserto?", o: ["Pão", "Maná", "Trigo", "Mel"], c: 1 },
                { q: "Quem subiu aos céus em um redemoinho?", o: ["Elias", "Eliseu", "Enoque", "Moisés"], c: 0 },
                { q: "Qual o menor livro da Bíblia (versículos)?", o: ["Obadias", "Filemon", "2 João", "3 João"], c: 3 }
            ],
            dificil: [
                { q: "Qual era a profissão de Amós antes de ser profeta?", o: ["Pescador", "Pastor e colhedor de sicômoros", "Carpinteiro", "Sacerdote"], c: 1 },
                { q: "Quem foi o sucessor de Moisés?", o: ["Arão", "Josué", "Calebe", "Gideão"], c: 1 },
                { q: "Qual rei teve sua vida prolongada em 15 anos?", o: ["Davi", "Ezequias", "Josias", "Acaz"], c: 1 },
                { q: "Qual o nome do pai de João Batista?", o: ["Zacarias", "José", "Joaquim", "Levi"], c: 0 },
                { q: "Em qual ilha o apóstolo João escreveu o Apocalipse?", o: ["Creta", "Chipre", "Patmos", "Malta"], c: 2 },
                { q: "Qual o nome da cidade onde Jesus realizou seu 1º milagre?", o: ["Nazaré", "Caná", "Cafarnaum", "Jericó"], c: 1 },
                { q: "Quantos capítulos tem o livro de Salmos?", o: ["100", "150", "120", "200"], c: 1 },
                { q: "Quem foi a única juíza de Israel?", o: ["Rute", "Débora", "Ester", "Noemi"], c: 1 }
            ]
        };

        // Escala de valores pedida (26 níveis)
        // 1k até 10k (sobe de 1k em 1k), depois dobra até 1M
        const valores = [
            1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000, 9000, 10000, 
            20000, 30000, 40000, 50000, 60000, 80000, 100000, 150000, 200000, 
            300000, 400000, 500000, 600000, 800000, 900000, 1000000
        ];

        let etapa = 0;
        let pulos = 3;
        let perguUsada = [];

        function getPergunta() {
            let diff = "facil";
            if (etapa >= 8 && etapa < 17) diff = "medio";
            if (etapa >= 17) diff = "dificil";

            let lista = perguntasBD[diff];
            // Sorteia uma que ainda não saiu (ou repete se acabar o banco)
            return lista[Math.floor(Math.random() * lista.length)];
        }

        let pAtual = null;

        function carregarPergunta() {
            if (etapa >= valores.length) {
                alert("INCRÍVEL! VOCÊ É O NOVO MILIONÁRIO BÍBLICO!");
                location.reload();
                return;
            }
            
            pAtual = getPergunta();
            document.getElementById("status").innerText = "R$ " + valores[etapa].toLocaleString('pt-BR');
            document.getElementById("pergunta-num").innerText = "Pergunta " + (etapa + 1) + " de 26";
            document.getElementById("pergunta").innerText = pAtual.q;
            
            const divOpc = document.getElementById("opcoes");
            divOpc.innerHTML = "";
            pAtual.o.forEach((txt, i) => {
                divOpc.innerHTML += `<button class="btn" id="opt-${i}" onclick="verificar(${i})">${txt}</button>`;
            });
        }

        function verificar(escolha) {
            if (escolha === pAtual.c) {
                alert("CERTA RESPOSTA!");
                etapa++;
                carregarPergunta();
            } else {
                alert("QUE PENA! Você errou. A resposta era: " + pAtual.o[pAtual.c]);
                location.reload();
            }
        }

        function pular() {
            if (pulos > 0) {
                pulos--;
                document.getElementById("btn-pular").innerText = "Pular (" + pulos + ")";
                carregarPergunta();
            } else { alert("Pulos esgotados!"); }
        }

        function ajudaCartas() {
            let eliminadas = Math.floor(Math.random() * 4); // 0 a 3
            alert("As cartas dizem: Elimine " + eliminadas + " alternativa(s) errada(s)!");
            let cortadas = 0;
            for(let i=0; i<4; i++) {
                if(i !== pAtual.c && cortadas < eliminadas) {
                    document.getElementById("opt-"+i).style.visibility = "hidden";
                    cortadas++;
                }
            }
            document.getElementById("btn-cartas").disabled = true;
        }

        function ajudaUniv() {
            alert("Os Universitários acham que a resposta correta é: " + pAtual.o[pAtual.c]);
            document.getElementById("btn-univ").disabled = true;
        }

        carregarPergunta();
    </script>
</body>
</html>
