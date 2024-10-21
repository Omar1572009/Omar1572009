<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>روبوت الطالب عمر</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .chat-container {
            background-color: #fff;
            width: 400px;
            max-width: 100%;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            overflow: hidden;
        }
        .chat-header {
            background-color: #007bff;
            padding: 15px;
            text-align: center;
            color: #fff;
            font-size: 20px;
        }
        .chat-body {
            padding: 15px;
            height: 400px;
            overflow-y: auto;
            background-color: #f9f9f9;
        }
        .chat-message {
            margin-bottom: 10px;
            display: flex;
            justify-content: flex-start;
        }
        .chat-message.bot {
            justify-content: flex-start;
        }
        .chat-message.user {
            justify-content: flex-end;
        }
        .chat-message .message {
            max-width: 70%;
            padding: 10px;
            border-radius: 10px;
        }
        .chat-message.bot .message {
            background-color: #007bff;
            color: #fff;
        }
        .chat-message.user .message {
            background-color: #ccc;
        }
        .chat-footer {
            padding: 10px;
            background-color: #fff;
            display: flex;
            justify-content: space-between;
        }
        .chat-footer input {
            width: 85%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .chat-footer button {
            padding: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<div class="chat-container">
    <div class="chat-header">روبوت الطالب عمر</div>
    <div class="chat-body" id="chat-body">
        <!-- رسائل الدردشة -->
    </div>
    <div class="chat-footer">
        <input type="text" id="user-input" placeholder="اكتب رسالتك هنا..." onkeydown="handleKey(event)">
        <button onclick="sendMessage()">إرسال</button>
    </div>
</div>

<script>
    const arabCountriesCount = 22;
    const totalCountries = 195;
    const arabCapitals = {
        "مصر": "القاهرة",
        "السعودية": "الرياض",
        "الجزائر": "الجزائر",
        "العراق": "بغداد",
        "السودان": "الخرطوم",
        "المغرب": "الرباط",
        "اليمن": "صنعاء",
        "سوريا": "دمشق",
        "تونس": "تونس",
        "الصومال": "مقديشو",
        "الأردن": "عمان",
        "الإمارات": "أبو ظبي",
        "ليبيا": "طرابلس",
        "فلسطين": "القدس",
        "لبنان": "بيروت",
        "عمان": "مسقط",
        "الكويت": "مدينة الكويت",
        "موريتانيا": "نواكشوط",
        "البحرين": "المنامة",
        "قطر": "الدوحة",
        "جيبوتي": "جيبوتي",
        "جزر القمر": "موروني"
    };

    function handleKey(event) {
        if (event.key === "Enter") {
            event.preventDefault(); // منع إعادة تحميل الصفحة
            sendMessage();
        }
    }

    function sendMessage() {
        const userInput = document.getElementById('user-input').value.trim();
        const chatBody = document.getElementById('chat-body');

        if (!userInput) return;

        // إضافة رسالة المستخدم إلى واجهة الدردشة
        const userMessage = document.createElement('div');
        userMessage.classList.add('chat-message', 'user');
        userMessage.innerHTML = `<div class="message">${userInput}</div>`;
        chatBody.appendChild(userMessage);

        // تمرير الصفحة إلى الأسفل تلقائياً
        chatBody.scrollTop = chatBody.scrollHeight;

        // استجابة الروبوت
        setTimeout(() => {
            const botMessage = document.createElement('div');
            botMessage.classList.add('chat-message', 'bot');

            let response = '';

            if (userInput.toLowerCase() === 'السلام عليكم') {
                response = 'وعليكم السلام!';
            } else if (userInput.toLowerCase().includes('كيف حالك')) {
                response = 'أنا بخير، شكرًا لسؤالك!';
            } else if (userInput.toLowerCase().includes('عدد الدول العربية')) {
                response = `عدد الدول العربية هو ${arabCountriesCount}.`;
            } else if (userInput.toLowerCase().includes('عدد دول العالم')) {
                response = `عدد دول العالم هو ${totalCountries}.`;
            } else if (userInput.toLowerCase().includes('من الذي صنعك')) {
                response = 'صنعني الطالب عمر أحمد.';
            } else if (userInput.toLowerCase().includes('من هو عمر أحمد')) {
                response = 'هو طالب ثانوي عام في مدرسة أسوان الجديدة الثانوي.';
            } else if (userInput.toLowerCase().includes('ما هي عاصمة') || userInput.toLowerCase().includes('عاصمة') || userInput.toLowerCase().includes('ما هي عاصمة دولة')) {
                const country = userInput.replace(/ما هي عاصمة(?: دولة)? |عاصمة /, '').trim();
                if (country && arabCapitals[country]) {
                    response = `عاصمة دولة ${country} هي ${arabCapitals[country]}.`;
                } else {
                    response = 'عذرًا، لم أفهم السؤال أو الدولة غير متاحة.';
                }
            } else {
                response = 'عذرًا، لم أفهم السؤال.';
            }

            botMessage.innerHTML = `<div class="message">${response}</div>`;
            chatBody.appendChild(botMessage);
            chatBody.scrollTop = chatBody.scrollHeight;
        }, 500);

        // إعادة تعيين الحقل بعد الإرسال
        document.getElementById('user-input').value = '';
    }
</script>

</body>
</html>