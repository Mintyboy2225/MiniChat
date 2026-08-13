<!DOCTYPE html>
<html>
<head>
  <title>Mini Chat</title>

  <style>
    /* ---------- BACKGROUND ---------- */
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #f0f0f0, #dcd4f7, #e8e0ff);
      background-size: 400% 400%;
      animation: gradientBG 15s ease infinite;
      display: flex;
      justify-content: center;
      margin-top: 40px;
      transition: background 0.3s, color 0.3s;
    }

    @keyframes gradientBG {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    /* ---------- DARK MODE ---------- */
    body.dark {
      background: linear-gradient(135deg, #1f1f1f, #3a225f, #2b1e44);
      color: #eee;
    }

    body.dark #chat {
      background: #2b1e44;
    }

    body.dark .other {
      background: #3f2a6b;
      color: #eee;
    }

    body.dark .me {
      background: #7c3aed;
    }

    body.dark #replyingTo {
      background: rgba(255,255,255,0.1);
    }

    /* ---------- ROOM SELECT ---------- */
    #roomSelection {
      width: 400px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    input, button {
      padding: 12px;
      border-radius: 8px;
      border: none;
      outline: none;
      font-size: 14px;
      box-sizing: border-box;
    }

    button {
      background: #7c3aed;
      color: white;
      cursor: pointer;
    }

    button:hover {
      filter: brightness(1.08);
    }

    /* ---------- CHAT ---------- */
    #chat {
      width: 400px;
      display: none;
      flex-direction: column;
      background: #f8f8f8;
      border-radius: 20px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      overflow: hidden;
      transition: background 0.3s;
    }

    #chatHeader {
      text-align: center;
      padding: 12px;
      font-weight: bold;
      border-bottom: 1px solid #ccc;
    }

    #messages {
      height: 350px;
      overflow-y: auto;
      padding: 12px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .message {
      max-width: 70%;
      padding: 10px;
      border-radius: 15px;
      position: relative;
      word-wrap: break-word;
    }

    .me {
      align-self: flex-end;
      background: #7c3aed;
      color: white;
    }

    .other {
      align-self: flex-start;
      background: #d9d5f6;
      color: #111;
    }

    .username {
      font-size: 11px;
      font-weight: bold;
      margin-bottom: 2px;
      opacity: 0.9;
    }

    .reply-preview {
      font-size: 11px;
      opacity: 0.8;
      border-left: 2px solid currentColor;
      padding-left: 6px;
      margin-bottom: 4px;
    }

    .reply-btn {
      position: absolute;
      top: -18px;
      right: 6px;
      font-size: 10px;
      background: rgba(0,0,0,0.25);
      color: white;
      padding: 3px 6px;
      border-radius: 6px;
      cursor: pointer;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s ease;
    }

    .message:hover .reply-btn,
    .reply-btn:hover {
      opacity: 1;
      pointer-events: auto;
    }

    .time {
      font-size: 10px;
      opacity: 0.8;
      margin-top: 2px;
      text-align: right;
    }

    #replyingTo {
      font-size: 12px;
      padding: 6px;
      background: rgba(0,0,0,0.1);
      display: none;
    }

    #username,
    #message {
      margin: 0 8px 8px 8px;
    }

    #chat > button {
      margin: 0 8px 8px 8px;
    }
  </style>
</head>

<body>

<div id="roomSelection">
  <input id="roomCodeInput" placeholder="Enter Room Code">
  <button onclick="joinRoom()">Join Room</button>
  <button onclick="createRoom()">Create New Room</button>
</div>

<div id="chat">

  <div id="chatHeader"></div>

  <div id="messages"></div>

  <div id="replyingTo"></div>

  <input id="username" placeholder="Your name">

  <input id="message" placeholder="Type a message">

  <button onclick="sendMessage()">Send</button>

  <button onclick="toggleDarkMode()">Toggle Dark Mode</button>

</div>

<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>

