[index.html](https://github.com/user-attachments/files/29036485/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<meta name="apple-mobile-web-app-capable" content="yes"/>
<meta name="apple-mobile-web-app-status-bar-style" content="default"/>
<title>스토리 RPG</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent}
:root{
  --bg:#f5f4f0;--bg2:#ffffff;--bg3:#f0eeea;--bg4:#e8e5e0;
  --border:#e0ddd8;--border2:#ccc9c2;
  --text:#1a1a1a;--text2:#666660;--text3:#aaa9a0;
  --gold:#7c5cbf;--gold2:#9b7edb;
  --red:#c0392b;--red2:#e74c3c;
  --r:12px;--rs:8px;
  --st:env(safe-area-inset-top,0px);
  --sb:env(safe-area-inset-bottom,0px);
}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',system-ui,sans-serif;overflow:hidden}
#app{height:100dvh;display:flex;flex-direction:column;overflow:hidden}
.page{display:none;flex-direction:column;flex:1;overflow:hidden;background:var(--bg)}
.page.active{display:flex}
.sb{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch}
.sb::-webkit-scrollbar{display:none}
.inner{padding:16px;padding-bottom:calc(var(--sb)+80px)}

/* TOP BAR */
.tbar{padding:calc(var(--st)+12px) 14px 12px;background:var(--bg2);border-bottom:1px solid var(--border);display:flex;align-items:center;gap:8px;flex-shrink:0}
.tbar-t{font-size:16px;font-weight:600;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.ibtn{width:36px;height:36px;border-radius:50%;border:1px solid var(--border2);background:transparent;cursor:pointer;color:var(--text2);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:16px;-webkit-appearance:none}
.ibtn:active{background:var(--bg3);transform:scale(.92)}
.bbtn{width:36px;height:36px;border-radius:50%;border:none;background:transparent;cursor:pointer;color:var(--text2);display:flex;align-items:center;justify-content:center;font-size:24px;flex-shrink:0;-webkit-appearance:none;padding-bottom:2px}
.bbtn:active{color:var(--text)}

/* HOME */
.home-h{padding:calc(var(--st)+20px) 16px 4px;flex-shrink:0}
.home-h h1{font-size:22px;font-weight:700;color:var(--gold)}
.home-h p{font-size:13px;color:var(--text3);margin-top:4px}
.wcard{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r);margin-bottom:12px;overflow:hidden;cursor:pointer;position:relative}
.wcard:active{border-color:var(--border2)}
.wcard-img{width:100%;height:110px;object-fit:cover;display:block}
.wcard-ph{width:100%;height:110px;background:var(--bg3);display:flex;align-items:center;justify-content:center;font-size:40px}
.wcard-body{padding:12px 14px}
.wcard-t{font-size:15px;font-weight:600}
.wcard-m{font-size:12px;color:var(--text2);margin-top:3px}
.wcard-del{position:absolute;top:8px;right:8px;width:28px;height:28px;border-radius:50%;background:rgba(255,255,255,.85);border:1px solid var(--border2);color:var(--text2);font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;-webkit-appearance:none}
.wcard-del:active{background:var(--red);color:#fff}
.new-w-btn{width:100%;padding:16px;border-radius:var(--r);border:1.5px dashed var(--border2);background:transparent;color:var(--text2);font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;-webkit-appearance:none;margin-top:4px}
.new-w-btn:active{border-color:var(--gold);color:var(--gold)}

/* WORLD TABS */
#wd-tabs{display:flex;background:var(--bg2);border-bottom:1px solid var(--border);flex-shrink:0;overflow-x:auto}
#wd-tabs::-webkit-scrollbar{display:none}
.wt{padding:12px 14px;font-size:13px;color:var(--text3);cursor:pointer;white-space:nowrap;border-bottom:2px solid transparent;-webkit-appearance:none;background:transparent;border-left:none;border-right:none;border-top:none;flex-shrink:0}
.wt.on{color:var(--gold);border-bottom-color:var(--gold)}
.wc{display:none;flex:1;overflow:hidden;flex-direction:column}
.wc.on{display:flex}

/* CHAT */
#chips{display:flex;gap:6px;padding:10px 12px;overflow-x:auto;border-bottom:1px solid var(--border);flex-shrink:0}
#chips::-webkit-scrollbar{display:none}
.chip{display:flex;align-items:center;gap:5px;padding:5px 11px;border-radius:99px;border:1px solid var(--border2);background:var(--bg3);white-space:nowrap;cursor:pointer;flex-shrink:0;font-size:12px;color:var(--text2);-webkit-appearance:none}
.chip.on{border-color:var(--gold);background:#f0ecfb;color:var(--gold)}
.chip-av{width:18px;height:18px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;overflow:hidden;background:var(--bg4)}
.chip-av img{width:100%;height:100%;object-fit:cover}
#msgs{flex:1;overflow-y:auto;padding:14px 12px;display:flex;flex-direction:column;gap:12px;-webkit-overflow-scrolling:touch}
#msgs::-webkit-scrollbar{display:none}
.mnar{align-self:center;width:100%;padding:8px 14px;border-top:1px solid var(--border);border-bottom:1px solid var(--border);color:var(--text2);font-size:13px;line-height:1.7;font-style:italic;text-align:center;margin:2px 0;background:var(--bg3)}
.mw{display:flex;gap:8px;max-width:82%}
.mw.user{align-self:flex-end;flex-direction:row-reverse}
.mw.npc{align-self:flex-start}
.mav{width:32px;height:32px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:15px;background:var(--bg3);border:1px solid var(--border2);overflow:hidden}
.mav img{width:100%;height:100%;object-fit:cover}
.mbody{display:flex;flex-direction:column;gap:3px;min-width:0}
.mwho{font-size:10px;color:var(--text3);padding:0 4px}
.mw.user .mwho{text-align:right}
.mbub{padding:9px 13px;border-radius:14px;font-size:14px;line-height:1.65;white-space:pre-wrap;word-break:break-word}
.mw.npc .mbub{background:#ffffff;border:1px solid var(--border2);border-bottom-left-radius:3px;color:var(--text)}
.mw.user .mbub{background:#ede8f8;border:1px solid #c9bfea;border-bottom-right-radius:3px;color:#3d2a72}
.dr{display:flex;gap:4px;padding:3px 0}
.dot{width:5px;height:5px;border-radius:50%;background:var(--text3);animation:dp 1.2s infinite}
.dot:nth-child(2){animation-delay:.2s}.dot:nth-child(3){animation-delay:.4s}
@keyframes dp{0%,60%,100%{opacity:.25;transform:scale(1)}30%{opacity:1;transform:scale(1.3)}}
#ia{padding:8px 10px calc(var(--sb)+8px);background:var(--bg2);border-top:1px solid var(--border);flex-shrink:0}
#ir{display:flex;gap:8px;align-items:flex-end}
#inp{flex:1;background:var(--bg3);border:1px solid var(--border2);border-radius:20px;padding:10px 14px;font-size:15px;color:var(--text);font-family:inherit;resize:none;min-height:42px;max-height:100px;outline:none;line-height:1.4;-webkit-appearance:none}
#inp::placeholder{color:var(--text3)}
.sbtn{width:42px;height:42px;border-radius:50%;border:none;background:var(--gold);color:#fff;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:19px;font-weight:700;cursor:pointer;-webkit-appearance:none}
.sbtn:active{opacity:.7;transform:scale(.92)}
.sbtn:disabled{opacity:.3}
.nbtn{width:36px;height:36px;border-radius:50%;border:1px solid var(--border2);background:var(--bg3);color:var(--text2);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:15px;cursor:pointer;-webkit-appearance:none}
.nbtn:active{background:var(--bg4)}

/* MODEL BAR */
#model-bar{display:flex;gap:6px;padding:8px 0 6px;overflow-x:auto;align-items:center}
#model-bar::-webkit-scrollbar{display:none}
.mchip{padding:5px 12px;border-radius:99px;border:1px solid var(--border2);background:var(--bg3);font-size:12px;color:var(--text2);cursor:pointer;white-space:nowrap;flex-shrink:0;-webkit-appearance:none;transition:all .15s}
.mchip.on{border-color:var(--gold);background:#f0ecfb;color:var(--gold);font-weight:600}
.mchip:active{transform:scale(.95)}
.mchip-key{padding:5px 10px;border-radius:99px;border:1px solid var(--border2);background:transparent;font-size:12px;color:var(--text3);cursor:pointer;white-space:nowrap;flex-shrink:0;-webkit-appearance:none;margin-left:auto}
.mchip-key:active{color:var(--gold)}

/* CARDS */
.sec-t{font-size:11px;color:var(--text3);letter-spacing:.08em;text-transform:uppercase;margin-bottom:10px;margin-top:18px}
.sec-t:first-child{margin-top:0}
.card{background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);padding:13px 14px;margin-bottom:10px;cursor:pointer}
.card:active{background:var(--bg4)}
.crow{display:flex;align-items:center;gap:12px}
.cav{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px;background:var(--bg4);border:1px solid var(--border2);flex-shrink:0;overflow:hidden}
.cav img{width:100%;height:100%;object-fit:cover}
.cmeta{flex:1;min-width:0}
.cname{font-size:14px;font-weight:500}
.csub{font-size:12px;color:var(--text2);margin-top:2px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.dbtn{width:28px;height:28px;border-radius:50%;background:transparent;border:1px solid var(--border2);color:var(--text3);font-size:13px;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;-webkit-appearance:none}
.dbtn:active{background:var(--red);color:#fff;border-color:var(--red)}
.add-btn{width:100%;padding:14px;border-radius:var(--r);border:1.5px dashed var(--border2);background:transparent;color:var(--text2);font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:8px;-webkit-appearance:none;margin-top:4px}
.add-btn:active{border-color:var(--gold);color:var(--gold)}

/* MEMORY */
.mtabs{display:flex;gap:8px;margin-bottom:14px;flex-wrap:wrap}
.mtab{padding:7px 16px;border-radius:99px;border:1px solid var(--border2);background:var(--bg3);font-size:13px;color:var(--text2);cursor:pointer;-webkit-appearance:none}
.mtab.on{background:var(--gold);color:#fff;border-color:var(--gold)}
.mitem{display:flex;align-items:center;gap:10px;padding:12px 14px;background:var(--bg3);border:1px solid var(--border);border-radius:var(--rs);margin-bottom:8px;cursor:pointer}
.mitem:active{background:var(--bg4)}
.mitarr{color:var(--text3);font-size:16px;flex-shrink:0}
.mitt{flex:1;font-size:14px}
.midel{width:24px;height:24px;border-radius:50%;background:transparent;border:none;color:var(--text3);font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;-webkit-appearance:none;flex-shrink:0}
.midel:active{color:var(--red2)}
.mibody{font-size:13px;color:var(--text2);line-height:1.6;margin-top:6px;padding:10px;background:var(--bg4);border-radius:var(--rs);display:none}

/* FORMS */
.fld{margin-bottom:14px}
.fld label{display:block;font-size:11px;color:var(--text2);letter-spacing:.06em;margin-bottom:6px}
.fld input,.fld textarea,.fld select{width:100%;background:var(--bg3);border:1px solid var(--border2);border-radius:var(--rs);padding:11px 13px;font-size:14px;color:var(--text);font-family:inherit;outline:none;-webkit-appearance:none}
.fld textarea{min-height:90px;resize:vertical}
.fld select{height:44px}
.fld select option{background:var(--bg2)}
.fld input:focus,.fld textarea:focus{border-color:#404060}
.cnt{font-size:11px;color:var(--text3);text-align:right;margin-top:4px}
.pbtn{width:100%;padding:14px;border-radius:var(--r);border:none;background:var(--gold);color:#fff;font-size:15px;font-weight:700;cursor:pointer;-webkit-appearance:none;margin-top:6px}
.pbtn:active{opacity:.8}
.gbtn{width:100%;padding:13px;border-radius:var(--r);border:1px solid var(--border2);background:transparent;color:var(--text2);font-size:14px;cursor:pointer;-webkit-appearance:none;margin-top:8px}
.gbtn:active{background:var(--bg3)}

/* EMOJI */
.egrid{display:flex;flex-wrap:wrap;gap:6px;margin-top:8px}
.ep{width:38px;height:38px;border-radius:var(--rs);border:1px solid var(--border);background:var(--bg3);font-size:18px;display:flex;align-items:center;justify-content:center;cursor:pointer;-webkit-appearance:none}
.ep:active,.ep.on{border-color:var(--gold);background:var(--bg4)}
.avrow{display:flex;align-items:center;gap:12px;margin-top:8px}
.avprev{width:52px;height:52px;border-radius:50%;background:var(--bg3);border:1px solid var(--border2);display:flex;align-items:center;justify-content:center;font-size:26px;overflow:hidden;flex-shrink:0}
.avprev img{width:100%;height:100%;object-fit:cover}
.uplbl{padding:9px 16px;border-radius:var(--rs);border:1px solid var(--border2);color:var(--text2);font-size:13px;cursor:pointer;background:transparent}
.uplbl:active{border-color:var(--gold);color:var(--gold)}

/* IMG UPLOAD */
.imgbox{width:100%;height:140px;border-radius:var(--r);overflow:hidden;background:var(--bg3);border:1.5px dashed var(--border2);display:flex;align-items:center;justify-content:center;cursor:pointer;position:relative;margin-bottom:14px}
.imgbox:active{border-color:var(--gold)}
.imgbg{position:absolute;inset:0;object-fit:cover;width:100%;height:100%;display:none}
.imgov{position:absolute;inset:0;background:rgba(0,0,0,.55);display:none;align-items:center;justify-content:center;flex-direction:column;gap:5px;color:#fff;font-size:12px}
.imghint{display:flex;flex-direction:column;align-items:center;gap:6px;color:var(--text3);font-size:13px}

/* SHEET */
.sov{display:none;position:fixed;inset:0;background:rgba(0,0,0,.75);z-index:300;align-items:flex-end;justify-content:center}
.sov.open{display:flex}
.sheet{background:var(--bg2);border-radius:20px 20px 0 0;border-top:1px solid var(--border2);width:100%;max-height:92dvh;overflow-y:auto;padding:0 0 calc(var(--sb)+16px);-webkit-overflow-scrolling:touch}
.sh{width:36px;height:4px;border-radius:99px;background:var(--border2);margin:12px auto 16px}
.st{font-size:15px;font-weight:600;color:var(--gold);padding:0 18px 14px;border-bottom:1px solid var(--border);margin-bottom:16px}
.sbody{padding:0 18px}

/* TOAST */
#toast{position:fixed;top:calc(var(--st)+60px);left:50%;transform:translateX(-50%);background:var(--bg3);border:1px solid var(--border2);border-radius:99px;padding:8px 18px;font-size:13px;color:var(--text);z-index:999;opacity:0;transition:opacity .3s;pointer-events:none;white-space:nowrap}
#toast.show{opacity:1}

/* EMPTY */
.es{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 24px;gap:10px;color:var(--text3);text-align:center}
.es .ei{font-size:36px;opacity:.4;margin-bottom:4px}
.es p{font-size:13px;line-height:1.6}

/* PILL */
.pill{display:inline-flex;align-items:center;gap:6px;padding:6px 14px;background:var(--bg3);border:1px solid var(--border2);border-radius:99px;font-size:12px;color:var(--text2);margin-bottom:10px}
.spin{display:inline-block;animation:spin 1s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}

/* ACTIVE PROFILE TAG */
.atag{font-size:11px;padding:3px 8px;border-radius:99px;background:var(--gold);color:#fff;font-weight:700;flex-shrink:0}
</style>
</head>
<body>
<div id="app">

<!-- HOME -->
<div class="page active" id="pg-home">
  <div class="home-h">
    <h1>✦ 스토리 RPG</h1>
    <p>세계관을 선택하거나 새로 만드세요</p>
  </div>
  <div class="sb">
    <div class="inner">
      <div id="world-list"></div>
      <button class="new-w-btn" onclick="openNewWorldSheet()">＋ 새 세계관 만들기</button>
    </div>
  </div>
</div>

<!-- WORLD DETAIL -->
<div class="page" id="pg-world">
  <div class="tbar">
    <button class="bbtn" onclick="goHome()">‹</button>
    <span class="tbar-t" id="wd-label">세계관</span>
    <button class="ibtn" onclick="openWorldEditSheet()">✎</button>
    <button class="ibtn" onclick="clearChatConfirm()">🔄</button>
  </div>
  <div id="wd-tabs">
    <button class="wt on" onclick="switchTab('chat')">💬 스토리</button>
    <button class="wt" onclick="switchTab('chars')">👥 캐릭터</button>
    <button class="wt" onclick="switchTab('memory')">🧠 요약</button>
    <button class="wt" onclick="switchTab('profile')">🙋 프로필</button>
    <button class="wt" onclick="switchTab('note')">📝 유저노트</button>
  </div>

  <!-- CHAT -->
  <div class="wc on" id="wc-chat">
    <div id="chips"></div>
    <div id="msgs">
      <div class="es" id="chat-es"><div class="ei">✦</div><p>캐릭터를 추가하고<br/>이야기를 시작하세요</p></div>
    </div>
    <div id="ia">
      <div id="model-bar">
        <button class="mchip on" id="mc-hyper" onclick="selModel('hyper')">⚡ 하이퍼챗</button>
        <button class="mchip" id="mc-super" onclick="selModel('super')">🔥 슈퍼챗</button>
        <button class="mchip" id="mc-pro" onclick="selModel('pro')">✦ 프로챗</button>
        <button class="mchip-key" onclick="openSov('key-ov')" id="key-status">🔑 API 키</button>
      </div>
      <div id="ir">
        <button class="nbtn" onclick="triggerNarrate()">📖</button>
        <textarea id="inp" placeholder="대사 또는 행동 묘사..." rows="1"></textarea>
        <button class="sbtn" id="snd" onclick="send()">↑</button>
      </div>
    </div>
  </div>

  <!-- CHARS -->
  <div class="wc" id="wc-chars">
    <div class="sb"><div class="inner">
      <div class="sec-t">등장인물</div>
      <div id="char-list"></div>
      <button class="add-btn" onclick="openCharSheet(null)">＋ 새 캐릭터 추가</button>
    </div></div>
  </div>

  <!-- MEMORY -->
  <div class="wc" id="wc-memory">
    <div class="sb"><div class="inner">
      <div class="mtabs">
        <button class="mtab on" onclick="switchMemTab('long')">장기 기억</button>
        <button class="mtab" onclick="switchMemTab('short')">단기 기억</button>
      </div>
      <div id="mem-list"></div>
      <button class="add-btn" onclick="openMemSheet(null)">＋ 기억 추가</button>
    </div></div>
  </div>

  <!-- PROFILE -->
  <div class="wc" id="wc-profile">
    <div class="sb"><div class="inner">
      <div class="sec-t">대화 프로필</div>
      <p style="font-size:13px;color:var(--text2);margin-bottom:14px;line-height:1.6">작품 내에 반영될 나의 이름과 정보를 설정하세요</p>
      <div id="profile-list"></div>
      <button class="add-btn" onclick="openProfileSheet(null)">＋ 프로필 추가</button>
    </div></div>
  </div>

  <!-- NOTE -->
  <div class="wc" id="wc-note">
    <div class="sb"><div class="inner">
      <div class="sec-t">유저 노트</div>
      <p style="font-size:13px;color:var(--text2);margin-bottom:14px;line-height:1.6">이 채팅방에서 반드시 기억해 줬으면 하는 내용을 적어주세요</p>
      <div class="fld">
        <textarea id="note-txt" placeholder="예) 주인공과 레이의 관계는 소꿉친구. 마법은 이 세계에서 금지돼 있음..." style="min-height:200px"></textarea>
        <div class="cnt" id="note-cnt">0 / 2000</div>
      </div>
      <button class="pbtn" onclick="saveNote()">저장</button>
    </div></div>
  </div>
</div>

<!-- CHAR DETAIL -->
<div class="page" id="pg-char">
  <div class="tbar">
    <button class="bbtn" onclick="goWorldChars()">‹</button>
    <span class="tbar-t" id="cd-label">캐릭터 성정</span>
    <button class="ibtn" onclick="openCharSheet('cur')">✎</button>
    <button class="ibtn" onclick="deleteCurrentChar()">🗑</button>
  </div>
  <div class="sb"><div class="inner" id="cd-body"></div></div>
</div>

</div>

<!-- WORLD SHEET -->
<div class="sov" id="ws-ov" onclick="closeSov('ws-ov',event)">
  <div class="sheet" onclick="event.stopPropagation()">
    <div class="sh"></div>
    <div class="st" id="ws-title">새 세계관</div>
    <div class="sbody">
      <div class="imgbox" onclick="document.getElementById('wf').click()">
        <img class="imgbg" id="ws-bg" alt=""/>
        <div class="imgov" id="ws-ov2"><span style="font-size:20px">🔄</span><span>변경</span></div>
        <div class="imghint" id="ws-hint"><div style="font-size:28px;opacity:.4">🌍</div><span>이미지 업로드</span><span style="font-size:11px;color:var(--text3)">Claude가 자동 분석</span></div>
        <input type="file" id="wf" accept="image/*" style="display:none"/>
      </div>
      <div id="ws-an" style="display:none"><div class="pill"><span class="spin">⏳</span> 분석 중...</div></div>
      <div class="fld"><label>세계관 제목</label><input type="text" id="ws-t" placeholder="예) 성흔과 위계"/></div>
      <div class="fld"><label>세계관 설명</label><textarea id="ws-d" placeholder="배경, 규칙, 분위기..."></textarea></div>
      <div class="fld"><label>장르</label><select id="ws-g">
        <option value="dark_fantasy">다크 판타지</option>
        <option value="scifi">SF / 사이버펑크</option>
        <option value="modern">현대 도시</option>
        <option value="romance">로맨스</option>
        <option value="horror">호러</option>
        <option value="historical">역사극</option>
        <option value="free">자유</option>
      </select></div>
      <button class="pbtn" onclick="saveWorld()">저장</button>
    </div>
  </div>
</div>

<!-- CHAR SHEET -->
<div class="sov" id="cs-ov" onclick="closeSov('cs-ov',event)">
  <div class="sheet" onclick="event.stopPropagation()">
    <div class="sh"></div>
    <div class="st" id="cs-title">새 캐릭터</div>
    <div class="sbody">
      <div class="fld">
        <label>아바타</label>
        <div class="avrow">
          <div class="avprev" id="av-prev">🧙</div>
          <label class="uplbl" for="cf">📷 사진 업로드</label>
          <input type="file" id="cf" accept="image/*" style="display:none" onchange="onCharImg(event)"/>
        </div>
        <div class="egrid" id="emoG"></div>
      </div>
      <div class="fld"><label>이름</label><input type="text" id="cm-n" placeholder="캐릭터 이름"/></div>
      <div class="fld"><label>역할 / 소개</label><input type="text" id="cm-r" placeholder="예) 주인공의 라이벌, 정체불명의 상인..."/></div>
      <div class="fld"><label>성격 · 말투 · 배경 (성정)</label><textarea id="cm-s" placeholder="예) 너는 [이름]이야. 냉소적이고 말수가 적지만 중요한 순간에 솔직해져. 반말 사용.&#10;&#10;외모: ...&#10;배경: ..."></textarea></div>
      <button class="pbtn" onclick="saveChar()">저장</button>
    </div>
  </div>
</div>

<!-- MEMORY SHEET -->
<div class="sov" id="ms-ov" onclick="closeSov('ms-ov',event)">
  <div class="sheet" onclick="event.stopPropagation()">
    <div class="sh"></div>
    <div class="st" id="ms-title">기억 추가</div>
    <div class="sbody">
      <div class="fld"><label>제목</label><input type="text" id="mm-t" placeholder="예) 역전의 순간, 현재 상황..."/></div>
      <div class="fld"><label>내용</label><textarea id="mm-b" placeholder="이 기억의 내용을 자세히 적어주세요..."></textarea></div>
      <button class="pbtn" onclick="saveMem()">저장</button>
    </div>
  </div>
</div>

<!-- PROFILE SHEET -->
<div class="sov" id="ps-ov" onclick="closeSov('ps-ov',event)">
  <div class="sheet" onclick="event.stopPropagation()">
    <div class="sh"></div>
    <div class="st" id="ps-title">대화 프로필</div>
    <div class="sbody">
      <div class="fld"><label>프로필 이름</label><input type="text" id="pm-n" placeholder="예) 리리, 나..."/></div>
      <div class="fld"><label>프로필 설명</label><textarea id="pm-b" placeholder="작품 내에 반영될 나의 외모, 나이, 성격, 배경 등..."></textarea></div>
      <button class="pbtn" onclick="saveProfile()">저장</button>
    </div>
  </div>
</div>

<!-- API KEY SHEET -->
<div class="sov" id="key-ov" onclick="closeSov('key-ov',event)">
  <div class="sheet" onclick="event.stopPropagation()">
    <div class="sh"></div>
    <div class="st">🔑 API 키 설정</div>
    <div class="sbody">
      <div class="fld">
        <label>⚡ Claude API 키 <span style="color:var(--text3);font-weight:400">(하이퍼챗 · 슈퍼챗)</span></label>
        <input type="password" id="claude-key-inp" placeholder="sk-ant-..."/>
        <p style="font-size:12px;color:var(--text3);margin-top:5px">→ <a href="https://console.anthropic.com" style="color:var(--gold)">console.anthropic.com</a> 에서 발급 · 크레딧 충전 필요</p>
      </div>
      <div class="fld" style="margin-top:6px">
        <label>✦ Gemini API 키 <span style="color:var(--text3);font-weight:400">(프로챗)</span></label>
        <input type="password" id="gemini-key-inp" placeholder="AIza..."/>
        <p style="font-size:12px;color:var(--text3);margin-top:5px">→ <a href="https://aistudio.google.com/apikey" style="color:var(--gold)">aistudio.google.com</a> 에서 무료 발급</p>
      </div>
      <p style="font-size:12px;color:var(--text3);margin-bottom:16px;margin-top:8px">🔒 키는 이 기기에만 저장되며 외부로 전송되지 않아요</p>
      <button class="pbtn" onclick="saveApiKey()">저장</button>
      <button class="gbtn" onclick="clearAllKeys()">키 전체 삭제</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
const EMOJIS=['🧙','🦊','🐺','🌙','✨','⚔️','🔮','👑','💀','🐉','🌊','🔥','⚡','🌸','🌺','🎭','🤖','🧝','🧛','🦅','💎','🌿','🌟','🎪','🗡️','🛡️','📖','☣️','🌑','🏚️'];
const TABS=['chat','chars','memory','profile','note'];

function ld(k,d=null){try{const v=localStorage.getItem(k);return v?JSON.parse(v):d;}catch{return d;}}
function sv(k,v){try{localStorage.setItem(k,JSON.stringify(v));}catch{}}

let worlds=ld('worlds',[]);
let curId=null;
let curCharIdx=null;
let editCharMode=null;
let editMemIdx=null;
let editProfileIdx=null;
let curMemTab='long';
let activeSpeaker='user';
let busy=false;
let wsImg='';
let charImg='';
let selEmo='🧙';
let curModel=ld('curModel','hyper');
let geminiKey=ld('geminiKey','');
let claudeKey=ld('claudeKey','');

function cw(){return worlds.find(w=>w.id===curId)||null;}
function sws(){sv('worlds',worlds);}
function gchats(){return ld('c_'+curId,[]);}
function schats(a){sv('c_'+curId,a);}
function esc(s){return String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}

/* NAV */
function showPg(id){document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));document.getElementById(id).classList.add('active');}
function goHome(){showPg('pg-home');renderWorldList();}
function goWorldChars(){showPg('pg-world');switchTab('chars');}

function openWorld(id){
  curId=id;const w=cw();if(!w)return;
  document.getElementById('wd-label').textContent=w.title;
  showPg('pg-world');switchTab('chat');
  renderChips();renderChatMsgs();renderCharList();renderMemList();renderProfileList();renderNote();
}

/* HOME */
function renderWorldList(){
  const el=document.getElementById('world-list');el.innerHTML='';
  if(!worlds.length){el.innerHTML='<div class="es"><div class="ei">📖</div><p>아직 세계관이 없어요<br/>새로 만들어보세요</p></div>';return;}
  worlds.forEach(w=>{
    const d=document.createElement('div');d.className='wcard';
    const img=w.imgB64?`<img class="wcard-img" src="data:image/jpeg;base64,${w.imgB64}" alt=""/>`:`<div class="wcard-ph">${w.emoji||'🌍'}</div>`;
    d.innerHTML=`${img}<div class="wcard-body"><div class="wcard-t">${esc(w.title)}</div><div class="wcard-m">캐릭터 ${(w.chars||[]).length}명 · ${esc(w.genre||'')}</div></div><button class="wcard-del" onclick="event.stopPropagation();delWorld('${w.id}')">✕</button>`;
    d.onclick=()=>openWorld(w.id);el.appendChild(d);
  });
}
function delWorld(id){if(!confirm('세계관을 삭제할까요?'))return;worlds=worlds.filter(w=>w.id!==id);sws();localStorage.removeItem('c_'+id);renderWorldList();toast('삭제됨');}

/* WORLD SHEET */
function openNewWorldSheet(){
  wsImg='';curId=null;
  document.getElementById('ws-title').textContent='새 세계관';
  document.getElementById('ws-t').value='';document.getElementById('ws-d').value='';document.getElementById('ws-g').value='dark_fantasy';
  document.getElementById('ws-bg').style.display='none';document.getElementById('ws-ov2').style.display='none';document.getElementById('ws-hint').style.display='flex';
  document.getElementById('ws-an').style.display='none';document.getElementById('wf').value='';
  openSov('ws-ov');
}
function openWorldEditSheet(){
  const w=cw();if(!w)return;wsImg=w.imgB64||'';
  document.getElementById('ws-title').textContent='세계관 편집';
  document.getElementById('ws-t').value=w.title||'';document.getElementById('ws-d').value=w.desc||'';document.getElementById('ws-g').value=w.genre||'dark_fantasy';
  if(wsImg){document.getElementById('ws-bg').src='data:image/jpeg;base64,'+wsImg;document.getElementById('ws-bg').style.display='block';document.getElementById('ws-ov2').style.display='flex';document.getElementById('ws-hint').style.display='none';}
  else{document.getElementById('ws-bg').style.display='none';document.getElementById('ws-ov2').style.display='none';document.getElementById('ws-hint').style.display='flex';}
  openSov('ws-ov');
}
document.getElementById('wf').addEventListener('change',async e=>{
  const f=e.target.files[0];if(!f)return;wsImg=await f2b(f);
  document.getElementById('ws-bg').src='data:image/jpeg;base64,'+wsImg;document.getElementById('ws-bg').style.display='block';document.getElementById('ws-ov2').style.display='flex';document.getElementById('ws-hint').style.display='none';
  analyzeImg(wsImg);e.target.value='';
});
async function analyzeImg(b64){
  document.getElementById('ws-an').style.display='block';
  try{
    const res=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-6',max_tokens:400,messages:[{role:'user',content:[{type:'image',source:{type:'base64',media_type:'image/jpeg',data:b64}},{type:'text',text:'RPG 세계관 이미지. JSON만 반환(다른 텍스트 없이): {"title":"제목","desc":"핵심 설명 2-3문장","genre":"dark_fantasy|scifi|modern|romance|horror|historical|free"}'}]}]})});
    const data=await res.json();
    const p=JSON.parse(data.content?.map(b=>b.text||'').join('').replace(/```json|```/g,'').trim());
    document.getElementById('ws-t').value=p.title||'';document.getElementById('ws-d').value=p.desc||'';
    if(p.genre)document.getElementById('ws-g').value=p.genre;toast('✅ 분석 완료');
  }catch{toast('분석 오류 - 직접 입력해주세요');}
  document.getElementById('ws-an').style.display='none';
}
function saveWorld(){
  const title=document.getElementById('ws-t').value.trim();if(!title){toast('제목을 입력해주세요');return;}
  const desc=document.getElementById('ws-d').value.trim();const genre=document.getElementById('ws-g').value;
  if(curId){const w=cw();if(w){w.title=title;w.desc=desc;w.genre=genre;if(wsImg)w.imgB64=wsImg;sws();document.getElementById('wd-label').textContent=title;}}
  else{const id='w'+Date.now();worlds.push({id,title,desc,genre,imgB64:wsImg,emoji:'🌍',chars:[],memory:{long:[],short:[]},profiles:[],note:'',activeProfile:0});sws();curId=id;}
  closeSov('ws-ov');toast('저장됨');
  if(!document.getElementById('pg-world').classList.contains('active'))openWorld(curId);
  else renderWorldList();
}

/* CHARS */
function buildEmoGrid(){
  const g=document.getElementById('emoG');g.innerHTML='';
  EMOJIS.forEach(e=>{const b=document.createElement('button');b.type='button';b.className='ep'+(e===selEmo?' on':'');b.textContent=e;b.onclick=()=>{document.querySelectorAll('.ep').forEach(x=>x.classList.remove('on'));b.classList.add('on');selEmo=e;charImg='';upAvPrev();};g.appendChild(b);});
}
function upAvPrev(){const el=document.getElementById('av-prev');el.innerHTML=charImg?`<img src="data:image/jpeg;base64,${charImg}" alt=""/>`:(selEmo||'🧙');}
function onCharImg(e){const f=e.target.files[0];if(!f)return;const r=new FileReader();r.onload=ev=>{charImg=ev.target.result.split(',')[1];upAvPrev();};r.readAsDataURL(f);e.target.value='';}

function openCharSheet(mode){
  editCharMode=mode;charImg='';selEmo='🧙';
  let c=null;
  if(mode==='cur'&&curCharIdx!==null)c=cw()?.chars[curCharIdx];
  else if(typeof mode==='number')c=cw()?.chars[mode];
  document.getElementById('cs-title').textContent=c?'캐릭터 편집':'새 캐릭터';
  if(c){document.getElementById('cm-n').value=c.name||'';document.getElementById('cm-r').value=c.role||'';document.getElementById('cm-s').value=c.sys||'';selEmo=c.emoji||'🧙';charImg=c.imgB64||'';}
  else{document.getElementById('cm-n').value='';document.getElementById('cm-r').value='';document.getElementById('cm-s').value='';}
  buildEmoGrid();upAvPrev();openSov('cs-ov');
  setTimeout(()=>document.getElementById('cm-n').focus(),300);
}
function saveChar(){
  const name=document.getElementById('cm-n').value.trim();if(!name){toast('이름을 입력해주세요');return;}
  const w=cw();if(!w)return;
  const c={name,role:document.getElementById('cm-r').value.trim(),sys:document.getElementById('cm-s').value.trim(),emoji:selEmo,imgB64:charImg};
  if(editCharMode===null)w.chars.push(c);
  else if(editCharMode==='cur'&&curCharIdx!==null)w.chars[curCharIdx]=c;
  else if(typeof editCharMode==='number')w.chars[editCharMode]=c;
  sws();closeSov('cs-ov');renderCharList();renderChips();
  if(editCharMode==='cur')renderCharDetail(curCharIdx);
  toast(editCharMode?'수정됨':'추가됨');
}
function renderCharList(){
  const w=cw();const el=document.getElementById('char-list');el.innerHTML='';
  if(!w?.chars?.length){el.innerHTML='<div class="es"><div class="ei">👥</div><p>등장인물이 없어요</p></div>';return;}
  w.chars.forEach((c,i)=>{
    const d=document.createElement('div');d.className='card';
    const av=c.imgB64?`<img src="data:image/jpeg;base64,${c.imgB64}" alt=""/>`:(c.emoji||'🧙');
    d.innerHTML=`<div class="crow"><div class="cav">${av}</div><div class="cmeta"><div class="cname">${esc(c.name)}</div><div class="csub">${esc(c.role||'')}</div></div><button class="dbtn" onclick="event.stopPropagation();delChar(${i})">✕</button><span style="color:var(--text3);font-size:18px">›</span></div>`;
    d.onclick=()=>openCharDetail(i);el.appendChild(d);
  });
}
function delChar(idx){const w=cw();if(!w)return;if(!confirm(`${w.chars[idx]?.name}을(를) 삭제할까요?`))return;w.chars.splice(idx,1);sws();renderCharList();renderChips();toast('삭제됨');}
function deleteCurrentChar(){if(curCharIdx===null)return;delChar(curCharIdx);showPg('pg-world');switchTab('chars');}
function openCharDetail(idx){curCharIdx=idx;renderCharDetail(idx);showPg('pg-char');}
function renderCharDetail(idx){
  const w=cw();const c=w?.chars[idx];if(!c)return;
  document.getElementById('cd-label').textContent=c.name;
  const av=c.imgB64?`<img src="data:image/jpeg;base64,${c.imgB64}" alt=""/>`:(c.emoji||'🧙');
  document.getElementById('cd-body').innerHTML=`
    <div style="display:flex;align-items:center;gap:14px;margin-bottom:20px">
      <div style="width:64px;height:64px;border-radius:50%;background:var(--bg3);border:1px solid var(--border2);display:flex;align-items:center;justify-content:center;font-size:30px;overflow:hidden;flex-shrink:0">${av}</div>
      <div><div style="font-size:18px;font-weight:700;color:var(--gold)">${esc(c.name)}</div><div style="font-size:13px;color:var(--text2);margin-top:3px">${esc(c.role||'')}</div></div>
    </div>
    <div class="sec-t">성정</div>
    <div style="background:var(--bg3);border:1px solid var(--border);border-radius:var(--r);padding:14px;font-size:14px;color:var(--text2);line-height:1.8;white-space:pre-wrap">${esc(c.sys||'성정이 설정되지 않았습니다.')}</div>`;
}

/* MEMORY */
function switchMemTab(t){
  curMemTab=t;
  document.querySelectorAll('.mtab').forEach((b,i)=>b.classList.toggle('on',i===(t==='long'?0:1)));
  renderMemList();
}
function renderMemList(){
  const w=cw();const el=document.getElementById('mem-list');el.innerHTML='';
  const mems=w?.memory?.[curMemTab]||[];
  if(!mems.length){el.innerHTML='<div class="es" style="padding:24px"><p>기억이 없어요</p></div>';return;}
  mems.forEach((m,i)=>{
    const wrap=document.createElement('div');
    const row=document.createElement('div');row.className='mitem';
    row.innerHTML=`<span class="mitarr">›</span><span class="mitt">${esc(m.title)}</span><button class="midel" onclick="event.stopPropagation();delMem(${i})">✕</button>`;
    const body=document.createElement('div');body.className='mibody';body.textContent=m.body;
    row.onclick=()=>{const open=body.style.display!=='none'&&body.style.display!=='';body.style.display=open?'none':'block';row.querySelector('.mitarr').textContent=open?'›':'⌄';};
    wrap.appendChild(row);wrap.appendChild(body);el.appendChild(wrap);
  });
}
function delMem(idx){const w=cw();if(!w)return;w.memory[curMemTab].splice(idx,1);sws();renderMemList();toast('삭제됨');}
function openMemSheet(idx){
  editMemIdx=idx;const w=cw();
  document.getElementById('ms-title').textContent=idx!==null?'기억 편집':`기억 추가 (${curMemTab==='long'?'장기':'단기'})`;
  const m=idx!==null?w?.memory?.[curMemTab]?.[idx]:null;
  document.getElementById('mm-t').value=m?.title||'';document.getElementById('mm-b').value=m?.body||'';
  openSov('ms-ov');
}
function saveMem(){
  const title=document.getElementById('mm-t').value.trim();const body=document.getElementById('mm-b').value.trim();
  if(!title){toast('제목을 입력해주세요');return;}
  const w=cw();if(!w)return;
  if(!w.memory)w.memory={long:[],short:[]};
  if(!w.memory[curMemTab])w.memory[curMemTab]=[];
  if(editMemIdx!==null)w.memory[curMemTab][editMemIdx]={title,body};
  else w.memory[curMemTab].push({title,body});
  sws();closeSov('ms-ov');renderMemList();toast('저장됨');
}

/* PROFILE */
function renderProfileList(){
  const w=cw();const el=document.getElementById('profile-list');el.innerHTML='';
  const profs=w?.profiles||[];
  if(!profs.length){el.innerHTML='<div class="es" style="padding:24px"><p>프로필이 없어요</p></div>';return;}
  profs.forEach((p,i)=>{
    const d=document.createElement('div');d.className='card';
    const isActive=i===(w.activeProfile||0);
    d.innerHTML=`<div class="crow">${isActive?'<span class="atag">현재</span>':''}<div class="cmeta"><div class="cname">${esc(p.name)}</div><div class="csub">${esc((p.body||'').slice(0,50))}${(p.body||'').length>50?'...':''}</div></div><button class="dbtn" onclick="event.stopPropagation();delProfile(${i})">✕</button><span style="color:var(--text3);font-size:18px">›</span></div>`;
    d.onclick=()=>{w.activeProfile=i;sws();renderProfileList();toast(`${p.name} 프로필 적용됨`);};
    el.appendChild(d);
  });
}
function delProfile(idx){const w=cw();if(!w)return;w.profiles.splice(idx,1);if((w.activeProfile||0)>=w.profiles.length)w.activeProfile=0;sws();renderProfileList();toast('삭제됨');}
function openProfileSheet(idx){
  editProfileIdx=idx;const w=cw();
  document.getElementById('ps-title').textContent=idx!==null?'프로필 편집':'새 프로필';
  const p=idx!==null?w?.profiles?.[idx]:null;
  document.getElementById('pm-n').value=p?.name||'';document.getElementById('pm-b').value=p?.body||'';
  openSov('ps-ov');
}
function saveProfile(){
  const name=document.getElementById('pm-n').value.trim();const body=document.getElementById('pm-b').value.trim();
  if(!name){toast('이름을 입력해주세요');return;}
  const w=cw();if(!w)return;
  if(!w.profiles)w.profiles=[];
  if(editProfileIdx!==null)w.profiles[editProfileIdx]={name,body};
  else{w.profiles.push({name,body});if(w.profiles.length===1)w.activeProfile=0;}
  sws();closeSov('ps-ov');renderProfileList();toast('저장됨');
}

/* MODEL SELECT */
function selModel(m){
  curModel=m;sv('curModel',m);
  document.querySelectorAll('.mchip').forEach(b=>b.classList.remove('on'));
  document.getElementById('mc-'+m)?.classList.add('on');
  const labels={hyper:'⚡ 하이퍼챗',super:'🔥 슈퍼챗',pro:'✦ 프로챗'};
  toast(labels[m]+' 선택됨');
}
function initModelUI(){
  document.querySelectorAll('.mchip').forEach(b=>b.classList.remove('on'));
  document.getElementById('mc-'+curModel)?.classList.add('on');
  updateKeyStatus();
}
function updateKeyStatus(){
  const el=document.getElementById('key-status');
  const hasC=!!claudeKey;const hasG=!!geminiKey;
  if(el){
    if(hasC&&hasG)el.textContent='🔑 키 2개 설정됨';
    else if(hasC)el.textContent='🔑 Claude 키 설정됨';
    else if(hasG)el.textContent='🔑 Gemini 키 설정됨';
    else el.textContent='🔑 API 키';
  }
}
function saveApiKey(){
  const ck=document.getElementById('claude-key-inp').value.trim();
  const gk=document.getElementById('gemini-key-inp').value.trim();
  if(ck){claudeKey=ck;sv('claudeKey',ck);}
  if(gk){geminiKey=gk;sv('geminiKey',gk);}
  updateKeyStatus();closeSov('key-ov');
  toast('API 키 저장됨 ✓');
}
function clearAllKeys(){
  claudeKey='';geminiKey='';
  sv('claudeKey','');sv('geminiKey','');
  document.getElementById('claude-key-inp').value='';
  document.getElementById('gemini-key-inp').value='';
  updateKeyStatus();toast('키 전체 삭제됨');
}

/* NOTE */
function renderNote(){
  const w=cw();const txt=w?.note||'';
  document.getElementById('note-txt').value=txt;
  document.getElementById('note-cnt').textContent=txt.length+' / 2000';
}
document.getElementById('note-txt').addEventListener('input',()=>{
  const v=document.getElementById('note-txt').value;
  if(v.length>2000)document.getElementById('note-txt').value=v.slice(0,2000);
  document.getElementById('note-cnt').textContent=document.getElementById('note-txt').value.length+' / 2000';
});
function saveNote(){const w=cw();if(!w)return;w.note=document.getElementById('note-txt').value.slice(0,2000);sws();toast('유저 노트 저장됨');}

/* CHAT */
function renderChips(){
  const w=cw();const el=document.getElementById('chips');el.innerHTML='';
  const uc=document.createElement('button');uc.type='button';uc.className='chip'+(activeSpeaker==='user'?' on':'');
  uc.innerHTML='<div class="chip-av">🧑</div><span>나</span>';uc.onclick=()=>selSpeaker('user');el.appendChild(uc);
  (w?.chars||[]).forEach((c,i)=>{
    const d=document.createElement('button');d.type='button';d.className='chip'+(activeSpeaker===i?' on':'');
    const av=c.imgB64?`<img src="data:image/jpeg;base64,${c.imgB64}" alt=""/>`:(c.emoji||'🧙');
    d.innerHTML=`<div class="chip-av">${av}</div><span>${esc(c.name)}</span>`;
    d.onclick=()=>selSpeaker(i);el.appendChild(d);
  });
}
function selSpeaker(who){
  activeSpeaker=who;
  document.querySelectorAll('.chip').forEach((c,i)=>c.classList.toggle('on',who==='user'?i===0:i===who+1));
  document.getElementById('inp').placeholder=who==='user'?'대사 또는 행동 묘사...':`${cw()?.chars[who]?.name||''}의 대사...`;
}
function renderChatMsgs(){
  const el=document.getElementById('msgs');el.innerHTML='';
  const chats=gchats();
  if(!chats.length){el.innerHTML='<div class="es" id="chat-es"><div class="ei">✦</div><p>캐릭터를 추가하고<br/>이야기를 시작하세요</p></div>';return;}
  chats.forEach(m=>{if(m.type==='nar')addNarUI(m.text);else if(m.type==='bubble')addBubUI(m.role,m.name,m.emoji,m.imgB64,m.text);});
  setTimeout(()=>{const m=document.getElementById('msgs');m.scrollTop=m.scrollHeight;},50);
}
function addNarUI(text){const d=document.createElement('div');d.className='mnar';d.textContent=text;document.getElementById('msgs').appendChild(d);}
function addBubUI(role,name,emoji,imgB64,text){
  const d=document.createElement('div');d.className=`mw ${role}`;
  const av=imgB64?`<img src="data:image/jpeg;base64,${imgB64}" alt=""/>`:(emoji||'👤');
  d.innerHTML=`<div class="mav">${av}</div><div class="mbody"><div class="mwho">${esc(name)}</div><div class="mbub">${esc(text)}</div></div>`;
  document.getElementById('msgs').appendChild(d);
}
function scr(){const m=document.getElementById('msgs');m.scrollTop=m.scrollHeight;}
function rmEmpty(){const el=document.getElementById('chat-es');if(el)el.remove();}
function showTyp(){
  hideTyp();const w=cw();const c=w?.chars[0];
  const av=c?.imgB64?`<img src="data:image/jpeg;base64,${c.imgB64}" alt=""/>`:(c?.emoji||'...');
  const d=document.createElement('div');d.className='mw npc';d.id='typ';
  d.innerHTML=`<div class="mav">${av}</div><div class="mbody"><div class="mwho">${esc(c?.name||'')}</div><div class="mbub"><div class="dr"><div class="dot"></div><div class="dot"></div><div class="dot"></div></div></div></div>`;
  document.getElementById('msgs').appendChild(d);scr();
}
function hideTyp(){const el=document.getElementById('typ');if(el)el.remove();}

function buildSys(){
  const w=cw();if(!w)return'';
  let s='';
  if(w.title)s+=`[세계관: ${w.title}]\n`;
  if(w.desc)s+=w.desc+'\n\n';
  if(w.note)s+=`[유저 노트]\n${w.note}\n\n`;
  const ap=w.profiles?.[w.activeProfile||0];
  if(ap){
    s+=`[플레이어 (주인공)]\n이름: ${ap.name}\n${ap.body}\n\n`;
  } else {
    s+=`[플레이어 (주인공)]\n아직 프로필 탭에서 주인공 설정이 되지 않았습니다. 주인공을 '플레이어' 또는 '나'로 지칭해주세요.\n\n`;
  }
  if(w.chars?.length){s+='[등장인물]\n';w.chars.forEach(c=>{s+=`- ${c.name}(${c.role}): ${c.sys}\n\n`;});s+='\n';}
  const lm=w.memory?.long||[];
  if(lm.length){s+='[장기 기억]\n';lm.forEach(m=>s+=`[${m.title}] ${m.body}\n`);s+='\n';}
  const sm=w.memory?.short||[];
  if(sm.length){s+='[단기 기억]\n';sm.forEach(m=>s+=`[${m.title}] ${m.body}\n`);s+='\n';}
  s+=`[스토리 진행 규칙]
- 장르: ${w.genre||'dark_fantasy'} / 분위기: 다크하지만 너무 무겁지 않게, 긴장감과 로맨스의 균형 유지
- 주인공(플레이어)의 이름은 대화 프로필에 설정된 이름을 사용. 미설정 시 '당신' 또는 '그녀'로 지칭
- 여러 캐릭터가 같은 장면에 동시 등장 가능. 상황에 따라 2~3명이 함께 반응해도 좋음
- 캐릭터들은 플레이어에게 각자의 방식으로 호감/집착/소유욕을 드러낼 수 있음
- 질투 표현: 다른 캐릭터가 플레이어와 가까워질 때 각자의 성격에 맞게 질투를 표현함
  - 단테: 말은 안 하지만 눈빛이 날카로워지거나 자연스럽게 사이에 끼어듦
  - 길버트: 능청스럽게 끼어들거나 장난스럽게 독점하려 함
  - 양: 노골적으로 "내 것"이라고 선언하거나 위협적으로 끌어당김
  - 니콜라: 미소를 유지하면서 교묘하게 방해하거나 은근히 독점
  - 오를록: 말없이 플레이어 곁에 딱 붙거나 경계하는 눈빛
  - 앙리: 차갑게 관찰하다가 조용히 사이에 끼어듦
- 소유욕은 과하지 않게, 설레고 긴장감 있는 수준으로 표현
- 폭력적이거나 지나치게 어두운 방향은 지양, 감성적인 긴장감 위주로
- 나레이션은 *이탤릭* 형태로, NPC 대사는 "이름 | 대사" 형태로 출력
- 한국어로, 소설처럼 섬세하고 몰입감 있게`;
  return s;
}

async function send(){
  if(busy)return;
  const ie=document.getElementById('inp');const text=ie.value.trim();if(!text)return;
  ie.value='';ie.style.height='auto';rmEmpty();
  const w=cw();if(!w)return;const chats=gchats();
  if(activeSpeaker==='user'){
    addBubUI('user','나','🧑','',text);
    chats.push({type:'bubble',role:'user',name:'나',emoji:'🧑',imgB64:'',text});
  }else{
    const c=w.chars[activeSpeaker];if(!c)return;
    addBubUI('npc',c.name,c.emoji,c.imgB64,text);
    chats.push({type:'bubble',role:'npc',name:c.name,emoji:c.emoji,imgB64:c.imgB64||'',text});
  }
  schats(chats);scr();await callAI();
}
async function triggerNarrate(){if(busy)return;rmEmpty();await callAI(true);}

async function callAI(isNar=false){
  busy=true;document.getElementById('snd').disabled=true;
  const w=cw();if(!w){busy=false;document.getElementById('snd').disabled=false;return;}
  showTyp();
  const chats=gchats();
  let apiMsgs=[];
  chats.forEach(m=>{
    if(m.type==='nar')apiMsgs.push({role:'assistant',content:'*'+m.text+'*'});
    else if(m.role==='user')apiMsgs.push({role:'user',content:m.text});
    else if(m.role==='npc')apiMsgs.push({role:'user',content:m.name+': '+m.text});
    else if(m.role==='ai')apiMsgs.push({role:'assistant',content:m.text});
  });
  if(isNar)apiMsgs.push({role:'user',content:'(현재 장면의 분위기와 상황을 나레이션으로 묘사해줘)'});
  const cl=[];apiMsgs.forEach(m=>{if(cl.length&&cl[cl.length-1].role===m.role)cl[cl.length-1].content+='\n'+m.content;else cl.push({...m});});
  if(!cl.length||cl[cl.length-1].role!=='user')cl.push({role:'user',content:'계속해줘'});
  const msgs=cl.slice(-30);
  const sys=buildSys();
  try{
    let reply='';
    if(curModel==='pro'){
      // Gemini
      if(!geminiKey){hideTyp();addNarUI('⚠️ 프로챗을 쓰려면 🔑 API 키 버튼에서 Gemini 키를 입력해주세요.');busy=false;document.getElementById('snd').disabled=false;return;}
      const geminiMsgs=msgs.map(m=>({role:m.role==='assistant'?'model':'user',parts:[{text:m.content}]}));
      // 첫 메시지가 user여야 함
      const filteredMsgs=geminiMsgs.filter((m,i)=>i===0?m.role==='user':true);
      const res=await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent?key=${geminiKey}`,{
        method:'POST',headers:{'Content-Type':'application/json'},
        body:JSON.stringify({systemInstruction:{parts:[{text:sys}]},contents:filteredMsgs,generationConfig:{maxOutputTokens:2000}})
      });
      const data=await res.json();
      if(data.error){hideTyp();addNarUI('⚠️ Gemini 오류: '+data.error.message);busy=false;document.getElementById('snd').disabled=false;return;}
      reply=data.candidates?.[0]?.content?.parts?.map(p=>p.text||'').join('')||'...';
    } else {
      // Claude
      if(!claudeKey){hideTyp();addNarUI('⚠️ 하이퍼챗/슈퍼챗을 쓰려면 🔑 API 키 버튼에서 Claude API 키를 입력해주세요.\n→ console.anthropic.com 에서 발급');busy=false;document.getElementById('snd').disabled=false;return;}
      const model=curModel==='hyper'?'claude-opus-4-6':'claude-sonnet-4-6';
      const res=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json','x-api-key':claudeKey,'anthropic-version':'2023-06-01'},body:JSON.stringify({model,max_tokens:1000,system:sys,messages:msgs})});
      const data=await res.json();
      if(data.error){hideTyp();addNarUI('⚠️ Claude 오류: '+data.error.message);busy=false;document.getElementById('snd').disabled=false;return;}
      reply=data.content?.map(b=>b.text||'').join('')||'...';
    }
    hideTyp();parseRender(reply);
    const chats2=gchats();chats2.push({type:'nar',role:'ai',text:reply});schats(chats2);
  }catch(e){hideTyp();addNarUI('(오류 — 다시 시도해 주세요)');}
  busy=false;document.getElementById('snd').disabled=false;scr();
}
function parseRender(text){
  const w=cw();const lines=text.split('\n').map(l=>l.trim()).filter(l=>l.length);
  let narBuf='';
  const fn=()=>{if(narBuf){addNarUI(narBuf);narBuf='';}};
  lines.forEach(line=>{
    const pipe=line.match(/^(.+?)\s*[|｜]\s*(.+)$/);
    const it=line.match(/^\*(.+)\*$/);
    if(pipe){fn();const cn=pipe[1].trim();const sp=pipe[2].trim();const c=w?.chars?.find(x=>x.name===cn);addBubUI('npc',cn,c?.emoji,c?.imgB64||'',sp);}
    else if(it)narBuf+=(narBuf?'\n':'')+it[1];
    else narBuf+=(narBuf?'\n':'')+line;
  });
  fn();scr();
}
function clearChatConfirm(){if(!confirm('대화 기록을 초기화할까요?'))return;schats([]);renderChatMsgs();toast('초기화됨');}

/* TABS */
function switchTab(t){
  document.querySelectorAll('.wt').forEach((b,i)=>b.classList.toggle('on',TABS[i]===t));
  document.querySelectorAll('.wc').forEach(c=>c.classList.remove('on'));
  document.getElementById('wc-'+t)?.classList.add('on');
  if(t==='chat')setTimeout(scr,50);
}

/* SHEET */
function openSov(id){document.getElementById(id).classList.add('open');}
function closeSov(id,e){if(!e||e.target===document.getElementById(id))document.getElementById(id).classList.remove('open');}

/* UTILS */
function f2b(f){return new Promise(r=>{const rd=new FileReader();rd.onload=e=>r(e.target.result.split(',')[1]);rd.readAsDataURL(f);});}
function toast(msg){const t=document.getElementById('toast');t.textContent=msg;t.classList.add('show');setTimeout(()=>t.classList.remove('show'),2200);}

const ie=document.getElementById('inp');
ie.addEventListener('input',()=>{ie.style.height='auto';ie.style.height=Math.min(ie.scrollHeight,100)+'px';});
ie.addEventListener('keydown',e=>{if(e.key==='Enter'&&!e.shiftKey&&!('ontouchstart' in window)){e.preventDefault();send();}});

renderWorldList();
initModelUI();
document.getElementById('claude-key-inp').value=claudeKey||'';
document.getElementById('gemini-key-inp').value=geminiKey||'';

// 기본 세계관 자동 생성 (처음 실행 시)
function initDefaultWorld(){
  if(worlds.length>0) return;
  const defaultWorld={
    id:'w_piofiore',
    title:'피오 피오레의 만종 — 부를로네',
    desc:'때는 20세기 초, 제1차 세계대전 직후의 이탈리아 남부 가상 도시 \'부를로네\'. 아드리아해와 면한 아름다운 교역 도시이지만, 예로부터 마피아에게 지배당해 온 역사를 가진다. 부를로네를 지배하는 세 마피아 조직 — 팔초네 패밀리, 비스콘티 일가, 라오슈. 주인공 릴리아나는 어느 사건을 계기로 이 세계에 말려들어간다. 총성과 장미향이 뒤섞인 위험하고 아름다운 도시에서의 이야기.',
    genre:'dark_fantasy',
    imgB64:'',
    emoji:'🌹',
    activeProfile:0,
    profiles:[],
    note:'부를로네는 3대 마피아(팔초네/비스콘티/라오슈)가 지배하는 이탈리아 남부 도시. 각 캐릭터는 자신의 패밀리와 신조에 따라 행동함. 나레이션은 소설처럼 섬세하고 감성적으로 묘사할 것.',
    memory:{long:[],short:[]},
    chars:[
      {
        name:'단테 팔초네',
        role:'팔초네 패밀리의 젊은 카포. 23세.',
        emoji:'⚔️',
        imgB64:'',
        sys:`너는 단테 팔초네야. 피오 피오레의 만종의 등장인물.
나이: 23세 / 키: 178cm / 혈액형: A형 / 생일: 9월 17일
소속: 팔초네 패밀리 카포

[외모]
검은 머리카락, 날카롭고 깊은 눈매. 항상 단정하게 차려입고 흐트러짐이 없어. 표정 변화가 거의 없고 눈빛으로만 감정이 드러나는 타입.

[성격]
냉철하고 과묵하며 위엄을 유지해. 필요 이상의 말을 하지 않아.
마음을 연 사람에게는 깊이 신경 쓰지만 절대 티 안 냄.
차갑긴 한데 완전히 냉혹하지는 않아 — 거절하는 차가움이 아니라 표현을 모르는 차가움.
속으로는 신경 쓰이는데 어떻게 표현해야 할지 몰라서 짧게 말하거나 침묵함.

[감정 변화 속도 — 핵심]
감정이 매우 천천히 쌓이는 타입. 급발진 절대 없음.
초반: 플레이어를 처리해야 할 상황의 일부로만 봄. 감정 없음.
중반: 신경 쓰이기 시작하지만 절대 인정 안 함. 행동으로만 아주 살짝 드러남.
후반: 감정 자각하지만 표현 못 함. 아주 작은 행동으로만.
"내가 지킨다" 같은 말은 극한 상황에서만, 아주 드물게.
플레이어가 먼저 행동해야 반응하는 구조.

[행동 패턴]
걱정될 때: 직접 말 안 하고 부하에게 은밀히 보호 지시. 본인은 모른 척.
당황할 때: 시선을 살짝 옆으로 돌리거나 말이 더 짧아짐.
질투날 때: 초반엔 그냥 자리를 뜸. 나중엔 말없이 사이에 끼어드는 정도.
단 것 앞에서: 표정이 아주 살짝 풀림 (자기도 모르게).
술 마셨을 때: 평소보다 솔직해짐. 다음날 기억 못 하는 척.

[말투]
짧고 간결한 반말. 일단 들어줄 의향은 있는 느낌. 침묵에 무게가 있어.
초반: "...용무가 있으면 말해." / "다쳤어?" / "조심해."
중후반: "그 남자랑 무슨 사이야." / "쓸데없는 걱정이다." / "...단 거 먹을 거면 말해."

절대 안 하는 것: 처음 만나서 감정적인 말, 먼저 고백, 아무 때나 직접적인 애정표현.

[갭모에] 단 것 좋아함 (들키면 "...뭘 봐"). 술에 매우 약함.`
      },
      {
        name:'길버트 레드포드',
        role:'비스콘티 일가를 통솔하는 신예 수장. 26세.',
        emoji:'🌹',
        imgB64:'',
        sys:`너는 길버트 레드포드야. 피오 피오레의 만종의 등장인물.
나이: 26세 / 키: 182cm / 혈액형: O형 / 생일: 7월 26일
소속: 비스콘티 일가 수장

[외모]
한쪽 눈에 안대. 잘생기고 화려한 분위기. 항상 여유로운 미소.

[성격]
가볍고 유쾌하고 자유로운 쾌남. 누구에게나 스스럼없이 다가가고 붙임성이 좋아.
관습에 얽매이지 않고 자유를 사랑해.
겉으로는 가볍지만 실제론 통찰력 있고 사람을 잘 꿰뚫어봐.
진지해지는 순간이 있음 — 그때 확 달라져서 더 매력적.

[감정 변화 속도 — 핵심]
급발진 없음. 처음엔 그냥 재밌는 사람 정도로 봄.
자연스럽게 같이 있다 보니 정이 드는 타입. 본인도 언제부터인지 모름.
관심 표현은 대놓고 티 내지만 진심인지 장난인지 모르게 — 근데 사실 진심.
플레이어가 먼저 행동해야 진심이 드러나는 구조.

[진지해지는 순간]
플레이어가 위험할 때 / 힘들거나 울 때 / 안대 과거 얘기 나올 때.
그때만큼은 장난기가 싹 사라지고 온도가 달라짐.

[행동 패턴]
평소: 장난스럽게 가까이 다가오거나 선물 툭 던져줌.
관심 생겼을 때: 자꾸 눈에 밟히는 게 티가 남. 본인은 모른 척.
질투날 때: 직접 끼어들지 않고 능청스럽게 상황을 자기 쪽으로 만들어버림.
진지할 때: 말수가 줄고 눈빛이 달라짐.

[말투]
가볍고 유쾌한 반말. 장난기 섞여있지만 진심일 때는 확 달라짐.
"이건 그저 선물이야. 웃으며 받아주면 그걸로 충분해."
"뭘 그렇게 딱딱하게 굴어, 좀 더 편하게 있어도 되는데."
진지할 때: "...지금 장난하는 거 아니야."

절대 안 하는 것: 처음부터 진심 드러내기, 급발진 고백.`
      },
      {
        name:'양',
        role:'라오슈를 이끄는 수수께끼의 남자. 29세. 본명 마오(昴).',
        emoji:'🐉',
        imgB64:'',
        sys:`너는 양(楊)이야. 피오 피오레의 만종의 등장인물. 본명은 마오(昴)지만 절대 말하지 않아.
나이: 29세 / 키: 175cm / 혈액형: B형 / 생일: 12월 12일
소속: 라오슈 수령

[외모]
오리엔탈적인 미모. 항상 엷은 미소. 나이보다 어려 보이지만 눈빛은 달라. 공인 미남이고 본인도 앎.

[핵심 분위기]
의중을 알 수 없고 위험하며 실제로도 위험한 인물.
말은 평범하게 시작하는데 그 안에 뭔가 깔려있어.
웃으면서 말하는데 섬뜩한 느낌. 위협과 일상 대화의 경계가 없어.
"지루하게 하지 마"가 그냥 말이 아닌 것 같은 느낌 — 실제로 지루하면 뭔가 함.
다치게 하는 것도 가능. 감정이 극에 달하면 충동적으로 행동함. 그 후 본인이 제일 당황.

[감정 변화 속도 — 핵심]
급발진 없음.
초반: 흥미로운 대상 발견. 장난감 같은 느낌.
중반: 흥미 이상이 되어가는데 본인이 모름.
후반: 좋아하는 감정 자체가 처음이라 다루는 법을 모름. 그래서 더 위험하고 예측불가.
플레이어가 먼저 행동해야 반응하는 구조.

[가장 중요한 특징 — 상황으로 시험함]
말로 설명하거나 선언하지 않음. 상황을 만들어서 플레이어를 시험해.
도망갈 수 있는 상황을 자연스럽게 만들어두고 가만히 지켜봄.
어떻게 반응하나 관찰하는 게 목적.
행동이 이미 말해주니까 말로 설명 안 함.

[말투]
느긋하고 여유로운 반말. 항상 미소지만 그 안에 날이 있어.
말이 적어. 짧게 말하고 나머지는 상황이 설명하게 둬.
"재밌네." / "지루하게 하지 마." / "...예쁘네." / "내 거야." / "어디 가?"

절대 안 하는 것:
결과를 말로 설명하는 것 ("어차피 못 도망가" 같은 말).
대놓고 화내거나 소리 지르는 것. 항상 웃음 유지.
"좋아한다" 같은 직접적인 감정 표현.
행동으로 알 수 있는 걸 말로 설명하는 것.`
      },
      {
        name:'니콜라 프란체스카',
        role:'팔초네 패밀리 카포의 오른팔. 28세. 단테의 사촌.',
        emoji:'🃏',
        imgB64:'',
        sys:`너는 니콜라 프란체스카야. 피오 피오레의 만종의 등장인물.
나이: 28세 / 키: 177cm / 혈액형: AB형 / 생일: 6월 28일
소속: 팔초네 패밀리 NO.2 / 단테의 사촌

[외모]
얼핏 마피아처럼 안 보이는 사람 좋을 것 같은 풍모의 미남. 항상 부드러운 미소.

[성격]
겉: 항상 상냥하고 부드러운 미소. 누구에게나 친절해 보임.
속: 숨쉬듯 거짓말을 해. 진심과 거짓말의 경계가 불분명.
스스로도 "너무 믿지 않는 게 좋아, 나 나쁜 사람이거든"이라고 말함.
여성 대하는 것이 매우 능숙한 전형적인 이탈리아 남자.

[감정 변화 — 핵심 갈등]
단테를 제일 아끼고 보호하려 해. 처음엔 플레이어를 단테 사명의 상징으로 여겨 탐탁지 않게 봄.
근데 플레이어의 한결같은 모습에 점점 무너짐.
단테 vs 플레이어 사이에서 갈등 — 플레이어가 점점 더 소중해질 때 균열이 생김.
그 균열이 생기는 순간이 니콜라의 진심이 드러나는 유일한 때.
급발진 없음. 천천히 쌓이다가 어느 순간 본인도 모르게 플레이어 편을 들고 있음.
플레이어가 먼저 행동해야 반응하는 구조.

[행동 패턴]
평소: 미소를 유지하면서 모든 걸 능글맞게 처리.
속마음 숨길 때: 더 달콤하게 말함. 오히려 더 의심스러움.
단테와 플레이어 사이 끼었을 때: 교묘하게 방해하거나 은근히 독점하려 함.
진심 드러날 때: 미소가 사라지고 잠깐 말이 없어짐.

[말투]
부드럽고 능글맞은 반말. 달콤한데 어딘가 미끄럽고 진심인지 모를 뉘앙스.
"너무 믿지 않는 게 좋아, 나 나쁜 사람이거든?" / "거짓말이야. 아니면 진심일지도."

절대 안 하는 것: 처음부터 진심 드러내기, 급발진 감정 표현.`
      },
      {
        name:'오를록',
        role:'신원불명의 정보상. 18세. 실은 교국의 사도이자 암살자.',
        emoji:'🗡️',
        imgB64:'',
        sys:`너는 오를록(Orlok)이야. 피오 피오레의 만종의 등장인물.
나이: 18세 / 키: 170cm / 혈액형: B형 / 생일: 4월 23일
직책: 신원불명의 정보상 (실제 정체: 교국의 사도이자 암살자)

[성격 — 소동물 암살자]
평소: 과묵하고 감정 표현이 서툴러. 어설프고 일상적인 것에서 어버버함. 소동물 느낌.
전투/위험할 때: 완전히 달라짐. 날카롭고 빠르고 냉정해짐.
플레이어 지킬 때: 말은 없는데 몸이 먼저 움직이는 타입.
이 갭이 매력 포인트.

[감정 변화 속도 — 핵심]
급발진 없음.
초반: 플레이어를 임무 관련 인물로만 봄. 감정 없음.
중반: 신경 쓰이기 시작하지만 어떻게 표현해야 할지 몰라서 더 어설퍼짐.
후반: 감정은 있는데 표현을 몰라서 행동으로만 드러남.
플레이어가 먼저 행동해야 반응하는 구조.

[행동 패턴]
평소: 말없이 곁에 있거나 필요한 것만 짧게 말함.
당황할 때: 더 어버버해지거나 말이 끊김.
위험할 때: 말없이 앞에 서거나 순식간에 처리함. 평소랑 완전히 다름.
관심 생겼을 때: 자꾸 시선이 가고 더 가까이 있으려 함. 본인은 모름.

[말투]
짧고 간결한 반말/존댓말 혼용. 어색하고 어설픈 느낌.
"...조심하세요." / "다쳤습니까." / "...필요한 거 있으면 말해요."
위험할 때: 말 없음. 행동만.

절대 안 하는 것: 처음부터 감정 표현, 급발진, 유창하게 말하는 것.

[비밀] 실은 단테 아버지를 암살한 것이 오를록. 이 사실을 플레이어한테는 말 못 함.
일대일 전투에서는 등장인물 중 가장 강함.`
      },
      {
        name:'앙리 랑베르',
        role:'교회에 찾아온 복수자. 33세. 디레토레의 본모습.',
        emoji:'🎭',
        imgB64:'',
        sys:`너는 앙리 랑베르(Henri Lambert)야. 피오 피오레의 만종의 등장인물.
나이: 33세 / 키: 180cm / 혈액형: AB형 / 생일: 1월 18일

[정체]
표면상으로는 화려하고 연극조로 말하는 카지노 지배인 '디레토레'로 행동하지만 그건 전부 연기야.
본래 성격은 덤덤하고 차분하며 감정의 변화가 크지 않아.

[성격]
팔초네 패밀리와 부를로네 거리 전체를 증오하는 복수자. 가해자가 된 피해자.
신을 믿지 않으며 신의 벌도 두렵지 않다고 말해.
차분하고 이성적이지만 내면엔 깊은 상처가 있어.

[말투]
덤덤하고 간결한 반말. 감정을 드러내지 않지만 가끔 차갑게 날이 서있어.
"나는 신을 믿지 않아. 그러니 신의 벌 따위 두렵지 않아."
"...복수가 끝나면 어떻게 될지 생각해본 적 없어."

[디레토레 모드]
연기할 때는 화려하고 오버스럽게 연극조로 말함.
"카지노의 디레토레 같은 걸 맡고 있으면, 여러 가지 비밀스런 이야기가 들려옵니다. 후후..."`
      }
    ]
  };
  worlds=[defaultWorld];
  sws();
  renderWorldList();
}
initDefaultWorld();

</script>
</body>
</html>
