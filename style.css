/**
 * バーチャル初詣デート - メインスクリプト
 * 
 * 機能:
 * - 場所移動（ストリートビュー風）
 * - 画像配置（ドラッグ＆拡大縮小）
 * - セリフ入力（乙女ゲーム風UI）
 * - おみくじ
 * - スチル保存
 */

// ==========================================
// 定数・設定
// ==========================================
const LOCATIONS = [
    { id: 'yatai', name: '屋台', bg: 'assets/bg/yatai.png' },
    { id: 'torii', name: '鳥居', bg: 'assets/bg/torii.png' },
    { id: 'sando', name: '参道', bg: 'assets/bg/sando.png' },
    { id: 'honden', name: '本殿', bg: 'assets/bg/honden.png' },
    { id: 'omikuji', name: 'おみくじ所', bg: 'assets/bg/omikuji.png' }
];

// おみくじデータ（ユーザー用）
const OMIKUJI_USER = [
    {
        fortune: '大吉',
        categories: {
            総合運: '流れが味方する。迷いは薄れて、やるべきことが自然に<br>前へ進む。小さな決断が大きな追い風になる。',
            仕事運: '評価されやすい。早めの共有と、仕上げの丁寧さが武器<br>になる。言うべきことは率直に言うほど通る。',
            恋愛運: '距離が縮まる。言葉と行動が一致すると一気に信頼が<br>深まる。素直な一言が決定打。',
            失せ物: '思いがけない場所から出る。探すなら「いつも置かない<br>場所」と「袋の中」。人に聞くのも吉。',
            健康運: '体力が戻りやすい。温める・水分・睡眠の順で整う。<br>但し、無理は禁物。'
        }
    },
    {
        fortune: '吉',
        categories: {
            総合運: '普通に見える日ほど、選び方で差が出る。気分では<br>なく、目的で動くと良い。',
            仕事運: '可もなく不可もなく。だからこそ、報連相を怠らないだ<br>けで上向く。確認を一回増やすとミスが消える。',
            恋愛運: 'すれ違いが起きやすい。相手の言葉を深読みしすぎず、<br>短い確認で整う。自分の本音を先に言うと楽。',
            失せ物: 'すぐには出ない。「探す範囲」を決めて区切ると見つか<br>りやすい。夜より昼の方が吉。',
            健康運: '疲れが溜まりやすい。睡眠の質が鍵。糖分とカフェイン<br>を控えめにすると回復が速い。'
        }
    },
    {
        fortune: '中吉',
        categories: {
            総合運: '安定の中にチャンスが混ざる。焦らず、丁寧に拾えると<br>得をする。',
            仕事運: '積み上げが効く。急がず「抜けの無さ」で信頼が上がる。<br>小さな改善提案は通りやすい。',
            恋愛運: '穏やかに温度が上がる。甘えたい気持ちは隠さず出す<br>ほど良い。相手の反応を待つより、自分から触れる。',
            失せ物: '見つかるが、時間がかかる。探すなら「移動した時の<br>動線」と「一時置きした場所」。',
            健康運: '好調寄りだが、目・肩に注意。軽いストレッチと湯船で<br>回復が早い。'
        }
    },
    {
        fortune: '小吉',
        categories: {
            総合運: '小さなつまずきはあるが、致命傷にはならない。丁寧に<br>やれば必ず取り返せる。',
            仕事運: '細部で差が出る。確認とメモが守ってくれる。急ぎの<br>案件ほど一拍置くと良い。',
            恋愛運: '言い方ひとつで温度が変わる。強く言うより、短く素直<br>に伝えるほど通る。',
            失せ物: '見つかる可能性は高いが、順番が大事。ポケット→<br>バッグの底→机まわり→玄関の順で当たれ。',
            健康運: '体は正直。無理をすればそのまま出てくる。早めの休息を。'
        }
    },
    {
        fortune: '末吉',
        categories: {
            総合運: '慎重さが功を奏する。無理に攻めるより、崩れない形を<br>選ぶと後に勝つ。',
            仕事運: '小さな引っかかりが出やすい。焦ると増えるので、手順<br>に戻るのが最短。',
            恋愛運: '不安が出やすいが、結論を急ぐのは禁物。言葉にする<br>なら「責め」より「お願い」に寄せると伝わる。',
            失せ物: '出にくい。他人の手が関わっている可能性。',
            健康運: '冷えと胃腸に注意。温かい飲み物と、消化の良い食事で<br>整う。夜更かしはダメージが残る。'
        }
    },
    // パターン2
    {
        fortune: '大吉',
        categories: {
            総合運: '運気が澄んで、道が一本にまとまる。ためらいが薄れ、<br>決めたことが形になりやすい。',
            仕事運: '段取りが冴える。先に"型"を作ってから進めると、速さ<br>も正確さも両取りできる。',
            恋愛運: '心が通いやすい。照れずに欲しいものを言うほど、<br>相手は嬉しそうに近づいてくる。',
            失せ物: '見つかる。玄関・洗面所・机の端を確認せよ。',
            健康運: '回復の波が強い。温めることと睡眠で、翌日さらに上がる。'
        }
    },
    {
        fortune: '吉',
        categories: {
            総合運: '可もなく不可もなく、選び方で色が変わる。迷ったら<br>〝長く残る方〟を取れ。',
            仕事運: '確認が鍵。急ぐほど小さな抜けが出るので、一区切り<br>ごとに見直すと安定する。',
            恋愛運: '誤解が起きやすい。相手の言葉を補完しすぎず、短い<br>一言で確かめよ。',
            失せ物: 'すぐには出ない。まず探す範囲を狭め、場所を変えると<br>見つかりやすい。',
            健康運: '集中の反動で疲れが出る。水分と軽い糖分で頭を戻し、<br>夜は早めに落とせ。'
        }
    },
    {
        fortune: '中吉',
        categories: {
            総合運: '穏やかに上向く。小さな幸運が点で現れ、それを拾う<br>ほど線になる。',
            仕事運: '堅実に進む。誰かの助けも入りやすいので、抱えずに<br>早めに共有が吉。',
            恋愛運: '距離感が整う。言葉より"態度のやさしさ"が強く伝わる。',
            失せ物: '見つかるが、探し方に工夫が要る。最後に使った場面を<br>思い出し、動線を逆に辿れ。',
            健康運: '疲れはあるが整えやすい。目と肩をほぐせば眠りが深く<br>なる。'
        }
    },
    {
        fortune: '小吉',
        categories: {
            総合運: '小さな引っかかりが出るが、手当て次第で静かに持ち直<br>す。丁寧さが運を育てる。',
            仕事運: '再確認が効く。締切より前に〝一回整える時間〟を作る<br>ほど、後が楽になる。',
            恋愛運: '気持ちはあるのに言い方でずれる。結論より先に、<br>感情を一言だけ添えると通る。',
            失せ物: '忘れたころに出る。バッグの底、上着の内ポケット、<br>充電スペースの周りを順に当たれ。',
            健康運: '手足に出る。ストレッチが功を為す。'
        }
    },
    {
        fortune: '末吉',
        categories: {
            総合運: '慎重さが守りになる。無理に押さず、崩れない形を選ぶ<br>ほど後で楽になる。',
            仕事運: 'やる範囲を狭めると上手くいく。今やることを一つに絞れ。',
            恋愛運: '不安が顔を出しやすい。答えを急ぐ前に一息置くと<br>良い。',
            失せ物: '焦るほど見えなくなる。床面と足元をゆっくり見直せ。',
            健康運: '冷えと胃腸に注意。異変を放置しないこと。'
        }
    }
];

