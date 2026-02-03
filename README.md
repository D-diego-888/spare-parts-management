# spare-parts-management
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>渣选厂备件管理系统</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }

        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }

        .login-page {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: linear-gradient(135deg, #1a3a5f 0%, #2c5282 100%);
        }

        .login-container {
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            padding: 40px;
            width: 90%;
            max-width: 400px;
            text-align: center;
        }

        .login-container h1 {
            color: #1a3a5f;
            margin-bottom: 10px;
            font-size: 28px;
        }

        .login-container p {
            color: #666;
            margin-bottom: 30px;
            font-size: 14px;
        }

        .login-form {
            text-align: left;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #444;
        }

        .form-group input {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            transition: border 0.3s;
        }

        .form-group input:focus {
            border-color: #2c5282;
            outline: none;
            box-shadow: 0 0 0 2px rgba(44, 82, 130, 0.2);
        }

        .login-btn {
            background-color: #2c5282;
            color: white;
            border: none;
            padding: 14px 20px;
            width: 100%;
            border-radius: 6px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .login-btn:hover {
            background-color: #1a3a5f;
        }

        .error-message {
            color: #e53e3e;
            font-size: 14px;
            margin-top: 10px;
            display: none;
        }

        .main-container {
            display: none;
        }

        .header {
            background: linear-gradient(to right, #1a3a5f, #2c5282);
            color: white;
            padding: 18px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
        }

        .header h1 {
            font-size: 24px;
            display: flex;
            align-items: center;
        }

        .header h1 i {
            margin-right: 12px;
        }

        .user-info {
            display: flex;
            align-items: center;
        }

        .user-info i {
            margin-right: 8px;
            font-size: 18px;
        }

        .logout-btn {
            background-color: rgba(255, 255, 255, 0.2);
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            margin-left: 15px;
            transition: background-color 0.3s;
        }

        .logout-btn:hover {
            background-color: rgba(255, 255, 255, 0.3);
        }

        .sidebar {
            background-color: white;
            width: 250px;
            height: calc(100vh - 70px);
            position: fixed;
            box-shadow: 2px 0 10px rgba(0, 0, 0, 0.05);
            padding-top: 20px;
        }

        .sidebar ul {
            list-style: none;
        }

        .sidebar li {
            margin-bottom: 2px;
        }

        .sidebar a {
            display: flex;
            align-items: center;
            padding: 15px 20px;
            color: #555;
            text-decoration: none;
            transition: all 0.3s;
            border-left: 4px solid transparent;
        }

        .sidebar a:hover, .sidebar a.active {
            background-color: #f0f7ff;
            color: #2c5282;
            border-left-color: #2c5282;
        }

        .sidebar a i {
            margin-right: 12px;
            width: 20px;
            text-align: center;
        }

        .content {
            margin-left: 250px;
            padding: 30px;
            min-height: calc(100vh - 70px);
        }

        .page {
            display: none;
            animation: fadeIn 0.5s;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .page-title {
            font-size: 28px;
            color: #1a3a5f;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
        }

        .page-title i {
            margin-right: 12px;
        }

        .card {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            padding: 25px;
            margin-bottom: 25px;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .card-title {
            font-size: 20px;
            color: #2c5282;
        }

        .btn {
            padding: 10px 18px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
        }

        .btn-primary {
            background-color: #2c5282;
            color: white;
        }

        .btn-primary:hover {
            background-color: #1a3a5f;
        }

        .btn-success {
            background-color: #38a169;
            color: white;
        }

        .btn-success:hover {
            background-color: #2f855a;
        }

        .btn-danger {
            background-color: #e53e3e;
            color: white;
        }

        .btn-danger:hover {
            background-color: #c53030;
        }

        .btn-sm {
            padding: 6px 12px;
            font-size: 14px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
        }

        table th, table td {
            padding: 14px 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }

        table th {
            background-color: #f8fafc;
            font-weight: 600;
            color: #4a5568;
        }

        table tr:hover {
            background-color: #f7fafc;
        }

        .warning {
            color: #dd6b20;
            font-weight: 600;
        }

        .danger {
            color: #e53e3e;
            font-weight: 600;
        }

        .success {
            color: #38a169;
            font-weight: 600;
        }

        .form-row {
            display: flex;
            flex-wrap: wrap;
            margin-bottom: 15px;
        }

        .form-group {
            flex: 1;
            min-width: 200px;
            margin-right: 15px;
            margin-bottom: 15px;
        }

        .form-group:last-child {
            margin-right: 0;
        }

        select {
            width: 100%;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 16px;
            background-color: white;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            border-radius: 10px;
            padding: 30px;
            width: 90%;
            max-width: 600px;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #999;
        }

        .close-modal:hover {
            color: #333;
        }

        .inventory-count {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
        }

        .inventory-low {
            background-color: #fed7d7;
            color: #c53030;
        }

        .inventory-normal {
            background-color: #c6f6d5;
            color: #276749;
        }

        .stats-cards {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
        }

        .stat-icon {
            width: 60px;
            height: 60px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 20px;
            font-size: 24px;
        }

        .stat-icon.blue {
            background-color: #ebf8ff;
            color: #3182ce;
        }

        .stat-icon.orange {
            background-color: #fffaf0;
            color: #dd6b20;
        }

        .stat-icon.green {
            background-color: #f0fff4;
            color: #38a169;
        }

        .stat-info h3 {
            font-size: 28px;
            margin-bottom: 5px;
        }

        .stat-info p {
            color: #718096;
            font-size: 14px;
        }

        .footer {
            text-align: center;
            padding: 20px;
            color: #718096;
            font-size: 14px;
            border-top: 1px solid #e2e8f0;
            margin-top: 30px;
        }

        .filter-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding: 15px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        .filter-group {
            display: flex;
            align-items: center;
        }

        .filter-group label {
            margin-right: 10px;
            font-weight: 600;
            color: #4a5568;
        }

        .filter-select {
            padding: 8px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            background-color: white;
            font-size: 14px;
            min-width: 200px;
        }

        .device-category-tabs {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 20px;
        }

        .category-tab {
            padding: 10px 20px;
            background-color: #edf2f7;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s;
            border: 2px solid transparent;
        }

        .category-tab:hover {
            background-color: #e2e8f0;
        }

        .category-tab.active {
            background-color: #2c5282;
            color: white;
            border-color: #2c5282;
        }

        .device-category-section {
            margin-bottom: 30px;
            padding: 20px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
        }

        .device-category-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #e2e8f0;
        }

        .device-category-title {
            font-size: 18px;
            color: #2c5282;
            font-weight: 600;
        }

        .spareparts-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 15px;
        }

        .sparepart-card {
            padding: 15px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
            transition: all 0.3s;
        }

        .sparepart-card:hover {
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            border-color: #2c5282;
        }

        .sparepart-card.warning {
            border-left: 4px solid #dd6b20;
        }

        .sparepart-card.danger {
            border-left: 4px solid #e53e3e;
        }

        .sparepart-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 10px;
        }

        .sparepart-name {
            font-weight: 600;
            color: #2d3748;
        }

        .sparepart-model {
            font-size: 14px;
            color: #718096;
        }

        .sparepart-info {
            display: flex;
            justify-content: space-between;
            margin-top: 10px;
            font-size: 14px;
        }

        .sparepart-quantity {
            font-weight: 600;
        }

        .sparepart-quantity.low {
            color: #c53030;
        }

        .sparepart-actions {
            display: flex;
            gap: 8px;
            margin-top: 15px;
        }

        .category-summary {
            display: flex;
            gap: 15px;
            margin-top: 10px;
        }

        .summary-item {
            display: flex;
            align-items: center;
            font-size: 14px;
        }

        .summary-label {
            margin-right: 5px;
            color: #718096;
        }

        .summary-value {
            font-weight: 600;
        }

        .summary-value.warning {
            color: #dd6b20;
        }

        .summary-value.danger {
            color: #e53e3e;
        }

        .summary-value.success {
            color: #38a169;
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #a0aec0;
        }

        .empty-state i {
            font-size: 48px;
            margin-bottom: 15px;
            color: #cbd5e0;
        }

        .empty-state p {
            font-size: 16px;
        }

        .toggle-details {
            background: none;
            border: none;
            color: #4a5568;
            cursor: pointer;
            font-size: 12px;
            margin-left: 10px;
        }

        .device-details {
            margin-top: 10px;
            padding: 10px;
            background-color: #f7fafc;
            border-radius: 6px;
            font-size: 14px;
            display: none;
        }

        .device-details.active {
            display: block;
        }

        .details-row {
            display: flex;
            margin-bottom: 5px;
        }

        .details-label {
            width: 100px;
            color: #718096;
        }

        .details-value {
            flex: 1;
        }

        @media (max-width: 992px) {
            .sidebar {
                width: 220px;
            }
            .content {
                margin-left: 220px;
            }
        }

        @media (max-width: 768px) {
            .sidebar {
                display: none;
            }
            .content {
                margin-left: 0;
            }
            .form-row {
                flex-direction: column;
            }
            .form-group {
                margin-right: 0;
            }
            .stats-cards {
                grid-template-columns: 1fr;
            }
            .filter-bar {
                flex-direction: column;
                align-items: flex-start;
                gap: 15px;
            }
            .spareparts-grid {
                grid-template-columns: 1fr;
            }
            .category-summary {
                flex-wrap: wrap;
            }
        }
    </style>
</head>
<body>
    <!-- 登录页面 -->
    <div class="login-page" id="loginPage">
        <div class="login-container">
            <h1><i class="fas fa-cogs"></i> 渣选厂备件管理系统</h1>
            <p>请输入您的账号和密码访问系统</p>
            <div class="login-form">
                <div class="form-group">
                    <label for="username">账号</label>
                    <input type="text" id="username" placeholder="请输入账号">
                </div>
                <div class="form-group">
                    <label for="password">密码</label>
                    <input type="password" id="password" placeholder="请输入密码">
                </div>
                <button class="login-btn" id="loginBtn">登录</button>
                <div class="error-message" id="errorMessage">账号或密码错误！请使用账号：Kobe，密码：242424</div>
            </div>
        </div>
    </div>

    <!-- 主系统 -->
    <div class="main-container" id="mainContainer">
        <!-- 顶部导航 -->
        <div class="header">
            <h1><i class="fas fa-industry"></i> 渣选厂备件管理系统</h1>
            <div class="user-info">
                <i class="fas fa-user"></i>
                <span>当前用户：Kobe</span>
                <button class="logout-btn" id="logoutBtn">退出登录</button>
            </div>
        </div>

        <!-- 侧边栏 -->
        <div class="sidebar">
            <ul>
                <li><a href="#" class="nav-link active" data-page="overview"><i class="fas fa-home"></i> 设备备件总览</a></li>
                <li><a href="#" class="nav-link" data-page="equipment"><i class="fas fa-tools"></i> 设备管理</a></li>
                <li><a href="#" class="nav-link" data-page="spareparts"><i class="fas fa-boxes"></i> 备件管理</a></li>
                <li><a href="#" class="nav-link" data-page="inventory"><i class="fas fa-warehouse"></i> 库存预警</a></li>
                <li><a href="#" class="nav-link" data-page="records"><i class="fas fa-clipboard-list"></i> 领用记录</a></li>
                <li><a href="#" class="nav-link" data-page="arrivals"><i class="fas fa-shipping-fast"></i> 到货记录</a></li>
                <li><a href="#" class="nav-link" data-page="maintenance"><i class="fas fa-calendar-alt"></i> 月度检修筹备</a></li>
            </ul>
        </div>

        <!-- 内容区域 -->
        <div class="content">
            <!-- 首页：设备备件总览 -->
            <div class="page active" id="overview">
                <h2 class="page-title"><i class="fas fa-home"></i> 渣选厂设备备件总览</h2>
                
                <div class="stats-cards">
                    <div class="stat-card">
                        <div class="stat-icon blue">
                            <i class="fas fa-tools"></i>
                        </div>
                        <div class="stat-info">
                            <h3 id="totalEquipment">0</h3>
                            <p>设备总数</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon orange">
                            <i class="fas fa-boxes"></i>
                        </div>
                        <div class="stat-info">
                            <h3 id="totalSpareparts">0</h3>
                            <p>备件种类</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon green">
                            <i class="fas fa-exclamation-triangle"></i>
                        </div>
                        <div class="stat-info">
                            <h3 id="warningCount">0</h3>
                            <p>库存预警</p>
                        </div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon blue">
                            <i class="fas fa-filter"></i>
                        </div>
                        <div class="stat-info">
                            <h3 id="categoryCount">0</h3>
                            <p>设备分类</p>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">设备分类概览</h3>
                        <button class="btn btn-primary" id="viewEquipmentDetails">设备详情</button>
                    </div>
                    <div id="equipmentOverview">
                        <!-- 设备概览将通过JavaScript动态生成 -->
                        <div class="empty-state">
                            <i class="fas fa-tools"></i>
                            <p>正在加载设备数据...</p>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">库存预警情况</h3>
                        <button class="btn btn-primary" id="viewAllWarning">查看全部预警</button>
                    </div>
                    <div id="warningOverview">
                        <!-- 预警信息将通过JavaScript动态生成 -->
                        <div class="empty-state">
                            <i class="fas fa-exclamation-triangle"></i>
                            <p>正在加载预警数据...</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 设备管理页面 -->
            <div class="page" id="equipment">
                <h2 class="page-title"><i class="fas fa-tools"></i> 设备管理</h2>
                
                <div class="filter-bar">
                    <div class="filter-group">
                        <label for="equipmentFilter">设备分类：</label>
                        <select id="equipmentFilter" class="filter-select">
                            <option value="all">全部设备</option>
                        </select>
                    </div>
                    <button class="btn btn-primary" id="addEquipmentBtn">添加新设备</button>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">设备列表</h3>
                        <div class="category-summary">
                            <div class="summary-item">
                                <span class="summary-label">设备总数：</span>
                                <span class="summary-value" id="equipmentTotal">0</span>
                            </div>
                            <div class="summary-item">
                                <span class="summary-label">分类数：</span>
                                <span class="summary-value" id="categoryTotal">0</span>
                            </div>
                        </div>
                    </div>
                    <div id="equipmentByCategory">
                        <!-- 设备按分类显示 -->
                        <div class="empty-state">
                            <i class="fas fa-tools"></i>
                            <p>暂无设备数据，请添加设备。</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 备件管理页面 -->
            <div class="page" id="spareparts">
                <h2 class="page-title"><i class="fas fa-boxes"></i> 备件管理</h2>
                
                <div class="filter-bar">
                    <div class="filter-group">
                        <label for="sparepartFilter">按设备筛选：</label>
                        <select id="sparepartFilter" class="filter-select">
                            <option value="all">全部备件</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="categoryFilter">按分类筛选：</label>
                        <select id="categoryFilter" class="filter-select">
                            <option value="all">全部分类</option>
                        </select>
                    </div>
                    <button class="btn btn-primary" id="addSparepartBtn">添加新备件</button>
                </div>
                
                <div id="sparepartsByDevice">
                    <!-- 备件按设备分类显示 -->
                    <div class="empty-state">
                        <i class="fas fa-boxes"></i>
                        <p>暂无备件数据，请添加备件。</p>
                    </div>
                </div>
            </div>

            <!-- 库存预警页面 -->
            <div class="page" id="inventory">
                <h2 class="page-title"><i class="fas fa-warehouse"></i> 库存预警</h2>
                
                <div class="filter-bar">
                    <div class="filter-group">
                        <label for="warningFilter">按设备筛选：</label>
                        <select id="warningFilter" class="filter-select">
                            <option value="all">全部设备</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="warningStatusFilter">按状态筛选：</label>
                        <select id="warningStatusFilter" class="filter-select">
                            <option value="all">全部状态</option>
                            <option value="warning">预警</option>
                            <option value="danger">紧急</option>
                        </select>
                    </div>
                    <button class="btn btn-primary" id="exportWarningBtn">导出预警列表</button>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">预警备件列表</h3>
                        <div class="category-summary">
                            <div class="summary-item">
                                <span class="summary-label">预警总数：</span>
                                <span class="summary-value warning" id="warningTotal">0</span>
                            </div>
                            <div class="summary-item">
                                <span class="summary-label">紧急预警：</span>
                                <span class="summary-value danger" id="dangerTotal">0</span>
                            </div>
                        </div>
                    </div>
                    <div id="warningByDevice">
                        <!-- 预警按设备分类显示 -->
                        <div class="empty-state">
                            <i class="fas fa-check-circle"></i>
                            <p>暂无库存预警，所有备件库存充足。</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 领用记录页面 -->
            <div class="page" id="records">
                <h2 class="page-title"><i class="fas fa-clipboard-list"></i> 领用记录</h2>
                
                <div class="filter-bar">
                    <div class="filter-group">
                        <label for="recordFilter">按设备筛选：</label>
                        <select id="recordFilter" class="filter-select">
                            <option value="all">全部设备</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="recordDateFilter">按日期筛选：</label>
                        <input type="month" id="recordDateFilter" class="filter-select">
                    </div>
                    <button class="btn btn-primary" id="addRecordBtn">添加领用记录</button>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">备件领用记录</h3>
                        <div class="category-summary">
                            <div class="summary-item">
                                <span class="summary-label">本月领用：</span>
                                <span class="summary-value" id="monthlyRecordTotal">0</span>
                            </div>
                        </div>
                    </div>
                    <div class="table-responsive">
                        <table id="recordsTable">
                            <thead>
                                <tr>
                                    <th>领用日期</th>
                                    <th>备件名称</th>
                                    <th>备件型号</th>
                                    <th>所属设备</th>
                                    <th>领用数量</th>
                                    <th>领用人</th>
                                    <th>领用用途</th>
                                    <th>领用后库存</th>
                                </tr>
                            </thead>
                            <tbody id="recordsTableBody">
                                <!-- 领用记录数据将通过JavaScript动态生成 -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- 到货记录页面 -->
            <div class="page" id="arrivals">
                <h2 class="page-title"><i class="fas fa-shipping-fast"></i> 到货记录</h2>
                
                <div class="filter-bar">
                    <div class="filter-group">
                        <label for="arrivalFilter">按设备筛选：</label>
                        <select id="arrivalFilter" class="filter-select">
                            <option value="all">全部设备</option>
                        </select>
                    </div>
                    <div class="filter-group">
                        <label for="arrivalDateFilter">按日期筛选：</label>
                        <input type="month" id="arrivalDateFilter" class="filter-select">
                    </div>
                    <button class="btn btn-primary" id="addArrivalBtn">添加到货记录</button>
                </div>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">备件到货记录</h3>
                        <div class="category-summary">
                            <div class="summary-item">
                                <span class="summary-label">本月到货：</span>
                                <span class="summary-value" id="monthlyArrivalTotal">0</span>
                            </div>
                        </div>
                    </div>
                    <div class="table-responsive">
                        <table id="arrivalsTable">
                            <thead>
                                <tr>
                                    <th>到货日期</th>
                                    <th>备件名称</th>
                                    <th>备件型号</th>
                                    <th>所属设备</th>
                                    <th>到货数量</th>
                                    <th>供应商</th>
                                    <th>到货后库存</th>
                                </tr>
                            </thead>
                            <tbody id="arrivalsTableBody">
                                <!-- 到货记录数据将通过JavaScript动态生成 -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- 月度检修筹备页面 -->
            <div class="page" id="maintenance">
                <h2 class="page-title"><i class="fas fa-calendar-alt"></i> 月度检修备件筹备</h2>
                
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">月度检修计划</h3>
                        <button class="btn btn-primary" id="addMaintenanceBtn">创建检修计划</button>
                    </div>
                    <div id="maintenancePlans">
                        <!-- 月度检修计划将通过JavaScript动态生成 -->
                        <div class="empty-state">
                            <i class="fas fa-calendar-alt"></i>
                            <p>暂无检修计划，请创建新的检修计划。</p>
                        </div>
                    </div>
                </div>

                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">检修备件需求汇总（按设备分类）</h3>
                    </div>
                    <div id="maintenanceSummary">
                        <!-- 检修备件汇总将通过JavaScript动态生成 -->
                        <div class="empty-state">
                            <i class="fas fa-clipboard-list"></i>
                            <p>暂无检修备件需求。</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="footer">
                <p>渣选厂备件管理系统 &copy; 2023 | 数据已保存到本地浏览器</p>
            </div>
        </div>
    </div>

    <!-- 添加设备模态框 -->
    <div class="modal" id="addEquipmentModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>添加新设备</h3>
                <button class="close-modal" id="closeEquipmentModal">&times;</button>
            </div>
            <form id="equipmentForm">
                <div class="form-row">
                    <div class="form-group">
                        <label for="equipmentName">设备名称 *</label>
                        <input type="text" id="equipmentName" required>
                    </div>
                    <div class="form-group">
                        <label for="equipmentModel">设备型号 *</label>
                        <input type="text" id="equipmentModel" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="equipmentCategory">设备分类 *</label>
                        <select id="equipmentCategory" required>
                            <option value="">请选择分类</option>
                            <option value="破碎设备">破碎设备</option>
                            <option value="磨矿设备">磨矿设备</option>
                            <option value="分级设备">分级设备</option>
                            <option value="浮选设备">浮选设备</option>
                            <option value="脱水设备">脱水设备</option>
                            <option value="输送设备">输送设备</option>
                            <option value="电气设备">电气设备</option>
                            <option value="其他设备">其他设备</option>
                        </select>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="equipmentLocation">安装位置</label>
                        <input type="text" id="equipmentLocation" placeholder="例如：破碎车间、磨矿车间等">
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="equipmentDescription">设备描述</label>
                        <textarea id="equipmentDescription" rows="3" placeholder="可填写设备用途、特点等信息"></textarea>
                    </div>
                </div>
                <div class="form-row">
                    <button type="submit" class="btn btn-primary">保存设备</button>
                    <button type="button" class="btn" id="cancelEquipmentBtn" style="margin-left: 10px;">取消</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 添加备件模态框 -->
    <div class="modal" id="addSparepartModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>添加新备件</h3>
                <button class="close-modal" id="closeSparepartModal">&times;</button>
            </div>
            <form id="sparepartForm">
                <div class="form-row">
                    <div class="form-group">
                        <label for="sparepartName">备件名称 *</label>
                        <input type="text" id="sparepartName" required>
                    </div>
                    <div class="form-group">
                        <label for="sparepartModel">备件型号 *</label>
                        <input type="text" id="sparepartModel" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="sparepartEquipment">所属设备 *</label>
                        <select id="sparepartEquipment" required>
                            <option value="">请选择设备</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="sparepartQuantity">库存数量 *</label>
                        <input type="number" id="sparepartQuantity" min="0" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="sparepartWarning">预警阈值 *</label>
                        <input type="number" id="sparepartWarning" min="1" required>
                        <small style="color: #666;">当库存低于此值时触发预警</small>
                    </div>
                    <div class="form-group">
                        <label for="sparepartUnit">计量单位</label>
                        <input type="text" id="sparepartUnit" value="个" placeholder="例如：个、件、套等">
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="sparepartSpec">规格参数</label>
                        <input type="text" id="sparepartSpec" placeholder="例如：材质、尺寸等">
                    </div>
                </div>
                <div class="form-row">
                    <button type="submit" class="btn btn-primary">保存备件</button>
                    <button type="button" class="btn" id="cancelSparepartBtn" style="margin-left: 10px;">取消</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 添加领用记录模态框 -->
    <div class="modal" id="addRecordModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>添加领用记录</h3>
                <button class="close-modal" id="closeRecordModal">&times;</button>
            </div>
            <form id="recordForm">
                <div class="form-row">
                    <div class="form-group">
                        <label for="recordSparepart">备件 *</label>
                        <select id="recordSparepart" required>
                            <option value="">请选择备件</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="recordQuantity">领用数量 *</label>
                        <input type="number" id="recordQuantity" min="1" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="recordPerson">领用人 *</label>
                        <input type="text" id="recordPerson" required>
                    </div>
                    <div class="form-group">
                        <label for="recordDate">领用日期 *</label>
                        <input type="date" id="recordDate" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group" style="flex: 2;">
                        <label for="recordPurpose">领用用途</label>
                        <input type="text" id="recordPurpose" placeholder="例如：设备维修、月度检修等">
                    </div>
                </div>
                <div class="form-row">
                    <button type="submit" class="btn btn-primary">保存记录</button>
                    <button type="button" class="btn" id="cancelRecordBtn" style="margin-left: 10px;">取消</button>
                </div>
            </form>
        </div>
    </div>

    <!-- 添加到货记录模态框 -->
    <div class="modal" id="addArrivalModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>添加到货记录</h3>
                <button class="close-modal" id="closeArrivalModal">&times;</button>
            </div>
            <form id="arrivalForm">
                <div class="form-row">
                    <div class="form-group">
                        <label for="arrivalSparepart">备件 *</label>
                        <select id="arrivalSparepart" required>
                            <option value="">请选择备件</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="arrivalQuantity">到货数量 *</label>
                        <input type="number" id="arrivalQuantity" min="1" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label for="arrivalSupplier">供应商 *</label>
                        <input type="text" id="arrivalSupplier" required>
                    </div>
                    <div class="form-group">
                        <label for="arrivalDate">到货日期 *</label>
                        <input type="date" id="arrivalDate" required>
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group" style="flex: 2;">
                        <label for="arrivalNote">备注</label>
                        <input type="text" id="arrivalNote" placeholder="可填写订单号、质量情况等">
                    </div>
                </div>
                <div class="form-row">
                    <button type="submit" class="btn btn-primary">保存记录</button>
                    <button type="button" class="btn" id="cancelArrivalBtn" style="margin-left: 10px;">取消</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // 数据存储
        let equipmentData = [];
        let sparepartsData = [];
        let recordsData = [];
        let arrivalsData = [];
        let maintenanceData = [];

        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', function() {
            // 加载保存的数据
            loadData();
            
            // 登录功能
            const loginBtn = document.getElementById('loginBtn');
            const logoutBtn = document.getElementById('logoutBtn');
            const errorMessage = document.getElementById('errorMessage');
            const loginPage = document.getElementById('loginPage');
            const mainContainer = document.getElementById('mainContainer');
            
            loginBtn.addEventListener('click', function() {
                const username = document.getElementById('username').value;
                const password = document.getElementById('password').value;
                
                if (username === 'Kobe' && password === '242424') {
                    loginPage.style.display = 'none';
                    mainContainer.style.display = 'block';
                    updateDashboard();
                    updateAllFilters();
                } else {
                    errorMessage.style.display = 'block';
                }
            });
            
            // 允许按Enter键登录
            document.getElementById('password').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    loginBtn.click();
                }
            });
            
            logoutBtn.addEventListener('click', function() {
                loginPage.style.display = 'flex';
                mainContainer.style.display = 'none';
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
                errorMessage.style.display = 'none';
            });
            
            // 导航功能
            const navLinks = document.querySelectorAll('.nav-link');
            const pages = document.querySelectorAll('.page');
            
            navLinks.forEach(link => {
                link.addEventListener('click', function(e) {
                    e.preventDefault();
                    
                    // 移除所有活动状态
                    navLinks.forEach(item => item.classList.remove('active'));
                    pages.forEach(page => page.classList.remove('active'));
                    
                    // 设置当前活动状态
                    this.classList.add('active');
                    const pageId = this.getAttribute('data-page');
                    document.getElementById(pageId).classList.add('active');
                    
                    // 更新页面数据
                    if (pageId === 'overview') {
                        updateDashboard();
                    } else if (pageId === 'equipment') {
                        updateEquipmentByCategory();
                    } else if (pageId === 'spareparts') {
                        updateSparepartsByDevice();
                    } else if (pageId === 'inventory') {
                        updateWarningByDevice();
                    } else if (pageId === 'records') {
                        updateRecordsTable();
                    } else if (pageId === 'arrivals') {
                        updateArrivalsTable();
                    } else if (pageId === 'maintenance') {
                        updateMaintenancePage();
                    }
                });
            });
            
            // 查看设备详情按钮
            document.getElementById('viewEquipmentDetails').addEventListener('click', function() {
                navLinks.forEach(item => item.classList.remove('active'));
                pages.forEach(page => page.classList.remove('active'));
                
                document.querySelector('[data-page="equipment"]').classList.add('active');
                document.getElementById('equipment').classList.add('active');
                
                updateEquipmentByCategory();
            });
            
            // 查看全部预警按钮
            document.getElementById('viewAllWarning').addEventListener('click', function() {
                navLinks.forEach(item => item.classList.remove('active'));
                pages.forEach(page => page.classList.remove('active'));
                
                document.querySelector('[data-page="inventory"]').classList.add('active');
                document.getElementById('inventory').classList.add('active');
                
                updateWarningByDevice();
            });
            
            // 初始化筛选器
            updateAllFilters();
            
            // 设备筛选功能
            document.getElementById('equipmentFilter').addEventListener('change', function() {
                updateEquipmentByCategory();
            });
            
            // 备件筛选功能
            document.getElementById('sparepartFilter').addEventListener('change', function() {
                updateSparepartsByDevice();
            });
            
            document.getElementById('categoryFilter').addEventListener('change', function() {
                updateSparepartsByDevice();
            });
            
            // 预警筛选功能
            document.getElementById('warningFilter').addEventListener('change', function() {
                updateWarningByDevice();
            });
            
            document.getElementById('warningStatusFilter').addEventListener('change', function() {
                updateWarningByDevice();
            });
            
            // 领用记录筛选功能
            document.getElementById('recordFilter').addEventListener('change', function() {
                updateRecordsTable();
            });
            
            document.getElementById('recordDateFilter').addEventListener('change', function() {
                updateRecordsTable();
            });
            
            // 到货记录筛选功能
            document.getElementById('arrivalFilter').addEventListener('change', function() {
                updateArrivalsTable();
            });
            
            document.getElementById('arrivalDateFilter').addEventListener('change', function() {
                updateArrivalsTable();
            });
            
            // 添加设备功能
            const addEquipmentBtn = document.getElementById('addEquipmentBtn');
            const addEquipmentModal = document.getElementById('addEquipmentModal');
            const closeEquipmentModal = document.getElementById('closeEquipmentModal');
            const cancelEquipmentBtn = document.getElementById('cancelEquipmentBtn');
            const equipmentForm = document.getElementById('equipmentForm');
            
            addEquipmentBtn.addEventListener('click', function() {
                addEquipmentModal.style.display = 'flex';
            });
            
            closeEquipmentModal.addEventListener('click', function() {
                addEquipmentModal.style.display = 'none';
            });
            
            cancelEquipmentBtn.addEventListener('click', function() {
                addEquipmentModal.style.display = 'none';
            });
            
            equipmentForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const equipmentName = document.getElementById('equipmentName').value;
                const equipmentModel = document.getElementById('equipmentModel').value;
                const equipmentCategory = document.getElementById('equipmentCategory').value;
                const equipmentLocation = document.getElementById('equipmentLocation').value || '';
                const equipmentDescription = document.getElementById('equipmentDescription').value || '';
                
                // 检查设备是否已存在
                const existingEquipment = equipmentData.find(e => e.name === equipmentName && e.model === equipmentModel);
                if (existingEquipment) {
                    alert('该设备已存在！');
                    return;
                }
                
                // 添加新设备
                const newEquipment = {
                    id: Date.now(),
                    name: equipmentName,
                    model: equipmentModel,
                    category: equipmentCategory,
                    location: equipmentLocation,
                    description: equipmentDescription,
                    spareparts: [],
                    createdAt: new Date().toISOString().split('T')[0]
                };
                
                equipmentData.push(newEquipment);
                saveData();
                updateEquipmentByCategory();
                updateAllFilters();
                addEquipmentModal.style.display = 'none';
                equipmentForm.reset();
                
                // 如果当前在总览页面，更新总览
                if (document.getElementById('overview').classList.contains('active')) {
                    updateDashboard();
                }
            });
            
            // 添加备件功能
            const addSparepartBtn = document.getElementById('addSparepartBtn');
            const addSparepartModal = document.getElementById('addSparepartModal');
            const closeSparepartModal = document.getElementById('closeSparepartModal');
            const cancelSparepartBtn = document.getElementById('cancelSparepartBtn');
            const sparepartForm = document.getElementById('sparepartForm');
            
            addSparepartBtn.addEventListener('click', function() {
                // 确保有设备可供选择
                if (equipmentData.length === 0) {
                    alert('请先添加设备，然后再添加备件！');
                    return;
                }
                
                addSparepartModal.style.display = 'flex';
            });
            
            closeSparepartModal.addEventListener('click', function() {
                addSparepartModal.style.display = 'none';
            });
            
            cancelSparepartBtn.addEventListener('click', function() {
                addSparepartModal.style.display = 'none';
            });
            
            sparepartForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const sparepartName = document.getElementById('sparepartName').value;
                const sparepartModel = document.getElementById('sparepartModel').value;
                const sparepartEquipmentId = parseInt(document.getElementById('sparepartEquipment').value);
                const sparepartQuantity = parseInt(document.getElementById('sparepartQuantity').value);
                const sparepartWarning = parseInt(document.getElementById('sparepartWarning').value);
                const sparepartUnit = document.getElementById('sparepartUnit').value || '个';
                const sparepartSpec = document.getElementById('sparepartSpec').value || '';
                
                // 检查备件是否已存在
                const existingSparepart = sparepartsData.find(s => s.name === sparepartName && s.model === sparepartModel && s.equipmentId === sparepartEquipmentId);
                if (existingSparepart) {
                    alert('该备件已存在！');
                    return;
                }
                
                // 查找设备
                const equipment = equipmentData.find(e => e.id === sparepartEquipmentId);
                if (!equipment) {
                    alert('所选设备不存在！');
                    return;
                }
                
                // 计算状态（预警、紧急或正常）
                let status = 'normal';
                if (sparepartQuantity <= 0) {
                    status = 'danger';
                } else if (sparepartQuantity <= sparepartWarning) {
                    status = 'warning';
                }
                
                // 添加新备件
                const newSparepart = {
                    id: Date.now(),
                    name: sparepartName,
                    model: sparepartModel,
                    equipmentId: sparepartEquipmentId,
                    equipmentName: equipment.name,
                    equipmentModel: equipment.model,
                    equipmentCategory: equipment.category,
                    quantity: sparepartQuantity,
                    warningThreshold: sparepartWarning,
                    unit: sparepartUnit,
                    specification: sparepartSpec,
                    status: status,
                    createdAt: new Date().toISOString().split('T')[0]
                };
                
                sparepartsData.push(newSparepart);
                
                // 更新设备的备件列表
                equipment.spareparts.push(newSparepart.id);
                
                saveData();
                updateSparepartsByDevice();
                updateAllFilters();
                addSparepartModal.style.display = 'none';
                sparepartForm.reset();
                
                // 如果当前在总览页面，更新总览
                if (document.getElementById('overview').classList.contains('active')) {
                    updateDashboard();
                }
            });
            
            // 添加领用记录功能
            const addRecordBtn = document.getElementById('addRecordBtn');
            const addRecordModal = document.getElementById('addRecordModal');
            const closeRecordModal = document.getElementById('closeRecordModal');
            const cancelRecordBtn = document.getElementById('cancelRecordBtn');
            const recordForm = document.getElementById('recordForm');
            
            addRecordBtn.addEventListener('click', function() {
                // 确保有备件可供选择
                if (sparepartsData.length === 0) {
                    alert('请先添加备件，然后再添加领用记录！');
                    return;
                }
                
                // 设置默认日期为今天
                document.getElementById('recordDate').valueAsDate = new Date();
                addRecordModal.style.display = 'flex';
            });
            
            closeRecordModal.addEventListener('click', function() {
                addRecordModal.style.display = 'none';
            });
            
            cancelRecordBtn.addEventListener('click', function() {
                addRecordModal.style.display = 'none';
            });
            
            recordForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const recordSparepartId = parseInt(document.getElementById('recordSparepart').value);
                const recordQuantity = parseInt(document.getElementById('recordQuantity').value);
                const recordPerson = document.getElementById('recordPerson').value;
                const recordDate = document.getElementById('recordDate').value;
                const recordPurpose = document.getElementById('recordPurpose').value || '未说明';
                
                // 查找备件
                const sparepart = sparepartsData.find(s => s.id === recordSparepartId);
                if (!sparepart) {
                    alert('所选备件不存在！');
                    return;
                }
                
                // 检查库存是否足够
                if (sparepart.quantity < recordQuantity) {
                    alert('库存不足！当前库存：' + sparepart.quantity + sparepart.unit);
                    return;
                }
                
                // 更新库存
                sparepart.quantity -= recordQuantity;
                
                // 更新状态
                if (sparepart.quantity <= 0) {
                    sparepart.status = 'danger';
                } else if (sparepart.quantity <= sparepart.warningThreshold) {
                    sparepart.status = 'warning';
                } else {
                    sparepart.status = 'normal';
                }
                
                // 添加领用记录
                const newRecord = {
                    id: Date.now(),
                    sparepartId: recordSparepartId,
                    sparepartName: sparepart.name,
                    sparepartModel: sparepart.model,
                    equipmentId: sparepart.equipmentId,
                    equipmentName: sparepart.equipmentName,
                    equipmentModel: sparepart.equipmentModel,
                    quantity: recordQuantity,
                    person: recordPerson,
                    date: recordDate,
                    purpose: recordPurpose,
                    remainingQuantity: sparepart.quantity,
                    unit: sparepart.unit
                };
                
                recordsData.push(newRecord);
                saveData();
                updateRecordsTable();
                updateSparepartsByDevice();
                
                // 如果当前在库存预警页面，更新预警表
                if (document.getElementById('inventory').classList.contains('active')) {
                    updateWarningByDevice();
                }
                
                addRecordModal.style.display = 'none';
                recordForm.reset();
                
                // 如果当前在总览页面，更新总览
                if (document.getElementById('overview').classList.contains('active')) {
                    updateDashboard();
                }
            });
            
            // 添加到货记录功能
            const addArrivalBtn = document.getElementById('addArrivalBtn');
            const addArrivalModal = document.getElementById('addArrivalModal');
            const closeArrivalModal = document.getElementById('closeArrivalModal');
            const cancelArrivalBtn = document.getElementById('cancelArrivalBtn');
            const arrivalForm = document.getElementById('arrivalForm');
            
            addArrivalBtn.addEventListener('click', function() {
                // 确保有备件可供选择
                if (sparepartsData.length === 0) {
                    alert('请先添加备件，然后再添加到货记录！');
                    return;
                }
                
                // 设置默认日期为今天
                document.getElementById('arrivalDate').valueAsDate = new Date();
                addArrivalModal.style.display = 'flex';
            });
            
            closeArrivalModal.addEventListener('click', function() {
                addArrivalModal.style.display = 'none';
            });
            
            cancelArrivalBtn.addEventListener('click', function() {
                addArrivalModal.style.display = 'none';
            });
            
            arrivalForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const arrivalSparepartId = parseInt(document.getElementById('arrivalSparepart').value);
                const arrivalQuantity = parseInt(document.getElementById('arrivalQuantity').value);
                const arrivalSupplier = document.getElementById('arrivalSupplier').value;
                const arrivalDate = document.getElementById('arrivalDate').value;
                const arrivalNote = document.getElementById('arrivalNote').value || '';
                
                // 查找备件
                const sparepart = sparepartsData.find(s => s.id === arrivalSparepartId);
                if (!sparepart) {
                    alert('所选备件不存在！');
                    return;
                }
                
                // 更新库存
                sparepart.quantity += arrivalQuantity;
                
                // 更新状态
                if (sparepart.quantity <= 0) {
                    sparepart.status = 'danger';
                } else if (sparepart.quantity <= sparepart.warningThreshold) {
                    sparepart.status = 'warning';
                } else {
                    sparepart.status = 'normal';
                }
                
                // 添加到货记录
                const newArrival = {
                    id: Date.now(),
                    sparepartId: arrivalSparepartId,
                    sparepartName: sparepart.name,
                    sparepartModel: sparepart.model,
                    equipmentId: sparepart.equipmentId,
                    equipmentName: sparepart.equipmentName,
                    equipmentModel: sparepart.equipmentModel,
                    quantity: arrivalQuantity,
                    supplier: arrivalSupplier,
                    date: arrivalDate,
                    note: arrivalNote,
                    remainingQuantity: sparepart.quantity,
                    unit: sparepart.unit
                };
                
                arrivalsData.push(newArrival);
                saveData();
                updateArrivalsTable();
                updateSparepartsByDevice();
                
                // 如果当前在库存预警页面，更新预警表
                if (document.getElementById('inventory').classList.contains('active')) {
                    updateWarningByDevice();
                }
                
                addArrivalModal.style.display = 'none';
                arrivalForm.reset();
                
                // 如果当前在总览页面，更新总览
                if (document.getElementById('overview').classList.contains('active')) {
                    updateDashboard();
                }
            });
            
            // 初始化备件选择下拉框
            updateSparepartsSelects();
            
            // 初始化示例数据
            if (equipmentData.length === 0) {
                initializeSampleData();
                updateAllFilters();
            }
        });
        
        // 加载数据
        function loadData() {
            const savedEquipmentData = localStorage.getItem('equipmentData');
            const savedSparepartsData = localStorage.getItem('sparepartsData');
            const savedRecordsData = localStorage.getItem('recordsData');
            const savedArrivalsData = localStorage.getItem('arrivalsData');
            const savedMaintenanceData = localStorage.getItem('maintenanceData');
            
            if (savedEquipmentData) equipmentData = JSON.parse(savedEquipmentData);
            if (savedSparepartsData) sparepartsData = JSON.parse(savedSparepartsData);
            if (savedRecordsData) recordsData = JSON.parse(savedRecordsData);
            if (savedArrivalsData) arrivalsData = JSON.parse(savedArrivalsData);
            if (savedMaintenanceData) maintenanceData = JSON.parse(savedMaintenanceData);
        }
        
        // 保存数据
        function saveData() {
            localStorage.setItem('equipmentData', JSON.stringify(equipmentData));
            localStorage.setItem('sparepartsData', JSON.stringify(sparepartsData));
            localStorage.setItem('recordsData', JSON.stringify(recordsData));
            localStorage.setItem('arrivalsData', JSON.stringify(arrivalsData));
            localStorage.setItem('maintenanceData', JSON.stringify(maintenanceData));
        }
        
        // 初始化示例数据
        function initializeSampleData() {
            // 添加示例设备
            const equipment1 = {
                id: 1,
                name: '颚式破碎机',
                model: 'PE600×900',
                category: '破碎设备',
                location: '破碎车间',
                description: '主要用于矿石的粗碎作业',
                spareparts: [101, 102, 103],
                createdAt: '2023-01-15'
            };
            
            const equipment2 = {
                id: 2,
                name: '圆锥破碎机',
                model: 'PYB1750',
                category: '破碎设备',
                location: '破碎车间',
                description: '用于矿石的中碎作业',
                spareparts: [104],
                createdAt: '2023-02-20'
            };
            
            const equipment3 = {
                id: 3,
                name: '球磨机',
                model: 'MQG2700×3600',
                category: '磨矿设备',
                location: '磨矿车间',
                description: '用于矿石的细磨作业',
                spareparts: [105, 106],
                createdAt: '2023-03-10'
            };
            
            const equipment4 = {
                id: 4,
                name: '螺旋分级机',
                model: 'FG-20',
                category: '分级设备',
                location: '磨矿车间',
                description: '用于矿浆的分级作业',
                spareparts: [107],
                createdAt: '2023-04-05'
            };
            
            const equipment5 = {
                id: 5,
                name: '渣浆泵',
                model: 'ZJ-200',
                category: '输送设备',
                location: '输送区',
                description: '用于矿浆输送',
                spareparts: [108, 109],
                createdAt: '2023-05-12'
            };
            
            equipmentData.push(equipment1, equipment2, equipment3, equipment4, equipment5);
            
            // 添加示例备件
            const sparepart1 = {
                id: 101,
                name: '颚板',
                model: 'PE600×900-01',
                equipmentId: 1,
                equipmentName: '颚式破碎机',
                equipmentModel: 'PE600×900',
                equipmentCategory: '破碎设备',
                quantity: 5,
                warningThreshold: 3,
                unit: '件',
                specification: '高锰钢，尺寸600×900mm',
                status: 'normal',
                createdAt: '2023-01-20'
            };
            
            const sparepart2 = {
                id: 102,
                name: '主轴',
                model: 'PE600×900-02',
                equipmentId: 1,
                equipmentName: '颚式破碎机',
                equipmentModel: 'PE600×900',
                equipmentCategory: '破碎设备',
                quantity: 2,
                warningThreshold: 2,
                unit: '根',
                specification: '合金钢，直径220mm',
                status: 'warning',
                createdAt: '2023-01-20'
            };
            
            const sparepart3 = {
                id: 103,
                name: '轴承',
                model: 'PE600×900-03',
                equipmentId: 1,
                equipmentName: '颚式破碎机',
                equipmentModel: 'PE600×900',
                equipmentCategory: '破碎设备',
                quantity: 8,
                warningThreshold: 4,
                unit: '套',
                specification: '调心滚子轴承',
                status: 'normal',
                createdAt: '2023-02-05'
            };
            
            const sparepart4 = {
                id: 104,
                name: '破碎壁',
                model: 'PYB1750-01',
                equipmentId: 2,
                equipmentName: '圆锥破碎机',
                equipmentModel: 'PYB1750',
                equipmentCategory: '破碎设备',
                quantity: 3,
                warningThreshold: 2,
                unit: '件',
                specification: '高锰钢',
                status: 'normal',
                createdAt: '2023-02-25'
            };
            
            const sparepart5 = {
                id: 105,
                name: '钢球',
                model: 'MQG-100',
                equipmentId: 3,
                equipmentName: '球磨机',
                equipmentModel: 'MQG2700×3600',
                equipmentCategory: '磨矿设备',
                quantity: 150,
                warningThreshold: 50,
                unit: '吨',
                specification: 'Φ100mm，高铬合金',
                status: 'normal',
                createdAt: '2023-03-15'
            };
            
            const sparepart6 = {
                id: 106,
                name: '衬板',
                model: 'MQG-201',
                equipmentId: 3,
                equipmentName: '球磨机',
                equipmentModel: 'MQG2700×3600',
                equipmentCategory: '磨矿设备',
                quantity: 12,
                warningThreshold: 10,
                unit: '套',
                specification: '高铬铸铁',
                status: 'normal',
                createdAt: '2023-03-15'
            };
            
            const sparepart7 = {
                id: 107,
                name: '螺旋叶片',
                model: 'FG-20-01',
                equipmentId: 4,
                equipmentName: '螺旋分级机',
                equipmentModel: 'FG-20',
                equipmentCategory: '分级设备',
                quantity: 3,
                warningThreshold: 2,
                unit: '件',
                specification: '耐磨合金',
                status: 'normal',
                createdAt: '2023-04-10'
            };
            
            const sparepart8 = {
                id: 108,
                name: '叶轮',
                model: 'ZJ-200-01',
                equipmentId: 5,
                equipmentName: '渣浆泵',
                equipmentModel: 'ZJ-200',
                equipmentCategory: '输送设备',
                quantity: 2,
                warningThreshold: 2,
                unit: '件',
                specification: '高铬合金，直径200mm',
                status: 'warning',
                createdAt: '2023-05-15'
            };
            
            const sparepart9 = {
                id: 109,
                name: '机械密封',
                model: 'ZJ-200-02',
                equipmentId: 5,
                equipmentName: '渣浆泵',
                equipmentModel: 'ZJ-200',
                equipmentCategory: '输送设备',
                quantity: 0,
                warningThreshold: 3,
                unit: '套',
                specification: '碳化硅',
                status: 'danger',
                createdAt: '2023-05-15'
            };
            
            sparepartsData.push(sparepart1, sparepart2, sparepart3, sparepart4, sparepart5, sparepart6, sparepart7, sparepart8, sparepart9);
            
            // 添加示例领用记录
            const record1 = {
                id: 1001,
                sparepartId: 101,
                sparepartName: '颚板',
                sparepartModel: 'PE600×900-01',
                equipmentId: 1,
                equipmentName: '颚式破碎机',
                equipmentModel: 'PE600×900',
                quantity: 2,
                person: '张三',
                date: '2023-10-15',
                purpose: '日常维修',
                remainingQuantity: 5,
                unit: '件'
            };
            
            const record2 = {
                id: 1002,
                sparepartId: 105,
                sparepartName: '钢球',
                sparepartModel: 'MQG-100',
                equipmentId: 3,
                equipmentName: '球磨机',
                equipmentModel: 'MQG2700×3600',
                quantity: 30,
                person: '李四',
                date: '2023-10-20',
                purpose: '月度检修',
                remainingQuantity: 150,
                unit: '吨'
            };
            
            const record3 = {
                id: 1003,
                sparepartId: 108,
                sparepartName: '叶轮',
                sparepartModel: 'ZJ-200-01',
                equipmentId: 5,
                equipmentName: '渣浆泵',
                equipmentModel: 'ZJ-200',
                quantity: 1,
                person: '王五',
                date: '2023-10-25',
                purpose: '故障更换',
                remainingQuantity: 2,
                unit: '件'
            };
            
            recordsData.push(record1, record2, record3);
            
            // 添加示例到货记录
            const arrival1 = {
                id: 2001,
                sparepartId: 101,
                sparepartName: '颚板',
                sparepartModel: 'PE600×900-01',
                equipmentId: 1,
                equipmentName: '颚式破碎机',
                equipmentModel: 'PE600×900',
                quantity: 4,
                supplier: '矿山机械有限公司',
                date: '2023-10-10',
                note: '订单号：2023101001',
                remainingQuantity: 9,
                unit: '件'
            };
            
            const arrival2 = {
                id: 2002,
                sparepartId: 105,
                sparepartName: '钢球',
                sparepartModel: 'MQG-100',
                equipmentId: 3,
                equipmentName: '球磨机',
                equipmentModel: 'MQG2700×3600',
                quantity: 50,
                supplier: '耐磨材料厂',
                date: '2023-10-18',
                note: '订单号：2023101802',
                remainingQuantity: 200,
                unit: '吨'
            };
            
            arrivalsData.push(arrival1, arrival2);
            
            // 添加示例月度检修计划
            const maintenance1 = {
                id: 3001,
                month: '2023-11',
                planName: '11月设备检修计划',
                equipmentIds: [1, 2],
                sparepartRequirements: [
                    { sparepartId: 101, quantity: 2 },
                    { sparepartId: 103, quantity: 4 },
                    { sparepartId: 104, quantity: 1 }
                ],
                status: 'pending'
            };
            
            maintenanceData.push(maintenance1);
            
            saveData();
        }
        
        // 更新所有筛选器
        function updateAllFilters() {
            updateEquipmentFilter();
            updateSparepartFilter();
            updateCategoryFilter();
            updateWarningFilter();
            updateRecordFilter();
            updateArrivalFilter();
            updateSparepartsSelects();
        }
        
        // 更新设备筛选器
        function updateEquipmentFilter() {
            const equipmentFilter = document.getElementById('equipmentFilter');
            let options = '<option value="all">全部设备</option>';
            
            // 按分类分组
            const categories = {};
            equipmentData.forEach(equipment => {
                if (!categories[equipment.category]) {
                    categories[equipment.category] = [];
                }
                categories[equipment.category].push(equipment);
            });
            
            // 添加分类选项
            for (const category in categories) {
                options += `<option value="category_${category}" disabled style="font-weight: bold; color: #2c5282;">--- ${category} ---</option>`;
                categories[category].forEach(equipment => {
                    options += `<option value="${equipment.id}">&nbsp;&nbsp;&nbsp;&nbsp;${equipment.name} (${equipment.model})</option>`;
                });
            }
            
            equipmentFilter.innerHTML = options;
        }
        
        // 更新备件筛选器
        function updateSparepartFilter() {
            const sparepartFilter = document.getElementById('sparepartFilter');
            let options = '<option value="all">全部备件</option>';
            
            equipmentData.forEach(equipment => {
                options += `<option value="${equipment.id}">${equipment.name} (${equipment.model})</option>`;
            });
            
            sparepartFilter.innerHTML = options;
        }
        
        // 更新分类筛选器
        function updateCategoryFilter() {
            const categoryFilter = document.getElementById('categoryFilter');
            let options = '<option value="all">全部分类</option>';
            
            // 获取所有分类
            const categories = [...new Set(equipmentData.map(e => e.category))];
            categories.forEach(category => {
                options += `<option value="${category}">${category}</option>`;
            });
            
            categoryFilter.innerHTML = options;
        }
        
        // 更新预警筛选器
        function updateWarningFilter() {
            const warningFilter = document.getElementById('warningFilter');
            let options = '<option value="all">全部设备</option>';
            
            equipmentData.forEach(equipment => {
                options += `<option value="${equipment.id}">${equipment.name} (${equipment.model})</option>`;
            });
            
            warningFilter.innerHTML = options;
        }
        
        // 更新领用记录筛选器
        function updateRecordFilter() {
            const recordFilter = document.getElementById('recordFilter');
            let options = '<option value="all">全部设备</option>';
            
            equipmentData.forEach(equipment => {
                options += `<option value="${equipment.id}">${equipment.name} (${equipment.model})</option>`;
            });
            
            recordFilter.innerHTML = options;
        }
        
        // 更新到货记录筛选器
        function updateArrivalFilter() {
            const arrivalFilter = document.getElementById('arrivalFilter');
            let options = '<option value="all">全部设备</option>';
            
            equipmentData.forEach(equipment => {
                options += `<option value="${equipment.id}">${equipment.name} (${equipment.model})</option>`;
            });
            
            arrivalFilter.innerHTML = options;
        }
        
        // 更新备件选择下拉框
        function updateSparepartsSelects() {
            const sparepartEquipmentSelect = document.getElementById('sparepartEquipment');
            const recordSparepartSelect = document.getElementById('recordSparepart');
            const arrivalSparepartSelect = document.getElementById('arrivalSparepart');
            
            // 更新设备选择下拉框
            let equipmentOptions = '<option value="">请选择设备</option>';
            equipmentData.forEach(equipment => {
                equipmentOptions += `<option value="${equipment.id}">${equipment.name} (${equipment.model}) - ${equipment.category}</option>`;
            });
            sparepartEquipmentSelect.innerHTML = equipmentOptions;
            
            // 更新领用记录备件选择下拉框
            let sparepartOptions = '<option value="">请选择备件</option>';
            sparepartsData.forEach(sparepart => {
                sparepartOptions += `<option value="${sparepart.id}">${sparepart.name} (${sparepart.model}) - ${sparepart.equipmentName}</option>`;
            });
            recordSparepartSelect.innerHTML = sparepartOptions;
            
            // 更新到货记录备件选择下拉框
            arrivalSparepartSelect.innerHTML = sparepartOptions;
        }
        
        // 更新设备按分类显示
        function updateEquipmentByCategory() {
            const equipmentByCategory = document.getElementById('equipmentByCategory');
            const equipmentFilter = document.getElementById('equipmentFilter').value;
            
            // 筛选设备
            let filteredEquipment = equipmentData;
            if (equipmentFilter !== 'all') {
                if (equipmentFilter.startsWith('category_')) {
                    const category = equipmentFilter.replace('category_', '');
                    filteredEquipment = equipmentData.filter(e => e.category === category);
                } else {
                    const equipmentId = parseInt(equipmentFilter);
                    filteredEquipment = equipmentData.filter(e => e.id === equipmentId);
                }
            }
            
            if (filteredEquipment.length === 0) {
                equipmentByCategory.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-tools"></i>
                        <p>暂无设备数据，请添加设备。</p>
                    </div>
                `;
                return;
            }
            
            // 按分类分组
            const categories = {};
            filteredEquipment.forEach(equipment => {
                if (!categories[equipment.category]) {
                    categories[equipment.category] = [];
                }
                categories[equipment.category].push(equipment);
            });
            
            let html = '';
            
            // 显示分类摘要
            document.getElementById('equipmentTotal').textContent = filteredEquipment.length;
            document.getElementById('categoryTotal').textContent = Object.keys(categories).length;
            
            // 显示每个分类的设备
            for (const category in categories) {
                const equipmentList = categories[category];
                
                // 计算分类统计
                let totalSpareparts = 0;
                let warningSpareparts = 0;
                let dangerSpareparts = 0;
                
                equipmentList.forEach(equipment => {
                    const equipmentSpareparts = sparepartsData.filter(s => s.equipmentId === equipment.id);
                    totalSpareparts += equipmentSpareparts.length;
                    warningSpareparts += equipmentSpareparts.filter(s => s.status === 'warning').length;
                    dangerSpareparts += equipmentSpareparts.filter(s => s.status === 'danger').length;
                });
                
                html += `
                    <div class="device-category-section">
                        <div class="device-category-header">
                            <div class="device-category-title">${category} (${equipmentList.length}台设备)</div>
                            <div class="category-summary">
                                <div class="summary-item">
                                    <span class="summary-label">备件总数：</span>
                                    <span class="summary-value">${totalSpareparts}</span>
                                </div>
                                <div class="summary-item">
                                    <span class="summary-label">预警备件：</span>
                                    <span class="summary-value ${warningSpareparts > 0 ? 'warning' : ''}">${warningSpareparts}</span>
                                </div>
                                <div class="summary-item">
                                    <span class="summary-label">紧急备件：</span>
                                    <span class="summary-value ${dangerSpareparts > 0 ? 'danger' : ''}">${dangerSpareparts}</span>
                                </div>
                            </div>
                        </div>
                        <div class="spareparts-grid">
                `;
                
                equipmentList.forEach(equipment => {
                    const equipmentSpareparts = sparepartsData.filter(s => s.equipmentId === equipment.id);
                    const warningCount = equipmentSpareparts.filter(s => s.status === 'warning').length;
                    const dangerCount = equipmentSpareparts.filter(s => s.status === 'danger').length;
                    
                    html += `
                        <div class="sparepart-card ${dangerCount > 0 ? 'danger' : (warningCount > 0 ? 'warning' : '')}">
                            <div class="sparepart-header">
                                <div>
                                    <div class="sparepart-name">${equipment.name}</div>
                                    <div class="sparepart-model">${equipment.model}</div>
                                    <div style="font-size: 12px; color: #718096; margin-top: 5px;">${equipment.location}</div>
                                </div>
                                <button class="toggle-details" data-equipment="${equipment.id}">
                                    <i class="fas fa-chevron-down"></i>
                                </button>
                            </div>
                            <div class="sparepart-info">
                                <div>
                                    <div>备件数量：${equipmentSpareparts.length}</div>
                                    <div>预警备件：<span class="${warningCount > 0 ? 'warning' : ''}">${warningCount}</span></div>
                                    <div>紧急备件：<span class="${dangerCount > 0 ? 'danger' : ''}">${dangerCount}</span></div>
                                </div>
                            </div>
                            <div class="device-details" id="details-${equipment.id}">
                                <div class="details-row">
                                    <div class="details-label">设备分类：</div>
                                    <div class="details-value">${equipment.category}</div>
                                </div>
                                <div class="details-row">
                                    <div class="details-label">安装位置：</div>
                                    <div class="details-value">${equipment.location || '未指定'}</div>
                                </div>
                                <div class="details-row">
                                    <div class="details-label">设备描述：</div>
                                    <div class="details-value">${equipment.description || '无描述'}</div>
                                </div>
                                <div class="details-row">
                                    <div class="details-label">创建时间：</div>
                                    <div class="details-value">${equipment.createdAt}</div>
                                </div>
                            </div>
                            <div class="sparepart-actions">
                                <button class="btn btn-primary btn-sm" onclick="viewEquipmentSpareparts(${equipment.id})">查看备件</button>
                                <button class="btn btn-danger btn-sm" onclick="deleteEquipment(${equipment.id})">删除设备</button>
                            </div>
                        </div>
                    `;
                });
                
                html += `
                        </div>
                    </div>
                `;
            }
            
            equipmentByCategory.innerHTML = html;
            
            // 添加设备详情切换事件
            document.querySelectorAll('.toggle-details').forEach(button => {
                button.addEventListener('click', function() {
                    const equipmentId = this.getAttribute('data-equipment');
                    const detailsDiv = document.getElementById(`details-${equipmentId}`);
                    const icon = this.querySelector('i');
                    
                    if (detailsDiv.classList.contains('active')) {
                        detailsDiv.classList.remove('active');
                        icon.classList.remove('fa-chevron-up');
                        icon.classList.add('fa-chevron-down');
                    } else {
                        detailsDiv.classList.add('active');
                        icon.classList.remove('fa-chevron-down');
                        icon.classList.add('fa-chevron-up');
                    }
                });
            });
        }
        
        // 查看设备备件
        function viewEquipmentSpareparts(equipmentId) {
            // 切换到备件管理页面
            document.querySelectorAll('.nav-link').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            document.querySelector('[data-page="spareparts"]').classList.add('active');
            document.getElementById('spareparts').classList.add('active');
            
            // 设置筛选器
            document.getElementById('sparepartFilter').value = equipmentId;
            
            // 更新备件显示
            updateSparepartsByDevice();
        }
        
        // 删除设备
        function deleteEquipment(equipmentId) {
            if (!confirm('确定要删除此设备吗？此操作将同时删除该设备的所有备件数据！')) {
                return;
            }
            
            // 查找设备
            const equipment = equipmentData.find(e => e.id === equipmentId);
            if (!equipment) return;
            
            // 删除设备
            equipmentData = equipmentData.filter(e => e.id !== equipmentId);
            
            // 删除该设备的所有备件
            const sparepartsToDelete = sparepartsData.filter(s => s.equipmentId === equipmentId);
            sparepartsToDelete.forEach(sparepart => {
                // 删除相关的领用记录
                recordsData = recordsData.filter(r => r.sparepartId !== sparepart.id);
                // 删除相关的到货记录
                arrivalsData = arrivalsData.filter(a => a.sparepartId !== sparepart.id);
            });
            
            sparepartsData = sparepartsData.filter(s => s.equipmentId !== equipmentId);
            
            saveData();
            updateEquipmentByCategory();
            updateSparepartsByDevice();
            updateAllFilters();
            
            // 如果当前在总览页面，更新总览
            if (document.getElementById('overview').classList.contains('active')) {
                updateDashboard();
            }
        }
        
        // 更新备件按设备分类显示
        function updateSparepartsByDevice() {
            const sparepartsByDevice = document.getElementById('sparepartsByDevice');
            const sparepartFilter = document.getElementById('sparepartFilter').value;
            const categoryFilter = document.getElementById('categoryFilter').value;
            
            // 筛选备件
            let filteredSpareparts = sparepartsData;
            
            // 按设备筛选
            if (sparepartFilter !== 'all') {
                const equipmentId = parseInt(sparepartFilter);
                filteredSpareparts = filteredSpareparts.filter(s => s.equipmentId === equipmentId);
            }
            
            // 按分类筛选
            if (categoryFilter !== 'all') {
                filteredSpareparts = filteredSpareparts.filter(s => s.equipmentCategory === categoryFilter);
            }
            
            if (filteredSpareparts.length === 0) {
                sparepartsByDevice.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-boxes"></i>
                        <p>暂无备件数据，请添加备件。</p>
                    </div>
                `;
                return;
            }
            
            // 按设备分组
            const equipmentGroups = {};
            filteredSpareparts.forEach(sparepart => {
                const key = `${sparepart.equipmentId}_${sparepart.equipmentName}`;
                if (!equipmentGroups[key]) {
                    equipmentGroups[key] = {
                        equipmentId: sparepart.equipmentId,
                        equipmentName: sparepart.equipmentName,
                        equipmentModel: sparepart.equipmentModel,
                        equipmentCategory: sparepart.equipmentCategory,
                        spareparts: []
                    };
                }
                equipmentGroups[key].spareparts.push(sparepart);
            });
            
            let html = '';
            
            // 显示每个设备的备件
            for (const key in equipmentGroups) {
                const group = equipmentGroups[key];
                const warningCount = group.spareparts.filter(s => s.status === 'warning').length;
                const dangerCount = group.spareparts.filter(s => s.status === 'danger').length;
                
                html += `
                    <div class="device-category-section">
                        <div class="device-category-header">
                            <div>
                                <div class="device-category-title">${group.equipmentName} (${group.equipmentModel})</div>
                                <div style="font-size: 14px; color: #718096;">${group.equipmentCategory} · ${group.spareparts.length}个备件</div>
                            </div>
                            <div class="category-summary">
                                <div class="summary-item">
                                    <span class="summary-label">预警备件：</span>
                                    <span class="summary-value ${warningCount > 0 ? 'warning' : ''}">${warningCount}</span>
                                </div>
                                <div class="summary-item">
                                    <span class="summary-label">紧急备件：</span>
                                    <span class="summary-value ${dangerCount > 0 ? 'danger' : ''}">${dangerCount}</span>
                                </div>
                            </div>
                        </div>
                        <div class="spareparts-grid">
                `;
                
                group.spareparts.forEach(sparepart => {
                    const statusClass = sparepart.status === 'danger' ? 'danger' : (sparepart.status === 'warning' ? 'warning' : '');
                    const statusText = sparepart.status === 'danger' ? '紧急' : (sparepart.status === 'warning' ? '预警' : '正常');
                    
                    html += `
                        <div class="sparepart-card ${statusClass}">
                            <div class="sparepart-header">
                                <div>
                                    <div class="sparepart-name">${sparepart.name}</div>
                                    <div class="sparepart-model">${sparepart.model}</div>
                                </div>
                                <span class="inventory-count ${sparepart.status === 'danger' ? 'inventory-low' : 'inventory-normal'}">${statusText}</span>
                            </div>
                            <div class="sparepart-info">
                                <div>
                                    <div>规格：${sparepart.specification || '无'}</div>
                                    <div>单位：${sparepart.unit}</div>
                                </div>
                                <div>
                                    <div class="sparepart-quantity ${sparepart.quantity <= sparepart.warningThreshold ? 'low' : ''}">库存：${sparepart.quantity}${sparepart.unit}</div>
                                    <div>预警：${sparepart.warningThreshold}${sparepart.unit}</div>
                                </div>
                            </div>
                            <div class="sparepart-actions">
                                <button class="btn btn-primary btn-sm" onclick="addRecordForSparepart(${sparepart.id})">领用</button>
                                <button class="btn btn-success btn-sm" onclick="addArrivalForSparepart(${sparepart.id})">到货</button>
                                <button class="btn btn-danger btn-sm" onclick="deleteSparepart(${sparepart.id})">删除</button>
                            </div>
                        </div>
                    `;
                });
                
                html += `
                        </div>
                    </div>
                `;
            }
            
            sparepartsByDevice.innerHTML = html;
        }
        
        // 删除备件
        function deleteSparepart(sparepartId) {
            if (!confirm('确定要删除此备件吗？此操作将同时删除该备件的所有记录！')) {
                return;
            }
            
            // 删除备件
            sparepartsData = sparepartsData.filter(s => s.id !== sparepartId);
            
            // 删除相关的领用记录
            recordsData = recordsData.filter(r => r.sparepartId !== sparepartId);
            
            // 删除相关的到货记录
            arrivalsData = arrivalsData.filter(a => a.sparepartId !== sparepartId);
            
            // 从设备中移除备件引用
            equipmentData.forEach(equipment => {
                equipment.spareparts = equipment.spareparts.filter(id => id !== sparepartId);
            });
            
            saveData();
            updateSparepartsByDevice();
            updateAllFilters();
            
            // 如果当前在总览页面，更新总览
            if (document.getElementById('overview').classList.contains('active')) {
                updateDashboard();
            }
        }
        
        // 为备件快速添加领用记录
        function addRecordForSparepart(sparepartId) {
            // 切换到领用记录页面
            document.querySelectorAll('.nav-link').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            document.querySelector('[data-page="records"]').classList.add('active');
            document.getElementById('records').classList.add('active');
            
            // 查找备件
            const sparepart = sparepartsData.find(s => s.id === sparepartId);
            if (!sparepart) return;
            
            // 设置领用记录表单
            document.getElementById('recordSparepart').value = sparepartId;
            document.getElementById('recordDate').valueAsDate = new Date();
            
            // 显示模态框
            document.getElementById('addRecordModal').style.display = 'flex';
        }
        
        // 为备件快速添加到货记录
        function addArrivalForSparepart(sparepartId) {
            // 切换到到货记录页面
            document.querySelectorAll('.nav-link').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            document.querySelector('[data-page="arrivals"]').classList.add('active');
            document.getElementById('arrivals').classList.add('active');
            
            // 查找备件
            const sparepart = sparepartsData.find(s => s.id === sparepartId);
            if (!sparepart) return;
            
            // 设置到货记录表单
            document.getElementById('arrivalSparepart').value = sparepartId;
            document.getElementById('arrivalDate').valueAsDate = new Date();
            
            // 显示模态框
            document.getElementById('addArrivalModal').style.display = 'flex';
        }
        
        // 更新预警按设备分类显示
        function updateWarningByDevice() {
            const warningByDevice = document.getElementById('warningByDevice');
            const warningFilter = document.getElementById('warningFilter').value;
            const warningStatusFilter = document.getElementById('warningStatusFilter').value;
            
            // 筛选预警备件
            let filteredSpareparts = sparepartsData.filter(s => s.status === 'warning' || s.status === 'danger');
            
            // 按设备筛选
            if (warningFilter !== 'all') {
                const equipmentId = parseInt(warningFilter);
                filteredSpareparts = filteredSpareparts.filter(s => s.equipmentId === equipmentId);
            }
            
            // 按状态筛选
            if (warningStatusFilter !== 'all') {
                filteredSpareparts = filteredSpareparts.filter(s => s.status === warningStatusFilter);
            }
            
            if (filteredSpareparts.length === 0) {
                warningByDevice.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-check-circle"></i>
                        <p>暂无库存预警，所有备件库存充足。</p>
                    </div>
                `;
                
                document.getElementById('warningTotal').textContent = '0';
                document.getElementById('dangerTotal').textContent = '0';
                return;
            }
            
            // 按设备分组
            const equipmentGroups = {};
            filteredSpareparts.forEach(sparepart => {
                const key = `${sparepart.equipmentId}_${sparepart.equipmentName}`;
                if (!equipmentGroups[key]) {
                    equipmentGroups[key] = {
                        equipmentId: sparepart.equipmentId,
                        equipmentName: sparepart.equipmentName,
                        equipmentModel: sparepart.equipmentModel,
                        spareparts: []
                    };
                }
                equipmentGroups[key].spareparts.push(sparepart);
            });
            
            // 计算统计
            const warningCount = filteredSpareparts.filter(s => s.status === 'warning').length;
            const dangerCount = filteredSpareparts.filter(s => s.status === 'danger').length;
            
            document.getElementById('warningTotal').textContent = warningCount + dangerCount;
            document.getElementById('dangerTotal').textContent = dangerCount;
            
            let html = '';
            
            // 显示每个设备的预警备件
            for (const key in equipmentGroups) {
                const group = equipmentGroups[key];
                const warningSpareparts = group.spareparts.filter(s => s.status === 'warning');
                const dangerSpareparts = group.spareparts.filter(s => s.status === 'danger');
                
                html += `
                    <div class="device-category-section">
                        <div class="device-category-header">
                            <div>
                                <div class="device-category-title">${group.equipmentName} (${group.equipmentModel})</div>
                                <div style="font-size: 14px; color: #718096;">${group.spareparts.length}个预警备件</div>
                            </div>
                            <div class="category-summary">
                                <div class="summary-item">
                                    <span class="summary-label">预警备件：</span>
                                    <span class="summary-value ${warningSpareparts.length > 0 ? 'warning' : ''}">${warningSpareparts.length}</span>
                                </div>
                                <div class="summary-item">
                                    <span class="summary-label">紧急备件：</span>
                                    <span class="summary-value ${dangerSpareparts.length > 0 ? 'danger' : ''}">${dangerSpareparts.length}</span>
                                </div>
                            </div>
                        </div>
                        <div class="spareparts-grid">
                `;
                
                group.spareparts.forEach(sparepart => {
                    const statusClass = sparepart.status === 'danger' ? 'danger' : 'warning';
                    const statusText = sparepart.status === 'danger' ? '紧急缺货' : '库存预警';
                    
                    html += `
                        <div class="sparepart-card ${statusClass}">
                            <div class="sparepart-header">
                                <div>
                                    <div class="sparepart-name">${sparepart.name}</div>
                                    <div class="sparepart-model">${sparepart.model}</div>
                                </div>
                                <span class="inventory-count ${statusClass === 'danger' ? 'inventory-low' : ''}">${statusText}</span>
                            </div>
                            <div class="sparepart-info">
                                <div>
                                    <div>当前库存：${sparepart.quantity}${sparepart.unit}</div>
                                    <div>预警阈值：${sparepart.warningThreshold}${sparepart.unit}</div>
                                </div>
                            </div>
                            <div class="sparepart-actions">
                                <button class="btn btn-success btn-sm" onclick="addArrivalForSparepart(${sparepart.id})">补充库存</button>
                                <button class="btn btn-primary btn-sm" onclick="viewSparepartDetails(${sparepart.id})">查看详情</button>
                            </div>
                        </div>
                    `;
                });
                
                html += `
                        </div>
                    </div>
                `;
            }
            
            warningByDevice.innerHTML = html;
        }
        
        // 查看备件详情
        function viewSparepartDetails(sparepartId) {
            // 切换到备件管理页面
            document.querySelectorAll('.nav-link').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            document.querySelector('[data-page="spareparts"]').classList.add('active');
            document.getElementById('spareparts').classList.add('active');
            
            // 设置筛选器
            const sparepart = sparepartsData.find(s => s.id === sparepartId);
            if (sparepart) {
                document.getElementById('sparepartFilter').value = sparepart.equipmentId;
            }
            
            // 更新备件显示
            updateSparepartsByDevice();
        }
        
        // 更新领用记录表格
        function updateRecordsTable() {
            const recordsTableBody = document.getElementById('recordsTableBody');
            const recordFilter = document.getElementById('recordFilter').value;
            const recordDateFilter = document.getElementById('recordDateFilter').value;
            
            // 筛选记录
            let filteredRecords = recordsData;
            
            // 按设备筛选
            if (recordFilter !== 'all') {
                const equipmentId = parseInt(recordFilter);
                filteredRecords = filteredRecords.filter(r => r.equipmentId === equipmentId);
            }
            
            // 按日期筛选
            if (recordDateFilter) {
                const [year, month] = recordDateFilter.split('-');
                filteredRecords = filteredRecords.filter(r => {
                    const recordDate = new Date(r.date);
                    return recordDate.getFullYear() === parseInt(year) && 
                           recordDate.getMonth() + 1 === parseInt(month);
                });
            }
            
            // 计算本月领用统计
            const currentDate = new Date();
            const currentYear = currentDate.getFullYear();
            const currentMonth = currentDate.getMonth() + 1;
            const monthlyRecords = recordsData.filter(r => {
                const recordDate = new Date(r.date);
                return recordDate.getFullYear() === currentYear && 
                       recordDate.getMonth() + 1 === currentMonth;
            });
            
            const monthlyTotal = monthlyRecords.reduce((sum, record) => sum + record.quantity, 0);
            document.getElementById('monthlyRecordTotal').textContent = monthlyTotal;
            
            if (filteredRecords.length === 0) {
                recordsTableBody.innerHTML = '<tr><td colspan="8" style="text-align: center;">暂无领用记录。</td></tr>';
                return;
            }
            
            // 按日期排序，最近的在前
            const sortedRecords = [...filteredRecords].sort((a, b) => new Date(b.date) - new Date(a.date));
            
            let html = '';
            sortedRecords.forEach(record => {
                html += `
                    <tr>
                        <td>${record.date}</td>
                        <td>${record.sparepartName}</td>
                        <td>${record.sparepartModel}</td>
                        <td>${record.equipmentName} (${record.equipmentModel})</td>
                        <td>${record.quantity}${record.unit}</td>
                        <td>${record.person}</td>
                        <td>${record.purpose}</td>
                        <td>${record.remainingQuantity}${record.unit}</td>
                    </tr>
                `;
            });
            
            recordsTableBody.innerHTML = html;
        }
        
        // 更新到货记录表格
        function updateArrivalsTable() {
            const arrivalsTableBody = document.getElementById('arrivalsTableBody');
            const arrivalFilter = document.getElementById('arrivalFilter').value;
            const arrivalDateFilter = document.getElementById('arrivalDateFilter').value;
            
            // 筛选记录
            let filteredArrivals = arrivalsData;
            
            // 按设备筛选
            if (arrivalFilter !== 'all') {
                const equipmentId = parseInt(arrivalFilter);
                filteredArrivals = filteredArrivals.filter(a => a.equipmentId === equipmentId);
            }
            
            // 按日期筛选
            if (arrivalDateFilter) {
                const [year, month] = arrivalDateFilter.split('-');
                filteredArrivals = filteredArrivals.filter(a => {
                    const arrivalDate = new Date(a.date);
                    return arrivalDate.getFullYear() === parseInt(year) && 
                           arrivalDate.getMonth() + 1 === parseInt(month);
                });
            }
            
            // 计算本月到货统计
            const currentDate = new Date();
            const currentYear = currentDate.getFullYear();
            const currentMonth = currentDate.getMonth() + 1;
            const monthlyArrivals = arrivalsData.filter(a => {
                const arrivalDate = new Date(a.date);
                return arrivalDate.getFullYear() === currentYear && 
                       arrivalDate.getMonth() + 1 === currentMonth;
            });
            
            const monthlyTotal = monthlyArrivals.reduce((sum, arrival) => sum + arrival.quantity, 0);
            document.getElementById('monthlyArrivalTotal').textContent = monthlyTotal;
            
            if (filteredArrivals.length === 0) {
                arrivalsTableBody.innerHTML = '<tr><td colspan="7" style="text-align: center;">暂无到货记录。</td></tr>';
                return;
            }
            
            // 按日期排序，最近的在前
            const sortedArrivals = [...filteredArrivals].sort((a, b) => new Date(b.date) - new Date(a.date));
            
            let html = '';
            sortedArrivals.forEach(arrival => {
                html += `
                    <tr>
                        <td>${arrival.date}</td>
                        <td>${arrival.sparepartName}</td>
                        <td>${arrival.sparepartModel}</td>
                        <td>${arrival.equipmentName} (${arrival.equipmentModel})</td>
                        <td>${arrival.quantity}${arrival.unit}</td>
                        <td>${arrival.supplier}</td>
                        <td>${arrival.remainingQuantity}${arrival.unit}</td>
                    </tr>
                `;
            });
            
            arrivalsTableBody.innerHTML = html;
        }
        
        // 更新仪表板
        function updateDashboard() {
            // 更新统计卡片
            document.getElementById('totalEquipment').textContent = equipmentData.length;
            document.getElementById('totalSpareparts').textContent = sparepartsData.length;
            
            const warningCount = sparepartsData.filter(s => s.status === 'warning').length;
            const dangerCount = sparepartsData.filter(s => s.status === 'danger').length;
            document.getElementById('warningCount').textContent = warningCount + dangerCount;
            
            // 计算分类数量
            const categories = [...new Set(equipmentData.map(e => e.category))];
            document.getElementById('categoryCount').textContent = categories.length;
            
            // 更新设备分类概览
            const equipmentOverview = document.getElementById('equipmentOverview');
            
            // 按分类统计设备
            const categoryCount = {};
            equipmentData.forEach(equipment => {
                const category = equipment.category || '未分类';
                categoryCount[category] = (categoryCount[category] || 0) + 1;
            });
            
            if (Object.keys(categoryCount).length === 0) {
                equipmentOverview.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-tools"></i>
                        <p>暂无设备数据，请添加设备。</p>
                    </div>
                `;
                return;
            }
            
            let categoryHtml = '';
            for (const category in categoryCount) {
                const count = categoryCount[category];
                const equipmentInCategory = equipmentData.filter(e => e.category === category);
                
                let sparepartCount = 0;
                let warningSpareparts = 0;
                let dangerSpareparts = 0;
                
                equipmentInCategory.forEach(equipment => {
                    const equipmentSpareparts = sparepartsData.filter(s => s.equipmentId === equipment.id);
                    sparepartCount += equipmentSpareparts.length;
                    warningSpareparts += equipmentSpareparts.filter(s => s.status === 'warning').length;
                    dangerSpareparts += equipmentSpareparts.filter(s => s.status === 'danger').length;
                });
                
                categoryHtml += `
                    <div style="margin-bottom: 15px; padding-bottom: 15px; border-bottom: 1px solid #eee;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <strong>${category}</strong>
                            <span>设备：${count}台 | 备件：${sparepartCount}种</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; font-size: 14px; color: #666;">
                            <span>预警备件：<span class="${warningSpareparts > 0 ? 'warning' : ''}">${warningSpareparts}种</span></span>
                            <span>紧急备件：<span class="${dangerSpareparts > 0 ? 'danger' : ''}">${dangerSpareparts}种</span></span>
                            <a href="#" onclick="viewCategory('${category}')" style="color: #2c5282;">查看详情</a>
                        </div>
                    </div>
                `;
            }
            
            equipmentOverview.innerHTML = categoryHtml;
            
            // 更新预警概览
            const warningOverview = document.getElementById('warningOverview');
            const warningSpareparts = sparepartsData.filter(s => s.status === 'warning' || s.status === 'danger');
            
            if (warningSpareparts.length === 0) {
                warningOverview.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-check-circle"></i>
                        <p>暂无库存预警，所有备件库存充足。</p>
                    </div>
                `;
                return;
            }
            
            // 只显示前5个预警
            const displayCount = Math.min(warningSpareparts.length, 5);
            let warningHtml = '';
            
            for (let i = 0; i < displayCount; i++) {
                const sparepart = warningSpareparts[i];
                const statusText = sparepart.status === 'danger' ? '紧急缺货' : '库存预警';
                const statusClass = sparepart.status === 'danger' ? 'danger' : 'warning';
                
                warningHtml += `
                    <div style="margin-bottom: 12px; padding: 12px; background-color: #fff5f5; border-radius: 6px; display: flex; justify-content: space-between; align-items: center;">
                        <div>
                            <strong>${sparepart.name} (${sparepart.model})</strong>
                            <div style="font-size: 14px; color: #666;">${sparepart.equipmentName} | 库存: <span class="${statusClass}">${sparepart.quantity}${sparepart.unit}</span> / 预警: ${sparepart.warningThreshold}${sparepart.unit}</div>
                        </div>
                        <button class="btn btn-primary btn-sm" onclick="addArrivalForSparepart(${sparepart.id})">补充库存</button>
                    </div>
                `;
            }
            
            if (warningSpareparts.length > 5) {
                warningHtml += `<p style="text-align: center; margin-top: 10px;">还有 ${warningSpareparts.length - 5} 个预警备件...</p>`;
            }
            
            warningOverview.innerHTML = warningHtml;
        }
        
        // 查看分类详情
        function viewCategory(category) {
            // 切换到设备管理页面
            document.querySelectorAll('.nav-link').forEach(item => item.classList.remove('active'));
            document.querySelectorAll('.page').forEach(page => page.classList.remove('active'));
            
            document.querySelector('[data-page="equipment"]').classList.add('active');
            document.getElementById('equipment').classList.add('active');
            
            // 设置筛选器
            document.getElementById('equipmentFilter').value = `category_${category}`;
            
            // 更新设备显示
            updateEquipmentByCategory();
        }
        
        // 更新月度检修页面
        function updateMaintenancePage() {
            const maintenancePlans = document.getElementById('maintenancePlans');
            const maintenanceSummary = document.getElementById('maintenanceSummary');
            
            // 显示月度检修计划
            if (maintenanceData.length === 0) {
                maintenancePlans.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-calendar-alt"></i>
                        <p>暂无检修计划，请创建新的检修计划。</p>
                    </div>
                `;
                maintenanceSummary.innerHTML = `
                    <div class="empty-state">
                        <i class="fas fa-clipboard-list"></i>
                        <p>暂无检修备件需求。</p>
                    </div>
                `;
                return;
            }
            
            // 按月份排序，最近的在前
            const sortedMaintenance = [...maintenanceData].sort((a, b) => b.month.localeCompare(a.month));
            
            let plansHtml = '';
            sortedMaintenance.forEach(plan => {
                const statusText = plan.status === 'pending' ? '待准备' : (plan.status === 'inprogress' ? '进行中' : '已完成');
                const statusClass = plan.status === 'pending' ? 'warning' : (plan.status === 'inprogress' ? 'orange' : 'success');
                
                plansHtml += `
                    <div style="margin-bottom: 20px; padding: 20px; border: 1px solid #e2e8f0; border-radius: 8px;">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                            <div>
                                <h4 style="margin: 0;">${plan.planName}</h4>
                                <div style="color: #666; font-size: 14px;">月份: ${plan.month}</div>
                            </div>
                            <div>
                                <span class="${statusClass}" style="padding: 5px 12px; border-radius: 20px; font-size: 14px; font-weight: 600;">${statusText}</span>
                                <button class="btn btn-primary btn-sm" onclick="editMaintenancePlan(${plan.id})" style="margin-left: 10px;">编辑</button>
                            </div>
                        </div>
                        <div>
                            <strong>涉及设备:</strong>
                            <div style="margin-top: 8px;">
                `;
                
                // 显示涉及的设备
                plan.equipmentIds.forEach(equipmentId => {
                    const equipment = equipmentData.find(e => e.id === equipmentId);
                    if (equipment) {
                        plansHtml += `<span style="display: inline-block; background-color: #edf2f7; padding: 5px 10px; border-radius: 4px; margin-right: 8px; margin-bottom: 8px;">${equipment.name} (${equipment.model})</span>`;
                    }
                });
                
                plansHtml += `
                            </div>
                        </div>
                    </div>
                `;
            });
            
            maintenancePlans.innerHTML = plansHtml;
            
            // 显示检修备件需求汇总（按设备分类）
            let summaryHtml = '';
            
            // 汇总所有检修计划的备件需求
            const sparepartRequirements = {};
            const equipmentRequirements = {};
            
            maintenanceData.forEach(plan => {
                if (plan.status !== 'completed') {
                    plan.equipmentIds.forEach(equipmentId => {
                        if (!equipmentRequirements[equipmentId]) {
                            equipmentRequirements[equipmentId] = {};
                        }
                    });
                    
                    plan.sparepartRequirements.forEach(req => {
                        const sparepart = sparepartsData.find(s => s.id === req.sparepartId);
                        if (sparepart) {
                            const key = `${sparepart.equipmentId}_${req.sparepartId}`;
                            if (!sparepartRequirements[key]) {
                                sparepartRequirements[key] = {
                                    sparepart: sparepart,
                                    quantity: 0,
                                    planCount: 0
                                };
                            }
                            sparepartRequirements[key].quantity += req.quantity;
                            sparepartRequirements[key].planCount += 1;
                            
                            // 添加到设备需求
                            if (!equipmentRequirements[sparepart.equipmentId]) {
                                equipmentRequirements[sparepart.equipmentId] = {};
                            }
                            equipmentRequirements[sparepart.equipmentId][req.sparepartId] = true;
                        }
                    });
                }
            });
            
            // 按设备显示需求汇总
            let hasRequirements = false;
            
            for (const equipmentId in equipmentRequirements) {
                const equipment = equipmentData.find(e => e.id === parseInt(equipmentId));
                if (!equipment) continue;
                
                // 获取该设备的所有需求备件
                const equipmentSparepartIds = Object.keys(equipmentRequirements[equipmentId]);
                if (equipmentSparepartIds.length === 0) continue;
                
                hasRequirements = true;
                
                summaryHtml += `
                    <div class="device-category-section" style="margin-bottom: 20px;">
                        <div class="device-category-header">
                            <div class="device-category-title">${equipment.name} (${equipment.model})</div>
                            <div class="category-summary">
                                <div class="summary-item">
                                    <span class="summary-label">需求备件：</span>
                                    <span class="summary-value">${equipmentSparepartIds.length}种</span>
                                </div>
                            </div>
                        </div>
                        <div style="overflow-x: auto;">
                            <table style="width: 100%; border-collapse: collapse;">
                                <thead>
                                    <tr>
                                        <th style="padding: 12px 15px; text-align: left; border-bottom: 1px solid #e2e8f0;">备件名称</th>
                                        <th style="padding: 12px 15px; text-align: left; border-bottom: 1px solid #e2e8f0;">备件型号</th>
                                        <th style="padding: 12px 15px; text-align: left; border-bottom: 1px solid #e2e8f0;">需求数量</th>
                                        <th style="padding: 12px 15px; text-align: left; border-bottom: 1px solid #e2e8f0;">当前库存</th>
                                        <th style="padding: 12px 15px; text-align: left; border-bottom: 1px solid #e2e8f0;">状态</th>
                                    </tr>
                                </thead>
                                <tbody>
                `;
                
                equipmentSparepartIds.forEach(sparepartIdStr => {
                    const sparepartId = parseInt(sparepartIdStr);
                    const requirement = sparepartRequirements[`${equipmentId}_${sparepartId}`];
                    if (requirement) {
                        const sparepart = requirement.sparepart;
                        const status = sparepart.quantity >= requirement.quantity ? '库存充足' : '库存不足';
                        const statusClass = sparepart.quantity >= requirement.quantity ? 'success' : 'danger';
                        
                        summaryHtml += `
                            <tr>
                                <td style="padding: 12px 15px; border-bottom: 1px solid #e2e8f0;">${sparepart.name}</td>
                                <td style="padding: 12px 15px; border-bottom: 1px solid #e2e8f0;">${sparepart.model}</td>
                                <td style="padding: 12px 15px; border-bottom: 1px solid #e2e8f0;">${requirement.quantity}${sparepart.unit}</td>
                                <td style="padding: 12px 15px; border-bottom: 1px solid #e2e8f0;">${sparepart.quantity}${sparepart.unit}</td>
                                <td style="padding: 12px 15px; border-bottom: 1px solid #e2e8f0;" class="${statusClass}">${status}</td>
                            </tr>
                        `;
                    }
                });
                
                summaryHtml += `
                                </tbody>
                            </table>
                        </div>
                    </div>
                `;
            }
            
            if (!hasRequirements) {
                summaryHtml = `
                    <div class="empty-state">
                        <i class="fas fa-clipboard-list"></i>
                        <p>暂无检修备件需求。</p>
                    </div>
                `;
            }
            
            maintenanceSummary.innerHTML = summaryHtml;
        }
        
        // 编辑检修计划
        function editMaintenancePlan(planId) {
            alert('检修计划编辑功能正在开发中...');
        }
    </script>
</body>
</html>
