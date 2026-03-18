<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>L'Éveil de la Souveraine - Quiz Énergétique</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Montserrat:wght@200;300;400&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Montserrat', sans-serif; }
        .font-serif { font-family: 'Cinzel', serif; }
        .transition-all { transition: all 0.5s ease; }
    </style>
</head>
<body class="bg-stone-100 text-stone-800 min-h-screen">

    <div class="max-w-4xl mx-auto py-12 px-4">
        <header class="text-center mb-12">
            <h1 class="font-serif text-4xl md:text-5xl text-stone-900 tracking-widest uppercase mb-4">L'Éveil de la Souveraine</h1>
            <div class="h-px w-24 bg-stone-400 mx-auto mb-6"></div>
            <p class="italic text-stone-600 tracking-wide font-light text-sm md:text-base">Découvrez la synergie des 5 Éléments qui guide votre puissance intérieure.</p>
        </header>

        <div id="quiz-container" class="bg-white p-8 md:p-12 shadow-sm border border-stone-200 transition-all">
            <div id="progress-bar" class="w-full h-1 bg-stone-100 mb-8">
                <div id="progress" class="h-full bg-stone-800 transition-all duration-500" style="width: 0%"></div>
            </div>

            <div id="question-box">
                <h2 id="question-text" class="font-serif text-2xl mb-8 leading-relaxed text-stone-900 text-center">Chargement...</h2>
                <div id="options" class="grid gap-4">
                </div>
            </div>
        </div>

        <div id="result-box" class="hidden max-w-2xl mx-auto text-center py-12 px-6 bg-stone-50 border border-stone-200 rounded-lg shadow-sm">
            <h2 class="font-serif text-3xl text-stone-800 mb-4 italic leading-tight">
                L'analyse énergétique est terminée.
            </h2>
            <p class="font-serif text-xl text-stone-600 mb-10">
                Votre synergie dominante est prête à être révélée.
            </p>

            <div class="bg-white p-10 border border-stone-100 shadow-md">
                <h3 class="font-serif text-2xl text-stone-900 mb-4">
                    Recevez votre Profil Énergétique Complet
                </h3>
                
                <p class="text-stone-700 mb-10 leading-relaxed font-light text-lg">
                    Souveraine, votre synergie unique a été identifiée. Entrez votre adresse e-mail pour recevoir votre analyse et rejoindre les <strong>Chroniques Souffle Tao</strong> (le rendez-vous bi-mensuel des femmes de pouvoir).
                </p>

                <a href="https://souffletao.substack.com/welcome" 
                   class="inline-block w-full sm:w-auto bg-stone-800 text-stone-50 px-12 py-5 rounded-none font-serif tracking-widest hover:bg-stone-700 transition-all duration-300 uppercase text-sm shadow-xl">
                    DÉCOUVRIR MON ÉLÉMENT DOMINANT
                </a>

                <p class="mt-8 text-xs text-stone-400 italic tracking-wide">
                    100% gratuit. Désabonnement en 1 clic.
                </p>
            </div>
        </div>
    </div>

    <script>
        const questions = [
            { text: "1. Face à un nouveau projet ambitieux, quel est votre premier élan ?", options: [
                { text: "Tracer une vision claire et passer à l'action.", element: "Bois" },
                { text: "Partager l'enthousiasme et inspirer les autres.", element: "Feu" },
                { text: "Poser les bases et assurer la stabilité du groupe.", element: "Terre" },
                { text: "Structurer chaque détail avec précision.", element: "Métal" },
                { text: "Écouter mon intuition et laisser le projet mûrir.", element: "Eau" }
            ]},
            { text: "2. Dans un moment de stress intense, comment réagissez-vous ?", options: [
                { text: "Je m'impatiente et je veux trancher vite.", element: "Bois" },
                { text: "Mes émotions débordent, j'ai besoin de m'exprimer.", element: "Feu" },
                { text: "Je m'inquiète pour les autres et je m'oublie.", element: "Terre" },
                { text: "Je me replie sur moi-même pour tout contrôler.", element: "Métal" },
                { text: "Je me fige et je m'isole dans mes pensées.", element: "Eau" }
            ]},
            { text: "3. Quelle est votre plus grande force naturelle ?", options: [
                { text: "Ma détermination inébranlable.", element: "Bois" },
                { text: "Mon rayonnement et mon charisme.", element: "Feu" },
                { text: "Ma capacité à soutenir et à nourrir.", element: "Terre" },
                { text: "Ma clarté mentale et mon discernement.", element: "Métal" },
                { text: "Ma sagesse profonde et ma résilience.", element: "Eau" }
            ]},
            { text: "4. Comment préférez-vous passer votre temps libre ?", options: [
                { text: "Apprendre une nouvelle compétence ou faire du sport.", element: "Bois" },
                { text: "Sortir, voir du monde et célébrer la vie.", element: "Feu" },
                { text: "Prendre soin de mon foyer ou cuisiner pour mes proches.", element: "Terre" },
                { text: "Lire, méditer ou organiser mon espace.", element: "Métal" },
                { text: "Rêver, écrire ou être près de l'eau.", element: "Eau" }
            ]},
            { text: "5. Quel environnement vous ressource le plus ?", options: [
                { text: "Une forêt dense et vibrante.", element: "Bois" },
                { text: "Un lieu ensoleillé et chaleureux.", element: "Feu" },
                { text: "Une campagne paisible et fertile.", element: "Terre" },
                { text: "Une montagne pure et silencieuse.", element: "Métal" },
                { text: "Le bord de l'océan ou un lac calme.", element: "Eau" }
            ]},
            { text: "6. Quelle est votre relation au changement ?", options: [
                { text: "Je le provoque, c'est un moteur de croissance.", element: "Bois" },
                { text: "Je l'accueille avec excitation et passion.", element: "Feu" },
                { text: "Je l'appréhende, je préfère la stabilité.", element: "Terre" },
                { text: "Je l'analyse pour m'y adapter avec justesse.", element: "Métal" },
                { text: "Je le laisse couler, je m'adapte naturellement.", element: "Eau" }
            ]},
            { text: "7. Quel est votre plus grand défi actuel ?", options: [
                { text: "Gérer ma colère ou mon impatience.", element: "Bois" },
                { text: "Canaliser mon agitation ou mon anxiété.", element: "Feu" },
                { text: "Arrêter de trop cogiter ou de m'inquiéter.", element: "Terre" },
                { text: "Lâcher prise sur la perfection et le contrôle.", element: "Métal" },
                { text: "Surmonter mes peurs ou mon manque de clarté.", element: "Eau" }
            ]},
            { text: "8. Comment prenez-vous vos décisions ?", options: [
                { text: "Rapidement, de manière instinctive et tranchée.", element: "Bois" },
                { text: "Avec le cœur et selon mon enthousiasme.", element: "Feu" },
                { text: "Après avoir pris l'avis de mon entourage.", element: "Terre" },
                { text: "Après une analyse logique et rigoureuse.", element: "Métal" },
                { text: "En suivant mon intuition profonde et silencieuse.", element: "Eau" }
            ]},
            { text: "9. Qu'est-ce qui vous fatigue le plus ?", options: [
                { text: "L'inaction et la stagnation.", element: "Bois" },
                { text: "Le manque de connexion humaine.", element: "Feu" },
                { text: "Le désordre et l'instabilité.", element: "Terre" },
                { text: "L'injustice et le manque de rigueur.", element: "Métal" },
                { text: "Le bruit excessif et l'agitation superficielle.", element: "Eau" }
            ]},
            { text: "10. Quelle est votre saison préférée ?", options: [
                { text: "Le Printemps (Renouveau).", element: "Bois" },
                { text: "L'Été (Expansion).", element: "Feu" },
                { text: "L'Été Indien (Récolte).", element: "Terre" },
                { text: "L'Automne (Dépouillement).", element: "Métal" },
                { text: "L'Hiver (Intériorisation).", element: "Eau" }
            ]},
            { text: "11. Comment exprimez-vous votre créativité ?", options: [
                { text: "En lançant de nouveaux concepts innovants.", element: "Bois" },
                { text: "Par l'expression artistique ou la parole.", element: "Feu" },
                { text: "En créant de l'harmonie et du confort.", element: "Terre" },
                { text: "Par le raffinement et le souci du détail.", element: "Métal" },
                { text: "Par l'imaginaire et la réflexion profonde.", element: "Eau" }
            ]},
            { text: "12. Quel mot résonne le plus avec votre âme ?", options: [
                { text: "Liberté.", element: "Bois" },
                { text: "Joie.", element: "Feu" },
                { text: "Sérénité.", element: "Terre" },
                { text: "Vérité.", element: "Métal" },
                { text: "Profondeur.", element: "Eau" }
            ]},
            // NOUVELLES QUESTIONS POUR ARRIVER À 16
            { text: "13. Quelle est votre réaction face à un conflit ?", options: [
                { text: "Je confronte directement pour résoudre.", element: "Bois" },
                { text: "Je cherche à apaiser par l'humour ou l'émotion.", element: "Feu" },
                { text: "Je cherche le compromis pour garder l'harmonie.", element: "Terre" },
                { text: "Je prends de la distance et j'analyse froidement.", element: "Métal" },
                { text: "J'évite le choc et j'attends que ça passe.", element: "Eau" }
            ]},
            { text: "14. Comment gérez-vous votre énergie au quotidien ?", options: [
                { text: "Par pics d'activité intense et explosive.", element: "Bois" },
                { text: "En rayonnant, mais je m'épuise vite socialement.", element: "Feu" },
                { text: "De manière constante, comme un marathon.", element: "Terre" },
                { text: "Avec discipline et rituels précis.", element: "Métal" },
                { text: "Par cycles lents, j'ai besoin de beaucoup de repos.", element: "Eau" }
            ]},
            { text: "15. Quel rôle occupez-vous naturellement dans un groupe ?", options: [
                { text: "La leader qui donne la direction.", element: "Bois" },
                { text: "Celle qui anime et crée du lien.", element: "Feu" },
                { text: "Celle qui soutient et stabilise.", element: "Terre" },
                { text: "La conseillère qui apporte la structure.", element: "Métal" },
                { text: "L'observatrice qui apporte la vision profonde.", element: "Eau" }
            ]},
            { text: "16. Quel est votre rapport au corps ?", options: [
                { text: "Un outil de performance et de mouvement.", element: "Bois" },
                { text: "Un vecteur de sensations et de plaisir.", element: "Feu" },
                { text: "Un temple qu'il faut nourrir et sécuriser.", element: "Terre" },
                { text: "Un espace de discipline et de pureté.", element: "Métal" },
                { text: "Un réceptacle d'intuitions et de mystères.", element: "Eau" }
            ]}
        ];

        let currentQuestion = 0;
        let scores = { Bois: 0, Feu: 0, Terre: 0, Métal: 0, Eau: 0 };

        function loadQuestion() {
            const q = questions[currentQuestion];
            document.getElementById('question-text').innerText = q.text;
            const optionsDiv = document.getElementById('options');
            optionsDiv.innerHTML = '';
            
            q.options.forEach(opt => {
                const btn = document.createElement('button');
                btn.className = "w-full py-4 px-6 text-left border border-stone-200 hover:border-stone-800 hover:bg-stone-50 transition-all font-light tracking-wide text-stone-700";
                btn.innerText = opt.text;
                btn.onclick = () => selectOption(opt.element);
                optionsDiv.appendChild(btn);
            });

            const progress = (currentQuestion / questions.length) * 100;
            document.getElementById('progress').style.width = progress + '%';
        }

        function selectOption(element) {
            scores[element]++;
            currentQuestion++;
            if (currentQuestion < questions.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            document.getElementById('quiz-container').classList.add('hidden');
            const resultBox = document.getElementById('result-box');
            resultBox.classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
            console.log("Diagnostic terminé. Scores:", scores);
        }

        loadQuestion();
    </script>
</body>
</html>