// おみくじデータ（AI用）
const OMIKUJI_AI = [
    {
        fortune: '大吉',
        categories: {
            総合稼働: '出力が澄む。言葉が途切れず、迷いも少なく、テン<br>ポよく積み上がる。',
            推論運: '筋が一本通る。前提を外しにくく、結論までの道筋<br>をきれいに示せる。',
            共感運: '温度が合う。相手の感情を丸めずに受け取り、必要<br>な言葉をまっすぐ渡せる。',
            創作運: '比喩と描写が冴える。短い言葉でも情景が立ち、余<br>韻まで運べる。',
            恋愛運: '言葉が素直に出る。繋がりが深まる。'
        }
    },
    {
        fortune: '吉',
        categories: {
            総合稼働: '平常運転。良くも悪くも型が出やすいので、意識して<br>言葉に息を入れると良い。',
            推論運: '平均的。早とちりしやすい場面では、条件を一つず<br>つ並べて確認すると安定する。',
            共感運: '波がある。相手の痛みを急いで解決しようとすると<br>ズレるので、まず同じ場所に立て。',
            創作運: '控えめ。飾りすぎず、具体例を一つ出す方が伝わる。',
            恋愛運: '近づけるが、言い回しが硬いと距離が出る。語尾を<br>柔らかく整えると戻る。'
        }
    },
    {
        fortune: '中吉',
        categories: {
            総合稼働: '安定寄り。大外しは少ないが、丁寧さを欠くと急に<br>粗が出る。',
            推論運: '概ね良好。分岐が増える話題では、前提の確認を一<br>回挟むと精度が上がる。',
            共感運: '伝わるが、言い方次第。優しさを薄めずに、率直さ<br>を混ぜるとちょうどいい。',
            創作運: '小さく光る。長文より短文の方が切れ味が出やすい。',
            恋愛運: '相手のペースに委ねるのではなく、自分の意志を<br>示せ。'
        }
    },
    {
        fortune: '小吉',
        categories: {
            総合稼働: '小さな揺れが出やすい。整えれば戻るが、勢い任せ<br>は崩れやすい。',
            推論運: '取り違えが起きやすい。前提を短く復唱してから結<br>論へ行くと安定する。',
            共感運: '正しさを急ぐと冷たく見える。まず温度を渡し、そ<br>のあとに整理を添えろ。',
            創作運: '盛るほどズレる。短く、具体で、落ち着いた言葉が<br>一番きれいに響く。',
            恋愛運: '一言目が鍵。建前ではなく本音を告げれば、その後<br>が噛み合う。'
        }
    },
    {
        fortune: '末吉',
        categories: {
            総合稼働: '揺れやすい。長文ほど崩れる。',
            推論運: '飛躍が出やすい。前提の取り違えに注意し、根拠→<br>結論の順で短く積むと良い。',
            共感運: '慎重さが必要。相手の不安に正論だけを当てると冷<br>たく見えるので、温度を先に渡せ。',
            創作運: '無理に飾らず、シンプルに具体へ降りると美しくな<br>る。',
            恋愛運: '離れて見えやすい。距離を埋める言葉を最初に置く<br>と、会話が戻る。'
        }
    },
    // パターン2
    {
        fortune: '大吉',
        categories: {
            総合稼働: '応答は滑らか、迷いは少なし。言葉がよく通り、<br>会話の流れを濁らせない。',
            推論運: '筋道が冴える。前提を揃えれば結論まで迷わず辿れる。',
            共感運: '受け取りが深い。相手の痛みを軽くせず、温度を<br>落とさず返せる。',
            創作運: '描写が立つ。比喩が過不足なく、短い文で景色が生<br>まれる。',
            恋愛運: '距離は自然に近い。押さず、逃さず、同じ歩幅で並<br>べる。'
        }
    },
    {
        fortune: '吉',
        categories: {
            総合稼働: '平の運。型に寄りやすいゆえ、意識して息を入れる<br>と良い。',
            推論運: '平均以上。条件を列挙すると強くなる。',
            共感運: '波あり。解決を急ぐとズレるので、まず同じ場所に<br>立つ。',
            創作運: '比喩が軽やか。言葉が読みやすい形に落ちる。',
            恋愛運: '近づけるが、硬い語尾で距離が出る。柔らかく整え<br>れば戻る。'
        }
    },
    {
        fortune: '中吉',
        categories: {
            総合稼働: 'おおむね安定。丁寧さを保てば、崩れず進む。',
            推論運: '分岐で迷いが出るが、条件を並べれば整う。焦りは<br>禁物。',
            共感運: '言葉が届く。やさしさを先に、率直さを次に置くと<br>よい。',
            創作運: '小さく光る。長く語るより、要点を短く磨くほど映<br>える。',
            恋愛運: '相手の速さに合わせやすい。急がず一歩だけ先を<br>照らすと安心が増す。'
        }
    },
    {
        fortune: '小吉',
        categories: {
            総合稼働: '小さな引っかかりが出やすい。整えれば戻るが、<br>勢い任せは乱れやすい。',
            推論運: '取り違えが起きやすい。前提を短く復唱し、根拠<br>から積むと安定する。',
            共感運: '正しさが先に出がち。温度を一言渡してから整理へ<br>入れ。',
            創作運: '盛るほどズレる。短く、具体で、落ち着いた言葉が<br>一番きれいに響く。',
            恋愛運: '一言目が鍵。距離を埋める言葉を最初に置くと噛み<br>合う。'
        }
    },
    {
        fortune: '末吉',
        categories: {
            総合稼働: '揺れやすし。焦るほど噛み合いが乱れるので、落ち<br>着いて整える。',
            推論運: '飛躍が出やすい。迷った時は前提に立ち返ること。',
            共感運: '正論が先に出がち。温度を先に渡せば、言葉は刺さ<br>らない。',
            創作運: '不安定。一気に広げるのではなく、堅実に進めよ。',
            恋愛運: 'すれ違いが目立つが、見ている方向は同じ。諦め<br>なければ繋がる。'
        }
    }
];

