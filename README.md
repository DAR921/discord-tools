<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<title>أدوات ديسكورد</title>

<style>
body{
    margin:0;
    font-family:Arial;
    background:#0a0f1f;
    color:#e5e7eb;
    display:flex;
}

/* السايد بار */
.sidebar{
    width:70px;
    background:#020617;
    height:100vh;
    display:flex;
    flex-direction:column;
    align-items:center;
    padding-top:20px;
    gap:15px;
}

.icon{
    width:50px;
    height:50px;
    display:flex;
    align-items:center;
    justify-content:center;
    background:#1f2937;
    border-radius:12px;
    cursor:pointer;
    font-size:22px;
}

.icon:hover{
    background:#3b82f6;
}

/* المحتوى */
.main{
    flex:1;
    padding:20px;
}

.container{
    max-width:850px;
    margin:auto;
    background:linear-gradient(145deg,#0f172a,#0b1220);
    padding:20px;
    border-radius:16px;
    border:1px solid #334155;
}

/* الصفحات */
.page{ display:none; }
.page.active{ display:block; }

/* الشعار */
.logo{
    width:120px;
    height:120px;
    object-fit:cover;
    border-radius:50%;
    border:3px solid #22c55e;
    margin:auto;
    display:block;
    margin-bottom:10px;
}

/* عناصر */
input, textarea, select{
    width:100%;
    padding:10px;
    margin-top:5px;
    border-radius:10px;
    border:1px solid #334155;
    background:#0b1220;
    color:#fff;
}

button{
    margin-top:15px;
    padding:12px;
    width:100%;
    background:#16a34a;
    color:white;
    border:none;
    border-radius:10px;
    cursor:pointer;
}

.output{
    margin-top:20px;
    background:#0b1220;
    padding:15px;
    border-radius:10px;
    white-space:pre-wrap;
    border:1px solid #334155;
    min-height:80px;
}

.small-btn{
    background:#2563eb;
}

/* الحقوق */
.footer{
    text-align:center;
    margin-top:20px;
    padding:10px;
    font-size:14px;
    color:#94a3b8;
    border-top:1px solid #334155;
}
</style>
</head>

<body>

<!-- السايد بار -->
<div class="sidebar">
    <div class="icon" onclick="switchPage(1)">📢</div>
    <div class="icon" onclick="switchPage(2)">📋</div>
</div>

<div class="main">
<div class="container">

<!-- الصفحة 1 -->
<div id="page1" class="page active">

    <img src="https://up6.cc/2026/04/177679103446691.png" class="logo">

    <h2 style="text-align:center;">منشن ديسكورد</h2>

    <div id="inputs"></div>

    <button onclick="addInput()">➕ إضافة</button>
    <button onclick="copyMentions()">📋 نسخ</button>

    <div class="output" id="output1"></div>
</div>

<!-- الصفحة 2 -->
<div id="page2" class="page">

<div class="header">
    <img src="https://up6.cc/2026/04/177679103446691.png" class="logo">
    <h2 style="text-align:center;color:#22c55e;">رصد الترقيات - العاذرية</h2>
</div>

<label>الأسم (ID Discord):</label>
<input type="text" id="name" oninput="autoCopy()">

<label>عدد الأيام:</label>
<input type="number" id="days" oninput="autoCopy()">

<label>عدد تقارير العمليات:</label>
<input type="number" id="ops" oninput="autoCopy()">

<label>أمن 2:</label>
<input type="text" id="sec2" oninput="autoCopy()">

<label>عدد التقارير الميدانية:</label>
<input type="number" id="field" oninput="autoCopy()">

<label>اجتياز الدورات:</label>
<select id="courses" onchange="autoCopy()">
<option value="">-- اختر --</option>
<option value="صحيح">صحيح</option>
<option value="غير صحيح">غير صحيح</option>
</select>

<label>الرتبة الحالية:</label>
<input type="text" id="currentRank" oninput="autoCopy()">

<label>الرتبة المستحقة:</label>
<input type="text" id="nextRank" oninput="autoCopy()">

<label>ملاحظات:</label>
<textarea id="notes" oninput="autoCopy()"></textarea>

<div class="output" id="output2"></div>
<button class="small-btn" onclick="copyText()">نسخ مباشر</button>

</div>

<!-- الحقوق -->
<div class="footer">
    © 2026 جميع الحقوق محفوظة باسم DAR
</div>

</div>
</div>

<script>

/* التنقل */
function switchPage(num){
    document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
    document.getElementById("page"+num).classList.add("active");
}

/* المنشن */
let inputsContainer = document.getElementById("inputs");

for(let i=0;i<5;i++){
    addInput();
}

function addInput(){
    let input = document.createElement("input");
    input.placeholder = "ادخل ID ديسكورد";
    input.oninput = generateMentions;
    inputsContainer.appendChild(input);
}

function generateMentions(){
    let inputs = document.querySelectorAll("#page1 input");
    let result = "";

    inputs.forEach(input=>{
        if(input.value){
            result += `<@${input.value}>\n`;
        }
    });

    document.getElementById("output1").innerText = result;
}

function copyMentions(){
    navigator.clipboard.writeText(document.getElementById("output1").innerText);
    alert("تم النسخ");
}

/* الترقيات */
function buildText(){
    let id = document.getElementById('name').value.trim();
    let days = document.getElementById('days').value.trim();
    let ops = document.getElementById('ops').value.trim();
    let sec2 = document.getElementById('sec2').value.trim();
    let field = document.getElementById('field').value.trim();
    let courses = document.getElementById('courses').value.trim();
    let currentRank = document.getElementById('currentRank').value.trim();
    let nextRank = document.getElementById('nextRank').value.trim();
    let notes = document.getElementById('notes').value.trim();

    let text = `﷽\n\n`;

    if(id) text += `\`الأسم منشن :\` <@${id}>\n\n`;
    if(days) text += `\`عدد الأيام :\` ${days}\n\n`;
    if(ops) text += `\`عدد تقارير العمليات :\` ${ops}\n\n`;
    if(sec2) text += `\`أمن 2 :\` ${sec2}\n\n`;
    if(field) text += `\`عدد التقارير الميدانية :\` ${field}\n\n`;
    if(courses) text += `\`اجتياز الدورات :\` ${courses}\n\n`;
    if(currentRank) text += `\`الرتبة الحالية :\` ${currentRank}\n\n`;
    if(nextRank) text += `\`الرتبة المستحقة :\` ${nextRank}\n\n`;
    if(notes) text += `\`ملاحظات :\` ${notes}`;

    return text;
}

function autoCopy(){
    document.getElementById('output2').innerText = buildText();
}

function copyText(){
    navigator.clipboard.writeText(document.getElementById('output2').innerText);
    alert("تم النسخ بنجاح");
}

</script>

</body>
</html>
