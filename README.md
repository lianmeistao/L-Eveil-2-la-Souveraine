<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz — Quel est ton élément dominant ?</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .fade-in { animation: fadeIn 0.4s ease both; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .serif { font-family: ui-serif, Georgia, Cambria, "Times New Roman", Times, serif; }
    </style>
</head>

<body class="min-h-screen bg-stone-100 flex items-center justify-center font-sans">
    <div id="quiz-container" class="max-w-2xl w-full bg-white rounded-3xl shadow-xl overflow-hidden p-8 md:p-12 m-4 relative">
        
        <!-- Header -->
        <div id="quiz-header" class="text-center mb-8">
            <span class="text-xs uppercase tracking-widest text-stone-400 mb-2 block">Voyage Intérieur</span>
            <h1 class="text-3xl md:text-4xl text-stone-800">Quel est ton élément dominant ?</h1>
            <div class="w-full bg-stone-100 h-1 mt-8 rounded-full">
                <div id="progress" class="bg-stone-400 h-1 rounded-full transition-all duration-300" style="width: 0%"></div>
            </div>
        </div>

        <!-- Question Area -->
        <div id="question-box" class="fade-in">
            <h3 id="question-text" class="text-xl md:text-2xl mb-8 leading-relaxed text-stone-700"></h3>
            <div id="options-container" class="space-y-4">
                <!-- Les options s'injectent ici -->
            </div>
        </div>

        <!-- Result Area (Masqué par défaut) -->
        <div id="result-box" class="hidden fade-in text-center">
            <div id="element-icon" class="text-6xl mb-4"></div>
            <h2 id="result-title" class="text-3xl mb-4 text-stone-800"></h2>
            <p id="result-archetype" class="italic text-stone-500 mb-6 font-serif text-lg"></p>
            <div id="result-content" class="text-left text-stone-600 leading-relaxed mb-8 p-6 bg-stone-50 rounded-2xl border border-stone-100"></div>
            
            <div class="border-t border-stone-100 pt-8 mt-8 text-left">
                <p class="text-sm text-stone-500 mb-2 italic text-center">Ton paysage intérieur se dessine...</p>
                <h3 class="serif text-2xl mb-4 text-stone-800 text-center">Reçois ton Oracle de Saison complet</h3>
                
                <!-- Message d'information avant abonnement -->
                <div class="bg-stone-50 border border-stone-100 rounded-2xl p-5 mb-6 text-sm text-stone-600 leading-relaxed">
                    <p class="mb-3">
                        En t'abonnant à mes Chroniques sur <strong>Substack</strong>, tu recevras immédiatement le lien pour télécharger ton PowerPoint 
                        <strong>"L'Éveil de la Souveraine"</strong> (le guide complet des 5 éléments) dans ton mail de bienvenue.
                    </p>
                    <p class="text-xs text-stone-400 italic">
                        Tu rejoins ainsi notre cercle privé. Désinscription possible d'un simple souffle.
                    </p>
                </div>

                <!-- Formulaire d'inscription Substack intégré -->
                <div class="max-w-md mx-auto border border-stone-200 rounded-xl overflow-hidden shadow-sm">
                    <iframe 
                        src="https://souffletao2lyanmey.substack.com/embed" 
                        width="100%" 
                        height="320" 
                        style="border:0; background:white;" 
                        frameborder="0" 
                        scrolling="no">
                    </iframe>
                </div>
                
                <p class="text-xs text-stone-400 mt-6 text-center italic">
                    Regarde ta boîte mail après avoir validé ton inscription !
                </p>
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
            A: { title: "L'Élan du BOIS", icon: "🌿", archetype: "La Visionnaire, l'Amazone", content: "Tu portes en toi l'énergie du Printemps, une sève montante qui demande à créer, décider et avancer. Ton super-pouvoir est ta vision du futur. <br><br><strong>Rituels :</strong> Libère tes tensions en massant le point Taichong sur tes pieds et privilégie les saveurs acidulées." },
            B: { title: "La Flamme du FEU", icon: "🔥", archetype: "L'Impératrice, l'Amoureuse", content: "Tu vibres à la fréquence de l'Été. Tu es faite pour la connexion, la joie et l'expression. Tu réchauffes ton entourage par ta simple présence. <br><br><strong>Rituels :</strong> Apaise ton cœur avec un peu d'amertume (cacao noir) et stimule le point Shenmen pour calmer l'agitation." },
            C: { title: "Le Socle de la TERRE", icon: "🏺", archetype: "La Mère Nourricière, la Gardienne", content: "Tu incarnes l'Intersaison, la récolte et la stabilité. Ta force réside dans ta capacité à soutenir et harmoniser les liens. <br><br><strong>Rituels :</strong> Reviens à toi avec des aliments orangés et stimule le point Zusanli pour renforcer ton ancrage." },
            D: { title: "Le Joyau du MÉTAL", icon: "✨", archetype: "L'Alchimiste, la Sage", content: "Tu es l'Automne, le moment où l'essentiel se révèle. Tu cherches la pureté et la clarté. Tu sais trancher pour garder ce qui a de la valeur. <br><br><strong>Rituels :</strong> Respire avec le point Hegu et mise sur les aliments blancs pour nourrir tes poumons." },
            E: { title: "La Source de l'EAU", icon: "💧", archetype: "La Mystique, la Femme Sauvage", content: "Tu portes l'énergie de l'Hiver, celle des profondeurs et de l'intuition. Tu sais écouter le silence et voir au-delà du visible. <br><br><strong>Rituels :</strong> Recharge tes réserves avec des aliments noirs et frictionne tes plantes de pieds (point Yongquan)." }
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
                btn.className = "option-btn w-full text-left p-5 rounded-2xl bg-white border border-stone-100 hover:border-stone-300 hover:shadow-md transition-all text-stone-700 font-light";
                btn.innerText = opt.t;
                btn.onclick = () => selectOption(opt.e);
                container.appendChild(btn);
            });

            const progress = (currentQuestion / quizData.length) * 100;
            document.getElementById('progress').style.width = progress + '%';
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

            let dominant = 'A';
            for (let e in scores) {
                if (scores[e] > scores[dominant]) dominant = e;
            }

            const res = results[dominant];
            document.getElementById('element-icon').innerText = res.icon;
            document.getElementById('result-title').innerText = res.title;
            document.getElementById('result-archetype').innerText = res.archetype;
            document.getElementById('result-content').innerHTML = res.content;
            document.getElementById('progress').style.width = '100%';
        }

        loadQuestion();
    </script>
</body>
</html>

