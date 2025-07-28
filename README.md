
<html lang="zh-TW">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400..700;1,400..700&display=swap"
      rel="stylesheet"
    />

    <title>今天，我想要來看...</title>
    <style>
      body {
        font-family: 'Poppins', sans-serif;
        padding: 40px 20px;
        min-height: 100vh;
        /* Changed background to a much lighter orange-yellow gradient */
        background: linear-gradient(135deg, #fffde7 0%, #ffe0b2 100%); /* Very Light Yellow to Light Orange */
        background-attachment: fixed;
        margin: 0 auto;
        max-width: 800px;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        align-items: center;
      }
      h1 {
        text-align: center;
        /* Keeping contrasting dark brown color */
        color: #795548; /* Brown */
        margin-bottom: 40px;
        font-weight: 700;
        /* Text shadow should work fine on lighter background */
        text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.15);
        font-size: 2.5em;
      }

      #wheelContainer {
        position: relative;
        width: 400px;
        height: 400px;
        margin-bottom: 40px;
        border-radius: 50%;
        overflow: hidden;
        /* Adjusted box shadow */
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1); /* Slightly softer shadow */
        /* Changed background color (will be mostly covered by segments) */
        background-color: #fff8e1; /* Palest Yellow */
        /* Keeping darker brown border for contrast */
        border: 8px solid #5d4037; /* Dark Brown */
        margin-left: auto;
        margin-right: auto;
      }

      #wheelSVG {
        width: 100%;
        height: 100%;
        viewBox="0 0 400 400";
      }

      #wheel {
        transform-origin: 50% 50%;
        transition: transform 5s cubic-bezier(0.25, 0.1, 0.25, 1);
      }

      .segment {
        /* Keeping white stroke for visibility */
        stroke: #fff;
        stroke-width: 1;
      }

      #pointer {
        position: absolute;
        top: -20px;
        left: 50%;
        transform: translateX(-50%);
        width: 0;
        height: 0;
        border-left: 20px solid transparent;
        border-right: 20px solid transparent;
        /* Changed pointer color to a less intense orange */
        border-top: 30px solid #ff8a65; /* Deep Orange 300 */
        z-index: 10;
      }

      #drawBtn {
        display: block;
        margin: 20px auto 0;
        padding: 15px 40px;
        font-size: 1.3em;
        /* Changed button colors to a lighter orange */
        background-color: #ffb74d; /* Orange 300 */
        color: #fff; /* White */
        border: none;
        border-radius: 30px;
        cursor: pointer;
        transition: all 0.3s ease;
        /* Adjusted box shadow color */
        box-shadow: 0 4px 15px rgba(255, 183, 77, 0.4);
        font-weight: 600;
      }
      #drawBtn:hover:not(:disabled) {
        transform: translateY(-2px);
        /* Slightly darker shade on hover */
        background-color: #ff8a65; /* Deep Orange 300 */
        /* Adjusted box shadow color on hover */
        box-shadow: 0 6px 20px rgba(255, 138, 101, 0.5);
      }
      #drawBtn:disabled {
        opacity: 0.6;
        cursor: not-allowed;
      }

      #winner {
        margin: 40px auto;
        padding: 25px;
        width: 80%;
        max-width: 600px;
        /* Keeping light background for readability */
        background-color: rgba(255, 255, 255, 0.95);
        border-radius: 15px;
        text-align: center;
        font-size: 1.6em;
        /* Keeping dark brown winner text color */
        color: #795548; /* Brown */
        font-weight: 600;
        /* Adjusted box shadow */
        box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08); /* Slightly softer shadow */
        /* Changed border color to a very light yellow */
        border: 2px solid #fffde7; /* Very Light Yellow */
        min-height: 2em;
        display: flex;
        align-items: center;
        justify-content: center;
        opacity: 0;
        transition: opacity 0.5s ease-in-out;
        word-break: break-word;
      }

      #winner::before {
        /* Keeping the confetti emoji */
        content: "🎉";
        display: block;
        font-size: 2.5em;
        margin-bottom: 10px;
        margin-right: 10px;
      }
       #winner:empty::before {
        content: none;
        margin-bottom: 0;
        margin-right: 0;
      }

      #wheelSVG circle {
        fill: #fff; /* White center circle fill */
        /* Changed stroke color to a lighter gold */
        stroke: #ffda6d; /* Amber 300 */
        stroke-width: 4;
      }
      /* Footer link styles (adjusted colors) */
      .footer-links {
        margin-top: 40px;
        text-align: center;
        /* Keeping dark brown footer text color */
        color: #795548; /* Brown */
        font-size: 0.9em;
        width: 100%;
      }

      .footer-links p {
        margin-bottom: 5px;
      }

      .footer-links a {
        /* Changed link color to a medium light orange/gold */
        color: #ffb74d; /* Orange 300 */
        text-decoration: none;
        margin: 0 10px;
        transition: color 0.3s ease;
      }

      .footer-links a:hover {
        color: #fff; /* White on hover */
        text-decoration: underline;
      }

      .footer-links span {
        /* Keeping separator color to match text */
        color: #795548; /* Brown */
      }

      /* --- Mobile Specific Styles --- */
      @media (max-width: 500px) {
        body {
          padding: 20px 10px;
        }

        h1 {
          font-size: 2em;
          margin-bottom: 20px;
        }

        #wheelContainer {
          width: 85vw;
          height: 85vw;
          max-width: 350px;
          max-height: 350px;
          margin-bottom: 20px;
          border-width: 4px;
        }

        #pointer {
          top: -15px;
          border-left-width: 15px;
          border-right-width: 15px;
          border-top-width: 25px;
        }

        #drawBtn {
          padding: 12px 30px;
          font-size: 1.2em;
        }

        #winner {
          width: 95%;
          padding: 15px;
          font-size: 1.3em;
          margin-top: 20px;
          margin-bottom: 20px;
        }

        #winner::before {
          font-size: 2em;
          margin-bottom: 5px;
          margin-right: 8px;
        }
      }

      /* Optional: Styles for even smaller screens */
      @media (max-width: 320px) {
        h1 {
          font-size: 1.8em;
        }
        #wheelContainer {
          width: 90vw;
          height: 90vw;
        }
        #pointer {
          top: -10px;
          border-left-width: 10px;
          border-right-width: 10px;
          border-top-width: 20px;
        }
        #drawBtn {
          padding: 10px 20px;
          font-size: 1.1em;
        }
        #winner {
          font-size: 1.1em;
          padding: 10px;
        }
         #winner::before {
          font-size: 1.8em;
          margin-bottom: 3px;
           margin-right: 5px;
        }
      }
    </style>
  </head>
  <body>
    <h1>🕶️今天是哪集GOING勒？</h1>

    <div id="wheelContainer">
      <div id="pointer"></div>
      <svg id="wheelSVG" viewBox="0 0 400 400">
        <g id="wheel"></g>
        <circle cx="200" cy="200" r="30" fill="#fff" stroke="#ffda6d" /* Lighter
        Golden color */ stroke-width="4" />
      </svg>
    </div>

    <button id="drawBtn">走吧 가자！</button>
    <div id="winner"></div>

    <div class="footer-links">
      <a
        href="https://www.instagram.com/svt._.230204/?hl=zh-tw"
        target="_blank"
        rel="noopener noreferrer"
        >@svt._.230204</a
      >
      <span>|</span>
      <a
        href="https://www.instagram.com/_ccni7/?hl=zh-tw"
        target="_blank"
        rel="noopener noreferrer"
        >@_ccni7</a
      >
    </div>

    <script>
      const participants = [
        "GOING SEVENTEEN 2017 EP.0 Prologue",
        "GOING SEVENTEEN 2017 EP.1",
        "GOING SEVENTEEN 2017 EP.2",
        "GOING SEVENTEEN 2017 EP.3",
        "GOING SEVENTEEN 2017 EP.4",
        "GOING SEVENTEEN 2017 EP.5",
        "GOING SEVENTEEN 2017 EP.6",
        "GOING SEVENTEEN 2017 EP.7",
        "GOING SEVENTEEN 2017 EP.8",
        "GOING SEVENTEEN 2017 EP.9",
        "GOING SEVENTEEN 2017 EP.10",
        "GOING SEVENTEEN 2017 EP.11",
        "GOING SEVENTEEN 2017 EP.12",
        "GOING SEVENTEEN 2017 EP.13",
        "GOING SEVENTEEN 2017 EP.14",
        "GOING SEVENTEEN 2017 EP.15",
        "GOING SEVENTEEN 2017 EP.16",
        "GOING SEVENTEEN 2017 EP.17",
        "GOING SEVENTEEN 2017 EP.18",
        "GOING SEVENTEEN 2017 EP.19",
        "GOING SEVENTEEN 2017 EP.20",
        "GOING SEVENTEEN 2017 EP.21",
        "GOING SEVENTEEN 2017 EP.22",
        "GOING SEVENTEEN 2017 EP.23",
        "GOING SEVENTEEN 2017 EP.24",
        "GOING SEVENTEEN 2017 EP.25",
        "GOING SEVENTEEN 2017 EP.26",
        "GOING SEVENTEEN 2017 EP.27",
        "GOING SEVENTEEN 2017 EP.28",
        "GOING SEVENTEEN 2017 EP.29",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.1",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.2",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.3",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.4",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.5",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.6",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.7",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.8",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.9",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.10",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.11",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.12",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.13",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.14",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.15",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.16",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.17",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.18",
        "GOING SEVENTEEN 2018 EP.19",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.20",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.21 TTT #1",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.22 TTT #2",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.23 TTT #3",
        "GOING SEVENTEEN 2018 SPIN-OFF EP.24",
        "GOING SEVENTEEN 2019 EP.1",
        "GOING SEVENTEEN 2019 EP.2",
        "GOING SEVENTEEN 2019 EP.3",
        "GOING SEVENTEEN 2019 EP.4 GOING公司新職員入職",
        "GOING SEVENTEEN 2019 EP.5",
        "GOING SEVENTEEN 2019 EP.6 GOING主題曲製作",
        "GOING SEVENTEEN 2019 EP.7 主題曲MV拍攝",
        "GOING SEVENTEEN 2019 EP.8",
        "GOING SEVENTEEN 2019 EP.9",
        "GOING SEVENTEEN 2019 EP.10 當.當.感.體 #1",
        "GOING SEVENTEEN 2019 EP.11 當.當.感.體 #2",
        "GOING SEVENTEEN 2019 EP.12 SVT TRIP #1",
        "GOING SEVENTEEN 2019 EP.13 SVT TRIP #2",
        "GOING SEVENTEEN 2019 EP.14 MBTI of SVT #1",
        "GOING SEVENTEEN 2019 EP.15 MBTI of SVT #2",
        "GOING SEVENTEEN 2019 EP.16 MBTI of SVT #3",
        "GOING SEVENTEEN 2019 EP.17 逃出KTV #1",
        "GOING SEVENTEEN 2019 EP.18 逃出KTV #2",
        "GOING SEVENTEEN 2019 EP.19 邏輯之夜 #1",
        "GOING SEVENTEEN 2019 EP.20 邏輯之夜 #2",
        "GOING SEVENTEEN 2019 EP.21 TTT 露營篇 #1",
        "GOING SEVENTEEN 2019 EP.22 TTT 露營篇 #2",
        "GOING SEVENTEEN 2019 EP.23 TTT 露營篇 #3",
        "GOING SEVENTEEN 2019 EP.24 SVT 遊樂場 #1",
        "GOING SEVENTEEN 2019 EP.25 SVT 遊樂場 #2",
        "GOING SEVENTEEN 2019 EP.26 SVT 祕密聖誕老人",
        "GOING SEVENTEEN 2019 TTT 露營篇存貨清理",
        "GOING SEVENTEEN 2019 EP.27 月刊SVT企劃會議 #1",
        "GOING SEVENTEEN 2019 EP.28 月刊SVT企劃會議 #2",
        "GOING SEVENTEEN 2020 EP.1 MYSTERY MYSTERY #1",
        "GOING SEVENTEEN 2020 EP.2 MYSTERY MYSTERY #2",
        "GOING SEVENTEEN 2020 EP.3 Don't Lie #1",
        "GOING SEVENTEEN 2020 EP.4 Don't Lie #2",
        "GOING SEVENTEEN 2020 EP.5 夫勝寛的前生緣分 #1",
        "GOING SEVENTEEN 2020 EP.6 夫勝寛的前生緣分 #2",
        "GOING SEVENTEEN 2020 EP.7 夫勝寛的前生緣分 #3",
        "GOING SEVENTEEN 2020 EP.8 不眠之夜 #1",
        "GOING SEVENTEEN 2020 EP.9 不眠之夜 #2",
        "GOING SEVENTEEN 2020 EP.10 SVT大腦生存戰 #1",
        "GOING SEVENTEEN 2020 EP.11 SVT大腦生存戰 #2",
        "GOING SEVENTEEN 2020 EP.12 SVT密室逃脫 #1",
        "GOING SEVENTEEN 2020 EP.13 SVT密室逃脫 #2",
        "GOING SEVENTEEN 2020 EP.14 DeFoFi #1",
        "GOING SEVENTEEN 2020 EP.15 DeFoFi #2",
        "GOING SEVENTEEN 2020 EP.16 人體國際象棋 #1",
        "GOING SEVENTEEN 2020 EP.17 人體國際象棋 #2",
        "GOING SEVENTEEN 2020 EP.18 邏輯之夜Ⅱ #1",
        "GOING SEVENTEEN 2020 EP.19 邏輯之夜Ⅱ #2",
        "GOING SEVENTEEN 2020 EP.20 象棋懲罰聚餐",
        "GOING SEVENTEEN 2020 EP.21 跑跑卡丁車 #1",
        "GOING SEVENTEEN 2020 EP.22 跑跑卡丁車 #2",
        "GOING SEVENTEEN 2020 EP.23 SVT的才藝選秀 #1",
        "GOING SEVENTEEN 2020 EP.24 SVT的才藝選秀 #2",
        "GOING SEVENTEEN 2020 EP.25 小八和他的十二個影子 #1",
        "GOING SEVENTEEN 2020 EP.26 小八和他的十二個影子 #2",
        "GOING SEVENTEEN 2020 EP.27 納涼特集-鬼抓人 #1",
        "GOING SEVENTEEN 2020 EP.28 納涼特集-鬼抓人 #2",
        "GOING SEVENTEEN 2020 EP.29 八月的聖誕節 #1",
        "GOING SEVENTEEN 2020 EP.30 八月的聖誕節 #2",
        "GOING SEVENTEEN 2020 EP.31 老鼠追擊戰 #1",
        "GOING SEVENTEEN 2020 EP.32 老鼠追擊戰 #2",
        "GOING SEVENTEEN 2020 EP.33 老鼠追擊戰 #3",
        "GOING SEVENTEEN 2020 EP.34 BAD CLUE #1",
        "GOING SEVENTEEN 2020 EP.35 BAD CLUE #2",
        "GOING SEVENTEEN 2020 EP.36 SVT SIDE OUT #1",
        "GOING SEVENTEEN 2020 EP.37 天高馬肥 #1",
        "GOING SEVENTEEN 2020 EP.38 天高馬肥 #2",
        "GOING SEVENTEEN 2020 EP.39 CARNIVAL",
        "GOING SEVENTEEN 2020 EP.40 Don't LieⅡ #1",
        "GOING SEVENTEEN 2020 EP.41 Don't LieⅡ #2",
        "GOING SEVENTEEN 2020 EP.42 GOING VS SEVENTEEN #1",
        "GOING SEVENTEEN 2020 EP.43 GOING VS SEVENTEEN #2",
        "GOING SEVENTEEN 2020 EP.44 TTT 超現實主義篇 #1",
        "GOING SEVENTEEN 2020 EP.45 TTT 超現實主義篇 #2",
        "GOING SEVENTEEN 2020 EP.46 GOING雜誌1.0 #1",
        "GOING SEVENTEEN 2020 EP.47 GOING雜誌1.0 #2",
        "GOING SEVENTEEN 2020 名場面獎項頒布",
        "GOING SEVENTEEN 2021 EP.1 GOING COMPANY #1",
        "GOING SEVENTEEN 2021 EP.2 GOING COMPANY #2",
        "GOING SEVENTEEN 2021 EP.3 ONE MILLION WON #1",
        "GOING SEVENTEEN 2021 EP.4 ONE MILLION WON #2",
        "GOING SEVENTEEN 2021 EP.5 出發SEVENTEEN！ #1",
        "GOING SEVENTEEN 2021 EP.6 出發SEVENTEEN！ #2",
        "GOING SEVENTEEN 2021 EP.7 無人島尋寶記 #1",
        "GOING SEVENTEEN 2021 EP.8 無人島尋寶記 #2",
        "GOING SEVENTEEN 2021 EP.9 Don't LieⅢ #1",
        "GOING SEVENTEEN 2021 EP.10 Don't LieⅢ #2",
        "GOING SEVENTEEN 2021 EP.11 廣告天才",
        "GOING SEVENTEEN 2021 EP.12 轉盤人生 #1",
        "GOING SEVENTEEN 2021 EP.13 轉盤人生 #2",
        "GOING SEVENTEEN 2021 EP.14 啵農田 #1",
        "GOING SEVENTEEN 2021 EP.15 啵農田 #2",
        "GOING SEVENTEEN 2021 EP.16 足壘球對決 #1",
        "GOING SEVENTEEN 2021 EP.17 足壘球對決 #2",
        "GOING SEVENTEEN 2021 EP.18 TTT-水上樂園篇 #1",
        "GOING SEVENTEEN 2021 EP.19 TTT-水上樂園篇 #2",
        "GOING SEVENTEEN 2021 EP.20 TTT-水上樂園篇 #3",
        "GOING SEVENTEEN 2021 EP.21 邏輯之夜Ⅲ #1",
        "GOING SEVENTEEN 2021 EP.22 邏輯之夜Ⅲ #2",
        "GOING SEVENTEEN 2021 EP.23 Boo族娛樂館 #1",
        "GOING SEVENTEEN 2021 EP.24 Boo族娛樂館 #2",
        "GOING SEVENTEEN 2021 EP.25 走口巴抓口巴 #1",
        "GOING SEVENTEEN 2021 EP.26 走口巴抓口巴 #2",
        "GOING SEVENTEEN 2021 EP.27 EGO #1",
        "GOING SEVENTEEN 2021 EP.28 EGO #2",
        "GOING SEVENTEEN 2021 EP.29 不眠之夜Ⅱ #1",
        "GOING SEVENTEEN 2021 EP.30 不眠之夜Ⅱ #2",
        "GOING SEVENTEEN 2021 EP.31 順應特輯 #1",
        "GOING SEVENTEEN 2021 EP.32 順應特輯 #2",
        "GOING SEVENTEEN 2021 EP.33 SEV食堂 #1",
        "GOING SEVENTEEN 2021 EP.34 SEV食堂 #2",
        "GOING SEVENTEEN 2021 EP.35 SEV食堂 #3",
        "GOING SEVENTEEN 2022 GOING名場面結算",
        "GOING SEVENTEEN 2022 EP.36 把白米飯吃得好吃的方法 #1",
        "GOING SEVENTEEN 2022 EP.37 把白米飯吃得好吃的方法 #2",
        "GOING SEVENTEEN 2022 EP.38 無挑SVT #1",
        "GOING SEVENTEEN 2022 EP.39 無挑SVT #2",
        "GOING SEVENTEEN 2022 EP.40 SVT先生之我獨自生活 #1",
        "GOING SEVENTEEN 2022 EP.41 SVT先生之我獨自生活 #2",
        "GOING SEVENTEEN 2022 EP.42 SVT SIDE OUTⅡ #1",
        "GOING SEVENTEEN 2022 EP.43 SVT SIDE OUTⅡ #2",
        "GOING SEVENTEEN 2022 EP.44 SVT電競比賽 #1",
        "GOING SEVENTEEN 2022 EP.45 SVT電競比賽 #2",
        "GOING SEVENTEEN 2022 EP.46 SVT電競比賽 #3",
        "GOING SEVENTEEN 2022 EP.47 JUN優勝運動會 #1",
        "GOING SEVENTEEN 2022 EP.48 JUN優勝運動會 #2",
        "GOING SEVENTEEN 2022 GOSE X 文明特輯 (可以去翻翻前面合作的兩集-夫心臟)",
        "GOING SEVENTEEN 2022 EP.49 GOING Radio Show #1",
        "GOING SEVENTEEN 2022 EP.50 GOING Radio Show #2",
        "GOING SEVENTEEN 2022 EP.51 認識你自己吧！ #1",
        "GOING SEVENTEEN 2022 EP.52 認識你自己吧！ #2",
        "GOING SEVENTEEN 2022 EP.53 HIDE N SEEK",
        "GOING SEVENTEEN 2022 EP.54 全圓佑日記 #1",
        "GOING SEVENTEEN 2022 EP.55 全圓佑日記 #2",
        "GOING SEVENTEEN 2022 EP.56 八月的聖誕節Ⅱ #1",
        "GOING SEVENTEEN 2022 EP.57 八月的聖誕節Ⅱ #2",
        "GOING SEVENTEEN 2022 EP.58 GOOD OFFER #1",
        "GOING SEVENTEEN 2022 EP.59 GOOD OFFER #2",
        "GOING SEVENTEEN 2022 EP.60 談話會聚餐 #1",
        "GOING SEVENTEEN 2022 EP.61 談話會聚餐 #2",
        "GOING SEVENTEEN 2022 EP.62 BAD CLUEⅡ #1",
        "GOING SEVENTEEN 2022 EP.63 BAD CLUEⅡ #2",
        "GOING SEVENTEEN 2022 EP.64 BAD CLUEⅡ #3",
        "GOING SEVENTEEN 2023 寒假特輯-要管和不管 #1",
        "GOING SEVENTEEN 2023 寒假特輯-要管和不管 #2",
        "GOING SEVENTEEN 2023 BSS回歸特輯 #1",
        "GOING SEVENTEEN 2023 BSS回歸特輯 #2",
        "GOING SEVENTEEN 2023 EP.65 GOING公司郊遊會",
        "GOING SEVENTEEN 2023 EP.66 突襲Don't Lie #1",
        "GOING SEVENTEEN 2023 EP.67 突襲Don't Lie #2",
        "GOING SEVENTEEN 2023 EP.68 Don't Lie-CLUE #1",
        "GOING SEVENTEEN 2023 EP.69 Don't Lie-CLUE #2",
        "GOING SEVENTEEN 2023 EP.70 Don't Lie-The CHASER #1",
        "GOING SEVENTEEN 2023 EP.71 Don't Lie-The CHASER #2",
        "GOING SEVENTEEN 2023 EP.72 法庭-洞席真相的眼睛 #1",
        "GOING SEVENTEEN 2023 EP.73 法庭-洞席真相的眼睛 #2",
        "GOING SEVENTEEN 2023 EP.74 尋找權順榮 #1",
        "GOING SEVENTEEN 2023 EP.75 尋找權順榮 #2",
        "GOING SEVENTEEN 2023 EP.76 全圓聚餐",
        "GOING SEVENTEEN 2023 EP.77 在白色區域能做的所有事 #1",
        "GOING SEVENTEEN 2023 EP.78 在白色區域能做的所有事 #2",
        "GOING SEVENTEEN 2023 EP.79 GOING雜誌2.0 #1",
        "GOING SEVENTEEN 2023 EP.80 GOING雜誌2.0 #2",
        "GOING SEVENTEEN 2023 EP.81 SEV SEV TOUR #1",
        "GOING SEVENTEEN 2023 EP.82 SEV SEV TOUR #2",
        "GOING SEVENTEEN 2023 EP.83 SEV SEV TOUR #3",
        "GOING SEVENTEEN 2023 EP.84 SEV SEV TOUR #4",
        "GOING SEVENTEEN 2023 EP.85 Boo家族誕生 #1",
        "GOING SEVENTEEN 2023 EP.86 Boo家族誕生 #2",
        "GOING SEVENTEEN 2023 EP.87 Boo家族誕生 #3",
        "GOING SEVENTEEN 2023 EP.88 Boo家族誕生 #4",
        "GOING SEVENTEEN 2023 EP.89 偷偷離開的客人 #1",
        "GOING SEVENTEEN 2023 EP.90 偷偷離開的客人 #2",
        "GOING SEVENTEEN 2023 EP.91 全知干預視角懲罰 #1",
        "GOING SEVENTEEN 2023 EP.92 全知干預視角懲罰 #2",
        "GOING SEVENTEEN 2023 EP.93 石頭剪刀布 #1",
        "GOING SEVENTEEN 2023 EP.94 石頭剪刀布 #2",
        "GOING SEVENTEEN 2023 輕音樂之神回歸特輯 #1",
        "GOING SEVENTEEN 2023 輕音樂之神回歸特輯 #2",
        "GOING SEVENTEEN 2023 EP.95 舊怨 #1",
        "GOING SEVENTEEN 2023 EP.96 舊怨 #2",
        "GOING SEVENTEEN 2023 EP.97 GOING最佳內容 #1",
        "GOING SEVENTEEN 2023 EP.98 GOING最佳內容 #2",
        "GOING SEVENTEEN 特別篇-BUNNY BUNNY 近況近況(勝寛)",
        "GOING SEVENTEEN 特別篇-嘿嘿嘿氣死你(俊輝)",
        "GOING SEVENTEEN 特別篇-我想看你做這個(明浩)",
        "GOING SEVENTEEN 特別篇-但是(珉奎)",
        "GOING SEVENTEEN 特別篇-發呆(燦)",
        "GOING SEVENTEEN 特別篇-關於改名為客串鐵人這件事(順榮)",
        "GOING SEVENTEEN 特別篇-DeFoFi(知勳)",
        "GOING SEVENTEEN 特別篇-吃美食的孤獨家(圓佑)",
        "GOING SEVENTEEN 特別篇-出去(碩珉)",
        "GOING SEVENTEEN 特別篇-名偵探VERNON(瀚率)",
        "GOING SEVENTEEN 特別篇-甲辰年也請多多關照(知秀)",
        "GOING SEVENTEEN MAESTRO回歸特輯 #1",
        "GOING SEVENTEEN MAESTRO回歸特輯 #2",
        "GOING SEVENTEEN 2024 EP.99 GOING RANGERS #1",
        "GOING SEVENTEEN 2024 EP.100 GOING GANGERS #2",
        "GOING SEVENTEEN 2024 EP.101 13 ANGRY MAN #1",
        "GOING SEVENTEEN 2024 EP.102 13 ANGRY MAN #2",
        "GOING SEVENTEEN 2024 EP.103 LIAR LIAR #1",
        "GOING SEVENTEEN 2024 EP.104 LIAR LIAR #2",
        "GOING SEVENTEEN 2024 EP.105 不眠之夜Ⅲ #1",
        "GOING SEVENTEEN 2024 EP.106 不眠之夜Ⅲ #2",
        "GOING SEVENTEEN 2024 EP.107 班長選舉 #1",
        "GOING SEVENTEEN 2024 EP.108 班長選舉 #2",
        "GOING SEVENTEEN 2024 EP.109 Grrreuk kak kak TTT #1",
        "GOING SEVENTEEN 2024 EP.110 Grrreuk kak kak TTT #2",
        "GOING SEVENTEEN 2024 EP.111 Grrreuk kak kak TTT #3",
        "GOING SEVENTEEN 2024 EP.112 陷阱 #1",
        "GOING SEVENTEEN 2024 EP.113 陷阱 #2",
        "GOING SEVENTEEN 2024 EP.114 BOSS #1",
        "GOING SEVENTEEN 2024 EP.115 BOSS #2",
        "GOING SEVENTEEN 2024 崔&夫心情愉快的早晨 #1",
        "GOING SEVENTEEN 2024 崔&夫心情愉快的早晨 #2",
        "GOING SEVENTEEN 2024 EP.116 竟然得在一天之內過去，這是不是太過份了！ #1",
        "GOING SEVENTEEN 2024 EP.117 竟然得在一天之內過去，這是不是太過份了！ #2",
        "GOING SEVENTEEN 2024 EP.118 GOING PRODUCTION-不要笑",
        "GOING SEVENTEEN 2024 EP.118 GOING PRODUCTION-殭屍採訪",
        "GOING SEVENTEEN 2024 EP.119 GOING PRODUCTION",
        "GOING SEVENTEEN 2024 EP.120 GOING Millionaire #1",
        "GOING SEVENTEEN 2024 EP.121 GOING Millionaire #2",
        "GOING SEVENTEEN 2024 EP.122 小十七小學 #1",
        "GOING SEVENTEEN 2024 EP.123 小十七小學 #2",
      ];

      const drawBtn = document.getElementById("drawBtn");
      const winnerDiv = document.getElementById("winner");
      const wheelSVG = document.getElementById("wheelSVG");
      const wheelGroup = document.getElementById("wheel");

      const centerX = 200;
      const centerY = 200;
      const radius = 200;

      function degToRad(degrees) {
        return degrees * (Math.PI / 180);
      }

      function getPointOnCircumference(angleInDegrees, r) {
        const angleInRadians = degToRad(angleInDegrees - 90);
        const x = centerX + r * Math.cos(angleInRadians);
        const y = centerY + r * Math.sin(angleInRadians);
        return { x, y };
      }

      function createSegmentPath(startAngle, endAngle, r) {
        const start = getPointOnCircumference(startAngle, r);
        const end = getPointOnCircumference(endAngle, r);
        const largeArcFlag = endAngle - startAngle > 180 ? 1 : 0;

        const pathData = [
          `M${centerX},${centerY}`,
          `L${start.x},${start.y}`,
          `A${r},${r}`,
          `0,${largeArcFlag},1`,
          `${end.x},${end.y}`,
          `Z`,
        ].join(" ");

        return pathData;
      }

      // New, lighter orange-yellow color palette
      const colorPalette = [
        "#fff8e1" /* Palest Yellow */,
        "#ffecb3" /* Extra Light Yellow */,
        "#ffe0b2" /* Light Yellow */,
        "#ffd597" /* Soft Orange-Yellow */,
        "#ffcc80" /* Light Orange */,
        "#ffb74d" /* Medium Light Orange */,
        "#ffc107" /* Medium Gold */,
        "#ffcd38" /* Medium Yellow-Orange */,
        "#ffda6d" /* Light Gold */,
        "#ffe89f" /* Palest Gold */,
        "#fff5d2" /* Very Very Light Yellow */,
        "#fffde7" /* Almost White Yellow */,
        "#fffaf0" /* Very Light Peach */,
        "#fffcf5" /* Pale Cream */,
        "#fae3d9" /* Light Peach */,
        "#f8c'cc" /* Pale Coral */,
      ];

      function drawWheel() {
        const totalSegments = participants.length;
        const anglePerSegment = 360 / totalSegments;

        wheelGroup.innerHTML = "";

        for (let i = 0; i < totalSegments; i++) {
          const startAngle = i * anglePerSegment;
          const endAngle = (i + 1) * anglePerSegment;
          const segmentPathData = createSegmentPath(
            startAngle,
            endAngle,
            radius
          );

          const segment = document.createElementNS(
            "http://www.w3.org/2000/svg",
            "path"
          );
          segment.setAttribute("d", segmentPathData);
          segment.setAttribute("class", "segment");
          segment.setAttribute("fill", colorPalette[i % colorPalette.length]);
          wheelGroup.appendChild(segment);
        }
      }

      drawWheel();

      drawBtn.addEventListener("click", () => {
        if (drawBtn.disabled) {
          return;
        }
        drawBtn.disabled = true;

        // Clear previous winner with transition
        winnerDiv.style.opacity = 0;
        setTimeout(() => {
          winnerDiv.textContent = "";
        }, 300); // Match or slightly less than opacity transition

        const totalSegments = participants.length;
        const anglePerSegment = 360 / totalSegments;
        const winnerIndex = Math.floor(Math.random() * totalSegments);
        const finalWinner = participants[winnerIndex];

        const targetAngleForMiddle =
          winnerIndex * anglePerSegment + anglePerSegment / 2;

        const numSpins = 8;
        const totalRotation = numSpins * 360 + targetAngleForMiddle;

        wheelGroup.style.transform = `rotate(-${totalRotation}deg)`;

        const spinDuration =
          parseFloat(getComputedStyle(wheelGroup).transitionDuration) * 1000;

        setTimeout(() => {
          winnerDiv.textContent = finalWinner;
          winnerDiv.style.opacity = 1; // Fade in winner text
          drawBtn.disabled = false;

          // Reset transition to snap to the final position immediately
          wheelGroup.style.transition = "none";
          const currentRotation = totalRotation % 360;
          // Snap to the negative of the target angle to center it under the pointer
          wheelGroup.style.transform = `rotate(-${targetAngleForMiddle}deg)`;

          // Re-enable transition after a very short delay
          setTimeout(() => {
            wheelGroup.style.transition =
              "transform 5s cubic-bezier(0.25, 0.1, 0.25, 1)";
          }, 50);
        }, spinDuration);
      });

      // Initial state for winner div
      winnerDiv.style.opacity = 0;
    </script>
  </body>
</html>
