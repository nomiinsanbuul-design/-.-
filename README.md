
<!DOCTYPE html>
<html lang="mn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Д.Нацагдоржийн тухай Quiz</title>
<style>
* { box-sizing: border-box; }
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f1f3f8;
  color: #202b43;
}
.container {
  max-width: 650px;
  margin: 35px auto;
  padding: 20px;
}
.card {
  background: white;
  padding: 30px;
  border-radius: 18px;
  box-shadow: 0 8px 30px #18233b12;
}
.tag {
  color: #3976d5;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
}
h1 { font-size: 28px; line-height: 1.35; }
.muted { color: #7b8495; line-height: 1.6; }
button {
  cursor: pointer;
  border: 0;
  border-radius: 10px;
  padding: 15px 20px;
  font-size: 16px;
  font-weight: bold;
}
.primary {
  width: 100%;
  color: white;
  background: #2866d6;
  margin-top: 18px;
}
.option {
  display: block;
  width: 100%;
  text-align: left;
  margin: 10px 0;
  background: #f4f6fa;
  color: #26334a;
  border: 2px solid transparent;
}
.option:hover { border-color: #8eb2f4; }
.option.selected {
  background: #eaf1ff;
  border-color: #2866d6;
}
.progress {
  height: 8px;
  background: #e8ebf2;
  border-radius: 20px;
  overflow: hidden;
  margin: 15px 0 25px;
}
.bar {
  height: 100%;
  background: #2866d6;
  transition: width .3s;
}
.hidden { display: none; }
.number {
  font-size: 42px;
  font-weight: bold;
  color: #2866d6;
}
.review {
  background: #f5f7fb;
  padding: 13px;
  border-radius: 10px;
  margin: 10px 0;
  line-height: 1.6;
}
</style>
</head>
<body>
<div class="container">

<section class="card" id="start">
  <div class="tag">МЭДЛЭГЭЭ СОРИХ QUIZ</div>
  <h1>Их зохиолч Д.Нацагдоржийн тухай хэр мэдэх вэ?</h1>
  <p class="muted">
    Монголын орчин үеийн уран зохиолын их төлөөлөгч
    Дашдоржийн Нацагдоржийн тухай 10 асуултад хариулаарай.
  </p>
  <p>📝 10 асуулт</p>
  <p>⏱ Өөрийн хурдаар</p>
  <p>🏆 Эцэст нь оноогоо мэдээрэй</p>
  <button class="primary" onclick="startQuiz()">QUIZ ЭХЛҮҮЛЭХ →</button>
</section>

<section class="card hidden" id="quiz">
  <div class="tag">Д. НАЦАГДОРЖИЙН ТУХАЙ</div>
  <p id="counter" class="muted"></p>
  <div class="progress"><div class="bar" id="bar"></div></div>
  <h2 id="question"></h2>
  <div id="options"></div>
  <button class="primary" id="next" onclick="nextQuestion()" disabled>
    ДАРААГИЙН АСУУЛТ →
  </button>
</section>

<section class="card hidden" id="result">
  <div class="tag">QUIZ ДУУСЛАА</div>
  <h1>Таны үр дүн</h1>
  <div class="number" id="score"></div>
  <h2 id="message"></h2>
  <p class="muted" id="percentage"></p>
  <div id="review"></div>
  <button class="primary" onclick="restart()">ДАХИН ЭХЛЭХ ↻</button>
</section>

</div>

<script>
const questions = [
{
 q:"Д.Нацагдорж хэдэн онд төрсөн бэ?",
 a:["1900 он","1906 он","1910 он","1915 он"],
 c:1,
 e:"Д.Нацагдорж 1906 онд төрсөн."
},
{
 q:"Д.Нацагдорж аль аймгийн нутагт төрсөн бэ?",
 a:["Архангай","Хэнтий","Төв","Дорнод"],
 c:2,
 e:"Тэрээр одоогийн Төв аймгийн Баяндэлгэр сумын Гүн Галуутайд төрсөн."
},
{
 q:"Д.Нацагдоржийн алдарт эх оронч шүлэг аль нь вэ?",
 a:["Миний нутаг","Харанхуй хад","Хуучин хүү","Шувуун саарал"],
 c:0,
 e:"Миний нутаг бол эх орон, байгаль дэлхийгээ магтан дуулсан алдарт шүлэг."
},
{
 q:"Д.Нацагдоржийн зохиол аль нь вэ?",
 a:["Монголын нууц товчоо","Хуучин хүү","Цогт тайж","Тунгалаг Тамир"],
 c:1,
 e:"Хуучин хүү бол Д.Нацагдоржийн алдарт өгүүллэг."
},
{
 q:"Д.Нацагдоржийн бичсэн алдарт дуурийн цомнол аль вэ?",
 a:["Учиртай гурван толгой","Жаргалын зам","Гэсэр","Алтан өргөө"],
 c:0,
 e:"Учиртай гурван толгой нь Д.Нацагдоржийн алдарт бүтээл."
},
{
 q:"Д.Нацагдорж хэдэн онд нас барсан бэ?",
 a:["1921 он","1930 он","1937 он","1945 он"],
 c:2,
 e:"Д.Нацагдорж 1937 онд нас барсан."
},
{
 q:"Д.Нацагдорж аль улсад суралцаж байсан бэ?",
 a:["Япон, Солонгос","ЗХУ, Герман","Франц, Англи","Хятад, Энэтхэг"],
 c:1,
 e:"Тэрээр ЗХУ болон Германд суралцаж байсан."
},
{
 q:"Дараахын аль нь Д.Нацагдоржийн өгүүллэг вэ?",
 a:["Харанхуй хад","Алтайн магтаал","Гэсэр","Уул усны шүлэг"],
 c:0,
 e:"Харанхуй хад бол Д.Нацагдоржийн алдарт өгүүллэг."
},
{
 q:"Д.Нацагдоржийн зохиосон хүүхдийн бүтээл аль вэ?",
 a:["Миний хэнз хурга","Алтан загас","Цагаан сар","Хөхөө Намжил"],
 c:0,
 e:"Миний хэнз хурга бол Д.Нацагдоржийн хүүхдэд зориулсан бүтээл."
},
{
 q:"Д.Нацагдоржийг Монголын утга зохиолд ямар байр суурьтай гэж үздэг вэ?",
 a:[
 "Монголын орчин үеийн уран зохиолыг үндэслэгчдийн нэг",
 "Зөвхөн орчуулагч",
 "Зөвхөн жүжигчин",
 "Зөвхөн түүхч"
 ],
 c:0,
 e:"Түүнийг Монголын орчин үеийн уран зохиолыг үндэслэгчдийн нэг гэж үздэг."
}
];

let current = 0;
let answers = [];
let selected = null;

function startQuiz() {
  current = 0;
  answers = [];
  document.getElementById("start").classList.add("hidden");
  document.getElementById("result").classList.add("hidden");
  document.getElementById("quiz").classList.remove("hidden");
  showQuestion();
}

function showQuestion() {
  selected = null;
  const item = questions[current];

  document.getElementById("counter").textContent =
    "Асуулт " + (current+1) + " / " + questions.length;

  document.getElementById("bar").style.width =
    ((current+1)/questions.length*100) + "%";

  document.getElementById("question").textContent = item.q;

  const box = document.getElementById("options");
  box.innerHTML = "";

  item.a.forEach((answer, index) => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.textContent = String.fromCharCode(65+index) + ". " + answer;

    btn.onclick = () => {
      selected = index;
      document.querySelectorAll(".option").forEach(
        b => b.classList.remove("selected")
      );
      btn.classList.add("selected");
      document.getElementById("next").disabled = false;
    };

    box.appendChild(btn);
  });

  document.getElementById("next").disabled = true;
  document.getElementById("next").textContent =
    current === questions.length-1 ? "ҮР ДҮН ХАРАХ →" : "ДАРААГИЙН АСУУЛТ →";
}

function nextQuestion() {
  if (selected === null) return;
  answers.push(selected);
  current++;

  if (current < questions.length) {
    showQuestion();
  } else {
    showResult();
  }
}

function showResult() {
  document.getElementById("quiz").classList.add("hidden");
  document.getElementById("result").classList.remove("hidden");

  const correct = answers.filter(
    (answer, i) => answer === questions[i].c
  ).length;

  document.getElementById("score").textContent =
    correct + " / " + questions.length;

  document.getElementById("percentage").textContent =
    "Таны зөв хариултын хувь: " + (correct*10) + "%";

  document.getElementById("message").textContent =
    correct >= 9 ? "Гайхалтай! 👏" :
    correct >= 7 ? "Маш сайн байна! 🌟" :
    correct >= 5 ? "Сайн оролцлоо! 😊" :
    "Дахин суралцаад оролдоорой! 💪";

  const review = document.getElementById("review");
  review.innerHTML = "<h3>Хариултын тайлбар</h3>";

  questions.forEach((item, i) => {
    const div = document.createElement("div");
    div.className = "review";

    const ok = answers[i] === item.c;
    div.textContent =
      (i+1) + ". " + (ok ? "✓ Зөв" : "✗ Буруу") +
      " — Зөв хариулт: " + item.a[item.c] +
      ". " + item.e;

    review.appendChild(div);
  });
}

function restart() {
  document.getElementById("result").classList.add("hidden");
  startQuiz();
}
</script>
</body>
</html># -.-
