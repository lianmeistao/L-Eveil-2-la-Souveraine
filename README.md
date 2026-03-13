<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Souffle TAO — L'Éveil de la Souveraine</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .fade-in { animation: fadeIn 0.6s cubic-bezier(0.4, 0, 0.2, 1) both; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }
        .serif { font-family: ui-serif, Georgia, Cambria, "Times New Roman", Times, serif; }
        .option-btn { transition: all 0.3s ease; cursor: pointer; }
        .option-btn:hover { transform: translateX(8px); background-color: #f5f5f4; border-color: #d6d3d1; }
        .prestige-box { background: linear-gradient(145deg, #292524, #1c1917); }
    </style>
</head>

<body class="min-h-screen bg-stone-100 flex items-center justify-center font-sans text-stone-800">

    <div id="quiz-container" class="max-w-2xl w-full bg-white rounded-[2.5rem] shadow-2xl overflow-hidden p-8 md:p-14 m-4 relative border border-stone-200">
        
        <!-- Header -->
        <div id="quiz-header" class="text-center mb-12">
            <span class="text-xs uppercase tracking-[0.3em] text-stone-400 mb-4 block">Chroniques Souffle TAO</span>
            <h1 class="text-3xl md:text-4xl text-stone-800 serif italic leading-tight">Quel est votre élément dominant ?</h1>
            <div class="w-full bg-stone-100 h-[2px] mt-10 rounded-full overflow-hidden">
                <div id="progress" class="bg-stone-400 h-full transition-all duration-700" style="width: 0%"></div>
            </div>
            <p id="progress-text" class="text-[10px] uppercase tracking-widest text-stone-400 mt-4 italic">Exploration énergétique en cours...</p>
        </div>

        <!-- Question Area -->
        <div id="question-box" class="fade-in">
            <h3 id="question-text" class="text-xl md:text-2xl mb-10 leading-relaxed text-stone-700 serif"></h3>
            <div id="options-container" class="space-y-4"></div>
        </div>

        <!-- Result Area (Modifié pour le teasing) -->
        <div id="result-box" class="hidden fade-in text-center">
            <span class="text-xs uppercase tracking-[0.3em] text-stone-400 mb-4 block">Analyse terminée</span>
            <div id="element-icon" class="text-6xl mb-4 drop-shadow-sm"></div>
            <h2 class="text-2xl md:text-3xl mb-2 text-stone-600 serif">Votre synergie énergétique est :</h2>
            <h2 id="result-title" class="text-4xl md:text-5xl mb-10 text-stone-800 serif italic font-bold"></h2>
            
            <!-- Message de teasing (Généré en JS) -->
            <div id="result-content" class="text-left leading-relaxed mb-12 p-8 bg-stone-50 rounded-[2rem] border border-stone-100 text-lg shadow-inner">
            </div>
            
            <!-- OFFRE MANUSCRIT (Capture d'email) -->
            <div class="border-t border-stone-100 pt-10 mt-10 text-center">
                <h3 class="serif text-2xl mb-6 text-stone-800">Décodez votre synergie secrète</h3>
                
                <div class="prestige-box text-stone-100 p-8 md:p-10 rounded-[2.5rem] mb-8 text-left shadow-2xl relative overflow-hidden">
                    <h4 class="serif italic text-2xl mb-4 text-white">Le Manuscrit : « Guide de Renaissance TAO »</h4>
                    <p class="text-sm text-stone-300 mb-8 leading-relaxed">
                        Indiquez votre adresse e-mail sur la page suivante pour recevoir immédiatement votre guide personnalisé de <strong>14 pages</strong> (PDF). 
                    </p>
                    
                    <ul class="text-[11px] space-y-4 mb-10 uppercase tracking-[0.15em] font-light opacity-90 border-l border-stone-600 pl-6">
                        <li>✦ La signification profonde de votre synergie</li>
                        <li>✦ Vos zones d'ombres énergétiques révélées</li>
                        <li>✦ Rituels de Renaissance sur-mesure</li>
                        <li>✦ Pratiques TAO et acupression ciblées</li>
                    </ul>

                    <!-- BOUTON D'ACTION : Redirige vers la page Substack pour l'email -->
                    <a href="https://souffletao.substack.com/welcome" 
                       target="_blank" 
                       class="block w-full bg-stone-100 text-stone-900 text-center py-6 rounded-2xl hover:bg-white transition-all shadow-xl uppercase tracking-[0.2em] text-sm font-bold no-underline">
                       Recevoir mon guide par e-mail
                    </a>
                </div>

                <!-- RÉASSURANCE SÉCURITÉ -->
                <div class="max-w-md mx-auto space-y-4">
                    <p class="text-xs text-stone-600 font-medium leading-relaxed">
                        100% gratuit. Votre adresse e-mail est en sécurité.
                    </p>
                    <p class="text-[11px] text-stone-400 leading-relaxed italic opacity-80">
                        Souveraine, votre confiance est le socle de notre cercle. <br>
                        Désinscription possible d'un simple souffle.
                    </p>
                </div>
            </div>
        </div>
    </div>

<script>
    const quizData = [
        { q: "1. Si vous deviez vous fondre dans un paysage pour vous ressourcer, lequel choisiriez-vous ?", options: [{ t: "Une forêt dense où l'on sent l'odeur de la mousse", e: "A" },{ t: "Un champ baigné de soleil où l'on s'enivre de chaleur", e: "B" },{ t: "Une plaine fertile où l'on pétrit la terre douce", e: "C" },{ t: "Une montagne pure où l'on respire l'air cristallin", e: "D" },{ t: "Un rivage nocturne où l'on écoute le chant des abysses", e: "E" }] },
        { q: "2. Quel aspect de la lumière vous appelle le plus intensément aujourd'hui ?", options: [{ t: "Le vert tendre des bourgeons qui percent l'écorce", e: "A" },{ t: "L'éclat vibrant de midi qui fait danser l'air", e: "B" },{ t: "La douceur dorée du crépuscule qui enveloppe le monde", e: "C" },{ t: "La clarté blanche de l'aube qui purifie le regard", e: "D" },{ t: "Les reflets argentés de la lune qui scintillent sur l'eau", e: "E" }] },
        { q: "3. Dans le cycle des saisons, quel moment vous semble le plus sacré ?", options: [{ t: "Le jaillissement irrésistible du renouveau printanier", e: "A" },{ t: "L'apogée radieuse et brûlante de l'été", e: "B" },{ t: "La transition généreuse et nourricière de l'été indien", e: "C" },{ t: "Le dépouillement élégant et nécessaire de l'automne", e: "D" },{ t: "Le silence régénérateur et mystérieux de l'hiver", e: "E" }] },
        { q: "4. Quelle sensation tactile évoque pour vous la plénitude absolue ?", options: [{ t: "Toucher la sève qui monte sous une écorce", e: "A" },{ t: "Sentir la caresse d'une braise sur la peau", e: "B" },{ t: "Enfoncer vos doigts dans le velouté du terreau", e: "C" },{ t: "Effleurer la fraîcheur polie d'un cristal de roche", e: "D" },{ t: "Se laisser porter par la fluidité d'une onde fraîche", e: "E" }] },
        { q: "5. Quand votre emploi du temps sature, comment votre corps s'exprime-t-il ?", options: [{ t: "Des tensions qui se logent dans la nuque", e: "A" },{ t: "Des palpitations ou une agitation dans la poitrine", e: "B" },{ t: "Une sensation de lourdeur après chaque repas", e: "C" },{ t: "Une respiration qui devient courte et serrée", e: "D" },{ t: "Une fatigue sourde nichée dans le creux des reins", e: "E" }] },
        { q: "6. Face à un imprévu, quelle est votre réaction émotionnelle réflexe ?", options: [{ t: "Une pointe d'impatience qui pousse à l'action", e: "A" },{ t: "Un besoin soudain de partager et de se connecter", e: "B" },{ t: "Une tendance à ruminer et à trop réfléchir", e: "C" },{ t: "Un retrait immédiat pour retrouver votre espace", e: "D" },{ t: "Une sensation de peur diffuse, un besoin de refuge", e: "E" }] },
        { q: "7. De quoi avez-vous le plus besoin pour retrouver votre calme ?", options: [{ t: "De mettre votre corps en mouvement et de créer", e: "A" },{ t: "De rire aux éclats et d'échanger avec votre cercle", e: "B" },{ t: "De vous sentir entourée et tendrement nourrie", e: "C" },{ t: "De trier vos objets, d'épurer et de faire le vide", e: "D" },{ t: "De silence absolu et de plonger dans l'obscurité", e: "E" }] },
        { q: "8. Quel est le goût qui vous réconforte instinctivement ?", options: [{ t: "L'acidulé d'un fruit frais et tonique", e: "A" },{ t: "L'amertume élégante d'un carré de cacao noir", e: "B" },{ t: "La douceur rassurante d'un aliment onctueux", e: "C" },{ t: "Le piquant d'une épice fine qui réveille les sens", e: "D" },{ t: "Le salé minéral d'une eau de source profonde", e: "E" }] },
        { q: "9. Dans vos projets, quelle étape vous procure le plus de joie ?", options: [{ t: "L'élan initial, la naissance d'une idée neuve", e: "A" },{ t: "Le moment du partage et du rayonnement public", e: "B" },{ t: "La consolidation lente et la mise en place stable", e: "C" },{ t: "La finition méticuleuse et l'épuration finale", e: "D" },{ t: "La gestation secrète et la réflexion intuitive", e: "E" }] },
        { q: "10. Quelle qualité féminine souhaitez-vous incarner davantage ?", options: [{ t: "La force d'affirmation et la croissance libre", e: "A" },{ t: "La joie de vivre solaire et la connexion au cœur", e: "B" },{ t: "La capacité d'ancrage et le soin apporté à soi", e: "C" },{ t: "L'intégrité souveraine et la clarté du discernement", e: "D" },{ t: "La sagesse silencieuse et l'écoute de l'invisible", e: "E" }] },
        { q: "11. Comment décririez-vous votre sommeil actuel ?", options: [{ t: "Agité, peuplé de rêves de mouvement", e: "A" },{ t: "Court mais intense, avec des réveils légers", e: "B" },{ t: "Lourd et profond, avec des réveils embrumés", e: "C" },{ t: "Calme et régulier, mais parfois sec", e: "D" },{ t: "Immense et onirique, plongée en eaux profondes", e: "E" }] },
        { q: "12. Si votre âme était un objet précieux aujourd'hui, lequel serait-ce ?", options: [{ t: "Une tige de bambou, flexible et incassable", e: "A" },{ t: "Une flamme libre, dansant librement", e: "B" },{ t: "Une poterie d'argile, façonnée avec amour", e: "C" },{ t: "Un miroir d'argent pur, poli et clair", e: "D" },{ t: "Une perle de nacre au fond de l'océan", e: "E" }] }
    ];

    // NOUVELLE LOGIQUE DE TEASING
    const results = {
        A: { icon: "🌿", label: "Bois", teasing: "Une force d'expansion naturelle et une vision claire, souvent freinées par une charge mentale invisible. Il est temps d'apprendre à avancer sans t'épuiser." },
        B: { icon: "🔥", label: "Feu", teasing: "Un rayonnement magnétique et une joie contagieuse, qui demandent à être nourris sans se consumer. Découvre comment canaliser cette intensité." },
        C: { icon: "🏺", label: "Terre", teasing: "Un pilier nourricier pour les autres et un ancrage profond, qui doit maintenant apprendre à se recevoir et se prioriser elle-même." },
        D: { icon: "✨", label: "Métal", teasing: "Une clarté d'esprit et une exigence rares, cachant une sensibilité précieuse qu'il te faut maintenant apprendre à protéger." },
        E: { icon: "💧", label: "Eau", teasing: "Une profondeur, une sagesse et une intuition puissantes, nécessitant de préserver farouchement ton énergie vitale de ce qui te draine." }
    };

    let currentQuestion = 0;
    let scores = { A: 0, B: 0, C: 0, D: 0, E: 0 };

    function loadQuestion() {
        const q = quizData[currentQuestion];
        document.getElementById('question-text').innerText = q.q;
        const container = document.getElementById('options-container');
        container.innerHTML = '';
        q.options.forEach(opt => {
            const btn = document.createElement('button');
            btn.className = "option-btn w-full text-left p-6 rounded-2xl bg-white border border-stone-200 text-stone-700 font-light shadow-sm hover:shadow-md";
            btn.innerText = opt.t;
            btn.onclick = () => selectOption(opt.e);
            container.appendChild(btn);
        });
        document.getElementById('progress').style.width = (currentQuestion / quizData.length * 100) + '%';
        document.getElementById('progress-text').innerText = "Question " + (currentQuestion + 1) + " / 12";
    }

    function selectOption(element) {
        scores[element]++;
        currentQuestion++;
        if (currentQuestion < quizData.length) {
            const box = document.getElementById('question-box');
            box.classList.remove('fade-in');
            void box.offsetWidth; 
            box.classList.add('fade-in');
            loadQuestion();
        } else {
            showResult();
        }
    }

    function showResult() {
        document.getElementById('question-box').classList.add('hidden');
        document.getElementById('quiz-header').classList.add('hidden');
        const resultBox = document.getElementById('result-box');
        resultBox.classList.remove('hidden');

        // Tri des scores pour trouver les 2 dominants
        let sorted = Object.entries(scores).sort((a,b) => b[1] - a[1]);
        let dom = sorted[0][0];
        let sec = sorted[1][0];

        const res = results[dom];
        const resSec = results[sec];

        // Affichage des éléments sans tout révéler
        document.getElementById('element-icon').innerText = res.icon;
        document.getElementById('result-title').innerText = `${res.label} & ${resSec.label}`;

        // Création du bloc de teasing
        const teasingHTML = `
            <p class="text-xl text-stone-700 font-serif italic mb-6">« ${res.teasing} »</p>
            <p class="text-stone-600 mb-4 text-base">La combinaison <strong>${res.label} - ${resSec.label}</strong> est une synergie énergétique unique. Elle porte en elle une puissance insoupçonnée, mais aussi une zone d'ombre silencieuse.</p>
            <p class="text-stone-800 font-medium text-base">Pour comprendre comment ces deux forces interagissent réellement en vous, j'ai préparé votre analyse complète.</p>
        `;
        document.getElementById('result-content').innerHTML = teasingHTML;
    }
    loadQuestion();
</script>
</body>
</html>