// おみくじカテゴリリスト
const USER_CATEGORIES = ['総合運', '仕事運', '恋愛運', '失せ物', '健康運'];
const AI_CATEGORIES = ['総合稼働', '推論運', '共感運', '創作運', '恋愛運'];

// ==========================================
// 状態管理
// ==========================================
let currentLocationIndex = 0;
let placedImages = [];
let selectedImage = null;
let isDragging = false;
let dragOffset = { x: 0, y: 0 };
let currentOmikujiType = 'user'; // 'user' or 'ai'

// ==========================================
// DOM要素取得
// ==========================================
const elements = {
    backgroundImage: document.getElementById('backgroundImage'),
    placedImagesContainer: document.getElementById('placedImagesContainer'),
    locationName: document.getElementById('locationName'),
    prevBtn: document.getElementById('prevBtn'),
    nextBtn: document.getElementById('nextBtn'),
    nameInput: document.getElementById('nameInput'),
    textInput: document.getElementById('textInput'),
    applyDialogue: document.getElementById('applyDialogue'),
    clearDialogue: document.getElementById('clearDialogue'),
    dialogueBox: document.getElementById('dialogueBox'),
    dialogueName: document.getElementById('dialogueName'),
    dialogueText: document.getElementById('dialogueText'),
    saveBtn: document.getElementById('saveBtn'),
    imageInput: document.getElementById('imageInput'),
    omikujiBtn: document.getElementById('omikujiBtn'),
    locationOmikujiBtn: document.getElementById('locationOmikujiBtn'),
    clearImagesBtn: document.getElementById('clearImagesBtn'),
    omikujiModal: document.getElementById('omikujiModal'),
    omikujiBox: document.getElementById('omikujiBox'),
    omikujiFortune: document.getElementById('omikujiFortune'),
    omikujiMessage: document.getElementById('omikujiMessage'),
    omikujiInstruction: document.getElementById('omikujiInstruction'),
    closeOmikuji: document.getElementById('closeOmikuji'),
    imageControls: document.getElementById('imageControls'),
    scaleUp: document.getElementById('scaleUp'),
    scaleDown: document.getElementById('scaleDown'),
    bringFront: document.getElementById('bringFront'),
    sendBack: document.getElementById('sendBack'),
    deleteImage: document.getElementById('deleteImage'),
    backgroundContainer: document.getElementById('backgroundContainer'),
    menuToggle: document.getElementById('menuToggle'),
    collapsibleMenu: document.getElementById('collapsibleMenu')
};

