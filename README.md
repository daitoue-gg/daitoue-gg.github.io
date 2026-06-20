# daitoue-gg.github.io
This is a personal demo  for my class
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>家政服务系统</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        :root {
            --primary-color: #4A90E2; --primary-dark: #357ABD; --secondary-color: #7B68EE;
            --success-color: #52C41A; --warning-color: #FAAD14; --danger-color: #FF4D4F;
            --text-color: #333; --text-light: #666; --bg-color: #F5F7FA;
            --white: #FFFFFF; --border-color: #E8E8E8;
            --shadow: 0 2px 8px rgba(0,0,0,0.1); --shadow-hover: 0 4px 16px rgba(0,0,0,0.15);
        }
        body {
            font-family: -apple-system,BlinkMacSystemFont,'Segoe UI','PingFang SC','Hiragino Sans GB','Microsoft YaHei',sans-serif;
            background: var(--bg-color); color: var(--text-color); line-height: 1.6;
        }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }
        header {
            background: linear-gradient(135deg,var(--primary-color),var(--secondary-color));
            color: var(--white); padding: 15px 0; position: fixed; width: 100%;
            top: 0; z-index: 1000; box-shadow: var(--shadow);
        }
        .header-content { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 15px; }
        .logo { font-size: 24px; font-weight: bold; display: flex; align-items: center; gap: 10px; }
        .logo-icon { font-size: 28px; }
        nav { display: flex; gap: 10px; flex-wrap: wrap; }
        nav button {
            background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.3);
            color: var(--white); padding: 8px 16px; border-radius: 20px; cursor: pointer;
            font-size: 14px; transition: all 0.3s ease;
        }
        nav button:hover { background: rgba(255,255,255,0.3); transform: translateY(-2px); }
        nav button.active { background: var(--white); color: var(--primary-color); }
        .user-info { display: flex; align-items: center; gap: 10px; }
        .user-avatar { width: 36px; height: 36px; border-radius: 50%; background: var(--white); display: flex; align-items: center; justify-content: center; font-size: 18px; }
        .user-name { font-weight: 500; }
        .btn-logout { background: rgba(255,255,255,0.2); border: 1px solid rgba(255,255,255,0.3); color: var(--white); padding: 6px 12px; border-radius: 15px; cursor: pointer; font-size: 12px; transition: all 0.3s ease; }
        .btn-logout:hover { background: rgba(255,77,79,0.8); }
        main { margin-top: 80px; padding: 20px 0; min-height: calc(100vh - 80px); }
        .page { display: none; animation: fadeIn 0.3s ease; }
        .page.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .hero {
            background: linear-gradient(135deg,var(--primary-color),var(--secondary-color));
            color: var(--white); padding: 60px 20px; text-align: center; border-radius: 12px; margin-bottom: 30px;
        }
        .hero h1 { font-size: 36px; margin-bottom: 15px; }
        .hero p { font-size: 18px; opacity: 0.9; margin-bottom: 30px; }
        .hero-buttons { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; }
        .btn { padding: 12px 30px; border: none; border-radius: 25px; cursor: pointer; font-size: 16px; font-weight: 500; transition: all 0.3s ease; display: inline-flex; align-items: center; gap: 8px; }
        .btn-primary { background: var(--white); color: var(--primary-color); }
        .btn-primary:hover { transform: translateY(-2px); box-shadow: var(--shadow-hover); }
        .btn-secondary { background: transparent; border: 2px solid var(--white); color: var(--white); }
        .btn-secondary:hover { background: var(--white); color: var(--primary-color); }
        .btn-success { background: var(--success-color); color: var(--white); }
        .btn-success:hover { background: #45a514; }
        .btn-danger { background: var(--danger-color); color: var(--white); }
        .btn-danger:hover { background: #d9363e; }
        .btn-small { padding: 6px 16px; font-size: 14px; }
        .features { display: grid; grid-template-columns: repeat(auto-fit,minmax(280px,1fr)); gap: 20px; margin-bottom: 30px; }
        .feature-card { background: var(--white); padding: 30px; border-radius: 12px; box-shadow: var(--shadow); text-align: center; transition: all 0.3s ease; }
        .feature-card:hover { transform: translateY(-5px); box-shadow: var(--shadow-hover); }
        .feature-icon { font-size: 48px; margin-bottom: 15px; }
        .feature-card h3 { font-size: 20px; margin-bottom: 10px; color: var(--primary-color); }
        .feature-card p { color: var(--text-light); font-size: 14px; }
        .card { background: var(--white); border-radius: 12px; box-shadow: var(--shadow); padding: 30px; margin-bottom: 20px; }
        .card-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; padding-bottom: 15px; border-bottom: 1px solid var(--border-color); }
        .card-title { font-size: 20px; color: var(--text-color); }
        .form-group { margin-bottom: 20px; }
        .form-group label { display: block; margin-bottom: 8px; font-weight: 500; color: var(--text-color); }
        .form-group label .required { color: var(--danger-color); }
        .form-control { width: 100%; padding: 12px 15px; border: 1px solid var(--border-color); border-radius: 8px; font-size: 14px; transition: all 0.3s ease; }
        .form-control:focus { outline: none; border-color: var(--primary-color); box-shadow: 0 0 0 3px rgba(74,144,226,0.1); }
        .form-control.error { border-color: var(--danger-color); }
        .error-message { color: var(--danger-color); font-size: 12px; margin-top: 5px; display: none; }
        .error-message.show { display: block; }
        .form-row { display: grid; grid-template-columns: repeat(auto-fit,minmax(200px,1fr)); gap: 20px; }
        .form-select { width: 100%; padding: 12px 15px; border: 1px solid var(--border-color); border-radius: 8px; font-size: 14px; background: var(--white); cursor: pointer; }
        .form-textarea { width: 100%; padding: 12px 15px; border: 1px solid var(--border-color); border-radius: 8px; font-size: 14px; min-height: 100px; resize: vertical; font-family: inherit; }
        .tabs { display: flex; gap: 5px; margin-bottom: 20px; border-bottom: 2px solid var(--border-color); }
        .tab { padding: 12px 24px; border: none; background: transparent; cursor: pointer; font-size: 16px; color: var(--text-light); position: relative; transition: all 0.3s ease; }
        .tab:hover { color: var(--primary-color); }
        .tab.active { color: var(--primary-color); font-weight: 500; }
        .tab.active::after { content: ''; position: absolute; bottom: -2px; left: 0; width: 100%; height: 2px; background: var(--primary-color); }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        .job-list { display: grid; gap: 15px; }
        .job-item { background: var(--bg-color); padding: 20px; border-radius: 10px; border-left: 4px solid var(--primary-color); transition: all 0.3s ease; }
        .job-item:hover { box-shadow: var(--shadow); }
        .job-item-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; flex-wrap: wrap; gap: 10px; }
        .job-item-title { font-size: 18px; font-weight: 600; color: var(--text-color); }
        .job-item-price { font-size: 18px; color: var(--danger-color); font-weight: 600; }
        .job-item-meta { display: flex; gap: 15px; flex-wrap: wrap; color: var(--text-light); font-size: 14px; margin-bottom: 10px; }
        .job-item-meta span { display: flex; align-items: center; gap: 5px; }
        .job-item-desc { color: var(--text-light); font-size: 14px; line-height: 1.6; margin-bottom: 15px; }
        .job-item-actions { display: flex; gap: 10px; flex-wrap: wrap; }
        .badge { display: inline-block; padding: 4px 12px; border-radius: 12px; font-size: 12px; font-weight: 500; }
        .badge-primary { background: rgba(74,144,226,0.1); color: var(--primary-color); }
        .badge-success { background: rgba(82,196,26,0.1); color: var(--success-color); }
        .badge-warning { background: rgba(250,173,20,0.1); color: var(--warning-color); }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: 2000; justify-content: center; align-items: center; padding: 20px; }
        .modal.show { display: flex; }
        .modal-content { background: var(--white); border-radius: 12px; max-width: 500px; width: 100%; max-height: 90vh; overflow-y: auto; animation: modalSlide 0.3s ease; }
        @keyframes modalSlide { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
        .modal-header { padding: 20px; border-bottom: 1px solid var(--border-color); display: flex; justify-content: space-between; align-items: center; }
        .modal-title { font-size: 18px; font-weight: 600; }
        .modal-close { background: transparent; border: none; font-size: 24px; cursor: pointer; color: var(--text-light); line-height: 1; }
        .modal-close:hover { color: var(--danger-color); }
        .modal-body { padding: 20px; }
        .modal-footer { padding: 20px; border-top: 1px solid var(--border-color); display: flex; justify-content: flex-end; gap: 10px; }
        .empty-state { text-align: center; padding: 60px 20px; color: var(--text-light); }
        .empty-state-icon { font-size: 64px; margin-bottom: 20px; opacity: 0.5; }
        .empty-state h3 { font-size: 20px; margin-bottom: 10px; color: var(--text-color); }
        .empty-state p { margin-bottom: 20px; }
        .stats { display: grid; grid-template-columns: repeat(auto-fit,minmax(200px,1fr)); gap: 20px; margin-bottom: 30px; }
        .stat-card { background: var(--white); padding: 25px; border-radius: 12px; box-shadow: var(--shadow); text-align: center; }
        .stat-number { font-size: 36px; font-weight: bold; color: var(--primary-color); margin-bottom: 5px; }
        .stat-label { color: var(--text-light); font-size: 14px; }
        .search-filter { display: flex; gap: 15px; margin-bottom: 20px; flex-wrap: wrap; }
        .search-box { flex: 1; min-width: 200px; position: relative; }
        .search-box input { width: 100%; padding: 12px 15px 12px 40px; border: 1px solid var(--border-color); border-radius: 8px; font-size: 14px; }
        .filter-select { min-width: 150px; }
        .toast { position: fixed; top: 100px; right: 20px; padding: 15px 25px; border-radius: 8px; color: var(--white); font-weight: 500; z-index: 3000; animation: toastSlide 0.3s ease; display: none; }
        .toast.show { display: block; }
        .toast-success { background: var(--success-color); }
        .toast-error { background: var(--danger-color); }
        .toast-warning { background: var(--warning-color); }
        @keyframes toastSlide { from { opacity: 0; transform: translateX(100%); } to { opacity: 1; transform: translateX(0); } }
        .profile-header { display: flex; align-items: center; gap: 20px; margin-bottom: 30px; padding-bottom: 20px; border-bottom: 1px solid var(--border-color); }
        .profile-avatar { width: 80px; height: 80px; border-radius: 50%; background: linear-gradient(135deg,var(--primary-color),var(--secondary-color)); display: flex; align-items: center; justify-content: center; font-size: 36px; color: var(--white); }
        .profile-info h2 { font-size: 24px; margin-bottom: 5px; }
        .profile-info p { color: var(--text-light); }
        .info-grid { display: grid; grid-template-columns: repeat(auto-fit,minmax(250px,1fr)); gap: 15px; }
        .info-item { padding: 15px; background: var(--bg-color); border-radius: 8px; }
        .info-item-label { font-size: 12px; color: var(--text-light); margin-bottom: 5px; }
        .info-item-value { font-size: 16px; font-weight: 500; }
        @media (max-width: 768px) {
            .header-content { flex-direction: column; text-align: center; }
            nav { justify-content: center; }
            .hero h1 { font-size: 28px; }
            .hero p { font-size: 16px; }
            .hero-buttons { flex-direction: column; align-items: center; }
            .card { padding: 20px; }
            .form-row { grid-template-columns: 1fr; }
            .job-item-header { flex-direction: column; }
            .profile-header { flex-direction: column; text-align: center; }
            .search-filter { flex-direction: column; }
            .filter-select { width: 100%; }
        }
        .checkbox-group { display: flex; flex-wrap: wrap; gap: 10px; }
        .checkbox-item { display: flex; align-items: center; gap: 8px; padding: 8px 15px; background: var(--bg-color); border-radius: 20px; cursor: pointer; transition: all 0.3s ease; }
        .checkbox-item:hover { background: rgba(74,144,226,0.1); }
        .checkbox-item input { display: none; }
        .checkbox-item.selected { background: var(--primary-color); color: var(--white); }
        .price-range { display: flex; align-items: center; gap: 10px; }
        .price-range input { flex: 1; }
        .price-range span { color: var(--text-light); }
    </style>
</head>
<body>
    <header>
        <div class="container header-content">
            <div class="logo"><span class="logo-icon">🏠</span><span>家政服务系统</span></div>
            <nav id="mainNav">
                <button class="active" id="navHome" onclick="showPage('home')">首页</button>
                <button id="navWorker" onclick="showPage('worker')">求职者入口</button>
                <button id="navEmployer" onclick="showPage('employer')">雇主入口</button>
                <button id="navJobs" onclick="showPage('jobs')">信息浏览</button>
            </nav>
            <div class="user-info" id="userInfo" style="display:none;">
                <div class="user-avatar" id="userAvatar">👤</div>
                <span class="user-name" id="userName"></span>
                <button class="btn-logout" onclick="logout()">退出</button>
            </div>
        </div>
    </header>

    <main class="container">
        <div id="homePage" class="page active">
            <div class="hero">
                <h1>专业家政服务平台</h1>
                <p>连接优质家政服务人员与需求家庭，让生活更美好</p>
                <div class="hero-buttons">
                    <button class="btn btn-primary" onclick="showPage('worker')">我是求职者</button>
                    <button class="btn btn-secondary" onclick="showPage('employer')">我是雇主</button>
                </div>
            </div>
            <div class="card" style="margin-bottom:20px;">
                <div class="card-header"><h3 class="card-title">数据管理</h3></div>
                <div style="display:flex;gap:10px;flex-wrap:wrap;">
                    <button class="btn btn-primary btn-small" onclick="exportData()">📥 导出数据到TXT</button>
                    <button class="btn btn-secondary btn-small" onclick="importData()" style="background:#7B68EE;color:white;border:none;">📤 从TXT导入数据</button>
                    <input type="file" id="importFileInput" accept=".txt" style="display:none;" onchange="handleFileImport(event)">
                </div>
            </div>
            <div class="stats">
                <div class="stat-card"><div class="stat-number" id="totalWorkers">0</div><div class="stat-label">注册求职者</div></div>
                <div class="stat-card"><div class="stat-number" id="totalEmployers">0</div><div class="stat-label">注册雇主</div></div>
                <div class="stat-card"><div class="stat-number" id="totalJobs">0</div><div class="stat-label">发布信息</div></div>
                <div class="stat-card"><div class="stat-number" id="totalMatches">0</div><div class="stat-label">成功匹配</div></div>
            </div>
            <div class="features">
                <div class="feature-card"><div class="feature-icon">👩‍🍳</div><h3>专业保姆</h3><p>经验丰富的保姆，提供专业的家庭照料服务</p></div>
                <div class="feature-card"><div class="feature-icon">👶</div><h3>月嫂服务</h3><p>持证月嫂，为新生儿和产妇提供专业护理</p></div>
                <div class="feature-card"><div class="feature-icon">🧹</div><h3>保洁服务</h3><p>专业保洁人员，让您的家焕然一新</p></div>
                <div class="feature-card"><div class="feature-icon">👴</div><h3>老人护理</h3><p>贴心护理服务，关爱老年人生活</p></div>
            </div>
        </div>

        <div id="workerPage" class="page">
            <div class="card">
                <div class="tabs" data-tab-group="worker">
                    <button class="tab active" data-tab="login">登录</button>
                    <button class="tab" data-tab="register">注册</button>
                </div>
                <div id="workerLoginTab" class="tab-content active">
                    <form id="workerLoginForm" onsubmit="return workerLogin(event)">
                        <div class="form-group"><label>手机号码 <span class="required">*</span></label><input type="tel" class="form-control" id="workerLoginPhone" placeholder="请输入手机号码"><div class="error-message" id="workerLoginPhoneError"></div></div>
                        <div class="form-group"><label>密码 <span class="required">*</span></label><input type="password" class="form-control" id="workerLoginPassword" placeholder="请输入密码"><div class="error-message" id="workerLoginPasswordError"></div></div>
                        <button type="submit" class="btn btn-primary" style="width:100%;">登录</button>
                    </form>
                </div>
                <div id="workerRegisterTab" class="tab-content">
                    <form id="workerRegisterForm" onsubmit="return workerRegister(event)">
                        <div class="form-row">
                            <div class="form-group"><label>姓名 <span class="required">*</span></label><input type="text" class="form-control" id="workerName" placeholder="请输入姓名"><div class="error-message" id="workerNameError"></div></div>
                            <div class="form-group"><label>手机号码 <span class="required">*</span></label><input type="tel" class="form-control" id="workerPhone" placeholder="请输入手机号码"><div class="error-message" id="workerPhoneError"></div></div>
                        </div>
                        <div class="form-row">
                            <div class="form-group"><label>密码 <span class="required">*</span></label><input type="password" class="form-control" id="workerPassword" placeholder="请设置密码（6-20位）"><div class="error-message" id="workerPasswordError"></div></div>
                            <div class="form-group"><label>确认密码 <span class="required">*</span></label><input type="password" class="form-control" id="workerPasswordConfirm" placeholder="请再次输入密码"><div class="error-message" id="workerPasswordConfirmError"></div></div>
                        </div>
                        <div class="form-row">
                            <div class="form-group"><label>年龄 <span class="required">*</span></label><input type="number" class="form-control" id="workerAge" placeholder="请输入年龄" min="18" max="65"><div class="error-message" id="workerAgeError"></div></div>
                            <div class="form-group"><label>性别 <span class="required">*</span></label><select class="form-select" id="workerGender"><option value="">请选择</option><option value="女">女</option><option value="男">男</option></select></div>
                        </div>
                        <div class="form-group"><label>居住地址 <span class="required">*</span></label><input type="text" class="form-control" id="workerAddress" placeholder="请输入详细地址"><div class="error-message" id="workerAddressError"></div></div>
                        <button type="submit" class="btn btn-success" style="width:100%;">注册</button>
                    </form>
                </div>
            </div>
        </div>

        <div id="workerDashboardPage" class="page">
            <div class="profile-header"><div class="profile-avatar">👩‍💼</div><div class="profile-info"><h2 id="workerProfileName"></h2><p id="workerProfilePhone"></p></div></div>
            <div class="tabs" data-tab-group="worker">
                <button class="tab active" data-tab="profile">个人信息</button>
                <button class="tab" data-tab="publish">发布求职</button>
                <button class="tab" data-tab="myJobs">我的求职</button>
            </div>
            <div id="workerProfileTab" class="tab-content active">
                <div class="card"><div class="card-header"><h3 class="card-title">基本信息</h3><button class="btn btn-primary btn-small" onclick="showEditProfileModal()">编辑</button></div><div class="info-grid" id="workerInfoGrid"></div></div>
            </div>
            <div id="workerPublishTab" class="tab-content">
                <div class="card">
                    <div class="card-header"><h3 class="card-title">发布求职信息</h3></div>
                    <form id="publishJobForm" onsubmit="return publishJob(event)">
                        <div class="form-group"><label>服务类型 <span class="required">*</span></label>
                            <div class="checkbox-group" id="serviceTypes">
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="保姆">保姆</label>
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="月嫂">月嫂</label>
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="保洁">保洁</label>
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="老人护理">老人护理</label>
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="育婴师">育婴师</label>
                                <label class="checkbox-item"><input type="checkbox" name="serviceType" value="钟点工">钟点工</label>
                            </div>
                            <div class="error-message" id="serviceTypeError"></div>
                        </div>
                        <div class="form-row">
                            <div class="form-group"><label>工作年限 <span class="required">*</span></label><select class="form-select" id="workExperience"><option value="">请选择</option><option value="1年以下">1年以下</option><option value="1-3年">1-3年</option><option value="3-5年">3-5年</option><option value="5-10年">5-10年</option><option value="10年以上">10年以上</option></select></div>
                            <div class="form-group"><label>学历</label><select class="form-select" id="education"><option value="">请选择</option><option value="小学">小学</option><option value="初中">初中</option><option value="高中">高中</option><option value="大专">大专</option><option value="本科">本科</option></select></div>
                        </div>
                        <div class="form-group"><label>服务价格 <span class="required">*</span></label><div class="price-range"><input type="number" class="form-control" id="priceMin" placeholder="最低价格" min="0"><span>-</span><input type="number" class="form-control" id="priceMax" placeholder="最高价格" min="0"><span>元/月</span></div><div class="error-message" id="priceError"></div></div>
                        <div class="form-group"><label>可用时间 <span class="required">*</span></label><select class="form-select" id="availableTime"><option value="">请选择</option><option value="随时上岗">随时上岗</option><option value="一周内">一周内</option><option value="两周内">两周内</option><option value="一个月内">一个月内</option><option value="待定">待定</option></select></div>
                        <div class="form-group"><label>工作经历描述 <span class="required">*</span></label><textarea class="form-textarea" id="workDescription" placeholder="请详细描述您的工作经历、技能特长等"></textarea><div class="error-message" id="workDescriptionError"></div></div>
                        <div class="form-group"><label>自我介绍</label><textarea class="form-textarea" id="selfIntroduction" placeholder="请简单介绍自己"></textarea></div>
                        <button type="submit" class="btn btn-success" style="width:100%;">发布求职信息</button>
                    </form>
                </div>
            </div>
            <div id="workerMyJobsTab" class="tab-content">
                <div class="card"><div class="card-header"><h3 class="card-title">我发布的求职信息</h3></div><div class="job-list" id="workerJobList"></div></div>
            </div>
        </div>

        <div id="employerPage" class="page">
            <div class="card">
                <div class="tabs" data-tab-group="employer">
                    <button class="tab active" data-tab="login">登录</button>
                    <button class="tab" data-tab="register">注册</button>
                </div>
                <div id="employerLoginTab" class="tab-content active">
                    <form id="employerLoginForm" onsubmit="return employerLogin(event)">
                        <div class="form-group"><label>手机号码 <span class="required">*</span></label><input type="tel" class="form-control" id="employerLoginPhone" placeholder="请输入手机号码"><div class="error-message" id="employerLoginPhoneError"></div></div>
                        <div class="form-group"><label>密码 <span class="required">*</span></label><input type="password" class="form-control" id="employerLoginPassword" placeholder="请输入密码"><div class="error-message" id="employerLoginPasswordError"></div></div>
                        <button type="submit" class="btn btn-primary" style="width:100%;">登录</button>
                    </form>
                </div>
                <div id="employerRegisterTab" class="tab-content">
                    <form id="employerRegisterForm" onsubmit="return employerRegister(event)">
                        <div class="form-row">
                            <div class="form-group"><label>姓名 <span class="required">*</span></label><input type="text" class="form-control" id="employerName" placeholder="请输入姓名"><div class="error-message" id="employerNameError"></div></div>
                            <div class="form-group"><label>手机号码 <span class="required">*</span></label><input type="tel" class="form-control" id="employerPhone" placeholder="请输入手机号码"><div class="error-message" id="employerPhoneError"></div></div>
                        </div>
                        <div class="form-row">
                            <div class="form-group"><label>密码 <span class="required">*</span></label><input type="password" class="form-control" id="employerPassword" placeholder="请设置密码（6-20位）"><div class="error-message" id="employerPasswordError"></div></div>
                            <div class="form-group"><label>确认密码 <span class="required">*</span></label><input type="password" class="form-control" id="employerPasswordConfirm" placeholder="请再次输入密码"><div class="error-message" id="employerPasswordConfirmError"></div></div>
                        </div>
                        <div class="form-group"><label>家庭住址 <span class="required">*</span></label><input type="text" class="form-control" id="employerAddress" placeholder="请输入详细地址"><div class="error-message" id="employerAddressError"></div></div>
                        <button type="submit" class="btn btn-success" style="width:100%;">注册</button>
                    </form>
                </div>
            </div>
        </div>

        <div id="employerDashboardPage" class="page">
            <div class="profile-header"><div class="profile-avatar">👨‍💼</div><div class="profile-info"><h2 id="employerProfileName"></h2><p id="employerProfilePhone"></p></div></div>
            <div class="tabs" data-tab-group="employer">
                <button class="tab active" data-tab="profile">个人信息</button>
                <button class="tab" data-tab="publish">发布雇佣</button>
                <button class="tab" data-tab="myJobs">我的雇佣</button>
            </div>
            <div id="employerProfileTab" class="tab-content active">
                <div class="card"><div class="card-header"><h3 class="card-title">基本信息</h3><button class="btn btn-primary btn-small" onclick="showEditEmployerProfileModal()">编辑</button></div><div class="info-grid" id="employerInfoGrid"></div></div>
            </div>
            <div id="employerPublishTab" class="tab-content">
                <div class="card">
                    <div class="card-header"><h3 class="card-title">发布雇佣信息</h3></div>
                    <form id="publishHireForm" onsubmit="return publishHire(event)">
                        <div class="form-group"><label>所需服务类型 <span class="required">*</span></label>
                            <div class="checkbox-group" id="hireServiceTypes">
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="保姆">保姆</label>
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="月嫂">月嫂</label>
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="保洁">保洁</label>
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="老人护理">老人护理</label>
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="育婴师">育婴师</label>
                                <label class="checkbox-item"><input type="checkbox" name="hireServiceType" value="钟点工">钟点工</label>
                            </div>
                            <div class="error-message" id="hireServiceTypeError"></div>
                        </div>
                        <div class="form-group"><label>工作地点 <span class="required">*</span></label><input type="text" class="form-control" id="hireLocation" placeholder="请输入详细工作地点"><div class="error-message" id="hireLocationError"></div></div>
                        <div class="form-group"><label>薪资范围 <span class="required">*</span></label><div class="price-range"><input type="number" class="form-control" id="hirePriceMin" placeholder="最低薪资" min="0"><span>-</span><input type="number" class="form-control" id="hirePriceMax" placeholder="最高薪资" min="0"><span>元/月</span></div><div class="error-message" id="hirePriceError"></div></div>
                        <div class="form-row">
                            <div class="form-group"><label>服务时间要求 <span class="required">*</span></label><select class="form-select" id="hireTimeRequirement"><option value="">请选择</option><option value="住家">住家</option><option value="白班">白班</option><option value="钟点">钟点</option><option value="周末">周末</option><option value="临时">临时</option></select></div>
                            <div class="form-group"><label>急需程度</label><select class="form-select" id="hireUrgency"><option value="一般">一般</option><option value="较急">较急</option><option value="非常急">非常急</option></select></div>
                        </div>
                        <div class="form-group"><label>工作内容描述 <span class="required">*</span></label><textarea class="form-textarea" id="hireDescription" placeholder="请详细描述工作内容、要求等"></textarea><div class="error-message" id="hireDescriptionError"></div></div>
                        <div class="form-group"><label>其他要求</label><textarea class="form-textarea" id="hireOtherRequirements" placeholder="如有其他要求请填写"></textarea></div>
                        <button type="submit" class="btn btn-success" style="width:100%;">发布雇佣信息</button>
                    </form>
                </div>
            </div>
            <div id="employerMyJobsTab" class="tab-content">
                <div class="card"><div class="card-header"><h3 class="card-title">我发布的雇佣信息</h3></div><div class="job-list" id="employerJobList"></div></div>
            </div>
        </div>

        <div id="jobsPage" class="page">
            <div class="card">
                <div class="card-header"><h3 class="card-title">信息浏览</h3></div>
                <div class="search-filter">
                    <div class="search-box"><input type="text" id="searchKeyword" placeholder="搜索关键词..." oninput="filterJobs()"></div>
                    <select class="form-select filter-select" id="filterType" onchange="filterJobs()">
                        <option value="">全部类型</option><option value="保姆">保姆</option><option value="月嫂">月嫂</option><option value="保洁">保洁</option><option value="老人护理">老人护理</option><option value="育婴师">育婴师</option><option value="钟点工">钟点工</option>
                    </select>
                    <select class="form-select filter-select" id="filterCategory" onchange="filterJobs()">
                        <option value="">全部信息</option><option value="worker">求职信息</option><option value="employer">雇佣信息</option>
                    </select>
                </div>
                <div class="tabs" data-tab-group="jobs">
                    <button class="tab active" data-tab="worker">求职信息</button>
                    <button class="tab" data-tab="employer">雇佣信息</button>
                </div>
                <div id="workerJobsTab" class="tab-content active"><div class="job-list" id="allWorkerJobs"></div></div>
                <div id="employerJobsTab" class="tab-content"><div class="job-list" id="allEmployerJobs"></div></div>
            </div>
        </div>
    </main>

    <div class="modal" id="editProfileModal">
        <div class="modal-content">
            <div class="modal-header"><h3 class="modal-title">编辑个人信息</h3><button class="modal-close" onclick="closeModal('editProfileModal')">&times;</button></div>
            <div class="modal-body">
                <form id="editProfileForm" onsubmit="return updateWorkerProfile(event)">
                    <div class="form-group"><label>姓名 <span class="required">*</span></label><input type="text" class="form-control" id="editWorkerName"></div>
                    <div class="form-row">
                        <div class="form-group"><label>年龄 <span class="required">*</span></label><input type="number" class="form-control" id="editWorkerAge" min="18" max="65"></div>
                        <div class="form-group"><label>性别 <span class="required">*</span></label><select class="form-select" id="editWorkerGender"><option value="女">女</option><option value="男">男</option></select></div>
                    </div>
                    <div class="form-group"><label>居住地址 <span class="required">*</span></label><input type="text" class="form-control" id="editWorkerAddress"></div>
                    <div class="modal-footer"><button type="button" class="btn btn-secondary" onclick="closeModal('editProfileModal')">取消</button><button type="submit" class="btn btn-primary">保存</button></div>
                </form>
            </div>
        </div>
    </div>

    <div class="modal" id="editEmployerProfileModal">
        <div class="modal-content">
            <div class="modal-header"><h3 class="modal-title">编辑个人信息</h3><button class="modal-close" onclick="closeModal('editEmployerProfileModal')">&times;</button></div>
            <div class="modal-body">
                <form id="editEmployerProfileForm" onsubmit="return updateEmployerProfile(event)">
                    <div class="form-group"><label>姓名 <span class="required">*</span></label><input type="text" class="form-control" id="editEmployerName"></div>
                    <div class="form-group"><label>家庭住址 <span class="required">*</span></label><input type="text" class="form-control" id="editEmployerAddress"></div>
                    <div class="modal-footer"><button type="button" class="btn btn-secondary" onclick="closeModal('editEmployerProfileModal')">取消</button><button type="submit" class="btn btn-primary">保存</button></div>
                </form>
            </div>
        </div>
    </div>

    <div class="modal" id="editJobModal">
        <div class="modal-content">
            <div class="modal-header"><h3 class="modal-title">编辑求职信息</h3><button class="modal-close" onclick="closeModal('editJobModal')">&times;</button></div>
            <div class="modal-body">
                <form id="editJobForm" onsubmit="return updateJob(event)">
                    <input type="hidden" id="editJobId">
                    <div class="form-group"><label>服务类型 <span class="required">*</span></label><div class="checkbox-group" id="editServiceTypes"></div></div>
                    <div class="form-row">
                        <div class="form-group"><label>工作年限 <span class="required">*</span></label><select class="form-select" id="editWorkExperience"><option value="1年以下">1年以下</option><option value="1-3年">1-3年</option><option value="3-5年">3-5年</option><option value="5-10年">5-10年</option><option value="10年以上">10年以上</option></select></div>
                        <div class="form-group"><label>学历</label><select class="form-select" id="editEducation"><option value="">请选择</option><option value="小学">小学</option><option value="初中">初中</option><option value="高中">高中</option><option value="大专">大专</option><option value="本科">本科</option></select></div>
                    </div>
                    <div class="form-group"><label>服务价格 <span class="required">*</span></label><div class="price-range"><input type="number" class="form-control" id="editPriceMin" min="0"><span>-</span><input type="number" class="form-control" id="editPriceMax" min="0"><span>元/月</span></div></div>
                    <div class="form-group"><label>可用时间 <span class="required">*</span></label><select class="form-select" id="editAvailableTime"><option value="随时上岗">随时上岗</option><option value="一周内">一周内</option><option value="两周内">两周内</option><option value="一个月内">一个月内</option><option value="待定">待定</option></select></div>
                    <div class="form-group"><label>工作经历描述 <span class="required">*</span></label><textarea class="form-textarea" id="editWorkDescription"></textarea></div>
                    <div class="form-group"><label>自我介绍</label><textarea class="form-textarea" id="editSelfIntroduction"></textarea></div>
                    <div class="modal-footer"><button type="button" class="btn btn-secondary" onclick="closeModal('editJobModal')">取消</button><button type="submit" class="btn btn-primary">保存</button></div>
                </form>
            </div>
        </div>
    </div>

    <div class="modal" id="editHireModal">
        <div class="modal-content">
            <div class="modal-header"><h3 class="modal-title">编辑雇佣信息</h3><button class="modal-close" onclick="closeModal('editHireModal')">&times;</button></div>
            <div class="modal-body">
                <form id="editHireForm" onsubmit="return updateHire(event)">
                    <input type="hidden" id="editHireId">
                    <div class="form-group"><label>所需服务类型 <span class="required">*</span></label><div class="checkbox-group" id="editHireServiceTypes"></div></div>
                    <div class="form-group"><label>工作地点 <span class="required">*</span></label><input type="text" class="form-control" id="editHireLocation"></div>
                    <div class="form-group"><label>薪资范围 <span class="required">*</span></label><div class="price-range"><input type="number" class="form-control" id="editHirePriceMin" min="0"><span>-</span><input type="number" class="form-control" id="editHirePriceMax" min="0"><span>元/月</span></div></div>
                    <div class="form-row">
                        <div class="form-group"><label>服务时间要求 <span class="required">*</span></label><select class="form-select" id="editHireTimeRequirement"><option value="住家">住家</option><option value="白班">白班</option><option value="钟点">钟点</option><option value="周末">周末</option><option value="临时">临时</option></select></div>
                        <div class="form-group"><label>急需程度</label><select class="form-select" id="editHireUrgency"><option value="一般">一般</option><option value="较急">较急</option><option value="非常急">非常急</option></select></div>
                    </div>
                    <div class="form-group"><label>工作内容描述 <span class="required">*</span></label><textarea class="form-textarea" id="editHireDescription"></textarea></div>
                    <div class="form-group"><label>其他要求</label><textarea class="form-textarea" id="editHireOtherRequirements"></textarea></div>
                    <div class="modal-footer"><button type="button" class="btn btn-secondary" onclick="closeModal('editHireModal')">取消</button><button type="submit" class="btn btn-primary">保存</button></div>
                </form>
            </div>
        </div>
    </div>

    <div class="modal" id="viewJobModal">
        <div class="modal-content">
            <div class="modal-header"><h3 class="modal-title">详细信息</h3><button class="modal-close" onclick="closeModal('viewJobModal')">&times;</button></div>
            <div class="modal-body" id="viewJobContent"></div>
        </div>
    </div>

    <div class="toast" id="toast"></div>
    <script>
        let currentUser = null;
        let currentUserType = null;

        // ========== 数据文件名 ==========
        var DATA_FILE = '家政服务系统_用户数据.txt';

        // ========== 初始化 ==========
        function init() {
            setupTabSwitching();
            loadStats();
            loadJobs();
            setupCheckboxGroups();
            var savedUser = localStorage.getItem('currentUser');
            var savedUserType = localStorage.getItem('currentUserType');
            if (savedUser && savedUserType) {
                currentUser = JSON.parse(savedUser);
                currentUserType = savedUserType;
                updateUIForLoggedInUser();
            }
        }

        // ========== Tab 切换（统一机制） ==========
        function setupTabSwitching() {
            document.querySelectorAll('.tabs[data-tab-group]').forEach(function(tabGroup) {
                var prefix = tabGroup.getAttribute('data-tab-group');
                tabGroup.querySelectorAll('.tab[data-tab]').forEach(function(btn) {
                    btn.addEventListener('click', function() {
                        var tabName = this.getAttribute('data-tab');
                        // 更新按钮状态
                        tabGroup.querySelectorAll('.tab').forEach(function(t) { t.classList.remove('active'); });
                        this.classList.add('active');
                        // 更新内容区（限定在当前 page/card 范围内）
                        var container = tabGroup.closest('.page, .card') || tabGroup.parentElement;
                        container.querySelectorAll('.tab-content').forEach(function(c) { c.classList.remove('active'); });
                        var targetId = prefix + tabName.charAt(0).toUpperCase() + tabName.slice(1) + 'Tab';
                        var targetEl = document.getElementById(targetId);
                        if (targetEl) {
                            targetEl.classList.add('active');
                        }
                        // 特殊处理 jobs 页面（ID 命名不同）
                        if (prefix === 'jobs') {
                            var jTarget = document.getElementById(tabName + 'JobsTab');
                            if (jTarget) jTarget.classList.add('active');
                        }
                        // 切换到 profile/myJobs 时加载数据
                        if (tabName === 'profile') {
                            if (currentUserType === 'worker') loadWorkerProfile();
                            else if (currentUserType === 'employer') loadEmployerProfile();
                        } else if (tabName === 'myJobs') {
                            if (currentUserType === 'worker') loadWorkerJobs();
                            else if (currentUserType === 'employer') loadEmployerJobs();
                        }
                    });
                });
            });
        }

        function setupCheckboxGroups() {
            document.querySelectorAll('.checkbox-item').forEach(function(item) {
                item.addEventListener('click', function(e) {
                    if (e.target.tagName !== 'INPUT') {
                        var checkbox = this.querySelector('input[type="checkbox"]');
                        checkbox.checked = !checkbox.checked;
                    }
                    this.classList.toggle('selected', this.querySelector('input[type="checkbox"]').checked);
                });
            });
        }

        function showPage(pageName) {
            document.querySelectorAll('.page').forEach(function(page) { page.classList.remove('active'); });
            document.querySelectorAll('#mainNav button').forEach(function(btn) { btn.classList.remove('active'); });
            if (pageName === 'worker' && currentUser && currentUserType === 'worker') {
                document.getElementById('workerDashboardPage').classList.add('active');
            } else if (pageName === 'employer' && currentUser && currentUserType === 'employer') {
                document.getElementById('employerDashboardPage').classList.add('active');
            } else {
                document.getElementById(pageName + 'Page').classList.add('active');
            }
            var navMap = { home: 'navHome', worker: 'navWorker', employer: 'navEmployer', jobs: 'navJobs' };
            document.getElementById(navMap[pageName]).classList.add('active');
            if (pageName === 'jobs') { loadJobs(); }
        }

        function validatePhone(phone) {
            return /^1[3-9]\d{9}$/.test(phone);
        }

        function validatePassword(password) {
            return password.length >= 6 && password.length <= 20;
        }

        function workerLogin(e) {
            e.preventDefault();
            var phone = document.getElementById('workerLoginPhone').value.trim();
            var password = document.getElementById('workerLoginPassword').value;
            var hasError = false;
            if (!validatePhone(phone)) { showError('workerLoginPhoneError', '请输入正确的手机号码'); hasError = true; }
            else { hideError('workerLoginPhoneError'); }
            if (!validatePassword(password)) { showError('workerLoginPasswordError', '密码长度应为6-20位'); hasError = true; }
            else { hideError('workerLoginPasswordError'); }
            if (hasError) return false;
            var workers = JSON.parse(localStorage.getItem('workers') || '[]');
            var worker = workers.find(function(w) { return w.phone === phone && w.password === password; });
            if (worker) {
                currentUser = worker;
                currentUserType = 'worker';
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                localStorage.setItem('currentUserType', currentUserType);
                showToast('登录成功！', 'success');
                updateUIForLoggedInUser();
                showPage('worker');
                loadWorkerProfile();
            } else {
                showToast('手机号或密码错误', 'error');
            }
            return false;
        }

        function workerRegister(e) {
            e.preventDefault();
            var name = document.getElementById('workerName').value.trim();
            var phone = document.getElementById('workerPhone').value.trim();
            var password = document.getElementById('workerPassword').value;
            var passwordConfirm = document.getElementById('workerPasswordConfirm').value;
            var age = document.getElementById('workerAge').value;
            var gender = document.getElementById('workerGender').value;
            var address = document.getElementById('workerAddress').value.trim();
            var hasError = false;
            if (!name) { showError('workerNameError', '请输入姓名'); hasError = true; } else { hideError('workerNameError'); }
            if (!validatePhone(phone)) { showError('workerPhoneError', '请输入正确的手机号码'); hasError = true; } else { hideError('workerPhoneError'); }
            if (!validatePassword(password)) { showError('workerPasswordError', '密码长度应为6-20位'); hasError = true; } else { hideError('workerPasswordError'); }
            if (password !== passwordConfirm) { showError('workerPasswordConfirmError', '两次输入的密码不一致'); hasError = true; } else { hideError('workerPasswordConfirmError'); }
            if (!address) { showError('workerAddressError', '请输入居住地址'); hasError = true; } else { hideError('workerAddressError'); }
            if (!age || parseInt(age) < 18 || parseInt(age) > 65) { showError('workerAgeError', '年龄应在18-65之间'); hasError = true; } else { hideError('workerAgeError'); }
            if (!gender) { showError('workerGender', '请选择性别'); hasError = true; }
            if (hasError) return false;
            var workers = JSON.parse(localStorage.getItem('workers') || '[]');
            if (workers.find(function(w) { return w.phone === phone; })) {
                showToast('该手机号已注册', 'error');
                return false;
            }
            var newWorker = {
                id: Date.now().toString(),
                name: name,
                phone: phone,
                password: password,
                age: parseInt(age),
                gender: gender,
                address: address,
                createdAt: new Date().toISOString()
            };
            workers.push(newWorker);
            localStorage.setItem('workers', JSON.stringify(workers));
            currentUser = newWorker;
            currentUserType = 'worker';
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            localStorage.setItem('currentUserType', currentUserType);
            showToast('注册成功！', 'success');
            updateUIForLoggedInUser();
            showPage('worker');
            loadWorkerProfile();
            loadStats();
            return false;
        }

        function employerLogin(e) {
            e.preventDefault();
            var phone = document.getElementById('employerLoginPhone').value.trim();
            var password = document.getElementById('employerLoginPassword').value;
            var hasError = false;
            if (!validatePhone(phone)) { showError('employerLoginPhoneError', '请输入正确的手机号码'); hasError = true; }
            else { hideError('employerLoginPhoneError'); }
            if (!validatePassword(password)) { showError('employerLoginPasswordError', '密码长度应为6-20位'); hasError = true; }
            else { hideError('employerLoginPasswordError'); }
            if (hasError) return false;
            var employers = JSON.parse(localStorage.getItem('employers') || '[]');
            var employer = employers.find(function(e) { return e.phone === phone && e.password === password; });
            if (employer) {
                currentUser = employer;
                currentUserType = 'employer';
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                localStorage.setItem('currentUserType', currentUserType);
                showToast('登录成功！', 'success');
                updateUIForLoggedInUser();
                showPage('employer');
                loadEmployerProfile();
            } else {
                showToast('手机号或密码错误', 'error');
            }
            return false;
        }

        function employerRegister(e) {
            e.preventDefault();
            var name = document.getElementById('employerName').value.trim();
            var phone = document.getElementById('employerPhone').value.trim();
            var password = document.getElementById('employerPassword').value;
            var passwordConfirm = document.getElementById('employerPasswordConfirm').value;
            var address = document.getElementById('employerAddress').value.trim();
            var hasError = false;
            if (!name) { showError('employerNameError', '请输入姓名'); hasError = true; } else { hideError('employerNameError'); }
            if (!validatePhone(phone)) { showError('employerPhoneError', '请输入正确的手机号码'); hasError = true; } else { hideError('employerPhoneError'); }
            if (!validatePassword(password)) { showError('employerPasswordError', '密码长度应为6-20位'); hasError = true; } else { hideError('employerPasswordError'); }
            if (password !== passwordConfirm) { showError('employerPasswordConfirmError', '两次输入的密码不一致'); hasError = true; } else { hideError('employerPasswordConfirmError'); }
            if (!address) { showError('employerAddressError', '请输入家庭住址'); hasError = true; } else { hideError('employerAddressError'); }
            if (hasError) return false;
            var employers = JSON.parse(localStorage.getItem('employers') || '[]');
            if (employers.find(function(e) { return e.phone === phone; })) {
                showToast('该手机号已注册', 'error');
                return false;
            }
            var newEmployer = {
                id: Date.now().toString(),
                name: name,
                phone: phone,
                password: password,
                address: address,
                createdAt: new Date().toISOString()
            };
            employers.push(newEmployer);
            localStorage.setItem('employers', JSON.stringify(employers));
            currentUser = newEmployer;
            currentUserType = 'employer';
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            localStorage.setItem('currentUserType', currentUserType);
            showToast('注册成功！', 'success');
            updateUIForLoggedInUser();
            showPage('employer');
            loadEmployerProfile();
            loadStats();
            return false;
        }

        function logout() {
            currentUser = null;
            currentUserType = null;
            localStorage.removeItem('currentUser');
            localStorage.removeItem('currentUserType');
            showToast('已退出登录', 'success');
            updateUIForLoggedInUser();
            showPage('home');
        }

        function updateUIForLoggedInUser() {
            var userInfo = document.getElementById('userInfo');
            var userName = document.getElementById('userName');
            var userAvatar = document.getElementById('userAvatar');
            if (currentUser) {
                userInfo.style.display = 'flex';
                userName.textContent = currentUser.name;
                userAvatar.textContent = currentUserType === 'worker' ? '👩‍💼' : '👨‍💼';
            } else {
                userInfo.style.display = 'none';
            }
        }

        function loadWorkerProfile() {
            if (!currentUser) return;
            document.getElementById('workerProfileName').textContent = currentUser.name;
            document.getElementById('workerProfilePhone').textContent = currentUser.phone;
            document.getElementById('workerInfoGrid').innerHTML =
                '<div class="info-item"><div class="info-item-label">姓名</div><div class="info-item-value">' + currentUser.name + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">手机号码</div><div class="info-item-value">' + currentUser.phone + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">年龄</div><div class="info-item-value">' + currentUser.age + '岁</div></div>' +
                '<div class="info-item"><div class="info-item-label">性别</div><div class="info-item-value">' + currentUser.gender + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">居住地址</div><div class="info-item-value">' + currentUser.address + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">注册时间</div><div class="info-item-value">' + new Date(currentUser.createdAt).toLocaleDateString() + '</div></div>';
        }

        function loadEmployerProfile() {
            if (!currentUser) return;
            document.getElementById('employerProfileName').textContent = currentUser.name;
            document.getElementById('employerProfilePhone').textContent = currentUser.phone;
            document.getElementById('employerInfoGrid').innerHTML =
                '<div class="info-item"><div class="info-item-label">姓名</div><div class="info-item-value">' + currentUser.name + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">手机号码</div><div class="info-item-value">' + currentUser.phone + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">家庭住址</div><div class="info-item-value">' + currentUser.address + '</div></div>' +
                '<div class="info-item"><div class="info-item-label">注册时间</div><div class="info-item-value">' + new Date(currentUser.createdAt).toLocaleDateString() + '</div></div>';
        }

        function showEditProfileModal() {
            document.getElementById('editWorkerName').value = currentUser.name;
            document.getElementById('editWorkerAge').value = currentUser.age;
            document.getElementById('editWorkerGender').value = currentUser.gender;
            document.getElementById('editWorkerAddress').value = currentUser.address;
            document.getElementById('editProfileModal').classList.add('show');
        }

        function showEditEmployerProfileModal() {
            document.getElementById('editEmployerName').value = currentUser.name;
            document.getElementById('editEmployerAddress').value = currentUser.address;
            document.getElementById('editEmployerProfileModal').classList.add('show');
        }

        function updateWorkerProfile(e) {
            e.preventDefault();
            var name = document.getElementById('editWorkerName').value.trim();
            var age = parseInt(document.getElementById('editWorkerAge').value);
            var gender = document.getElementById('editWorkerGender').value;
            var address = document.getElementById('editWorkerAddress').value.trim();
            currentUser.name = name;
            currentUser.age = age;
            currentUser.gender = gender;
            currentUser.address = address;
            var workers = JSON.parse(localStorage.getItem('workers') || '[]');
            var index = workers.findIndex(function(w) { return w.id === currentUser.id; });
            if (index !== -1) { workers[index] = currentUser; localStorage.setItem('workers', JSON.stringify(workers)); }
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            closeModal('editProfileModal');
            showToast('信息更新成功！', 'success');
            loadWorkerProfile();
            updateUIForLoggedInUser();
            return false;
        }

        function updateEmployerProfile(e) {
            e.preventDefault();
            var name = document.getElementById('editEmployerName').value.trim();
            var address = document.getElementById('editEmployerAddress').value.trim();
            currentUser.name = name;
            currentUser.address = address;
            var employers = JSON.parse(localStorage.getItem('employers') || '[]');
            var index = employers.findIndex(function(emp) { return emp.id === currentUser.id; });
            if (index !== -1) { employers[index] = currentUser; localStorage.setItem('employers', JSON.stringify(employers)); }
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
            closeModal('editEmployerProfileModal');
            showToast('信息更新成功！', 'success');
            loadEmployerProfile();
            updateUIForLoggedInUser();
            return false;
        }

        function getSelectedServiceTypes(containerId) {
            var checkboxes = document.querySelectorAll('#' + containerId + ' input[type="checkbox"]:checked');
            var result = [];
            checkboxes.forEach(function(cb) { result.push(cb.value); });
            return result;
        }

        function publishJob(e) {
            e.preventDefault();
            var serviceTypes = getSelectedServiceTypes('serviceTypes');
            var workExperience = document.getElementById('workExperience').value;
            var education = document.getElementById('education').value;
            var priceMin = parseInt(document.getElementById('priceMin').value);
            var priceMax = parseInt(document.getElementById('priceMax').value);
            var availableTime = document.getElementById('availableTime').value;
            var workDescription = document.getElementById('workDescription').value.trim();
            var selfIntroduction = document.getElementById('selfIntroduction').value.trim();
            var hasError = false;
            if (serviceTypes.length === 0) { showError('serviceTypeError', '请至少选择一种服务类型'); hasError = true; }
            else { hideError('serviceTypeError'); }
            if (isNaN(priceMin) || isNaN(priceMax) || priceMin >= priceMax) { showError('priceError', '请输入有效的价格范围（最低价应小于最高价）'); hasError = true; }
            else { hideError('priceError'); }
            if (!workDescription) { showError('workDescriptionError', '请填写工作经历描述'); hasError = true; }
            else { hideError('workDescriptionError'); }
            if (!workExperience) { hasError = true; }
            if (!availableTime) { hasError = true; }
            if (hasError) return false;
            var job = {
                id: Date.now().toString(),
                workerId: currentUser.id,
                workerName: currentUser.name,
                workerPhone: currentUser.phone,
                serviceTypes: serviceTypes,
                workExperience: workExperience,
                education: education,
                priceMin: priceMin,
                priceMax: priceMax,
                availableTime: availableTime,
                workDescription: workDescription,
                selfIntroduction: selfIntroduction,
                createdAt: new Date().toISOString()
            };
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            jobs.push(job);
            localStorage.setItem('workerJobs', JSON.stringify(jobs));
            showToast('求职信息发布成功！', 'success');
            document.getElementById('publishJobForm').reset();
            document.querySelectorAll('#serviceTypes .checkbox-item').forEach(function(item) { item.classList.remove('selected'); });
            setupCheckboxGroups();
            loadStats();
            return false;
        }

        function publishHire(e) {
            e.preventDefault();
            var serviceTypes = getSelectedServiceTypes('hireServiceTypes');
            var location = document.getElementById('hireLocation').value.trim();
            var priceMin = parseInt(document.getElementById('hirePriceMin').value);
            var priceMax = parseInt(document.getElementById('hirePriceMax').value);
            var timeRequirement = document.getElementById('hireTimeRequirement').value;
            var urgency = document.getElementById('hireUrgency').value;
            var description = document.getElementById('hireDescription').value.trim();
            var otherRequirements = document.getElementById('hireOtherRequirements').value.trim();
            var hasError = false;
            if (serviceTypes.length === 0) { showError('hireServiceTypeError', '请至少选择一种服务类型'); hasError = true; }
            else { hideError('hireServiceTypeError'); }
            if (!location) { showError('hireLocationError', '请输入工作地点'); hasError = true; }
            else { hideError('hireLocationError'); }
            if (isNaN(priceMin) || isNaN(priceMax) || priceMin >= priceMax) { showError('hirePriceError', '请输入有效的薪资范围（最低薪资应小于最高薪资）'); hasError = true; }
            else { hideError('hirePriceError'); }
            if (!description) { showError('hireDescriptionError', '请填写工作内容描述'); hasError = true; }
            else { hideError('hireDescriptionError'); }
            if (!timeRequirement) { hasError = true; }
            if (hasError) return false;
            var hire = {
                id: Date.now().toString(),
                employerId: currentUser.id,
                employerName: currentUser.name,
                employerPhone: currentUser.phone,
                serviceTypes: serviceTypes,
                location: location,
                priceMin: priceMin,
                priceMax: priceMax,
                timeRequirement: timeRequirement,
                urgency: urgency,
                description: description,
                otherRequirements: otherRequirements,
                createdAt: new Date().toISOString()
            };
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            hires.push(hire);
            localStorage.setItem('employerJobs', JSON.stringify(hires));
            showToast('雇佣信息发布成功！', 'success');
            document.getElementById('publishHireForm').reset();
            document.querySelectorAll('#hireServiceTypes .checkbox-item').forEach(function(item) { item.classList.remove('selected'); });
            setupCheckboxGroups();
            loadStats();
            return false;
        }

        function loadStats() {
            var workers = JSON.parse(localStorage.getItem('workers') || '[]');
            var employers = JSON.parse(localStorage.getItem('employers') || '[]');
            var workerJobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var employerJobs = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var totalJobs = workerJobs.length + employerJobs.length;
            var totalMatches = Math.min(workerJobs.length, employerJobs.length);
            document.getElementById('totalWorkers').textContent = workers.length;
            document.getElementById('totalEmployers').textContent = employers.length;
            document.getElementById('totalJobs').textContent = totalJobs;
            document.getElementById('totalMatches').textContent = totalMatches;
        }

        function loadWorkerJobs() {
            var container = document.getElementById('workerJobList');
            if (!currentUser || currentUserType !== 'worker') return;
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var myJobs = jobs.filter(function(j) { return j.workerId === currentUser.id; });
            if (myJobs.length === 0) {
                container.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📋</div><h3>暂无求职信息</h3><p>还没有发布任何求职信息</p></div>';
            } else {
                container.innerHTML = myJobs.map(function(job) {
                    return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + job.serviceTypes.join('、') + '</div><div class="job-item-price">' + job.priceMin + '-' + job.priceMax + '元/月</div></div><div class="job-item-meta"><span>📅 ' + job.availableTime + '</span><span>📅 ' + new Date(job.createdAt).toLocaleDateString() + '</span></div><div class="job-item-desc">' + job.workDescription.substring(0, 100) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="editJob(\'' + job.id + '\')">编辑</button><button class="btn btn-danger btn-small" onclick="deleteJob(\'' + job.id + '\')">删除</button></div></div>';
                }).join('');
            }
        }

        function loadEmployerJobs() {
            var container = document.getElementById('employerJobList');
            if (!currentUser || currentUserType !== 'employer') return;
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var myHires = hires.filter(function(h) { return h.employerId === currentUser.id; });
            if (myHires.length === 0) {
                container.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📋</div><h3>暂无雇佣信息</h3><p>还没有发布任何雇佣信息</p></div>';
            } else {
                container.innerHTML = myHires.map(function(hire) {
                    return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + hire.serviceTypes.join('、') + '</div><div class="job-item-price">' + hire.priceMin + '-' + hire.priceMax + '元/月</div></div><div class="job-item-meta"><span>📍 ' + hire.location + '</span><span>⏰ ' + hire.timeRequirement + '</span><span class="badge badge-warning">' + hire.urgency + '</span></div><div class="job-item-desc">' + hire.description.substring(0, 100) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="editHire(\'' + hire.id + '\')">编辑</button><button class="btn btn-danger btn-small" onclick="deleteHire(\'' + hire.id + '\')">删除</button></div></div>';
                }).join('');
            }
        }

        function loadJobs() {
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var workerContainer = document.getElementById('allWorkerJobs');
            var employerContainer = document.getElementById('allEmployerJobs');
            if (jobs.length === 0) {
                workerContainer.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📋</div><h3>暂无求职信息</h3><p>还没有求职者发布信息</p></div>';
            } else {
                workerContainer.innerHTML = jobs.map(function(job) {
                    return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + job.serviceTypes.join('、') + '</div><div class="job-item-price">' + job.priceMin + '-' + job.priceMax + '元/月</div></div><div class="job-item-meta"><span>👤 ' + job.workerName + '</span><span>📍 ' + job.workExperience + '</span><span>📅 ' + job.availableTime + '</span></div><div class="job-item-desc">' + job.workDescription.substring(0, 150) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="viewJob(\'' + job.id + '\', \'worker\')">查看详情</button></div></div>';
                }).join('');
            }
            if (hires.length === 0) {
                employerContainer.innerHTML = '<div class="empty-state"><div class="empty-state-icon">📋</div><h3>暂无雇佣信息</h3><p>还没有雇主发布信息</p></div>';
            } else {
                employerContainer.innerHTML = hires.map(function(hire) {
                    return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + hire.serviceTypes.join('、') + '</div><div class="job-item-price">' + hire.priceMin + '-' + hire.priceMax + '元/月</div></div><div class="job-item-meta"><span>👤 ' + hire.employerName + '</span><span>📍 ' + hire.location + '</span><span>⏰ ' + hire.timeRequirement + '</span></div><div class="job-item-desc">' + hire.description.substring(0, 150) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="viewJob(\'' + hire.id + '\', \'employer\')">查看详情</button></div></div>';
                }).join('');
            }
        }

        function filterJobs() {
            var keyword = document.getElementById('searchKeyword').value.toLowerCase();
            var filterType = document.getElementById('filterType').value;
            var filterCategory = document.getElementById('filterCategory').value;
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var filteredJobs = jobs.filter(function(job) {
                var matchKeyword = !keyword || job.serviceTypes.some(function(t) { return t.toLowerCase().indexOf(keyword) !== -1; }) || job.workDescription.toLowerCase().indexOf(keyword) !== -1 || job.workerName.toLowerCase().indexOf(keyword) !== -1;
                var matchType = !filterType || job.serviceTypes.indexOf(filterType) !== -1;
                return matchKeyword && matchType;
            });
            var filteredHires = hires.filter(function(hire) {
                var matchKeyword = !keyword || hire.serviceTypes.some(function(t) { return t.toLowerCase().indexOf(keyword) !== -1; }) || hire.description.toLowerCase().indexOf(keyword) !== -1 || hire.employerName.toLowerCase().indexOf(keyword) !== -1 || hire.location.toLowerCase().indexOf(keyword) !== -1;
                var matchType = !filterType || hire.serviceTypes.indexOf(filterType) !== -1;
                return matchKeyword && matchType;
            });
            var workerContainer = document.getElementById('allWorkerJobs');
            var employerContainer = document.getElementById('allEmployerJobs');
            if (filterCategory !== 'employer') {
                if (filteredJobs.length === 0) {
                    workerContainer.innerHTML = '<div class="empty-state"><div class="empty-state-icon">🔍</div><h3>未找到相关信息</h3><p>请尝试其他搜索条件</p></div>';
                } else {
                    workerContainer.innerHTML = filteredJobs.map(function(job) {
                        return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + job.serviceTypes.join('、') + '</div><div class="job-item-price">' + job.priceMin + '-' + job.priceMax + '元/月</div></div><div class="job-item-meta"><span>👤 ' + job.workerName + '</span><span>📍 ' + job.workExperience + '</span><span>📅 ' + job.availableTime + '</span></div><div class="job-item-desc">' + job.workDescription.substring(0, 150) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="viewJob(\'' + job.id + '\', \'worker\')">查看详情</button></div></div>';
                    }).join('');
                }
            }
            if (filterCategory !== 'worker') {
                if (filteredHires.length === 0) {
                    employerContainer.innerHTML = '<div class="empty-state"><div class="empty-state-icon">🔍</div><h3>未找到相关信息</h3><p>请尝试其他搜索条件</p></div>';
                } else {
                    employerContainer.innerHTML = filteredHires.map(function(hire) {
                        return '<div class="job-item"><div class="job-item-header"><div class="job-item-title">' + hire.serviceTypes.join('、') + '</div><div class="job-item-price">' + hire.priceMin + '-' + hire.priceMax + '元/月</div></div><div class="job-item-meta"><span>👤 ' + hire.employerName + '</span><span>📍 ' + hire.location + '</span><span>⏰ ' + hire.timeRequirement + '</span></div><div class="job-item-desc">' + hire.description.substring(0, 150) + '</div><div class="job-item-actions"><button class="btn btn-primary btn-small" onclick="viewJob(\'' + hire.id + '\', \'employer\')">查看详情</button></div></div>';
                    }).join('');
                }
            }
        }

        function viewJob(id, type) {
            var storage = type === 'worker' ? 'workerJobs' : 'employerJobs';
            var jobs = JSON.parse(localStorage.getItem(storage) || '[]');
            var job = jobs.find(function(j) { return j.id === id; });
            if (!job) return;
            var content = '';
            if (type === 'worker') {
                content = '<div class="info-grid"><div class="info-item"><div class="info-item-label">求职者姓名</div><div class="info-item-value">' + job.workerName + '</div></div><div class="info-item"><div class="info-item-label">联系电话</div><div class="info-item-value">' + job.workerPhone + '</div></div><div class="info-item"><div class="info-item-label">服务类型</div><div class="info-item-value">' + job.serviceTypes.join('、') + '</div></div><div class="info-item"><div class="info-item-label">工作年限</div><div class="info-item-value">' + job.workExperience + '</div></div><div class="info-item"><div class="info-item-label">学历</div><div class="info-item-value">' + (job.education || '不限') + '</div></div><div class="info-item"><div class="info-item-label">期望薪资</div><div class="info-item-value">' + job.priceMin + '-' + job.priceMax + '元/月</div></div><div class="info-item"><div class="info-item-label">可用时间</div><div class="info-item-value">' + job.availableTime + '</div></div><div class="info-item"><div class="info-item-label">发布时间</div><div class="info-item-value">' + new Date(job.createdAt).toLocaleDateString() + '</div></div></div><div class="info-item" style="margin-top:15px;"><div class="info-item-label">工作经历描述</div><div class="info-item-value">' + job.workDescription + '</div></div>' + (job.selfIntroduction ? '<div class="info-item" style="margin-top:15px;"><div class="info-item-label">自我介绍</div><div class="info-item-value">' + job.selfIntroduction + '</div></div>' : '');
            } else {
                content = '<div class="info-grid"><div class="info-item"><div class="info-item-label">雇主姓名</div><div class="info-item-value">' + job.employerName + '</div></div><div class="info-item"><div class="info-item-label">联系电话</div><div class="info-item-value">' + job.employerPhone + '</div></div><div class="info-item"><div class="info-item-label">所需服务</div><div class="info-item-value">' + job.serviceTypes.join('、') + '</div></div><div class="info-item"><div class="info-item-label">工作地点</div><div class="info-item-value">' + job.location + '</div></div><div class="info-item"><div class="info-item-label">薪资范围</div><div class="info-item-value">' + job.priceMin + '-' + job.priceMax + '元/月</div></div><div class="info-item"><div class="info-item-label">服务时间</div><div class="info-item-value">' + job.timeRequirement + '</div></div><div class="info-item"><div class="info-item-label">急需程度</div><div class="info-item-value">' + job.urgency + '</div></div><div class="info-item"><div class="info-item-label">发布时间</div><div class="info-item-value">' + new Date(job.createdAt).toLocaleDateString() + '</div></div></div><div class="info-item" style="margin-top:15px;"><div class="info-item-label">工作内容描述</div><div class="info-item-value">' + job.description + '</div></div>' + (job.otherRequirements ? '<div class="info-item" style="margin-top:15px;"><div class="info-item-label">其他要求</div><div class="info-item-value">' + job.otherRequirements + '</div></div>' : '');
            }
            document.getElementById('viewJobContent').innerHTML = content;
            document.getElementById('viewJobModal').classList.add('show');
        }

        function deleteJob(id) {
            if (!confirm('确定要删除这条求职信息吗？')) return;
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var newJobs = jobs.filter(function(j) { return j.id !== id; });
            localStorage.setItem('workerJobs', JSON.stringify(newJobs));
            showToast('删除成功！', 'success');
            loadWorkerJobs();
            loadStats();
        }

        function deleteHire(id) {
            if (!confirm('确定要删除这条雇佣信息吗？')) return;
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var newHires = hires.filter(function(h) { return h.id !== id; });
            localStorage.setItem('employerJobs', JSON.stringify(newHires));
            showToast('删除成功！', 'success');
            loadEmployerJobs();
            loadStats();
        }

        function editJob(id) {
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var job = jobs.find(function(j) { return j.id === id; });
            if (!job) return;
            document.getElementById('editJobId').value = job.id;
            var types = ['保姆', '月嫂', '保洁', '老人护理', '育婴师', '钟点工'];
            var serviceTypesHtml = types.map(function(type) {
                var checked = job.serviceTypes.indexOf(type) !== -1 ? ' checked' : '';
                var selectedClass = job.serviceTypes.indexOf(type) !== -1 ? ' selected' : '';
                return '<label class="checkbox-item' + selectedClass + '"><input type="checkbox" name="editServiceType" value="' + type + '"' + checked + '>' + type + '</label>';
            }).join('');
            document.getElementById('editServiceTypes').innerHTML = serviceTypesHtml;
            document.getElementById('editWorkExperience').value = job.workExperience;
            document.getElementById('editEducation').value = job.education || '';
            document.getElementById('editPriceMin').value = job.priceMin;
            document.getElementById('editPriceMax').value = job.priceMax;
            document.getElementById('editAvailableTime').value = job.availableTime;
            document.getElementById('editWorkDescription').value = job.workDescription;
            document.getElementById('editSelfIntroduction').value = job.selfIntroduction || '';
            document.querySelectorAll('#editServiceTypes .checkbox-item').forEach(function(item) {
                item.addEventListener('click', function(e) {
                    if (e.target.tagName !== 'INPUT') {
                        var checkbox = this.querySelector('input[type="checkbox"]');
                        checkbox.checked = !checkbox.checked;
                    }
                    this.classList.toggle('selected', this.querySelector('input[type="checkbox"]').checked);
                });
            });
            document.getElementById('editJobModal').classList.add('show');
        }

        function editHire(id) {
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var hire = hires.find(function(h) { return h.id === id; });
            if (!hire) return;
            document.getElementById('editHireId').value = hire.id;
            var types = ['保姆', '月嫂', '保洁', '老人护理', '育婴师', '钟点工'];
            var serviceTypesHtml = types.map(function(type) {
                var checked = hire.serviceTypes.indexOf(type) !== -1 ? ' checked' : '';
                var selectedClass = hire.serviceTypes.indexOf(type) !== -1 ? ' selected' : '';
                return '<label class="checkbox-item' + selectedClass + '"><input type="checkbox" name="editHireServiceType" value="' + type + '"' + checked + '>' + type + '</label>';
            }).join('');
            document.getElementById('editHireServiceTypes').innerHTML = serviceTypesHtml;
            document.getElementById('editHireLocation').value = hire.location;
            document.getElementById('editHirePriceMin').value = hire.priceMin;
            document.getElementById('editHirePriceMax').value = hire.priceMax;
            document.getElementById('editHireTimeRequirement').value = hire.timeRequirement;
            document.getElementById('editHireUrgency').value = hire.urgency;
            document.getElementById('editHireDescription').value = hire.description;
            document.getElementById('editHireOtherRequirements').value = hire.otherRequirements || '';
            document.querySelectorAll('#editHireServiceTypes .checkbox-item').forEach(function(item) {
                item.addEventListener('click', function(e) {
                    if (e.target.tagName !== 'INPUT') {
                        var checkbox = this.querySelector('input[type="checkbox"]');
                        checkbox.checked = !checkbox.checked;
                    }
                    this.classList.toggle('selected', this.querySelector('input[type="checkbox"]').checked);
                });
            });
            document.getElementById('editHireModal').classList.add('show');
        }

        function updateJob(e) {
            e.preventDefault();
            var id = document.getElementById('editJobId').value;
            var checkboxes = document.querySelectorAll('#editServiceTypes input[type="checkbox"]:checked');
            var serviceTypes = Array.from(checkboxes).map(function(cb) { return cb.value; });
            var workExperience = document.getElementById('editWorkExperience').value;
            var education = document.getElementById('editEducation').value;
            var priceMin = parseInt(document.getElementById('editPriceMin').value);
            var priceMax = parseInt(document.getElementById('editPriceMax').value);
            var availableTime = document.getElementById('editAvailableTime').value;
            var workDescription = document.getElementById('editWorkDescription').value.trim();
            var selfIntroduction = document.getElementById('editSelfIntroduction').value.trim();
            var jobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var index = jobs.findIndex(function(j) { return j.id === id; });
            if (index !== -1) {
                jobs[index] = {
                    id: jobs[index].id,
                    workerId: jobs[index].workerId,
                    workerName: jobs[index].workerName,
                    workerPhone: jobs[index].workerPhone,
                    createdAt: jobs[index].createdAt,
                    serviceTypes: serviceTypes,
                    workExperience: workExperience,
                    education: education,
                    priceMin: priceMin,
                    priceMax: priceMax,
                    availableTime: availableTime,
                    workDescription: workDescription,
                    selfIntroduction: selfIntroduction
                };
                localStorage.setItem('workerJobs', JSON.stringify(jobs));
            }
            closeModal('editJobModal');
            showToast('更新成功！', 'success');
            loadWorkerJobs();
        }

        function updateHire(e) {
            e.preventDefault();
            var id = document.getElementById('editHireId').value;
            var checkboxes = document.querySelectorAll('#editHireServiceTypes input[type="checkbox"]:checked');
            var serviceTypes = Array.from(checkboxes).map(function(cb) { return cb.value; });
            var location = document.getElementById('editHireLocation').value.trim();
            var priceMin = parseInt(document.getElementById('editHirePriceMin').value);
            var priceMax = parseInt(document.getElementById('editHirePriceMax').value);
            var timeRequirement = document.getElementById('editHireTimeRequirement').value;
            var urgency = document.getElementById('editHireUrgency').value;
            var description = document.getElementById('editHireDescription').value.trim();
            var otherRequirements = document.getElementById('editHireOtherRequirements').value.trim();
            var hires = JSON.parse(localStorage.getItem('employerJobs') || '[]');
            var index = hires.findIndex(function(h) { return h.id === id; });
            if (index !== -1) {
                hires[index] = {
                    id: hires[index].id,
                    employerId: hires[index].employerId,
                    employerName: hires[index].employerName,
                    employerPhone: hires[index].employerPhone,
                    createdAt: hires[index].createdAt,
                    serviceTypes: serviceTypes,
                    location: location,
                    priceMin: priceMin,
                    priceMax: priceMax,
                    timeRequirement: timeRequirement,
                    urgency: urgency,
                    description: description,
                    otherRequirements: otherRequirements
                };
                localStorage.setItem('employerJobs', JSON.stringify(hires));
            }
            closeModal('editHireModal');
            showToast('更新成功！', 'success');
            loadEmployerJobs();
        }

        function showError(id, message) {
            var el = document.getElementById(id);
            if (el) {
                el.textContent = message;
                el.classList.add('show');
                var input = el.previousElementSibling;
                if (input) input.classList.add('error');
            }
        }

        function hideError(id) {
            var el = document.getElementById(id);
            if (el) {
                el.classList.remove('show');
                var input = el.previousElementSibling;
                if (input) input.classList.remove('error');
            }
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('show');
        }

        function showToast(message, type) {
            var toast = document.getElementById('toast');
            toast.textContent = message;
            toast.className = 'toast toast-' + (type || 'success') + ' show';
            setTimeout(function() { toast.classList.remove('show'); }, 3000);
        }

        window.addEventListener('load', init);

        document.querySelectorAll('.modal').forEach(function(modal) {
            modal.addEventListener('click', function(e) {
                if (e.target === modal) modal.classList.remove('show');
            });
        });

        // ========== TXT 文件导出/导入 ==========
        function exportData() {
            var workers = JSON.parse(localStorage.getItem('workers') || '[]');
            var employers = JSON.parse(localStorage.getItem('employers') || '[]');
            var workerJobs = JSON.parse(localStorage.getItem('workerJobs') || '[]');
            var employerJobs = JSON.parse(localStorage.getItem('employerJobs') || '[]');

            var lines = [];
            lines.push('========================================');
            lines.push('  家政服务系统 - 用户数据');
            lines.push('  导出时间: ' + new Date().toLocaleString());
            lines.push('========================================');
            lines.push('');

            lines.push('--- 求职者账号 ---');
            lines.push('共 ' + workers.length + ' 条记录');
            lines.push('序号 | 姓名 | 手机号 | 密码 | 年龄 | 性别 | 地址 | 注册时间');
            lines.push('---');
            workers.forEach(function(w, i) {
                lines.push([
                    i + 1, w.name, w.phone, w.password,
                    w.age || '', w.gender || '', w.address || '',
                    new Date(w.createdAt).toLocaleString()
                ].join(' | '));
            });
            lines.push('');

            lines.push('--- 雇主账号 ---');
            lines.push('共 ' + employers.length + ' 条记录');
            lines.push('序号 | 姓名 | 手机号 | 密码 | 地址 | 注册时间');
            lines.push('---');
            employers.forEach(function(e, i) {
                lines.push([
                    i + 1, e.name, e.phone, e.password,
                    e.address || '',
                    new Date(e.createdAt).toLocaleString()
                ].join(' | '));
            });
            lines.push('');

            lines.push('--- 求职信息 ---');
            workerJobs.forEach(function(j) {
                lines.push('求职者: ' + j.workerName + ' | 电话: ' + j.workerPhone +
                    ' | 类型: ' + j.serviceTypes.join('、') +
                    ' | 薪资: ' + j.priceMin + '-' + j.priceMax + '元/月' +
                    ' | 年限: ' + j.workExperience +
                    ' | 时间: ' + j.availableTime);
                lines.push('  描述: ' + j.workDescription);
                if (j.selfIntroduction) lines.push('  自我介绍: ' + j.selfIntroduction);
                lines.push('');
            });

            lines.push('--- 雇佣信息 ---');
            employerJobs.forEach(function(h) {
                lines.push('雇主: ' + h.employerName + ' | 电话: ' + h.employerPhone +
                    ' | 类型: ' + h.serviceTypes.join('、') +
                    ' | 薪资: ' + h.priceMin + '-' + h.priceMax + '元/月' +
                    ' | 地点: ' + h.location +
                    ' | 时间: ' + h.timeRequirement +
                    ' | 紧急: ' + h.urgency);
                lines.push('  描述: ' + h.description);
                if (h.otherRequirements) lines.push('  其他要求: ' + h.otherRequirements);
                lines.push('');
            });

            var content = lines.join('\r\n');
            var blob = new Blob(['\uFEFF' + content], { type: 'text/plain;charset=utf-8' });
            var url = URL.createObjectURL(blob);
            var a = document.createElement('a');
            a.href = url;
            a.download = DATA_FILE;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
            showToast('数据已导出到 ' + DATA_FILE, 'success');
        }

        function importData() {
            document.getElementById('importFileInput').click();
        }

        function handleFileImport(event) {
            var file = event.target.files[0];
            if (!file) return;
            var reader = new FileReader();
            reader.onload = function(e) {
                var content = e.target.result;
                var workers = parseWorkersFromText(content);
                var employers = parseEmployersFromText(content);
                if (workers.length === 0 && employers.length === 0) {
                    showToast('未从文件中解析到有效账号数据，请确认文件格式', 'error');
                    return;
                }
                // 合并到现有数据（不覆盖已存在的手机号）
                var existingWorkers = JSON.parse(localStorage.getItem('workers') || '[]');
                var existingEmployers = JSON.parse(localStorage.getItem('employers') || '[]');
                var addedW = 0, addedE = 0;
                workers.forEach(function(w) {
                    if (!existingWorkers.find(function(ew) { return ew.phone === w.phone; })) {
                        existingWorkers.push(w);
                        addedW++;
                    }
                });
                employers.forEach(function(e) {
                    if (!existingEmployers.find(function(ee) { return ee.phone === e.phone; })) {
                        existingEmployers.push(e);
                        addedE++;
                    }
                });
                localStorage.setItem('workers', JSON.stringify(existingWorkers));
                localStorage.setItem('employers', JSON.stringify(existingEmployers));
                showToast('导入完成！新增求职者: ' + addedW + '，新增雇主: ' + addedE, 'success');
                loadStats();
            };
            reader.readAsText(file, 'UTF-8');
            event.target.value = '';
        }

        function parseWorkersFromText(content) {
            var workers = [];
            var inWorkerSection = false;
            var lines = content.split(/\r?\n/);
            for (var i = 0; i < lines.length; i++) {
                var line = lines[i].trim();
                if (line.indexOf('--- 求职者账号 ---') !== -1) { inWorkerSection = true; continue; }
                if (line.indexOf('--- 雇主账号 ---') !== -1) { inWorkerSection = false; continue; }
                if (!inWorkerSection) continue;
                if (!line || line.indexOf('共 ') === 0 || line.indexOf('序号 |') === 0 || line === '---') continue;
                var cols = line.split('|').map(function(c) { return c.trim(); });
                if (cols.length >= 8) {
                    workers.push({
                        id: Date.now().toString() + '_w_' + workers.length,
                        name: cols[1], phone: cols[2], password: cols[3],
                        age: parseInt(cols[4]) || 0, gender: cols[5], address: cols[6],
                        createdAt: new Date().toISOString()
                    });
                }
            }
            return workers;
        }

        function parseEmployersFromText(content) {
            var employers = [];
            var inEmployerSection = false;
            var lines = content.split(/\r?\n/);
            for (var i = 0; i < lines.length; i++) {
                var line = lines[i].trim();
                if (line.indexOf('--- 雇主账号 ---') !== -1) { inEmployerSection = true; continue; }
                if (line.indexOf('--- 求职信息 ---') !== -1) { inEmployerSection = false; continue; }
                if (!inEmployerSection) continue;
                if (!line || line.indexOf('共 ') === 0 || line.indexOf('序号 |') === 0 || line === '---') continue;
                var cols = line.split('|').map(function(c) { return c.trim(); });
                if (cols.length >= 6) {
                    employers.push({
                        id: Date.now().toString() + '_e_' + employers.length,
                        name: cols[1], phone: cols[2], password: cols[3],
                        address: cols[4],
                        createdAt: new Date().toISOString()
                    });
                }
            }
            return employers;
        }
    </script>
</body>
</html>
