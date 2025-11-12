[index.html](https://github.com/user-attachments/files/23490116/index.html)[Uploading index.ht<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Báo Không Ngủ 📰</title>
<!-- Nội dung code đầy đủ đã gửi ở trên -->
</head>
<body>
<p>Nội dung website Báo Không Ngủ (phiên bản đầy đủ).</p>
</body>
</html><!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Báo Không Ngủ 📰</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0; padding: 0;
      background-color: var(--bg-color, #f4f4f4);
      color: var(--text-color, #222);
      transition: background 0.3s, color 0.3s;
    }
    header {
      background-color: #222;
      color: white;
      padding: 15px;
      text-align: center;
    }
    nav {
      background-color: #444;
      display: flex;
      justify-content: center;
      gap: 15px;
      padding: 10px;
    }
    nav button {
      background: #666;
      color: white;
      border: none;
      padding: 8px 16px;
      border-radius: 8px;
      cursor: pointer;
      transition: 0.2s;
    }
    nav button:hover { background: #999; }
    main {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 20px;
      gap: 20px;
    }
    .post {
      background: white;
      border-radius: 10px;
      box-shadow: 0 0 5px rgba(0,0,0,0.2);
      width: 300px;
      padding: 15px;
    }
    .post h2 { margin: 0; }
    .like {
      color: #e00;
      cursor: pointer;
      user-select: none;
    }
    .comment-section {
      margin-top: 10px;
    }
    .comment-section input {
      width: 80%;
      padding: 5px;
    }
    .comment-section button {
      padding: 5px 10px;
    }
    footer {
      text-align: center;
      background: #222;
      color: white;
      padding: 10px;
      position: fixed;
      bottom: 0;
      width: 100%;
    }
    .theme-btn {
      position: fixed;
      top: 10px;
      right: 10px;
      background: orange;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 8px;
      cursor: pointer;
    }
    .auth {
      text-align: center;
      margin: 20px;
    }
    .auth input {
      margin: 5px;
      padding: 8px;
    }
  </style>
</head>
<body>

  <header><h1>📰 Báo Không Ngủ</h1></header>
  
  <nav>
    <button onclick="showSection('news')">Trang Chủ</button>
    <button onclick="showSection('create')">Đăng Bài</button>
    <button onclick="logout()">Đăng Xuất</button>
  </nav>

  <button class="theme-btn" onclick="toggleTheme()">🌙 Giao diện</button>

  <div id="login-section" class="auth">
    <h2>Đăng nhập</h2>
    <input id="login-username" placeholder="Tên đăng nhập"><br>
    <input id="login-password" placeholder="Mật khẩu" type="password"><br>
    <button onclick="login()">Đăng nhập</button>
    <p>Chưa có tài khoản? <a href="#" onclick="toggleAuth('register')">Đăng ký</a></p>
  </div>

  <div id="register-section" class="auth" style="display:none;">
    <h2>Đăng ký</h2>
    <input id="register-username" placeholder="Tên đăng nhập"><br>
    <input id="register-password" placeholder="Mật khẩu" type="password"><br>
    <button onclick="register()">Đăng ký</button>
    <p>Đã có tài khoản? <a href="#" onclick="toggleAuth('login')">Đăng nhập</a></p>
  </div>

  <main id="main-content" style="display:none;">
    <section id="create" style="display:none;">
      <h2>🖋️ Đăng bài mới</h2>
      <input id="title" placeholder="Tiêu đề bài viết"><br><br>
      <textarea id="content" placeholder="Nội dung..." rows="5" cols="40"></textarea><br><br>
      <button onclick="savePost()">Đăng bài</button>
    </section>

    <section id="news">
      <h2>📰 Bài viết mới nhất</h2>
      <div id="post-list"></div>
    </section>
  </main>

  <footer>Báo Không Ngủ © 2025 | Làm bởi bạn 💻</footer>

<script>
  let currentUser = localStorage.getItem('currentUser');
  let posts = JSON.parse(localStorage.getItem('posts') || '[]');

  function showSection(id) {
    document.querySelectorAll('section').forEach(s => s.style.display = 'none');
    document.getElementById(id).style.display = 'block';
    if (id === 'news') loadPosts();
  }

  function register() {
    let user = document.getElementById('register-username').value;
    let pass = document.getElementById('register-password').value;
    if (!user || !pass) return alert('Điền đầy đủ thông tin!');
    let users = JSON.parse(localStorage.getItem('users') || '{}');
    if (users[user]) return alert('Tên đã tồn tại!');
    users[user] = pass;
    localStorage.setItem('users', JSON.stringify(users));
    alert('Đăng ký thành công!');
    toggleAuth('login');
  }

  function login() {
    let user = document.getElementById('login-username').value;
    let pass = document.getElementById('login-password').value;
    let users = JSON.parse(localStorage.getItem('users') || '{}');
    if (users[user] === pass) {
      currentUser = user;
      localStorage.setItem('currentUser', user);
      document.getElementById('login-section').style.display = 'none';
      document.getElementById('register-section').style.display = 'none';
      document.getElementById('main-content').style.display = 'block';
      showSection('news');
    } else alert('Sai thông tin đăng nhập!');
  }

  function logout() {
    localStorage.removeItem('currentUser');
    location.reload();
  }

  function toggleAuth(mode) {
    document.getElementById('login-section').style.display = mode === 'login' ? 'block' : 'none';
    document.getElementById('register-section').style.display = mode === 'register' ? 'block' : 'none';
  }

  function savePost() {
    let title = document.getElementById('title').value;
    let content = document.getElementById('content').value;
    if (!title || !content) return alert('Nhập đủ thông tin!');
    posts.push({title, content, user: currentUser, likes: 0, comments: []});
    localStorage.setItem('posts', JSON.stringify(posts));
    alert('Đăng bài thành công!');
    showSection('news');
  }

  function loadPosts() {
    let list = document.getElementById('post-list');
    list.innerHTML = '';
    posts.forEach((p, i) => {
      let div = document.createElement('div');
      div.className = 'post';
      div.innerHTML = `
        <h2>${p.title}</h2>
        <p>${p.content}</p>
        <p><small>Đăng bởi: ${p.user}</small></p>
        <p class="like" onclick="likePost(${i})">❤️ ${p.likes}</p>
        <div class="comment-section">
          <input id="comment-${i}" placeholder="Bình luận...">
          <button onclick="commentPost(${i})">Gửi</button>
          <div>${p.comments.map(c => `<p><b>${c.user}:</b> ${c.text}</p>`).join('')}</div>
        </div>`;
      list.appendChild(div);
    });
  }

  function likePost(i) {
    posts[i].likes++;
    localStorage.setItem('posts', JSON.stringify(posts));
    loadPosts();
  }

  function commentPost(i) {
    let cmt = document.getElementById(`comment-${i}`).value;
    if (!cmt) return;
    posts[i].comments.push({user: currentUser, text: cmt});
    localStorage.setItem('posts', JSON.stringify(posts));
    loadPosts();
  }

  function toggleTheme() {
    let dark = getComputedStyle(document.body).getPropertyValue('--bg-color') === '#f4f4f4';
    document.body.style.setProperty('--bg-color', dark ? '#111' : '#f4f4f4');
    document.body.style.setProperty('--text-color', dark ? '#fff' : '#222');
  }

  if (currentUser) {
    document.getElementById('login-section').style.display = 'none';
    document.getElementById('main-content').style.display = 'block';
    showSection('news');
  }
</script>

</body>
</html>
function savePost() {
   </ht let title = document.getElementById('title').value;
    let content = document.getElementById('content').value;
    if (!title || !content) return alert('Nhập đủ thông tin!');
    
    // Thêm bài mới vào posts chung
    posts.push({title, content, user: currentUser, likes: 0, comments: []});
    localStorage.setItem('posts', JSON.stringify(posts));
    
    alert('Đăng bài thành công!');
    document.getElementById('title').value = '';
    document.getElementById('content').value = '';
    
    showSection('news'); // Hiển thị danh sách bài viết sau khi đăng
}

function loadPosts() {
    let list = document.getElementById('post-list');
    list.innerHTML = '';
    
    // Hiển thị tất cả bài viết, bất kể ai đăng
    posts.forEach((p, i) => {
        let div = document.createElement('div');
        div.className = 'post';
        div.innerHTML = `
            <h2>${p.title}</h2>
            <p>${p.content}</p>
            <p><small>Đăng bởi: ${p.user}</small></p>
            <p class="like" onclick="likePost(${i})">❤️ ${p.likes}</p>
            <div class="comment-section">
                <input id="comment-${i}" placeholder="Bình luận...">
                <button onclick="commentPost(${i})">Gửi</button>
                <div>${p.comments.map(c => `<p><b>${c.user}:</b> ${c.text}</p>`).join('')}</div>
            </div>`;
        list.appendChild(div);
    });
}


ml…]()
