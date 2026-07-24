let childName="おともだち";
const childNameInput=document.getElementById("childName");
if(childNameInput){
 childNameInput.addEventListener("input",()=>{childName=childNameInput.value.trim()||"おともだち";});
}

const steps = [
      {
        title: "こんにちは",
        text: "ふうせんを やさしく みせてね",
        spoken: "こんにちは。ふうせんを、あかちゃんに、やさしく、みせてみましょう。",
        motion: "float",
        duration: 9000,
        tone: 261.63
      },
      {
        title: "ゆらゆら",
        text: "みぎ・ひだりに ゆっくり ゆらしてね",
        spoken: "ふうせんを、みぎ、ひだりに、ゆっくり、ゆらしてみましょう。",
        motion: "sway",
        duration: 12000,
        tone: 293.66
      },
      {
        title: "うえ・した",
        text: "たかく、ひくく、ゆっくり うごかしてね",
        spoken: "ふうせんを、うえへ。つぎは、したへ。あかちゃんのようすを みながら、ゆっくり、うごかしましょう。",
        motion: "updown",
        duration: 12000,
        tone: 329.63
      },
      {
        title: "やさしく たっち",
        text: "てを そえて、そっと ふれてみよう",
        spoken: "あかちゃんの、てを、やさしく、そえて、ふうせんに、そっと、ふれてみましょう。",
        motion: "tap",
        duration: 11000,
        tone: 349.23
      },
      {
        title: "ぴたっ",
        text: "うごきを とめて、おかおを みてね",
        spoken: "ぴたっ。うごきを、とめて、あかちゃんの、おかおを、みてみましょう。",
        motion: "",
        duration: 9000,
        tone: 392.00
      },
      {
        title: "ばいばい",
        text: "ふうせんを ゆらして おしまい",
        spoken: "〇〇ちゃん、きょうも、たのしかったね。〇〇ちゃん、また、いっしょに、あそぼうね。ばいばい。",
        motion: "bye",
        duration: 10000,
        tone: 329.63
      }
    ];

    const startScreen = document.getElementById("startScreen");
    const playScreen = document.getElementById("playScreen");
    const endScreen = document.getElementById("endScreen");
    const startBtn = document.getElementById("startBtn");
    const againBtn = document.getElementById("againBtn");
    const muteBtn = document.getElementById("muteBtn");
    const titleEl = document.getElementById("stepTitle");
    const textEl = document.getElementById("stepText");
    const balloon = document.getElementById("balloon");
    const progress = document.getElementById("progress");
    const musicBoxBgm = document.getElementById("musicBoxBgm");

    let muted = false;
    let current = 0;
    let stepTimer = null;
    let raf = null;
    let audioCtx = null;
    let musicTimer = null;

    function show(screen) {
      [startScreen, playScreen, endScreen].forEach(s => s.classList.remove("active"));
      screen.classList.add("active");
    }

    function speak(text) {
      if (muted || !("speechSynthesis" in window)) return;
      speechSynthesis.cancel();
      const name = (typeof childName!=="undefined" && childName)?childName:"おともだち";
      const msg = text.replace(/あかちゃん/g,name).replace(/〇〇ちゃん/g,name);
      const u = new SpeechSynthesisUtterance(msg);
      u.lang="ja-JP";
      u.rate=0.62;
      u.pitch=0.88;
      u.volume=0.28;
      speechSynthesis.speak(u);
    }

    function initAudio() {
      if (!audioCtx) {
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
      }
      if (audioCtx.state === "suspended") audioCtx.resume();
    }

    function startMusic() {
      if (muted || !musicBoxBgm) return;
      musicBoxBgm.volume = 0.72;
      const p = musicBoxBgm.play();
      if (p && typeof p.catch === "function") p.catch(() => {});
    }

    function stopMusic() {
      if (!musicBoxBgm) return;
      musicBoxBgm.pause();
    }

    function setBalloonMotion(name) {
      balloon.className = "balloon";
      if (name) balloon.classList.add(name);
    }

    function runStep(index) {
      if (index >= steps.length) {
        finish();
        return;
      }

      current = index;
      const step = steps[index];
      titleEl.textContent = step.title;
      textEl.textContent = step.text;
      setBalloonMotion(step.motion);
      speak(step.spoken);
      startMusic();

      const started = performance.now();
      const total = step.duration;

      function update(now) {
        const elapsed = now - started;
        progress.style.width = Math.min(100, (elapsed / total) * 100) + "%";
        if (elapsed < total) raf = requestAnimationFrame(update);
      }

      cancelAnimationFrame(raf);
      progress.style.width = "0%";
      raf = requestAnimationFrame(update);

      clearTimeout(stepTimer);
      stepTimer = setTimeout(() => runStep(index + 1), total);
    }

    function begin() {
      if (musicBoxBgm) {
        musicBoxBgm.currentTime = 0;
        musicBoxBgm.volume = 0.72;
        musicBoxBgm.play().catch(() => {});
      }
      initAudio();
      show(playScreen);
      current = 0;
      runStep(0);
    }

    function finish() {
      clearTimeout(stepTimer);
      cancelAnimationFrame(raf);
      stopMusic();
      if ("speechSynthesis" in window) speechSynthesis.cancel();
      show(endScreen);
      if (!muted) {
        speak("〇〇ちゃん、きょうも、たのしかったね。〇〇ちゃん、また、いっしょに、あそぼうね。ばいばい。");

      }
    }

    startBtn.addEventListener("click", begin);
    againBtn.addEventListener("click", begin);

    muteBtn.addEventListener("click", () => {
      muted = !muted;
      muteBtn.textContent = muted ? "🔇" : "🔊";
      if (musicBoxBgm) {
        musicBoxBgm.muted = muted;
        if (!muted && playScreen.classList.contains("active")) startMusic();
      }

      muteBtn.setAttribute("aria-label", muted ? "おとを だす" : "おとを きる");

      if (muted) {
        stopMusic();
        if ("speechSynthesis" in window) speechSynthesis.cancel();
      } else if (playScreen.classList.contains("active")) {
        initAudio();
        const step = steps[current];
        speak(step.spoken);
        startMusic();
      }
    });

    document.addEventListener("visibilitychange", () => {
      if (document.hidden) {
        stopMusic();
        if ("speechSynthesis" in window) speechSynthesis.cancel();
      }
    });
  
/*
改良版BGM:
・子守歌をイメージしたゆったりした伴奏
・ピアノ＋やわらかいストリングス風
・高音のキーンとした音を使わない
・読み上げは小さめ、伴奏はやや大きめ
*/