<script>
  /* ---------- FIREBASE ---------- */

  firebase.initializeApp({
    apiKey: "AIzaSyCR_fzXg5elyqPiBFxjn7l98y7pHFtFrBI",
    authDomain: "chat-85bb8.firebaseapp.com",
    databaseURL: "https://chat-85bb8-default-rtdb.firebaseio.com",
    projectId: "chat-85bb8",
    appId: "1:925323589808:web:6b599f66cbbbe0f7e1e375"
  });


  /* ---------- VARIABLES ---------- */

  let roomCode = "";
  let db = null;
  let myUser = "";
  let replyData = null;
  let unread = 0;

  const baseTitle = "Mini Chat";


  /* ---------- LOAD SAVED USERNAME ---------- */

  const savedUsername = localStorage.getItem("miniChatUsername");

  if (savedUsername) {
    username.value = savedUsername;
    myUser = savedUsername;
  }


  /* ---------- ROOM FUNCTIONS ---------- */

  function randomRoomCode() {
    return Math.random()
      .toString(36)
      .substring(2, 7)
      .toUpperCase();
  }


  function createRoom() {
    roomCode = randomRoomCode();
    startChat();
  }


  function joinRoom() {
    const enteredCode = roomCodeInput.value.trim().toUpperCase();

    if (!enteredCode) return;

    roomCode = enteredCode;

    startChat();
  }


  /* ---------- START CHAT ---------- */

  function startChat() {

    roomSelection.style.display = "none";
    chat.style.display = "flex";

    chatHeader.textContent = "Room: " + roomCode;

    /*
      Remove the previous Firebase listener before
      creating a new one.

      This prevents duplicate messages when rooms
      are switched later.
    */

    if (db) {
      db.off();
    }

    db = firebase
      .database()
      .ref("rooms/" + roomCode + "/messages");


    /*
      Clear the current message display.
    */

    messages.innerHTML = "";


    /*
      Listen for new messages.
    */

    db.on("child_added", snap => {

      const msg = snap.val();

      if (!document.hasFocus()) {

        unread++;

        document.title =
          `${baseTitle} (${unread})`;
      }

      renderMessage(msg);
    });
  }


  /* ---------- TAB NOTIFICATIONS ---------- */

  window.addEventListener("focus", () => {

    unread = 0;

    document.title = baseTitle;
  });


  /* ---------- SEND MESSAGE ---------- */

  function sendMessage() {

    /*
      Get username if we don't already have it.
    */

    if (!myUser) {

      myUser = username.value.trim();

      if (!myUser) return;

      localStorage.setItem(
        "miniChatUsername",
        myUser
      );
    }


    const text = message.value.trim();

    if (!text) return;


    /*
      Send message to Firebase.
    */

    db.push({

      user: myUser,

      text: text,

      reply: replyData,

      timestamp: Date.now()
    });


    /*
      Clear reply state.
    */

    replyData = null;

    replyingTo.style.display = "none";

    message.value = "";
  }


  /* ---------- RENDER MESSAGE ---------- */

  function renderMessage(msg) {

    const div = document.createElement("div");

    div.className =
      "message " +
      (msg.user === myUser ? "me" : "other");


    /* ---------- REPLY BUTTON ---------- */

    const replyBtn =
      document.createElement("div");

    replyBtn.className = "reply-btn";

    replyBtn.textContent = "Reply";


    replyBtn.onclick = () => {

      replyData = {
        user: msg.user,
        text: msg.text
      };

      replyingTo.textContent =
        `Replying to ${msg.user}: ${msg.text}`;

      replyingTo.style.display = "block";
    };


    /* ---------- REPLY PREVIEW ---------- */

    if (msg.reply) {

      const rp =
        document.createElement("div");

      rp.className = "reply-preview";

      rp.textContent =
        msg.reply.user +
        ": " +
        msg.reply.text;

      div.appendChild(rp);
    }


    /* ---------- USERNAME ---------- */

    const userDiv =
      document.createElement("div");

    userDiv.className = "username";

    userDiv.textContent = msg.user;


    /* ---------- MESSAGE TEXT ---------- */

    const textDiv =
      document.createElement("div");

    textDiv.textContent = msg.text;


    /* ---------- TIMESTAMP ---------- */

    const timeDiv =
      document.createElement("div");

    timeDiv.className = "time";


    const timestamp =
      Number(msg.timestamp);


    /*
      Prevent NaN timestamps from appearing
      if an old/broken Firebase message exists.
    */

    if (!Number.isNaN(timestamp)) {

      const d = new Date(timestamp);

      let h = d.getHours();

      let m =
        d.getMinutes()
         .toString()
         .padStart(2, "0");

      timeDiv.textContent =
        `${h % 12 || 12}:${m} ${
          h >= 12 ? "PM" : "AM"
        }`;

    } else {

      timeDiv.textContent = "";
    }


    /* ---------- BUILD MESSAGE ---------- */

    div.append(
      replyBtn,
      userDiv,
      textDiv,
      timeDiv
    );


    messages.appendChild(div);


    /*
      Keep the newest message visible.
    */

    messages.scrollTop =
      messages.scrollHeight;
  }


  /* ---------- DARK MODE ---------- */

  function toggleDarkMode() {

    document.body.classList.toggle("dark");
  }


  /* ---------- ENTER TO SEND ---------- */

  message.addEventListener("keydown", e => {

    if (e.key === "Enter") {

      e.preventDefault();

      sendMessage();
    }
  });


  /* ---------- SAVE USERNAME WHEN CHANGED ---------- */

  username.addEventListener("change", () => {

    const name =
      username.value.trim();

    if (!name) return;

    myUser = name;

    localStorage.setItem(
      "miniChatUsername",
      name
    );
  });

</script>

</body>
</html>
