<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <title>絶対に逆らってはいけない玉２４時</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      margin-top: 50px;
      background-color: #fff0f6; /* ピンクっぽい背景色 */
    }
    button {
      font-size: 18px;
      padding: 8px 16px;
      margin: 10px;
      cursor: pointer;
    }
    #playButton {
      font-size: 36px;
      background: none;
      border: none;
      cursor: pointer;
      margin-bottom: 30px;
      color: #e91e63;
    }
    h2 {
      margin-top: 30px;
      min-height: 3em;
    }
    #image {
      max-width: 80%;
      max-height: 400px;
      margin-top: 20px;
      display: none;
      opacity: 0;
      transition: opacity 0.5s ease;
      border-radius: 10px;
    }
    #image.show {
      display: block;
      opacity: 1;
    }
    #player {
      display: none;
    }
  </style>

  <!-- YouTube IFrame API -->
  <script src="https://www.youtube.com/iframe_api"></script>
</head>
<body>
  <h1>絶対に逆らってはいけない玉２４時</h1>

  <!-- BGMスタートボタン -->
  <button id="playButton">⋆͛📢 BGMスタート！</button>

  <!-- YouTubeプレイヤー -->
  <div id="player"></div>

  <!-- お題ガチャボタン -->
  <button onclick="draw()">挑戦する！</button>
  <h2 id="title">ここにお題が出るよ！</h2>
  <img id="image" src="" alt="挑戦イメージ" />

  <script>
    let player;
    function onYouTubeIframeAPIReady() {
      player = new YT.Player('player', {
        height: '0',
        width: '0',
        videoId: 'pLvJaU4vFrQ',
        playerVars: {
          autoplay: 0,
          loop: 1,
          playlist: 'pLvJaU4vFrQ',
          controls: 0,
          modestbranding: 1
        },
        events: {
          'onReady': onPlayerReady
        }
      });
    }

    function onPlayerReady(event) {
      document.getElementById('playButton').addEventListener('click', () => {
        event.target.playVideo();
        const btn = document.getElementById('playButton');
        btn.disabled = true;
        btn.innerText = "♪ BGM再生中";
      });
    }

    const data = [
      { title: "２４時間、語尾に「どすえ」を付けて過ごしなさい", img: "どすえ.png" },
      { title: "２４時間、人に話しかけるときにナンパ風でしか声をかけてはいけません", img: "チャラ男.png" },
      { title: "２４時間、名前を呼ばれるたびに名言を言いながら決めポーズをしなさい", img: "ふざけた.png" },
      { title: "２４時間、一人称を「麿（まろ）」にしなさい", img: "麿.png" },
      { title: "２４時間、エセ中国語でしか意思疎通を図ってはいけません", img: "チャラ.png" },
      { title: "２４時間、お嬢様言葉しか使ってはいけません", img: "お嬢様.png" },
      { title: "２４時間、「チョベリグ～」などの死語でしかリアクションしてはいけません", img: "チャラ.png" },
      { title: "２４時間、スマホの壁紙を自分の変顔にしなさい", img: "顔.png" },
      { title: "２４時間、鏡を見るたびに自分の美貌について３０秒間褒め称えなさい", img: "鏡.png" },
      { title: "２４時間、自分の行動を実況しながら過ごしなさい（例：「今、水を飲みます！」）", img: "実況.png" },
      { title: "２４時間、エセ関西弁でしか意思疎通を図ってはいけません", img: "チャラ.png" },
      { title: "２４時間、横文字以外の使用を禁止します", img: "チャラ男.png" },
      { title: "２４時間、Siriなどの音声認識できるものに「おいしいね♡」と声をかけながら食事しなさい", img: "箸.png" },
      { title: "２４時間、「王子」「姫」「勇者」「魔王」からひとつ選んで他人にその名称で呼ばれなさい", img: "お嬢様.png" },
      { title: "２４時間、小泉構文を使って話しなさい", img: "小泉.png" },
      { title: "２４時間、足音を立てるたびに10歩戻りなさい", img: "丸.png" },
      { title: "２４時間、スマホの明るさを一番低く設定して過ごしなさい", img: "顔.png" },
      { title: "２４時間、しりとりで会話しなさい", img: "チャラ.png" },
      { title: "２４時間、片手ピースで過ごしなさい", img: "ピース.png" },
      { title: "２４時間、扉をくぐるたびに「扉開けて」を歌いなさい", img: "歌う.png" },
      { title: "２４時間、YouTubeなどの広告を飛ばさずに全て見なさい", img: "リモート.png" },
      { title: "２４時間、通知がくるたびに5回スクワットしなさい", img: "ポーズ.png" },
      { title: "２４時間、手話っぽい手の動きをしながら会話しなさい", img: "チャラ男.png" },
      { title: "２４時間、何かあるたびに「これは伏線だな」といいなさい", img: "あご.png" },
      { title: "２４時間、ファンサをして過ごしなさい", img: "へい.png" },
      { title: "２４時間、固有名詞の使用禁止", img: "もの.png" },
      { title: "２４時間、ミッキーの声真似をして過ごしなさい", img: "ミッキー.png" },
      { title: "２４時間、立つときに毎回すごくかっこつけなさい", img: "疲労.png" },
      { title: "２４時間、LINEやインスタでおじさん構文を使いなさい", img: "ひげ.png" },
      { title: "２４時間、利き手とは逆の手を使って食事しなさい", img: "箸.png" }
    ];

    function draw() {
      const r = Math.floor(Math.random() * data.length);
      const t = data[r];
      const titleElem = document.getElementById('title');
      const imgElem = document.getElementById('image');

      titleElem.innerText = t.title;

      if (t.img) {
        imgElem.src = t.img;
        imgElem.classList.add('show');
      } else {
        imgElem.classList.remove('show');
        imgElem.src = "";
      }
    }
  </script>
</body>
</html>