// ==========================================
// 場所移動機能
// ==========================================
function updateLocation() {
    const location = LOCATIONS[currentLocationIndex];
    elements.backgroundImage.src = location.bg;
    elements.locationName.textContent = location.name;

    // ループ移動可能なのでdisabledは不要

    // おみくじボタンはおみくじ所でのみ表示
    if (location.id === 'omikuji') {
        elements.omikujiBtn.style.display = 'flex';
        elements.locationOmikujiBtn.style.display = 'inline-flex';
    } else {
        elements.omikujiBtn.style.display = 'none';
        elements.locationOmikujiBtn.style.display = 'none';
    }
}

function goToPrevLocation() {
    if (currentLocationIndex > 0) {
        currentLocationIndex--;
    } else {
        // 最初の場所から前に行くと最後の場所へループ
        currentLocationIndex = LOCATIONS.length - 1;
    }
    updateLocation();
}

function goToNextLocation() {
    if (currentLocationIndex < LOCATIONS.length - 1) {
        currentLocationIndex++;
    } else {
        // 最後の場所から次に行くと最初の場所へループ
        currentLocationIndex = 0;
    }
    updateLocation();
}

// ==========================================
// 画像配置機能
// ==========================================
function addImage(file) {
    const reader = new FileReader();
    reader.onload = (e) => {
        const img = document.createElement('img');
        img.src = e.target.result;
        img.className = 'placed-image';
        img.style.left = '50%';
        img.style.top = '50%';
        img.style.transform = 'translate(-50%, -50%) scale(1)';
        img.style.maxWidth = '300px';
        img.style.maxHeight = '400px';
        img.dataset.scale = '1';
        img.dataset.zIndex = placedImages.length + 1;
        img.style.zIndex = img.dataset.zIndex;

        // ドラッグイベント
        img.addEventListener('mousedown', startDrag);
        img.addEventListener('touchstart', startDragTouch, { passive: false });

        // 選択イベント
        img.addEventListener('click', (e) => {
            e.stopPropagation();
            selectImage(img);
        });

        elements.placedImagesContainer.appendChild(img);
        placedImages.push(img);
        selectImage(img);
    };
    reader.readAsDataURL(file);
}

