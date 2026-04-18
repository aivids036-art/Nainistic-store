<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nainistic V11 - Professional Store</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        :root { --pink: #ff007f; --dark: #111; --light: #fafafa; --purple: #6a11cb; --blue: #2575fc; }
        body { font-family: 'Poppins', sans-serif; margin: 0; background: var(--light); color: var(--dark); overflow-x: hidden; }
        
        nav { background: white; padding: 15px 5%; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 2px 10px rgba(0,0,0,0.05); position: sticky; top: 0; z-index: 1000; }
        .logo { font-size: 26px; font-weight: 800; color: var(--pink); text-decoration: none; letter-spacing: 2px; }
        .btn-login { background: var(--pink); color: white; padding: 8px 18px; border-radius: 5px; border:none; cursor:pointer; font-weight:600; }
        .btn-logout { background: #333; color: white; padding: 8px 18px; border-radius: 5px; border:none; cursor:pointer; display:none; }

        #loginPage { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 2000; background: white; }
        .login-container { display: flex; height: 100vh; }
        .login-left { flex: 1; background: linear-gradient(135deg, var(--purple), var(--blue)); color: white; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 40px; text-align: center; }
        .login-right { flex: 1; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 40px; }
        .login-form { width: 100%; max-width: 350px; }
        .input-group { width: 100%; margin-bottom: 15px; position: relative; }
        .input-group input { width: 100%; padding: 12px 40px; border: 1px solid #ddd; border-radius: 8px; box-sizing: border-box; }
        .input-group i { position: absolute; left: 15px; top: 15px; color: #aaa; }
        .btn-signin { width: 100%; padding: 12px; background: var(--purple); color: white; border: none; border-radius: 8px; cursor: pointer; font-weight: 600; }

        .hero-banner { width: 100%; height: 250px; background: url('https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?auto=format&fit=crop&w=1000') center/cover; position: relative; display: flex; align-items: center; justify-content: center; color: white; }
        .hero-banner::after { content: ''; position: absolute; inset: 0; background: rgba(0,0,0,0.3); }
        .hero-text { position: relative; z-index: 2; font-size: 24px; text-transform: uppercase; letter-spacing: 3px; font-weight: 800; }

        .category-tabs { display: flex; justify-content: center; gap: 15px; margin: 25px 0; }
        .tab-btn { padding: 8px 25px; border: 2px solid var(--pink); background: white; color: var(--pink); border-radius: 20px; cursor: pointer; font-weight: 700; transition: 0.3s; }
        .tab-btn.active { background: var(--pink); color: white; }

        .portal-box { display: none; width: 90%; max-width: 600px; margin: 20px auto; background: white; padding: 20px; border-radius: 10px; box-shadow: 0 5px 15px rgba(0,0,0,0.1); border-left: 5px solid var(--pink); }
        .form-group { margin-bottom: 10px; }
        .form-group input, .form-group select { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; box-sizing: border-box; }

        .grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; padding: 0 5%; margin-bottom: 50px; }
        .pin { background: white; border-radius: 12px; overflow: hidden; box-shadow: 0 3px 10px rgba(0,0,0,0.05); position: relative; border: 1px solid #eee; }
        .pin img { width: 100%; height: 250px; object-fit: cover; }
        .pin-info { padding: 12px; }
        .pin-price { color: var(--pink); font-weight: 800; font-size: 16px; margin: 5px 0; }
        
        .comment-sec { border-top: 1px solid #f0f0f0; margin-top: 10px; padding-top: 10px; }
        .comment-item { font-size: 12px; margin-bottom: 5px; display: flex; justify-content: space-between; align-items: center; background: #f9f9f9; padding: 5px 8px; border-radius: 4px; }
        .del-comm { color: #ff4d4d; cursor: pointer; font-size: 10px; display: none; }
        .is-staff .del-comm { display: inline; }
        .del-post { position: absolute; top: 10px; right: 10px; background: white; border: none; border-radius: 50%; width: 25px; height: 25px; color: red; cursor: pointer; display: none; z-index: 5; box-shadow: 0 2px 4px rgba(0,0,0,0.2); }
        .is-staff .del-post { display: block; }
    </style>
</head>
<body onload="init()">

    <nav>
        <a href="#" class="logo">NAINISTIC</a>
        <div class="nav-right">
            <button id="navLoginBtn" class="btn-login" onclick="toggleLogin(true)">Login</button>
            <button id="navLogoutBtn" class="btn-logout" onclick="logout()">Logout</button>
        </div>
    </nav>

    <div id="loginPage">
        <div class="login-container">
            <div class="login-left">
                <h2>Hello, Beauty!</h2>
                <p>Sign in to manage your store and admins.</p>
            </div>
            <div class="login-right">
                <div class="login-form">
                    <h3>Sign In</h3>
                    <div class="input-group">
                        <i class="fa fa-envelope"></i>
                        <input type="email" id="authEmail" placeholder="Email Address">
                    </div>
                    <div class="input-group">
                        <i class="fa fa-lock"></i>
                        <input type="password" id="authPass" placeholder="Password">
                    </div>
                    <button class="btn-signin" onclick="handleAuth()">Sign In</button>
                    <p style="font-size:12px; color: #666; margin-top:15px; cursor:pointer;" onclick="toggleLogin(false)">Go Back to Store</p>
                </div>
            </div>
        </div>
    </div>

    <div class="hero-banner"><div class="hero-text">Elite Beauty Store</div></div>

    <div class="category-tabs">
        <button id="tabM" class="tab-btn active" onclick="filter('makeup')">Makeup</button>
        <button id="tabS" class="tab-btn" onclick="filter('skincare')">Skincare</button>
    </div>

    <div id="portal" class="portal-box">
        <h4 id="portalTitle">Staff Portal</h4>
        <div class="form-group"><input type="text" id="pName" placeholder="Product Name"></div>
        <div class="form-group">
            <select id="pCat">
                <option value="makeup">Makeup</option>
                <option value="skincare">Skincare</option>
            </select>
        </div>
        <div class="form-group"><input type="text" id="pPrice" placeholder="Price (PKR)"></div>
        <div class="form-group"><input type="file" id="pImg" accept="image/*"></div>
        <button class="btn-signin" style="background:var(--pink)" onclick="upload()">Post Product</button>
        
        <div id="ownerSection" style="display:none; margin-top:15px; padding-top:15px; border-top:1px dashed #ccc;">
            <h5>Add Staff Admin</h5>
            <div class="form-group"><input type="email" id="admE" placeholder="New Admin Email"></div>
            <div class="form-group"><input type="password" id="admP" placeholder="Password"></div>
            <button class="btn-signin" style="background:#333" onclick="addAdmin()">Save Admin</button>
        </div>
    </div>

    <div class="grid" id="mainGrid"></div>

    <script>
        let db = JSON.parse(localStorage.getItem('nn_db_final')) || { posts: [], admins: [], comms: {} };
        let curCat = 'makeup';
        const OWNER = { e: "sensec920@gmail.com", p: "8730154731m" };

        function init() { checkSess(); render(); }
        function toggleLogin(show) { document.getElementById('loginPage').style.display = show ? 'block' : 'none'; }

        function handleAuth() {
            let e = document.getElementById('authEmail').value, p = document.getElementById('authPass').value;
            if(e === OWNER.e && p === OWNER.p) { localStorage.setItem('role', 'owner'); location.reload(); }
            else {
                let a = db.admins.find(x => x.e === e && x.p === p);
                if(a) { localStorage.setItem('role', 'admin'); location.reload(); }
                else alert("Access Denied!");
            }
        }

        function checkSess() {
            let role = localStorage.getItem('role');
            if(role) {
                document.getElementById('navLoginBtn').style.display = 'none';
                document.getElementById('navLogoutBtn').style.display = 'block';
                document.getElementById('portal').style.display = 'block';
                document.body.classList.add('is-staff');
                if(role === 'owner') {
                    document.getElementById('portalTitle').innerText = "Owner Portal";
                    document.getElementById('ownerSection').style.display = 'block';
                }
            }
        }

        function addAdmin() {
            let e = document.getElementById('admE').value, p = document.getElementById('admP').value;
            db.admins.push({e, p}); save(); alert("Admin Added!");
        }

        function upload() {
            let n = document.getElementById('pName').value, c = document.getElementById('pCat').value, 
                pr = document.getElementById('pPrice').value, f = document.getElementById('pImg').files[0];
            if(!n || !f) return alert("Fill details!");
            let r = new FileReader();
            r.onload = (e) => {
                db.posts.push({ id: Date.now(), n, c, pr, img: e.target.result });
                save(); location.reload();
            }; r.readAsDataURL(f);
        }

        function render() {
            let g = document.getElementById('mainGrid'); g.innerHTML = '';
            db.posts.filter(x => x.c === curCat).forEach(p => {
                let cs = db.comms[p.id] || [];
                let cHtml = cs.map((c, i) => `<div class="comment-item"><span>${c}</span><i class="fa fa-trash del-comm" onclick="delComm(${p.id}, ${i})"></i></div>`).join('');
                g.innerHTML += `<div class="pin"><button class="del-post" onclick="delPost(${p.id})">&times;</button><img src="${p.img}"><div class="pin-info"><div style="font-weight:600">${p.n}</div><div class="pin-price">PKR ${p.pr}</div><div class="comment-sec"><div id="clist-${p.id}">${cHtml}</div><div style="display:flex; gap:5px; margin-top:5px;"><input type="text" id="cin-${p.id}" placeholder="Comment..." style="flex:1; font-size:10px; padding:5px; border:1px solid #ddd;"><button onclick="addComm(${p.id})" style="font-size:10px; background:var(--pink); color:white; border:none; padding:5px 10px; border-radius:3px;">Add</button></div></div></div></div>`;
            });
        }

        function addComm(id) {
            let v = document.getElementById('cin-'+id).value; if(!v) return;
            if(!db.comms[id]) db.comms[id] = [];
            db.comms[id].push(v); save(); render();
        }

        function delComm(pid, index) { if(confirm("Delete comment?")) { db.comms[pid].splice(index, 1); save(); render(); } }
        function delPost(id) { if(confirm("Delete product?")) { db.posts = db.posts.filter(x => x.id !== id); save(); render(); } }
        function filter(c) { curCat = c; document.getElementById('tabM').classList.toggle('active', c==='makeup'); document.getElementById('tabS').classList.toggle('active', c==='skincare'); render(); }
        function save() { localStorage.setItem('nn_db_final', JSON.stringify(db)); }
        function logout() { localStorage.removeItem('role'); location.reload(); }
    </script>
</body>
</html>
