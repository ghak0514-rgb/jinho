
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>너를 위한 작은 선물 ♡</title>
<link href="https://fonts.googleapis.com/css2?family=Gowun+Dodum&family=Nanum+Myeongjo:wght@400;700&display=swap" rel="stylesheet">

<style>
* { box-sizing:border-box; }

body {
  margin:0;
  min-height:100vh;
  font-family:'Gowun Dodum',sans-serif;
  color:#75465c;
  background:linear-gradient(145deg,#ffe0ed,#fff4f8,#ffd9e9);
  overflow-x:hidden;
}

.screen {
  display:none;
  min-height:100vh;
  width:100%;
  padding:25px 16px;
  align-items:center;
  justify-content:center;
  flex-direction:column;
  text-align:center;
  position:relative;
}

.screen.active { display:flex; }

.panel {
  width:min(100%,440px);
  padding:30px 23px;
  border:1px solid rgba(255,255,255,.9);
  border-radius:28px;
  background:rgba(255,255,255,.76);
  box-shadow:0 12px 35px rgba(190,100,140,.16);
  backdrop-filter:blur(8px);
  position:relative;
  z-index:2;
}

h1,h2 { font-family:'Nanum Myeongjo',serif; }
h1 { font-size:27px; line-height:1.5; }
p { line-height:1.8; }

input {
  width:100%;
  padding:15px;
  margin:10px 0;
  border:1px solid #f1bfd2;
  border-radius:14px;
  outline:none;
  background:#fffafd;
  font-family:inherit;
  font-size:16px;
  color:#75465c;
}

button {
  border:none;
  border-radius:30px;
  padding:13px 25px;
  margin:7px;
  background:linear-gradient(135deg,#ff9fc5,#ed78a8);
  color:white;
  font-family:inherit;
  font-size:16px;
  cursor:pointer;
  box-shadow:0 5px 13px rgba(220,100,150,.2);
  transition:.2s;
}

button:active { transform:scale(.96); }

button:disabled {
  background:#bdbdbd !important;
  color:white;
  box-shadow:none;
  cursor:not-allowed;
  transform:none;
}

.small-text { font-size:13px; color:#a77b90; }

.cloud {
  position:fixed;
  width:130px;
  height:45px;
  border-radius:50px;
  background:rgba(255,255,255,.55);
  z-index:0;
  pointer-events:none;
}

.cloud::before,.cloud::after {
  content:"";
  position:absolute;
  background:inherit;
  border-radius:50%;
}

.cloud::before {
  width:55px;
  height:55px;
  top:-23px;
  left:20px;
}

.cloud::after {
  width:65px;
  height:65px;
  top:-30px;
  right:15px;
}

.cloud.one { top:12%; left:-35px; }
.cloud.two { bottom:13%; right:-35px; transform:scale(.8); }

.heart {
  position:fixed;
  color:rgba(255,130,175,.35);
  font-size:23px;
  animation:float 5s ease-in-out infinite;
  pointer-events:none;
  z-index:0;
}

@keyframes float {
  0%,100% { transform:translateY(0) rotate(-8deg); }
  50% { transform:translateY(-18px) rotate(8deg); }
}

.question-buttons {
  display:flex;
  flex-wrap:wrap;
  justify-content:center;
}

#errorScreen {
  position:fixed;
  inset:0;
  z-index:100;
  background:#050505;
  color:#ff1010;
  overflow:hidden;
}

.error-grid {
  width:100%;
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:18px 8px;
  font-size:clamp(18px,5vw,30px);
  font-weight:900;
  text-shadow:3px 0 red,-3px 0 #8b0000;
  animation:glitch .08s infinite;
}

@keyframes glitch {
  0% { transform:translate(2px,0); }
  25% { transform:translate(-3px,2px); }
  50% { transform:translate(2px,-2px); }
  75% { transform:translate(-2px,1px); }
  100% { transform:translate(1px,-1px); }
}

.gift-list {
  display:flex;
  flex-direction:column;
  gap:20px;
  align-items:center;
  margin-top:20px;
}

.gift-item {
  width:100%;
  max-width:310px;
  padding:19px;
  background:rgba(255,255,255,.85);
  border:1px solid #f7c8dc;
  border-radius:23px;
  box-shadow:0 8px 22px rgba(180,100,130,.12);
}

.gift-item.hidden { display:none; }

.gift-box {
  width:125px;
  height:110px;
  margin:10px auto 17px;
  position:relative;
  cursor:pointer;
}

.gift-base {
  position:absolute;
  width:110px;
  height:72px;
  left:7px;
  bottom:0;
  border-radius:8px;
  background:linear-gradient(135deg,#ffb2d0,#f27eaa);
}

.gift-lid {
  position:absolute;
  width:125px;
  height:27px;
  left:0;
  top:20px;
  border-radius:7px;
  background:linear-gradient(135deg,#ffd1e3,#f58db7);
  z-index:2;
}

.gift-ribbon {
  position:absolute;
  width:17px;
  height:92px;
  left:54px;
  top:20px;
  background:#ffe4a3;
  z-index:3;
}

.gift-bow {
  position:absolute;
  top:0;
  left:42px;
  font-size:35px;
  z-index:4;
}

.gift-caption {
  font-size:13px;
  line-height:1.8;
  color:#a16d83;
  white-space:pre-line;
}

.gift-item h3 { color:#d66d9a; }

.modal {
  display:none;
  position:fixed;
  inset:0;
  z-index:50;
  background:rgba(75,35,55,.45);
  align-items:center;
  justify-content:center;
  padding:18px;
}

.modal.active { display:flex; }

.modal-box {
  width:min(100%,410px);
  max-height:90vh;
  overflow-y:auto;
  padding:27px 22px;
  background:#fffafd;
  border:2px solid #f8c6d9;
  border-radius:25px;
  box-shadow:0 12px 40px rgba(70,20,45,.2);
  text-align:center;
}

.letter-paper {
  background:#fffaf0;
  border:1px solid #ead8bd;
  padding:23px 18px;
  border-radius:12px;
  text-align:left;
  line-height:2;
  color:#765c4d;
  white-space:pre-line;
  font-family:'Nanum Myeongjo',serif;
}

.read-check {
  display:flex;
  align-items:center;
  justify-content:center;
  gap:9px;
  margin:20px 0;
  font-size:15px;
  color:#a45e7d;
  cursor:pointer;
}

.read-check input {
  width:20px;
  height:20px;
  margin:0;
  accent-color:#ed78a8;
}

.final-heart {
  font-size:75px;
  animation:float 3s ease-in-out infinite;
}

.final-message {
  font-family:'Nanum Myeongjo',serif;
  font-size:25px;
  line-height:1.8;
  color:#d45f91;
  font-weight:bold;
}

#countdown {
  font-size:48px;
  color:#e36d9c;
}
</style>
</head>

<body>

<div class="cloud one"></div>
<div class="cloud two"></div>
<div class="heart" style="top:20%;left:12%">♡</div>
<div class="heart" style="top:70%;right:12%;animation-delay:1s">♡</div>
<div class="heart" style="top:45%;right:8%;animation-delay:2s">✧</div>
<div class="heart" style="bottom:10%;left:18%;animation-delay:1.5s">♡</div>

<!-- 로그인 -->
<section class="screen active" id="loginScreen">
  <div class="panel">
    <div style="font-size:55px">💗</div>
    <h1>특별한 사람만을 위한 공간</h1>
    <p>특별한 사람만 들어올 수 있어요.</p>
    <input id="mainPassword" type="password" placeholder="암호를 입력하세요">
    <p class="small-text">암호를 얻는 법: 진호에게 전화를 하라.</p>
    <button onclick="login()">입력</button>
    <p id="loginMessage" class="small-text"></p>
  </div>
</section>

<!-- 첫 번째 질문 -->
<section class="screen" id="question1">
  <div class="panel">
    <div style="font-size:50px">💕</div>
    <h1>당신은 저를 사랑합니까?</h1>
    <div class="question-buttons">
      <button onclick="chooseAnswer(1)">너무너무 사랑해요❤️💋</button>
      <button id="choice2" onclick="chooseAnswer(2)">엄</button>
      <button id="choice3" onclick="chooseAnswer(3)">아니요</button>
    </div>
  </div>
</section>

<!-- 두 번째 질문 -->
<section class="screen" id="question2">
  <div class="panel">
    <div style="font-size:50px">💞</div>
    <h1>진짜입니까?</h1>
    <div class="question-buttons">
      <button onclick="showScreen('giftScreen')">예 ♡</button>
      <button id="noButton" onclick="showError()">아니요</button>
    </div>
    <p>진심으로 대답해줘 ♡</p>
  </div>
</section>

<!-- BEEN 화면 -->
<section class="screen" id="angryScreen">
  <div class="panel">
    <div style="font-size:85px">😡</div>
    <h1>BEEN</h1>
    <button onclick="restartAfterAngry()">다시 하기</button>
  </div>
</section>

<!-- 60초 대기 화면 -->
<section class="screen" id="hateScreen">
  <div class="panel">
    <div style="font-size:75px">😢</div>
    <h1>너 미워...😢</h1>
    <p>잠깐만 기다려 줘...</p>
    <h2 id="countdown">60</h2>
    <button id="retryButton" onclick="restartAfterWait()" disabled>
      60초 기다려 줘
    </button>
  </div>
</section>

<!-- 에러 화면 -->
<section class="screen" id="errorScreen">
  <div class="error-grid" id="errorGrid"></div>
</section>

<!-- 선물 화면 -->
<section class="screen" id="giftScreen">
  <div class="panel">
    <div style="font-size:45px">🎀</div>
    <h1>너를 위한 작은 선물</h1>
    <p style="letter-spacing:3px;font-size:12px;color:#d77ba1">
      THREE LITTLE GIFTS FOR YOU ♡
    </p>

    <div class="gift-list">

      <div class="gift-item" id="giftItem1">
        <h3>첫 번째 선물</h3>
        <div class="gift-box" onclick="openPassword(1)">
          <div class="gift-bow">🎀</div>
          <div class="gift-lid"></div>
          <div class="gift-base"></div>
          <div class="gift-ribbon"></div>
        </div>
        <div class="gift-caption">남은 선물 2개!
암호를 얻는 방법:
진호에게 부를 때 진호야 말고 자기야로 부르기</div>
        <button onclick="openPassword(1)">선물 열기</button>
      </div>

      <div class="gift-item hidden" id="giftItem2">
        <h3>두 번째 선물</h3>
        <div class="gift-box" onclick="openPassword(2)">
          <div class="gift-bow">🎀</div>
          <div class="gift-lid"></div>
          <div class="gift-base"></div>
          <div class="gift-ribbon"></div>
        </div>
        <div class="gift-caption">남은 선물 1개!
암호를 얻는 방법:
진호 칭찬하기</div>
        <button onclick="openPassword(2)">선물 열기</button>
      </div>

      <div class="gift-item hidden" id="giftItem3">
        <h3>마지막 선물</h3>
        <div class="gift-box" onclick="openPassword(3)">
          <div class="gift-bow">💝</div>
          <div class="gift-lid"></div>
          <div class="gift-base"></div>
          <div class="gift-ribbon"></div>
        </div>
        <div class="gift-caption">내 진심이 담긴 편지
암호를 얻는 방법:
전화로 사랑한다고 말하기</div>
        <button onclick="openPassword(3)">편지 열기</button>
      </div>

    </div>
  </div>
</section>

<!-- 선물 암호 -->
<div class="modal" id="passwordModal">
  <div class="modal-box">
    <div style="font-size:45px">🔐</div>
    <h2>선물 상자 암호</h2>
    <input type="password" id="giftPassword" placeholder="암호를 입력하세요">
    <p id="giftPasswordMessage" class="small-text"></p>
    <button onclick="checkGiftPassword()">확인</button>
    <button onclick="closeModal('passwordModal')" style="background:#c9a9b8">닫기</button>
  </div>
</div>

<!-- 첫 번째 선물 -->
<div class="modal" id="giftOneModal">
  <div class="modal-box">
    <div style="font-size:65px">🎁</div>
    <h2>빼빼로 당첨!</h2>
    <p>얻는 방법:<br>진호야 나 빼빼로 좀 줄수있어?라고 말하기</p>
    <button onclick="closeGiftReward(1)">확인했어 ♡</button>
  </div>
</div>

<!-- 두 번째 선물 -->
<div class="modal" id="giftTwoModal">
  <div class="modal-box">
    <div style="font-size:65px">🎁</div>
    <h2>GS25 3000권 당첨!</h2>
    <p>얻는 방법:<br>진호야 나 상품권 줄수있어? 라고 말하기</p>
    <button onclick="closeGiftReward(2)">확인했어 ♡</button>
  </div>
</div>

<!-- 마지막 편지 -->
<div class="modal" id="letterModal">
  <div class="modal-box">
    <div id="envelopeView">
      <div style="font-size:75px">💌</div>
      <h2>너에게 전하는 편지</h2>
      <p>마지막 선물 안에 편지가 들어 있어.</p>
      <button onclick="openLetter()">편지 열기</button>
    </div>

    <div id="letterView" style="display:none">
      <div class="letter-paper">♡ 너에게 전하는 편지 ♡

내가 가끔 서툴거나 부족한 모습을 보여도 예쁘게 봐줬으면 좋겠어. 나도 너에게 더 잘하고, 항상 아껴 주고 사랑해 줄게.

앞으로 서로 서운한 일이 생기더라도 대화하면서 잘 풀어 가고, 좋은 일도 힘든 일도 함께 나누면서 오래오래 잘 지내 보자.

너와 함께할 앞으로의 시간이 정말 기대돼.

내 곁에 있어 줘서 고맙고, 앞으로도 잘 부탁해.

많이 많이 사랑해 💗💋</div>

      <label class="read-check">
        <input type="checkbox" id="letterReadCheck" onchange="updateCloseButton()">
        다 읽으셨습니까?
      </label>

      <button id="letterCloseButton" onclick="finishLetter()" disabled>
        닫기
      </button>
    </div>
  </div>
</div>

<!-- 마지막 화면 -->
<section class="screen" id="finalScreen">
  <div class="panel">
    <div class="final-heart">💗</div>
    <div class="final-message">끝까지 해줘서 고맙고 항상 사랑해❤️</div>
    <p style="color:#bd7896">여기까지 함께해 줘서 고마워.</p>
    <button onclick="exitApp()">나가기</button>
  </div>
</section>

<script>
const giftPasswords = {
  1:"자기야",
  2:"0504",
  3:"사랑해"
};

let passwordTarget = 0;
let currentGift = 0;
let errorTimer = null;

let deletedChoices = [];
let selectedChoice = null;
let waitTimer = null;
let remainingSeconds = 60;

function showScreen(id) {
  document.querySelectorAll(".screen").forEach(screen => {
    screen.classList.remove("active");
  });

  document.getElementById(id).classList.add("active");
}

function login() {
  const password = document.getElementById("mainPassword").value;

  if (password === "0514") {
    document.getElementById("loginMessage").textContent = "";
    showScreen("question1");
  } else {
    document.getElementById("loginMessage").textContent = "암호가 틀렸어!";
  }
}

/* 첫 번째 질문 선택 */
function chooseAnswer(number) {
  if (number === 1) {
    resetChoices();
    showScreen("question2");
    return;
  }

  if (deletedChoices.includes(number)) return;

  selectedChoice = number;

  if (deletedChoices.length === 0) {
    showScreen("angryScreen");
  } else {
    showScreen("hateScreen");
    startWait();
  }
}

/* BEEN 화면에서 다시 하기 */
function restartAfterAngry() {
  if (selectedChoice !== null &&
      !deletedChoices.includes(selectedChoice)) {
    deletedChoices.push(selectedChoice);
  }

  selectedChoice = null;
  updateChoices();
  showScreen("question1");
}

/* 60초 대기 */
function startWait() {
  clearInterval(waitTimer);
  remainingSeconds = 60;

  document.getElementById("countdown").textContent = 60;

  const button = document.getElementById("retryButton");
  button.disabled = true;
  button.textContent = "60초 기다려 줘";

  waitTimer = setInterval(() => {
    remainingSeconds--;

    document.getElementById("countdown").textContent =
      remainingSeconds;

    button.textContent = remainingSeconds + "초 기다려 줘";

    if (remainingSeconds <= 0) {
      clearInterval(waitTimer);
      waitTimer = null;
      button.disabled = false;
      button.textContent = "처음부터 다시 하기";
    }
  }, 1000);
}

function restartAfterWait() {
  if (remainingSeconds > 0) return;

  clearInterval(waitTimer);
  waitTimer = null;

  if (selectedChoice !== null &&
      !deletedChoices.includes(selectedChoice)) {
    deletedChoices.push(selectedChoice);
  }

  selectedChoice = null;
  updateChoices();
  showScreen("question1");
}

/* 선택지 삭제 및 복구 */
function updateChoices() {
  document.getElementById("choice2").style.display =
    deletedChoices.includes(2) ? "none" : "";

  document.getElementById("choice3").style.display =
    deletedChoices.includes(3) ? "none" : "";
}

function resetChoices() {
  clearInterval(waitTimer);
  waitTimer = null;

  remainingSeconds = 60;
  deletedChoices = [];
  selectedChoice = null;

  document.getElementById("countdown").textContent = "60";

  const button = document.getElementById("retryButton");
  button.disabled = true;
  button.textContent = "60초 기다려 줘";

  updateChoices();
}

/* 두 번째 질문의 ERROR 화면 */
function showError() {
  const grid = document.getElementById("errorGrid");
  grid.innerHTML = "";

  for (let i = 0; i < 27; i++) {
    const item = document.createElement("div");
    item.textContent = "ERROR";
    grid.appendChild(item);
  }

  showScreen("errorScreen");

  if (errorTimer) clearTimeout(errorTimer);

  errorTimer = setTimeout(() => {
    const noButton = document.getElementById("noButton");
    if (noButton) noButton.remove();

    showScreen("question2");
    errorTimer = null;
  }, 2000);
}

/* 처음부터 다시 시작 */
function restartApp() {
  location.reload();
}

/* 선물상자 */
function openPassword(number) {
  if (number !== currentGift + 1) return;

  passwordTarget = number;
  document.getElementById("giftPassword").value = "";
  document.getElementById("giftPasswordMessage").textContent = "";
  document.getElementById("passwordModal").classList.add("active");
}

function checkGiftPassword() {
  const password = document.getElementById("giftPassword").value;

  if (password !== giftPasswords[passwordTarget]) {
    document.getElementById("giftPasswordMessage").textContent =
      "암호가 틀렸습니다.";
    return;
  }

  closeModal("passwordModal");
  openGift(passwordTarget);
}

function openGift(number) {
  if (number !== currentGift + 1) return;

  const item = document.getElementById("giftItem" + number);
  if (!item) return;

  item.remove();
  currentGift = number;

  if (number === 1) {
    document.getElementById("giftOneModal").classList.add("active");
  } else if (number === 2) {
    document.getElementById("giftTwoModal").classList.add("active");
  } else if (number === 3) {
    document.getElementById("letterModal").classList.add("active");
  }
}

function closeGiftReward(number) {
  if (number === 1) {
    closeModal("giftOneModal");
    document.getElementById("giftItem2").classList.remove("hidden");
  }

  if (number === 2) {
    closeModal("giftTwoModal");
    document.getElementById("giftItem3").classList.remove("hidden");
  }
}

/* 편지 */
function openLetter() {
  document.getElementById("envelopeView").style.display = "none";
  document.getElementById("letterView").style.display = "block";

  document.getElementById("letterReadCheck").checked = false;
  updateCloseButton();
}

function updateCloseButton() {
  const checked = document.getElementById("letterReadCheck").checked;
  const button = document.getElementById("letterCloseButton");

  button.disabled = !checked;

  if (checked) {
    button.style.background =
      "linear-gradient(135deg,#ff9fc5,#ed78a8)";
    button.style.cursor = "pointer";
    button.style.boxShadow =
      "0 5px 13px rgba(220,100,150,.2)";
  } else {
    button.style.background = "#bdbdbd";
    button.style.cursor = "not-allowed";
    button.style.boxShadow = "none";
  }
}

function finishLetter() {
  if (!document.getElementById("letterReadCheck").checked) return;

  closeModal("letterModal");
  showScreen("finalScreen");
}

function closeModal(id) {
  document.getElementById(id).classList.remove("active");
}

/* 나가기 */
function exitApp() {
  location.reload();
}
</script>

</body>
</html>