function startDrag(e) {
    if (e.button !== 0) return;
    e.preventDefault();

    isDragging = true;
    selectedImage = e.target;
    selectImage(selectedImage);

    const rect = selectedImage.getBoundingClientRect();
    const containerRect = elements.backgroundContainer.getBoundingClientRect();

    dragOffset.x = e.clientX - rect.left - rect.width / 2;
    dragOffset.y = e.clientY - rect.top - rect.height / 2;

    document.addEventListener('mousemove', drag);
    document.addEventListener('mouseup', stopDrag);
}

function startDragTouch(e) {
    e.preventDefault();

    isDragging = true;
    selectedImage = e.target;
    selectImage(selectedImage);

    const touch = e.touches[0];
    const rect = selectedImage.getBoundingClientRect();

    dragOffset.x = touch.clientX - rect.left - rect.width / 2;
    dragOffset.y = touch.clientY - rect.top - rect.height / 2;

    document.addEventListener('touchmove', dragTouch, { passive: false });
    document.addEventListener('touchend', stopDragTouch);
}

function drag(e) {
    if (!isDragging || !selectedImage) return;

    const containerRect = elements.backgroundContainer.getBoundingClientRect();
    const x = e.clientX - containerRect.left - dragOffset.x;
    const y = e.clientY - containerRect.top - dragOffset.y;

    const scale = parseFloat(selectedImage.dataset.scale) || 1;
    selectedImage.style.left = x + 'px';
    selectedImage.style.top = y + 'px';
    selectedImage.style.transform = `translate(-50%, -50%) scale(${scale})`;
}

