# DiagnosticQuizz<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Souffle Tao - Le Quiz</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #fdfbf7;
            color: #3d3d3d;
        }
        h1, h2, h3, .serif {
            font-family: 'Bodoni Moda', serif;
        }
        .option-btn {
            transition: all 0.3s ease;
            border: 1px solid #e5e7eb;
        }
        .option-btn:hover {
            border-color: #c5a67c;
            background-color: #fffaf0;
            transform: translateY(-2px);
        }
        .progress-bar {
            transition: width 0.5s ease-in-out;
        }
        .fade-in {
            animation: fadeIn 0.8s ease-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-4">

    <div id="quiz-container" class="max-w-2xl w-full bg-white rounded-3xl shadow-xl overflow-hidden p-8 md:p-12 relative">
        <!-- Header -->
        <div id="quiz-header" class="text-center mb-8">
            <span class="text-xs uppercase tracking-widest text-stone-400 mb-2 block">Voyage Intérieur</span>
            <h1 class="text-3xl md:text-4xl text-stone-800">Quel est ton élément dominant ?</h1>
            <div class="w-full bg-stone-100 h-1 mt-8 rounded-full">
                <div id="progress" class="progress-bar bg-stone-400 h-1 rounded-full" style="width: 0%"></div>
            </div>
        </div>

        <!-- Question Area -->
        <div id="question-box" class="fade-in">
            <h3 id="question-text" class="text-xl md:text-2xl mb-8 leading-relaxed text-stone-700"></h3>
            <div id="options-container" class="space-y-4">
                <!-- Options injected here -->
            </div>
        </div>

        <!-- Result Area (Hidden by default) -->
        <div id="result-box" class="hidden fade-in text-center">
            <div id="element-icon" class="text-5xl mb-4"></div>
            <h2 id="result-title" class="text-3xl mb-4 text-stone-800"></h2>
            <p id="result-archetype" class="italic text-stone-500 mb-6"></p>
            <div id="result-content" class="text-left text-stone-600 leading-relaxed mb-8 p-6 bg-stone-50 rounded-2xl"></div>
            
            <div class="border-t border-stone-100 pt-8 mt-8">
                <p class="text-sm text-stone-500 mb-4">Ton paysage intérieur se dessine...</p>
                <h3 class="serif text-xl mb-6 text-stone-800">Reçois ton Oracle de Saison complet</h3>
                <form id="capture-form" class="space-y-4">
                    <input type="text" placeholder="Ton prénom" required class="w-full px-4 py-3 rounded-lg border border-stone-200 focus:outline-none focus:ring-1 focus:ring-stone-400">
                    <input type="email" placeholder="Ton e-mail" required class="w-full px-4 py-3 rounded-lg border border-stone-200 focus:outline-none focus:ring-1 focus:ring-stone-400">
                    <button type="submit" class="w-full bg-stone-800 text-white py-4 rounded-lg hover:bg-stone-700 transition shadow-lg uppercase tracking-widest text-sm">Recevoir mon Guide PDF</button>
                </form>
                <p class="text-xs text-stone-400 mt-6">Tes données sont protégées dans notre temple numérique, tu pourras te désinscrire d'un simple souffle.</p>
            </div>
        </div>
    </div>

    <script>
        const quizData = [
            {
                q: "1. Si tu devais te fondre dans un paysage pour te ressourcer, lequel choisirais-tu ?",
                options: [
                    { t: "Une forêt dense où l'on sent l'odeur de la mousse", e: "A" },
                    { t: "Un champ baigné de soleil où l'on s'enivre de chaleur", e: "B" },
                    { t: "Une plaine fertile où l'on pétrit la terre douce", e: "C" },
                    { t: "Une montagne pure où l'on respire l'air cristallin", e: "D" },
                    { t: "Un rivage nocturne où l'on écoute le chant des abysses", e: "E" }
                ]
            },
            {
                q: "2. Quel aspect de la lumière t'appelle le plus intensément aujourd'hui ?",
                options: [
                    { t: "Le vert tendre des bourgeons qui percent l'écorce", e: "A" },
                    { t: "L'éclat vibrant de midi qui fait danser l'air", e: "B" },
                    { t: "La douceur dorée du crépuscule qui enveloppe le monde", e: "C" },
                    { t: "La clarté blanche de l'aube qui purifie le regard", e: "D" },
                    { t: "Les reflets argentés de la lune qui scintillent sur l'eau", e: "E" }
                ]
            },
            {
                q: "3. Dans le cycle des saisons, quel moment te semble le plus sacré ?",
                options: [
                    { t: "Le jaillissement irrésistible du renouveau printanier", e: "A" },
                    { t: "L'apogée radieuse et brûlante de l'été", e: "B" },
                    { t: "La transition généreuse et nourricière de l'été indien", e: "C" },
                    { t: "Le dépouillement élégant et nécessaire de l'automne", e: "D" },
                    { t: "Le silence régénérateur et mystérieux de l'hiver", e: "E" }
                ]
            },
            {
                q: "4. Quelle sensation tactile évoque pour toi la plénitude absolue ?",
                options: [
                    { t: "Toucher la sève qui monte sous une écorce", e: "A" },
                    { t: "Sentir la caresse d'une braise sur la peau", e: "B" },
                    { t: "Enfoncer ses doigts dans le velouté du terreau", e: "C" },
                    { t: "Effleurer la fraîcheur polie d'un cristal de roche", e: "D" },
                    { t: "Se laisser porter par la fluidité d'une onde fraîche", e: "E" }
                ]
            },
            {
                q: "5. En ce moment, quand ton emploi du temps sature, comment ton corps s'exprime-t-il ?",
                options: [
                    { t: "Des tensions qui se logent dans la nuque", e: "A" },
                    { t: "Des palpitations ou une agitation dans la poitrine", e: "B" },
                    { t: "Une sensation de lourdeur après chaque repas", e: "C" },
                    { t: "Une respiration qui devient courte et serrée", e: "D" },
                    { t: "Une fatigue sourde nichée dans le creux des reins", e: "E" }
                ]
            },
            {
                q: "6. Ces derniers temps, face à un imprévu, quelle est ta réaction émotionnelle réflexe ?",
                options: [
                    { t: "Une pointe d'impatience qui pousse à l'action", e: "A" },
                    { t: "Un besoin soudain de partager et de se connecter", e: "B" },
                    { t: "Une tendance à ruminer et à trop réfléchir", e: "C" },
                    { t: "Un retrait immédiat pour retrouver son espace", e: "D" },
                    { t: "Une sensation de peur diffuse, un besoin de refuge", e: "E" }
                ]
            },
            {
                q: "7. En ce moment, de quoi as-tu le plus besoin pour retrouver ton calme ?",
                options: [
                    { t: "De mettre ton corps en mouvement et de créer", e: "A" },
                    { t: "De rire aux éclats et d'échanger avec ton cercle", e: "B" },
                    { t: "De te sentir entourée et tendrement nourrie", e: "C" },
                    { t: "De trier tes objets, d'épurer et de faire le vide", e: "D" },
                    { t: "De silence absolu et de plonger dans l'obscurité", e: "E" }
                ]
            },
            {
                q: "8. Ces jours-ci, quel est le goût qui te réconforte instinctivement ?",
                options: [
                    { t: "L'acidulé d'un fruit frais et tonique", e: "A" },
                    { t: "L'amertume élégante d'un carré de cacao noir", e: "B" },
                    { t: "La douceur rassurante d'un aliment onctueux et sucré", e: "C" },
                    { t: "Le piquant d'une épice fine qui réveille les sens", e: "D" },
                    { t: "Le salé minéral d'une eau de source profonde", e: "E" }
                ]
            },
            {
                q: "9. En ce moment, dans tes projets, quelle étape te procure le plus de joie ?",
                options: [
                    { t: "L'élan initial, la naissance d'une idée neuve", e: "A" },
                    { t: "Le moment du partage et du rayonnement public", e: "B" },
                    { t: "La consolidation lente et la mise en place stable", e: "C" },
                    { t: "La finition méticuleuse et l'épuration finale", e: "D" },
                    { t: "La gestation secrète et la réflexion intuitive", e: "E" }
                ]
            },
            {
                q: "10. Ces derniers temps, quelle qualité féminine souhaites-tu incarner davantage ?",
                options: [
                    { t: "La force d'affirmation et la croissance libre", e: "A" },
                    { t: "La joie de vivre solaire et la connexion au cœur", e: "B" },
                    { t: "La capacité d'ancrage et le soin apporté à soi", e: "C" },
                    { t: "L'intégrité souveraine et la clarté du discernement", e: "D" },
                    { t: "La sagesse silencieuse et l'écoute de l'invisible", e: "E" }
                ]
            },
            {
                q: "11. En ce moment, comment décrirais-tu ton sommeil ?",
                options: [
                    { t: "Agité, peuplé de rêves de mouvement et d'action", e: "A" },
                    { t: "Court mais intense, avec des réveils légers", e: "B" },
                    { t: "Lourd et profond, avec des réveils embrumés", e: "C" },
                    { t: "Calme et régulier, mais parfois sec", e: "D" },
                    { t: "Immense et onirique, plongée en eaux profondes", e: "E" }
                ]
            },
            {
                q: "12. Si ton âme était un objet précieux aujourd'hui, lequel serait-ce ?",
                options: [
                    { t: "Une tige de bambou, flexible et incassable", e: "A" },
                    { t: "Une flamme libre, dansant librement", e: "B" },
                    { t: "Une poterie d'argile, façonnée avec amour", e: "C" },
                    { t: "Un miroir d'argent pur, poli et clair", e: "D" },
                    { t: "Une perle de nacre au fond de l'océan", e: "E" }
                ]
            }
        ];

        const results = {
            A: {
                title: "L'Élan du BOIS",
                icon: "🌿",
                archetype: "La Visionnaire, l'Amazone",
                content: "Tu portes en toi l'énergie du Printemps, une sève montante qui demande à créer, décider et avancer. Ton super-pouvoir est ta vision du futur. <br><br><strong>Conseil :</strong> Libère tes tensions en massant le point Taichong sur tes pieds et privilégie les saveurs acidulées."
            },
            B: {
                title: "La Flamme du FEU",
                icon: "🔥",
                archetype: "L'Impératrice, l'Amoureuse",
                content: "Tu vibres à la fréquence de l'Été. Tu es faite pour la connexion, la joie et l'expression. Tu réchauffes ton entourage par ta simple présence. <br><br><strong>Conseil :</strong> Apaise ton cœur avec un peu d'amertume (cacao noir) et stimule le point Shenmen pour calmer l'agitation."
            },
            C: {
                title: "Le Socle de la TERRE",
                icon: "🏺",
                archetype: "La Mère Nourricière, la Gardienne",
                content: "Tu incarnes l'Intersaison, la récolte et la stabilité. Ta force réside dans ta capacité à soutenir et harmoniser les liens. <br><br><strong>Conseil :</strong> Reviens à toi avec des aliments orangés et stimule le point Zusanli pour renforcer ton ancrage."
            },
            D: {
                title: "Le Joyau du MÉTAL",
                icon: "✨",
                archetype: "L'Alchimiste, la Sage",
                content: "Tu es l'Automne, le moment où l'essentiel se révèle. Tu cherches la pureté et la clarté. Tu sais trancher pour garder ce qui a de la valeur. <br><br><strong>Conseil :</strong> Respire avec le point Hegu et mise sur les aliments blancs pour nourrir tes poumons."
            },
            E: {
                title: "La Source de l'EAU",
                icon: "💧",
                archetype: "La Mystique, la Femme Sauvage",
                content: "Tu portes l'énergie de l'Hiver, celle des profondeurs et de l'intuition. Tu sais écouter le silence et voir au-delà du visible. <br><br><strong>Conseil :</strong> Recharge tes réserves avec des aliments noirs et frictionne tes plantes de pieds (Yongquan)."
            }
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
                btn.className = "option-btn w-full text-left p-5 rounded-2xl bg-white hover:shadow-md text-stone-700";
                btn.innerText = opt.t;
                btn.onclick = () => selectOption(opt.e);
                container.appendChild(btn);
            });

            const progress = ((currentQuestion) / quizData.length) * 100;
            document.getElementById('progress').style.width = progress + '%';
        }

        function selectOption(element) {
            scores[element]++;
            currentQuestion++;
            
            if (currentQuestion < quizData.length) {
                const box = document.getElementById('question-box');
                box.classList.remove('fade-in');
                void box.offsetWidth; // trigger reflow
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

            // Find dominant element
            let dominant = 'A';
            for (let e in scores) {
                if (scores[e] > scores[dominant]) dominant = e;
            }

            const res = results[dominant];
            document.getElementById('element-icon').innerText = res.icon;
            document.getElementById('result-title').innerText = res.title;
            document.getElementById('result-archetype').innerText = res.archetype;
            document.getElementById('result-content').innerHTML = res.content;
        }

        document.getElementById('capture-form').onsubmit = (e) => {
            e.preventDefault();
            const btn = e.target.querySelector('button');
            btn.innerText = "Invitation envoyée...";
            btn.disabled = true;
            btn.style.backgroundColor = "#a8a29e";
            setTimeout(() => {
                alert("Merci de ta confiance. Ton Oracle arrive dans ton écrin mail.");
            }, 500);
        };

        loadQuestion();
    </script>
</body>
</html>
