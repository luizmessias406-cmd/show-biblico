
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Show do Milhão Bíblico Profissional</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #000030; color: white; text-align: center; padding: 10px; margin: 0; }
        .painel { border: 3px solid #FFD700; padding: 15px; border-radius: 20px; background: linear-gradient(180deg, #000050 0%, #000020 100%); max-width: 400px; margin: 10px auto; box-shadow: 0 0 20px rgba(255, 215, 0, 0.3); }
        .info { color: #FFD700; font-size: 1.4rem; font-weight: bold; margin-bottom: 5px; }
        .progresso { font-size: 0.9rem; color: #aaa; margin-bottom: 15px; }
        .pergunta { font-size: 1.1rem; margin-bottom: 20px; min-height: 80px; display: flex; align-items: center; justify-content: center; font-weight: bold; padding: 0 10px; }
        .btn { display: block; width: 100%; padding: 12px; margin: 8px 0; border: 2px solid #fff; border-radius: 25px; background: #000080; color: white; font-weight: bold; font-size: 1rem; cursor: pointer; }
        .btn:active { background: #FFD700; color: #000; }
        .ajudas-container { display: flex; justify-content: space-around; margin-top: 15px; border-top: 1px solid #444; padding-top: 15px; }
        .btn-ajuda { background: #d9534f; border: none; padding: 10px; border-radius: 10px; color: white; font-size: 0.8rem; font-weight: bold; width: 30%; }
        .btn-ajuda:disabled { background: #333; color: #777; }
    </style>
</head>
<body>

    <div class="painel">
        <div class="info" id="status">R$ 1.000</div>
        <div class="progresso" id="pergunta-num">Pergunta 1 de 26</div>
        <div id="set-info" style="font-size: 10px; color: #555;"></div>
        <div class="pergunta" id="pergunta">Carregando...</div>
        
        <div id="opcoes"></div>

        <div class="ajudas-container">
            <button class="btn-ajuda" onclick="pular()" id="btn-pular">Pular (3)</button>
            <button class="btn-ajuda" onclick="ajudaCartas()" id="btn-cartas">Cartas</button>
            <button class="btn-ajuda" onclick="ajudaUniv()" id="btn-univ">Univ.</button>
        </div>
    </div>

    <script>
        const setA = [
            // Nível 1-8
            { q: "Quem construiu a arca?", o: ["Moisés", "Noé", "Davi", "Abraão"], c: 1 },
            { q: "Quantos discípulos Jesus escolheu?", o: ["10", "12", "7", "3"], c: 1 },
            { q: "Quem matou o gigante Golias?", o: ["Saul", "Davi", "Sansão", "Gideão"], c: 1 },
            { q: "Qual foi o primeiro livro da Bíblia?", o: ["Êxodo", "Gênesis", "Levítico", "Mateus"], c: 1 },
            { q: "Em qual cidade Jesus nasceu?", o: ["Nazaré", "Belém", "Jerusalém", "Jericó"], c: 1 },
            { q: "Quem foi jogado na cova dos leões?", o: ["José", "Daniel", "Paulo", "Pedro"], c: 1 },
            { q: "Quem traiu Jesus?", o: ["Pedro", "Judas Iscariotes", "João", "Tomé"], c: 1 },
            { q: "Qual mar se abriu para o povo de Israel passar?", o: ["Mar Morto", "Mar Vermelho", "Mar da Galileia", "Mar Mediterrâneo"], c: 1 },
            // Nível 9-16
            { q: "Qual era o nome original de Abraão?", o: ["Abimeleque", "Abrão", "Israel", "Isaac"], c: 1 },
            { q: "Quem foi o irmão de Moisés que se tornou o primeiro sumo sacerdote?", o: ["Arão", "Miriã", "Josué", "Calebe"], c: 0 },
            { q: "Qual juiz de Israel teve sua força ligada ao cabelo?", o: ["Gideão", "Sansão", "Baraque", "Jefté"], c: 1 },
            { q: "Quem sucedeu Moisés na liderança de Israel?", o: ["Arão", "Josué", "Calebe", "Eleazar"], c: 1 },
            { q: "Qual rei pediu sabedoria a Deus em vez de riquezas?", o: ["Davi", "Salomão", "Saul", "Josias"], c: 1 },
            { q: "Qual discípulo andou sobre as águas com Jesus?", o: ["João", "Pedro", "André", "Tiago"], c: 1 },
            { q: "Em qual livro encontramos a história de Ester?", o: ["Rute", "Ester", "Judite", "Esdras"], c: 1 },
            { q: "Quem escreveu o livro de Apocalipse?", o: ["Paulo", "João", "Pedro", "Lucas"], c: 1 },
            // Nível 17-22
            { q: "Qual profeta se casou com Gômer como sinal profético?", o: ["Amós", "Oseias", "Joel", "Miqueias"], c: 1 },
            { q: "Qual era o nome do rei da Babilônia que destruiu Jerusalém?", o: ["Ciro", "Nabucodonosor", "Dário", "Artaxerxes"], c: 1 },
            { q: "Quantos capítulos tem o livro de Salmos?", o: ["120", "150", "100", "200"], c: 1 },
            { q: "Qual discípulo também era chamado de Dídimo?", o: ["Filipe", "Tomé", "Bartolomeu", "Mateus"], c: 1 },
            { q: "Onde Paulo estava quando teve a visão do homem macedônio?", o: ["Atenas", "Trôade", "Éfeso", "Corinto"], c: 1 },
            { q: "Qual sacerdote ajudou Joás a se tornar rei criança?", o: ["Elias", "Joiada", "Zacarias", "Abiatar"], c: 1 },
            // Nível 23-26
            { q: "Qual profeta anunciou a destruição de Nínive antes de Jonas?", o: ["Naum", "Obadias", "Sofonias", "Amós"], c: 0 },
            { q: "Quem era o pai de João Batista?", o: ["José", "Zacarias", "Joaquim", "Levi"], c: 1 },
            { q: "Qual igreja do Apocalipse recebeu apenas elogios?", o: ["Éfeso", "Filadélfia", "Laodiceia", "Sardes"], c: 1 },
            { q: "Qual o nome do campo comprado com as 30 moedas de Judas?", o: ["Gólgota", "Acéldama", "Getsêmani", "Siloé"], c: 1 }
        ];

        const setB = [
            // Nível 1-8
            { q: "Quem foi o primeiro rei de Israel?", o: ["Davi", "Saul", "Salomão", "Samuel"], c: 1 },
            { q: "Quem construiu o templo em Jerusalém?", o: ["Davi", "Salomão", "Ezequias", "Josias"], c: 1 },
            { q: "Qual é o último livro da Bíblia?", o: ["Malaquias", "Apocalipse", "Judas", "João"], c: 1 },
            { q: "Quem foi o homem mais forte do Antigo Testamento?", o: ["Davi", "Sansão", "Golias", "Saul"], c: 1 },
            { q: "Quem interpretou os sonhos do faraó no Egito?", o: ["Moisés", "José", "Daniel", "Jacó"], c: 1 },
            { q: "Qual era o nome da esposa de Abraão?", o: ["Rebeca", "Sara", "Raquel", "Lia"], c: 1 },
            { q: "Quem foi escolhido para substituir Judas Iscariotes?", o: ["Paulo", "Matias", "Barnabé", "Estêvão"], c: 1 },
            { q: "Em qual monte Moisés recebeu os Dez Mandamentos?", o: ["Monte das Oliveiras", "Monte Sinai", "Monte Carmelo", "Monte Nebo"], c: 1 },
            // Nível 9-16
            { q: "Qual profeta confrontou Davi após o pecado com Bate-Seba?", o: ["Samuel", "Natã", "Elias", "Eliseu"], c: 1 },
            { q: "Qual era o nome do filho de Abraão com Agar?", o: ["Isaque", "Ismael", "Jacó", "Esaú"], c: 1 },
            { q: "Quem foi o pai de Salomão?", o: ["Saul", "Davi", "Samuel", "Jesse"], c: 1 },
            { q: "Qual discípulo era irmão de João?", o: ["Pedro", "Tiago", "André", "Filipe"], c: 1 },
            { q: "Qual livro vem logo depois de Atos?", o: ["Gálatas", "Romanos", "Coríntios", "Hebreus"], c: 1 },
            { q: "Qual rainha visitou Salomão por sua sabedoria?", o: ["Rainha de Sabá", "Ester", "Jezabel", "Vasti"], c: 0 },
            { q: "Quem jogou os jovens na fornalha ardente?", o: ["Dário", "Nabucodonosor", "Belsazar", "Herodes"], c: 1 },
            { q: "Qual apóstolo era natural de Tarso?", o: ["Pedro", "Paulo", "João", "André"], c: 1 },
            // Nível 17-22
            { q: "Qual era o nome hebraico de Daniel?", o: ["Azarias", "Beltessazar", "Misael", "Ananias"], c: 1 },
            { q: "Qual rei tentou matar Jesus quando criança?", o: ["Pilatos", "Herodes", "Agripa", "César"], c: 1 },
            { q: "Quantos livros tem o Novo Testamento?", o: ["39", "27", "66", "12"], c: 1 },
            { q: "Quem foi o avô do rei Josias?", o: ["Ezequias", "Manassés", "Amom", "Acaz"], c: 1 },
            { q: "Qual profeta teve a visão do vale de ossos secos?", o: ["Jeremias", "Ezequiel", "Isaías", "Daniel"], c: 1 },
            { q: "Qual mágico tentou comprar o dom do Espírito Santo?", o: ["Elimas", "Simão", "Barjesus", "Alexandre"], c: 1 },
            // Nível 23-26
            { q: "Qual era o nome do pai de Abraão?", o: ["Naor", "Terá", "Arã", "Ló"], c: 1 },
            { q: "Qual juiz de Israel fez um voto envolvendo sua filha?", o: ["Gideão", "Jefté", "Sansão", "Samuel"], c: 1 },
            { q: "Em qual livro não aparece a palavra 'Deus'?", o: ["Rute", "Ester", "Cantares", "Eclesiastes"], c: 1 },
            { q: "Qual era o nome do sumo sacerdote no julgamento de Jesus?", o: ["Anás", "Caifás", "Gamaliel", "Nicodemos"], c: 1 }
        ];

        const valores = [1000, 2000, 3000, 4000, 5000, 6000, 7000, 8000, 9000, 10000, 20000, 30000, 40000, 50000, 60000, 80000, 100000, 150000, 200000, 300000, 400000, 500000, 600000, 800000, 900000, 1000000];

        let perguntasAtuais = [];
        let etapa = 0;
        let pulos = 3;
        let pAtual = null;

        function iniciarJogo() {
            // Escolhe aleatoriamente entre Set A e Set B
            const sortearSet = Math.random() < 0.5;
            perguntasAtuais = sortearSet ? setA : setB;
            etapa = 0;
            pulos = 3;
            document.getElementById("btn-pular").innerText = "Pular (3)";
            document.getElementById("btn-cartas").disabled = false;
            document.getElementById("btn-univ").disabled = false;
            carregarPergunta();
        }

        function carregarPergunta() {
            if (etapa >= valores.length) {
                alert("PARABÉNS! VOCÊ GANHOU 1 MILHÃO!");
                iniciarJogo();
                return;
            }
            
            pAtual = perguntasAtuais[etapa];
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
                alert("ERROU! A resposta era: " + pAtual.o[pAtual.c] + "\nO jogo vai recomeçar com novas perguntas!");
                iniciarJogo();
            }
        }

        function pular() {
            if (pulos > 0) {
                pulos--;
                document.getElementById("btn-pular").innerText = "Pular (" + pulos + ")";
                etapa++; // No show do milhão, pular consome a pergunta e vai para a próxima de mesmo valor
                carregarPergunta();
            } else { alert("Sem pulos!"); }
        }

        function ajudaCartas() {
            let eliminadas = Math.floor(Math.random() * 4); // Sorteia 0 a 3
            alert("Cartas: " + (eliminadas == 0 ? "Rei (Nenhuma eliminada)" : "Eliminando " + eliminadas + " errada(s)!"));
            let removidas = 0;
            for(let i=0; i<4; i++) {
                if(i !== pAtual.c && removidas < eliminadas) {
                    document.getElementById("opt-"+i).style.visibility = "hidden";
                    removidas++;
                }
            }
            document.getElementById("btn-cartas").disabled = true;
        }

        function ajudaUniv() {
            alert("Os Universitários sugerem: " + pAtual.o[pAtual.c]);
            document.getElementById("btn-univ").disabled = true;
        }

        iniciarJogo();
    </script>
</body>
</html>