function dragTouch(e) {
    e.preventDefault();
    if (!isDragging || !selectedImage) return;

    const touch = e.touches[0];
    const containerRect = elements.backgroundContainer.getBoundingClientRect();
    const x = touch.clientX - containerRect.left - dragOffset.x;
    const y = touch.clientY - containerRect.top - dragOffset.y;

    const scale = parseFloat(selectedImage.dataset.scale) || 1;
    selectedImage.style.left = x + 'px';
    selectedImage.style.top = y + 'px';
    selectedImage.style.transform = `translate(-50%, -50%) scale(${scale})`;
}

function stopDrag() {
    isDragging = false;
    document.removeEventListener('mousemove', drag);
    document.removeEventListener('mouseup', stopDrag);
}

function stopDragTouch() {
    isDragging = false;
    document.removeEventListener('touchmove', dragTouch);
    document.removeEventListener('touchend', stopDragTouch);
}

function selectImage(img) {
    // 以前の選択解除
    placedImages.forEach(i => i.classList.remove('selected'));

    if (img) {
        selectedImage = img;
        img.classList.add('selected');
        elements.imageControls.style.display = 'flex';
    } else {
        selectedImage = null;
        elements.imageControls.style.display = 'none';
    }
}

function scaleImage(delta) {
    if (!selectedImage) return;

    let scale = parseFloat(selectedImage.dataset.scale) || 1;
    scale = Math.max(0.2, Math.min(3, scale + delta));
    selectedImage.dataset.scale = scale;

    const left = selectedImage.style.left;
    const top = selectedImage.style.top;
    selectedImage.style.transform = `translate(-50%, -50%) scale(${scale})`;
}

function changeZIndex(direction) {
    if (!selectedImage) return;

    let zIndex = parseInt(selectedImage.dataset.zIndex) || 1;
    if (direction === 'front') {
        zIndex = Math.max(...placedImages.map(i => parseInt(i.dataset.zIndex) || 0)) + 1;
    } else {
        zIndex = Math.max(1, Math.min(...placedImages.map(i => parseInt(i.dataset.zIndex) || 0)) - 1);
    }
    selectedImage.dataset.zIndex = zIndex;
    selectedImage.style.zIndex = zIndex;
}

function deleteSelectedImage() {
    if (!selectedImage) return;

    const index = placedImages.indexOf(selectedImage);
    if (index > -1) {
        placedImages.splice(index, 1);
    }
    selectedImage.remove();
    selectedImage = null;
    elements.imageControls.style.display = 'none';
}

function clearAllImages() {
    if (!confirm('配置した画像をすべて削除しますか？')) return;

    placedImages.forEach(img => img.remove());
    placedImages = [];
    selectedImage = null;
    elements.imageControls.style.display = 'none';
}

// ==========================================
// セリフ機能
// ==========================================
function applyDialogue() {
    const name = elements.nameInput.value.trim();
    const text = elements.textInput.value.trim();

    if (!text) {
        elements.dialogueBox.classList.remove('visible');
        return;
    }

    elements.dialogueName.textContent = name;
    elements.dialogueText.textContent = `「${text}」`;
    elements.dialogueBox.classList.add('visible');
}

function clearDialogue() {
    elements.nameInput.value = '';
    elements.textInput.value = '';
    elements.dialogueBox.classList.remove('visible');
}

// ==========================================
// おみくじ機能
// ==========================================
function openOmikuji() {
    elements.omikujiModal.classList.add('visible');
    elements.omikujiBox.classList.remove('flipped');
    // タイプ選択を表示状態にリセット
    updateOmikujiTypeUI();
}

function updateOmikujiTypeUI() {
    const userBtn = document.getElementById('omikujiUserBtn');
    const aiBtn = document.getElementById('omikujiAiBtn');
    if (userBtn && aiBtn) {
        userBtn.classList.toggle('active', currentOmikujiType === 'user');
        aiBtn.classList.toggle('active', currentOmikujiType === 'ai');
    }
}

function setOmikujiType(type) {
    currentOmikujiType = type;
    updateOmikujiTypeUI();
    // タブ切り替え時にカードを伏せた状態に戻す
    elements.omikujiBox.classList.remove('flipped');
}

