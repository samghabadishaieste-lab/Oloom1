<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>بازی علمی - کلاس خانم شایسته صفی</title>
    <style>
        body { background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%); font-family: Tahoma, sans-serif; text-align: center; padding: 20px; }
        .card { background: white; padding: 25px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.2); max-width: 600px; margin: auto; }
        button { background-color: #ff7e5f; color: white; border: none; padding: 12px 20px; border-radius: 12px; cursor: pointer; margin: 8px; font-size: 16px; transition: 0.3s; }
        button:hover { background-color: #feb47b; }
        .hidden { display: none; }
        h1 { color: #333; }
    </style>
</head>
<body>

<div id="start-screen" class="card">
    <h1>به بازی علمی خوش آمدید!</h1>
    <p>آموزگار:   <strong>شایسته صفی</strong></p>
    <input type="text" id="studentName" placeholder="نام خود را وارد کنید..." style="padding: 10px; border-radius: 5px; border: 1px solid #ccc;">
    <br><br>
    <button onclick="startGame()">شروع بازی</button>
</div>

<div id="quiz-screen" class="card hidden">
    <h3 id="question">سوال</h3>
    <div id="options"></div>
</div>

<div id="result-screen" class="card hidden">
    <h2>کارنامه نهایی</h2>
    <p id="finalScore"></p>
    <div id="cheer" style="font-size: 1.2em; font-weight: bold; margin: 20px 0;"></div>
    <button onclick="location.reload()">شروع دوباره</button>
</div>

<script>
    const questions = [
        { q: "۱- کدام میوه، یک دانه ای است؟", options: ["سیب", "پرتقال", "زردآلو", "گوجه فرنگی"], a: 2 },
        { q: "۲- غذای کدام جانور، دانه ی گیاهان است؟", options: ["کبوتر", "گوسفند", "خرگوش", "بز"], a: 0 },
        { q: "۳- مهم ترین شباهت چرخ ریسک با خرگوش چیست؟", options: ["نوع غذا", "نوع تولید مثل", "ساختن لانه", "محل زندگی"], a: 2 },
        { q: "۴- غذای کرم ابریشم چیست؟", options: ["باقی مانده پیله", "کرم های دیگر", "برگ درخت توت", "میوه ی درختان"], a: 2 },
        { q: "۵- کدام مورد برای رشد بدن مفید نیست؟", options: ["گوشت و حبوبات", "کلم و سبزیجات", "لبنیات", "سوسیس و کالباس"], a: 3 },
        { q: "۶- راه مراقبت از دندان ها کدام است؟", options: ["مراجعه به دندانپزشک", "مسواک زدن", "شکستن چیزهای سفت با دندان", "گزینه ی (۱) و (۲)"], a: 3 },
        { q: "۷- استفاده ی زیاد از سوخت ها باعث ......... می شود.", options: ["آلودگی هوا", "تمام شدن سوخت ها", "مورد ۱ و ۲"], a: 2 },
        { q: "۸- سوخت ها می سوزند و ......... تولید می کنند.", options: ["گرما و صدا", "حرکت و صدا", "گرما و انرژی"], a: 2 },
        { q: "۹- دانه ها در کجا قرار دارند؟", options: ["درون ساقه", "درون گل", "درون میوه"], a: 2 },
        { q: "۱۰- محل زندگی کدام جانور با بقیه فرق دارد؟", options: ["آهو", "خرگوش", "نهنگ"], a: 2 },
        { q: "۱۱- کدام دسته از دندان های ما در دوران کودکی می افتد؟", options: ["آسیا", "همیشگی", "شیری"], a: 2 }
    ];

    let currentQ = 0, score = 0, name = "";

    function startGame() {
        name = document.getElementById("studentName").value || "دانش آموز عزیز";
        document.getElementById("start-screen").classList.add("hidden");
        document.getElementById("quiz-screen").classList.remove("hidden");
        showQuestion();
    }

    function showQuestion() {
        if(currentQ >= questions.length) return endQuiz();
        document.getElementById("question").innerText = questions[currentQ].q;
        let container = document.getElementById("options");
        container.innerHTML = "";
        questions[currentQ].options.forEach((opt, i) => {
            let btn = document.createElement("button");
            btn.innerText = opt;
            btn.onclick = () => { if(i === questions[currentQ].a) score++; currentQ++; showQuestion(); };
            container.appendChild(btn);
        });
    }

    function endQuiz() {
        document.getElementById("quiz-screen").classList.add("hidden");
        document.getElementById("result-screen").classList.remove("hidden");
        document.getElementById("finalScore").innerText = name + " عزیز، امتیاز شما: " + score + " از " + questions.length;
        
        let msg = score === questions.length ? "🌟 عالی بودی قهرمان! تو یک دانشمند کوچولوی واقعی هستی! 🌟" : "😊 تلاش خوبی بود! دوباره امتحان کن تا استاد بشی!";
        document.getElementById("cheer").innerHTML = msg;
    }
</script>
</body>
</html>
