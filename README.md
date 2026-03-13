<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>毕设提交 · 学生自助 + 负责人隐私面板</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, system-ui, sans-serif;
        }
        body {
            background: #e7eef7;
            margin: 0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .app-container {
            max-width: 1300px;
            width: 100%;
        }

        /* ---------- 公共提交区 ---------- */
        .public-submit {
            background: white;
            border-radius: 40px 40px 30px 30px;
            padding: 28px 32px 32px;
            margin-bottom: 28px;
            box-shadow: 0 15px 30px rgba(0,30,60,0.12);
            border: 1px solid #b9d5fd;
        }
        .public-submit h2 {
            font-size: 2rem;
            font-weight: 650;
            margin: 0 0 8px;
            color: #113355;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .public-submit h2::before {
            content: "📮";
            font-size: 2rem;
        }
        .public-desc {
            color: #2a4f70;
            margin: 5px 0 25px;
            font-size: 1.15rem;
            border-left: 5px solid #2b82d9;
            padding-left: 20px;
            background: #e8f1fe;
            border-radius: 0 40px 40px 0;
            line-height: 1.5;
            width: fit-content;
            padding: 12px 30px;
        }
        .submit-form {
            display: flex;
            gap: 16px;
            flex-wrap: wrap;
            align-items: center;
            margin: 28px 0 16px;
        }
        #studentNameInput {
            flex: 2 1 280px;
            padding: 18px 28px;
            font-size: 1.2rem;
            border: 2px solid #b0caec;
            border-radius: 60px;
            outline: none;
            transition: 0.2s;
            background: #f6faff;
        }
        #studentNameInput:focus {
            border-color: #1e6bc7;
            box-shadow: 0 0 0 4px rgba(30,107,199,0.2);
        }
        #submitNameBtn {
            flex: 0 1 auto;
            background: #1f6c46;
            color: white;
            border: none;
            padding: 18px 38px;
            font-size: 1.2rem;
            font-weight: 600;
            border-radius: 60px;
            cursor: pointer;
            box-shadow: 0 10px 18px #1f6c4660;
            transition: 0.15s;
            border: 2px solid #1e8b3a;
        }
        #submitNameBtn:hover {
            background: #118c4a;
            transform: scale(1.02);
        }
        .submit-message {
            min-height: 50px;
            font-size: 1.1rem;
            color: #1e3b5e;
            background: #e2f0fa;
            border-radius: 40px;
            padding: 14px 28px;
            margin: 20px 0 15px;
            border-left: 8px solid #328fdc;
        }
        .public-summary {
            background: #ecf3fb;
            border-radius: 50px;
            padding: 12px 28px;
            font-size: 1.2rem;
            color: #103459;
            font-weight: 500;
            display: inline-block;
        }
        .public-summary span {
            font-weight: 700;
            font-size: 1.6rem;
            background: #2966a3;
            color: white;
            padding: 4px 18px;
            border-radius: 40px;
            margin-left: 12px;
        }

        /* ---------- 负责人隐私区 ---------- */
        .private-section {
            background: #dbe6f2;
            border-radius: 40px;
            box-shadow: 0 20px 35px rgba(0,25,55,0.3);
            border: 3px solid #31578b;
            overflow: hidden;
            backdrop-filter: blur(2px);
        }
        .private-header {
            background: #1f3b5c;
            color: white;
            padding: 18px 32px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 20px;
        }
        .private-header h3 {
            font-size: 1.8rem;
            margin: 0;
            font-weight: 550;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .private-header h3::before {
            content: "🔒";
            font-size: 2rem;
        }
        .lock-toggle-area {
            display: flex;
            align-items: center;
            gap: 16px;
        }
        #unlockBtn, #lockBtn {
            background: white;
            border: none;
            padding: 14px 34px;
            border-radius: 50px;
            font-weight: 600;
            font-size: 1.1rem;
            cursor: pointer;
            transition: 0.1s;
            box-shadow: 0 5px 12px rgba(0,0,0,0.25);
            border: 2px solid #9dc0f0;
        }
        #unlockBtn {
            background: #f6d758;
            color: #1e3b5e;
        }
        #lockBtn {
            background: #bccfe6;
            color: #192e46;
        }
        #unlockBtn:hover { background: #ffc107; }
        #lockBtn:hover { background: #a5bbd9; }

        .password-box {
            display: flex;
            gap: 10px;
            align-items: center;
            background: #2f5075;
            padding: 8px 20px;
            border-radius: 50px;
        }
        .password-box input {
            padding: 12px 16px;
            border-radius: 40px;
            border: none;
            width: 220px;
            font-size: 1.1rem;
            background: #ebf3ff;
            border: 2px solid #95b6e3;
        }
        .password-box button {
            background: #92b9f2;
            border: none;
            padding: 12px 24px;
            border-radius: 40px;
            font-weight: 600;
            cursor: pointer;
            font-size: 1rem;
        }
        .password-box button:hover { background: #b3d0ff; }
        .password-error {
            color: #ffb9a7;
            margin-left: 16px;
            font-weight: 500;
        }

        /* 隐私内容区域 (默认隐藏) */
        .private-content {
            padding: 28px 28px 20px;
            background: white;
            transition: all 0.2s;
        }
        .grid-3 {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 24px;
            margin: 22px 0 28px;
        }
        .group-card {
            background: white;
            border-radius: 28px;
            padding: 0 0 18px 0;
            box-shadow: 0 8px 20px rgba(0,20,50,0.08);
            border: 1px solid rgba(59,130,246,0.15);
            transition: transform 0.1s ease;
        }
        .group-card:hover {
            box-shadow: 0 18px 30px -8px rgba(0,80,160,0.2);
        }
        .group-header {
            background: linear-gradient(145deg, #f9fcff, #eef4fe);
            padding: 20px 22px 14px 22px;
            border-radius: 28px 28px 24px 24px;
            border-bottom: 2px dashed #a9c9fa;
        }
        .group-name {
            font-size: 1.8rem;
            font-weight: 650;
            color: #0c2b4f;
            display: flex;
            justify-content: space-between;
            align-items: center;
            letter-spacing: -0.01em;
        }
        .teacher-badge {
            background: #1e4f8a;
            color: white;
            padding: 8px 20px;
            border-radius: 40px;
            font-size: 0.9rem;
            font-weight: 500;
            box-shadow: 0 4px 8px #1e4f8a40;
        }
        .teacher-info {
            font-size: 1.2rem;
            font-weight: 400;
            margin-top: 6px;
            color: #2e4b74;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .teacher-info i {
            font-size: 1.4rem;
            color: #3b82f6;
        }
        .progress-badge {
            margin-top: 14px;
            background: #d9e9ff;
            border-radius: 30px;
            padding: 10px 14px;
            font-weight: 550;
            color: #10355e;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }
        .student-list {
            padding: 10px 16px 8px 16px;
        }
        .student-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px 12px 12px 20px;
            margin: 8px 0;
            background: #fafcff;
            border-radius: 60px;
            border: 1px solid #dde7f5;
            transition: all 0.15s;
        }
        .student-row:hover {
            background: #eef5ff;
            border-color: #80b4ff;
        }
        .student-name {
            font-weight: 550;
            color: #1f2e4e;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .student-name::before {
            content: "👤";
            font-size: 0.95rem;
            opacity: 0.9;
        }
        .toggle-submit {
            appearance: none;
            background: #e9ecf3;
            width: 64px;
            height: 32px;
            border-radius: 40px;
            position: relative;
            cursor: pointer;
            transition: 0.2s;
            border: 2px solid #b3c7e3;
            outline: none;
            box-shadow: inset 0 1px 4px #0000001a;
        }
        .toggle-submit:checked {
            background: #1c8b3c;
            border-color: #0f6b2c;
        }
        .toggle-submit::after {
            content: "未交";
            position: absolute;
            top: 4px;
            left: 8px;
            font-size: 0.7rem;
            font-weight: bold;
            color: #2e405b;
            text-transform: uppercase;
            transition: 0