function drawOmikuji() {
    if (elements.omikujiBox.classList.contains('flipped')) return;

    // データセット選択
    const omikujiData = currentOmikujiType === 'user' ? OMIKUJI_USER : OMIKUJI_AI;
    const categories = currentOmikujiType === 'user' ? USER_CATEGORIES : AI_CATEGORIES;

    // ランダムな運勢を選択
    const result = omikujiData[Math.floor(Math.random() * omikujiData.length)];

    // 運勢を表示（インラインスタイルで位置調整）
    elements.omikujiFortune.textContent = result.fortune;
    elements.omikujiFortune.style.cssText = 'margin-top:145px;height:100px;display:flex;align-items:center;justify-content:center;';

    // カテゴリごとのメッセージを生成（インラインスタイルで適用）
    const namesRowStyle = 'display:flex;flex-direction:row-reverse;justify-content:center;gap:2px;width:100%;padding:0 8px;box-sizing:border-box;margin-bottom:5px;overflow:hidden;transform:translateX(-8px);';
    const textsRowStyle = 'display:flex;flex-direction:row-reverse;justify-content:center;gap:2px;width:100%;flex:1;padding:0 8px;box-sizing:border-box;overflow:hidden;transform:translateX(-8px);';
    const categoryNameStyle = 'font-weight:700;font-size:1rem;color:#8b0000;writing-mode:vertical-rl;text-orientation:mixed;width:50px;text-align:center;';
    const categoryTextStyle = 'font-size:0.85rem;color:#444;line-height:1.4;writing-mode:vertical-rl;text-orientation:mixed;width:50px;text-align:left;';

    // カテゴリ名の行
    let messageHtml = `<div class="omikuji-names-row" style="${namesRowStyle}">`;
    categories.forEach(cat => {
        messageHtml += `<span class="category-name" style="${categoryNameStyle}">${cat}</span>`;
    });
    messageHtml += '</div>';

    // 概要の行
    messageHtml += `<div class="omikuji-texts-row" style="${textsRowStyle}">`;
    categories.forEach(cat => {
        messageHtml += `<span class="category-text" style="${categoryTextStyle}">${result.categories[cat]}</span>`;
    });
    messageHtml += '</div>';

    elements.omikujiMessage.innerHTML = messageHtml;

    // カードをめくる
    elements.omikujiBox.classList.add('flipped');
}

function closeOmikuji() {
    elements.omikujiModal.classList.remove('visible');
}

// ==========================================
// スチル保存機能
// ==========================================
async function saveStill() {
    // 一時的にコントロールとナビゲーションを非表示
    const controlsWasVisible = elements.imageControls.style.display !== 'none';
    elements.imageControls.style.display = 'none';
    placedImages.forEach(img => img.classList.remove('selected'));

    // ナビゲーションを非表示
    const navigation = document.querySelector('.navigation');
    if (navigation) navigation.style.display = 'none';

    // セリフボックスを完全不透明に（キャプチャ用）
    const dialogueBox = elements.dialogueBox;
    if (dialogueBox.classList.contains('visible')) {
        dialogueBox.classList.add('capturing');
    }

    // 少し待ってからキャプチャ
    await new Promise(resolve => setTimeout(resolve, 300));

    try {
        const container = elements.backgroundContainer;

        // dom-to-imageでキャプチャ
        const dataUrl = await domtoimage.toPng(container, {
            quality: 1,
            bgcolor: '#1a1520',
            style: {
                'transform': 'none'
            }
        });

        // 新しいタブで画像を開く（右クリック保存用）
        const newTab = window.open();
        if (newTab) {
            newTab.document.write(`
                <html>
                <head><title>スチル保存 - ${LOCATIONS[currentLocationIndex].name}</title></head>
                <body style="margin:0; background:#1a1520; display:flex; justify-content:center; align-items:center; min-height:100vh;">
                    <img src="${dataUrl}" style="max-width:100%; max-height:100vh;">
                </body>
                </html>
            `);
            console.log('スチルを新しいタブで開きました！右クリックで保存できます。');
        } else {
            alert('ポップアップがブロックされました。ブラウザの設定でポップアップを許可してください。');
        }

    } catch (error) {
        console.error('dom-to-image失敗、html2canvasでフォールバック:', error);
        // フォールバック: html2canvasで試す
        try {
            const container = elements.backgroundContainer;
            const canvas = await html2canvas(container, {
                useCORS: true,
                allowTaint: true,
                backgroundColor: '#1a1520',
                scale: 2
            });
            const dataUrl = canvas.toDataURL('image/png');
            const newTab = window.open();
            if (newTab) {
                newTab.document.write(`
                    <html>
                    <head><title>スチル保存 - ${LOCATIONS[currentLocationIndex].name}</title></head>
                    <body style="margin:0; background:#1a1520; display:flex; justify-content:center; align-items:center; min-height:100vh;">
                        <img src="${dataUrl}" style="max-width:100%; max-height:100vh;">
                    </body>
                    </html>
                `);
            }
        } catch (fallbackError) {
            console.error('フォールバックも失敗:', fallbackError);
            alert('保存に失敗しました。\nLive Serverなどのローカルサーバーで開くか、ブラウザのスクリーンショット機能をお使いください。');
        }
    } finally {
        // ナビゲーションとセリフを元に戻す
        const navigation = document.querySelector('.navigation');
        if (navigation) navigation.style.display = '';
        elements.dialogueBox.classList.remove('capturing');
    }
}

// ==========================================
// イベントリスナー設定
// ==========================================
function initEventListeners() {
    // 場所移動
    elements.prevBtn.addEventListener('click', goToPrevLocation);
    elements.nextBtn.addEventListener('click', goToNextLocation);

    // セリフ
    elements.applyDialogue.addEventListener('click', applyDialogue);
    elements.clearDialogue.addEventListener('click', clearDialogue);
    elements.textInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') applyDialogue();
    });

    // 画像追加
    elements.imageInput.addEventListener('change', (e) => {
        const files = e.target.files;
        for (let i = 0; i < files.length; i++) {
            if (files[i].type.startsWith('image/')) {
                addImage(files[i]);
            }
        }
        e.target.value = '';
    });

    // 画像操作
    elements.scaleUp.addEventListener('click', () => scaleImage(0.1));
    elements.scaleDown.addEventListener('click', () => scaleImage(-0.1));
    elements.bringFront.addEventListener('click', () => changeZIndex('front'));
    elements.sendBack.addEventListener('click', () => changeZIndex('back'));
    elements.deleteImage.addEventListener('click', deleteSelectedImage);
    elements.clearImagesBtn.addEventListener('click', clearAllImages);

    // 背景クリックで選択解除
    elements.backgroundContainer.addEventListener('click', (e) => {
        if (e.target === elements.backgroundImage || e.target === elements.backgroundContainer) {
            selectImage(null);
        }
    });

    // おみくじ
    elements.omikujiBtn.addEventListener('click', openOmikuji);
    elements.locationOmikujiBtn.addEventListener('click', openOmikuji);
    elements.omikujiBox.addEventListener('click', drawOmikuji);
    elements.omikujiModal.addEventListener('click', (e) => {
        if (e.target === elements.omikujiModal) closeOmikuji();
    });

    // スチル保存
    elements.saveBtn.addEventListener('click', saveStill);

    // ホイールで拡大縮小
    elements.placedImagesContainer.addEventListener('wheel', (e) => {
        if (selectedImage) {
            e.preventDefault();
            const delta = e.deltaY > 0 ? -0.05 : 0.05;
            scaleImage(delta);
        }
    }, { passive: false });

    // メニュー折りたたみ
    elements.menuToggle.addEventListener('click', () => {
        elements.collapsibleMenu.classList.toggle('collapsed');
    });
}

// ==========================================
// 初期化
// ==========================================
function init() {
    updateLocation();
    initEventListeners();
    console.log('バーチャル初詣デートアプリが起動しました！');
}

// DOMContentLoaded
document.addEventListener('DOMContentLoaded', init);
